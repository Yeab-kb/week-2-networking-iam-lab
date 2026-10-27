# AWS Student Builders Group — Week 2 Lab
## Networking & IAM Fundamentals

**Name:** Yeabsira  
**Track:** Cloud & DevOps  
**Date:** October 2026  

---

## Task 1 — Network Information
- **Operating System:** Windows (Git Bash)
- **Local IPv4 Address:** 10.2.74.80
- **Default Gateway:** 10.2.64.1
- **Address Type:** Private IPv4 Address

---

## Task 2 — Subnetting Calculations
Starting network: `10.0.0.0/24` divided into 4 equal subnets.

### Subnet 1
- **CIDR:** 10.0.0.0/26
- **Network Address:** 10.0.0.0
- **Full Range:** 10.0.0.0 - 10.0.0.63
- **Usable Host Range:** 10.0.0.1 - 10.0.0.62
- **Broadcast Address:** 10.0.0.63
- **Usable IPv4 (Standard / AWS):** 62 / 59

### Subnet 2
- **CIDR:** 10.0.0.64/26
- **Network Address:** 10.0.0.64
- **Full Range:** 10.0.0.64 - 10.0.0.127
- **Usable Host Range:** 10.0.0.65 - 10.0.0.126
- **Broadcast Address:** 10.0.0.127
- **Usable IPv4 (Standard / AWS):** 62 / 59

### Subnet 3
- **CIDR:** 10.0.0.128/26
- **Network Address:** 10.0.0.128
- **Full Range:** 10.0.0.128 - 10.0.0.191
- **Usable Host Range:** 10.0.0.129 - 10.0.0.190
- **Broadcast Address:** 10.0.0.191
- **Usable IPv4 (Standard / AWS):** 62 / 59

### Subnet 4
- **CIDR:** 10.0.0.192/26
- **Network Address:** 10.0.0.192
- **Full Range:** 10.0.0.192 - 10.0.0.255
- **Usable Host Range:** 10.0.0.193 - 10.0.0.254
- **Broadcast Address:** 10.0.0.255
- **Usable IPv4 (Standard / AWS):** 62 / 59
---

## Task 3 — Test DNS Resolution
- **Domain Tested:** `example.com`
- **DNS Resolution Status:** Succeeded
- **IP Address Returned:** `93.184.215.14`
- **What DNS Does:** DNS (Domain Name System) acts as the phonebook of the internet. It translates human-readable domain names (like `example.com`) into machine-readable IP addresses so browsers can locate servers across the network.

---

## Task 4 — Inspect an HTTPS Website
- **Website Loaded:** Successfully (`200 OK`)
- **HTTP Status Code Returned:** `HTTP/2 200`
- **What HTTPS Adds to HTTP:** HTTPS adds an encryption and authentication layer using TLS/SSL. This encrypts data in transit to protect against eavesdropping and tampering, and verifies the identity of the server.
- **Why DNS Alone Does Not Guarantee Loading:** DNS only maps a domain name to an IP address. It does not check whether the destination server is online, whether a web server process is listening on port 80/443, whether firewall rules block traffic, or whether TLS handshake succeeds.

---

## Task 5 — HTTP Status Codes

| Status code | Meaning | Example situation |
|---|---|---|
| `200` | OK | Request succeeded and page content is returned normally. |
| `301` | Moved Permanently | A site has permanently changed its URL and redirects the browser to the new location. |
| `403` | Forbidden | Server understands the request, but client lacks permission (e.g., restricted admin panel). |
| `404` | Not Found | Server cannot find the requested URL path/resource. |
| `500` | Internal Server Error | Unhandled exception or code crash on the backend application server. |

### Network vs HTTP Error Differences:
- **DNS Failure:** The client cannot resolve the hostname to an IP address (e.g., domain does not exist or DNS server unreachable).
- **Connection Timeout:** The IP address was resolved, but no TCP response was received before timing out (e.g., firewall dropping packets).
- **TLS Certificate Error:** TCP connection established, but cryptographic handshake failed (e.g., expired or untrusted certificate).
- **HTTP Error Response:** Network and TLS connections succeeded, but the server explicitly returned an error status code (e.g., `404` or `500`).

---

## Task 6 — AWS IAM Policy Questions
1. **Permitted Action Field:** The `"Action"` field specifies the permitted API call(s).
2. **Resources Field:** The `"Resource"` field specifies the specific AWS resource ARN(s) affected.
3. **`s3:GetObject` Scope:** No, `s3:GetObject` only allows reading existing object contents. Listing objects requires `s3:ListBucket`.
4. **Least-Privilege Safety:** Granting narrow permissions (`s3:GetObject`) limits potential blast radius if credentials are compromised, preventing unauthorized deletion or administrative changes.
5. **Credentials on GitHub:** AWS access keys uploaded to GitHub can be indexed by automated bots in seconds, leading to unauthorized resource creation, data theft, and massive cloud bills.

---

## Task 7 — Troubleshooting Scenarios
1. **Scenario 1 (Domain does not resolve):** **DNS Layer** — First check if the domain exists and local/upstream DNS servers are responding properly.
2. **Scenario 2 (Connection times out):** **Network Connectivity Layer** — Domain resolved to an IP, but TCP packets are blocked by firewalls or routing rules.
3. **Scenario 3 (TLS Certificate Warning):** **TLS Layer** — Network connection established, but certificate verification failed due to expiration or authority mismatches.
4. **Scenario 4 (HTTP 404 Response):** **HTTP / Application Layer** — Server is reachable and working, but the requested path/endpoint was not found.
5. **Scenario 5 (EC2 receives AccessDenied reading S3):** **IAM / S3 Authorization Layer** — Network and HTTP work, but the IAM role attached to the EC2 instance lacks `s3:GetObject` permissions on the target bucket.


