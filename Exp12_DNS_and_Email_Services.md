# Experiment 12: Implement DNS and Email Services in a Network

## Aim
To implement DNS and email services in a network using Cisco Packet Tracer.

## Theory

### DNS (Domain Name System)
A service that translates human-readable domain names into IP addresses (e.g. www.google.com to an IP address), so users need not remember numerical IP addresses. DNS is a distributed, hierarchical database: root, top-level domain (.com, .in), then authoritative servers. It uses UDP port 53 (TCP for large transfers). Resolution can be recursive or iterative; answers are cached.

Record types: **A** (name to IPv4), **AAAA** (IPv6), **CNAME** (alias), **MX** (mail server for the domain), **NS** (name server), **PTR** (reverse lookup).

### Email service
Allows users to send and receive electronic messages over a network. It mainly uses **SMTP, POP3 and IMAP**:
- **SMTP (port 25):** sending mail from client to server and between servers (push).
- **POP3 (port 110):** the client downloads mail from the server (normally deleting it there).
- **IMAP (port 143):** mail stays on the server and is managed from many devices.
An address looks like user@domain; the server needs a domain name and user accounts with passwords.

## Topology
```
PC0 ──┐
      ├── Switch ─── Server   (router optional, as in your file)
PC1 ──┘
```

## IP addressing
| Device | Your file | Crash-course PDF |
|---|---|---|
| Router G0/0 | 192.168.1.1/24 | not used |
| Server | 192.168.1.2 | 192.168.1.10 |
| PC0 | e.g. 192.168.1.10 | 192.168.1.20 |
| PC1 | e.g. 192.168.1.11 | 192.168.1.21 |
Mask 255.255.255.0; gateway 192.168.1.1 (if router used); **DNS server = the server's IP** on every PC.

## Procedure as written in your file
1. Open Cisco Packet Tracer.
2. Add one router, one switch, one server and 2 PCs.
3. Connect the router and all devices through the switch.
4. Configure the router interface.
5. Configure the server with: IP address 192.168.1.2; Subnet mask 255.255.255.0; Default gateway 192.168.1.1; DNS server 192.168.1.2.
6. Configure PC0 and PC1 with the IP addresses mentioned in the table.

**DNS configuration:**
1. Click on the server.
2. Open the Services tab.
3. Select DNS.
4. Turn the DNS service On.
5. Add the following DNS record (name, type A, server IP).
6. Click Add to save the DNS record.

**Email configuration:**
1. Open the server, Services, Email.
2. Turn the email service ON.
3. Set the domain name.
4. Add two email users.
5. Click Add after creating each user.

**Email client configuration:**
1. Open PC0, Desktop, Email.
2. Enter the details.
3. Click Save.

## Clear values to use

**DNS record:** Name `www.example.com`, Type A Record, Address = server IP (192.168.1.2, or .10 in the PDF version), click Add.
**Test:** PC0 Command Prompt `ping www.example.com` (should resolve to the server IP) or Desktop, Web Browser, `http://www.example.com` (enable HTTP on the server and edit its page if needed).

**Email (server):** Services, EMAIL: turn SMTP and POP3 On; Domain Name `example.com`, click Set; add users, e.g. `user1` / `pass1` and `user2` / `pass2` (the PDF uses `nakul` / `123` and `student` / `123`), clicking **+** after each. Addresses become `user1@example.com`, `user2@example.com`.

**Email (client):** Desktop, Email, Configure Mail:
| Field | Value (example) |
|---|---|
| Display / Your Name | User 1 |
| Email Address | user1@example.com |
| Incoming Mail Server | server IP (or domain) |
| Outgoing Mail Server | server IP (or domain) |
| User Name | user1 |
| Password | pass1 |
Repeat on PC1 with user2.

**Send and receive:** PC0, Desktop, Email, Compose; To: `user2@example.com`; Subject: CN Practical Test; type a message; **Send**. On PC1, Desktop, Email, click **Receive**; the mail appears.

## Result
Successfully implemented DNS and email services using Cisco Packet Tracer.

## Viva
- What does DNS do and which port does it use? (Resolves names to IPs; port 53.)
- **Which protocol sends email?** SMTP. **Which receives?** POP3 or IMAP.
- **What is an MX record?** DNS record identifying the mail servers of a domain.
- Why does the PC need the DNS server address?
- Record type that maps a name to IPv4 (A record).
