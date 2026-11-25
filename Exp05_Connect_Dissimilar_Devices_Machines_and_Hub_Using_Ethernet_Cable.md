# Experiment 5: Connect Dissimilar Devices (Machines and Hub) Using Ethernet Cable
*(Date in your file: 27-8-26)*

## Aim
To connect dissimilar devices (machines and hub) using Ethernet cable.

## Theory
A **hub** is a Layer 1 (physical layer) multiport repeater. Whatever signal arrives on one port is regenerated and sent out of **all other ports**, whether or not they are the intended destination.
- No intelligence and **no MAC address table**; it cannot filter traffic.
- All ports are in **one collision domain and one broadcast domain**; bandwidth is shared (a 10 Mbps hub with 5 PCs shares 10 Mbps).
- Works in **half duplex**, so CSMA/CD is needed to handle collisions.
- Only the device whose address matches the destination accepts the data; others discard it.
- Cheap but causes more traffic and offers poor security; switches have replaced hubs.

A PC and a hub are **dissimilar devices**, so they are connected using a **copper straight-through** cable through the FastEthernet port. All PCs need IP addresses in the same network so they can communicate.

**Hub vs switch (viva):** hub repeats signals (Layer 1); switch learns MAC addresses and forwards frames selectively (Layer 2).

## Topology
```
        PC0
         |
PC1 ---- HUB ---- PC2
         |
        PC3 (PC4 ...)
```

## IP configuration
Mask for all: 255.255.255.0

| Device | IP |
|---|---|
| PC0 | 192.168.1.1 |
| PC1 | 192.168.1.2 |
| PC2 | 192.168.1.3 |
| PC3 | 192.168.1.4 |
| PC4 (if you add 5 PCs as in your file) | 192.168.1.5 |

## Procedure as written in your file
1. Open Cisco Packet Tracer.
2. From the toolbars at the bottom, click on the end devices and select end devices 'PC', then click on the screen. By this, add 5 PCs.
3. Connect all devices with a generic hub using copper straight-through cable with the FastEthernet port.
4. Now we need to assign IP addresses to all PCs. Click on PC0. A dialog box will appear. Select Desktop, then select IP Configuration. Assign IP 192.168.1.1 onwards to the other PCs (your file writes "1 to 6"; with 5 PCs it is .1 to .5).
5. Now the computers can communicate with each other. To test the connection, click on PC0, select Desktop and then select cmd (Command Prompt).
6. Execute the following commands: `ipconfig`, `ipconfig /all`, `ping 192.168.1.2`.
7. Repeat step 6 for any other combination.

## Procedure (click by click, crash-course version)
1. Open Cisco Packet Tracer.
2. Drag PCs (4 or 5).
3. Network Devices, Hubs, drag a **Generic Hub (Hub-PT)** and place it centrally.
4. Connect each PC's FastEthernet0 to a hub port with Copper Straight-Through.
5. Assign the IP addresses above (Desktop, IP Configuration).
6. Open PC0 Command Prompt and run `ping 192.168.1.2`, `ping 192.168.1.3`, `ping 192.168.1.4`.
7. Test from another PC as well.
8. Optional: Simulation mode, send a simple PDU (envelope) from PC0 to PC1 and watch the hub copy the packet to every port while only PC1 replies.

**Why can the PCs communicate?** All PCs are in the same IP network and the hub repeats their signals.

## Result
Dissimilar devices (PCs and hub) were connected using Ethernet cable and communication between all PCs was verified.

## Viva
- Why straight-through? (PC and hub are dissimilar.)
- Hub vs switch vs router (layer, collision domain, broadcast domain, MAC/IP table).
- Why is a hub called a multiport repeater?
- Hub operates at Layer 1; a switch commonly at Layer 2.
