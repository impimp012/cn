# Experiment 11: Implement Dynamic Host Configuration Protocol (DHCP) on a Network Topology

## Aim
To implement Dynamic Host Configuration Protocol (DHCP) on a network topology using Cisco Packet Tracer.

## Theory
DHCP stands for Dynamic Host Configuration Protocol. It is a network management protocol used to automatically assign IP addresses and other network configuration. Without DHCP an administrator must type an address on every device (static addressing), which is slow and causes mistakes such as duplicate IPs.

**A DHCP server automatically provides (your file):** IP address, subnet mask, default gateway, DNS server address.

**DORA process:**
1. **D**iscover: a new client broadcasts "is there a DHCP server?" (source 0.0.0.0, destination 255.255.255.255). It broadcasts because a client with no IP does not know where the server is.
2. **O**ffer: the server proposes an IP address and settings.
3. **R**equest: the client broadcasts that it accepts that offer.
4. **A**cknowledge: the server confirms and the client gets a **lease** for a time period.

DHCP uses UDP: port 67 (server) and 68 (client). The address is leased, not owned; it is renewed at half the lease time and returned when the lease ends. A **DHCP pool** is the range of addresses the server may give out; **excluded addresses** (e.g. the router's own IP) are kept out of the pool. If no server answers, a PC self-assigns an APIPA address (169.254.x.x).

Two ways to build it in Packet Tracer: **(A) router as DHCP server** (your file) and **(B) server as DHCP server** (crash-course PDF).

## IP addressing table (your file, version A)
| Device | IP address |
|---|---|
| Router (G0/0) | 192.168.1.1 |
| PC0 | DHCP |
| PC1 | DHCP |
| PC2 | DHCP |
Subnet mask: 255.255.255.0

## Procedure as written in your file (version A: router as DHCP server)
1. Open Cisco Packet Tracer.
2. Add one router, one switch and three PCs.
3. Connect the router to the switch.
4. Connect all three PCs to the switch using copper straight-through cables.
5. Open the router CLI.
6. Configure the router interface.
7. Configure the DHCP pool.
8. Save the config (`end`, then `write memory`).
9. Click PC0 and navigate to Desktop.
10. Select the DHCP option (in IP Configuration).
11. Repeat the same process for PC1 and PC2.
12. The PCs will automatically receive IP addresses from the DHCP server.
13. Verify the assigned IPs using `ipconfig`.
14. Test connectivity by pinging the router: `ping 192.168.1.1`.

## Router commands for steps 5 to 8
```
Router> enable
Router# configure terminal
Router(config)# interface gigabitEthernet 0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# ip dhcp excluded-address 192.168.1.1
Router(config)# ip dhcp pool LAN1
Router(dhcp-config)# network 192.168.1.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.1.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# exit
Router(config)# end
Router# write memory
```
- `ip dhcp excluded-address`: keeps the router's own IP out of the pool.
- `ip dhcp pool`: creates the pool. `network`: sets the range. `default-router`: the gateway given to clients. `dns-server`: the DNS given to clients.

## Alternative procedure (version B: server as DHCP server, crash-course PDF)
1. Place 2 PCs, 1 switch, 1 server; connect all with straight-through cables.
2. Server, Desktop, IP Configuration: IP 192.168.1.2, mask 255.255.255.0.
3. Server, Services, DHCP: switch DHCP **On** and configure:

| Field | Value |
|---|---|
| Pool Name | LAN |
| Default Gateway | 192.168.1.1 (if a router exists; otherwise blank) |
| DNS Server | 192.168.1.2 (if this server is also DNS) |
| Start IP | 192.168.1.10 |
| Subnet Mask | 255.255.255.0 |
| Maximum Users | 50 |
Click Add/Save.
4. PC, Desktop, IP Configuration: choose **DHCP**. Repeat for the second PC. Each gets a different address.
5. Verify with `ipconfig` and test `ping 192.168.1.2`.

## Expected output
Each PC shows an address such as 192.168.1.2/3/4 (version A) or 192.168.1.10/11 (version B), mask 255.255.255.0, gateway 192.168.1.1. `show ip dhcp binding` on the router lists the leases.

## Result
Implemented DHCP using Cisco Packet Tracer.

## Viva
- **What is DHCP?** Protocol that automatically assigns IP configuration to clients.
- **What is DORA?** Discover, Offer, Request, Acknowledge.
- **Why does DHCP use broadcast initially?** A client without an IP does not know the DHCP server's location.
- Port numbers (UDP 67/68). Why exclude addresses? Static vs dynamic addressing. APIPA (169.254.x.x).
