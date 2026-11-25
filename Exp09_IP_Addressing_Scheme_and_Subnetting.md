# Experiment 9: Implement an IP Addressing Scheme and Subnetting in a Small Network

## Aim
To implement an IP addressing scheme and subnetting in a small network.

## Theory
**IP address:** a unique logical address assigned to a device in a network, used to identify devices and enable communication between them.

**IPv4:** 32 bits divided into four octets (8 bits each), written in decimal separated by dots, each octet 0 to 255. Example: 192.168.1.10. An address has a **network part** and a **host part**; the **subnet mask** shows where the split is (255.255.255.0 = /24 means the first 24 bits are the network part).

**Classes of IPv4:**
| Class | First octet | Default mask | Note |
|---|---|---|---|
| A | 1 to 126 | 255.0.0.0 (/8) | very large networks |
| B | 128 to 191 | 255.255.0.0 (/16) | medium |
| C | 192 to 223 | 255.255.255.0 (/24) | small (192.168.x.x is class C) |
| D | 224 to 239 | none | multicast |
| E | 240 to 255 | none | reserved |

Private ranges: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16; 127.0.0.1 is loopback.

**Subnetting:** dividing a large network into smaller networks called subnets. Benefits: less broadcast traffic, better security and management, efficient use of addresses, separation of broadcast domains.

**Your worked example (page 24):**
- IP address: 192.168.1.10
- Subnet mask: 255.255.255.0
- Network address: 192.168.1.0 (IP AND mask; all host bits 0)
- Broadcast address: 192.168.1.255 (all host bits 1)
- Usable hosts: 192.168.1.1 to 192.168.1.254 = 2^8 - 2 = 254.

**Basic subnetting table**
| CIDR | Mask | Total addresses | Usable hosts |
|---|---|---|---|
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 8 | 6 |
| /30 | 255.255.255.252 | 4 | 2 |
(Usable hosts exclude the network and broadcast addresses.)

**Subnetting method (any question):** split 192.168.1.0/24 into 4 subnets: borrow 2 host bits, new mask /26 = 255.255.255.192; block size 256 - 192 = 64; subnets .0, .64, .128, .192; each has 2^6 - 2 = 62 usable hosts. For subnet .64: network .64, first host .65, last host .126, broadcast .127. Formulas: subnets = 2^n (n borrowed bits); hosts per subnet = 2^h - 2.

## IP addressing table (your file)
| Device | IP address | Subnet mask |
|---|---|---|
| PC0 | 192.168.1.10 | 255.255.255.0 |
| PC1 | 192.168.1.20 | 255.255.255.0 |
| PC2 (crash-course PDF extra) | 192.168.1.30 | 255.255.255.0 |

## Procedure as written in your file
1. Open Cisco Packet Tracer.
2. Add two PCs and one 2960 switch to the workspace.
3. Connect both PCs to the switch using copper straight-through wires.
4. Click PC0 and open Desktop, IP Config.
5. Assign the following IP config: IP address 192.168.1.10; Subnet mask 255.255.255.0.
6. Similarly configure PC1 (192.168.1.20, mask 255.255.255.0).
7. Open the command prompt on PC0.
8. Execute the command `ping 192.168.1.20`.
9. Check whether packets are successfully transmitted and received.

**Screenshot in your file (page 25, rotated):** Router with G0/0 and G0/1, a Switch0 on each side with PC0 to PC3, and PC0 Command Prompt showing `ping 192.168.1.130` with four replies (32 bytes, TTL=128), Sent 4, Received 4, Lost 0 (0% loss). It comes from a two-subnet reference example.

## Procedure (crash-course version)
1. Open Packet Tracer.
2. Place two or more PCs and a switch.
3. Connect all PCs to the switch.
4. Assign IPs from the same subnet.
5. Use the subnet mask consistently.
6. Test with ping (PC0, PC1, PC2 among each other).

## Extra demonstration for subnetting
Set mask 255.255.255.192 on both PCs. PC0 192.168.1.10 is in subnet .0 to .63 and PC1 192.168.1.70 is in .64 to .127, so a ping fails without a router. Put both in the same block and the ping works again. This shows the purpose of the mask.

## Result
Implemented an IP addressing scheme and subnetting in a small network using Cisco Packet Tracer.

## Viva
- **What is a subnet?** A logical division of an IP network.
- **Why subnet?** Better address allocation, management, and separation of broadcast domains.
- **What is a broadcast address?** An address used to communicate with all hosts in a subnet.
- Network and broadcast address of 192.168.1.10/24.
- Mask for /26 and its host count (255.255.255.192, 62).
- Difference between classful and classless (CIDR) addressing.
