# Experiment 1: Introduction to Computer Network and Cisco Packet Tracer
*(Date in your file: 6-8-26)*

## Aim
To understand what a computer network is, its applications, transmission media and modes, types and topologies of networks, the client-server architecture, and to get introduced to Cisco Packet Tracer.

## Theory

### 1. Computer network
A computer network is a collection of interconnected devices that communicate with each other and share resources such as data, files, printers and internet connections. The devices (nodes/hosts) can be computers, laptops, phones, servers, printers, switches and routers. They are linked by cables or wireless signals and follow common rules (protocols) so they understand each other.

Key terms: **Node** (any connected device), **Host** (endpoint that sends/receives data), **Link** (connection between devices), **Client** (requests a service), **Server** (provides a service), **Interface** (point where a device connects to a network).

### 2. Applications of computer networks (as in your file)
- **Resource sharing:** printers, files, software, storage shared by many users.
- **Communication:** email, messaging, video calls.
- **Internet access:** browsing websites and online services through one shared connection.
- **Remote access:** using another computer/server from a distance (remote desktop, SSH, telnet).
- **Online services:** banking, shopping, education.
- **Entertainment:** online gaming, streaming music/video.

### 3. Components of data communication (five)
1. **Sender:** device that sends the data/message.
2. **Receiver:** device that receives the data.
3. **Message:** the actual information (text, numbers, image, audio, video).
4. **Transmission medium:** path through which the message travels.
5. **Protocol:** set of rules controlling communication (without it, two connected devices cannot understand each other).

Examples of protocols: HTTP (web), HTTPS (secure web), TCP (reliable delivery), UDP (fast, connectionless), IP (addressing/routing), DNS (names to IPs), DHCP (automatic IP), ARP (IP to MAC), ICMP (diagnostics), SMTP (sending email), FTP (file transfer).

### 4. Transmission medium: guided and unguided
- **Guided (wired) media:** data travels through a physical cable (twisted pair UTP/STP, coaxial, optical fibre).
- **Unguided (wireless) media:** data travels through electromagnetic waves (radio waves, microwaves, infrared, satellite).

### 5. Transmission modes
- **Simplex:** data flows in one direction only (keyboard to computer, TV broadcast).
- **Half duplex:** both directions but not at the same time (walkie-talkie).
- **Full duplex:** both directions simultaneously (telephone call, modern switched Ethernet).

### 6. Cisco Packet Tracer
A network simulation and visualization tool by Cisco, used to create, configure and test computer networks virtually without physical devices.

**Main features:** create different network topologies; add and connect PCs, switches, routers, servers, etc.; configure IP addresses; configure routers and switches; observe how data packets travel; use **Simulation mode** to observe packet flow step by step.

**Main components:**
1. **End devices:** devices that communicate over the network (PC, laptop, server).
2. **Network devices:** devices that connect and manage networks (switch, router, hub).
3. **Connections:** copper straight-through, copper cross-over, fibre, console.
4. **Protocols:** rules used for communication, e.g. TCP/IP.

**Modes:**
- **Realtime mode:** the network operates normally and results appear immediately.
- **Simulation mode:** lets us see packets moving between devices and understand the communication process; step with the Capture/Forward button and inspect each layer of a packet.

### 7. Types of computer networks
1. **PAN (Personal Area Network):** connects devices within a very small area around an individual, e.g. a laptop to wireless earbuds. Range a few metres.
2. **LAN (Local Area Network):** connects computers and devices within a limited area such as home, school, office. High speed, resource sharing, usually one owner.
3. **MAN (Metropolitan Area Network):** connects multiple LANs across a city; larger than a LAN. Example: cable TV network, a bank's city branches.
4. **WAN (Wide Area Network):** covers a very large area such as a country, continent or the world. The Internet is the biggest WAN.

### 8. Network topologies
Topology is the arrangement (physical or logical) of devices and links.

| Topology | Description | Advantages | Disadvantages | Use |
|---|---|---|---|---|
| **Bus** | All devices on one central cable; data travels along the bus until it reaches the destination | Simple, inexpensive, less cable | Whole network down if cable fails; performance degrades with more devices | Small networks |
| **Star** | All devices connected to a central hub/switch | Easy to install and manage; one device failing does not affect others | Hub failure affects whole network; more cable than bus | Home networks |
| **Ring** | Each device connected to exactly two others, forming a ring | Predictable data transmission; easy to troubleshoot | Failure of one device disrupts network; more cable than bus | High-speed data transfer networks |
| **Mesh** | Each device connected to multiple others (full mesh: n(n-1)/2 links) | Scalable; one segment failing does not affect others | Complex and expensive (many cables) | Mission-critical networks |
| **Tree** | Star groups connected to a linear bus (backbone) | Easy management and troubleshooting; scalable | Backbone failure brings down the network; more cabling | Large organizations, schools, universities |
| **Hybrid** | Combination of two or more topologies | Flexible and scalable | Complex design and management | Enterprise environments |

### 9. Client-server architecture
A network architecture in which clients request services or resources from a central server, and the server processes the request and provides the response.

**Process (as in your file):**
1. Client sends a request to the server.
2. Server receives and processes the request.
3. Server accesses the required resource/data if needed.
4. Server sends a response back to the client.
5. The client displays or uses the response.

**Advantages:** centralized data management; better security and access control; easy backup and maintenance; multiple clients can use the same server; resources shared efficiently.
**Examples:** web browser and web server, email client and mail server.

## Procedure / activity
This experiment is theory in your file. In Packet Tracer practise:
1. Open Packet Tracer.
2. Explore the device panel (bottom left): End Devices, Network Devices, Connections.
3. Explore the workspace and the Logical/Physical tabs.
4. Drag a PC into the workspace.
5. Drag a switch into the workspace.
6. Connect the PC to the switch.
7. Explore Realtime mode.
8. Explore Simulation mode (bottom right).
9. Observe packet flow.

## Result
Studied computer networks, their applications, transmission media and modes, types and topologies, client-server architecture and the Cisco Packet Tracer tool.

## Viva
- **What is Packet Tracer?** A network simulation and visualization tool used to create, configure and test virtual networks.
- **What is a topology?** The arrangement of devices and links in a network.
- **What is Simulation mode?** A mode in which packets can be observed and inspected as they move through the network.
- Difference between guided and unguided media.
- Name the five components of data communication.
- Which topology fails completely if the central device fails? (Star: hub/switch; bus: backbone.)
