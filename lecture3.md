# Lecture 3

## Why Layering?
- Decomposed complex delivery into fundamental components
- explicit structure allows identifications, relationship of complex system's pieces
  - layered reference model for discussion
- Modularization eases maintenance, updating of system
  - change of implementation of layer's service transparent to the rest of system

## Layering in internet protocol stack
- Application built on
- Reliable transport built on
- Best-effort global packet delivery built on
- Best-effort local packet delivery built on
- physical transfer of bits
- Application: supporting network applications
  - FTP, SMTP, HTTP
- transport: process- process data transfer
  - TCP, UDP
- network: routing of datagrams from source to destination
  - IP, routing protocols
- link: data transfer between neighboring network elements

## ISO/OSI reference model
- presentation: allow applications to interpret meaning of data, e.g. encryption, compression, machine-specific conventions
- session: synchronization, checkpointing, recovering of data exchange
- Internet stack "missing" these layers!

## Application layer: overview
- principles of network applications
- web and HTTP
- E-mail, SMTP, IMAP
- Domain Name System DNS
- P2P applications
- video streaming and content distribution networks

## Some network apps
- social networking
- Web
- text messaging
- e-mail
- multi-user network games
- streaming stored video
- P2P file sharing
- voice over IP
- etc.

## Creating a network app
- write programs that:
  - run on different end systems
  - communicate over network
  - e.g., web server software communicates with browser software
- no need to write software for network-core devices
  - network-core devices do not run user applications
  - applications on end systems allows for rapid app development, propagation

## Question: Do all end systems play the same role?
- No

## Client-server paradigm
- server
  - always-on host
  - permanent IP address
  - often in data centers, for scaling
- clients:
  - contact, communicate with server
  - may be intermittently connected
  - may have dynamic IP addresses
  - do not communicate directly with each other
  - examples: HTTP, IMAP, FTP

## Peer-peer architecture
- no always-on server
- arbitrary end systems directly communicate
- peers request service from other peers, provide service in return to other peers
  - self scalability - new peers bring new service capacity, as well as new service demands
- peers are intermittently connected and change IP addresses
  - complex management
- example: P2P file sharing

## Processes communicating
- process: program running within a host

## Sockets
- process sends/receives messages to/from its socket
- socket analogous to door

## Addressing processes
- to receive messages, process must have identifier
- host device has unique 32-bit IP address
- Q: does IP address of host on which process runs suffice for identifying the process?
  - A: no, many processes can be running on same host
- identifier includes both IP address and port numbers associated with process on host
- example port numbers:
  - HTTP server: 80
  - mail server: 25
- to send HTTP message to gaia.cs.umass.edu web server:
  - IP address: 128.119.245.12
  - port number: 80
- more shortly...

## What transport service does an app need?
- data integrity
  - some apps (e.g. file transfer, web transactions) require 100% reliable data transfer
  - other apps (e.g. audio/vido) can tolerate some loss
- timing
  - some apps (e.g. Internet telephony, interactive games) require low delay to be "effective
- throughput
  - some apps (e.g. multimedia) require minimum amount of throughput to be "effective"
  - other apps ("elastic apps) make use of whatever throughput they get

## Internet transport protocols services
### TCP service:
- reliable transport between sending and receiving process
- flow control: sender won't overwhelm receiver
- congestion control: throttle sender when network overloaded
- does not provide: timing, minimum throughput guarantee, security
- connection-oriented: setup required between client and server processes
### UDP service:
- unreliable data transfer between sending and receiving process
- does not provide: reliability, flow control, congestion control, timing, throughput guarantee, security, or connection setup
  - Q: why bother? Why is there a UDP?

## Securing TCP
- Vanilla TCP & UDP sockets:
  - no encryption
  - cleartext passwords sent into socket traverse Internet in cleartext
- Transport Layer Security (TLS)
  - provides encrypted TCP connections
  - data integrity
  - end-point authentication
- TSL implemented in application layer
  - apps use TSL libraries, that use TCP in turn
- TLS socket API

## 4 Questions in Web and HTTP
1. What content?
   - Web pages
2. How to transfer?
   - HTTP
3. In what messages?
4. Advanced features

## Web Pages
- web page consists of objects, each of which can be stored on difference Web servers
- object can be HTML file, JPEG image, Java applet, audio file
- web page consists of base HTML-file which includes several referenced objects, each addressable by a URL

## HTTP Overview
- HTTP: hypertext transfer protocol
  - web's application layer protocol
  - client/server model:
    - client: browser that requests, receives, (using HTTP protocol) and "displays" Web objects
    - server: Web server sends (using HTTP protocol) objects in response to requests
- HTTP uses TCP
  - client initiates TCP connection to server, port 80
  - server accepts TCP connection from client
  - HTTP messages (application -layer protocol messages) exchanged between browser (HTTP client) and Web server (HTTP server)
  - TCP connection clised
- HTTP is "stateless"
  - server maintains no information about past client requests

## HTTP connections: two types
- Non-persistent HTTP
- Persistent HTTP

## Nonpersistent HTTP
- requires 2 RTTs per object