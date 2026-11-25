# Experiment 7(A) and 7(B): Implement Bus, Star, Ring, Mesh and Hybrid Topologies
*(Date in your file: 17-9-26)*

## Aim
To implement Bus, Star, Mesh, Ring and Hybrid topology.

## Theory
**Network topology** describes the method in which all the elements of a network are mapped (arranged and connected). It can be physical (actual layout) or logical (how data flows). In Packet Tracer, each PC is joined to its own switch and the switches are arranged in the required shape.

1. **Ring topology:** every device has exactly two neighbouring devices for communication and resource sharing. It uses **tokens** to pass information from one node to another (only the token holder transmits, so collisions are avoided). A single break can stop the ring unless it is a dual ring. (In Packet Tracer, Spanning Tree Protocol blocks one link of the ring to prevent a switching loop; this is normal and prevents broadcast storms.)
2. **Bus topology:** a single cable connects all nodes. The main cable acts as a spine (backbone) for the entire network. If the main cable fails, the whole network goes down. Terminators are needed at both ends in a real bus.
3. **Mesh topology:** each computer connects to every other computer; a peer-to-peer connection is established between all devices. Links for n nodes = n(n-1)/2 (6 links for 4 nodes); each node needs n-1 ports. Very reliable but costly.
4. **Star topology:** all computers connect to a single hub/switch (the central node). If the hub fails, the whole network fails.
5. **Hybrid topology:** a combination of two or more topologies such as mesh, bus and ring. Its use depends on requirements like performance, number of computers and location. It is a powerful setup with many real-time applications: homes, offices, multi-floor buildings.

| Topology | Links/cables | Key weakness |
|---|---|---|
| Bus | 1 backbone | Backbone failure kills all; collisions |
| Star | n | Hub/switch single point of failure |
| Ring | n | One break disrupts ring (unless dual) |
| Mesh | n(n-1)/2 | Costly and complex |

**Packet Tracer note:** Packet Tracer may not provide a literal Ethernet bus with a shared coaxial backbone. Your notebook simulates the bus using switches connected in a linear chain; this is a logical/visual bus-like layout.

## Procedure as written in your file

### 1. Ring topology
1. First take 4 generic PCs and 4 generic switches.
2. Now connect each PC to a switch.
3. Now connect all PCs using their switches in a ring fashion.
4. Use automatically chosen connection type to make adjacent connections.
5. Now assign IP addresses to all 4 PCs: PC0 = 192.168.0.1, PC1 = 192.168.0.2, PC2 = 192.168.0.3, PC3 = 192.168.0.4.
6. Now ping devices, i.e. PC0 with PC3.
7. Ring topology is established.

### 2. Bus topology
1. Connect PCs with switches.
2. Connect the switches simply in a linear way using automatic connection type.
3. Assign class C IP addresses to all PCs: PC8 = 192.168.0.9, PC9 = 192.168.0.10, PC10 = 192.168.0.11, PC11 = 192.168.0.12.
4. Ping PCs with PCs.

### 3. Mesh topology
1. Take the formation of the ring topology as reference and make a copy. Then connect each PC's switch with every remaining switch one by one (add the diagonal links).
2. Assign IP addresses: PC12 = 192.168.0.13, PC13 = 192.168.0.14 (your file has .13 twice; correct it), PC14 = 192.168.0.15, PC15 = 192.168.0.16.
3. Ping PC13 with PC15.

### 4. Star topology
1. Take 4 PCs and connect them with a single switch.
2. Make the connections using automatic connection type.
3. Assign IP addresses: PC4 = 192.168.0.5, PC5 = 192.168.0.6, PC6 = 192.168.0.7, PC7 = 192.168.0.8.
4. Ping PC4 with PC7.

## Experiment 7(B): 5. Hybrid topology (as written in your file)
1. First we need to make all different topologies separately.
2. Firstly implement ring topology using 4 PCs.
3. Assign IP addresses from 192.168.0.1 to 192.168.0.4.
4. Now, make star topology adjacent to it.
5. Assign IP addresses from 192.168.0.5 to 192.168.0.8.
6. Thirdly, make bus topology below ring topology.
7. Assign IP addresses from 192.168.0.9 to 192.168.0.12.
8. Lastly, make hybrid (mesh) topology in the bottom right corner.
9. Assign IP addresses from 192.168.0.13 to 192.168.0.16.
10. Connect all 4 topologies using automatic connection cable by connecting the switches of all 4 topologies.
11. Ping PC1 (ring topology) with PC14 (hybrid topology).
12. To check, try sending a data packet from PC1 to PC15.
13. Established successfully.

## Additional detail (crash-course PDF)
- **Star:** 4 PCs on one switch; automatic or straight-through; ping PC3 from PC0 (`ping 192.168.0.4`).
- **Bus (linear):** `Switch0 ── Switch1 ── Switch2`, PCs on each; ping PCs at opposite ends.
- **Ring:** four PCs and four switches in a closed loop; some links may be blocked by STP.
- **Mesh (full):** every node linked to every other (use crossover or automatic). For 4 nodes: 4 x 3 / 2 = 6 links. A pure PC-to-PC mesh needs 3 NICs per PC; the switch-based mesh (copy of the ring plus diagonals) is easier.
- **Hybrid:** build each topology independently, give each section its own IP range, connect sections via switches, verify local communication, ping between sections, use Simulation mode to watch packets.

All sixteen PCs use mask 255.255.255.0 in 192.168.0.0/24, so all can ping each other once the switches are joined. PC-to-switch cables: straight-through; switch-to-switch: automatic. Wait for green link lights; the first ping can time out.

## Result
Bus, star, ring, mesh and hybrid topologies were implemented and connectivity was verified with ping.

## Viva
- Which topology uses the most cable? (Mesh.) Which fails entirely if the backbone fails? (Bus.)
- How many links in a full mesh of 5 nodes? (10.)
- Why does STP block a link in a ring of switches? (To prevent loops and broadcast storms.)
- What is a full mesh? Each node has a direct connection to every other node.
- What is a hybrid topology and where is it used?
