# HTTP Traffic Investigation

## Objective
Analyze HTTP GET requests, response status codes, and HTTP headers using Wireshark.

## Tools Used
- Wireshark 4.6.9
- Windows 10
- HTTP packet capture

## Investigation Environment
- Client IP: 192.168.1.145
- Server IP: 3.213.114.44
- Source Port: 53415
- Destination Port: 80
- Protocol: HTTP/1.1

## Wireshark Display Filters
```text
http
http.request
http.response
```

## HTTP Request Analysis
- Request Packet: 352
- Request Method: GET
- Request Path: /ping
- Host: deviceserver-production.us-east-1.elasticbeanstalk.com
- User-Agent: python-requests/2.18.4
- Accept: */*
- Accept-Encoding: gzip, deflate

## HTTP Response Analysis
- Response Packet: 368
- HTTP Status: 200 OK
- Content-Type: text/plain; charset=utf-8
- Content-Length: 2 bytes
- Connection: keep-alive
- Server: nginx
- X-Powered-By: Express
- Response Time: 212.9064 ms

## SOC Investigation Findings
An HTTP GET request was observed from the local computer to the /ping endpoint. The request used a Python requests User-Agent and received an HTTP 200 OK response.

The User-Agent indicates automated HTTP client behavior, which can be associated with legitimate monitoring tools, scripts, or software agents.

The Server and X-Powered-By headers disclosed information about the server's web technology.

## SOC Conclusion
The observed request-response exchange is consistent with automated HTTP communication. No direct evidence of malicious activity was identified in the inspected packets.

The exact process responsible for the request was not independently verified.

## Evidence
See the accompanying HTTP GET request and HTTP 200 OK response screenshots.
