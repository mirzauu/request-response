+----------------+    +-------------------+    +-----------------+    +--------------------+
|                |    |                   |    |                 |    |                    |
|    Browser     |    |       DNS         |    |       TCP       |    |      Server        |
| (Client)       |    |     (Resolver)    |    |  (Connection)   |    |  (Web Server)      |
|                |    |                   |    |                 |    |                    |
+----------------+    +-------------------+    +-----------------+    +--------------------+
        |                     |                     |                       |
        | 1. User Enters URL  |                     |                       |
        |-------------------->|                     |                       |
        |                     |                     |                       |
        | 2. Check Cache      |                     |                       |
        | 3. DNS Lookup       |                     |                       |
        |-------------------->| 4. Query DNS Server |                       |
        |                     |-------------------->|                       |
        |                     | 5. DNS Resolution   |                       |
        |<--------------------|<--------------------|                       |
        |                     |                     |                       |
        | 6. Obtain IP Address|                     |                       |
        |<--------------------|                     |                       |
        |                     |                     |                       |
        | 7. TCP Connection   |                     |                       |
        |-------------------->| 8. SYN              |                       |
        |                     |-------------------->| 9. SYN-ACK            |
        |                     |<--------------------|                       |
        |                     | 10. ACK             |                       |
        |                     |-------------------->|                       |
        |                     |                     |                       |
        | 11. (Optional)      |                     |                       |
        |     TLS Handshake   |                     |                       |
        |-------------------->|                     |                       |
        |                     |<--------------------|                       |
        |                     |                     |                       |
        | 12. HTTP Request    |                     |                       |
        |    Formation        |                     |                       |
        |-------------------->|                     |                       |
        |                     |                     |                       |
        | 13. Send HTTP       |                     |                       |
        |     Request         |                     |                       |
        |-------------------->|                     |                       |
        |                     |                     |                       |
        +---------------------+                     +-----------------------+




Detailed Steps Leading to HTTP Request Headers Formation


User Action: User enters a URL in the browser and presses Enter.

Browser Checks Cache: The browser checks its cache to see if it has a valid, unexpired copy of the requested resource.

DNS Lookup: If the resource is not in the cache, the browser needs to resolve the domain name to an IP address:

Browser Cache: The browser checks its own DNS cache.
Operating System Cache: If not found, it checks the OS's DNS cache.
Router Cache: The OS may query the router’s DNS cache.
ISP DNS Server: If none of the caches have the record, a query is sent to the ISP’s DNS server.
Recursive Query: If necessary, the ISP’s DNS server performs recursive queries to find the authoritative DNS server for the domain.
TCP Connection: Once the IP address is known, the browser establishes a TCP connection to the server using a three-way handshake:

SYN: Client sends a SYN packet.
SYN-ACK: Server responds with a SYN-ACK packet.
ACK: Client sends an ACK packet, completing the handshake.
TLS Handshake (if using HTTPS): If the request uses HTTPS, a TLS handshake occurs to establish a secure connection:

ClientHello: Client sends a ClientHello message to the server.
ServerHello: Server responds with a ServerHello message.
Key Exchange: Client and server exchange keys and establish a secure session.
HTTP Request Formation: Once the TCP (and optionally TLS) connection is established, the browser constructs the HTTP request. This includes forming the request line, headers, and optionally a body.