# Day 2 — IPv4, CIDR and Subnetting

## Learning Objective

Today's goal was to understand:

- IPv4 addressing
- Network and host portions
- Subnet masks
- CIDR notation
- Network addresses
- Broadcast addresses
- Usable host ranges
- Default gateways
- Basic subnetting using block sizes

## Learning Resource

TryHackMe — Networking Concepts:

https://tryhackme.com/room/networkingconcepts

---

# IPv4

An IPv4 address identifies a device or network interface on a network.

An IPv4 address contains **32 bits**, divided into four sections called octets.

Example:

```text
192.168.1.25
```

The four octets are:

```text
192 . 168 . 1 . 25
```

Each octet contains 8 bits.

Therefore:

```text
8 + 8 + 8 + 8 = 32 bits
```

An IP address can be compared to a residential address because it helps identify where data should be delivered.

---

# Network Portion vs Host Portion

An IPv4 address contains:

- A **network portion**
- A **host portion**

The network portion identifies the network that the device belongs to.

The host portion identifies the specific device inside that network.

For example:

```text
192.168.1.25/24
```

The `/24` means that:

```text
24 bits = Network portion
8 bits  = Host portion
```

Because IPv4 contains 32 bits:

```text
32 - 24 = 8 host bits
```

---

# Subnet Mask

A subnet mask is used to determine which part of an IPv4 address represents the network and which part represents the host.

Example:

```text
IP Address:  192.168.1.25
Subnet Mask: 255.255.255.0
```

The subnet mask:

```text
255.255.255.0
```

is equivalent to:

```text
/24
```

The first 24 bits represent the network portion.

The remaining 8 bits represent the host portion.

---

# CIDR Notation

CIDR stands for **Classless Inter-Domain Routing**.

CIDR provides a shorter way of representing a subnet mask.

Examples:

| CIDR | Subnet Mask | Total Addresses | Usable Hosts |
|---|---|---:|---:|
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |

Every additional network bit reduces the number of host addresses available.

The block sizes follow this pattern:

```text
/24 = 256 addresses
/25 = 128 addresses
/26 = 64 addresses
/27 = 32 addresses
/28 = 16 addresses
```

---

# Calculating Host Bits

IPv4 has 32 total bits.

To calculate the number of host bits:

```text
Host bits = 32 - CIDR prefix
```

For example:

```text
/26
```

means:

```text
32 - 26 = 6 host bits
```

The number of total addresses is:

```text
2^6 = 64
```

The normal usable host count is:

```text
64 - 2 = 62 usable hosts
```

The two reserved addresses are normally:

- Network address
- Broadcast address

---

# Network Address

The network address is the **first address in a subnet**.

It identifies the subnet itself and is not normally assigned to a host.

Example:

```text
192.168.10.0/24
```

Network address:

```text
192.168.10.0
```

---

# Broadcast Address

The broadcast address is the **last address in the subnet**.

It can be used to communicate with all hosts inside that subnet.

Example:

```text
192.168.10.0/24
```

Broadcast:

```text
192.168.10.255
```

---

# Usable Host Range

Usable host addresses normally exist between the network address and the broadcast address.

Example:

```text
Network:   192.168.10.0
Broadcast: 192.168.10.255
```

Usable range:

```text
192.168.10.1 - 192.168.10.254
```

There are:

```text
254 usable hosts
```

---

# Default Gateway

A default gateway is the router or next-hop device that a computer uses when it needs to communicate with a destination outside its local subnet.

If two computers are inside the same subnet, they can normally communicate directly without using the default gateway.

If the destination is outside the local subnet, the packet is normally sent to the default gateway.

Example:

```text
Computer A:
192.168.10.25/24

Computer B:
192.168.10.200/24
```

Both devices belong to:

```text
192.168.10.0/24
```

Therefore, they can normally communicate directly on the local network.

---

# Commands Used

I used the Windows networking command:

```powershell
ipconfig
```

This command allows me to inspect information such as:

- IPv4 address
- Subnet mask
- Default gateway
- Network adapters

---

# My Local Network Observation

When I used:

```powershell
ipconfig
```

I was able to see the network configuration of my computer.

Important information included:

- IPv4 address
- Subnet mask
- Default gateway
- Network adapter information

The IP address identifies my computer's interface on the network.

The subnet mask tells the computer which addresses belong to the same local subnet.

The default gateway is used when traffic needs to travel outside the local subnet.

---

# Subnetting Method

The method I practiced was based on identifying the **block size**.

For example:

## /25

Block size:

```text
128
```

Ranges:

```text
0 - 127
128 - 255
```

## /26

Block size:

```text
64
```

Ranges:

```text
0 - 63
64 - 127
128 - 191
192 - 255
```

## /27

Block size:

```text
32
```

Ranges:

```text
0 - 31
32 - 63
64 - 95
96 - 127
128 - 159
160 - 191
192 - 223
224 - 255
```

To find the subnet, I identify which block contains the host address.

The first address in that block is the network address.

The final address in that block is the broadcast address.

Everything between them is normally part of the usable host range.

---

# Practical Subnetting Exercises

## Exercise 1 — `192.168.10.25/24`

```text
Subnet mask:     255.255.255.0
Network address: 192.168.10.0
First host:      192.168.10.1
Last host:       192.168.10.254
Broadcast:       192.168.10.255
Usable hosts:    254
```

### What I corrected

I initially placed the first and last host values incorrectly.

I learned that in a normal `/24` subnet:

```text
Network address = first address
Broadcast       = last address
Usable hosts    = everything in between
```

---

## Exercise 2 — `192.168.10.130/25`

A `/25` uses blocks of:

```text
128
```

The ranges are:

```text
0 - 127
128 - 255
```

Since `130` falls inside:

```text
128 - 255
```

the result is:

```text
Subnet mask:     255.255.255.128
Network address: 192.168.10.128
First host:      192.168.10.129
Last host:       192.168.10.254
Broadcast:       192.168.10.255
Usable hosts:    126
```

---

## Exercise 3 — `10.10.5.70/26`

A `/26` uses blocks of:

```text
64
```

The ranges are:

```text
0 - 63
64 - 127
128 - 191
192 - 255
```

Since `70` falls inside:

```text
64 - 127
```

the result is:

```text
Subnet mask:     255.255.255.192
Network address: 10.10.5.64
First host:      10.10.5.65
Last host:       10.10.5.126
Broadcast:       10.10.5.127
Usable hosts:    62
```

### What I corrected

I initially confused the correct network block.

I learned that I must first find the block containing the host address.

Because `70` falls between `64` and `127`, the network address must be:

```text
10.10.5.64
```

---

## Exercise 4 — `172.16.20.200/27`

A `/27` uses blocks of:

```text
32
```

The relevant ranges include:

```text
160 - 191
192 - 223
224 - 255
```

Since `200` falls inside:

```text
192 - 223
```

the result is:

```text
Subnet mask:     255.255.255.224
Network address: 172.16.20.192
First host:      172.16.20.193
Last host:       172.16.20.222
Broadcast:       172.16.20.223
Usable hosts:    30
```

---

# Important Concepts I Learned

## Host Bits vs Usable Hosts

One mistake I made was confusing **host bits** with **usable host addresses**.

For example:

```text
/24
```

IPv4 contains 32 bits:

```text
32 - 24 = 8 host bits
```

Those 8 host bits provide:

```text
2^8 = 256 total addresses
```

Then:

```text
256 - 2 = 254 usable hosts
```

Therefore:

```text
8 = host bits
254 = usable host addresses
```

They are not the same thing.

---

# Assessment Results

**Final Score: 19/20**

## Question 1

For:

```text
192.168.50.20/24
```

I understood that:

- `192.168.50.20` represents the IPv4 address of a host/interface.
- `/24` means 24 bits are used for the network portion.
- IPv4 contains 32 bits.
- Therefore 8 host bits remain.
- The subnet mask is `255.255.255.0`.

### Correction

I initially said there were **254 host bits**.

The correct explanation is:

```text
32 - 24 = 8 host bits
```

Those host bits produce:

```text
2^8 = 256 total addresses
254 usable hosts
```

---

## Question 2

Given:

```text
192.168.1.75/24
```

My result was:

```text
Subnet mask:     255.255.255.0
Network address: 192.168.1.0
First host:      192.168.1.1
Last host:       192.168.1.254
Broadcast:       192.168.1.255
Usable hosts:    254
```

This answer was correct.

---

## Question 3

Given:

```text
192.168.1.130/25
```

My result was:

```text
Subnet mask:     255.255.255.128
Network address: 192.168.1.128
First host:      192.168.1.129
Last host:       192.168.1.254
Broadcast:       192.168.1.255
Usable hosts:    126
```

This answer was correct.

---

## Question 4

Computer A:

```text
192.168.10.25/24
```

Computer B:

```text
192.168.10.200/24
```

Both computers belong to the same subnet:

```text
192.168.10.0/24
```

They share the same network and broadcast boundaries.

Therefore, they can normally communicate directly on the local network without using the default gateway.

This answer was correct.

---

## Question 5

### IP Address

An IP address identifies a particular device or network interface so that data can be delivered to it.

It can be compared to a residential address.

### Subnet Mask / CIDR

A subnet mask separates the network portion of an IP address from the host portion.

CIDR is a shorter way of representing a subnet mask.

Examples:

```text
/24
/25
/26
```

### Default Gateway

A default gateway is the router or next-hop device that provides a path for packets that need to leave the local subnet and travel to another network.

This answer was correct.

---

# What I Understood Well

- IPv4 addressing
- Network and host portions
- `/24` subnetting
- `/25` subnetting
- `/26` subnetting
- `/27` subnetting
- Subnet masks
- Network addresses
- Broadcast addresses
- Usable host ranges
- Default gateways
- Communication between devices in the same subnet
- Block-size subnetting

---

# Weak Area

My main mistake today was confusing:

```text
Host bits
```

with:

```text
Usable hosts
```

I now understand that they represent different things.

Example:

```text
/24
32 - 24 = 8 host bits

2^8 = 256 total addresses

256 - 2 = 254 usable hosts
```

---

# Things to Revise

- Continue practicing CIDR block sizes.
- Remember that the network address is the first address in a subnet.
- Remember that the broadcast address is the final address in a subnet.
- Remember that usable hosts normally exist between those two addresses.
- Keep the difference between host bits, total addresses, and usable hosts clear.
- Continue practicing subnetting without relying on a subnet calculator.

---

# Things I Can Explain Without Notes

- What an IPv4 address is.
- What a subnet mask does.
- What CIDR notation means.
- What a network address is.
- What a broadcast address is.
- What a default gateway does.
- Why two hosts in the same subnet normally do not need the default gateway to communicate.
- How block sizes can be used to calculate basic IPv4 subnets.

---

# Day 2 Status

**Completed successfully.**

**Assessment Score: 19/20**

**Ready for Day 3 — TCP vs UDP and Common Ports.**