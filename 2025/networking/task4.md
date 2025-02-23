# Week 1: Networking Challenge
## Task 3

# Essential Networking Commands

## 1. `ping` (Check Connectivity)
```sh
ping <hostname or IP>
```
**Purpose:** Tests network connectivity by sending ICMP echo request packets.

**Example:**
```sh
ping google.com
```
**Output:**
```sh
PING google.com (142.250.182.142): 56 data bytes
64 bytes from 142.250.182.142: icmp_seq=1 ttl=118 time=12.3 ms
64 bytes from 142.250.182.142: icmp_seq=2 ttl=118 time=10.5 ms
```
**Fields:**
- **Bytes**: Packet size sent.
- **icmp_seq**: Sequence number of the request.
- **ttl (Time-to-Live)**: Number of hops before the packet is discarded.
- **time**: Round-trip time in milliseconds.

---

## 2. `traceroute / tracert` (Trace Packet Routes)
- 🐧 Linux/macOS: `traceroute <hostname or IP>`  
- 🖥️ Windows: `tracert <hostname or IP>`  

**Purpose:** Shows the route that packets take to reach a destination.

**Example:**
```sh
traceroute google.com
```
**Output:**
```sh
1  192.168.1.1 (192.168.1.1)  2.5 ms  1.8 ms  1.7 ms
2  10.1.1.1 (10.1.1.1)  5.6 ms  5.2 ms  5.3 ms
3  172.217.160.142 (172.217.160.142)  15.2 ms  14.7 ms  15.0 ms
```
**Key Fields:**
- Each line represents a router/hop.
- The IP addresses of routers along the path.
- Three time values for round-trip latency per hop.

---

## 3. `netstat` (Network Statistics)
```sh
netstat -an
```
**Purpose:** Displays network connections, listening ports, and statistics.

**Example:**
```sh
netstat -an
```
**Output:**
```sh
Proto  Local Address   Foreign Address  State
TCP    
TCP    
UDP    
```
** Fields:**
- **Proto**: Protocol (TCP/UDP).
- **Local Address**: IP and port on the local machine.
- **Foreign Address**: IP and port of the remote machine.
- **State**: Connection state (LISTENING, ESTABLISHED, TIME_WAIT, etc.).

---

## 4️⃣ `curl`  (Make HTTP Requests)
```sh
curl -I <URL>
```
**Purpose:** Sends HTTP requests and retrieves web content or API responses.

**Example:**
```sh
curl -I https://www.google.com
```
** Output:**
```sh
HTTP/2 200
content-type: text/html;
date:
server:
```
**Fields:**
- **HTTP/2 200**: HTTP status code (200 = OK, 404 = Not Found).
- **Content-Type**: Type of data returned (HTML, JSON, etc.).
- **Date**: Server response time.
- **Server**: Web server details.

---

## 5. `dig` / `nslookup` (🔎 DNS Lookup)
- 🐧 `dig <domain>` (Linux/macOS)  
- 🖥️ `nslookup <domain>` (Windows)  

**Purpose:** Retrieves DNS records for a domain.

**Example:**
```sh
dig google.com
```
**Output:**
```sh
;; QUESTION SECTION:
;google.com. IN A

;; ANSWER SECTION:
google.com.  300  IN A  142.250.182.142
```
**Fields:**
- **QUESTION SECTION**: What was queried (google.com).
- **ANSWER SECTION**: The resolved IP address (142.250.182.142).
- **TTL (Time to Live)**: How long the DNS record is cached.

---
These commands help in troubleshooting network issues, checking connectivity, and analyzing DNS records.
