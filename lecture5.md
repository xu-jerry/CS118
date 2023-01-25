# Lecture 5

## Application Layer: Overview
- Domain Name System DNS
- Basic Function: find the IP address, given the host name (name -> IP address translation)
- Why and What is DNS?
- How DNS works?

## Why DNS?
- Application: host-to-host, process-to-process communication
  - Process identifier: IP address and port number
- IDs for Internet hosts, routers:
  - "name", e.g. google.com- used by humans
  - IP address (32 bit) - 173.194.204.99, used for addressing datagrams, used by routers
- Q: how to map between IP address and name, and vice versa?

## DNS Services
- hostname to IP address translation
- host aliasing
  - canonical, alias names
- mail server aliasing
- load distribution
  - replicated Web servers: many IP addresses correspond to one name
- Q: Why not centralize DNS?
  - single point of failure
  - traffic volume
  - distant centralized database
  - maintenance
- A: doesn't scale!
- distributed database implemented in hierarchy of many name servers
- application-layer protocol: hosts, name servers communicate to resolve names (address/name translation)
  - note: core Internet function, implemented as application -layer protocol
  - complexity at network's "edge"

## Key design concepts in DNS System
- Names are heirarchial
  - no flat names
  - Hierarchical names (e.g. kiwi.cs.ucla.edu)
    - Highest hierarchy: edu, com, gov, org, ... us, jp, fr
    - next-level hierarchy: ucla, mit, ... google, ibm, ca, il
  - Hierarchical names form the name space hierarchy
- Name servers are also organized into a hierarchy
- Name resultion follows the hierarchy to resolve names to IP addresses

## DNS: routing
- official, contact-of-last-resort by name servers that can not resolve name
- incredibly important internet function
  - Internet couldn't function without it
  - DNSSEC - provides security (authentication and message integrity)
- ICANN (Internet Corporation for Assigned Names and Numbers) manages root DNS domain

## Local DNS
- does not strictly belong to hierarchy
- each ISP has one
  - also called "default name server"
- when host makes DNS query, query is setnt to its local DNS server
  - has local cache of recent name-to-address translation pairs (but may be out of date!)
  - acts as proxy, forwards query into hierarchy

## DNS name
- Example: host at engineering.nyu.edu
- wants IP address for gaia.cs.umass.edu
- Iterated query:
  - contacted server replies with name of server to contact
  - "I don't know this name, but ask this server"
- Recursive query:
  - puts burden of name resultion on contacted name server
  - heavy load at upper levels of hierarchy?

## Caching
- once (any) name server learns mapping, it caches mapping
  - cache entries timeout (disappear) after some time (TTL)
  - TLD servers typically cahced in local name servers
    - thus root name servers not often visited
  - cached entries may be out-of-date (best-effort name-to-address translation!)
    - if name host changes IP address, may not be known Internet-wide until all TTLs expired
  - update/notify mechanisms proposed IETF standard
    - RFC 2136

## DNS records
- DNS: distributed database storing resource records (RR)
- RR format: {name, value, type, ttl}
- type = A
  - name is hostname
  - value is IP address
- type = NS
  - name is domain (e.g., foo.com)
  - value is hostname of authoritative name server for this domain
- type = CNAME
  - name is alias name for some "canonical" (the real) name

## DNS protocol messages
- DNS query and reply messages, both have same format

## Inserting records into DNS
- register at DNS registrar
- create authoritative server locally with IP address

## DNS security
- DDoS attacks
  - bombard root servers with traffic
    - not successful to date
    - traffic filtering
    - local DNS servers cahce IPs of TLD servers, allowing root server bypass
  - bombard TLD servers
    - potentially more dangerous
- Redirect attacks
  - man-in-middle
    - intercept DNS queries
  - DNS poisoning
    - send bogus relies to DNS server, which caches
- Exploit DNS for DDoS
  - send queries with spoofed source address: target IP
  - requires amplification

## Peer-to-peer (P2P) architecture
- no always-on server
- arbitrary end systems directly communicate
- peers request service from other peers, provide service in return to other peers
  - self scalability - new peers bring new service capacity, and new service demands
- peers are intermittently connected and change IP addresses
  - complex management
- examples: P2P file sharing (BitTorrent), streaming (KanKan), VolP (Skype)

## File distribution time: client-server
- server transmission: must sequentially send (upload) N file copies
  - time to send one copy: $F/u_s$
  - time to send N copies: $NF/u_s$
- client: each client must download file copy
  - $d_{min}$ = min client download rate
  - min client download time $F/d_{min}$
  - time to distribute F to N clients using client-server approach $D_{c-s}$
  - linear

## File distribution time: P2P
- server transmission: must upload at least one copy:
  - time to send one copy: F/u_s
- client: each client must download file copy
  - min client download time: F/d_min
  - clients: as aggregate must download NF bits
    - max upload rate (limiting max download rate is $u_s + \sum u_i$)
  - time to distribute F to N clients using P2P approach
  - $D_{P2P} \ge max\{F/u_s, F/d_{min}, NF/(u_s+\sum u_j)\}$
  - flattens out, does not grow linearly