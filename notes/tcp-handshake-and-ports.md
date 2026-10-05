# TCP Handshake, TCP vs UDP, and Why Attackers Care About Ports

## Introduction

In my previous networking notes, I learned about IP addresses, MAC addresses, ports, TCP, UDP, packets, and sockets.

In this section I am going deeper into **TCP** and understanding how a TCP connection is established.

I am learning:

* TCP three-way handshake
* SYN
* SYN-ACK
* ACK
* TCP vs UDP
* Why attackers care about ports

---

# 1. What is TCP?

**TCP (Transmission Control Protocol)** is a Transport Layer (Layer 4) protocol.

TCP is designed to provide reliable and ordered communication between applications.

Before TCP normally starts transferring application data, the two endpoints establish a connection.

This process is called the:

> **TCP three-way handshake**

The three main steps are:

```text
SYN
SYN-ACK
ACK
```

---

# 2. TCP Three-Way Handshake

The handshake allows the client and server to establish a TCP connection and synchronize their initial sequence numbers.

A simplified example:

```text
Client                              Server

   SYN ---------------------------->

       <---------------------------- SYN-ACK

   ACK ---------------------------->

          TCP connection established
```

After this process, the endpoints can begin exchanging application data.

---

# 3. Step 1 — SYN

The client sends a **SYN** packet to the server.

SYN means:

> **Synchronize**

The client is essentially saying:

> "I want to establish a TCP connection with you."

The SYN contains an initial sequence number.

Simplified:

```text
Client                         Server

SYN -------------------------->
```

The client is now waiting for a response.

---

# 4. Step 2 — SYN-ACK

The server receives the SYN and responds with:

```text
SYN + ACK
```

This is called **SYN-ACK**.

The server is essentially saying:

> "I received your request, and I also want to establish this connection."

Simplified:

```text
Client                         Server

SYN -------------------------->

    <-------------------------- SYN-ACK
```

The server also provides its own initial sequence number.

---

# 5. Step 3 — ACK

The client receives the SYN-ACK and sends an **ACK**.

ACK means:

> **Acknowledgment**

The client is saying:

> "I received your response."

Simplified:

```text
Client                         Server

SYN -------------------------->

    <-------------------------- SYN-ACK

ACK -------------------------->
```

The TCP connection is now established.

The endpoints can begin exchanging data.

---

# 6. Remembering SYN, SYN-ACK and ACK

A simple way to remember the process is:

```text
SYN
↓
"Can we connect?"

SYN-ACK
↓
"Yes, I received you and I'm ready."

ACK
↓
"Confirmed."
```

Or simply:

```text
Client → SYN → Server
Client ← SYN-ACK ← Server
Client → ACK → Server
```

Then:

```text
Connection established
        ↓
Data transmission
```

---

# 7. Why Does TCP Need a Handshake?

The handshake helps both sides establish the connection and synchronize their sequence numbers.

TCP needs to keep track of data so that it can provide reliable, ordered communication.

For example, if data is sent:

```text
Segment 1
Segment 2
Segment 3
Segment 4
```

TCP can detect when something is missing and use acknowledgements and retransmission mechanisms to help recover lost data.

This is one of the major differences between TCP and UDP.

---

# 8. TCP vs UDP

Both TCP and UDP operate at the Transport layer.

However, they work differently.

| TCP                                        | UDP                               |
| ------------------------------------------ | --------------------------------- |
| Connection-oriented                        | Connectionless                    |
| Uses a handshake to establish a connection | No TCP-style handshake            |
| Reliable delivery mechanisms               | No built-in guarantee of delivery |
| Ordered data                               | No TCP-style ordering guarantee   |
| Uses acknowledgements                      | No TCP-style acknowledgements     |
| Retransmits lost data                      | No TCP-style retransmission       |
| More overhead                              | Less overhead                     |

### TCP

TCP is useful when reliability and ordered delivery are important.

Examples include:

```text
SSH
HTTP/1.1
HTTPS over TCP
SMB
RDP
```

### UDP

UDP is useful when low overhead and speed are important, and the application can tolerate or handle loss in its own way.

Examples include:

```text
DNS
DHCP
Some streaming/real-time applications
```

Modern protocols can also use UDP for reliable higher-level protocols. For example, **HTTP/3 uses QUIC over UDP**.

Therefore, I should not simply think:

> TCP = reliable, UDP = unreliable

A better understanding is:

> TCP provides transport-level connection management, ordering, acknowledgements and retransmission mechanisms, while UDP provides a simpler connectionless transport and leaves reliability, if needed, to the application or another protocol.

---

# 9. Visualizing TCP vs UDP

A simple way to think about the difference:

```text
TCP

Client                         Server

Connection setup
     SYN -------------------->
         <------------------- SYN-ACK
     ACK -------------------->

Data ------------------------>
         <------------------- ACK

Data ------------------------>
         <------------------- ACK
```

TCP keeps track of communication and acknowledgements.

UDP is simpler:

```text
UDP

Client                         Server

Data ------------------------>

Data ------------------------>

Data ------------------------>

Data ------------------------>
```

There is no TCP-style connection establishment or acknowledgement mechanism built into UDP.

---

# 10. Why Attackers Care About Ports

This is especially important for penetration testing.

A computer can have many network services running.

For example:

```text
Target
192.168.1.50

22    SSH
80    HTTP
443   HTTPS
445   SMB
3389  RDP
```

The **IP address** helps identify the host.

The **port** helps identify where a network service is listening.

Therefore, an attacker performing authorized reconnaissance may ask:

> "Which ports are open?"

Then:

> "What services are running on those ports?"

Then:

> "What versions are those services running?"

Then:

> "Are those services vulnerable or misconfigured?"

This is called **enumeration**.

---

# 11. Open Ports Increase the Attack Surface

An open port does **not automatically mean the system is vulnerable**.

It means that a service is listening and potentially reachable over the network.

For example:

```text
192.168.1.50:22
```

might indicate an SSH service.

The next questions could be:

```text
What SSH software?
↓
What version?
↓
Is it configured securely?
↓
Is authentication secure?
↓
Are there known vulnerabilities?
```

Another example:

```text
192.168.1.50:445
```

could indicate SMB.

A penetration tester might then investigate:

* What SMB version is being used?
* Is SMB exposed unnecessarily?
* Is authentication configured securely?
* Are there known vulnerabilities?
* Are there dangerous shares or permissions?

The important lesson is:

> **A port is not the vulnerability. The service behind the port is what needs to be investigated.**

---

# 12. Ports as Doors

A useful mental model is to think of ports as doors into a building.

```text
                SERVER
          192.168.1.50
                 |
       -----------------------
       |    |     |     |    |
      22   53    80    443  445
       |    |     |     |    |
      SSH  DNS   HTTP HTTPS SMB
```

Each open port can potentially expose a service.

From a security perspective:

```text
Open port
    ↓
Service exposed
    ↓
Identify service
    ↓
Identify version
    ↓
Check configuration
    ↓
Look for vulnerabilities
```

Again:

> **Open does not automatically mean vulnerable.**

---

# 13. Why Port Scanning Matters

A penetration tester cannot effectively test a network service if they don't know that the service exists.

Port scanning helps identify accessible services.

For example, an Nmap scan might eventually show:

```text
PORT     STATE    SERVICE

22/tcp   open     ssh
80/tcp   open     http
443/tcp  open     https
```

Now I have information about the target's attack surface.

I can investigate each service further.

This is why **Nmap** will become an important tool later in my learning.

---

# 14. TCP Flags

TCP uses flags to communicate different control information.

Some important TCP flags include:

| Flag | Meaning                             |
| ---- | ----------------------------------- |
| SYN  | Synchronize/start connection        |
| ACK  | Acknowledgment                      |
| FIN  | Finish/close connection             |
| RST  | Reset connection                    |
| PSH  | Push data to the application        |
| URG  | Urgent pointer field is significant |

For the TCP three-way handshake, the most important flags are:

```text
SYN
SYN-ACK
ACK
```

---

# 15. Connection to My OSI Model Notes

This connects directly to what I learned about the OSI model.

```text
Layer 4 — Transport
        ↓
       TCP
       UDP
       Ports

Layer 3 — Network
        ↓
        IP
      Packets

Layer 2 — Data Link
        ↓
       MAC
      Frames
```

So when I see:

```text
192.168.1.50:443
```

I can break it down as:

```text
192.168.1.50
      ↓
IP address
Layer 3

443
 ↓
Port
Layer 4

TCP
 ↓
Transport protocol
Layer 4
```

---

# 16. Pentesting Perspective

As a future penetration tester, I need to think about network communication from the perspective of both the defender and attacker.

A simplified process is:

```text
Find host
   ↓
Find open ports
   ↓
Identify services
   ↓
Identify versions
   ↓
Understand configurations
   ↓
Identify vulnerabilities
   ↓
Test vulnerabilities
   ↓
Document findings
```

For example:

```text
Target:
192.168.1.50

Port:
80/tcp

Service:
HTTP

Next questions:
What web server?
What version?
What website?
What technologies?
Are there vulnerabilities?
```

This is why learning TCP, UDP and ports before learning Nmap is important.

I don't want to blindly run tools.

I want to understand **what the tool is actually showing me**.

---

# 17. Key Takeaways

### TCP

> A connection-oriented Transport Layer protocol that provides reliable, ordered communication mechanisms.

### SYN

> Used to initiate a TCP connection and synchronize sequence numbers.

### SYN-ACK

> The server's response acknowledging the SYN and sending its own SYN.

### ACK

> Acknowledges the server's response and completes the normal three-way handshake.

### TCP vs UDP

```text
TCP
→ Connection-oriented
→ Reliable delivery mechanisms
→ Ordered communication
→ Handshake
→ Acknowledgements
→ Retransmission

UDP
→ Connectionless
→ Less overhead
→ No TCP-style handshake
→ No TCP-style acknowledgement/retransmission mechanism
```

### Ports

> Ports identify service/application endpoints on a host.

### Why attackers care about ports

> Open ports reveal potentially accessible services. Attackers and penetration testers can enumerate those services to understand the target's attack surface and identify possible vulnerabilities or misconfigurations.

---

# My Mental Model

I want to remember the process like this:

```text
IP address
    ↓
Find the host
    ↓
Port
    ↓
Find the service
    ↓
TCP/UDP
    ↓
Understand how communication happens
    ↓
Service/version
    ↓
Look for vulnerabilities
```

The goal is not just to memorize:

```text
SYN
SYN-ACK
ACK
```

The goal is to understand what is happening when two systems communicate.

That understanding will become important when I start learning **Nmap, Wireshark, network enumeration, and eventually network penetration testing**.
