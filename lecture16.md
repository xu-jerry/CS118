# Lecture 16

## MAC Addresses
- MAC address allocation administered by IEEE
- manufacturer buys portion of MMAC address space (to assure uniquness)
- MAC flat address: portability
  - can move interface from one LAN to another
- Question: how to determine interface's MAC address, knowing its IP address?
  - ARP table: each IP node (host, router) on LAN has table
    - IP/MAC address mappings for some LAN nodes:
      - <IP address; MAC address; TTL>

## ARP protocol in action
- example: A wants to send datagram to B
  - B's MAC address not in A's ARP table, so A uses ARP to find B's MAC address
- A broadcasts ARP query, containing B's IP addr
  - destination MAC address = FF-FF-FF-FF-FF-FF
  - all nodes on LAN receive ARP query
  - B replies
  - A receives B's reply, adds B into its local ARP table

## Routing to another subnet: addressing
- walkthrough: sending a datagram from A to B via R
  - focus on addressing - at IP (datagram) and MAC layer (frame) levels
  - assume that:
    - A knows B's IP address
    - A knows IP address of first hop router, R
      - DHCP
    - A knows R's MAC address
      - ARP table

## Ethernet
- "dominant" wired LAN technology
  - first widely used LAN technology
  - simpler, cheap
  - kept up with speed race: 10Mbps - 100Gbps
  - single chip, multiple speeds (e.g. Broadcom BCM5761)

## Ethernet: physical topology
- bus: popular through mid 90s
  - all nodes in same collision domain (can collide wih each other)
- switched: prevails today
  - active link-layer 2 switch in center
  - each "spoke" runs a (separate) Ethernet protocol (nodes do not collide with each other)

## Ethernet frame structure
- sending interface encapsulates IP datagram (or other network layer protocol packet) in Ethernet frame

## Switches vs Routers
- both are store and forward
  - routers: network-layer devices (examine network-layer headers)
  - switches: link-layer devices (examine link-layer headers)
