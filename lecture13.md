# Lecture 13
## Graph abstraction: link costs
- graph: G = (N, E)
- N = set of routers
- E = set of links
- $c_{a, b}$: cost of direct link 

## Routing algorithm classification
- global: all routers have complete topology, link cost info
  - "link state" algorithms
- decentralized: iterative process of computation, exchange of info with neighbors
  - routers initially only know link costs to attached neighbors
  - "distance vector" algorithms
    - local information
- link state is now default used by global internet
- static: routes change slowly over time
- dynamic: much quicker changes

## Dijkstra's link-state routing algorithm
- initialization: distance is infinity if not connected,
- keep iterating, create least cost path tree

## Dijstra's algorithm: discussion
- algorithm complexity: n nodes
  - each of n iteration: need to check all nodes, w, not in N
  - n(n+1)/2 comparisons: O(n^2) complexity
  - more efficient implementations possible: O(n log n)

## Dijkstra's algorithm: oscillations possible
- when link costs depend on traffic volume, route oscillations possible
- sample scenario:
  - routing to dstination a, traffic entering at d, c, e with rates 1, e (<1), 1
  - link costs are directional, and volume-dependent

## Distance vector algorithm
- based on Bellman-Ford equation
- Let $D_x(y)$: cost of least-cost path from x to y
- Then:
  - $D_x(y) = \min_v\{c_{x, v} + D_v(y)\}$
- each node: wait for change or msg
- recompute DV estimates using DV received from neighbor

## Distance vector: link cost cahnges
- node detects local link cost change
- updates routing info, recalculates local DV
- if DV changes, notify neighbors
- "good news travels fast"
- "bad news travels slow"

## Comparison of LS and DV algorithms
- Message complexity
  - LS: n routers, O(n^2) messages sent
  - DV: exchange between neighbors; convergence time varies
- Speed of convergence
  - LS: O(n^2) algorithm, O(n^2) messages
    - may have oscillations
  - DV: convergence time varies
    - may have routing loops
    - count-to-infinity problem
- robustness:
  - LS: router can advertise inforrect link cost
    - each router computes only its own table
  - DV: DV router can advertise incorrect path cost: black-holing
    - each router's table used by others: error propagate through network

## Making routing scalable
- aggregate routers into regions known as "autonomous systems" (AS) (aka "domains")
- intra-AS (aka "intra-domain")
- inter-AS (aka "inter-domain")

## Iter-AS routing
- RIP: Routing Information Protocol [RFC 1723]
  - classic DV: DVs exchanged every 30 secs
  - no longer widely used
- EIGRP: Enhanced Interior Gateway Routing Protocol
  - DV based
  - formerly Cisco-proprietary for decades
- OSPF: Open Shortest Path First [RFC 2328]
  - link-state routing
  - IS-IS protocol (ISO standard, not RFC standard) essentially same as OSPF

## Hierarchical OSPF
- two-level hierarchy: local area, backbone
  - link-state advertisements flooded only in area, or backbone
  - each node has detailed area topology; only knows direction to reach other destinations

## Internet inter-AS routing: BGP
- BGP (Border Gateway Protocol): the de facto inter-domain routing protocol

