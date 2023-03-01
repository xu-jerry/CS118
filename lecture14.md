# Lecture 14

## Path attributes and BGP routes
- BGP advertised route: prefix + attributes
  - prefix: destination being advertised
  - two important attributes:
    - AS- path: list of ASes through which prefix advertisement has passed
    - NEXT-HOP: indicates specific internal-AS router to next-hop AS
- policy-based routing:
  - gateway receiving route advertisement uses import policy to accept/decline path (e.g., never route through AS Y)
  - AS policy also determines whether to advertise path to other neighboring ASes

## Why different Intra- Inter-AS routing?
- Policy:
  - inter-AS: admin wants control over how its traffic routed, who routes through its network
  - intra-AS: single admin, so policy less of an issue
- scale:
  - hierarchical routing saves table size, reduced update traffic
- performance:
  - intra-AS: can focus on performance
  - inter-AS: policy dominates over performance

## Hot potato routing
- choose local gateway that has least intra-domain cost, don't worry about inter-domain cost!

## ICMP: internet control message protocol
- used by hosts and routers to communicate network-level information
  - error reporting: unreachable host, network, port, protocol
  - eacho request/reply (used by ping)

## Chapter 6: Link Layer
- best effort local packet delivery

## Link Layer: introduction
- terminology
  - hosts and routers: nodes
  - communication channels that connect adjacent nodes along communication path: links 
    - wired

## Link layer: services
- framing, link access
- flow control
- error detection
- error correction
- half-duplex and full-duplex

## Where is the link layer implemented?
- in each and every host
- link layer implemented in network interface card or on a chip

## Error detection
- EDC error detection and correction bits
- not 100% reliable
- parity checking
  - single bit parity
    - detect single bit errors
  - two dimensional bit parity
- Internet checksum
- Cyclic Redundancy Check (CRC)
  - more powerful error-detection coding
  - D: data bits (given, this of these as a binary number)
  - G: bit pattern (generator), of r+1 bits (given)

## Multiple access links, protocols
- two types of "links":
  - point-to-point
    - point-to-point link between Ethernet switch, host
    - PPP for dial-up access
  - broadcast (shared wire or mediun)
    - old-fashioned Ethernet
    - upstream HFC in cable-based access network
    - 802.11 wireless LAN, 4G/4G, satellite

## Multiple access protocols
- single shared broadcast channel
- two or more simultaneous transmissions by nodes: interference
  - collision if node receves two or more signals at the same time

## MAC protocols: taxonomy
- three broad classes:
  - channel partitioning
    - divide channel into smaller "pieces" (time slots, frequency, code)
    - allocate piece to node for exclusive use
  - random access
    - channel not divided, allow collisions
    - "recover" from collisions
  - TDMA: time division multiple access
  - FDMA: frequency division multiple access