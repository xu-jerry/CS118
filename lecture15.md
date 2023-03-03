# Lecture 15

## MAC protocols: taxonomy
- three broad classeS:
  - channel partitioning
    - divide channel into smaller "pieces" (timeslots, frequency, code)
    - allocate piece to node for exclusive use
  - random access

## Random access protocols
- when node has packet to send
  - transmit at full channel data rate R
  - no a priori coordination among nodes
- two or more transmitting nodes: "collision"
- random access MAC protocol specifies:
  - how to detect collisions
  - how to recover from collisions (e.g., via delayed retransmissions)

## Slotted ALOHA
- assumptions:
  - all frames same size
  - time divided into equal size slots (time to transmit 1 frame)
  - nodes start to transmit only slow beginning
  - nodes are synchronized
  - if 2 or more nodes transmit in slot, all nodes detect collision
- operation:
  - when node obtains fresh frame, retransmits in next slot
    - if no collision: node can send new frame in next slot
    - if collision: node retransmits frame in each subsequent slot with probability p until success
- efficiency
  - suppose: N nodes with many frames to send, each transmits in slot with probability p
    - probability that given node has success in a slot = p(1 - p)^(N-1)
    - prob that any node has a success = Np(1 - p)^(N - 1)
    - max efficiency: find p* that maximizes Np(1 - p)^(N - 1)
    - for many nodes, take limit of Np*(1 - p*)^(N - 1) as N goes to infinity, gives:
    - max efficiency = 1/e = .37

## Pure ALOHA efficiency
- even worse than slotted Aloha
- half of optimum value

## CSMA (carrier sense multiple access) 
- simple CSMA: listen before transmit
  - if channel sensed idle: transmit entire frame
  - if channel sensed busy: defer transmission
- human analogy: don't interrupt others
- CSMA/CD: CSMA with collision detection
  - collesions detected within short time
  - colliding transmissions aborted, reducing channel wastage
  - collision detection easy in wired, deifficult with wireless
- human analogy: the polite conversationalist
  - transmission aborted on collision detection

## Ethernet CSMA/CD Algorithm
- NIC receives datagram from network layer, creates frame
- If NIC senses channel
  - if idle: start frame transmission
  - if busy: wait until channel idle, then transmit
- If NIC transmits entire frame without collision, NIC is done with frame!
- If NIC detects another transmission while sendin: abort, send jam signal
- After aborting, NIC enters binary (exponential) backoff
  - after mth collision, NIC chooses K at random from {0, 1, 2, ..., 2^m - 1}. NIC waits K*512 bit times, returns to Step 2
  - more collisions: longer backoff interval

## CSMA/CD
- $T_{prop}$ = max prop delay between 2 nodes in LAN
- $t_{trans}$ = time to transmit max-size frame
- $$efficiency = \frac{1}{1+5t_{prop}/t_{trans}}$$
- efficiency goes to 1
  - as $t_{prop}$ goes to 0
  - as $t_{trans}$ goes to infinity
- better performance than ALOHA: and simple, cheap, decentralized!

## "Taking turns" MAC protocols
- polling:
  - master node "invites" other nodes to transmit in turn
  - typically used with "dumb" devices
  - concerns:
    - polling overhead
    - latency
    - single point of failure (master)
- token passing:
  - control token passed from one node to next sequentially
  - token message
  - concerns:
    - token overhead
    - latency
    - single point of failure (token)

## Cable access network: FDM, TDM, and random
- multiple downstream (broadcast) FDM channels: up to 1.6 Gbps/channel
  - single CMTS transmits into channels
- multiple upstream channels (up to 1 Gbps/channel)
  - multiple access: all users content (random access) for certain upstream channel time slots; others assigned TDM

## DOCSIS
- data over cable service interface specification
- FDM over upstream, downstream frequency channels
- TDM upstream: some slots assigned, some have contention
  - downstream MAP fram: assigns upstream slots
  - request for upstream slots (and data) transmitted random access (binary backoff) in selected slots

## Summary of MAC protocols
- channel partitioning, by time frequency or code
- random access
- taking turns

## MAC addresses
- 32 bit IP address
  - network-layer address for interface
  - used for layer 3 (network layer) forwarding
  - e.g.: 128.119.40.136
- MAC (or LAN or physical or Ethernet) address:
  - function: used "locally" to get frame from one interface to another physically-connected interface (same subnet, in IP-addressing sense)
  - 48-bit MAC address (for most LANs) burned in NIC ROM, also sometimes software settable
  - e.g.: 1A-2F-BB-76-09-AD
    - hex notation
- each interface on LAN
  - has unique 48-bit MAC address
  - has a locally unique 32-bit IP address (as we've seen)

## MAC Addresses
- MAC Address allocation administered by IEEE
- manufacturer buys portion of MAC address space (to assure uniqueness)
- analogy:
  - MAC Address: like Social Security Number
  - IP address: like postal address
- MAC flat address: portability
  - can move interface from one LAN to another
  - recall IP address not portable: depends on IP subnet to which node is attached