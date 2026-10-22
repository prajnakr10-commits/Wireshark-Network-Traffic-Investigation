# Wireshark Network Traffic Investigation

### SOC Analyst L1 | Network Traffic Analysis & Security Monitoring

A hands-on cybersecurity project demonstrating packet capture, network protocol analysis, TCP connection investigation, port-scan detection, and suspicious traffic analysis using Wireshark, Nmap, and Windows PowerShell.

## Project Overview

This project contains five practical network security investigations performed in a controlled lab environment. Each investigation includes the objective, methodology, display filters, packet-level observations, evidence screenshots, and SOC analyst conclusions.

## Tools and Technologies

- Wireshark 4.6.9
- Nmap 7.992
- Windows 10
- Windows PowerShell
- Npcap
- TCP/IP, DNS, HTTP, TLS

## Investigations

### 1. DNS Traffic Analysis
**Directory:** [01-DNS-Traffic-Analysis](01-DNS-Traffic-Analysis/Investigation.md)

- Captured and analyzed DNS queries and responses.
- Correlated DNS transaction ID 0xb917 across request and response packets.
- Identified domain resolution for i.instagram.com and IPv4 address 57.144.210.192.
- Investigated DNS query types, CNAME records, and response time.

### 2. TCP Three-Way Handshake Analysis
**Directory:** [02-TCP-Handshake-Analysis](02-TCP-Handshake-Analysis/Investigation.md)

- Analyzed SYN, SYN-ACK, and ACK packets.
- Correlated packets 7039, 7040, and 7042 using TCP stream 87.
- Verified TCP connection establishment to port 443.
- Observed subsequent TLS 1.3 negotiation.

### 3. HTTP Traffic Investigation
**Directory:** [03-HTTP-Traffic-Analysis](03-HTTP-Traffic-Analysis/Investigation.md)

- Inspected HTTP GET requests and 200 OK responses.
- Analyzed the /ping request and matching response.
- Identified HTTP headers, User-Agent information, and server technology disclosures.
- Correlated request packet 352 with response packet 368.

### 4. TCP Port Scan Detection
**Directory:** [04-Port-Scan-Detection](04-Port-Scan-Detection/Investigation.md)

- Generated authorized TCP SYN scans against localhost using Nmap.
- Captured SYN, SYN-ACK, and RST responses.
- Identified ports 135 and 445 as open and ports 80 and 3389 as closed in the lab.
- Correlated Nmap scan results with Wireshark packet evidence.

### 5. Repeated TCP Connection Investigation
**Directory:** [05-Repeated-TCP-Connections](05-Repeated-TCP-Connections/Investigation.md)

- Generated repeated localhost TCP connection attempts using PowerShell.
- Captured SYN and RST/ACK packets targeting TCP port 65000.
- Examined connection failures and repeated traffic patterns.
- Distinguished benign automated testing from indicators that could warrant C2 investigation.

## Wireshark Display Filters

```text
dns
dns.flags.response == 1
tcp.flags.syn == 1 && tcp.flags.ack == 0
tcp.stream == 87
http
http.request
http.response
ip.addr == 127.0.0.1 && tcp
tcp.port == 65000
tcp.dstport == 65000 && tcp.flags.syn == 1 && tcp.flags.ack == 0
```

## Skills Demonstrated

- Network packet capture and analysis
- TCP/IP, DNS, HTTP, and TLS protocol investigation
- TCP handshake and flag analysis
- HTTP request-response correlation
- Port scan detection and Nmap validation
- Investigation of repeated outbound-style connection patterns in a localhost simulation
- Security event triage and evidence documentation
- True-positive and benign-positive interpretation

## Key Findings

The DNS, TCP, and HTTP investigations demonstrated successful network communication and protocol behavior.

The Nmap investigation demonstrated controlled port-scanning behavior against localhost.

The repeated-connection investigation demonstrated failed TCP connection attempts and reset responses in an authorized simulation.

No actual malware or malicious command-and-control infrastructure was used or identified.

## Evidence

Packet analysis screenshots are available in the corresponding investigation folders. Captured traffic was generated or observed in a controlled learning environment. Evidence should be reviewed for sensitive information before public distribution.

## Disclaimer

This project is intended for cybersecurity education and defensive network traffic analysis. Active scans were limited to an authorized local system. Observed packet patterns alone should not be treated as conclusive evidence of malicious behavior.
