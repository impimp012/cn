# Experiment 10: Implement Static Routing

## Aim
To implement static routing using Cisco Packet Tracer.

## Theory
**Routing** is the process of selecting the path along which packets travel from a source network to a destination network. A router decides using its **routing table**. A router automatically knows only its **directly connected** networks; for remote networks it needs a route.

**Static routing:** the network administrator manually configures routes in the routing table of a router. A static route specifies:
- the **destination network**,
- the **subnet mask**,
- the **next-hop IP address** (or exit interface).

Static routing suits small networks where the topology does not change frequently.

- **Advantages:** simple, no routing-protocol overhead (CPU/bandwidth), more secure, predictable.
- **Disadvantages:** manual work grows with network size, does not adapt to link failures, easy to make errors.
- **Administrative distance** of a static route = 1 (connected 0, EIGRP 90, OSPF 110, RIP 120).
- **Next hop:** the next router/interface to which a packet should be forwarded.
- Routes are needed on **both** routers: the forward path must exist and the destination network must also know how to return traffic to the source; otherwise the packet arrives but the reply is lost and the ping fails.

**Command:** `ip route <destination-network> <subnet-mask> <next-hop>`
Example: `ip route 192.168.2.0 255.255.255.0 10.0.0.2` means "to reach 192.168.2.0/24, forward packets to next-hop router 10.0.0.2."

## Topology
```
LAN-A                                   LAN-B
PC0 ─ Switch0 ─ Router0 ═══════ Router1 ─ Switch1 ─ PC1
```
Router-to-router link: copper cross-over (similar devices), G0/1 to G0/1.

## IP addressing table (your file)
| Device | Interface | IP address |
|---|---|---|
| Router0 | G0/0 | 192.168.1.1 |
| Router0 | G0/1 | 10.0.0.1 |
| Router1 | G0/0 | 192.168.2.1 |
| Router1 | G0/1 | 10.0.0.2 |
| PC0 | NIC | 192.168.1.10 (gateway 192.168.1.1) |
| PC1 | NIC | 192.168.2.10 (gateway 192.168.2.1) |

(The crash-course PDF uses 10.0.0.1/30 and 10.0.0.2/30 for the router link, mask 255.255.255.252. Either mask works if both routers use the same.)

## Procedure as written in your file
1. Open Cisco Packet Tracer.
2. Place two routers, two switches and two PCs.
3. Connect each PC to its respective switch.
4. Connect each switch to a router.
5. Connect both routers using their gigabit ethernet interfaces.
6. Configure the IP address on both PCs.
7. Configure Router0 (and Router1; your file only says Router0, but both are required).
8. Check the routing table using `show ip route`.
9. Open PC0's command prompt and execute `ping 192.168.2.10`.

## Commands

**PCs:** PC0: IP 192.168.1.10, mask 255.255.255.0, gateway 192.168.1.1. PC1: IP 192.168.2.10, mask 255.255.255.0, gateway 192.168.2.1.

**Router0:**
```
enable
configure terminal
interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
interface g0/1
ip address 10.0.0.1 255.255.255.0
no shutdown
exit
ip route 192.168.2.0 255.255.255.0 10.0.0.2
end
write memory
```
**Router1:**
```
enable
configure terminal
interface g0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
exit
interface g0/1
ip address 10.0.0.2 255.255.255.0
no shutdown
exit
ip route 192.168.1.0 255.255.255.0 10.0.0.1
end
write memory
```

## Verification
- `show ip route` on both routers: `C` (connected) and `S` (static) entries, e.g. `S 192.168.2.0/24 [1/0] via 10.0.0.2`.
- On PC0: `ping 192.168.2.10`: four replies.
- **Screenshot in your file (page 27, rotated):** Router0 CLI with `ip route 192.168.2.0 255.255.255.0 10.0.0.2`, `end`, then `ping 192.168.2.2` with `!!!!!` and "Success rate is 100 percent (5/5)". `!` = reply received, `.` = timeout.

## Result
Successfully implemented static routing between two different networks using Cisco Packet Tracer.

## Viva
- **What is a next hop?** The next router/interface to which a packet should be forwarded.
- **Why configure routes on both routers?** Forward path must exist and the destination network must know how to return traffic.
- **Static vs dynamic routing?** Static is manually configured; dynamic protocols learn and exchange routes.
- Syntax of the static route command.
- What does the `S` code in the routing table mean?
- Common mistake: configuring only one router (packets reach the far PC but replies cannot return).
