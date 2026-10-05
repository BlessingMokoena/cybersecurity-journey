# Networking Basics

## Introduction

Networking is the foundation of cybersecurity and penetration testing. Before I can understand how attackers discover and interact with systems, I need to understand how devices communicate with each other.

In this section I am learning:

* IP addresses
* MAC addresses
* TCP
* UDP
* Ports
* Packets
* Sockets
* Basic networking commands on Windows and Linux

---

# 1. IP Addresses

An **IP address** is a logical address used to identify a device or network interface on an IP network.

Example:

```text
192.168.1.25
```

An IP address helps network traffic determine where data should be delivered.

There are two main versions:

* IPv4 — for example, `192.168.1.25`
* IPv6 — for example, `2001:db8::1`

For now, I am focusing mainly on IPv4.

### Simple way to remember it

> **IP address = where the device is on the network**

For example:

```text
192.168.1.25
```

can identify my computer on my local network.

---

# 2. MAC Addresses

A **MAC address** is an address associated with a network interface and is used at the Data Link layer (Layer 2).

Example:

```text
A4:5E:60:12:AB:91
```

MAC addresses are important for communication on the local network.

For example, when devices communicate through Ethernet or Wi-Fi, MAC addresses are involved in local network delivery.

### Simple way to remember it

> **MAC address = network interface identity on the local network**

A computer can have different network interfaces, such as:

* Ethernet
* Wi-Fi
* Bluetooth

Each network interface can have its own MAC address.

---

# 3. IP Address vs MAC Address

The main difference is the level at which they operate.

| IP Address                                            | MAC Address                            |
| ----------------------------------------------------- | -------------------------------------- |
| Logical address                                       | Link-layer address                     |
| Layer 3                                               | Layer 2                                |
| Used for routing between networks                     | Used mainly for local network delivery |
| Example: `192.168.1.25`                               | Example: `A4:5E:60:12:AB:91`           |
| Associated with an IP interface/network configuration | Associated with a network interface    |

### Simple mental model

> **IP = where**
> **MAC = which local network interface**

---

# 4. TCP

**TCP (Transmission Control Protocol)** operates at the Transport layer (Layer 4).

TCP is connection-oriented and provides mechanisms for reliable, ordered delivery of data.

TCP uses a three-way handshake to establish a connection.

```text
Client                         Server

   SYN ------------------------>

       <------------------------ SYN/ACK

   ACK ------------------------>

          Connection established
```

After the connection is established, data can be exchanged.

TCP provides features such as:

* Reliable delivery
* Ordered delivery
* Error detection
* Retransmission of lost data
* Flow control
* Connection management

### Common TCP services

Examples include:

```text
22/tcp     SSH
80/tcp     HTTP
443/tcp    HTTPS
445/tcp    SMB
3389/tcp   RDP
```

TCP is extremely important in penetration testing because many network services use TCP.

---

# 5. UDP

**UDP (User Datagram Protocol)** also operates at the Transport layer.

Unlike TCP, UDP does not establish a TCP-style connection before sending data.

UDP is:

* Connectionless
* Lightweight
* Faster in some situations
* Without built-in guarantees of delivery
* Without TCP-style retransmission and ordering

Examples of services that can use UDP include DNS and many real-time applications.

### Simple comparison

```text
TCP
↓
Connection-oriented
Reliable
Ordered
More overhead

UDP
↓
Connectionless
No built-in delivery guarantee
No TCP-style ordering
Less overhead
```

It is important not to think of UDP simply as "fast" and TCP as "slow". The important difference is how they provide transport.

---

# 6. Ports

A **port** identifies a network service or application endpoint on a host.

An IP address helps identify the host, while a port helps identify the service that network traffic is intended for.

For example:

```text
192.168.1.50:443
```

Here:

```text
IP address = 192.168.1.50
Port       = 443
```

Port `443` is commonly associated with HTTPS.

### Common ports

| Port | Common service |
| ---: | -------------- |
|   22 | SSH            |
|   25 | SMTP           |
|   53 | DNS            |
|   80 | HTTP           |
|  443 | HTTPS          |
|  445 | SMB            |
| 3389 | RDP            |

Ports are extremely important in penetration testing.

When I eventually use Nmap, I may see:

```text
22/tcp    open    ssh
80/tcp    open    http
443/tcp   open    https
```

This tells me that the target has services listening on those ports.

This leads to an important pentesting concept:

> **Port scanning helps identify exposed services.**

---

# 7. Packets

Data sent across a network is divided into smaller units.

At the Network layer, these units are commonly called **packets**.

For example:

```text
Large amount of data
        ↓
   Packet 1
   Packet 2
   Packet 3
   Packet 4
```

Different OSI layers use different terminology.

A simplified view is:

```text
Application data
       ↓
TCP segment
       ↓
IP packet
       ↓
Ethernet frame
       ↓
Bits
```

Therefore:

* Transport layer → segments/datagrams
* Network layer → packets
* Data Link layer → frames
* Physical layer → bits/signals

The exact terminology can vary depending on the protocol.

---

# 8. Sockets

A **socket** represents an endpoint for network communication.

A useful simplified way to think about a network endpoint is:

```text
IP address + port + transport protocol
```

For example:

```text
192.168.1.50:443/TCP
```

means:

```text
Host:     192.168.1.50
Port:     443
Protocol: TCP
```

A connection could look conceptually like:

```text
Client                              Server

192.168.1.20:51532  ───────────→  192.168.1.50:443
              TCP connection
```

The client uses an ephemeral port (`51532` in this example), while the server is listening on port `443`.

---

# 9. IP Address vs MAC Address vs Port

This is one of the most important concepts from this section.

### IP address

Identifies a host/interface at the network layer and allows traffic to be routed between networks.

```text
192.168.1.50
```

Think:

> **Where is the device?**

### MAC address

Identifies a network interface at the Data Link layer and is used for local network communication.

```text
A4:5E:60:12:AB:91
```

Think:

> **Which local network interface?**

### Port

Identifies a service/application endpoint on a host.

```text
443
```

Think:

> **Which service?**

### Putting them together

```text
192.168.1.50:443
```

means:

```text
192.168.1.50 → destination host
443           → destination service
```

The MAC address is used when delivering the traffic across the local network.

---

# 10. Windows Networking Practice

I can practice basic networking using Windows PowerShell or Command Prompt.

## ipconfig

Run:

```powershell
ipconfig
```

This shows basic network configuration.

For more detailed information:

```powershell
ipconfig /all
```

Important information to look for:

* IPv4 address
* Subnet mask
* Default gateway
* DNS servers
* Physical/MAC address

---

## ping

I can test connectivity using:

```powershell
ping 8.8.8.8
```

I can also test a hostname:

```powershell
ping google.com
```

When I ping a hostname, the system needs to resolve that hostname to an IP address before communicating with the destination.

`ping` commonly uses ICMP Echo Request and Echo Reply messages.

---

## tracert

Windows uses:

```powershell
tracert google.com
```

`tracert` shows the network hops between my computer and the destination.

A simplified path could look like:

```text
My computer
     ↓
Home router
     ↓
ISP
     ↓
Other routers
     ↓
Destination network
```

Some hops may display:

```text
*
* 
*
```

This does not necessarily mean the route is broken. A router may simply not respond to the traceroute probes.

---

# 11. Linux Networking Practice

Linux provides several useful networking commands.

## ip addr

Run:

```bash
ip addr
```

This displays network interfaces and their IP addresses.

I can use it to identify:

* Network interfaces
* IPv4 addresses
* IPv6 addresses
* Interface status
* MAC addresses

---

## ip route

Run:

```bash
ip route
```

This displays the routing table.

It helps me understand where my computer sends traffic.

For example, I may see a default route:

```text
default via 192.168.1.1
```

This means traffic that does not have a more specific route can be sent through the gateway `192.168.1.1`.

---

## ping

Linux also uses:

```bash
ping 8.8.8.8
```

or:

```bash
ping google.com
```

This can be used to test network reachability.

---

## traceroute

Linux commonly uses:

```bash
traceroute google.com
```

This performs a similar general function to Windows `tracert` by showing network hops toward a destination.

Some Linux distributions may require the `traceroute` package to be installed first.

---

# 12. Networking and the OSI Model

These concepts connect directly to what I learned about the OSI model.

```text
Layer 4 — Transport
    ↓
TCP / UDP
Ports

Layer 3 — Network
    ↓
IP
Packets
Routing

Layer 2 — Data Link
    ↓
MAC addresses
Frames

Layer 1 — Physical
    ↓
Bits
Signals
Cables / Wi-Fi
```

This helps me understand how the different pieces work together.

---

# 13. Pentesting Connection

Networking knowledge is essential for penetration testing.

A simplified pentesting process might look like:

```text
Target IP
   ↓
Discover the host
   ↓
Scan ports
   ↓
Identify services
   ↓
Identify versions
   ↓
Research vulnerabilities
   ↓
Test vulnerabilities
   ↓
Document findings
```

For example:

```text
192.168.1.50
      ↓
Port 22 open
      ↓
SSH detected
      ↓
Identify SSH version
      ↓
Research potential vulnerabilities
```

This is why understanding IP addresses, ports, TCP, UDP and network communication is important before moving into tools such as Nmap.

---

# 14. My Understanding

### IP Address

An IP address is a logical address that identifies a device/interface on a network and allows traffic to be routed toward it.

### MAC Address

A MAC address identifies a network interface at the Data Link layer and is used mainly for communication on the local network.

### Port

A port identifies a service or application endpoint on a host.

### Simple memory trick

```text
IP     = Which host?
MAC    = Which local interface?
Port   = Which service?
```

---

# 15. Practical Exercise

On Windows, I should run:

```powershell
ipconfig /all
ping 8.8.8.8
ping google.com
tracert google.com
```

I should record:

* My IPv4 address
* My default gateway
* My MAC/Physical Address
* Whether `ping 8.8.8.8` succeeds
* Whether `ping google.com` succeeds
* How many hops `tracert google.com` shows

I should not publish my real public IP address, MAC address, or other sensitive network information on GitHub.

---

# Key Takeaways

```text
IP address
→ Identifies a host/interface at Layer 3
→ Used for routing
→ Example: 192.168.1.50

MAC address
→ Identifies a network interface at Layer 2
→ Important for local network delivery
→ Example: A4:5E:60:12:AB:91

Port
→ Identifies a service/application endpoint
→ Example: 443 = HTTPS

TCP
→ Connection-oriented transport
→ Reliable and ordered

UDP
→ Connectionless transport
→ Lightweight, without TCP's built-in reliability mechanisms

Packet
→ Network-layer unit of data

Socket
→ Network communication endpoint, commonly thought of as IP + port + protocol
```

## Next Goal

The next step is to become comfortable with **network enumeration**.

I should eventually be able to look at:

```text
192.168.1.50
```

and think:

> "That's the host."

Then:

```text
192.168.1.50:22
192.168.1.50:80
192.168.1.50:443
```

and think:

> "Those are services exposed by that host."

That is the foundation for learning **Nmap and network enumeration**.
