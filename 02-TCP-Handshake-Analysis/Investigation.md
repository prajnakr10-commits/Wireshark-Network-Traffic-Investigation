# TCP Three-Way Handshake Investigation

## Objective
Analyze the TCP three-way handshake using Wireshark and verify successful connection establishment.

## Tools Used
- Wireshark 4.6.9
- Windows 10
- TCP/IP packet capture

## Investigation Environment
- Client IP: 192.168.1.145
- Destination IP: 57.144.210.192
- Source Port: 64414
- Destination Port: 443 (HTTPS)
- TCP Stream Index: 87

## Wireshark Display Filters
```wireshark
tcp.flags.syn == 1 && tcp.flags.ack == 0
tcp.stream == 87
```

## Packet Analysis

| Packet Number | TCP Flags | Description |
|---|---|---|
| 7039 | SYN | Client initiated a TCP connection |
| 7040 | SYN, ACK | Remote server acknowledged the connection request |
| 7042 | ACK | Client completed the TCP handshake |

## Additional Observations
- Packet 7055: TLS 1.3 Client Hello with SNI i.instagram.com.
- Packet 7057: TLS 1.3 Server Hello and additional TLS handshake messages.
- The remote IP matched the IPv4 address observed during the earlier DNS investigation.
- Relative sequence and acknowledgment values confirmed the TCP handshake.

## SOC Investigation Findings
The TCP three-way handshake successfully established a connection from 192.168.1.145:64414 to 57.144.210.192:443.

Subsequent TLS messages showed that the client initiated encrypted communication with the server.

## SOC Conclusion
The observed TCP handshake and subsequent TLS negotiation are consistent with normal HTTPS connection establishment. No clear malicious indicators were identified in the inspected packets alone.

## Evidence
TCP handshake and TCP stream screenshots are provided in this directory.
