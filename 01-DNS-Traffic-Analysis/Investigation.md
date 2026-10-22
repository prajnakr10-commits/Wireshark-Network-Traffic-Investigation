# DNS Traffic Investigation

## Objective
Analyze DNS queries and responses using Wireshark.

## Tools
- Wireshark 4.6.9
- Windows

## Wireshark Filters
- `dns`
- `dns.flags.response == 1`

## Investigation
- DNS query packet: 6991
- DNS response packet: 6994
- Client IP: 192.168.1.145
- DNS resolver: 192.168.1.1
- Queried domain: i.instagram.com
- Query type: A
- Transaction ID: 0xb917
- CNAME: instagram.c10r.instagram.com
- Resolved IPv4: 57.144.210.192
- DNS response time: 3.7567 ms

## SOC Conclusion
The observed DNS resolution completed successfully, with no obvious malicious indicators in this exchange. This observation alone does not establish the safety of subsequent connections.

## Evidence
See the screenshots directory for the captured DNS request and response.
