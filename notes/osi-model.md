#  OSI Model

## Objective

Understand the seven layers of the OSI model instead of simply memorising their names.

The OSI model helps me understand how data moves between devices across a network and what happens at each stage of communication.

---

# The 7 Layers

| Layer | Name         | My focus                                                |
| ----- | ------------ | ------------------------------------------------------- |
| 7     | Application  | Applications and network services                       |
| 6     | Presentation | Data format, encryption and compression                 |
| 5     | Session      | Starting, maintaining and ending communication sessions |
| 4     | Transport    | Reliable or fast delivery using TCP or UDP              |
| 3     | Network      | IP addressing and routing                               |
| 2     | Data Link    | Frames and local network communication                  |
| 1     | Physical     | Bits, signals and physical connections                  |

---

# 7 — Application Layer

### My understanding

The Application layer is the layer closest to the software and services that we interact with on our devices.

Examples include:

* Email applications
* Web browsers
* Web services
* DNS
* HTTP/HTTPS
* FTP

For example, when I use a web browser to access a website, the application layer is involved in the network services that allow the browser to communicate with the web server.

### Simple way I remember it

> **Application = Where network services interact with applications.**

---

# 6 — Presentation Layer

### My understanding

The Presentation layer deals with how data is represented so that it can be understood and processed by the receiving system.

It can be associated with:

* Data formatting
* Encoding
* Encryption and decryption
* Compression and decompression

The important idea for me is that this layer deals with the **format and representation of data**.

For example, data may need to be converted into a format that the receiving application can understand.

### Simple way I remember it

> **Presentation = How the data is represented.**

---

# 5 — Session Layer

### My understanding

The Session layer is responsible for establishing, managing and terminating communication sessions between systems.

It helps manage a communication session so that two systems can communicate for a period of time.

It can be thought of as managing:

```
Start session
     ↓
Maintain session
     ↓
Communication
     ↓
Terminate session
```

### Simple way I remember it

> **Session = Manages the conversation.**

---

# 4 — Transport Layer

### My understanding

The Transport layer is responsible for delivering data between applications on different devices.

Two important transport protocols are:

* TCP
* UDP

TCP focuses on reliable delivery. It establishes a connection and uses mechanisms such as acknowledgements and retransmissions.

UDP is connectionless and generally provides faster communication with less overhead, but it does not provide the same delivery guarantees as TCP.

The Transport layer also works with **segments** when discussing TCP and **datagrams** when discussing UDP.

### Simple way I remember it

> **Transport = How data is delivered between applications.**

---

# 3 — Network Layer

### My understanding

The Network layer deals with logical addressing and routing.

This is where **IP addresses** are important.

The source IP address identifies where the packet came from, while the destination IP address identifies where the packet needs to go.

Routers operate primarily at this layer because they use IP addressing to make routing decisions.

For example:

```
Source
192.168.1.10
     |
     | Packet
     ↓
  Router
     |
     ↓
Destination
8.8.8.8
```

The router examines the destination IP address and determines where to forward the packet.

### Simple way I remember it

> **Network = IP addressing and routing.**

---

# 2 — Data Link Layer

### My understanding

The Data Link layer deals with communication between devices on the same local network.

It works with **frames** and uses physical addressing such as **MAC addresses**.

For example, when devices communicate across a local Ethernet network, the Data Link layer helps deliver frames between devices on that local network.

Network switches primarily operate at this layer.

### Simple way I remember it

> **Data Link = Local network communication and frames.**

---

# 1 — Physical Layer

### My understanding

The Physical layer deals with the actual transmission of bits across a physical or wireless medium.

This can include:

* Ethernet cables
* Fibre-optic cables
* Radio signals
* Network interfaces
* Electrical signals
* Light signals
* Wireless signals

At this layer, data is represented as **bits** and transmitted through the physical medium.

For example:

```
Computer
   |
   | Electrical signals
   ↓
Ethernet cable
   |
   ↓
Switch
```

### Simple way I remember it

> **Physical = Bits and signals moving through the medium.**

---

# How the Layers Work Together

The most important thing I am learning is that the OSI model is not seven completely separate systems.

The layers work together.

When sending data, it generally moves:

```
Application
     ↓
Presentation
     ↓
Session
     ↓
Transport
     ↓
Network
     ↓
Data Link
     ↓
Physical
```

When receiving data, the process works in the opposite direction:

```
Physical
     ↓
Data Link
     ↓
Network
     ↓
Transport
     ↓
Session
     ↓
Presentation
     ↓
Application
```

---



## Important note

In a real modern web connection, the OSI model is a **conceptual model**. Actual Internet protocols do not always map perfectly to one OSI layer.

For example, modern web communication can involve:

* DNS
* TCP
* TLS
* HTTP/2 or HTTP/3
* IP
* Ethernet or Wi-Fi

So I should use the OSI model as a framework for understanding networking rather than assuming every real-world protocol fits perfectly into exactly one layer.

---

#  Example: Troubleshooting Using the OSI Model

The OSI model can also help me troubleshoot network problems.

For example, if my computer cannot connect to the network:

### Layer 1 — Physical

Check:

* Is the cable connected?
* Is Wi-Fi enabled?
* Are there link lights?

### Layer 2 — Data Link

Check:

* Is the network adapter working?
* Is the device connected to the local network?
* Are there switching or MAC-related problems?

### Layer 3 — Network

Check:

* Does the computer have an IP address?
* Is the subnet correct?
* Is the default gateway correct?
* Can I ping the gateway?

### Layer 4 — Transport

Check:

* Is the required TCP/UDP port reachable?
* Is a firewall blocking the connection?

### Layer 7 — Application

Check:

* Is the application working?
* Is DNS working?
* Is the website/service available?

This shows me that the OSI model can be used as a **troubleshooting framework**, not just something to memorise for an exam.

---

#  Commands I Can Use to Practice



### Linux

```
ip addr
```

View network interfaces and IP addresses.

```
ping 8.8.8.8
```

Test connectivity.

```
traceroute google.com
```

View the route to a destination.

```
dig google.com
```

Query DNS information.

---

# 🎯 What I Learned

The biggest lesson from the OSI model is that network communication happens through multiple stages.

I should not simply memorise:

```
7 Application
6 Presentation
5 Session
4 Transport
3 Network
2 Data Link
1 Physical
```

Instead, I should understand the role of each layer.

My current mental model is:

```
Application → What service am I using?
Presentation → How is the data represented?
Session → How is the communication session managed?
Transport → How is the data delivered?
Network → Where does the data need to go?
Data Link → How does it move across the local network?
Physical → How are the bits transmitted?
```

---

#  Key Takeaway

> **The OSI model gives me a way to break down network communication into seven conceptual layers, making it easier to understand, troubleshoot and analyze network activity.**

---

