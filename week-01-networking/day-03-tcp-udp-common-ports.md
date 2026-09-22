# Day 3 — TCP vs UDP and Common Ports

## Learning Objectives

Today's goal was to understand:

- What TCP is and how it works
- What UDP is and how it differs from TCP
- The TCP three-way handshake
- Connection-oriented vs connectionless communication
- Reliability and protocol overhead
- How ports identify network services
- Common/default service ports
- Client source ports vs server destination ports
- TCP connection states such as `ESTABLISHED`

---

## Learning Resource

TryHackMe — Networking Concepts:

https://tryhackme.com/room/networkingconcepts

Main topics studied:

- TCP
- UDP
- TCP three-way handshake
- Port numbers
- Common network services

---

# TCP

TCP stands for:

```text
Transmission Control Protocol
```

TCP is a **connection-oriented protocol**.

This means that TCP establishes a connection between two systems before application data is exchanged.

TCP focuses on reliable communication.

Important TCP characteristics include:

- Connection-oriented communication
- Reliable delivery
- Packet ordering
- Acknowledgements
- Retransmission of lost data
- Higher overhead than UDP
- TCP connection states

Examples of services commonly associated with TCP include:

```text
HTTP
HTTPS
SSH
FTP
SMTP
```

---

# TCP Three-Way Handshake

Before a TCP connection becomes established, TCP performs a three-way handshake.

The process is:

```text
SYN → SYN-ACK → ACK
```

## Step 1 — SYN

The client sends a:

```text
SYN
```

packet to the server.

This means that the client wants to begin a TCP connection.

I understand this as the client saying:

```text
"I want to establish a connection."
```

---

## Step 2 — SYN-ACK

The server responds with:

```text
SYN-ACK
```

The `ACK` acknowledges the client's original SYN request.

The server is also sending its own SYN as part of the connection establishment process.

I understand this as:

```text
"I received your request and I am ready to communicate."
```

---

## Step 3 — ACK

The client sends an:

```text
ACK
```

back to the server.

This acknowledges the server's response.

After the final ACK, the TCP connection becomes established.

The systems can now exchange application data.

---

## My Explanation of the TCP Handshake

During the TCP three-way handshake, the client first sends a SYN packet to the server requesting a connection.

The server then responds with a SYN-ACK packet. This acknowledges the client's SYN while also responding with its own synchronization request.

The client then sends an ACK packet back to the server.

After this final ACK, the TCP connection is established and communication can begin.

---

# TCP Connection State — ESTABLISHED

When inspecting TCP connections, I may see a state such as:

```text
ESTABLISHED
```

This means that the TCP connection has successfully been set up and the two endpoints currently have an active TCP connection.

In simple terms:

```text
The TCP connection is active and the two systems can exchange data.
```

The three-way handshake has already completed before the connection reaches the established state.

---

# UDP

UDP stands for:

```text
User Datagram Protocol
```

UDP is a **connectionless protocol**.

Unlike TCP, UDP does not establish a TCP-style connection before sending data.

UDP also does not provide TCP's built-in reliability mechanisms.

Important UDP characteristics include:

- Connectionless communication
- No TCP three-way handshake
- No built-in guarantee of delivery
- No built-in packet ordering guarantee
- No TCP-style retransmission mechanism
- Lower protocol overhead than TCP

UDP is commonly useful when low latency is important and the application can tolerate some data loss or handle reliability itself.

Examples can include:

```text
DNS queries
Streaming
Voice communication
Video communication
Online gaming
```

---

# Why UDP Does Not Show ESTABLISHED

TCP keeps track of connection state.

For example:

```text
LISTENING
ESTABLISHED
TIME_WAIT
```

UDP is connectionless.

Because UDP does not establish the same type of persistent connection, I would not normally expect UDP endpoints to show a TCP state such as:

```text
ESTABLISHED
```

---

# TCP vs UDP

| Feature | TCP | UDP |
|---|---|---|
| Full Name | Transmission Control Protocol | User Datagram Protocol |
| Connection Type | Connection-oriented | Connectionless |
| Three-Way Handshake | Yes | No |
| Reliable Delivery | Yes | No built-in guarantee |
| Packet Ordering | Maintained by TCP | No built-in guarantee |
| Retransmission | Supported | Not provided by UDP itself |
| Overhead | Higher | Lower |
| Connection States | Yes | No TCP-style connection states |
| Example Use | Email | Streaming |

---

## My Main TCP vs UDP Comparison

TCP is a connection-oriented protocol while UDP is connectionless.

TCP focuses on reliable delivery, while UDP does not guarantee that data will arrive.

TCP also has higher overhead because it performs tasks such as:

- Establishing connections
- Tracking connection state
- Sending acknowledgements
- Maintaining ordering
- Retransmitting lost data

UDP has lower overhead because it does not perform all of these TCP mechanisms.

---

# Example TCP Use Case

One TCP example I learned is:

```text
Email
```

For example, SMTP commonly uses TCP.

Email delivery benefits from reliable communication because missing or incorrectly ordered application data could cause problems.

---

# Example UDP Use Case

One UDP example I learned is:

```text
Streaming
```

Streaming and other real-time applications can benefit from lower latency.

In some real-time situations, receiving newer data quickly may be more important than waiting for old missing data to be retransmitted.

---

# What Is a Port?

A port helps identify the network service or application that should receive traffic on a device.

A useful comparison is:

```text
IP address = building address
Port       = specific door or service inside the building
```

For example:

```text
192.168.1.20:443
```

contains:

```text
192.168.1.20 = IP address
443          = port number
```

---

# Common Ports

| Port | Service | Purpose |
|---:|---|---|
| 21 | FTP | File Transfer Protocol |
| 22 | SSH | Secure remote access |
| 25 | SMTP | Email transmission |
| 53 | DNS | Domain name resolution |
| 80 | HTTP | Unencrypted web traffic |
| 443 | HTTPS | Encrypted web traffic |
| 445 | SMB | Windows file/resource sharing |
| 1433 | MSSQL | Microsoft SQL Server |
| 3306 | MySQL | MySQL database service |
| 3389 | RDP | Windows Remote Desktop |

---

# Ports I Practiced

The ports I practiced during today's assessment were:

```text
SSH   = 22
DNS   = 53
HTTPS = 443
SMB   = 445
RDP   = 3389
MySQL = 3306
```

---

# Important Port Correction

During the assessment, I initially answered:

```text
MySQL = 3308
```

The correct default/common port is:

```text
MySQL = 3306
```

This is one port I need to continue reviewing.

---

# Default Ports Do Not Guarantee the Service

A common port number tells me what service is **normally associated** with that port.

For example:

```text
443 = HTTPS
22  = SSH
```

However, a port number by itself does not guarantee that the expected service is actually running there.

Administrators can configure applications to use different ports.

Later, service enumeration tools can help determine what service is actually listening on an open port.

---

# Client and Server Ports

During the assessment, I analyzed:

```text
192.168.1.20:51522 → 93.184.216.34:443
```

I now understand this as:

```text
192.168.1.20 = client/local host IP address
51522        = temporary client/source port

93.184.216.34 = remote server IP address
443           = server/destination HTTPS port
```

---

## Why Are the Two Ports Different?

The two ports are different because they perform different roles.

The server is listening for HTTPS traffic on the commonly used service port:

```text
443
```

The client uses a temporary source port such as:

```text
51522
```

This allows the client's operating system to keep track of its network communication.

So:

```text
51522 = client/source port
443   = server/destination service port
```

---

# Correction From My Original Explanation

I originally explained the different ports by saying they were different because they had different locations.

That explanation was incomplete.

The better explanation is:

> The client normally uses a temporary source port while the server listens on a known service port such as HTTPS port 443.

---

# Practical Commands

The Windows commands for examining TCP and UDP communication include:

```powershell
netstat -ano -p tcp
```

This can display TCP connections and information such as:

```text
Local Address
Foreign Address
State
PID
```

---

For UDP:

```powershell
netstat -ano -p udp
```

UDP output does not normally contain TCP connection states such as:

```text
ESTABLISHED
```

because UDP is connectionless.

---

PowerShell can also display TCP connections using:

```powershell
Get-NetTCPConnection
```

Established TCP connections can be filtered using:

```powershell
Get-NetTCPConnection -State Established
```

UDP endpoints can be inspected using:

```powershell
Get-NetUDPEndpoint
```

---

# Testing Web Ports

TCP connectivity to HTTPS can be tested using:

```powershell
Test-NetConnection example.com -Port 443
```

HTTP can be tested using:

```powershell
Test-NetConnection example.com -Port 80
```

Important output includes:

```text
RemotePort
TcpTestSucceeded
```

---

# Practical Observations

## TCP Observation

TCP is connection-oriented and keeps track of active connections.

When a connection has successfully been established, TCP can show a state such as:

```text
ESTABLISHED
```

This tells me that an active TCP connection exists between the two endpoints.

---

## UDP Observation

UDP does not establish a TCP-style connection.

Because it is connectionless, UDP does not normally display TCP connection states such as:

```text
ESTABLISHED
```

---

## TCP vs UDP Observation

The biggest practical difference I noticed conceptually is that TCP tracks the state of a connection while UDP does not create the same persistent connection state.

TCP therefore provides more reliability mechanisms, while UDP uses fewer connection-management mechanisms.

---

# Assessment

## Question 1 — TCP Three-Way Handshake

### My Answer

During a TCP three-way handshake, the first thing that happens is that the client sends a SYN packet to the server requesting a connection.

The server then sends a SYN-ACK packet acknowledging the synchronization packet sent first.

After that, the client sends an ACK packet back to acknowledge the server's response.

### Corrected Version

The client first sends a SYN packet requesting a TCP connection.

The server replies with a SYN-ACK packet to acknowledge the client's SYN and respond with its own synchronization request.

The client then sends an ACK.

After the final ACK, the TCP connection is established.

### Score

```text
4/4
```

---

# Question 2 — TCP vs UDP

### My Answers

TCP is connection-oriented while UDP is connectionless.

TCP is reliable while UDP is faster/lower overhead and does not guarantee delivery.

TCP has higher overhead while UDP has lower overhead.

TCP can be used for email services.

UDP can be used for streaming.

### Corrected / Expanded Version

TCP is connection-oriented, provides reliable delivery, maintains connection state, and has higher protocol overhead.

UDP is connectionless, does not provide a built-in delivery guarantee, and has lower protocol overhead.

Example TCP use:

```text
Email
```

Example UDP use:

```text
Streaming
```

### Score

```text
4/4
```

---

# Question 3 — Common Ports

### My Answers

```text
SSH   = 22
DNS   = 53
HTTPS = 443
SMB   = 445
RDP   = 3389
MySQL = 3308
```

### Correction

Everything was correct except MySQL.

I answered:

```text
3308
```

The correct MySQL port is:

```text
3306
```

Correct table:

```text
SSH   = 22
DNS   = 53
HTTPS = 443
SMB   = 445
RDP   = 3389
MySQL = 3306
```

### Score

```text
3/4
```

---

# Question 4 — Interpreting an IP and Port Connection

Given:

```text
192.168.1.20:51522 → 93.184.216.34:443
```

### My Original Explanation

I identified:

```text
192.168.1.20 = host system IP address
51522        = port number on the system
93.184.216.34 = remote website/server address
443           = HTTPS server port
```

I initially said that the port numbers were different because they had different locations.

### Corrected Explanation

```text
192.168.1.20
```

is the local/client IP address.

```text
51522
```

is a temporary client-side source port being used for the connection.

```text
93.184.216.34
```

is the remote server IP address.

```text
443
```

is the destination server port commonly associated with HTTPS.

The port numbers are different because they have different roles:

```text
51522 = temporary client/source port
443   = server/destination service port
```

### Score

```text
3/4
```

---

# Question 5 — ESTABLISHED TCP State

### My Answer

I can see `ESTABLISHED` because the TCP connection successfully completed the three-way handshake and the connection was created between the client and server.

UDP does not show the same state because it is connectionless.

### Corrected Version

`ESTABLISHED` means that the TCP connection has successfully been set up and the two endpoints currently have an active TCP connection.

TCP maintains connection state.

UDP does not normally show an `ESTABLISHED` state because UDP is connectionless and does not perform TCP's three-way handshake or maintain TCP-style connection states.

### Score

```text
4/4
```

---

# Assessment Results

```text
Question 1: 4/4
Question 2: 4/4
Question 3: 3/4
Question 4: 3/4
Question 5: 4/4
```

## Final Score

```text
18/20
```

### Result

```text
STRONG
```

---

# What I Understood Well

- TCP is connection-oriented.
- UDP is connectionless.
- TCP uses the three-way handshake.
- The handshake follows:

```text
SYN → SYN-ACK → ACK
```

- TCP provides reliable delivery mechanisms.
- UDP does not provide a built-in delivery guarantee.
- TCP has higher overhead than UDP.
- UDP has lower overhead than TCP.
- TCP maintains connection states.
- I understand what `ESTABLISHED` means.
- I know the common ports for SSH, DNS, HTTPS, SMB, and RDP.
- I understand that a client can use a temporary source port when connecting to a server service port.

---

# Weak Areas

## MySQL Port

I initially confused:

```text
3308
```

with the correct MySQL port:

```text
3306
```

I need to memorize:

```text
MySQL = 3306
```

---

## Client Source Ports

I initially knew that `51522` was a port belonging to the client system, but I did not clearly understand why it differed from the server's port.

I now understand that:

```text
51522 = temporary client/source port
443   = server HTTPS destination port
```

---

# Things to Revise

- Memorize `MySQL = 3306`.
- Continue practicing common service ports.
- Remember the difference between source and destination ports.
- Remember that the server usually listens on a known service port.
- Remember that clients often use temporary high-numbered source ports.
- Continue practicing TCP connection-state interpretation.

---

# Things I Can Explain Without Notes

I can now explain:

- What TCP is
- What UDP is
- The difference between connection-oriented and connectionless communication
- The TCP three-way handshake
- SYN
- SYN-ACK
- ACK
- What `ESTABLISHED` means
- Why UDP does not normally show an established connection
- Why TCP has more overhead than UDP
- Why UDP can be useful for real-time communication
- What a network port is
- Why a client source port and server destination port can be different
- Common ports such as:

```text
22   SSH
53   DNS
443  HTTPS
445  SMB
3306 MySQL
3389 RDP
```

---

# Day 3 Summary

Today I learned how TCP and UDP operate differently at the transport layer.

TCP establishes connections using:

```text
SYN → SYN-ACK → ACK
```

TCP provides reliability mechanisms and maintains connection states such as:

```text
ESTABLISHED
```

UDP is connectionless and does not maintain the same connection state.

I also practiced common network ports and learned the difference between a temporary client source port and a server destination/service port.

My biggest corrections today were:

```text
MySQL = 3306
```

and:

```text
51522 = temporary client/source port
443   = server HTTPS destination port
```

---

# Day 3 Status

**Learning:** Completed

**Assessment:** Completed

**Assessment Score:** 18/20

**Result:** Strong

**Next Topic:** Day 4 — DNS, `nslookup`, and `dig`