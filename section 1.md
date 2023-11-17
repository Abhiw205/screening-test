# Section 1
## Challenge Collapsar (CC) attack

**Cause:**
In a Challenge Collapsar (CC) attack, the attacker uses a proxy server to generate and send a huge number of requests to the target host. Additionally, the attacker floods the system with a large number of data packets to the target server to exhaust its resources. Ultimately, the target server stops responding to requests.

**Identify:**
To identify a CC DDoS attack, monitoring network traffic patterns (i.e., checking if requests are sending the same header) and analyzing server logs (to check which IP addresses are sending identical requests on a regular basis) are crucial. Detection systems can be set up to look for sudden spikes in traffic, especially if there is an abnormal increase in the number of challenge-response interactions. Unusual patterns in the type and frequency of requests can be indicative of a CC DDoS attack.

**Effect:**
The effects of a CC DDoS attack can be severe during high business hours. The targeted service may experience degraded performance and respond with 503 errors or complete downtime, leading to financial losses and overexhaustion of the server in a short period. The attack can also strain network resources and result in increased operational costs, as most applications use a load balancer that auto-scales based on requirements to handle the increased load.

**Mitigation:**
There are two effective methods of DDoS protection to mitigate this particular CC attack:

1. **Geo-restriction:**
   Restrict incoming traffic to specific regions by securing traffic from the main user base's countries and regions. This includes preventing incoming traffic from known "attack regions" such as Russia, Ukraine, and India.

2. **Enabling browser-based challenge:**
   Use a web application firewall (WAF) with challenge-based algorithms to filter out CC attack bots. Built on a global public cloud infrastructure, leverage computing power via Multi CDN to auto-scale defenses proportionate to the attack. This capability allowed us to fend off a 300-million-request-per-minute CC attack.

------------------------------------------------------------------------------------------------------------------------------------
## SYN Flood DDoS attack 

**Cause:**

In a SYN Flood DDoS attack, the attacker exploits the TCP handshake processwhich aims to make a server unavailable to legitimate traffic by consuming all available server resources. The attacker sends a large number of connection requests (SYN packets) to the target server but does not complete the handshake by sending the expected ACK packets. This leads to a depletion of resources on the target server as it maintains partially open connections waiting for completion

**Identify:**

To identify a SYN Flood DDoS attack, monitoring network traffic for an unusually high number of half-open connections is crucial. Detection systems can be set up to analyze the ratio of SYN to ACK packets, and if there is a significant imbalance, it may indicate a SYN Flood attack. Additionally,  the attacker is able to overwhelm all available ports on a targeted server machine, causing the targeted device to respond to legitimate traffic sluggishly or not at all.

**Effect:**

The effects of a SYN Flood DDoS attack can be disruptive. The targeted service experiences a degradation in performance, increased latency, and potential denial of service. The server's resources become exhausted as it tries to handle the influx of incomplete connection requests, leading to a slowdown in legitimate connection establishment and a potential service outage.

**Mitigation:**

Mitigating SYN Flood DDoS attacks involves implementing various strategies:

1. **SYN Cookies:**
   This strategy involves the creation of a cookie by the server. In order to avoid the risk of dropping connections when the backlog has been filled, the server responds to each connection request with a SYN-ACK packet but then drops the SYN request from the backlog, removing the request from memory and leaving the port open and ready to make a new connection.

2. **Firewalls and Load Balancers:**
   Configure firewalls to identify and block malicious SYN packets. Load balancers can distribute incoming traffic effectively, preventing a single server from being a target of the attack.

3. **Increasing Backlog Queue:**
   Each operating system on a targeted device has a certain number of half-open connections that it will allow. One response to high volumes of SYN packets is to increase the maximum number of possible half-open connections the operating system will allow. In order to successfully increase the maximum backlog, the system must reserve additional memory resources to deal with all the new requests

4. **Recycling the Oldest Half-Open TCP connection:**
   This strategy involves overwriting the oldest half-open connection once the backlog has been filled. This strategy requires that the legitimate connections can be fully established in less time than the backlog can be filled with malicious SYN packets

------------------------------------------------------------------------------------------------------------------------------------

## SSL Attack Note DDoS attack 
**Cause:**
In an SSL Attack Note DDoS attack, the attacker targets the SSL/TLS handshake process during the establishment of secure connections. The attacker floods the target server with specially crafted SSL/TLS handshake requests, The Pushdo botnet accomplishes this quite easily by sending garbage data to a target SSL server. The SSL protocol is computationally expensive and it generates extra workload on the server to process garbage data as a legitimate handshake and firewalls don't help in this case because they are usually not capable of differentiating between valid and invalid SSL handshake packets. 

**Identify:**

To identify an SSL Attack Note DDoS attack, monitoring the SSL/TLS handshake process is important. Detection systems can be set up to analyze the rate of incoming SSL/TLS handshake requests and identify abnormal patterns. Anomalies may include an unusually high number of incomplete handshakes or a rapid increase in the volume of SSL/TLS negotiation traffic.

**Effect:**

SSL/TLS Exhaustion DDoS Attacks present a real danger because a single home computer can take down an entire SSL-encrypted web application. A cluster of computers are capable of knocking out a large farm of secured online services. These types of DDoS attacks are highly popular because they require minimal efforts for maximum impact. Each SSL session handshake exhausts 15 times more resources from the server side than from the client side.

**Mitigation:**

Mitigating SSL Attack Note DDoS attacks involves implementing various strategies:

1. **SSL Acceleration and Offloading:**
   Utilize SSL acceleration and offloading techniques to offload the SSL/TLS handshake processing to specialized hardware or dedicated appliances. This helps in reducing the burden on the server's CPU.

2. **Rate Limiting and Connection Monitoring:**
   Implement rate limiting to control the rate of incoming SSL/TLS handshake requests. Connection monitoring systems can identify abnormal patterns, triggering automated responses to block or mitigate suspicious traffic.

3. **SSL/TLS Session Resumption:**
   Enable SSL/TLS session resumption to reduce the computational overhead of repeated handshakes. This allows clients to resume previous sessions, saving resources on both the server and client side.

4. **Content Delivery Networks (CDNs):**
   Employ Content Delivery Networks to distribute SSL/TLS processing geographically. CDNs can absorb and mitigate DDoS attacks by distributing the load across multiple servers in different locations.

5. **Web Application Firewalls (WAF):**
   Deploy WAFs with SSL/TLS inspection capabilities to filter out malicious SSL/TLS handshake requests. WAFs can detect and block abnormal patterns associated with SSL Attack Note DDoS attacks.



