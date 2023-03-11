# Lecture 17

## Synthesis: a day in the life of a web request
- assuming Bob's laptop first gets connected on Ethernet, which is connected to the router
- DHCP server is running within router
- DHCP to get IP address
- put DHCP message in UDP, encapsulated in IP, encapsulated in 802.3 Ethernet frame, with all 1's, FF:FF...
- broadcast on LAN, received at router
- Ethernet demuxed to IP demuxed UDP demuxed to DHCP
- DHCP server formulates DHCP response containing client's IP address, address of first-hop router for client, and address of DNS server
- encapsulation at HTCP server, fram forwawrded (switch learning) through LAN, demultiplexing at client
- DHCP client receives DHCP ACK reply
  - client now has IP address, knows name & addr of DHS server, IP address of its first-hop router
- before sending HTTP request, need IP of www.google.com: DNS
- DNS query created, encapsulated, in UDP segment
- ARP to determine MAC address of router
- ARP query and then reply
- finally knows MAC address of gateway router

## Chapter 7: Wireless and Mobile Networks