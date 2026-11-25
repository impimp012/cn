# Experiment 8: Connect Two LANs Using a Router
*(Date in your file: 29-9-26)*

## Aim
To create a connection between 2 LANs using a router on Cisco Packet Tracer.

## Theory
A **LAN** connects devices in a small area through a switch. Devices inside one LAN share the same network address and talk directly (Layer 2, MAC addresses). A **switch cannot connect two different networks**; for that a **router** (Layer 3 device) is needed.

- A router has several interfaces; each belongs to a different network and has its own IP address.
- The router reads the destination **IP address** of each packet, checks its **routing table** and forwards the packet out of the correct interface. It stops broadcasts, so each interface is a separate broadcast domain.
- The IP address of the router interface facing a LAN acts as the **default gateway** for all devices of that LAN. When a PC wants to reach an address outside its own network, it sends the packet to its default gateway (PC0 does not know how to reach 192.168.2.0/24 directly).
- Router interfaces are shut down by default: use `no shutdown` (or tick **On** in the Config tab).
- Ports used: GigabitEthernet0/0 (Gig0/0) and GigabitEthernet0/1 (Gig0/1).
- Both LANs are directly connected to the router, so their networks appear as **Connected (C)** routes automatically; no routing protocol or static route is needed.

This is the key experiment that teaches the difference between a switch and a router.

## Topology
```
LAN 1                                   LAN 2
PC0 ─ Switch0 ─ Gig0/0 [Router] Gig0/1 ─ Switch1 ─ PC1
```

## IP addressing table
| Device | IP | Mask | Gateway |
|---|---|---|---|
| PC0 | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |
| PC1 (or PC2/PC3 in your 2 to 3 PC LANs: .11 etc.) | 192.168.2.10 | 255.255.255.0 | 192.168.2.1 |
| Router G0/0 | 192.168.1.1 | 255.255.255.0 | n/a |
| Router G0/1 | 192.168.2.1 | 255.255.255.0 | n/a |

## Procedure as written in your file
1. Firstly, we will create 2 different LAN networks having one switch and 2-3 PCs each.
2. Select the generic tab and select PC, then drag them on screen.
3. Select the switch tab and drag them on screen.
4. Make another similar network.
5. Now connect each PC in each LAN to its corresponding switch using copper straight-through wires.
6. Now set separate IP addresses for either LAN.
7. Now ping 2 PCs of LAN1 and check the connectivity.
8. Repeat the same for LAN2.
9. Go to router and drag it to the screen.
10. Now connect LAN1 to gigabit 0/0 of the router and LAN2 to gigabit 0/1 of the router.
11. Now turn on the router.
12. To configure, select gigabit 0/0, select On (check) and enter the address.
13. This IP address acts as a gateway for all devices of LAN1 to enter.
14. Repeat the same for LAN2.
15. Ping a device on LAN2 using its IP address from a device in LAN1.
16. Connection between two LANs using router has been successfully established.

## Procedure (click by click, crash-course version)
**Step 1, place devices:** 2 PCs (or 4), 2 switches (2960), 1 router (2911).
**Step 2, connect** (straight-through for PC/switch and switch/router): PC0 to Switch0; Switch0 to Router G0/0; Router G0/1 to Switch1; Switch1 to PC1.
**Step 3, configure PCs:** IP, mask and **default gateway** (a missing gateway is the commonest reason the cross-LAN ping fails).
**Step 4, configure the router:** Router, CLI (or the Config tab, select the port, tick On, enter IP and mask):
```
Router> enable
Router# configure terminal
Router(config)# interface gigabitEthernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# interface gigabitEthernet 0/1
Router(config-if)# ip address 192.168.2.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# end
Router# write memory
```
| Command | Meaning |
|---|---|
| enable | Enter privileged EXEC mode |
| configure terminal | Enter global configuration |
| interface gigabitEthernet 0/0 | Select router interface |
| ip address ... | Assign IP address |
| no shutdown | Turn interface on |
| exit | Exit current configuration level |
| write memory | Save configuration |

**Step 5, test:** from PC0 `ping 192.168.2.10`. The first reply may time out (ARP); the rest succeed. `show ip route` on the router shows C entries for both networks.

## Result
Two LANs were successfully connected using a router and communication between them was verified.

## Viva
- Role of a default gateway.
- Why can't a switch connect two different networks?
- What does `no shutdown` do?
- What happens if the gateway is not set on the PC?
