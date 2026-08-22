# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

## Objective

Today I strengthened my networking fundamentals by learning how DNS works, understanding IP addressing, CIDR notation, subnetting, and common network ports used in Linux and cloud environments.

I practiced these concepts on an AWS EC2 Ubuntu server using real networking commands.

---

## DNS, IP, Subnets & Ports

Today I worked with:

- DNS Resolution
- IPv4 & IPv6
- Public vs Private IPs
- CIDR & Subnetting
- Linux networking commands
- Common network ports
- AWS EC2 networking

---

## Task 1 – DNS: How Names Become IPs

### What happens when I type `google.com` in a browser?

1. My system sends a DNS request to a DNS resolver.
2. The resolver finds the IP address of `google.com`.
3. The browser receives the IP address.
4. It connects to Google's server using TCP/IP and loads the webpage.

### Common DNS Record Types

| Record | Purpose |
|--------|---------|
| A | Maps a domain to an IPv4 address |
| AAAA | Maps a domain to an IPv6 address |
| CNAME | Creates an alias for another domain |
| MX | Specifies mail servers for a domain |
| NS | Identifies authoritative name servers |

### DNS Lookup

Command:

```bash
dig google.com
```

Output:

```text
google.com. 199 IN A 172.217.19.238
```

- **A Record:** `172.217.19.238`
- **TTL:** `199`

I also checked the IPv6 record:

```bash
getent hosts google.com
```

Output:

```text
2a00:1450:400f:807::200e google.com
```

### Observation

My EC2 server successfully resolved both IPv4 and IPv6 addresses for Google.

---

## Task 2 – IP Addressing

### What is an IPv4 Address?

An IPv4 address is a **32-bit numeric address** written as four decimal numbers separated by dots.

Example:

```text
192.168.1.10
```

### Public vs Private IP

| Type | Example |
|------|---------|
| Public | 8.8.8.8 |
| Private | 172.31.33.72 |

### Private IP Ranges

- `10.0.0.0/8`
- `172.16.0.0 – 172.31.255.255`
- `192.168.0.0/16`

### My EC2 Network Information

Command:

```bash
ip addr show
```

I identified these addresses:

| Interface | IP Address | Type |
|-----------|------------|------|
| ens5 | `172.31.33.72/20` | AWS Private IP |
| docker0 | `172.17.0.1/16` | Docker Bridge Network |
| lo | `127.0.0.1` | Loopback |

### Observation

- `172.31.33.72` belongs to AWS's private VPC network.
- `172.17.0.1` is Docker's internal bridge network.
- `127.0.0.1` is the local loopback address.

---

## Task 3 – CIDR & Subnetting

### What does `/24` mean?

`/24` means the first **24 bits** are reserved for the network, leaving **8 bits** for host addresses.

### Why do we subnet?

Subnetting divides large networks into smaller networks, making them easier to manage, more secure, and more efficient.

### CIDR Table

| CIDR | Subnet Mask | Total IPs | Usable Hosts |
|------|-------------|-----------|--------------|
| /24 | 255.255.255.0 | 256 | 254 |
| /16 | 255.255.0.0 | 65,536 | 65,534 |
| /28 | 255.255.255.240 | 16 | 14 |

---

## Task 4 – Ports: The Doors to Services

### What is a Port?

A port is a communication endpoint that allows multiple services to run on the same IP address.

### Common Ports

| Port | Service |
|------|---------|
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 53 | DNS |
| 3306 | MySQL |
| 6379 | Redis |
| 27017 | MongoDB |

### Listening Ports on My Server

Command:

```bash
ss -tulpn
```

I identified these active services:

| Port | Service |
|------|---------|
| 22 | SSH |
| 80 | Nginx |
| 53 | Local DNS Resolver |
| 68 | DHCP Client |

### Observation

- SSH is actively listening on **port 22**.
- Nginx is serving web traffic on **port 80**.
- The local DNS resolver is listening on **port 53**.

---

## Task 5 – Putting It Together

### Scenario 1

Command:

```bash
curl http://myapp.com:8080
```

Networking concepts involved:

- DNS resolves `myapp.com`.
- TCP establishes a connection.
- IP routes the traffic.
- HTTP communicates with the application on **port 8080**.

### Scenario 2

Database:

```text
10.0.1.50:3306
```

The first things I would check are:

- Network connectivity.
- Whether MySQL is listening on port **3306**.
- Firewall or AWS Security Group rules.
- DNS (if using a hostname).

---

## Commands Used

```bash
dig google.com
```

```bash
getent hosts google.com
```

```bash
ip addr show
```

```bash
ss -tulpn
```

---

## What I Learned

- DNS converts domain names into IP addresses using records like A and AAAA.
- AWS EC2 instances use private IP addresses inside a VPC.
- CIDR notation determines network size and available hosts.
- Ports allow multiple services to communicate over the same IP address.
- Commands like `dig`, `ip addr show`, and `ss -tulpn` are essential for networking troubleshooting.

---

## DevOps Takeaway

Networking is one of the most important foundations in DevOps. Before assuming an application is broken, I can follow a simple troubleshooting flow:

1. Verify the IP address.
2. Check DNS resolution.
3. Confirm network connectivity.
4. Verify listening ports.
5. Test the application endpoint.

This structured approach helps quickly identify whether an issue is related to DNS, networking, or the application itself.

---

## Evidence

Screenshots collected during this exercise:

- `dns-lookup.png`
- `ip-address.png`
- `listening-ports.png`

---

## Day 15 Summary

Today I built a stronger networking foundation by understanding DNS resolution, IP addressing, CIDR notation, subnetting, and common ports while validating these concepts using real Linux networking commands on my AWS EC2 server.
