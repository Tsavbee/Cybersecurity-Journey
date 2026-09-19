# Day 1 — OSI Model and TCP/IP

## What I Learned

From today's lesson, I learned that the OSI Model is made up of seven layers that help describe how data moves through a network.

I also learned that the TCP/IP Model performs a similar role, but it groups some of the OSI layers together into four broader layers.

Understanding these models gives me a foundation for learning networking and cybersecurity because they help me understand where communication happens and where network or security problems may occur.

---

## OSI Model

| Layer | Name | Main Job | Example |
|---|---|---|---|
| 7 | Application | Provides network services and interfaces to applications | HTTP, HTTPS, FTP |
| 6 | Presentation | Handles data formatting, encoding, compression, and representation | JPEG, PNG, MPEG, Unicode |
| 5 | Session | Establishes, maintains, and manages communication sessions | Session management, RPC |
| 4 | Transport | Provides end-to-end communication and data segmentation | TCP, UDP |
| 3 | Network | Handles IP addressing and routing between networks | IP, ICMP, IPsec |
| 2 | Data Link | Handles communication between devices on the same local network using frames | Ethernet (802.3), Wi-Fi (802.11) |
| 1 | Physical | Handles the physical transmission of bits through a medium | Electrical, optical, and wireless signals |

The OSI Model contains seven layers:

1. Application
2. Presentation
3. Session
4. Transport
5. Network
6. Data Link
7. Physical

Each layer has a different responsibility, but they all work together during network communication.

---

## TCP/IP Model

The TCP/IP Model is another networking model used to describe how data is transmitted across networks and the Internet.

Unlike the OSI Model, which contains seven layers, the TCP/IP Model is commonly represented using four layers.

### 1. Application Layer

The Application layer provides networking services to applications.

It broadly combines the following OSI layers:

- Application
- Presentation
- Session

Examples of protocols that operate at this level include:

- HTTP
- HTTPS
- FTP
- DNS

### 2. Transport Layer

The Transport layer handles end-to-end communication between applications.

Two important protocols at this layer are:

- TCP
- UDP

TCP can provide reliable communication between applications, while UDP provides a simpler communication method without the same reliability mechanisms.

### 3. Internet Layer

The Internet layer handles logical addressing and routing between networks.

IP addresses are used at this layer to identify devices and help packets reach their destination.

This layer corresponds closely to the Network layer of the OSI Model.

### 4. Link Layer

The Link layer handles communication across the local network and the transmission of data through the network medium.

It broadly combines the following OSI layers:

- Data Link
- Physical

---

## OSI vs TCP/IP

The OSI Model and TCP/IP Model both help explain how network communication works.

The major difference is how the layers are organized.

The OSI Model uses seven layers, while the TCP/IP Model groups some of those layers together into four broader layers.

The relationship can be represented like this:

| OSI Model | TCP/IP Model |
|---|---|
| Application | Application |
| Presentation | Application |
| Session | Application |
| Transport | Transport |
| Network | Internet |
| Data Link | Link |
| Physical | Link |

The TCP/IP Application layer combines the OSI Application, Presentation, and Session layers.

The TCP/IP Transport layer corresponds closely to the OSI Transport layer.

The TCP/IP Internet layer corresponds closely to the OSI Network layer.

The TCP/IP Link layer combines functions associated with the OSI Data Link and Physical layers.

Both models therefore describe similar networking processes, but they organize those processes differently.

---

## Commands Used

I used the following Windows command:

```powershell
ipconfig
```

I used `ipconfig` to view the network configuration of my computer.

It allowed me to see information about my network adapters and basic IP configuration.

---

## Example — Loading a Website

When I open:

`https://example.com`

the data can be thought of as moving through the network stack like this:

Browser

↓

Application Layer

↓

Transport Layer

↓

Network / Internet Layer

↓

Data Link Layer

↓

Physical Layer

↓

Network

↓

Destination Server

---

## Explaining What Happens

When I open a website such as `https://example.com`, the browser creates application data at the Application layer.

The Transport layer handles end-to-end communication between applications. Protocols such as TCP can be used to provide reliable communication between the browser and the server.

The Network layer uses IP addresses to determine where packets need to go. Routers can then forward those packets toward their destination.

The Data Link layer handles communication between devices on the local network using frames.

The Physical layer carries the actual bits through a transmission medium such as Ethernet cables, fibre-optic cables, or wireless radio signals.

All of these layers work together so that data can move from my device to another system across a network.

---

## Hands-On Practice

### What I Did

I used the following command:

```powershell
ipconfig
```

This allowed me to view my computer's network configuration.

I also completed networking exercises in TryHackMe and used a Linux command-line environment.

During the TryHackMe exercise, I ran networking-related commands and started learning how command-line tools can be used to gather information about systems and network services.

---

### What I Observed

When I ran `ipconfig`, I was able to view information about my Windows network configuration.

I observed information such as:

- Network adapters
- IPv4 address
- Subnet mask
- Default gateway
- Adapter connection states

I also noticed that a computer can have several different network adapters, even if only one of them is currently being used to connect to the network.

During the TryHackMe exercises, I was introduced to a Linux command-line environment.

I also ran my first networking-related commands, which helped me see how cybersecurity professionals can use command-line tools to gather information about computers, websites, and network services.

---

## What I Learned From the Practical Exercise

I learned that understanding the fundamentals is very important and should not be skipped.

I can now see why networking is important in cybersecurity because computers need to communicate across networks before many security concepts can be properly understood.

The OSI Model gives me a structured way to understand where different networking functions happen.

I also learned that command-line tools can be used to inspect the networking configuration of a computer.

---

## What Confused Me Today

- I am still getting used to remembering which OSI layer is responsible for each function.
- I need more practice understanding exactly how the OSI Model maps to the TCP/IP Model.
- I still need to understand more deeply how all the layers work together during real network communication.

---

## Things I Can Explain Without Notes

- I can explain what the OSI Model is used for.
- I can name most of the seven OSI layers.
- I can explain the general purpose of several OSI layers.
- I can explain the basic difference between the OSI Model and TCP/IP Model.
- I can use `ipconfig` to view basic network configuration information on Windows.
- I understand that IP addressing is mainly associated with the Network layer.
- I understand that TCP and UDP operate at the Transport layer.

---

## Things I Still Need to Improve

- Memorizing all seven OSI layers in the correct order.
- Understanding TCP and UDP in more detail.
- Understanding IP addresses and subnetting.
- Understanding how DNS works.
- Understanding HTTP and HTTPS.
- Understanding how actual packets move through the different networking layers.

These topics will be studied in more detail during the remaining networking days.

---

## Assessment Results

**Score:** 19/20

### What I Understood Well

- I can correctly list the seven OSI layers in order.
- I understand that the Network Layer is responsible for IP addressing and routing.
- I understand that the TCP/IP Application layer broadly combines the OSI Application, Presentation, and Session layers.
- I understand why the OSI model is useful for learning and troubleshooting networks.

### Weak Area

I initially confused the purpose of the OSI model with network resilience or fault tolerance.

The OSI model does not itself keep a network running when services fail. Its main purpose is to provide a structured way to understand how network communication works and to help identify where networking or security problems may occur.

### Things to Revise

- Keep the purpose of the OSI model separate from concepts like redundancy, resilience, and fault tolerance.
- Continue practicing how each OSI layer maps to the TCP/IP model.

### Day 1 Status

**Completed successfully — ready for Day 2.**