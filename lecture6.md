# Lecture 6

## P2P file distribution: BitTorrent
- file divided into 256Kb chunks
- peers in torrent send/receive file chunks

## P2P file distribution
- peer joining torrent:
  - has no chunks, but will accumulate them over time from other peers
  - registers with tracker to get list of peers, connects to subset of peers ("neighbors")
  - while downloading, peer uploads chunks to other peers
  - peer may change peers with whom it exchanges chunks
  - churn: peers may come and go
  - once peer has entire file, it may (selfishly) leave or (altruistically) remain in torrent

## BitTorrent: tit-for-tat
- Alice optimistically unchokes Bob
- Alice becomes one of Bob's top-four providers; Bob reciprocates
- Bob becomes one of Alice's top-four providers

## Video Streaming and CDNs: context
- stream video traffic: major consumer of Internet bandwidth
  - Netflix, YouTube, Amazon Prime: 80% of residential ISP traffic
- challenge: scale - how to reach ~1B users?
  - single mega-video server won't work
- challenge: heterogeneity
  - different users have different capabilities (e.g., wired versus mobile; bandwidth rich versus bandwidth poor)
- solution: distributed, application-level infrastructure

## Multimedia: video
- video: sequence of images displayed at constant rate
  - e.g., 24 images/sec
- digital image: array of pixels
  - each pixel represented by bits
- coding: use redundancy within and between images to decrease # bits used to encode image
  - spatial (within image)
  - temporal (from one image to next)
- CBR: (constant bit rate): video encoding rate fixed
- VBR: (variable bit rate): video encoding rate changes as amount of spatial, temporal changes

## Streaming stored video
- Main challenges:
  - server-to-client bandwidth will varyover time, with changing network congestion levels (in house, in access network, in network core, at video server)
  - packet loss and delay due to congestion will delay playout, or result in poor video quality

## Streaming multimedia: DASH
- DASH: Dynamic, Adaptive Streaming over HTTP
- server:
  - divides video file into multiple chunks
  - each chunk stored, encoded at different rates
  - manifest file: provides URLs for different chunks
- client:
  - periodically measures server-to-client bandwidth
  - consulting manifest, requests one chunk at a time
    - chooses maximum coding rate sustainable given current bandwidth
    - can choose different coding rates at different points in time (depending on available bandwidth at time)
- "intelligence" at client: client determines
  - when to request chunk (so that buffer starvation, or overflow does not occur)
  - what encoding rate to request (higher quality when more bandwidth available)
  - where to request chunk (can request from URL server that is "close" to client or has high available bandwidth)
  - streaming video = encoding + DASH + playout buffering

## Content distribution networks (CDNs)
- challenge: how to stream content (selected from millions of videos) to hundreds of thousands of simultaneous users?
- option 1: single, large "mega-server"
  - single point of failure
  - point of network congestion
  - long path to distant clients
  - multiple copies of video sent over outgoing link
- option 2: store/serve multiple copies of videos at multiple geographically distributed sites (CDN)
  - enter deep: push CDN servers deep into many access networks
    - close to users
    - Akamai: 240,000 servers deployed in more than 120 countries (2015)
  - bring home: smaller number (10s) of larger clusters in POPs near (but not within) access networks
    - used by Limelight

## Case study: Netflix
- many CDNs

# Chapter 3: Transport Layer
## Transport services and protocols
- provide logical communication between application processes running on different hosts
- transport protocols actions in end systems:
  - sender: breaks application messages into segments, passes to network layer
  - receiver: reassembles segments into messages, passes to application layer

## How demultiplexing works
- host receives IP datagrams
- connectionless demultiplexing