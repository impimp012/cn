# CN Practical File: Experiment Index

Each file contains: aim, theory, topology/IP table, the procedure exactly as written in your handwritten file, the click-by-click (crash-course PDF) version, commands, expected output, result and viva points.

| File | Experiment |
|---|---|
| Exp01_Introduction_to_Computer_Network_and_Cisco_Packet_Tracer.md | 1. Introduction to Computer Network and Cisco Packet Tracer |
| Exp02_Peer_to_Peer_Connection_Between_Two_Similar_Devices.md | 2. Peer-to-peer, similar devices |
| Exp03_Peer_to_Peer_Connection_Between_Dissimilar_Devices.md | 3. Peer-to-peer, dissimilar devices |
| Exp04_Straight_Through_Crossover_Cables_and_RJ45_Connector.md | 4. Straight-through, crossover, RJ45 |
| Exp05_Connect_Dissimilar_Devices_Machines_and_Hub_Using_Ethernet_Cable.md | 5. PCs and hub using Ethernet cable |
| Exp06_ARP_Configuration_Using_ARP_Protocol.md | 6. ARP configuration |
| Exp07_Bus_Star_Ring_Mesh_and_Hybrid_Topologies.md | 7(A)/(B). Bus, star, ring, mesh, hybrid |
| Exp08_Connect_Two_LANs_Using_a_Router.md | 8. Two LANs using a router |
| Exp09_IP_Addressing_Scheme_and_Subnetting.md | 9. IP addressing and subnetting |
| Exp10_Static_Routing.md | 10. Static routing |
| Exp11_DHCP.md | 11. DHCP |
| Exp12_DNS_and_Email_Services.md | 12. DNS and email |
| Exp13_Multiple_Router_Network_and_EIGRP.md | 13. Multiple routers and EIGRP |
| Exp14_Dynamic_Routing_Protocols_RIP_and_IGRP.md | 14. RIP and IGRP (manual item 5) |
| Exp15_Network_Address_Translation_NAT.md | 15. NAT (manual item 7) |

## Fixes to make in your handwritten file
- Exp 3: PC and laptop are similar devices (crossover is right for that pair); use straight-through for PC to switch/hub/router.
- Exp 5: IPs .1 to .6 but only 5 PCs.
- Exp 7: PC12 and PC13 both 192.168.0.13 (make one .14); "197.168" should be "192.168" (Exp 3, 7, 8, 9).
- Exp 10: both routers need a static route, not only Router0.

## Exam-day rules
- Similar devices: crossover. Dissimilar devices: straight-through.
- Always `no shutdown` on router interfaces; set the default gateway on PCs.
- Ping not working? Check cable/lights, IP and mask, same subnet, gateway, router interfaces, routes on both sides.
