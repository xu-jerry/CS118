# Lecture 11

## Evolving transport-layer functionality
- TCP, UDP: principal transport

## QUIC: Quick UDP Intern Connections
- application-layer protocol, on top of UDP
  - increase performance of HTTP
  - deployed on many Google servers, apps (Chrome, mobile YouTube app)

## Chapter 3: Summary
- principles behind transport layer services: multiplexing, demultiplexing
  - reliable data transfer
  - flow control
  - congestion control
- instantiation, implementation in the Internet
  - UDP
  - TCP

## Chapter 4, Network Layer: The Data Plane
- Layering in Internet Protocol stack

## Network layer: "data plane" roadmap
- network layer: overview
  - data plane
  - control plane
- What's inside a router
  - input ports, switching, output ports
  - buffer management, scheduling
- IP: the Internet Protocol
  - datagram format

## Two key network-layer functions
- forwarding: move packets from a router's input link to appropriate router output link
- routing: determine route taken by packets from source to destination

## Reflections on best-effort service:
- simplicity of mechanism has allowed internet to be widely deployed adopted
- sufficient provisioning of bandwidth
- replicated, application-layer distributed services
- congestion control of "elastic" services helps
