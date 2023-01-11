# Lecture 1

## What is the Internet?
- global infrastructure that connects computers
- hosts = end systems
  - running netowrk apps
  - billions of connected computing devices
- communication links
  - fiber, copper, radio, ...
  - transmission rate: bandwidth
- routers and switches
  - packet switching: forward packets (chunks of data)

## A closer look at network structure
- network edge
  - hosts: clients and servers
  - servers often in data centers
- access networks, physical media: 
  - wired, wireless communication links
  - (usually what is slow)
- network core:
  - interconnected routers
  - network of networks

## Access network: digital subscriber line (DSL)
- use existing telphone line to central office DSLAM

## Access network: home network
- cable or DSL modem

## Enterprise access networks (Ethernet)
- typically used in companies, universities, etc.
- 100Mbps, 1Gbps, 10Gbps transmission rates
- today, end systems typically connect into Ethernet switch

## Wireless access networks
- shared wireless access network connects end system to router
  - via base station aka "access point"
- wireless LANs
  - within building
- wide-area wireless access
  - provided by telco (cellular) operator, 10's km
  - between 1 and 10 Mbps
  - 3G, 4G, 5G, 3G, LTE, LTE-A, 5G

## Physical media
- bit: propagates between transmitter/receiver pairs
- physical link: what lies between transmitter & receiver
- guided media:
  - signals propagate in solid media: copper, fiber, coax
- unguided media:
  - signals propagate freely, e.g., radio
- twisted pair (TP)
  - two insulated copper wires
- coaxial cable
- fiber optic cable

## Two key network-core functions
- routing: determines source-destination route taken by packets
  - routing algorithms
- forwarding: move packets from router's input to appropriate router output

## Network core: packet-switching
- Packet-switching: hosts break application-layer message into packets
  - forward packets from one router to the next, across links on path from source to destination
  - each packet transmitted at full link capacity
- takes L/R seconds to transmit (push out) L-bit packet into link at R bps
- store and forward: entire packet must arrive at router before it can be transmitted on next link
- end-end delay = 2L/R (assuming zero propagation delay)
- one-hop numerical example:
  - L = 7.5 Mbits
  - R = 1.5 Mbps
  - one-hop transmission delay = 5 s

## Alternative core: circuit switching
- end-end resources allocated to, reserved for voice "call" btw. source & dest
- Example: each link as four circuits
- dedicated resources: no sharing
  - circuit-like (guaranteed) performance
- circuit segment idle if not used by call (no sharing)
- Commonly used in traditional telephone networks