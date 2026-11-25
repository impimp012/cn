# Experiment 13: Construct a Multiple-Router Network and Implement EIGRP

## Aim
To construct a multiple router network and implement the Enhanced Interior Gateway Routing Protocol (EIGRP).

## Theory
EIGRP is a dynamic routing protocol developed by Cisco. It is used to exchange routing information between routers and automatically determine the best path. EIGRP uses a composite metric based primarily on **bandwidth and delay** by default. The problem it solves: with 3 routers (LAN1 - R0 - R1 - R2 - LAN2) you do not want to configure every route by hand; routers should learn networks automatically.

**More detail for the viva:**
- Advanced distance-vector (hybrid) protocol using **DUAL (Diffusing Update Algorithm)** to compute loop-free paths and converge fast.
- Default metric uses bandwidth and delay (K1 = K3 = 1); load and reliability are off by default.
- **Administrative distance 90** (internal routes): lower than RIP (120) and OSPF (110), higher than static (1).
- Hello packets use multicast **224.0.0.10**; neighbours must share the same **autonomous system (AS) number** and K values.
- Keeps three tables: **neighbor table**, **topology table**, **routing table**.
- **Successor** = best route; **feasible successor** = loop-free backup.
- Sends partial, triggered updates; supports VLSM/CIDR and unequal-cost load balancing.
- Dynamic routing needs less manual work than static routing and adapts to failures.

## Topology
```
PC0 ─ SW0 ─ R0 ═ R1 ═ R2 ─ SW2 ─ PC2
                  │
                 SW1 ─ PC1
```

## IP addressing table (your file)
| Device | Interface | IP address |
|---|---|---|
| Router0 | G0/0 | 192.168.1.1 |
| Router0 | G0/1 | 10.0.12.1 |
| Router1 | G0/0 | 192.168.2.1 |
| Router1 | G0/1 | 10.0.12.2 |
| Router1 | G0/2 | 10.0.23.1 |
| Router2 | G0/0 | 192.168.3.1 |
| Router2 | G0/1 | 10.0.23.2 |
| PC0 | NIC | 192.168.1.10 |
| PC1 | NIC | 192.168.2.10 |
| PC2 | NIC | 192.168.3.10 |
Router1 needs three gigabit interfaces, so use a 2911 (the 1941 has two). PC gateways = the G0/0 of their router. Interface names depend on the router model you pick.

**Simpler version from the crash-course PDF (2 PCs, 3 routers in a line):** PC0 192.168.1.10; R0 G0/0 192.168.1.1/24, G0/1 10.0.0.1/30; R1 G0/0 10.0.0.2/30, G0/1 10.0.0.5/30; R2 G0/1 10.0.0.6/30, G0/0 192.168.2.1/24; PC1 192.168.2.10.

## Procedure as written in your file
1. Open Cisco Packet Tracer.
2. Place three routers, three switches and three PCs in the workspace.
3. Connect each PC to its respective switch.
4. Connect each switch to its router.
5. Connect Router0 to Router1 and Router1 to Router2.
6. Configure the IP address on all router interfaces and enable them using `no shutdown`.
7. Configure the IP addresses and default gateways on all PCs.
8. Verify EIGRP using `show ip eigrp neighbors`.
9. Check the routing table: `show ip route`.

## Commands
Cables: PC to switch and switch to router G0/0 straight-through; router to router copper cross-over. On each router: `interface g0/x`, `ip address ... mask`, `no shutdown`.

**EIGRP configuration (your file's addressing):**
```
R0(config)# router eigrp 100
R0(config-router)# network 192.168.1.0
R0(config-router)# network 10.0.12.0
R0(config-router)# no auto-summary

R1(config)# router eigrp 100
R1(config-router)# network 192.168.2.0
R1(config-router)# network 10.0.12.0
R1(config-router)# network 10.0.23.0
R1(config-router)# no auto-summary

R2(config)# router eigrp 100
R2(config-router)# network 192.168.3.0
R2(config-router)# network 10.0.23.0
R2(config-router)# no auto-summary
```
**PDF version:** R0: `router eigrp 100`, `network 192.168.1.0`, `network 10.0.0.0`, `no auto-summary`; R1: `router eigrp 100`, `network 10.0.0.0`, `no auto-summary`; R2: `router eigrp 100`, `network 192.168.2.0`, `network 10.0.0.0`, `no auto-summary`.
The **AS number (100)** must match on all routers.

## Verification and expected output
- `show ip eigrp neighbors`: lists neighbouring routers (R0 sees 10.0.12.2; R1 sees 10.0.12.1 and 10.0.23.2).
- `show ip route`: `D` entries (EIGRP-learned), e.g. `D 192.168.3.0/24 [90/...] via 10.0.12.2`, and `C` for connected networks.
- PC0: `ping 192.168.3.10` (or 192.168.2.10 in the PDF version): replies. Successful replies prove connectivity through the routers.
- No neighbours? Check `no shutdown`, matching AS number, and that `network` statements match the connected subnets.

## Result
Successfully implemented the EIGRP dynamic routing protocol in a multiple-router network using Cisco Packet Tracer.

## Viva
- **What is EIGRP?** Dynamic routing protocol that exchanges routing information between routers.
- **What does DUAL do?** Computes loop-free routes and supports fast convergence.
- **What is the AS number?** Identifies the EIGRP process/group; routers must match to become neighbours.
- **How to see EIGRP routes?** `show ip route`, look for `D`.
- **Static routing vs EIGRP?** Static is manual; EIGRP exchanges route information automatically.
- Successor vs feasible successor; administrative distance (90).
