# Experiment 6: ARP Configuration of Various Devices Using ARP Protocol
*(Date in your file: 2-9-26)*

## Aim
ARP configuration of various devices using ARP protocol. Connect system and server through copper straight-through cable with a switch.

## Theory
**ARP (Address Resolution Protocol)** maps a known IP address (logical, Layer 3) to the MAC address (physical, Layer 2) of a device on the same LAN. A frame on Ethernet needs a destination MAC, but applications only know the IP, so ARP is needed before the first frame can be sent. ARP is used automatically in most Ethernet IPv4 communication.

**How it works:**
1. Host A wants to send to Host B (same subnet). A checks its **ARP cache**. If B's IP is there, A uses the stored MAC.
2. If not, A broadcasts an **ARP request** (destination MAC FF:FF:FF:FF:FF:FF): "Who has 192.168.1.10? Tell 192.168.1.1."
3. Only B recognizes its IP and sends a unicast **ARP reply**: "192.168.1.10 is at <my MAC>."
4. A stores the IP-to-MAC mapping in its ARP table (dynamic entry, ages out after a few minutes) and sends the data frame.

If the destination is on another network, the host ARPs for the **default gateway's** MAC instead. ARP works only inside a broadcast domain. RARP does the reverse (MAC to IP). A **switch** (Layer 2) learns source MAC addresses into its MAC table and forwards frames only to the right port; ARP requests are broadcast, so the switch floods them to all ports.

## Topology
```
PC0 ───────┐
PC1 ───────┤
PC2 ───────┼── Switch ─── Server
(PC3) ─────┘
```

## IP addressing
Mask 255.255.255.0 for all.

| Device | IP (your file / simple) | IP (crash-course PDF) |
|---|---|---|
| PC0 | 192.168.1.1 | 192.168.1.1 |
| PC1 | 192.168.1.2 | 192.168.1.2 |
| PC2 | 192.168.1.3 | 192.168.1.3 |
| PC3 (optional) | n/a | 192.168.1.4 |
| Server | 192.168.1.4 | 192.168.1.10 |

(Use any consistent set in the same subnet; ping whichever server IP you assigned.)

## Procedure as written in your file
1. Start Cisco Packet Tracer.
2. Select 3 similar end devices (PC) and a switch with 2950-24 config, as well as a server (generic).
3. Arrange them as shown in the pictures on the LHS.
4. Now, with the help of copper straight-through wires, connect all the devices; use FastEthernet ports.
5. Now, set the IP address for each PC.
6. Open terminal (Command Prompt) for any of the devices and run `arp -a`.
7. Now run the ping command and ping 2 PCs.
8. Switch to Simulation from Realtime through the option at the bottom right of the screen.
9. Now use the Capture/Forward button to simulate how devices ping each other.
10. After the simulation is completed, the ARP table has one entry.

## Procedure (click by click)
1. Place 3 or 4 PCs, a **2950-24 (or 2960) switch** and a Server.
2. Connect all devices to the switch using Copper Straight-Through (Fa0/1, Fa0/2, ...). Wait for green lights.
3. Assign IP addresses to all devices.
4. Open a PC Command Prompt and run `arp -a`. Output: "No ARP Entries Found".
5. Ping the server: `ping 192.168.1.4` (or .10). The first request may time out (ARP being resolved), the rest succeed.
6. Run `arp -a` again: one entry showing Internet Address, Physical Address (MAC) and Type dynamic. After pinging a second host there are two entries.
7. Switch to **Simulation mode**. Click Edit Filters and keep only ARP and ICMP.
8. Send a ping and click Capture/Forward repeatedly. Observe the **ARP request** (broadcast, flooded through the switch), the **ARP reply** (unicast back), then ICMP echo request and echo reply.
9. `arp -d` clears the cache.

## Commands to remember
`arp -a`, `ipconfig`, `ping <server IP>`, `arp -d`

## Result
ARP configuration was done; after simulation the ARP table holds an entry (IP to MAC) for the pinged device.

## Viva
- What does ARP do and at which layer? (Maps IP to MAC; Layer 2/3 boundary.)
- Is an ARP request unicast or broadcast? (Broadcast; the reply is unicast.)
- Why does the first ping often fail? (ARP resolution delay.)
- Command to see the ARP table: `arp -a`.
