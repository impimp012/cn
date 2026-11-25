# Experiment 3: Peer-to-Peer Connection Between Dissimilar Devices
*(Date in your file: 13-8-26)*

## Aim
To establish a peer-to-peer connection using Cisco Packet Tracer between dissimilar devices.

## Theory
Cisco Packet Tracer is a simulation software used to create complicated network topologies as well as test and simulate abstract networking concepts.

**Dissimilar devices** are devices of different categories, e.g. a PC (end device) and a switch, hub or router (network device). A computer's NIC transmits on pins 1 and 2 and receives on pins 3 and 6. A switch or hub is wired the opposite way (receives on 1,2 and transmits on 3,6). Because the transmit/receive pairs are already opposite, the cable must keep pins the same at both ends (pin 1 to pin 1, 2 to 2, and so on). That is the **straight-through cable**.

**Straight-through cable:** both ends use the same wiring standard, no left/right distinction, no manual configuration needed.

**Note on your screenshot (page 11):** the screenshot shows PC0 and Laptop0 joined by a dotted line (crossover). A PC and a laptop are both end devices, so strictly they are similar devices and crossover is correct for that pair. For a true dissimilar pair use PC to switch, PC to hub, or PC to router with straight-through. Be ready to explain this.

**Packet Tracer note:** with devices that support auto-crossover (Auto-MDIX) both cable types may work; in the viva explain the traditional Tx/Rx pair difference.

## Topology
```
PC0 ───── Switch0 ───── PC1        (Copper Straight-Through)
```
(or PC to hub, PC to router)

## IP addresses
| Device | IP | Mask |
|---|---|---|
| PC0 | 192.168.1.1 | 255.255.255.0 |
| PC1 (or Laptop) | 192.168.1.2 | 255.255.255.0 |

## Procedure as written in your file
**Steps to build a straight-through connection between dissimilar devices.**

**Step 1 (to connect, peer-to-peer connection is developed):**
1. Select and drag 2 dissimilar end devices from the device panels at the bottom left corner.
2. Select and drag straight-through copper cables from the wire panel and connect the two devices while choosing the 'FastEthernet' option.
3. Required connection is established.

**Step 2 (to test and configure the network):**
1. Select a device and give it an IP address.
2. Repeat for other devices.
3. Open command prompt and run the `ping` command.

**Commands:** `ping ip-address`: primary TCP/IP command used to troubleshoot connectivity, reachability and name resolution.

**Simulation using the traffic generator (your page 12):** go to traffic generator; destination IP 192.168.1.2; source IP 192.168.1.1 (write 192, not 197); sequence number 1; periodic interval 1; click Send; click Simulation; Play.

**Screenshots in your file (page 11):** IP Configuration window (Static, IPv4, mask, gateway, DNS) and Command Prompt on laptop0 showing `ipconfig` (192.168.1.2 / 255.255.255.0) and `ping 192.168.1.1` with four replies (32 bytes, TTL=128), Sent 4, Received 4, Lost 0 (0% loss).

## Procedure (click by click, crash-course version)
1. Drag a PC into the workspace.
2. Drag a Laptop (or switch) into the workspace.
3. Select Copper Straight-Through (or Automatic Connections).
4. Connect both devices through Ethernet (FastEthernet0).
5. Assign PC IP 192.168.1.1 and the other device 192.168.1.2, mask 255.255.255.0.
6. Open PC Command Prompt and run `ping 192.168.1.2`.

## Result
The devices communicate successfully; peer-to-peer connection between dissimilar devices was established.

## Viva
- Rule: similar devices get crossover, dissimilar devices get straight-through.
- What is a peer-to-peer connection?
- What does Auto-MDIX do? (Modern ports detect and correct the cable type automatically.)
- Why do two devices need IP addresses?
