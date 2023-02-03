# Lecture 7

## UDP: User Datagram Protocol
- no frills, bare bones Internet transport protocol
- "best effort" service, UDP segments may be:
  - lost
  - delivered out-of-order to app
- UDP use:
  - streaming multimedia apps (loss tolerance, rate sensitive)
  - DNS
  - SNMP
  - HTTP/3
- if reliable transfer needed over UDP (e.g., HTTP/3)
  - add needed reliability at application layer
  - add congestion control at application layer

## UDP checksum
- Goal: detect errors (i.e., flipped bits) in trasmitted segment

## Summary: UDP
- "no frills" protocol:
  - segments may be lost, delivered out of order
  - best effort service: "send and hope for the best"
- UDP has its plusses:
  - no setup/handshaking needed (no RTT incurred)
  - can function when network service is compromised

## Principles of reliable data transfer
- important @ application, transport, link layers
  - reliable transport of packets
    - a single sender and a single receiver
  - packet delivery imperfect
    - with bit errors, dropping packets, out-of-order delivery, duplicate copies, long delay, ...

## Reliable data transfer
- underlying channel perfectly reliable
  - no bit errors
  - no loss of packets
- separate FSMs for sender, receiver:
  - sender sends data into underlying channel
  - receiver reads data from underlying channel

## "Stop and Wait" Scenario
- Simple setting: one packet at a time (stop and wait)
  - one sender, one receiver
  - sender has infinite number of packets to transfer to the receiver
  - sender starts one-packet transmission at a time, and will not proceed with the next new packet transmission until the current packet has been successfully received & acknowledged by the receiver

## rdt2.0: channel with bit errors
- How to detect bit errors in packet?
  - internet checksum algorithms
- How to recover from errors?
  - ACKs: receiver explicitly tells sender that pkt received ok
  - NACKs: receiver explicity tells sender that had errors
  - sender retransmits packet upon receiving NAK
- new mechanisms in rdt2.0 (beyond rdt1.0):
  - Error detection at receiver
  - Feedback from receiver: control messages (ACK, NAK) from receiver to sender
  - Retramsission at the sender upon NAK feedback
