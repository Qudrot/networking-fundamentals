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
IP Addressing Calculations As noted in our earlier conversation, the provided sources do not contain the mathematical formulas or tools required to perform specific IP addressing or subnetting calculations. However, they do explain the underlying concepts of IP addressing:
An IP address operates at the Network Layer (Layer 3) and is used to route packets across multiple network boundaries
.
An IP address essentially consists of two parts: a network number and a host number, which allows routers to view an entire internetwork as a single network from the outside
.
The sources outline the structure of an IPv4 packet header—which includes 32-bit source and destination IP addresses—and mention that networks can be segmented (subnetting), but they do not provide the calculator functions or mathematical steps to execute that segmentation
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
