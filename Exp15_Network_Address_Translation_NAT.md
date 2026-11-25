# Experiment 15 (manual item 7): Implement Network Address Translation (NAT)

*(Listed in your lab manual; not in your handwritten file or the crash-course PDF. The manual says "Network Address Resolution" but NAT stands for Network Address **Translation**; address resolution is ARP. Write "Translation" in your file.)*

## Aim
To implement Network Address Translation (NAT) using Cisco Packet Tracer.

## Theory
**Why NAT exists.** IPv4 has only about 4.3 billion addresses, far fewer than the number of devices. Organizations use **private addresses** inside (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, RFC 1918), which are **not routable on the Internet**. **NAT**, running on the edge router or firewall, **translates private addresses into public (global) addresses** and back, so many internal hosts can reach the Internet. It also hides the internal addressing (basic security) and lets a company change ISP without renumbering. Disadvantages: breaks end-to-end addressing, adds delay and processing, problems with some protocols (IPsec, peer-to-peer), harder tracing.

**Terminology (very important in viva):**
| Term | Meaning |
|---|---|
| Inside local | private address of an inside host (192.168.1.10) |
| Inside global | public address that represents the inside host outside (200.1.1.10) |
| Outside local | address of an outside host as seen from inside |
| Outside global | real public address of the outside host (200.1.1.2) |
| Inside interface | router interface facing the private LAN (`ip nat inside`) |
| Outside interface | router interface facing the ISP/Internet (`ip nat outside`) |

**Types of NAT:**
1. **Static NAT:** permanent **one-to-one** mapping between one inside local and one inside global address. For servers that must be reachable from outside. One public address per host.
2. **Dynamic NAT:** inside local addresses are mapped to inside global addresses from a **pool**, first come first served; mapping lasts until it times out. If the pool is exhausted, new hosts cannot get out.
3. **PAT (Port Address Translation) / NAT overload:** **many inside hosts share one public address**, distinguished by **port numbers**. Most common (home routers).

**How PAT works:** PC 192.168.1.10 sends to server 200.1.1.2 with source 192.168.1.10:1025. The router rewrites the source to 200.1.1.1:5001, records it in the **NAT table** and forwards. The reply arrives at 200.1.1.1:5001; the router looks up the table, rewrites the destination to 192.168.1.10:1025 and delivers it.

## Topology
```
PC0 ─┐
     ├─ Switch0 ─ G0/0 [Router0 NAT] G0/1 ─ Server0 (acts as Internet/ISP)
PC1 ─┘
```
| Device | Interface | IP address |
|---|---|---|
| PC0 | NIC | 192.168.1.10/24, gateway 192.168.1.1 |
| PC1 | NIC | 192.168.1.11/24, gateway 192.168.1.1 |
| Router0 (inside) | G0/0 | 192.168.1.1/24 |
| Router0 (outside) | G0/1 | 200.1.1.1/24 |
| Server0 (outside) | NIC | 200.1.1.2/24, gateway 200.1.1.1 |
Public pool for dynamic NAT: 200.1.1.10 to 200.1.1.20.

## Procedure
1. Open Cisco Packet Tracer.
2. Place one router (2911), one switch, two PCs and one server.
3. Connect PCs and Router G0/0 to the switch (straight-through). Connect Router G0/1 to the server (cross-over; straight-through also works with Auto-MDIX; use cross-over if the link stays red).
4. Assign IP addresses to the PCs (with gateway) and the server as in the table.
5. Configure the router interfaces and mark inside/outside:
```
Router> enable
Router# configure terminal
Router(config)# interface gigabitEthernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# ip nat inside
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# interface gigabitEthernet 0/1
Router(config-if)# ip address 200.1.1.1 255.255.255.0
Router(config-if)# ip nat outside
Router(config-if)# no shutdown
Router(config-if)# exit
```
6. Configure **one** of the three NAT types:

**(a) Static NAT** (PC0 always appears as 200.1.1.10):
```
Router(config)# ip nat inside source static 192.168.1.10 200.1.1.10
```
**(b) Dynamic NAT** (pool):
```
Router(config)# access-list 1 permit 192.168.1.0 0.0.0.255
Router(config)# ip nat pool MYPOOL 200.1.1.10 200.1.1.20 netmask 255.255.255.0
Router(config)# ip nat inside source list 1 pool MYPOOL
```
**(c) PAT / overload** (all hosts share the outside interface address):
```
Router(config)# access-list 1 permit 192.168.1.0 0.0.0.255
Router(config)# ip nat inside source list 1 interface gigabitEthernet 0/1 overload
```
The **access list** says which inside addresses may be translated (0.0.0.255 is a wildcard mask, the inverse of 255.255.255.0). The **pool** is the set of public addresses.

7. Save: `end`, then `write memory`.
8. Test: from PC0 Command Prompt `ping 200.1.1.2` (the server): four replies.
9. Verify on the router:
   - `show ip nat translations` (inside global, inside local, outside local, outside global). Example (PAT): `icmp 200.1.1.1:1 192.168.1.10:1 200.1.1.2:1 200.1.1.2:1`.
   - `show ip nat statistics` (translations, hits, misses, interfaces).
   - `clear ip nat translation *` clears dynamic entries.
10. Optional: Simulation mode, send a ping and click the packet at the router to compare the **inside** packet (source 192.168.1.10) with the **outside** packet (source 200.1.1.x).
11. Optional (static NAT): from the server, ping 200.1.1.10; the router translates it to 192.168.1.10 and PC0 replies.

## Common mistakes
- Forgetting `ip nat inside` / `ip nat outside` on the interfaces (nothing is translated).
- Access list that does not match the inside addresses.
- Missing default gateway on the PCs.
- Pool overlapping the router's own interface address.
- Without a real Internet the "outside" is just the server; that is enough.

## Result
Network Address Translation (static, dynamic and PAT) was implemented; private addresses were translated to public addresses, as verified by `show ip nat translations`.

## Viva
- Expand NAT; why needed? (IPv4 exhaustion; private addresses not routable.)
- Static vs dynamic NAT vs PAT.
- Inside local, inside global, outside local, outside global.
- Which command shows the NAT table? What does `overload` do?
- Difference between NAT and ARP, and why the manual's title is wrong.
- Private ranges (RFC 1918).
