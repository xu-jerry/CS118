# Lecture 12

## IP addressing: CIDR
- Classless InternDomain Routing (pronounced "cider")
- subnet portion of address of arbitrary length
- address format: a.b.c.d/x, where x is length

## IP addresses: how to get one?
- That's actually two questions:
1. Q: How does a host get IP address within its network (host part of address)?
2. Q: How does a network get IP address for itself (network part of address)
- How does host get IP address?
  - hard-coded by sysadmin in config file

## DHCP: Dynamic Host Configuration Protocol
- goal: host dynamically obtains IP address from network server when it "joins" network
  - can renew its lease on address in use
  - allows reuse of addresses (only hold address while connected/on)

## DHCP: more than IP addresses
- DHCP can return more than just allocated IP address on subnet:
  - address of first-hop router for client
  - name and IP address of DNS server
  - network mask (indicating network versus host portion of address)


## NAT: network address translation
- NAT: all devices in local network share just one IPv4 address as far as outside world is concerned
- NAT translation table