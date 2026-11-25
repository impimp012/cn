# Experiment 2: Peer-to-Peer Connection Between Two Similar Devices
*(Date in your file: 13-8-26)*

## Aim
To establish a peer-to-peer connection between two similar devices using Cisco Packet Tracer.

## Theory
Cisco Packet Tracer is a simulation software used to create complicated network topologies as well as test and simulate abstract networking concepts.

**Peer-to-peer (P2P) connection:** two devices communicate directly with each other, with no intermediate device (no switch/hub) and no dedicated server. Each device can send and receive data.

**Similar devices** are of the same category: PC to PC, laptop to laptop, switch to switch, router to router. They have the same pin arrangement: they transmit on pins 1 and 2 and receive on pins 3 and 6. With a straight-through cable the transmit pins of one device would meet the transmit pins of the other and neither would receive. A **crossover cable** swaps the pairs (pin 1 to 3, pin 2 to 6) so transmit of one reaches receive of the other. Hence a **copper cross-over** cable is used.

**Fast Ethernet:** the 100 Mbps Ethernet port (FastEthernet0) on the PC, selected when connecting.

**IP address:** logical address given to each device. Both PCs must be in the same network (same network part and subnet mask), e.g. 192.168.1.1 and 192.168.1.2 with mask 255.255.255.0 (network 192.168.1.0/24). Because they are in the same network, PC0 reaches PC1 directly at Layer 2 without a router.

## Topology
```
PC0 ───────── PC1      (Copper Cross-Over, FastEthernet0 to FastEthernet0)
```

## IP configuration
| PC | IP address | Mask |
|---|---|---|
| PC0 | 192.168.1.1 | 255.255.255.0 |
| PC1 | 192.168.1.2 | 255.255.255.0 |

## Procedure as written in your file
**Step 1 (to connect, peer-to-peer connection is developed):**
1. Select and drag two end devices from the device panel at the bottom left corner.
2. Select and drag copper crosswise (cross-over) from the wires panel and connect the two devices while choosing the 'FastEthernet' option.
3. After dragging the wire to the second device, again select the 'FastEthernet' option.
4. The required connection is established.

**Step 2 (to test and configure the network):**
1. Select a device, click it, go to Desktop option, then IP Configuration option, and add the IP address for the device.
2. (Repeat for the second device.)
3. Now open Command Prompt for the first device.
4. Run command `ipconfig` in cmd to get basic info about the connection.
5. Run command `ipconfig /all` to see all info about that device related to the network.
6. Now type `ping <ip address>` of the device on the network to check whether they can communicate or not.
7. Repeat steps 3 to 6 for each device on the network.

## Procedure (click by click, crash-course version)
1. Open Packet Tracer.
2. Drag two PCs into the workspace.
3. Click Connections (lightning bolt).
4. Select Copper Cross-Over (or Automatic Connections).
5. Connect PC0 to PC1 (FastEthernet0 on both). Wait for the link lights to turn green.
6. Click PC0, Desktop, IP Configuration, Static: set 192.168.1.1, mask 255.255.255.0.
7. Repeat for PC1 using 192.168.1.2.
8. Open PC0, Desktop, Command Prompt and execute `ping 192.168.1.2`.

## Commands
1. `ipconfig`: displays all current TCP/IP network configuration values and refreshes DHCP and DNS settings.
2. `ipconfig /all`: displays all configuration information for each adapter (IP, mask, gateway, DNS, MAC address, DHCP status).
3. `ping ip-address`: primary TCP/IP command to troubleshoot connectivity, reachability and name resolution; sends 4 ICMP echo request packets of 32 bytes each.

**Traffic generator (from your file):** open Traffic Generator (Desktop tab); set source and destination IP; sequence number 1, periodic interval 1; click Send and minimize the window; switch to Simulation and Play.

## Expected output
`Reply from 192.168.1.2: bytes=32 time<1ms TTL=128` four times, then Sent = 4, Received = 4, Lost = 0 (0% loss). (The first ping may time out while ARP resolves.)

## Result
Peer-to-peer connection between two similar devices was established and tested using Cisco Packet Tracer.

## Viva
- Why crossover for similar devices? (Tx/Rx pairs must be swapped.)
- What is TTL=128? (Windows default TTL, reduced by 1 at each router.)
- What does ping use? (ICMP echo request/reply.)
- Difference between `ipconfig` and `ipconfig /all`.
- Can they communicate without a router? Yes, if both are in the same network with a compatible configuration.
- Why do two devices need IP addresses? For logical identification and communication at the Network layer.
