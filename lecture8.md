# Lecture 8

## rdt2.2: NAK-free
- duplicate acks mean corrupted signals
- mean the same as NAK

## rdt3.0
- adds timeout for resending packets
- handles packet loss and ack loss
- timeout cannot be smaller than RTT, otherwise premature timeout

## Summary: reliable data transfer
- rdt1.0: nothing
- rdt2.0: error detection via checksum, ACK/NAK, retransmission upon NAK
- rdt2.1: seq# (1 bit) for each pkt
- rdt2.2: A variant to rdt2.0 (no NAK)
- rdt3.0: retransmission upon timeout No NAK, only ACK

## Performance of rdt3.0 (stop-and-wait)
- U_sender: utilization - fraction of time sender busy sending
- performance is terrible!

## rdt3.0: pipelined protocols operation
- pipelining- send multiple packets at a time

## Pipelined protocols: overview
### Go-back-N:
- sender can have up to N unacked packets in pipeline
- receiver only sends cumulative ack
  - does't ack packet if there's a gap
- sender has timer for oldest unacked packet
  - when timer expires, retransmit all unacked packets
### Selective Repeat:
- sender can have up to N unacked packets in pipeline
- receiver sends individual ack for each packet
- sender maintains timer for each unacked packet
  - when timer expires, retransmit only that unacked packet

## Selective repeat: a dilemma
- Q: What relationship is needed between sequence # size and window size to avoid problem in scenario (b)?
  - n+1

## TCP: overview
- point to point
- reliable, in-order byte stream
  - no data "boundaries

## TCP segment structure
- source port #, dest port #
- sequence number
- acknowledgement number
- receive window
- checksum, urg data pointer
- options (variable length)
- application data

## More of the Checksum Field in the TCP header
- the 16-bit checksum field for error-checking of the TCP header, the payload and an IP pseudo-header
- also relies on length of TCP, which gets from IP

## TCP sequence numbers, ACKs
- Sequence numbers:
  - byte stream "number" of first byte in segment's data
- Acknowledgements:
  - seq # of next byte expected from other side
  - cumulative ACK

## TCP round trip time, timeout
- Q: how to set TCP timeout value?
  - longer than RTT, but RTT varies!
  - too short: premature timeout, unnecessary retransmissions
  - too long: slowreaction to segment loss
- Q: how to estimate RTT?
  - Sample RTT: measured time from segment transmission until ACK receipt 
    - ignore retreansmissions
  - SampleRTT will vary, want estimated RTT "smoother"
    - average several recent measurements, not just current SampleRTT
- EstimatedRTT = $(1-\alpha)*$EstimatedRTT + $\alpha*SampleRTT$
- exponential weighted moving average (EWMA)
- influence of past sample decreases exponentially fast
- typical value $\alpha = 1/8$