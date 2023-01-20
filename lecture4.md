# Lecture 4

## Non-persistent HTTP vs persistent HTTP
- a web page (base html) with 10 (small) referenced objects
- How long to complete all?
  - ignore the object transmission time
  - 2 RTT = 2 RTT * 10 = 22 RTT
- Persistent HTTP
  - 2 RTT + 10 RTT = 12 RTT
- non-persistent HTTP (5 objects in parallel)
  - 2 RTT + 2 RTT (1~5 objects) + 2 RTT (6~10 objects) = 6 RTT
- 1. index.html
- 2. objects

## HTTP request message
- two types of HTTP messages: request, response
- HTTP request message:
  - request line (GET, POST, HEAD commands)
  - header lines
  - carriage return, line feed at start of line indicates end of header lines

## Other HTTP request messages
- POST method
  - web page often includes form input
  - user input sent from client to server in entity body of HTTP POST request message
- GET method
  - include user data in URL field of HTTP GET request message (following a '?')
- HEAD method
  - requests headers that would be returned if specified URL were requested with an HTTP GET method
- PUT method
  - uploads new file (object) to server
  - completely replaces file that exists at specified URL with content in entity body of POST HTTP request message

## HTTP response status codes
- status code appears in 1st line in server-to-client response message
- some sample codes:
  - 200 OK
    - request succeeded, requested object later in this message
  - 301 Moved Permanently
  - 400 Bad Request
  - 404 Not Found
  - 505 HTTP Version not supported

## Questions on basic HTTP
- HTTP is stateless
  - the server can't infer whether the client visits her before
- However, it is concenient and friendly to know that
  - Amazon example
- In CS@UCLA, many want to watch the same video at Youtube
- Basic HTTP: many connections over many communication links
  - throughput bottleneck
- Your experience at Youtube
- How to solve it?

## Cookies
- What cookies can be used for:
  - authorization
  - shopping carts
  - recommendations
  - user session state
- Challenge: How to keep state:
  - protocol endpoints: maintain state at sender/receiver over multiple transactions
  - cookies: HTTP messages carry state

## Web caches (proxy servers)
- Goal: satisfy client request without involving origin server
- user configures browser to point to a Web cache
- browser sends all HTTP requests to cache
  - if object in cache: cache returns object to client
  - else cache requests object from origin server, caches receved object, then returns object to client

## Conditional GET
- Goal: don't send object if cache has up-to-date cached version
  - no object transmission delay
  - lower link utilization
- cache: specify date of cached copy in HTTP request
- server: response contains no object if cached copy is up-to-date
  - HTTP/1.0 304 Not Modified

## HTTP/2
- Key goal: decreased delay in multi-object HTTP requests
- not FCFS
- split into smaller chunks, can send out of order

## HTTP/3
- adds security, per object error and congestion control over UDP

## Email
- Three major components:
  - user agents
  - mail servers
  - simple mail transfer protocol: SMTP
- User Agent
  - aka "mail reader"
  - composing, editing, reading mail messages
  - e.g., Outlook, iPhone mail client
  - outgoing, incoming messages stored on server

## Mail message format
- RFC 531 defins SMTP protocol
- RFC 822 defines syntax for email message itself (like HTML)