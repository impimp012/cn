# Experiment 14 (manual item 5): Implement Dynamic Routing Protocols RIP and IGRP

*(Listed in your lab manual; not in your handwritten file or the crash-course PDF. Write it up in the same format as the others.)*

## Aim
To implement the dynamic routing protocols RIP and IGRP using Cisco Packet Tracer.

## Theory
**Routing** moves packets between different networks. A router learns routes in three ways: **connected** (its own interfaces), **static** (typed by the administrator, Exp 10) and **dynamic** (learnt automatically by a **routing protocol**). In dynamic routing the routers exchange information with neighbours, build the routing table themselves and **adapt when a link or router fails**. It suits large and changing networks; disadvantages are CPU, memory and bandwidth use for updates, and lower security than static routes.

**Classification:**
- **IGP (interior)** run inside one autonomous system: RIP, IGRP, EIGRP, OSPF, IS-IS. **EGP (exterior)** between autonomous systems: BGP.
- By algorithm: **distance vector** (RIP, IGRP; EIGRP is advanced distance vector) and **link state** (OSPF, IS-IS). Distance vector: routers share distance information with their neighbours; RIP uses hop count.
- **Classful** (no mask in updates: RIPv1, IGRP) and **classless** (mask sent, VLSM/CIDR: RIPv2, EIGRP, OSPF).
- **Metric:** value used to choose the best path (hop count, bandwidth, delay, cost). **Administrative distance (AD):** trustworthiness of the route source, lower is better: connected 0, static 1, EIGRP 90, IGRP 100, OSPF 110, RIP 120.
- **Convergence:** all routers have the same, correct view of the network.

### RIP (Routing Information Protocol)
- **Distance vector**; metric = **hop count**. **Maximum 15 hops; 16 = unreachable**, so only for small networks.
- Each router sends its **whole routing table to neighbours every 30 s** over **UDP port 520**. Timers: update 30 s, invalid 180 s, hold-down 180 s, flush 240 s.
- Bellman-Ford algorithm; best path = fewest hops regardless of bandwidth.
- Loop prevention: **split horizon, route poisoning (poison reverse), hold-down timers, triggered updates, max hop count**. Count-to-infinity problem.
- Equal-cost load balancing up to 4 paths; AD = 120.
- **RIPv1:** classful, broadcast updates (255.255.255.255), no mask, no authentication. **RIPv2:** classless, multicast **224.0.0.9**, authentication, summarization. RIPng is for IPv6.

### IGRP (Interior Gateway Routing Protocol)
- **Cisco-proprietary distance vector**, created to overcome RIP's 15-hop limit.
- **Composite metric** from bandwidth, delay, reliability, load and MTU; by default only **bandwidth and delay**.
- Updates every **90 s**; max hops 255 (default 100); **AD = 100**; needs an **AS number** matching on all routers; **classful** (no VLSM); runs directly over IP (protocol 9).
- **Obsolete:** removed from IOS 12.3 and replaced by **EIGRP**. Newer Packet Tracer versions may not accept `router igrp`. If yours does not, tell the examiner and show the same topology with RIP and EIGRP instead.

| Point | RIP | IGRP |
|---|---|---|
| Type | distance vector, open standard | distance vector, Cisco proprietary |
| Metric | hop count | bandwidth, delay, reliability, load, MTU |
| Max hops | 15 | 255 (default 100) |
| Update timer | 30 s | 90 s |
| Admin distance | 120 | 100 |
| Classful / classless | v1 classful, v2 classless | classful |
| AS number | no | yes |
| Transport | UDP 520 | IP protocol 9 |

## Topology and addressing (same as Exp 13)
```
PC0 ─ SW0 ─ R0 ═ R1 ═ R2 ─ SW2 ─ PC2
                  │
                 SW1 ─ PC1
```
| Device | Interface | IP address |
|---|---|---|
| R0 | G0/0 | 192.168.1.1/24 |
| R0 | G0/1 | 10.0.12.1/24 |
| R1 | G0/0 | 192.168.2.1/24 |
| R1 | G0/1 | 10.0.12.2/24 |
| R1 | G0/2 | 10.0.23.1/24 |
| R2 | G0/0 | 192.168.3.1/24 |
| R2 | G0/1 | 10.0.23.2/24 |
| PC0 / PC1 / PC2 | NIC | 192.168.1.10, 192.168.2.10, 192.168.3.10 (gateway = their router's G0/0) |

## Procedure
1. Open Cisco Packet Tracer.
2. Place three routers (2911, since R1 needs three gigabit ports), three switches and three PCs.
3. Connect each PC to its switch and each switch to its router's G0/0 with straight-through cables. Connect routers with cross-over cables (R0 G0/1 to R1 G0/1, R1 G0/2 to R2 G0/1).
4. Configure the IP address of every router interface and `no shutdown`.
5. Configure IP, mask and default gateway on every PC.
6. Configure the routing protocol on each router (below).
7. Verify with `show ip route`, `show ip protocols`, and ping from PC0 to PC2.
8. Optional: shut down a link and watch the routes change and recover (shows the benefit of dynamic routing).

**RIP (version 2):**
```
R0(config)# router rip
R0(config-router)# version 2
R0(config-router)# network 192.168.1.0
R0(config-router)# network 10.0.12.0
R0(config-router)# no auto-summary

R1(config)# router rip
R1(config-router)# version 2
R1(config-router)# network 192.168.2.0
R1(config-router)# network 10.0.12.0
R1(config-router)# network 10.0.23.0
R1(config-router)# no auto-summary

R2(config)# router rip
R2(config-router)# version 2
R2(config-router)# network 192.168.3.0
R2(config-router)# network 10.0.23.0
R2(config-router)# no auto-summary
```
The `network` command lists the directly connected classful networks to advertise and the interfaces on which RIP runs. `no auto-summary` stops summarizing at classful boundaries.

**IGRP (if supported):** first `no router rip`, then:
```
R0(config)# router igrp 100
R0(config-router)# network 192.168.1.0
R0(config-router)# network 10.0.0.0

R1(config)# router igrp 100
R1(config-router)# network 192.168.2.0
R1(config-router)# network 10.0.0.0

R2(config)# router igrp 100
R2(config-router)# network 192.168.3.0
R2(config-router)# network 10.0.0.0
```
100 is the AS number and must match on all routers. IGRP is classful, so give full class A/B/C networks (10.0.0.0).

## Verification and expected output
- `show ip route`: RIP routes marked **R**, e.g. `R 192.168.3.0/24 [120/2] via 10.0.12.2, GigabitEthernet0/1` (120 = AD, 2 = hops). IGRP routes marked **I** with `[100/metric]`.
- `show ip protocols`: protocol, timers (update 30 s), networks, routing information sources.
- `debug ip rip` shows updates (`undebug all` to stop).
- `ping 192.168.3.10` from PC0: four replies (the first may time out while ARP and convergence settle).

## Result
Dynamic routing protocols RIP (and IGRP) were implemented on a multi-router network and connectivity between all networks was verified.

## Viva
- Static vs dynamic routing; distance vector vs link state.
- RIP metric, max hops (15), update time (30 s), AD (120), port (UDP 520).
- Difference between RIPv1 and RIPv2.
- Why IGRP is obsolete and what replaced it (EIGRP).
- What does `no auto-summary` do? Why does `network` take classful networks in RIP?
