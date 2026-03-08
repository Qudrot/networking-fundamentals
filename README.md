# networking-fundamentals

OSI Model Summary The Open Systems Interconnection (OSI) model is a conceptual framework that divides network communication into seven distinct layers, helping network professionals understand how hardware and software interact, troubleshoot issues, and standardize equipment
. As discussed previously, the layers from bottom to top are:
Layer 1 - Physical: Transmits raw binary data over physical mediums like copper wires, fiber optics, or radio frequencies
.
Layer 2 - Data Link: Handles node-to-node delivery on a local network, packaging data into "frames" and using MAC addresses
.
Layer 3 - Network: Routes data across different networks by packaging it into "packets" and adding logical IP addresses
.
Layer 4 - Transport: Breaks data into manageable segments or datagrams, assigns port numbers, and handles flow control and error recovery
.
Layer 5 - Session: Establishes, manages, and terminates connections or "sessions" between applications
.
Layer 6 - Presentation: Translates, formats, encrypts, and compresses data so it can be understood by the receiving application
.
Layer 7 - Application: Provides the direct interface and protocols (like HTTP or SMTP) for end-user applications to access network resources
.
When sending data, the information flows down these layers on the sender's side—encapsulating the data with headers at each step—and flows back up the layers on the receiver's side to be decapsulated
.
IP Addressing Calculations
1. IPv4 Address Basics

An IPv4 address is a 32-bit number, written in dotted-decimal format (4 octets, e.g., 192.168.1.10).
Each octet = 8 bits → range 0–255 per octet.
Total possible addresses: 2³² ≈ 4.3 billion.
Divided into two logical parts:
Network portion — identifies the network (or subnet).
Host portion — identifies individual devices on that network.


2. Subnet Mask & CIDR Notation

Subnet mask — 32-bit value that separates network bits from host bits (e.g., 255.255.255.0).
CIDR notation (Classless Inter-Domain Routing) — shorthand like /24, where the number after the slash is the count of network bits (leading 1s in the mask).
Example: 192.168.1.0**/24** → first 24 bits = network, last 8 bits = hosts.

Common masks:
/8 → 255.0.0.0 (Class A-like)
/16 → 255.255.0.0 (Class B-like)
/24 → 255.255.255.0 (Class C-like, most common for small networks)


3. Key Calculations & Formulas

Total addresses in a subnet = 2^(32 - prefix_length)
Example: /24 → 2^(32-24) = 2⁸ = 256 addresses.
Usable hosts per subnet = 2^(32 - prefix_length) - 2
(Subtract 2 for: network address + broadcast address.)
Example: /24 → 256 - 2 = 254 usable hosts.
Number of subnets when borrowing bits = 2^n
where n = number of bits borrowed from host portion.
Example: Start with /24, borrow 2 bits → 2² = 4 subnets, new mask /26.
Addresses per subnet after borrowing = 2^(remaining host bits).

4. Subnetting Process (Step-by-Step Summary)

Start with base network (e.g., 192.168.1.0/24).
Determine requirement: number of subnets or hosts per subnet.
Calculate bits to borrow:
For subnets: find smallest n where 2^n ≥ required subnets.
For hosts: find smallest h where 2^h - 2 ≥ required usable hosts, then prefix = 32 - h.

New mask = original prefix + borrowed bits.
Subnet increment (block size) = 256 ÷ number of subnets (or 2^(8 - borrowed bits in last octet)).
List subnets by adding increment repeatedly:
Network, first usable, last usable, broadcast for each.


Example quick calc: 192.168.1.0/24 → need 6 subnets
→ Borrow 3 bits (2³=8 ≥6) → /27 mask (255.255.255.224)
→ Increment = 32
→ Subnets: 192.168.1.0/27, .32/27, .64/27, .96/27, .128/27, .160/27, etc.
→ Each has 32 addresses → 30 usable hosts.
5. CIDR vs. Classful vs. VLSM

Classful (old): Fixed classes A (/8), B (/16), C (/24) — wasteful.
CIDR (modern): Flexible prefix lengths, no class boundaries → efficient allocation + route summarization.
VLSM (Variable Length Subnet Masking): Apply different subnet sizes within the same major network (e.g., one /27 for 30 hosts, one /30 for 2 hosts on a link) → maximizes address usage, reduces waste.
.
TCP/IP Analysis While the OSI model is a generic reference framework, the TCP/IP model is the practical, functional framework that the modern internet is actually built upon
. It simplifies the OSI model by combining OSI layers 5, 6, and 7 into a single Application Layer, and OSI layers 1 and 2 into a single Network Access/Link Layer
.
In a real-world scenario, such as a client loading a web page from a server, the TCP/IP suite operates like this:
Application Layer: The web browser uses HTTP to format the request for the web page
.
Transport Layer: The HTTP request is passed to the Transmission Control Protocol (TCP), which breaks the data into segments and tracks the session using port numbers (e.g., Port 80 for web traffic)
. TCP is connection-oriented, meaning it builds a tracked connection that guarantees reliable delivery, manages retransmissions for lost data, and uses sequence numbers to keep data in order
. In contrast, real-time applications like voice or video might use User Datagram Protocol (UDP) instead, which skips error recovery to prioritize speed
.
Network Layer: The segment is passed to the Internet Protocol (IP), which packages it into a packet and adds the source and destination IP addresses
.
Link/Physical Layer: The packet is wrapped in a frame using a protocol like Ethernet, which adds MAC addresses for local delivery, before being converted into physical signals (like electrical pulses or light) to be sent across the wire
