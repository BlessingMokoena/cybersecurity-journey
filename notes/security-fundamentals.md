# Security Fundamentals

## Understand the Battlefield

These are some of the fundamental cybersecurity concepts I am learning as I begin my journey toward becoming a penetration tester.

> **Learning approach:** I am first explaining each concept in my own words, then comparing my understanding with trusted cybersecurity resources and correcting anything I misunderstood.

---

# 1. Cybersecurity

### My understanding

Cybersecurity is the practice of protecting information systems, networks, applications, IoT devices and other technology from unauthorized access, attacks, damage or disruption.

This can include protecting devices such as:

* Computers
* Mobile phones
* Servers
* Routers
* Wi-Fi networks
* IoT devices
* Applications
* Cloud systems

### My understanding before further research

I initially understood cybersecurity as the principle of protecting IT/IoT devices such as mobile phones, PCs, servers and Wi-Fi networks from unauthorized access by attackers.

### What I learned

Cybersecurity is broader than simply preventing hackers from accessing devices. It also involves protecting the **confidentiality, integrity and availability** of systems and information.

---

# 2. Blue Team vs Red Team

## Blue Team

### My understanding

Blue team members are the defenders of an organization's systems.

They monitor systems and security alerts, investigate suspicious activity, respond to incidents and work to protect the organization's systems and data.

### What I learned

The Blue Team is generally associated with **defensive security operations**, including detection, monitoring, incident response and improving security controls.

---

## Red Team

### My understanding

Red team members are authorized attackers who test an organization's security defenses.

Their goal is to simulate attacks, identify weaknesses and help the organization improve its security.

### What I learned

Red teams conduct authorized adversary simulations to test how effectively an organization can prevent, detect and respond to attacks.

---

# 3. Penetration Testing

### My understanding

Penetration testing is authorized security testing where a tester attempts to identify and, where permitted, exploit vulnerabilities in a system.

The tester documents the findings and reports them to the organization so that the vulnerabilities can be fixed.

### Key idea

**Authorized testing is essential.**

A penetration test is performed with clearly defined permission and scope.

---

# 4. Vulnerability Assessment

### My understanding

A vulnerability assessment involves looking for vulnerabilities in an organization's systems and devices and determining the potential risk they could create.

### What I learned

Vulnerability assessment is primarily focused on **identifying and evaluating vulnerabilities**.

It does not necessarily mean exploiting every vulnerability.

For example:

```text
Identify vulnerability
        ↓
Determine affected system
        ↓
Assess severity
        ↓
Determine potential impact
        ↓
Recommend remediation
```

---

# 5. Exploit

### My understanding

An exploit is a method or technique used to take advantage of a vulnerability.

### What I learned

An exploit is not the vulnerability itself.

The relationship can be understood as:

```text
Vulnerability
      ↓
Weakness in a system
      ↓
Exploit
      ↓
Method that takes advantage of the weakness
```

For example, if a software application contains a vulnerability, an exploit may be developed that takes advantage of that vulnerability.

---

# 6. Common Vulnerabilities and Exposures (CVE)

### My understanding

I initially thought of CVE as a library of discovered vulnerabilities and patches for different software.

### What I learned

CVE stands for **Common Vulnerabilities and Exposures**.

A CVE is a standardized identifier assigned to a publicly known cybersecurity vulnerability.

For example:

```text
CVE-YYYY-NNNNN
```

The CVE identifier allows security professionals, vendors and researchers to refer to a specific vulnerability consistently.

### Important distinction

A CVE is **not the patch itself**.

The vulnerability can have:

* A CVE identifier
* Technical descriptions
* Affected products/versions
* Severity information
* References
* Available vendor fixes or mitigations

---

# 7. Threat

### My understanding

A threat is a potential danger to a system.

### What I learned

A threat is a potential cause of harm to a system, organization or information.

Examples can include:

* Attackers
* Malware
* Phishing
* Insider threats
* Natural events
* Exploitation attempts

A threat does not necessarily mean that an attack has already happened.

---

# 8. Risk

### My understanding

Risk is how badly an organization could be damaged or affected if an attack occurs.

### What I learned

Risk involves the potential for harm or loss when a threat can take advantage of a vulnerability.

A simplified way of thinking about it is:

```text
Threat
   +
Vulnerability
   +
Potential Impact
   =
Risk
```

Risk assessment considers factors such as:

* Likelihood
* Impact
* Asset value
* Existing security controls

---

# 9. Attack Surface

### My understanding

I initially thought of the attack surface as a radius or group of connected devices that could be exposed during an attack.

### What I learned

An organization's **attack surface** is the collection of points through which an attacker could potentially interact with or attempt to compromise its systems.

This can include:

* Internet-facing servers
* Websites
* APIs
* Open ports
* Remote-access services
* Cloud services
* Employee accounts
* Applications
* IoT devices
* Network infrastructure

### Example

An organization might have:

```text
Internet
    │
    ├── Website
    ├── VPN
    ├── Email server
    ├── API
    └── Remote-access service
```

Each exposed service can potentially contribute to the organization's attack surface.

---
