# Experiment 4: Introduction to Straight-Through Cables, Crossover Cables and RJ45 Connector
*(Date in your file: 20-8-26)*

## Aim
Introduction to straight-through cables, crossover cables and the RJ45 connector.

## Theory

### A. Straight-through cable
A straight-through cable is a type of Ethernet cable used to connect different types of devices within a network. When connecting two dissimilar devices, for example a computer to a router, a straight-through cable is needed. There are no left or right distinctions: both ends have the same wiring signals, so each wire corresponds to the same pin at the other end. No manual configuration is needed.

**Features:**
1. **Direct connection:** links devices of different categories, e.g. a computer with a switch or router.
2. **Standard Ethernet cable:** used in Ethernet networks for data transmission.
3. **Colour code consistency:** both ends have identical colour-code sequences.
4. **Common usage:** home and office networks for sharing devices among nodes and link points.

Examples: PC to switch, PC to hub, switch to router.

### B. Crossover cable
A crossover cable is a type of Ethernet cable used to connect similar devices directly to each other without an intermediate network device like a switch or hub. Examples: two computers or two switches. The order of wires differs at each end of the cable; by crossing over the Tx and Rx the data can be obtained by both similar devices.

**Features:**
1. **Device-to-device connection:** direct connectivity between devices of similar types, e.g. two computers.
2. **Pin configuration:** different arrangements on the two ends, e.g. T568A on one end and T568B on the other.
3. **Transmit/Receive swapping:** exchanges the Tx/Rx pairs between the two ends.
4. **Specific purpose:** used where devices must interface without a hub.
5. **Colour code variation:** some wires at each end have colour sequences different from the other end.

Examples: PC to PC, switch to switch.

### C. RJ45 connector
RJ45 stands for Registered Jack 45 and is the most commonly used connector in wired networks. The jacks are mainly used to connect to the LAN. RJ45 is wider than the telephone (RJ11) connector. Bandwidth is high; speed is up to 10 Gbps (depends on the cable category).

**Structure:** transparent plastic body, an 8-pin connector, used with shielded (STP) or unshielded (UTP) twisted pair cables. Out of 8 wires, 4 are solid and 4 are stripe coloured. Two colour code schemes: T568A and T568B.

**Advantages:** (1) much greater speed; (2) cheaper than other connectors; (3) supports much greater bandwidth; (4) very reliable.
**Disadvantages:** (1) compatibility issues, not compatible with other connectors; (2) neither weatherproof, so not much durability.

### Wiring standards (for viva)
- **T568A:** 1 white-green, 2 green, 3 white-orange, 4 blue, 5 white-blue, 6 orange, 7 white-brown, 8 brown.
- **T568B:** 1 white-orange, 2 orange, 3 white-green, 4 blue, 5 white-blue, 6 green, 7 white-brown, 8 brown.
- **Straight-through:** same standard at both ends (T568B-T568B is common).
- **Crossover:** T568A at one end and T568B at the other (pairs 1,2 and 3,6 swap).
- 10/100 Mbps Ethernet uses only pins 1, 2, 3, 6; Gigabit uses all 8. Maximum segment length 100 m. Tools: crimping tool, cable tester, RJ45 plugs, UTP cable.

## Packet Tracer demonstration (from the crash-course PDF)
1. Open Packet Tracer.
2. Place two PCs.
3. Open Connections.
4. Select Copper Straight-Through.
5. Connect PC0 to PC1 and observe the link.
6. Remove the cable.
7. Repeat using Copper Cross-Over.
8. Observe the link status.

Packet Tracer may allow both cable types to work with devices that support auto-crossover. In the viva, explain the traditional transmit/receive pair difference. Also show the Connections panel: Copper Straight-Through (solid line), Copper Cross-Over (dashed line), Console, Fiber, Automatically Choose Connection Type.

## Result
Studied straight-through cables, crossover cables and the RJ45 connector.

## Viva
- Difference between T568A and T568B.
- When do we use crossover vs straight-through?
- Which pins carry data in Fast Ethernet? (1, 2, 3, 6.)
- Maximum length of a UTP segment? (100 m.)
