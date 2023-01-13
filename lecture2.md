# Lecture 2

## Circuit switching
- FDM vs TDM (frequency division multiplexors vs time division multiplexors)
- users use different frequencies or different time slots

## Packet switching vs circuit switching
- Q: Why packet switching is chosen by the Internet?
- packet switching allows more users to use network
- example:
  - 1Mb/s link
  - each user:
    - 100 kb/s when "active"
    - active 10% of the time
  - for circuit switching, max of 10 users
  - with packet switching, with 35 users, the probability more than 10 users at 1 time is 0.04%
  - Given N users, the probability that x users are active is $P(N, x)= {N \choose k} p^x(1-p)^{N-x}$
- Q: Is packet switching a "slam dunk winner?"
  - great for bursty data
    - resource sharing
    - simplier, no call setup
  - excessive congestion possible: packet dely and loss (see the following slides)
    - protocols needed for reliable data transfer, congestion control
- Q: human analogies of reserved resources (circuit switching) versus on-demand allocation (packet-switching)?

### Option 1: every ISP connected to every ISP
- O(N^2) connections
### Option 2: one Global ISP
- single point of failure
- monopoly, no free market
### multiple Global ISPs
### Internet structure: network of networks
- at center: small # of well-connected large networks
- "tier-1" commercial ISPs (e.g. Google)
### Option 3: Hierarchiacal structure

## Host: sends packets of data (Recap)
- host sending function:
- takes application message
- breaks into smaller chunks, known as packets of length L bits
- transmits packet into access network at transmission rate R
  - link transmission rate, aka link capacity, aka link bandwidth
  - packet transmission delay = time needed to transmit L-bit packet into link = $\frac{L}{R}$

## Packet Switching: queueing delay, loss
- if arrival rate (in bits) to link exceeds transmission rate of link for a period of time:
  - packets will queue, wait to be transmitted on link
  - packets can be dropped (lost) if memory (buffer) fills up

## Four sources of packet delay
- $d_{nodal}=d_{proc} + d_{queue} + d_{trans}+d_{prop}$
- $d_{proc}$: nodal processing
  - check bit errors
  - determine output link
  - typically < msec
- $d_{queue}$: queueing delay
  - time waiting at output link for transmission
  - depends on congestion level of router
- $d_{trans}$: transmission delay:
  - L: packet length (bits)
  - R: link bandwidth (bps)
  - $d_{trans}$ = L/R
- $d_{prop}$: propagation delay:
  - d: length of physical link
  - s: propagation speed (~2x10^8 m/sec)
  - $d_{prop} = d/s$

## "Real Internet delays and routes
- traceroute program: provides delay measurement from source to router

## Throughput
- throughput: rate (bits/time unit) at which bits transferred between sender/receiver
  - instantaneous: rate at given point in time
  - average: rate over longer period of time

## 3 major metrics
- throughput, delay, loss

## What's the Internet: a software view
- protocols control sending, receiving msgs
  - e.g. HTTP, Skype, TCP, IP, 802.11
- Internet standards: standardize protocol speicifcations
  - RFC: Request for comments
  - IETF: Internet Engineering Task Force

## Protocol
- define format, order of messages sent and received among network entities, and actions taken on msg transmission, receipt

## Internet Protocol "layers"
- Networks are complex, with many pieces
  - hosts
  - routers
  - links of various media
  - applications
  - protocols
  - hardware, software
- Layers: Application, Transport, Network, Link, Physical