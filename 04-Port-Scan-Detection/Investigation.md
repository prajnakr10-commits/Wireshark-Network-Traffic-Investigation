# TCP Port Scan Detection Using Wireshark and Nmap

## Objective
Investigate TCP SYN port-scanning behavior using Nmap and Wireshark, and correlate TCP packet responses with port states.

## Tools Used
- Wireshark 4.6.9
- Nmap 7.992
- Windows 10
- Npcap loopback capture adapter

## Lab Environment
- Target IP: 127.0.0.1
- Scan Type: TCP SYN Scan (-sS)
- Target Ports: 80, 135, 445, 3389
- Environment: Authorized local Windows lab

## Nmap Command
```bash
nmap -sS -Pn -n -p 80,135,445,3389 127.0.0.1
```

## Wireshark Display Filters
```text
ip.addr == 127.0.0.1 && tcp

tcp.flags.syn == 1 && tcp.flags.ack == 0

tcp && ip.addr == 127.0.0.1 && (tcp.port == 80 || tcp.port == 135 || tcp.port == 445 || tcp.port == 3389)
```

## Confirmed Nmap Results

| Port | Service Label | State |
|---|---|---|
| 80/tcp | HTTP | Closed |
| 135/tcp | MSRPC | Open |
| 445/tcp | Microsoft-DS | Open |
| 3389/tcp | RDP | Closed |

Service names are standard port labels, not independently verified application versions.

## Packet Analysis

| Packet | Observation |
|---|---|
| 4655 | SYN probe to port 3389 |
| 4656 | RST, ACK response |
| 4657 | SYN probe to port 445 |
| 4658 | SYN, ACK response |
| 4659 | SYN probe to port 80 |
| 4661 | RST, ACK response |
| 4662 | SYN probe to port 135 |
| 4663 | SYN, ACK response |

## SOC Investigation Findings
Multiple TCP SYN probes targeting different destination ports were observed on the loopback interface.

Ports 135 and 445 responded with SYN-ACK packets, indicating open ports.

Ports 80 and 3389 returned connection-reset responses, consistent with closed ports.

## Security Analysis
Multiple SYN connection attempts to different destination ports can indicate port scanning or network reconnaissance.

Similar patterns can also occur during authorized vulnerability assessments or network troubleshooting.

## SOC Conclusion
The observed traffic was generated during an authorized local Nmap port-scanning exercise.

Classification: Benign Positive — Authorized Security Testing.

No malicious activity was established.

## Evidence
Wireshark SYN packet screenshots, TCP response screenshots, and Nmap scan results are included in this directory.
