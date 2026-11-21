# Experiment 06: DNS Commands Using Terminal

## 1. Experiment Title
Demonstration and Analysis of DNS and Network Diagnostic Commands Using the Terminal.

---

## 2. Aim
To study the architecture of the Domain Name System (DNS) and examine terminal diagnostic commands including `nslookup`, `ping`, `ipconfig`, and `tracert` on Windows and Linux environments for forward DNS resolution, reverse DNS resolution (PTR), local DNS cache inspection, network interface configuration, and ICMP connectivity analysis.

---

## 3. Theory / Introduction
The Domain Name System (DNS) is a hierarchical, decentralized naming system that maps human-friendly Fully Qualified Domain Names (FQDNs), such as `www.google.com` or `sitnagpur.edu.in`, into machine-routable IP addresses (such as `142.251.156.119` or `13.204.121.160`).

### 3.1 DNS Hierarchy and Resolution Flow

```
                         [ Root DNS Servers (.) ]
                                     |
                       [ TLD DNS Servers (.edu / .com / .in) ]
                                     |
              [ Authoritative DNS Servers (sitnagpur.edu.in) ]
                                     ^
                                     | (Recursive Queries)
                            [ Local DNS Resolver ]
                              (e.g., 10.17.28.42)
                                     ^
                                     | (Query: sitnagpur.edu.in)
                               [ Client Host ]
```

### 3.2 DNS Record Types
- **A Record (Address):** Maps an FQDN to an IPv4 address (32-bit).
- **AAAA Record (IPv6 Address):** Maps an FQDN to an IPv6 address (128-bit).
- **CNAME (Canonical Name):** Creates an alias mapping one domain name to another domain name.
- **PTR (Pointer):** Resolves an IP address to a canonical hostname in reverse lookups (`in-addr.arpa`).
- **MX (Mail Exchanger):** Specifies mail servers responsible for accepting email for the domain.
- **NS (Name Server):** Delegates a DNS zone to use specific authoritative name servers.
- **SOA (Start of Authority):** Contains administrative information about the zone.

### 3.3 Core Network Diagnostic Commands

#### 1. `nslookup` (Name Server Lookup)
A cross-platform network administration command-line tool used for querying DNS servers to obtain domain name or IP address mappings.
- **Forward Lookup:** Queries for an IP address corresponding to a hostname (`nslookup <domain-name>`).
- **Reverse Lookup:** Queries for a hostname associated with an IP address using the PTR record (`nslookup <ip-address>`).
- **Non-Authoritative Answer:** An answer returned by a caching or recursive server that does not hold the primary master zone file for the queried domain.

#### 2. `ping` (Packet Internet Groper)
Uses Internet Control Message Protocol (ICMP) **Echo Request (Type 8)** and **Echo Reply (Type 0)** packets to verify network-layer connectivity and measure round-trip time (RTT) and packet loss.
- In Windows: Defaults to sending 4 echo requests of 32 bytes each.
- Key options:
  - `-t`: Pings the target host continuously until interrupted with `Ctrl + C`.
  - `-a`: Resolves IP address to hostname.
  - `-n count`: Number of echo requests to send.
  - `-l size`: Size of send buffer payload in bytes.
  - `-i TTL`: Sets Time to Live in the IP header.

#### 3. `ipconfig` (Windows) / `ip` or `ifconfig` (Linux)
Displays all current TCP/IP network configuration values, refreshes DHCP settings, and manages local DNS resolver cache:
- `ipconfig /all`: Displays full configuration (MAC address, IP, Subnet Mask, Default Gateway, DNS Servers, DHCP status).
- `ipconfig /flushdns`: Purges and resets the local DNS client resolver cache.
- `ipconfig /displaydns`: Displays contents of the local DNS client cache.

#### 4. `tracert` (Windows) / `traceroute` (Linux)
Traces the route packets take to reach a destination host by sending packets with incrementing Time To Live (TTL) values, inducing ICMP **Time Exceeded (Type 11)** responses from each intermediary router along the path.

---

## 4. Objectives
1. Perform forward and reverse DNS queries using `nslookup`.
2. Distinguish between authoritative and non-authoritative DNS responses.
3. Inspect network adapter parameters and local DNS resolver configurations.
4. Test network latency, reachability, and packet fragmentation thresholds using `ping`.

---

## 5. Required Software and Tools
- **Operating System:** Windows 10/11 Command Prompt / PowerShell or Linux Terminal.
- **Tools:** Built-in command-line networking utilities (`nslookup`, `ping`, `ipconfig`, `tracert`).

---

## 6. Command Reference and Working Principles

| Utility | Underlying Protocol | Operating Layer | Primary Diagnostic Function |
|---|---|---|---|
| `nslookup` | DNS (UDP/TCP Port 53) | Application Layer | Forward name resolution, reverse IP lookup, DNS record inspection |
| `ping` | ICMP (IPv4 Protocol 1) | Network Layer | End-to-end reachability, RTT measurement, packet loss detection |
| `ipconfig` | DHCP / Local OS Stack | Network / Data Link | Adapter configuration, IP/MAC mapping, DNS resolver cache management |
| `tracert` | ICMP / UDP (TTL manipulation) | Network Layer | Hop-by-hop route tracing, intermediary router identification |

---

## 7. Result / Conclusion
DNS resolution and fundamental network troubleshooting utilities (`nslookup`, `ping`, `ipconfig`, `tracert`) were demonstrated. The principles of forward DNS resolution, PTR reverse lookups, IPv4/IPv6 dual-stack addressing, and ICMP connectivity analysis were verified.
