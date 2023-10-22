# Computer Networking Top Down Approach



{{< admonition type=note title="" open=false >}}

I made this note based on Computer Networking A Top-Down Approach Seventh Edition.

{{< /admonition >}}


{{< admonition type=warning title="" open=false >}}

The note is made for the sole purpose of reviewing what i learned and understood from the book.Some statements and descryptions might be subjective and incorrect.If you have doubts please leave comments or contact me.

{{< /admonition >}}



> # Chapter 1 Computer Networks and the Internet



- End systems are connected together by a network of <mark>communication links</mark> and<mark> packet switches</mark>.
- When one end system has data to send to another end system, the sending end systemsegments the data and adds header bytes to each segment. The resulting packages of information, known as <mark>packets</mark>.
-  the two most prominent types in today’s Internet are <mark> routers </mark> and <mark> link-layer switches</mark>
-   The sequence of communication
links and packet switches traversed by a packet from the sending end system to the receiving end
system  is known as a <mark>route</mark> or <mark>path</mark> through the network.
-  ISPs : Internet Service Providers 
-  <mark> Store-and-forward
transmission</mark> means that the packet switch must receive the entire packet before it can begin to transmit
the first bit of the packet onto the outbound link.
- If an arriving packet needs to be
transmitted onto a link but finds the link busy with the transmission of another packet, the arriving packet must wait in the <mark> output buffer </mark>. Thus, in addition to the store-and-forward delays, packets suffer <mark> output
buffer queuing delays </mark>.
- arriving packet may find that the buffer is completely full with other packets waiting for transmission. In
this case, <mark> packet loss </mark> will occur—either the arriving packet or one of the already-queued packets will
be dropped.
-  a router uses a packet’s destination address to index a forwarding table and determine the appropriate outbound link
- There are two fundamental approaches to moving data through a network of links and switches: <mark> circuit
switching </mark> and <mark> packet switching </mark>.
- In circuit-switched networks, the resources needed along a path (buffers, link transmission rate) to
provide for communication between the end systems are<mark> reserved </mark>for the duration of the communication
session between the end systems.
- A circuit in a link is implemented with either <mark>frequency-division multiplexing (FDM)</mark> or<mark> time-division
multiplexing (TDM)</mark>.
- The most important of these delays are the <mark>nodal processing delay </mark>,<mark> queuing delay </mark>,<mark> transmission delay </mark>, and<mark> propagation delay </mark>;
- The time required to examine the packet’s header and determine where to direct the packet is part of the <mark> processing delay</mark>.
- <mark>Transmission Delay</mark>:amount of time required to push (that is, transmit) all of the packet’s bits into the link.
- The time required to propagate from
 the beginning of the link to router B is the <mark>propagation delay</mark>.
-  let<mark> a </mark>denote the<mark> average rate at which packets arrive at the queue</mark> (a is in units of packets/sec).
Recall that R is the transmission rate; that is, it is the <mark>rate (in bits/sec) at which bits are pushed out of the
queue</mark>. Also suppose, for simplicity, that all packets consist of <mark>L bits</mark>. Then the average rate at which bits
arrive at the queue is <mark>La</mark> bits/sec.  The ratio La/R,is called the traffic intensity.

-  If <mark>La/R > 1</mark>, then the average rate at which
bits arrive at the queue exceeds the rate at which the bits can be transmitted from the queue. In this unfortunate situation, the queue will tend to increase without bound and the queuing delay will approach<mark>
infinity</mark>.

- a packet can arrive to find a <mark>full</mark> queue.With no place to store such a packet, a router will <mark>drop</mark> that packet; that is, the packet will be<mark> lost</mark>.
  
- a lost packet may be <mark>retransmitted</mark> on an end-to-end basis in order to ensure that all data are eventually transferred from source to destination.
-  In VoIP, the sending side must first fill a packet with encoded digitized speech
before passing the packet to the Internet. <mark>This time to fill a packet</mark>—called the <mark>packetization delay</mark>—can be significant and can impact the user-perceived quality of a VoIP call
-  The instantaneous throughput at any instant of time is the <mark>rate (in bits/sec) at
which client is receiving the file</mark>.
- If there are multiple links , the thoroughput is the <mark>bottleneck</mark> of transmission rate.
- when there is no other intervening traffic, the throughput can simply be approximated as the <mark>minimum transmission rate</mark> along the path between source and destination.
- The Internet protocol stack consists of five layers: the <mark>physical</mark>, <mark>link</mark>, <mark>network</mark>, <mark>transport</mark>, and <mark>application</mark> layers.
- link-layer switches implement layers 1 and 2; routers implement layers 1 through 3.
-  DoS attacks fall into one of three categories:
 1. <mark>Vulnerability attack</mark>. This involves sending a few well-crafted messages to a vulnerable application or operating system running on a targeted host. If the right sequence of packets is sent to a vulnerable application or operating system, the service can stop or, worse, the host can crash.
 2. <mark>Bandwidth flooding</mark>. The attacker sends a deluge of packets to the targeted host—so many packets that the target’s access link becomes clogged, preventing legitimate packets from reaching the server.
 3. <mark>Connection flooding</mark>. The attacker establishes a large number of half-open or fully open TCP connections (TCP connections are discussed in Chapter 3) at the target host. The host can become
so bogged down with these bogus connections that it stops accepting legitimate connections.
-  A passive receiver that records a copy of every packet that flies by is called a <mark>packet
sniffer</mark>.
- The ability to inject packets into the Internet with a false source address is known as <mark>IP spoofing</mark>, and is but one of many ways in which one user can masquerade as another user.To solve this problem, we will need <mark>end-point authentication</mark>.

> # Chapter 2 Application Layer


-  two predominant architectural paradigms:the <mark>client-server architecture</mark> or the <mark>peer-to-peer (P2P) architecture</mark>.
-  A process sends messages into, and receives messages from, the network through a software interface called a <mark>socket</mark>,also referred to as the Application Programming Interface (API) between the application and the network.
-  We can broadly classify the possible services provided by transport-layer protocol along four dimensions: <mark>reliable data transfer</mark>, <mark>throughput</mark>, <mark>timing</mark>,and <mark>security</mark>.
-  When an application invokes TCP as its transport protocol, the application receives both of these services from TCP：<mark>Connection-oriented service</mark>,<mark>Reliable data transfer service</mark>,<mark> congestion-control mechanism  </mark>.
-  UDP is connectionless, so there is no handshaking before the two processes start to communicate. 
-  UDP provides an unreliable data transfer service.
-  UDP does not include a congestion-control mechanism.

> ## 2.1 HTTP

-  HTTP is said to be a <mark>stateless</mark> protocol: server sends requested files to clients <mark>without storing any state
information</mark> about the client.
- Non-Persistent:each request/response pair be sent over a <mark>separate TCP connection</mark>.
- Persistent Connections:all of the requests and their corresponding responses be sent over the <mark>same TCP connection</mark>.
- HTTP uses persistent connections in its default mode.
-  the steps of transferring a Web page from server to client for the case of non-
persistent connections: Let’s suppose the page consists of a base HTML file and 10 JPEG images/computer_networking_topdown, and that all 11 of these objects reside on the same server.Further suppose the URL for the base HTML file
is:http://www.someSchool.edu/someDepartment/home.index

Here is what happens:
1.  The HTTP client process initiates a <mark>TCP connection</mark> to the server  www.someSchool.edu on port number 80, which is the default port number for HTTP. Associated with the TCP connection, there will be a socket at the client and a socket at the server.
2. The HTTP client sends an <mark>HTTP request message</mark> to the server via its socket. The request message includes the path name  /someDepartment/home .index. (We will discuss HTTP messages in some detail below.)
3.  The HTTP server process receives the request message via its socket, retrieves the object from path: /someDepartment/home.index from its storage (RAM or disk), encapsulates the object in an <mark>HTTP response message</mark>, and sends the response message to the client via its socket.
4.  The HTTP server process tells TCP to <mark>close</mark> the TCP connection. (But TCP doesn’t actually terminate the connection until it knows for sure that the client has received the response message intact.)
5.  The HTTP client receives the response message. The TCP connection terminates. The message indicates that the encapsulated object is an HTML file. The client extracts the file from the response message, examines the HTML file, and finds references to the 10 JPEG objects.
6. The first four steps are then repeated for each of the referenced JPEG objects.


- round-trip time (RTT), is the time it takes for a <mark>small packet</mark> to travel from client to server and then back to the client.
- The RTT includes <mark>packet-propagation delays</mark>, <mark>packet-queuing delays</mark> in intermediate routers and switches, and <mark>packet-processing delays</mark>.(the packet is small so there is no transmission delay)
- Non-persistent connections have some shortcomings. 
  1. a brand-new connection must be
established and maintained for each requested object. For each of these connections, <mark>TCP buffers must be allocated and TCP variables must be kept in both the client and server</mark>. This can place a significant burden on the Web server, which may be serving requests from hundreds of different clients simultaneously. 
  2. each object suffers a delivery delay of <mark>two RTTs</mark>—one RTT to <mark>establish the TCP connection</mark> and one RTT to <mark> request and receive an object</mark>.


-  The first line of an HTTP request message is called the <mark>request line</mark>,the subsequent lines are called the <mark>header lines</mark>.

> ### 2.1.1 Request Message

![http_req](/images/computer_networking_topdown/http_req.png)

- The request line has three fields: the <mark>method field</mark>, the <mark>URL</mark> field, and the <mark>HTTP version</mark> field.




- The method field can take on several different values, including <mark>GET</mark>, <mark>POST</mark>,<mark>HEAD</mark>,<mark>PUT</mark>,and <mark>DELETE</mark>
- The header lines:
    1. Host: xxx.xxx.xxx specifies the host on which the object resides.
    2. Connection:close/keep-alive header line tells the server to set the connection to whether <mark>persistent</mark> or <mark>non-persistent</mark>.
    3. The  User-agent: header line specifies the user agent, that is, the <mark>browser type</mark> that is making the request to the server.
- after the header lines there is an <mark>entity body</mark>.The entity body is <mark>empty with the  GET</mark> method, but is <mark>used with the  POST</mark> method.
- HTML form elements often use the GET method and include the inputted data (in the form fields) in the <mark>requested URL</mark>
- The  <mark>HEAD</mark> method is similar to the  GET method. When a server receives a request with the  HEAD method, it responds with an HTTP message but it <mark>leaves out the requested object</mark>.
- The  PUT method allows a user to upload an object to a specific path (directory) on a specific Web server. 
- The  DELETE method allows a user, or an application, to delete an object on a Web server.

> ## 2.1.2 Response Message


![http_res](/images/computer_networking_topdown/http_res.png)

- HTTP response message has three sections:
    1. Initial status line:The status line has three fields: the protocol version field, a status code, and a corresponding status message.
    2. Header lines:
        - Date:  indicates the time and date when the HTTP response was created and sent by the server. Note that this is not the time when the object was created or last modified; it is the time <mark>when the server retrieves the object from its file system, inserts the object into the response message, and sends the response message</mark>.
        - Content-Type: indicates the type of the object in the entity body. 
    3. Entity line.

{{< admonition type=info title="" open=false >}}
The object type is officially indicated by the <mark>Content-Type</mark>: header and not by the file extension.
{{< /admonition >}}

{{< admonition type=info title="" open=false >}}
Some common status codes and
associated phrases include:
 1. 200 OK: Request succeeded and the information is returned in the response.
 2. 301 Moved Permanently: Requested object has been permanently moved; the new URL is specified in  Location: header of the response message. The client software will automatically retrieve the new URL.
 3. 400 Bad Request: This is a generic error code indicating that the request could not be understood by the server.
 4. 404 Not Found: The requested document does not exist on this server.
 5. 505 HTTP Version Not Supported: The requested HTTP protocol version is not supported by the server.
 6. 304 Not Modified:The web server informs the cache that the requested resource is not modified and go send the cached copy to the client.
{{< /admonition >}}


> ### 2.1.3 Cookies

- cookie technology has four components: 
  1. a cookie header line in the HTTP response message; 
  1. a cookie header line in the HTTP request message; 
  2. a cookie file kept on the
user’s end system and managed by the user’s browser; 
  1. a back-end database at the Web site.

- How the cookies work:
  1. request comes into the Web server, the server creates a unique identification number and creates an entry in its back-end database that is indexed by the identification number. The Web server then responds to client’s browser, including in the HTTP response a <mark>Set-cookie</mark>: header, which contains the identification number.
  2. When Client’s browser receives the HTTP response message, it sees the  <mark>Set-cookie</mark>: header. The browser then appends a line to the special cookie file that it manages. This line includes the hostname of the server and the identification number in the  Set-cookie: header.
  3.  As client continues to browse the site, each time he requests a Web page, his browser consults his cookie file,extracts his identification number for this site, and puts a <mark>Cookie</mark> header line that includes the identification number in the HTTP request. 
  4. In this manner, the server is able to track client’s activity at the  site. 

> ### 2.1.4 Web Cache(Proxy)

- A Web cache—also called a proxy server—is a network entity that satisfies HTTP requests on the behalf of an origin Web server.
- A user’s browser can be configured so that all of the user’s HTTP requests are first directed to the Web cache.
- How does web cache work:
  1.  The browser establishes a TCP connection to the Web cache and sends an HTTP request for the object to the Web cache.
  2.  The Web cache checks to see if it has a copy of the object stored locally:
      1. If it does, the cache performs an up-to-date check by issuing a conditional GET to the web server telling the server to send the object only if the object has been modified since the specified date:
          - If it does then the object is updated.
          - If it doesn't the object remains the same
  
          The Web cache returns the object within an HTTP response message to the client browser.

      2. If the Web cache does not have the object, the Web cache opens a TCP connection to the web server, The Web cache then sends an HTTP request for the object into the cache-to-server TCP connection. After receiving this request, the origin server sends the object within an HTTP response to the Web cache.
  3. When the Web cache receives the object, it stores a copy in its local storage and sends a copy, within an HTTP response message, to the client browser (over the existing TCP connection between the client browser and the Web cache).

- The benefits of a web cache:

  1. First, a Web cache can substantially reduce the <mark>response time</mark> for a client request.
  2. Second, Web caches can substantially <mark>reduce traffic</mark> on an institution’s access link to the Internet


- HTTP has a mechanism that allows a cache to <mark>verify that its objects are up to date</mark>. This mechanism is called the <mark>conditional GET</mark>



> ## 2.2 SMTP

- A typical message starts its journey in <mark>the sender’s user agent</mark>, travels to <mark>the sender’s mail server</mark>, and travels to <mark>the recipient’s mail server</mark>, where it is deposited in the recipient’s mailbox.


- How SMTP works:


1.  Alice invokes her user agent for e-mail, provides Bob’s e-mail address (for example,bob@someschool.edu), composes a message, and instructs the user agent to send the message.
2.  Alice’s user agent sends the message to her mail server, where it is placed in a message queue.
3.  The client side of SMTP, running on Alice’s mail server, sees the message in the message queue. It opens a TCP connection to an SMTP server, running on Bob’s mail server.
4.  After some initial SMTP handshaking, the SMTP client sends Alice’s message into the TCP connection.
5.  At Bob’s mail server, the server side of SMTP receives the message. Bob’s mail server then
places the message in Bob’s mailbox.
1.  Bob invokes his user agent to read the message at his convenience.

- Five commands in SMTP:
  1. HELO (an abbreviation for HELLO)  
  2. MAIL FROM  
  3. RCPT TO  
  4. DATA
  5. QUIT

- SMTP uses <mark>persistent connection</mark>.
- MTP requires each message, including the body of each message, to be in <mark>7-bit ASCII format</mark>.
- A mail access protocol is used to transfer mail from <mark>the recipient’s mail server to the recipient’s user agent</mark>.
- There are currently a number of popular mail access protocols, including Post Office Protocol—Version 3 (POP3), Internet Mail Access Protocol (IMAP), and HTTP.



> ## 2.3 DNS

- The DNS protocol runs over <mark>UDP</mark> and uses port 53.
- How DNS works(approximately):
  1.  The browser extracts the <mark>hostname</mark>,  from the URL and passes the hostname to the client side of the DNS application.
  2.  The DNS client sends a query containing the hostname to a <mark>DNS server</mark>.
  3.  The DNS client eventually receives a reply, which includes the IP address for the hostname.
  4.  Once the browser receives the IP address from DNS, it can initiate a TCP connection to the HTTP server process located at port 80 at that IP address

- The desired IP address is often cached in a “nearby” DNS server, which helps to reduce DNS network traffic as well as the average DNS delay.



- DNS provides services such as:
  1. Host aliasing
  2. Mail server aliasing
  3. Load distribution

- there are three classes of DNS servers:
  1. root DNS servers
  2. top-level domain (TLD) DNS servers
  3. authoritative DNS servers

- How DNS works(in detail):
  1. The client first contacts one of the root servers,which returns IP addresses for TLD servers for the top-level domain  com. 
  2. The client then contacts one of these TLD servers, which returns the IP address of an authoritative server for  amazon.com. 
  3. Finally,the client contacts one of the authoritative servers for amazon.com, which returns the IP address for the hostname www.amazon.com.

- 2 query methods in DNS:<mark>recursive queries</mark> and<mark> iterative queries</mark>


- Typically,The query <mark>from the requesting host to the local DNS server</mark> is recursive, and <mark>the remaining queries</mark> are iterative.
- The DNS servers that together implement the DNS distributed database store <mark>resource records (RRs)</mark>
- A resource record is a four-tuple that contains the following fields:
  1. Name 
  2. Value
  3. Type
  4. TTL
  
- TTL is the time to live of the resource record; it determines <mark>when a resource should be removed from a cache</mark>.
- If  Type=A, then  Name is a <mark>hostname</mark> and  Value is the <mark>IP address</mark> for the hostname.
- If  Type=NS, then  Name is a <mark>domain</mark> (such as  foo.com) and  Value is the <mark>hostname of an authoritative DNS server that knows how to obtain the IP addresses for hosts in the domain</mark>.
- If  Type=CNAME, then  Value is a <mark>canonical hostname</mark> for the alias hostname  Name.
- If  Type=MX, then  Value is the <mark>canonical name</mark> of a mail server that has an alias hostname  Name.


> ## 2.4 Video Streaming

- A video is a sequence of images, typically being displayed at a constant rate, for example, at 24 or 30 images.
- the network must provide an average throughput to the streaming application that is at least <mark>as large as the bit rate of the compressed video</mark>.
- In HTTP streaming, the video is simply stored at an HTTP server as an ordinary file with a specific URL.
- How HTTP streaming works:
  1. When a user wants to see the video, the client establishes a TCP connection with the server and issues an HTTP  GET request for that URL. 
  2. The server then sends the video file, within an HTTP response message.
  3. On the client side, the bytes are collected in a client application buffer. 
  4. Once the number of bytes in this buffer exceeds a predetermined threshold, the client application begins playback—specifically, the streaming video application periodically grabs video frames from the client application buffer, decompresses the frames, and displays them on the user’s screen. 

- Dynamic Adaptive Streaming over HTTP(DASH):The client dynamically requests chunks of video segments of a few seconds in length. When the amount of available bandwidth is high, the client naturally selects chunks from a high-rate version; and when the available bandwidth is low, it naturally selects from a low-rate version.

> ## 2.5 Content Distribution Networks


- A CDN manages servers in multiple geographically distributed locations, stores copies of content in its servers, and attempts to direct each user request to a CDN location that will provide the best user experience.


- How CDN works:
  1.  The user’s host sends a DNS query for the host name of the requested resource.
  2.  The user’s Local DNS Server (LDNS) relays the DNS query to an authoritative DNS server for the hostname, which observes in the hostname that this belongs to CDN. To “hand over” the DNS query to CDN, instead of returning an IP address, the authoritative DNS server returns to the LDNS a hostname in the CDN’s domain.
  3.  The user’s LDNS then sends a second query, now for the hostname provided in 2, and CDN’s DNS system eventually returns the IP addresses of a <mark>CDN content server</mark> to the LDNS. 
  4.  The LDNS forwards the IP address of the content-serving CDN node to the user’s host.
  5.  Once the client receives the IP address for a CDN content server, it establishes a direct TCP connection with the server at that IP address and issues an HTTP GET request for the content. 

  

> # Chapter 3 Transport layer

- Port number is the identifier of the socket.

- Extending host-to-host delivery to process-to-process delivery is called transport-layer multiplexing and demultiplexing.


- This job of delivering the data in a transport-layer segment to the correct socket is called demultiplexing.
- The job of gathering data chunks at the source host from different sockets,encapsulating each data chunk with header information to create segments, and passing the segments to the network layer is called <mark>multiplexing</mark>. 
- UDP socket is fully identified by a two-tuple consisting of a <mark>destination IP address</mark> and a <mark>destination port number</mark>. 
- TCP socket is identified by a four-tuple: (source IP address, source port number,destination IP address,destination port number).

> ## 3.1 UDP


- Note that with UDP there is <mark>no handshaking</mark> between sending and receiving transport-layer entities before sending a segment.

- UDP's advantages over TCP:  
  1. Finer application-level control over what data is sent, and when.
  2. No connection establishment.
  3. No connection state. 
  4. Small packet header overhead. 

- UDP Segment Structure
  1. port numbers allow the destination host to pass the application data to the <mark>correct process</mark> running on the destination end system (that is, to perform the <mark>demultiplexing</mark> function). 
  2. The length field specifies the number of bytes in the UDP segment (header plus data).  
  3. The checksum is used by the receiving host to check whether errors have been introduced into the segment. 



- How checksum works
  1. At the sender side,assign the 1s complement(The 1s complement is obtained by
converting all the 0s to 1s and converting all the 1s to 0s) of the sum of all the 16-bit words in the segment to the checksum field.
  2. At the receiver, all four 16-bit words are added, including the checksum. 
  3. If no errors are introduced into the packet, then clearly the sum at the receiver will be 1111111111111111. If one of the bits is a 0, then we know that errors have been introduced into the pack.


- Although UDP provides error checking, <mark>it does not do anything to recover from an error</mark>.


> ## 3.2 Reliable Data Transfer

- With a reliable data transfer, no transferred data bits are corrupted (flipped from 0 to 1, or vice versa) or lost, and all are delivered in the order in which they were sent.


- RDT 1.0
  - FSM
  ![rdt1](/images/computer_networking_topdown/rdt1.png)

- RDT 2.0

  - Control messages allow the receiver to let the sender know what has been received correctly by sending <mark>ACK</mark>, and what has been received in error by <mark>NAK</mark> and thus requires repeating. In a computer network setting, reliable data transfer protocols based on such retransmission are known as <mark>ARQ (Automatic Repeat reQuest) protocols</mark>.
  
  - FSM
  ![rdt2](/images/computer_networking_topdown/rdt2.png)

  - Flaw:the ACK or NAK packet could be corrupted! 

- RDT 2.1
  
  - Fix Measure: The sender simply to <mark>resend</mark> the current data packet when it receives a garbled ACK or NAK packet. And add a new field to the data packet and have the sender number its data packets by putting a sequence number into this field to check whether or not the received packet is a retransmission.

  - FSM
  ![sender  ](/images/computer_networking_topdown/rdt2_1_sender.png)
  ![receiver](/images/computer_networking_topdown/rdt2_1_receiver.png)


- RDT 2.2
  
  - We can accomplish the same effect as a NAK if, instead of sending a NAK, we send an ACK for the last correctly received packet.
  
  - FSM
  ![sender](/images/computer_networking_topdown/rdt2_2_sender.png)
  ![receiver](/images/computer_networking_topdown/rdt2_2_receiver.png)


- RDT 3.0
  
  - Suppose now that in addition to corrupting bits, the underlying channel can lose packets as well.Two additional concerns must now be addressed by the protocol: how to detect packet loss and what to do when packet loss occurs.
  - Implementing a <mark>time-based</mark> retransmission mechanism requires a countdown timer that can <mark>interrupt</mark> the sender after a given amount of time has expired.
  - FSM
  ![sender](/images/computer_networking_topdown/rdt3_sender.png)
  ![receiver](/images/computer_networking_topdown/rdt3_receiver.png)


> ### 3.2.1 Pipelined Reliable Data Transfer

- Pipelined Reliable Data Transfer:Rather than operate in a stop-and-wait manner, the sender is allowed to send multiple packets without waiting for acknowledgments.
  ![pipeline](/images/computer_networking_topdown/pipelined_transfer.png)

- Pipelining has the following consequences:
  
  1. The range of sequence numbers must be increased.
  2. The sender and receiver sides of the protocols may have to buffer more than one packet.
  3. The range of sequence numbers needed and the buffering requirements will depend on the manner in which a data transfer protocol responds to lost, corrupted, and overly delayed packets. 
    

> #### 3.2.1.1 GBN

- Go-Back-N (GBN): the sender is allowed to transmit multiple packets (when available) without waiting for an acknowledgment, but is constrained to have no more than some maximum allowable number, N, of unacknowledged packets in the pipeline.
![GBN](/images/computer_networking_topdown/GBN.png)

1. Sequence numbers in the interval [0, base-1] correspond to packets that have already been <mark>transmitted and acknowledged</mark>.
2. The interval  [base, nextseqnum-1] corresponds to packets that have been <mark>sent but not yet acknowledged</mark>.
3. Sequence numbers in the interval  [nextseqnum , base+N-1] can be used for packets that <mark>can be sent immediately</mark>, should data arrive from the upper layer.
4.  Finally, sequence numbers greater than or equal to  base+N <mark>cannot be used</mark> until the packet with sequence number base has been acknowledged.

-  the range of permissible sequence numbers for transmitted but not yet acknowledged packets can be viewed as a window of size N over the range of sequence numbers.

![GBN_FSM](/images/computer_networking_topdown/GBN_FSM.png)


> #### 3.2.1.2 Selective Repeat

- As the name suggests, selective-repeat protocols avoid unnecessary retransmissions by having the sender <mark>retransmit only those packets that it suspects were received in error</mark> (that is, were lost or corrupted) at the receiver.



- The SR receiver will acknowledge a correctly received packet whether or not it is in order. Out-of-order packets are <mark>buffered</mark> until all packets with lower sequence numbers are received, at which point a batch of packets can be delivered in order to the upper layer.
  - How Selective Repeat Works 
    - Sender
      1. Data received from above.When data is received from above, the SR sender checks the next available sequence number for the packet. If the sequence number is within the sender's window, the data is packetized and sent; other-wise it is either buffered or returned to the upper layer for later transmission,as in GBN.
      2. Timeout.Timers are again used to protect against lost packets. However, each packet must now have <mark>its own logical timer</mark>, since only a single packet will be transmitted on timeout.
      3. ACK received.If an ACK is received, the SR sender marks that packet as having been <mark>received</mark>, provided it is in the window. If the packet's sequencenumber is <mark>equal to send_base</mark>, the window base is moved forward to the <mark>unacknowledged packet with the smallest sequence number</mark>. If the window moves and there are <mark>untransmitted packets</mark> with sequence numbers that now fall within the window, these packets are transmitted.
    - Receiver
      1. Packet with sequence number in [rcv_base, rcvbase+N-1 ] is correctly received.In this case, the received packet falls within the receiver's window and a selective <mark>ACK</mark> packet is returned to the sender. If there are previous packets not received, the packet in the middle is buffered. If this packet has a sequence number <mark>equal to the base of the receive window</mark> , then this packet,and any previously buffered and consecutively numbered packets are delivered to the upper layer. The receive window is then moved forward by the number of packets delivered to the upper layer. 
      2. Packet with sequence number in [rcv_base-N, rcv_base-1] is correctly received.In this case, <mark>an ACK must be generated</mark>, even though this is apacket that the receiver has previously acknowledged
      3. Otherwise. Ignore the packet.



- window size must be less than or equal to <mark>half the size of the sequence number space</mark> for SR protocols.


> ## 3.3 TCP

- TCP is said to be <mark>connection-oriented</mark> because before one application process can begin to send data to another, the two processes must first <mark>“handshake”</mark> with each other—that is, they must send some preliminary segments to each other to establish the parameters of the ensuing data transfer.
- The TCP “connection” is not an end-to-end TDM or FDM circuit as in a circuit-switched network. Instead,the “connection” is a <mark>logical</mark> one, with <mark>common state</mark> residing only in the TCPs in the two communicating <mark>end systems</mark>.
- A TCP connection provides a <mark>full-duplex service</mark>: If there is a TCP connection between Process A on one host and Process B on another host, then application-layer data can flow from Process A to Process B at the same time as application-layer data flows from Process B to Process A.
- A TCP connection is also always <mark>point-to-point</mark>, that is, between a single sender and a single receiver. So-called “multicasting”—the transfer of data from one sender to many receivers in a single send operation—is not possible with TCP.
- The maximum amount of data that can be grabbed and placed in a segment is limited by the <mark>maximum segment size (MSS)</mark>.
- The MSS is typically set by first determining <mark>the length of the largest link-layer frame</mark> that can be sent by the local sending host (the so-called maximum transmission unit, MTU), and then setting the MSS to ensure that a <mark>TCP segment</mark>(when encapsulated in an IP datagram) plus <mark>the TCP/IP header length</mark> (typically 40 bytes) will fit into a single link-layer frame. 
- Note that the MSS is the maximum amount of
<mark>application-layer data</mark> in the segment, not the maximum size of the TCP segment including headers.
- a TCP connection consists of <mark>buffers, variables, and a socket connection to a process</mark> in two hosts of a connection pair.
- The TCP segment consists of <mark>header fields</mark> and a <mark>data field</mark>.
- When TCP sends a large file, such as an image as part of a Web page, it typically <mark>breaks the file into chunks of size MSS</mark> (except for the last chunk, which will often be less than the MSS).
  
- The Structure Of The TCP Segment
  
  ![tcp_struct](/images/computer_networking_topdown/TCP_seg_struct.png)
  1. the header includes source and destination port numbers.
  2. the header includes a checksum field
  3. The 32-bit sequence number field and the 32-bit acknowledgment number field are used by the TCP sender and receiver in implementing a reliable data transfer service.
  4. The 16-bit receive window field is used for flow control. 
  5. The 4-bit header length field specifies the length of the TCP header in 32-bit words. 
  6. The optional and variable-length options field is used when a sender and receiver negotiate the maximum segment size (MSS) or as a window scaling factor for use in high-speed networks. A time-stamping option is also defined.
  7. The flag field contains 6 bits:
    1. The ACK bit is used to indicate that the value carried in the acknowledgment field is valid.
    2. The RST,SYN, and FIN bits are used for connection setup and teardown.
    3. The CWR and ECE bits are used in explicit congestion notification.
    4. Setting the PSH bit indicates that the receiver should pass the data to the upper layer immediately.
    5.  the URG bit is used to indicate that there is data in this segment that the sending-side upper-layer entity has marked as “urgent.”The location of the last byte of this urgent data is indicated by the 16-bit urgent data pointer field

- The sequence number for a segment is the <mark>byte-stream number of the first byte in the segment</mark>.
- The acknowledgment number that a host  puts in its segment is <mark>the sequence number of the next byte</mark> the host  is expecting from its peer host.
- TCP only acknowledges bytes up to the first missing byte in the stream, TCP is said to provide <mark>cumulative acknowledgments</mark>.
-  when a host receives out-of-order
segments in a TCP connection,it keeps the out-of-order bytes and waits for the missing bytes to fill in the gaps.
- In practice, both sides of a TCP connection randomly choose an initial sequence number.This is done to minimize the possibility that a segment that is still present in the network from an <mark>earlier, already-terminated connection</mark> between two hosts is mistaken for a valid segment in a later connection between these same two hosts (which also happen to be using the same port numbers as the old connection)

- Telnet : A Case Study for Sequence and Acknowledgment Numbers

![telnet_case](/images/computer_networking_topdown/telnet_example.png)

- most TCP implementations take only one  Sample RTT measurement at a time.That is, at any point in time, the  SampleRTT is being estimated for only one of the transmitted but currently unacknowledged segments, leading to a new value of  SampleRTT approximately once every RTT.
- TCP updates  EstimatedRTT according to the following formula:EstimatedRTT=(1−α)⋅EstimatedRTT+α⋅SampleRTT
-  DevRTT, as an estimate of how much  SampleRTT
typically deviates from  Estimated RTT:DevRTT=(1−β)⋅DevRTT+β⋅|SampleRTT−EstimatedRTT|
- How to compute timeout interval:
  1. An initial  TimeoutInterval value of 1 second is recommended [RFC 6298]. 
  2. When a timeout occurs, the value of  TimeoutInterval is <mark>doubled</mark>. 
  3. As soon as a segment is received and EstimatedRTT is updated, the  TimeoutInterval is computed using the formula:TimeoutInterval=EstimatedRTT+4⋅DevRTT

- the recommended TCP timer management procedures [RFC 6298] use only a <mark>single</mark> retransmission timer, even if there are multiple transmitted but not yet acknowledged segments


> ### 3.3.1 TCP Reliable Data Transfer


- Highly Simplified Description


```javascript
// Assume sender is not constrained by TCP flow or congestion control,that data from above is less than MSS in size, and that data transfer is in one direction only. 
NextseqNum=InitialseqNumber
sendBase=InitialseqNumber
loop (forever) {
  switch(event)
    event: data received from application above
      create TCP segment with sequence number NextSegNum
      if ( timer currently not running)
        start timer
      pass segment to IP
      NextseqNum=NextseqNum+length (data)
      break;
    event: timer timeout
      retransmit not-yet-acknowledged segment with smallest sequence number
      start timer
      timer*=2
      break;
    event: ACK received, with ACK field value of y
            if (y > SendBase) {
              SendBase=y
              if (there are currently any not yet acknowledged segments)
                 start timer
            }
            else {/* a duplicate ACK for already ACKed segment */
               increment number of duplicate ACKs received for y
               if (number of duplicate ACKS received for y==3)
                   /* TCP fast retransmit */
                   resend segment with sequence number y
            }
           break;

```


- TCP ACK Generation Recommendation 


|Event| TCP Receiver Action|
|-----|--------------------|
|Arrival of in-order segment with expected sequence number. All data up to expected sequence number already acknowledged.| Delayed ACK. <mark>Wait</mark> up to 500 msec for arrival of another in-order segment. If next in-order segment does not arrive in this interval, send an ACK.|
|Arrival of in-order segment with expected sequence number. One other in-order segment waiting for ACK transmission.| One Immediately send single cumulative ACK,ACKing both in-order segments.|
|Arrival of out-of-order segment with higher- than-expected sequence number. Gap detected.|Immediately send duplicate ACK, indicating sequence number of next expected byte (which is the lower end of the gap).|
|Arrival of segment that partially or completely fills in gap in received data.| Immediately send ACK as long as the segment starts at the lower end of gap.|

- Fast Retransmit:If the TCP sender receives <mark>three duplicate ACKs</mark> for the same data, it takes this as an indication that the segment following the segment that has been ACKed three times has been <mark>lost</mark>.the TCP sender performs a fast retransmit , retransmitting the missing segment before that segment’s timer expires.
  

- TCP’s error-recovery mechanism is probably best categorized as a <mark>hybrid of GBN and SR protocols</mark>.

> ### 3.3.2 TCP Flow Control



- If the application is relatively slow at reading the data, the sender can very easily <mark>overflow</mark> the connection’s receive buffer by sending too much data too quickly.
- TCP provides a flow-control service to its applications to eliminate the possibility of the sender overflowing the receiver’s buffer. 
- How TCP Flow Control Works:
  1. Suppose that Host A is sending a large file to Host B over a TCP connection. Host B allocates a receive buffer to this connection; denote its size by  <mark>$RcvBuffer$</mark>. From time to time, the application process in Host B reads from the buffer. Define the following variables:
    - <mark>$LastByteRead$</mark>: the number of the last byte in the data stream <mark>read</mark> from the buffer by the application process in B
    - <mark>$LastByteRcvd$</mark>: the number of the last byte in the data stream that has <mark>arrived</mark> from the network and has been placed in the receive buffer at B
  2. Because TCP is not permitted to overflow the allocated buffer, we must have:
      $$ LastByteRcvd−LastByteRead≤RcvBuffer $$
  
  3. The receive window, denoted  <mark>$rwnd$</mark> is set to the <mark>amount of spare room</mark> in the buffer:
      $$ rwnd=RcvBuffer−[LastByteRcvd−LastByteRead] $$

  4. Host B tells Host A how much spare room it has in the connection buffer by placing its current value of  $rwnd$ in the receive window field of every segment it sends to A. 
  5. Host A in turn keeps track of two variables,  $LastByteSent$ and  $LastByteAcked$,$LastByteSent - LastByteAcked$, is the <mark>amount of unacknowledged data that A has sent into the connection</mark>
  6. Host A makes sure throughout the connection’s life that:
  $$LastByteSent−LastByteAcked≤rwnd$$

- The TCP specification requires Host A to continue to send segments with one data byte when <mark>B’s receive window is zero</mark>. These segments will be acknowledged by the receiver. Eventually the buffer will begin to empty and the acknowledgments will contain <mark>a nonzero  $rwnd$ value</mark>.

> ### 3.3.3 TCP Three-Way Handshake

- How The Three-way Handshaking Works:
  ![Three_Way_Handshake](/images/computer_networking_topdown/THREE_WAY_HANDSHAKE.png)
  1. The client-side TCP first sends a special TCP segment to the server-side TCP. This special segment contains <mark>no application-layer data</mark>. But one of the flag bits in the segment’s header , <mark>the SYN bit</mark>, is set to 1.  For this reason, this special segment is referred to as a <mark>SYN segment</mark>. In addition, the client <mark>randomly</mark> chooses an <mark>initial sequence number ($client_isn$)</mark> and puts this number in the <mark>sequence number field</mark> of the initial TCP SYN segment. This segment is encapsulated within an IP datagram and sent to the server.
  2. Once the IP datagram containing the TCP SYN segment arrives at the server host (assuming it does arrive!), the server extracts the TCP SYN segment from the datagram, <mark>allocates the TCP buffers and variables</mark> to the connection, and sends a <mark>connection-granted segment</mark> to the client TCP.The connection-granted segment is referred to as a <mark>SYNACK</mark> segment.This connection-granted segment also contains <mark>no application-layer data</mark>. However, it does contain three important pieces of information in the segment header:
       - the SYN bit is set to 1.
       - the acknowledgment field of the TCP segment header is set to <mark>$client_isn+1$</mark>
       - the server chooses its own <mark>initial sequence number (server_isn)</mark> and puts this value in the <mark>sequence number field</mark> of the TCP segment header
  3. Upon receiving the SYNACK segment, the client also <mark>allocates buffers and variables</mark> to the connection. The client host then sends the server yet another segment; this last segment acknowledges the server’s connection-granted segment (the client does so by putting the value <mark>server_isn+1 in the acknowledgment field</mark> of the TCP segment header). The <mark>SYN bit is set to zero</mark>, since the connection is established. This third stage of the three-way handshake may carry <mark>client-to-server data</mark> in the segment payload.


> ### 3.3.4 TCP Closing



![TCP_closing](/images/computer_networking_topdown/tcp_close.png)

  1. The client application process issues a <mark>close command</mark>. This causes the client TCP to send a special TCP segment to the server process. This special segment has a flag bit in the segment’s header, <mark>the FIN bit </mark>, set to 1.
  2. When the server receives this segment, it sends the client an acknowledgment segment in return. The server then sends its own shutdown segment, which has <mark>the FIN bit</mark> set to 1.
  3. Finally, the client acknowledges the server’s shutdown segment. At this point, all the resources in the two hosts are now deallocated.


- TCP States

![client_side](/images/computer_networking_topdown/client_states.png)

![server_side](/images/computer_networking_topdown/server_states.png)

- RST Segment:suppose a host receives a TCP SYN packet with destination port  which it is not accepting connections on . Then the host will send a special reset segment to the source. This TCP segment has the <mark>RST flag bit</mark> set to 1.

> ### 3.3.5 TCP Congestion Control

- Costs of Congestion:
  1. <mark>large queuing delays</mark> are experienced as the packet-arrival rate nears the link capacity.
  2. the sender must perform <mark>retransmissions</mark> in order to compensate for dropped (lost) packets due to buffer overflow.
  3.  a router to use its link bandwidth to forward unneeded copies of a packet.
  4.  when a packet is dropped along a path, the transmission capacity that was used at each of the upstream links to forward that packet to the point at which it is dropped ends up having been wasted.

- Approaches to Congestion Control:
  1. End-to-end congestion control
  2. Network-assisted congestion control

![nacg](/images/computer_networking_topdown/networkassist.png)

- The TCP congestion-control mechanism
operating at the sender keeps track of an additional variable, the congestion window,denoted  <mark>$cwnd$</mark>.
-  At the beginning of every RTT, the constraint permits the sender to send  <mark>$cwnd$</mark> bytes of data into the connection; at the end of the RTT the sender receives acknowledgments for the data. Thus the sender’s <mark>send rate</mark> is roughly <mark>$cwnd/RTT \ bytes/sec$</mark>.

- How TCP Sender Determines Sending Rate
  1. A lost segment implies congestion, and hence, the TCP sender’s rate should be decreased when a segment is lost.
  2. An acknowledged segment indicates that the network is delivering the sender’s segments to the receiver, and hence, the sender’s rate can be increased when an ACK arrives for a previously unacknowledged segment.

- TCP congestion-control algorithm consists of 3 components:

![TCP_CG_FSM](/images/computer_networking_topdown/TCP_congestion_control.png)

  1. Slow Start
  2. Congestion avoidance
  3. fast recovery

- Slow Start

![slow_start](/images/computer_networking_topdown/slow_start.png)

  1.  The value of  cwnd begins at 1 MSS and increases by 1 MSS every time a transmitted segment is first acknowledged.This process results in a doubling of the sending rate every RTT.
  2.  If there is a loss event (i.e., congestion) indicated by a timeout, the TCP sender sets the value of cwnd to 1 and begins the slow start process anew. It also sets the value of  <mark>ssthresh</mark> (shorthand for “slow start threshold”) to  cwnd/2—half of the value of the congestion window value when congestion was detected. 
  3.  Thus, when the value of  cwnd equals  ssthresh, slow start ends and TCP transitions into <mark>congestion avoidance mode</mark>.
  4.   if three duplicate ACKs are detected, in which case TCP performs a <mark>fast retransmit</mark> and enters the <mark>fast recovery state</mark>

- Congestion Avoidance
  1. TCP adopts a more conservative approach and increases the value of  cwnd by just a single MSS every RTT.
  2. When a timeout occurs. The value of  cwnd is set to 1 MSS, and the value of  ssthresh is updated to half the value of  cwnd when the loss event occurred.TCP transitions to Slow Start mode.
  3. Triple duplicate ACK:TCP <mark>halves the value of  cwnd</mark>  and records the value of  <mark>ssthresh</mark> to be half the value of  cwnd (adding in 3 MSS for good measure to account for the triple duplicate ACKs received). The <mark>fast-recovery</mark> state is then entered.

- Fast Recovery
  1. The value of  cwnd is increased by 1 MSS for every <mark>duplicate ACK</mark> received for the missing segment that caused TCP to enter the fast-recovery state.
  2. when an <mark>ACK arrives for the missing segment</mark>, TCP enters the congestion-avoidance state after deflating  $cwnd$.
  3. If a <mark>timeout</mark> event occurs, fast recovery transitions to the <mark>slow-start state</mark> after performing the same actions as in slow start and congestion avoidance.
 
- How TCP Congestion Control Provides Fairness
  
![fairness](/images/computer_networking_topdown/fairness.png)

- Explicit Congestion Notification (ECN): Network-assisted Congestion Control:At the network layer, two bits (with four possible values, overall) in the <mark>Type of Service</mark> field of the IP datagram header are used for ECN:
  1. One setting of the ECN bits-<mark>ECE</mark> (Explicit Congestion Notification Echo) bit is used by a router to indicate that it (the router) is <mark>experiencing congestion</mark>. This congestion indication is then carried in the marked IP datagram to the destination host, which then informs the sending host.
  2. A second setting of the ECN bits is used by the sending host to inform routers that the sender and receiver are <mark>ECN-capable</mark>


> # Chapter 4 Network Layer








- <mark>Forwarding</mark> refers to the <mark>router-local</mark> action of transferring a packet from an input link interface to the appropriate output link interface. Forwarding takes place at very short timescales (typically a few nanoseconds), and thus is typically implemented in <mark>hardware</mark>.
-  <mark>Routing</mark> refers to the <mark>network-wide</mark> process that determines the end-to-end paths that packets take from source to destination. Routing takes place on much longer timescales (typically seconds), and as we will see is often implemented in <mark>software</mark>.
-  A router forwards a packet by examining the value of one or more fields in the arriving packet’s header, and then using these header values to index into its <mark>forwarding table</mark>. The value stored in the forwarding table entry for those values indicates the outgoing link interface at that router to which that packet is to be forwarded.

![forwarding_tab](/images/computer_networking_topdown/forwarding_tab.png)

![forwarding_tab_sdn](/images/computer_networking_topdown/forwarding_tab_sdn.png)

- Best-effort Service:With best-effort service, packets are neither guaranteed to be received in the order in which they were sent, nor is their eventual delivery even guaranteed. There is no guarantee on the end-to-end delay nor is there a minimal bandwidth guarantee. 


> ## 4.1 Router Architecture

![router_arch](/images/computer_networking_topdown/router_architecture.png)

  - Input ports. An input port performs several key functions:
    1. It performs the physical layer function of <mark>terminating an incoming physical link</mark> at a router; this is shown in the leftmost box of an input port and the rightmost box of an output port . 
    2. An input port also performs link-layer functions needed to <mark>interoperate with the link layer at the other side of the incoming link</mark>; this is represented by the middle boxes in the input and output ports. 
    3. Perhaps most crucially, a <mark>lookup function</mark> is also performed at the input port; this will occur in the rightmost box of the input port. It is here that the <mark>forwarding table</mark> is consulted. 
  - Switching fabric: The switching fabric connects the router’s input ports to its output ports.
  - Output ports: An output port stores packets received from the switching fabric and transmits these packets on the outgoing link by performing the necessary link-layer and physical-layer functions.When a link is bidirectional (that is, carries traffic in both directions), an output port will typically be paired with the input port for that link on the same line card.
  - Routing processor. The routing processor performs control-plane functions. In traditional routers, it executes the routing protocols, maintains routing tables and attached link state information, and <mark>computes the forwarding table</mark> for the router. In SDN routers, the routing processor is responsible for <mark>communicating with the remote controller</mark> in order to (among other activities) receive forwarding table entries computed by the remote controller, and install these entries in the router’s input ports. The routing processor also performs the network management functions.
- A router’s input ports, output ports, and switching fabric are almost always implemented in <mark>hardware</mark>
- While the data plane operates at the nanosecond time scale, a router’s control functions。operate at the millisecond or second timescale.
- the router uses the <mark>longest prefix matching rule</mark>; that is, it finds the longest matching entry in the table and forwards the packet to the link interface associated with the longest prefix match.

- Switching Methods:
  1. Switching via memory:The simplest, earliest routers were traditional computers, with switching between input and output ports being done under direct control of the CPU (routing processor).
  ![mem_switch](/images/computer_networking_topdown/mem_switch.png)
  2. Switching via a bus:The <mark>input port</mark> pre-pend a <mark>switch-internal label</mark> (header) to the packet indicating the local output port to which this packet is being transferred and transmitting the packet onto the bus. All output ports receive the packet, but only <mark>the port that matches the label</mark> will keep the packet.
  ![single_bus_switch](/images/computer_networking_topdown/single_bus_switch.png)

  3. One way to overcome the bandwidth limitation of a single, shared bus is to use a more sophisticated <mark>interconnection network</mark>.A crossbar switch is an interconnection network consisting of 2N buses that connect N input ports to N output ports. Each vertical bus intersects each horizontal bus at a crosspoint, which can be opened or closed at any time by the switch fabric controller (whose logic is part of the switching fabric itself). 


- Packet Scheduling
  1. First-in-First-Out (FIFO)
    ![fifo](/images/computer_networking_topdown/fifo.png)
  2. Priority Queuing: packets arriving at the output link are classified into priority classes upon arrival at the queue.When choosing a packet to transmit, the priority queuing discipline will transmit a packet from the <mark>highest priority class</mark> that has a nonempty queue (that is, has packets waiting for transmission). The choice among packets in the same priority class is typically done in a <mark>FIFO</mark> manner.Under a <mark>non-preemptive</mark> priority queuing discipline, the transmission of a packet is not interrupted once it has begun.
    ![pq](/images/computer_networking_topdown/priority_queue.png)
  3. Round Robin:Under the round robin queuing discipline, packets are sorted into classes as with priority queuing. However, rather than there being a strict service priority among classes, a round robin scheduler <mark>alternates service among the classes</mark>.
    ![rr](/images/computer_networking_topdown/round_robin.png)
  4. A generalized form of round robin queuing that has been widely implemented in routers is the so-called <mark>weighted fair queuing (WFQ)</mark> discipline.during any interval of time during which there are class i packets to send, class i will then be guaranteed to receive a fraction of service equal to $w_i/(∑w_j)$  where the sum in the denominator is taken over <mark>all classes</mark> that also have packets queued for transmission.
    ![wfq](/images/computer_networking_topdown/weighted_fair_queueing.png)


> ## 4.2 The Internet Protocol (IP)


> ### 4.2.1 IPv4

> #### 4.2.1.1 IPv4 Datagram Structure


![ipv4_datagram](/images/computer_networking_topdown/ipv4_datagram.png)

  1. Version number
  2. Header length:these 4 bits are needed to determine <mark>where in the IP datagram the payload actually begins</mark>
  3. Type of service: The type of service (TOS) bits were included in the IPv4 header to allow different types of IP datagrams to be distinguished from each other
  4. Datagram length. This is the <mark>total length</mark> of the IP datagram (header plus data), measured in bytes.
  5. Identifier, flags, fragmentation offset
  6. Time-to-live:This field is <mark>decremented by one</mark> each time the datagram is processed by a router. If the TTL field reaches 0, a router must drop that datagram.
  7. Protocol:The value of this field indicates the specific <mark>transport-layer protocol</mark> to which the data portion of this IP datagram should be passed.
  8. Header Checksum:The header checksum is computed by treating each 2 bytes in the header as a number and summing these numbers using 1s complement arithmetic.
  9. Source and destination IP addresses
  10. Options
  11. Data (payload):In most circumstances, the data field of the IP datagram contains the transport-layer segment (TCP or UDP) to be delivered to the destination. However, the data field can carry <mark>other types of data</mark>, such as ICMP messages 
  
{{< admonition type=info title="why does TCP/IP perform error checking at both the transport and network layers?" open=false >}}




 - Only the <mark>IP header</mark> is checksummed at the IP layer, while the TCP/UDP checksum is computed over the <mark>entire TCP/UDP segment</mark>.
 - TCP/UDP and IP do not necessarily both have to belong to the same <mark>protocol stack</mark>. TCP can, in principle, run over a different network-layer protocol and IP can carry data that will not be passed to TCP/UDP.

{{< /admonition >}}


> #### 4.2.1.2 Fragment

- The maximum amount of data that a link-layer frame can carry is called the <mark>maximum transmission unit (MTU)</mark>
- each of the links along the route between sender and destination can use <mark>different link-layer protocols</mark>, and each of these protocols can have <mark>different MTUs</mark>
- When Does Fragment Occur:When outgoing link has an MTU that is <mark>smaller than the length of the IP datagram</mark>,the payload in the IP datagram is <mark>fragmented</mark> into two or more smaller IP datagrams,and encapsulated in a separate link-layer frame
- Fragments Reassembly:When a destination host receives a series of datagrams from the same source,it needs to determine whether any of these datagrams are fragments of some original, larger datagram.If some datagrams are fragments, it must further determine when it has received the <mark>last fragment</mark> and how the fragments it has received should be <mark>pieced back</mark> together to form the original datagram:
  1. When a datagram is created, the sending host stamps the datagram with an <mark>identification number</mark> as well as source and destination addresses.
  2. When a router needs to fragment a datagram, each resulting datagram (that is, fragment) is stamped with the source address, destination address, and identification number of the original datagram.
  3. When the destination receives a series of datagrams from the same sending host, it can examine the <mark>identification numbers</mark> of the datagrams to determine which of the datagrams are actually fragments of the same larger datagram.
  4.  In order for the destination host to be absolutely sure it has received the last fragment of he original datagram, the last fragment has a <mark>flag bit set to 0</mark>, whereas all the other fragments have this flag bit set to 1.
  5.   In order for the destination host to determine whether a fragment is missing (and also to be able to reassemble the fragments in their proper order), the <mark>offset field</mark> is used to specify <mark>where the fragment fits</mark> within the original IP datagram.


> #### 4.2.1.3 Addressing



- The <mark>boundary</mark> between the host or router and the physical link is called an <mark>interface</mark>

- An <mark>IP address</mark> is technically associated with an <mark>interface</mark>, rather than with the host or router containing that interface
- In IP terms, the network interconnecting host interfaces and router interface forms a <mark>subnet</mark>.
- subnet mask:/n indicates that the <mark>leftmost n bits of the 32-bit quantity</mark> define the subnet address.

- Classless Interdomain Routing (CIDR) strategy:The x most significant bits of an address of the form a.b.c.d/x constitute the network portion of the IP address, and are often referred to as the prefix (or network prefix) of the address.only these x leading prefix bits are considered by routers <mark>outside</mark> the organization’s network. That is, when a router outside the organization forwards a datagram whose destination address is inside the organization, only the leading x bits of the address need be considered.The remaining 32-x bits of an address can be thought of as distinguishing among the devices <mark>within</mark> the organization.
- For DHCP protocol to work,each subnet will have a <mark>DHCP server</mark>. If no server is present on the subnet, a <mark>DHCP relay agent</mark> (typically a router) that <mark>knows the address of a DHCP server</mark> for that network is needed. 
- DHCP protocol is a four-step process:

  ![DHCP_process](/images/computer_networking_topdown/DHCP_Process.png)
  1. DHCP server discovery: A newly arriving host  sends within a <mark>UDP packet</mark> to port 67. the DHCP client creates an IP datagram containing its DHCP discover message along with the <mark>broadcast</mark> destination IP address of <mark>255.255.255.255</mark> and a “this host” source IP address of 0.0.0.0. The DHCP client passes the IP datagram to the link layer, which then <mark>broadcasts this frame to all nodes attached to the subnet</mark>
  2. DHCP server offer(s). A DHCP server receiving a DHCP discover message responds to the client with a <mark>DHCP offer message</mark> that is <mark>broadcast</mark> to all nodes on the subnet  ,  again using the IP broadcast address of <mark>255.255.255.255</mark>.Each server offer message contains the <mark>transaction ID</mark> of the received discover message, the <mark>proposed IP address</mark> for the client, the <mark>network mask</mark>, and an IP address <mark>lease time</mark>.
  3. DHCP request. The newly arriving client will <mark>choose</mark> from among one or more server offers and respond to its selected offer with a <mark>DHCP request message</mark>, echoing back the configuration parameters
  4. DHCP ACK. The server responds to the DHCP request message with a <mark>DHCP ACK message</mark>, confirming the requested parameters

-  A realm with private addresses refers to a network whose addresses only have meaning to devices <mark>within that network</mark>.
- The NAT router behaves to the outside world as a single device with a <mark>single IP address</mark>.

![NAT](/images/computer_networking_topdown/NAT.png)

- The router gets its address from the <mark>ISP’s DHCP server</mark>, and the router runs a DHCP server itself to provide addresses to computers within the NAT-DHCP-router- controlled home network’s address space.
- All datagrams arriving at the NAT router from the WAN have the <mark>same destination IP address</mark> , how does the router know the internal host to which it should forward a given datagram?
  1.  Suppose a user sitting in a home network behind host 10.0.0.1 requests a Web page on some Web server (port 80) with IP address 128.119.40.186. The host 10.0.0.1 assigns the (arbitrary) source port number 3345 and sends the datagram into the LAN.
  2.  The NAT router receives the datagram, generates a <mark>new source port number</mark> 5001 for the datagram, <mark>replaces the source IP address with its WAN-side IP address</mark> 138.76.29.7, and <mark>replaces the original source port number 3345 with the new source port number</mark> 5001.NAT in the router also <mark>adds an entry to its NAT translation table</mark>.
  3.  The Web server responds with a datagram whose destination address is the IP address of the NAT router, and whose destination port number is 5001. When this datagram arrives at the NAT router, the router indexes the <mark>NAT translation table</mark> using the destination IP address and destination port number to obtain the appropriate IP address (10.0.0.1) and destination port number (3345) for the browser in the home network. The router then <mark>rewrites the datagram’s destination address and destination port number</mark>, and forwards the datagram into the home network.



> ### 4.2.2 IPv6 

- IPv6 Important Changes:
  1. Expanded addressing capabilities
  2. A streamlined 40-byte header
  3. Flow labeling

- IPv6 datagram format

![ipv6_format](/images/computer_networking_topdown/ipv6_format.png)

  1. Version
  2. Traffic class: The 8-bit traffic class field, like the TOS field in IPv4, can be used to give <mark>priority</mark> to certain datagrams within a flow, or it can be used to give priority to datagrams from certain applications (for example, voice-over-IP) over datagrams from other applications (for example, SMTP e-mail).
  3. Flow label
  4. Payload length
  5. Next header. This field identifies the <mark>protocol</mark> to which the contents (data field) of this datagram will be delivered (for example, to TCP or UDP). The field uses the same values as the protocol field in the IPv4 header.
  6. Hop limit: The contents of this field are <mark>decremented by one by each router that forwards the datagram</mark>. If the hop limit count reaches zero, the datagram is <mark>­discarded</mark>.
  7. Source and destination addresses
  8. Data

-  Fields appearing in the IPv4 datagram are no longer present in the IPv6 datagram:
     1. Fragmentation/reassembly:If an IPv6 datagram received by a router is too large to be forwarded over the outgoing link, the router simply <mark>drops</mark> the datagram and sends a “Packet Too Big” ICMP error message back to the sender. The sender can then <mark>resend</mark> the data, using a smaller IP datagram size.
     2. Header checksum: Because the transport-layer (for example, TCP and UDP) and link-layer (for example, Ethernet) protocols in the Internet layers perform checksumming, the designers of IP probably felt that this functionality was sufficiently redundant in the network layer that it could be removed.
     3.  Options:Instead, the options field is one of the possible next headers pointed to from within the IPv6 header. That is, just as TCP or UDP protocol headers can be the next header within an IP packet, so too can an options field. The removal of the options field results in a fixed-length, 40-byte IP header

- The approach to IPv4-to-IPv6 transition that has been most widely adopted in practice involves tunneling:With tunneling, the IPv6 node on the sending side of the tunnel (in this example, B) takes the entire IPv6 datagram and <mark>puts it in the data (payload) field</mark> of an IPv4 datagram. This IPv4 datagram is then addressed to the IPv6 node on the receiving side of the tunnel.
- Each entry in the match-plus-action forwarding table, known as a flow table in OpenFlow, includes:
  1. A set of header field values to which an incoming packet will be matched.If a packet matches multiple flow table entries, the selected match and corresponding action will be that of the highest priority entry with which the packet matches. 
  ![match_fields](/images/computer_networking_topdown/match_fields.png)
  2. A set of counters that are updated as packets are matched to flow table entries. These counters might include the number of packets that have been matched by that table entry, and the time since the table entry was last updated.
  3. A set of actions to be taken when a packet matches a flow table entry. These actions might be to forward the packet to a given output port, to drop the packet, makes copies of the packet and sent them to multiple output ports, and/or to rewrite selected header fields. 


> # Chapter 5 The Network Layer: Control Plane

- A centralized routing algorithm computes the least-cost path between a source and destination using complete, <mark>global knowledge</mark> about the network.Algorithms with global state information are often referred to as <mark>link-state (LS) algorithms</mark>, since the algorithm must be aware of the cost of each link in the network.

- In a decentralized routing algorithm, the calculation of the least-cost path is carried out in iterative, distributed manner by the routers. <mark>No node has complete information</mark> about the costs of all network links. Instead, each node begins with only the knowledge of the costs of its own directly attached links.The decentralized routing algorithm we’ll study  is called a <mark>distance-vector (DV) algorithm</mark>, because each node maintains a vector of estimates of the costs (distances) to all other nodes in the network

- A second broad way to classify routing algorithms is according to whether they are <mark> or dynamic</mark>. In  routing algorithms, routes change very <mark>slowly over time</mark>. Dynamic routing algorithms change the routing paths as the <mark>network traffic loads or topology change</mark>. A dynamic algorithm can be run either periodically or in direct response to topology or link cost changes.
- A third way to classify routing algorithms is according to whether they are <mark>load-sensitive or load- insensitive</mark>. In a load-sensitive algorithm, link costs vary dynamically to reflect the current level of congestion in the underlying link.load-insensitive does not explicitly reflect its current (or recent past) level of congestion.

-  In a link-state algorithm, the network topology and all link costs are known.In practice this is accomplished by having each node <mark>broadcast</mark> link-state packets to all other nodes in the network, with each link-state packet containing the <mark>identities and costs of its attached links</mark>. The result of the nodes’ broadcast is that all nodes have an <mark>identical and complete view of the network</mark>. Each node can then run the LS algorithm and compute the same set of least-cost paths as every other node

- Popular LS-Algorithm:Dijkstra’s algorithm,Prim’s algorithm

- How does DV algorithm work:
  1. each node x maintains the following routing information:
      1. For each neighbor v, the cost c(x, v) from x to directly attached neighbor, v
      2. Node x’s distance vector, that is,$D_x=[D_x(y):y \ in \ N]$ , containing x’s estimate of its cost to all destinations, y, in N
      3. The distance vectors of each of its neighbors, that is $D_v=[D_v(y):y \ in \ N]$,  for each neighbor v of x
  2.  each node sends a copy of its distance vector to each of its neighbors.
  3.  When a node x receives a new distance vector from any of its neighbors w, it saves w’s distance vector, and then uses the <mark>Bellman-Ford equation</mark> to update its own distance vector as follows:
  $$ D_x(y)=minv{c(x,v)+D_v(y)} \qquad for \ each \ node \ y  \ in \ N $$
  1. If node x’s distance vector has changed as a result of this update step, node x will then send its updated,distance vector to each of its neighbors, which can in turn update their own distance vectors.
  2. When a node running the DV algorithm detects a change in the link cost from itself to a neighbor , it updates its distance vector  and, if there’s a change in the cost of the least-cost path, <mark>informs its neighbors</mark> of its new distance vector.

```javascript
 Initialization:
   for all destinations y in N:
      Dx (y)= c(x, y)/* if y is not a neighbor then c(x, y)= ∞ */
      for each neighbor w
          Dw (y) = ? for all destinations y in N
      for each neighbor w
          send distance vector  Dx  = [Dx (y): y in N] to w

 loop 
    wait  (until I see a link cost change to some neighbor w or
            until I receive a distance vector from some neighbor w)

    for each y in N:
        Dx (y) = min {c(x, v) + Dw (y)}
        update v*y /* the next hop router along the shortest path to y  */

 if Dx(y) changed for any destination y
       send distance vector Dx   = [Dx (y): y in N] to all neighbors

 forever 
```

![dv_eg](/images/computer_networking_topdown/dv_eg.png)


- When Does count-to-infinity Problem Occurs:
![c2i](/images/computer_networking_topdown/c2i.png)

1.  Before the link cost changes,Dy(x)=4, Dy(z)=1, Dz(y)=1, Dz(x)=5.At time t0, y detects the link cost change (the cost has changed from 4 to 60). y computes its new minimum-cost path to x to have a cost of $Dy(x)=min(c(y,x)+Dx(x), c(y,z)+Dz(x))=min(60+0,1+5)=6$ . Of course, with our global view of the network, we can see that this new cost via z is wrong. But the only information node y has is that its direct cost to x is 60 and that z has last told y that z could get to x with a cost of 5. So in order to get to x, y would now route through z, fully expecting that z will be able to get to x with a cost of 5. As of t  we have a routing loop—in order to get to x, y routes through z, and z routes through y. A routing loop is like a black hole—a packet destined for x arriving at y or z as of t  will bounce back and forth between these two nodes forever (or until the forwarding tables are changed).
2.  Since node y has computed a new minimum cost to x, it informs z of its new distance vector at time
t .
3.  Sometime after t , z receives y’s new distance vector, which indicates that y’s minimum cost to x is 6.z knows it can get to y with a cost of 1 and hence computes a new least cost to x of Since z’s least cost to x has increased, it then informs y of its new distance vector at t .
4. In a similar manner, after receiving z’s new distance vector, y determines  and sends z its distance vector. z then determines  and sends y its distance vector, and so on

- Poisoned Reverse:if z <mark>routes through y</mark> to get to destination x, then z will advertise <mark>to y</mark> that its distance to x is <mark>infinity</mark>, that is, z will advertise to y that $D_z(x)=\inf$

- autonomous ­systems (ASs):Routers within the same AS all run the <mark>same routing algorithm and have information about each other</mark>. The routing algorithm ­running within an autonomous system is called an <mark>intra-autonomous system routing ­protocol</mark>.
- An autonomous system is identified by its globally unique <mark>autonomous system number (ASN)</mark>

- OSPF is a <mark>link-state</mark> protocol that uses flooding of link-state information and a <mark>Dijkstra’s least-cost path algorithm</mark>.
-  With OSPF, each router constructs a <mark>complete topological map (that is, a graph) of the entire autonomous system</mark>. Each router then locally runs Dijkstra’s shortest-path algorithm to determine a shortest-path tree to all subnets, with itself as the root node. Individual link costs are configured by the network administrator.
-  With OSPF, a router <mark>broadcasts</mark> routing information to all other routers in the autonomous system, <mark>not just to its neighboring routers</mark>. A router broadcasts link-state information whenever there is a <mark>change in a link’s state</mark> (for example, a change in cost or a change in up/down status). It also broadcasts a link’s state periodically (at least once every 30 minutes), <mark>even if the link’s state has not changed</mark>.
-  OSPF advertisements are contained in OSPF messages that are carried directly by IP, with an upper-layer protocol of 89 for OSPF. Thus, the OSPF protocol must itself implement functionality such as <mark>reliable message transfer</mark> and <mark>link-state broadcast</mark>.

- Some of the advances embodied in OSPF include the following:
  1. Security: Exchanges between OSPF routers (for example, link-state updates) can be authenticated. With authentication, only trusted routers can participate in the OSPF protocol within an AS.Two types of authentication can be configured— simple and MD5
  2. Multiple same-cost paths:When multiple paths to a destination have the same cost, OSPF allows multiple paths to be used
  3. Support for hierarchy within a single AS


- In the Internet, all ASs run <mark>the same inter-AS routing protocol</mark>, called the <mark>Border Gateway Protocol</mark>, more commonly known as BGP
- In BGP, packets are not routed to a specific destination address, but instead to <mark>CIDRized prefixes</mark>, with each prefix representing a <mark>subnet or a collection of subnets</mark>.

- Thus, a router’s forwarding table will have entries of the form (x, I), where x is a <mark>prefix</mark> (such as 138.16.68/22) and I is an <mark>interface number</mark> for one of the router’s interfaces.

- As an inter-AS routing protocol, BGP provides each router a means to:
  1.  Obtain prefix reachability information from <mark>neighboring ASs</mark>. In particular, BGP allows each subnet to <mark>advertise its existence to the rest of the Internet</mark>.
  2.  Determine the <mark>“best” routes</mark> to the prefixes. 

- For each AS, each router is either a <mark>gateway router</mark> or an <mark>internal router</mark>. 
  1. A gateway router is a router on the <mark>edge</mark> of an AS that directly connects to one or more routers in <mark>other ASs</mark>.
  2. An internal router connects only to hosts and routers <mark>within its own AS</mark>. 

- In BGP,pairs of routers exchange routing information over semi-permanent <mark>TCP</mark> connections using port 179.Each such TCP connection, along with all the BGP messages sent over the connection, is called a <mark>BGP connection</mark>
- Furthermore, a BGP connection that spans two ASs is called an <mark>external BGP (eBGP) connection</mark>, and a BGP session between routers in the same AS is called an <mark>internal BGP (iBGP)</mark> connection. 
![bgp_conn](/images/computer_networking_topdown/BGP_connections.png)

- In BGP jargon, a <mark>prefix</mark> along with its <mark>attributes</mark> is called a <mark>route</mark>.
- Two of the more important attributes are <mark>AS-PATH</mark> and <mark>NEXT-HOP</mark>. 
  1. The AS-PATH attribute contains the <mark>list of ASs through which the advertisement has passed</mark>.To generate the AS-PATH value, when a prefix is passed to an AS, the AS adds its ASN to the existing list in the AS-PATH.BGP routers also use the AS-PATH attribute to detect and prevent looping advertisements; specifically, if a router sees that <mark>its own AS is contained in the path list</mark>, it will reject the advertisement.
  2. The NEXT-HOP is the IP address of the <mark>router interface</mark> that begins the AS-PATH. 

- Hot Potato Algorithm
  ![hot_potato](/images/computer_networking_topdown/hot_potato.png)

- BGP uses an algorithm that is <mark>more complicated</mark> than hot potato routing, but nevertheless incorporates hot potato routing:
  1.  A route is assigned a <mark>local preference value</mark> as one of its attributes . The local preference of a route could have been set by the router or could have been learned from another router in the same AS. The value of the local preference attribute is a policy decision that is left entirely up to the AS’s network administrator.  The routes with the <mark>highest local preference values</mark> are selected.
  2.  From the remaining routes (all with the same highest local preference value), the route with the <mark>shortest AS-PATH</mark> is selected.
  3.  From the remaining routes (all with the same highest local preference value and the same AS-PATH length), <mark>hot potato routing</mark> is used, that is, the route with the <mark>closest NEXT-HOP router</mark> is selected.
  4.  If more than one route still remains, the router uses <mark>BGP identifiers</mark> to select the route;


- How Does IP-Anycast Work:
  1. the server-provider assigns the <mark>same IP address</mark> to each of its servers, and uses standard BGP to <mark>advertise</mark> this IP address from each of the servers.
  2. When configuring its routing table, each router will locally use the <mark>BGP route-selection algorithm</mark> to pick the “best” (for example, closest, as determined by AS-hop counts) route to that IP address.
  3. When a client requests the content on the server,  it sends request to the <mark>common IP address</mark> used by the geographically dispersed servers, no matter where the client is located.
  4. Internet routers then forward the request packet to the “closest” server, as defined by the BGP route-selection algorithm.

- IP-anycast is extensively used by the DNS system to <mark>direct DNS queries to the closest root DNS server</mark>

- How To Prevent multi-homed access ISP from acting as an intermidiate AS:It advertises  that <mark>it has no paths to any other destinations except itself</mark>

- Four key characteristics of an SDN architecture can be identified:
  1. Flow-based forwarding. Packet forwarding by SDN-controlled switches can be based on any number of <mark>header field values</mark> in the transport-layer, network-layer, or link-layer header.
  2. <mark>Separation</mark> of data plane and control plane
  3. Network control functions: <mark>external</mark> to data-plane switches
  4. A <mark>programmable</mark> network

-  the SDN control plane divides broadly into two components—<mark>the SDN controller</mark> and <mark>the SDN network-control applications</mark>.
![SDN_arch](/images/computer_networking_topdown/SDN_arch.png)
- A controller’s functionality can be broadly organized into three layers:
  1. A communication layer: communicating between the SDN <mark>controller</mark> and controlled network <mark>devices</mark>. 
  2. A network-wide state-management layer
  3. The interface to the network-control application layer

![SDN_controller](/images/computer_networking_topdown/sdc_controller.png)

- The OpenFlow protocol operates over <mark>TCP</mark>, with a default port number of 6653
- Among the important messages flowing from the controller to the controlled switch are the following:
    - Configuration: This message allows the controller to <mark>query and set a switch’s configuration parameters</mark>.
    - Modify-State. This message is used by a controller to add/delete or <mark>modify entries</mark> in the switch’s flow table, and to set switch port properties.
    - Read-State. This message is used by a controller to collect statistics and counter values from the switch’s flow table and ports.
    - Send-Packet. This message is used by the controller to send a specific packet out of a specified port at the controlled switch. The message itself contains the packet to be sent in its payload.

- Among the messages flowing from the <mark>SDN-controlled switch to the controller</mark> are the following:
    - Flow-Removed: This message informs the controller that a flow table entry has been removed, for example by a timeout or as the result of a received modify-state message.
    - Port-status: This message is used by a switch to inform the controller of a change in port status.
    - Packet-in: A packet arriving at a switch port and not matching any flow table entry is <mark>sent to the controller</mark> for additional processing. Matched packets may also be sent to the controller, as an action to be taken on a match. The packet-in message is used to send such packets to the controller.

- The SDN has two important differences from the earlier per-router-control scenario , where Dijkstra’s algorithm was implemented in each and every router .Dijkstra’s algorithm is executed as <mark>a separate application</mark>, outside of the packet switches. Packet switches send link updates to <mark>the SDN controller</mark> and not to each other.

![sdn_state_change](/images/computer_networking_topdown/sdn_shortest_path.png)


- The Internet Control Message Protocol (ICMP), specified in [RFC 792], is used by hosts and routers to communicate network-layer information to each other.

- ICMP messages are carried as IP payload.

- ICMP messages have a <mark>type</mark> and a <mark>code</mark> field, and contain the header and the first 8 bytes of the IP datagram that caused the ICMP message to be generated in the first place (so that the sender can determine the datagram that caused the error)

![ICMP_types](/images/computer_networking_topdown/ICMP_types.png)

- How Does Ping Program Work:
  1. The well-known ping program sends an ICMP type 8 code 0 message to the specified host. 
  2. The destination host, seeing the echo request, sends back a type 0 code 0 ICMP echo reply.

- Most TCP/IP implementations support the ping server directly in the operating system; that is, the server is not a process.

- How Does Traceroute Program Work:
  1. Traceroute in the source sends aseries of ordinary IP datagrams to the destination. Each of these datagrams carries a <mark>UDP</mark> segment with an <mark>unlikely UDP port number</mark>. The first of these datagrams has a TTL of 1, the second of 2, the third of 3, and so on. The source also starts timers for each of the datagrams.
  2. When the nth datagram arrives at the nth router, the nth router observes that the TTL of the datagram has just <mark>expired</mark>. According to the rules of the IP protocol, the router <mark>discards</mark> the datagram and sends an ICMP warning message to the source (type 11 code 0). This warning message includes the name of the router and its IP address.
  3. When this ICMP message arrives back at the source, the source obtains the round-trip time from the timer and the name and IP address of the nth router from the ICMP message
  4. one of the datagrams will eventually make it all the way to the destination host. Because this datagram contains a UDP segment with an unlikely port number, the destination host sends a <mark>port unreachable ICMP message (type 3 code 3)</mark> back to the source.
  5.  When the source host receives this particular ICMP message, it knows it does not need to send additional probe packets. 

- the key components of network management:


![network_man_elems](/images/computer_networking_topdown/Network_Management_Elements.png)


  1. The managing server is an application, controls the collection, processing, analysis, and/or display of network management information.
  2. A managed device is a piece of network equipment (including its software) that resides on a managed network.
  3. Each managed object within a managed device associated information that is collected into a Management Information Base (MIB)
  4. Also resident in each managed device is a network management agent, a process running in the managed device that <mark>communicates with the managing server</mark>
  5. network ­management protocol

- The Simple Network Management Protocol version 2 (SNMPv2) [RFC 3416] is an application-layer protocol used to convey network-management control and information messages between a managing server and an agent executing on behalf of that managing server.

- SNMPv2 defines seven types of messages, known generically as protocol data units—PDUs:


|SNMPv2 PDU Type|Sender-receiver |Description|
|---|---|---|
|GetRequest| manager-to-agent| get value of one or more MIB object instances|
|GetNextRequest| manager-to-agent|get value of next MIB object instance in list or table|
|GetBulkRequest| manager-to-agent|get values in large block of data, for example, values in a large table|
|InformRequest| manager-to-manager|inform remote managing entity of MIB values remote to its access|
|SetRequest| manager-to- agent| set value of one or more MIB object instances|
|Response| agent-to- manager or| generated in response to|
||manager-to-manager|GetRequest|,
 |||GetNextRequest|,
 |||GetBulkRequest|,
 |||SetRequest PDU, or|
 |||InformRequest|
|SNMPv2-Trap| agent-to- manager|inform manager of an exceptional event #|

- the SNMP PDU is preferrably carried in the payload of a UDP datagram

> # Chapter 6 The Link Layer and LANs

- Any device that runs a link-layer protocol is a <mark>node</mark>.
- The communication channels that connect adjacent nodes along the communication path are <mark>links</mark>. 
- Possible services that can be offered by a link-layer protocol include:
  1. Framing. Almost all link-layer protocols encapsulate each network-layer datagram within a link-layer frame before transmission over the link. A frame consists of a <mark>data field</mark>, in which the network-layer datagram is inserted, and a number of <mark>header fields</mark>. The structure of the frame is specified by the link-layer protocol.
  2. Link access. A <mark>medium access control (MAC) protocol</mark> specifies the rules by which a frame is transmitted onto the link. 
  3. Reliable delivery. When a link-layer protocol provides reliable delivery service, it guarantees to move each network-layer datagram across the link without error. Similar to a transport-layer reliable delivery service, a link-layer reliable delivery service can be achieved with <mark>acknowledgments and retransmissions</mark> . A link-layer reliable delivery service is often used for links that are <mark>prone to high error rates</mark>, such as a <mark>wireless link</mark>, with the goal of correcting an error locally—on the link where the error occurs—rather than forcing an end-to-end retransmission of the data by a transport- or application-layer protocol. However, link-layer reliable delivery can be considered an unnecessary overhead for low bit-error links, including fiber, coax, and many twisted-pair copper links. For this reason, many wired link-layer protocols do not provide a reliable delivery service.
  4. Error detection and correction.This is done by having the transmitting node include <mark>error-detection bits</mark> in the frame, and having the receiving node perform an <mark>error check</mark>. Error correction is similar to error detection, except that a receiver not only detects when bit errors have occurred in the frame but also determines exactly <mark>where</mark> in the frame the errors have occurred (and then <mark>corrects</mark> these errors)

- Network Adapter:For the most part, the link layer is implemented in a network adapter, also sometimes known as a <mark>network interface card (NIC)</mark>. At the heart of the network adapter is the <mark>link-layer controller</mark>, usually a single, special-purpose chip that implements many of the link-layer services (framing, link access, error detection, and so on). 

![network_adapter](/images/computer_networking_topdown/network_adapter.png)

- while most of the link layer is implemented in hardware, part of the link layer is implemented in software that runs on the <mark>host’s CPU</mark>. 
    1. On the sending side  : The software components of  the link layer implement higher-level link-layer functionality such as assembling link-layer addressing information and activating the controller hardware. 
    2. On the receiving side, link-layer software responds to controller interrupts (e.g., due to the receipt of one or more frames), handling error conditions and passing a datagram up to the network layer. 


- At the sending node, data, D, to be protected against bit errors is augmented with <mark>error-detection and -correction bits (EDC)</mark>.Both D and EDC are sent to the receiving node in a <mark>link-level frame</mark>. At the receiving node, a sequence of bits, D′ and EDC′ is received.The receiver’s challenge is to determine whether or not D′ is the same as the original D, given that it has only received D′ and EDC′.

- Generally, more sophisticated error-detection and-correction techniques (that is, those that have a smaller probability of allowing undetected bit errors) incur a <mark>larger overhead</mark>—more computation is needed to compute and transmit a larger number of error-detection and -correction bits.
- Parity Checks:Suppose that the information to be sent, D , has d bits. In an <mark>even parity scheme</mark>, the sender simply includes one additional bit and chooses its value such that <mark>the total number of 1s in the  bits (the original information plus a parity bit) is even</mark>. For odd parity schemes, the parity bit value is chosen such that <mark>there is an odd number of 1s</mark>.

![parity_check](/images/computer_networking_topdown/parity_check.png)

- The receiver need only count the number of 1s in the received  bits. If an odd number of 1-valued bits are found with an even parity scheme(or vice versa), the receiver knows that at least one bit error has occurred.

- The ability of the receiver to both <mark>detect and correct</mark> errors is known as <mark>forward error correction (FEC)</mark>

- The Internet checksum:
    1. Bytes of data are treated as <mark>16-bit integers<mark> and summed. The <mark>1s complement</mark> of this sum then forms the Internet checksum that is carried in the segment header.
    2.  the receiver checks the checksum by taking the  the sum of the received data (including the checksum) and checking whether the result is all 1 bits. If <mark>any of the bits are 0</mark>, an error is indicated.

- Cyclic Redundancy Check (CRC) codes operate as follows:
    1. Consider the d-bit piece of data, D, that the sending node wants to send to the receiving node. 
    2. The sender and receiver must first agree on an  bit pattern, known as a <mark>generator</mark>, which we will denote as G.We will require that the leftmost bit of G be a 1.
    3. For a given piece of data, D, the sender will choose <mark>r additional bits, R</mark>, and append them to D such that the resulting  bit pattern  is exactly <mark>divisible by G</mark> (i.e., has no remainder) using modulo-2 arithmetic.The sender calculate R like this:$R=remainder(D/(2^r\times G))$
    4. The receiver divides the d+r  received bits by G. If the remainder is <mark>nonzero</mark>, the receiver knows that an error has occurred; otherwise the data is accepted as being correct



- There are two types of network links: <mark>point-to-point links</mark> and <mark>broadcast links</mark>. 
    1. A point-to-point link consists of a <mark>single sender</mark> at one end of the link and a <mark>single receiver</mark> at the other end of the link.
    2. A broadcast link, can have <mark>multiple sending and receiving nodes</mark> all connected to the <mark>same, single, shared broadcast channel</mark>.

- The multiple access problem:Because all nodes are capable of transmitting frames, more than two nodes can transmit frames at the same time. When this happens, all of the nodes receive multiple frames at the same time; that is, the transmitted frames <mark>collide</mark> at all of the receivers,which are useless.
- In order to ensure that the broadcast channel performs useful work when multiple nodes are active, it is necessary to somehow <mark>coordinate the transmissions of the active nodes</mark>. This coordination job is the responsibility of the <mark>multiple access protocol</mark>.

- Channel Partitioning Protocols:
    1. TDM divides time into time frames and further divides each time frame into N time slots. Each time slot is then assigned to one of the N nodes. Whenever a node has a packet to send, it transmits the packet’s bits during its assigned time slot in the revolving TDM frame. Typically, slot sizes are chosen so that a single packet can be transmitted during a slot time.
    2. FDM divides the R bps channel into different frequencies (each with a bandwidth of R/N) and assigns each frequency to one of the N nodes. FDM thus creates N smaller channels of R/N bps out of the single, larger R bps channel
    3. CDMA assigns a different code to each node. Each node then uses its unique code to encode the data bits it sends.receivers correctly receive a sender’s encoded data bits (assuming thereceiver knows the sender’s code)

- Random Access Protocols:In a random access protocol, a transmitting node always transmits at the <mark>full rate</mark> of the channel, namely, R bps. When there is a collision, each node involved in the collision <mark>repeatedly retransmits</mark> its frame (that is, packet) until its frame gets through without a collision. But when a node experiences a collision, it doesn’t necessarily retransmit the frame right away. Instead it waits a <mark>random delay</mark> before retransmitting the frame.
- one of the simplest random access protocols, the slotted ALOHA protocol. In our description of slotted ALOHA, we assume the following:
    1. All frames consist of exactly L bits.
    2. Time is divided into slots of size L/R seconds (that is, a slot equals the time to transmit one frame).
    3. Nodes start to transmit frames only at the beginnings of slots.
    4. The nodes are synchronized so that each node knows when the slots begin.
    5. If two or more frames collide in a slot, then all the nodes detect the collision event before the slot ends.

- Slotted ALOHA:
    1. When the node has a fresh frame to send, it waits until <mark>the beginning of the next slot</mark> and transmits the entire frame in the slot.
    2. 
        - If there isn’t a collision, the node has successfully transmitted its frame and thus need not consider retransmitting the frame. (The node can prepare a new frame for transmission, if it has one.)
        - If there is a collision, the node detects the collision before the end of the slot. The node retransmits its frame in each subsequent slot with <mark>probability p</mark> until the frame is transmitted without a collision.

- Concerns With Slotted ALOHA:
    1. a certain fraction of the slots will have collisions and will therefore be “wasted.”
    2. another fraction of the slots will be empty because all active nodes <mark>refrain from transmitting</mark> as a result of the probabilistic transmission policy.

- ALOHA: 
    1. In pure ALOHA, <mark>when a frame first arrives</mark> , the node immediately transmits the frame in its entirety into the broadcast channel.
    2. If a transmitted frame experiences a collision with one or more other transmissions, the node will then immediately (after completely transmitting its collided frame) <mark>retransmit the frame with probability p</mark>.
    3. Otherwise, the node <mark>waits for a frame transmission time</mark>. After this wait, it then <mark>transmits the frame with probability p</mark>, or <mark>waits</mark> (remaining idle) for another frame time <mark>with probability 1 – p</mark>.


-  Carrier sensing—a node listens to the channel before transmitting. If a frame from another node is currently being transmitted into the channel, a node then <mark>waits until it detects no transmissions for a short amount of time</mark> and then begins transmission
-  Collision detection—a transmitting node listens to the channel while it is transmitting. If it detects that another node is transmitting an interfering frame, it <mark>stops transmitting and waits a random amount of time</mark> before repeating the sense-and-transmit-when-idle cycle.

- channel propagation delay of a broadcast channel:the time it takes for a signal to propagate from one of the nodes to another.will play a crucial role in determining its performance. The longer this propagation delay, the larger the chance that a carrier-sensing node is not yet able to sense a transmission that has already begun at another node in the network

- Carrier Sense Multiple Access with Collision Dection (CSMA/CD):When a node performs collision detection, it ceases transmission as soon as it detects a collision

![csma/cd](/images/computer_networking_topdown/csma_cd.png)


- CSMA/CD from the perspective of an <mark>adapter</mark> (in a node) attached to a broadcast channel:

    1.  The adapter obtains a datagram from the network layer, prepares a link-layer frame, and puts
    the frame adapter buffer.
    2.  If the adapter senses that the <mark>channel is idle</mark> (that is, there is no signal energy entering the adapter from the channel), it starts to transmit the frame. If, on the other hand, the adapter senses that the channel is busy, it waits until <mark>it senses no signal energy</mark> and then starts to transmit the frame.
    3.  While transmitting, the adapter monitors for <mark>the presence of signal energy coming from other adapters using the broadcast channel</mark>.
    4.  If the adapter transmits the entire frame <mark>without detecting signal energy from other adapters</mark>, the adapter is finished with the frame. If, on the other hand, the adapter detects signal energy from other adapters while transmitting, it <mark>aborts</mark> the transmission (that is, it stops transmitting its frame).
    5.  After aborting, the adapter <mark>waits a random amount of time</mark> and then returns to step 2.

- The binary exponential backoff algorithm:when transmitting a frame that has <mark>already experienced n collisions</mark>, a node chooses the value of K <mark>at random</mark> from $\{ 0,1,2,...2^{n−1} \}$,For <mark>Ethernet</mark>, the actual amount of time a node waits is $K\times the \ amount \ of \ time \ needed \ to \ send \ 512 \ bits \ into \ the \ Ethernet$, the maximum value that n can take is capped at 10

- Taking-Turns Protocols:
    1. polling protocol. The polling protocol requires one of the nodes to be designated as a master node. The master node polls each of the nodes in a round-robin fashion. In particular, the master node first sends a message to node 1, saying that it (node 1) can transmit up to some maximum number of frames. After node 1 transmits some frames, the master node tells node 2 it (node 2) can transmit up to the maximum number of frames. (The master node can determine when a node has finished sending its frames by observing the lack of a signal on the channel.) The procedure continues in this manner, with <mark>the master node polling each of the nodes in a cyclic manner</mark>.
    2. token-passing protocol. In this protocol there is <mark>no master node</mark>. A small, special-purpose frame known as a <mark>token</mark> is exchanged among the nodes in some fixed order. For example, node 1 might always send the token to node 2, node 2 might always send the token to node 3, and node N might always send the token to node 1. When a node receives a token, it holds onto the token <mark>only if it has some frames to transmit</mark>; otherwise, it immediately forwards the token to the next node. If a node does have frames to transmit when it receives the token, it sends up to a maximum number of frames and then forwards the token to the next node.


- DOCSIS: The Link-Layer Protocol for Cable Internet Access: DOCSIS uses FDM to divide the downstream (CMTS to modem) and upstream (modem to CMTS) network segments into multiple <mark>frequency channels</mark>(all broadcast chanels),each upstream channel is divided into intervals of time (TDM-like).

![DOCSIS](/images/computer_networking_topdown/DOCSIS.png)

- How does the CMTS know which cable modems have data to send in the first place? This is accomplished by having cable modems send <mark>mini-slot-request frames</mark> to the CMTS during a special set of interval mini-slots that are dedicated for this purpose,These mini-slot-request frames are transmitted in a <mark>random access manner</mark> and so may collide with each other.When a collision is inferred, a cable modem uses <mark>binary exponential backoff</mark> to defer the retransmission of its mini-slot-request frame to a future time slot. 

- In truth, it is not hosts and routers that have link-layer addresses but rather their <mark>adapters</mark> (that is, network interfaces) that have link-layer addresses. 

- <mark>link-layer switches do not have link- layer addresses</mark> associated with their interfaces that connect to hosts and routers

- A link-layer address is variously called a LAN address, a physical address, or a MAC address.


- For most LANs (including Ethernet and 802.11 wireless LANs), the MAC address is <mark>6 bytes long</mark>, giving $2^{48}$  possible MAC addresses.

- One interesting property of MAC addresses is that <mark>no two adapters have the same address</mark>.

- An adapter’s MAC address has a <mark>flat structure</mark> (as opposed to a hierarchical structure) and <mark>doesn’t change</mark> no matter where the adapter goes.

- Sometimes a sending adapter does want all the other adapters on the LAN to receive and process the frame it is about to send. In this case, the sending adapter inserts a special <mark>MAC broadcast address</mark> into the destination address field of the frame. For LANs that use 6-byte addresses (such as Ethernet and 802.11), the broadcast address is a string of 48 consecutive 1s (that is, FF-FF-FF-FF-FF- FF in hexadecimal notation)

- Address Resolution Protocol (ARP):translate between network-layer addresses (for example, Internet IP addresses) and link-layer addresses (that is, MAC addresses)

- ARP resolves IP addresses only for hosts and router interfaces <mark>on the same subnet</mark>.

- Each host and router has an <mark>ARP table</mark> in its memory, which contains mappings of IP addresses to MAC addresses. 
-  The ARP table also contains a <mark>time- to-live (TTL)</mark> value, which indicates when each mapping will be deleted from the table.
-   A table does not necessarily contain an entry for every host and router on the subnet; some may have never been entered into the table, and others may have expired.

- How does ARP work:
    1. The sending host needs to obtain the MAC address of the destination given the IP address by consulting to ARP table.
    2. If the ARP table doesn’t currently have an entry for the destination,the sender constructs a special packet called an <mark>ARP packet</mark>,adapter along with an indication that the adapter should send the packet to the <mark>MAC broadcast address</mark>, namely, FF-FF-FF- FF-FF-FF.  
    3. The adapter encapsulates the ARP packet in a link-layer frame, uses the broadcast address for the frame’s destination address, and transmits the frame into the subnet.
    4. The frame containing the ARP query is received by <mark>all the other adapters on the subnet</mark>, and (because of the broadcast address) each adapter passes the ARP packet within the frame up to its ARP module.Each of these ARP modules checks to see <mark>if its IP address matches the destination IP address in the ARP packet</mark>. The one with a match sends back to the querying host a <mark>response ARP packet</mark> with the desired mapping. The querying host  can then <mark>update its ARP table</mark> and send its IP datagram, encapsulated in a link-layer frame whose destination MAC is that of the host or router responding to the earlier ARP query.
  

- Sending a Datagram off the Subnet:
    1. The sending host passes the datagram to its adapter
    2. Sending host adapter acquires the appropriate MAC address for the frame which is <mark>the address of the adapter for first hop router interface</mark> by using ARP
    3. Once the sending adapter has this MAC address, it creates a frame (containing the datagram with the target IP address of the router) and sends the frame into the Subnet . The router adapter on Subnet sees that the link-layer frame is addressed to it, and therefore passes the frame to the network layer of the router.
    4. The router now has to determine the correct interface on which the datagram is to be forwarded.  This is done by consulting a <mark>forwarding table</mark> in the router.
    5. This interface then passes the datagram to its adapter, which encapsulates the datagram in a new frame and sends the frame into another Subnet. The destination MAC address is again acquired by ARP .

- Today,Ethernet mainly uses a switch-based star topology.
- switch is not only “collision-less” but is also a bona-fide store-and-forward packet switch
- a switch operates only up through layer 2

- Ethernet Frame Structure
![ethernet_frame](/images/computer_networking_topdown/ethernet_frame.png)

1. Data field (46 to 1,500 bytes). This field carries the IP datagram.
2. Destination address (6 bytes)
3. Source address (6 bytes).
4. Type field (2 bytes): The type field permits Ethernet to multiplex and demultiplex network-layer protocols
5. Cyclic redundancy check (CRC) (4 bytes). the purpose of the CRC field is to allow the receiving adapter, adapter B, to detect bit errors in the frame
6. Preamble (8 bytes). The Ethernet frame begins with an 8-byte preamble field. Each of the first 7 bytes of the preamble has a value of 10101010;(this allows the receiver to set its clock) the last byte is 10101011. The first 7 bytes of the preamble serve to “wake up” the receiving adapters and to synchronize their clocks to that of the sender’s clock.The last 2 bits of the eighth byte of the preamble (the first two consecutive 1s) alert adapter B that the “important stuff” is about to come



- All of the Ethernet technologies provide connectionless service to the network layer. That is, there is <mark>no handshaking</mark>.

- Ethernet technologies provide an <mark>unreliable service</mark> to the network layer. Specifically, when adapter B receives a frame from adapter A, it runs the frame through a CRC check, but doesn't send ACK or NCK. When a frame fails the CRC check, adapter B <mark>simply discards the frame</mark>.
- Ethernet Acronyms Naming Order:
    1. The first part of the acronym refers to <mark>the speed of the standard</mark>
    2. "BASE" refers to baseband Ethernet, meaning that the physical media <mark>only carries Ethernet traffic</mark>
    3.  The final part of the acronym refers to <mark>the physical media itself</mark>;

- Filtering is the switch function that determines <mark>whether a frame should be forwarded to some interface or should just be dropped</mark>
- Forwarding is the switch function that determines <mark>the interfaces to which a frame should be directed, and then moves the frame to those interfaces</mark>
-  Switch filtering and forwarding are done with a <mark>switch table</mark>. The switch table contains entries for some, but not necessarily all, of the hosts and routers on a LAN. An entry in the switch table contains 
    1. A MAC address 
    2. The switch interface that leads toward that MAC address
    3. The time at which the entry was placed in the table

- In a <mark>switch-based Ethernet LAN</mark> there are <mark>no collisions</mark> because a switch coordinates its transmissions and <mark>never forwards more than one frame onto the same interface</mark> at any time. and, therefore, there is <mark>no need for a MAC protocol</mark> such as CSMA/CD.


- The switch indexes its table with <mark>the MAC address</mark>. There are three possible cases:
    1. There is <mark>no entry</mark> in the table for the address. In this case, the switch forwards copies of the frame to the output buffers preceding <mark>all interfaces except for interface it came in</mark>. In other words, if there is no entry for the destination address, the switch <mark>broadcasts</mark> the frame
    2. There is <mark>an entry</mark> in the table, associating the with <mark>interface it came in</mark>. In this case, the frame is coming from a LAN segment that <mark>contains adapter with the MAC address of the requested MAC address</mark>. There being no need to forward the frame to any of the other interfaces, the switch performs the filtering function by <mark>discarding the frame</mark>.
    3. There is <mark>an entry</mark> in the table, associating the requested MAC address with <mark>interface different from the one it came in</mark>. In this case, the frame needs to be forwarded to the LAN segment <mark>attached to interface mentioned</mark>. The switch performs its forwarding function by putting the frame in an output buffer that precedes the interface.
 
- How the switches implement Self-Learning ability:
  1. The switch table is <mark>initially empty</mark>.
  2. For each incoming frame received on an interface, the switch stores in its table:
      1. The MAC address in the frame’s <mark>source address</mark> field 
      2. The interface from which the frame arrived
      3. The current time. 
  3. The switch deletes an address in the table if no frames are received with that address as the source address <mark>after some period of time</mark> (the aging time).


- We can identify several advantages of using switches, rather than broadcast links such as buses or hub-based star topologies:
    1. Elimination of collisions:The switches buffer frames and <mark>never transmit more than one frame on a segment</mark> at any one time.
    2. Heterogeneous links:the different links in the LAN can operate at <mark>different speeds</mark> and can run over <mark>different media</mark>.
    3. Management:switch also <mark>eases network management</mark>.

- Switches Versus Routers
  1. Switches:
    - Pros:
        - Switches are <mark>plug-and-play</mark>
        - Switches can also have relatively <mark>high filtering and forwarding rates</mark>.
    - Cons:
        - To prevent the cycling of broadcast frames, the active topology of a switched network is <mark>restricted to a spanning tree</mark>
        - A large switched network would require <mark>large ARP tables</mark> in the hosts and routers and would generate substantial <mark>ARP traffic</mark> and processing.
        - Switches are susceptible to <mark>broadcast storms</mark>—if one host goes haywire and transmits an endless stream of Ethernet broadcast frames, the switches will forward all of these frames, causing the entire network to collapse. 
  2. Routers:
    - Pros:
        - Because network addressing is often hierarchical , packets <mark>do not normally cycle through routers</mark> even when the network has redundant paths.
        - Another feature of routers is that they provide <mark>firewall protection</mark> against layer-2 broadcast storms.
    - Cons:
        - They are not plug-and-play—they and the hosts that connect to them need their <mark>IP addresses to be configured</mark> 
        - Routers often have a <mark>larger per-packet processing time</mark> than switches, because they have to process up through the layer-3 fields.

- VLAN:a switch that supports VLANs allows <mark>multiple virtual local area networks</mark> to be defined over a <mark>single physical local area network infrastructure</mark>. Hosts within a VLAN communicate with each other as if they (and no other hosts) were connected to the switch.
![VLAN](/images/computer_networking_topdown/VLAN.png)

- VLAN trunking:In the VLAN trunking approach , a special port on each switch  is configured as a <mark>trunk port</mark> to interconnect the two VLAN switches. The trunk port belongs to all VLANs, and <mark>frames sent to any VLAN are forwarded over the trunk link</mark> to the other switch. 
![TRUNK_LINK](/images/computer_networking_topdown/TRUNK_LINK.png)


> # Chapter 7 Wireless and Mobile Networks

- When we say a wireless host is<mark>“associated”</mark> with a base station, we mean that 
  1. the host is within the wireless communication distance of the base station. 
  2. the host uses that base station to relay data between it (the host) and the larger network.

- Hosts associated with a base station are often referred to as operating in <mark>­infrastructure mode</mark>,since all traditional network services (e.g., address assignment and routing) are provided by the network to which a host is connected via the base station.
-  In <mark>ad hoc networks</mark>, wireless hosts have no such infrastructure with which to connect. In the absence of such infrastructure, <mark>the hosts themselves</mark> must provide for services such as routing, address assignment, DNS-like name translation, and more.
-  When a mobile host moves beyond the range of one base station and into the range of another, it will change its <mark>point of attachment</mark> into the larger network,a process referred to as <mark>handoff</mark>

- At the highest level we can classify wireless networks according to two criteria: 
    1. Whether a packet in the wireless network crosses exactly <mark>one wireless hop or multiple wireless hops</mark> 
    2. Whether there is <mark>infrastructure</mark> such as a base station in the network
  - Single-hop, infrastructure-based. These networks have a base station that is connected to a larger wired network (e.g., the Internet). Furthermore, all communication is between this base station and a wireless host over a single wireless hop.eg:802.11 networks,4G LTE data networks.
  - Single-hop, infrastructure-less. In these networks, there is no base station that is connected to a wireless network. However, as we will see, one of the nodes in this single-hop network may coordinate the transmissions of the other nodes.eg:Bluetooth,802.11 ad hoc mode.
  - Multi-hop, infrastructure-based. In these networks, a base station is present that is wired to the larger network. However, some wireless nodes may have to relay their communication through other wireless nodes in order to communicate via the base station.eg: Wireless sensors,Wireless Mesh Networks.
  - Multi-hop, infrastructure-less. There is no base station in these networks, and nodes may have to relay messages among several other nodes in order to reach a destination. Nodes may also be mobile, with connectivity changing among nodes

- Differences between a wired link and a wireless link:
    1. Decreasing signal strength
    2. Interference from other sources
    3. Multipath propagation

- The SNR(Signal Noise Ratio), measured in dB, is <mark>twenty times the ratio of the base-10 logarithm of the amplitude of the received signal to the amplitude of the noise</mark>.

- Several physical-layer characteristics that are important in understanding higher-layer wireless communication protocols:
    1. For a given modulation scheme, the higher the SNR, the lower the BER.
    2. For a given SNR, a modulation technique with a higher bit transmission rate (whether in error or not) will have a higher BER.
    3. <mark>Dynamic selection of the physical-layer modulation</mark> technique can be used to adapt the modulation technique to channel conditions.

- <mark>Code division multiple access (CDMA)</mark> belongs to the family of <mark>channel partitioning protocols</mark>.
- In a CDMA protocol, each bit being sent is encoded by <mark>multiplying the bit by a signal</mark> (the code) that changes at a much faster rate (known as the chipping rate) than the original sequence of data bits
- How CDMA Works:
    - Let $d_i$  be the value of the data bit for the $i$th bit slot.
    - We represent a data bit with a 0 value as <mark>-1</mark> . 
    - Each bit slot is further subdivided into <mark>M mini-slots</mark>;
    - The CDMA code used by the sender consists of a sequence of M values,$c_m$,m=1,2,3,...M,each taking a +1 or -1 value.
    - Focus on the ith data bit, $d_i$ .For the mth mini-slot of the bit- transmission time of $d_i$ , the output of the CDMA encoder,$Z_{i,m}$, is the value of <mark>$d_i$  multiplied by the mth bit in the assigned CDMA code, $c_m$;</mark>
    $$ Z_{i,m} = d_i\times c_m $$
    1. With no interfering senders, the receiver would receive the encoded bits, $Z$ , and <mark>recover the original data bit</mark>, d , by computing:
    $$ d_i= \frac{\sum^{M}_{m=1} Z_{i,m}\cdot c_m }{M} $$
    2. In the presence of <mark>multiple senders</mark>, sender s computes its encoded transmissions,$Z_{i,m}$, in exactly the same manner.The value received at a receiver during the $m$th mini-slot of the ith bit slot, however, is now the <mark>sum of the transmitted bits from all N senders during that mini-slot</mark>:
    $$ Z_{i,m}^{*} =\sum_{j=1}^{N} Z_{i,m}^{j} =  \sum_{j=1}^{N} d_{i}^{j}\cdot c_{m}^{j} $$
    3. If the senders’ codes are chosen carefully(each two combination is <mark>orthogonal</mark>), each receiver can recover the data sent by a given sender out of the aggregate signal simply by using the sender’s code <mark>in exactly the same manner</mark> as in Equation :
    $$ d_{i}^{j} = \frac{\sum_{m=1}^{M} Z_{i,m}^{*} \cdot c_{m}^{j} }{M} $$
    

- When a network administrator installs an AP, the administrator assigns a one- or two-word <mark>Service Set Identifier (SSID)</mark> to the access point.
- Within this 85 MHz band, 802.11 defines <mark>11 partially overlapping channels</mark>. Any two channels are non-overlapping if and only if they are separated by four or more channels. In particular, <mark>the set of channels 1, 6, and 11 is the only set of three non-overlapping channels</mark>.


- The fundamental building block of the 802.11 architecture is the <mark>basic service set (BSS)</mark>. A BSS contains one or more wireless stations and a central base station, known as an <mark>access point (AP)</mark> in 802.11 <mark>parlance</mark>. 


- How A Wireless Device Associates With An AP:

    1. Detect
        1. The 802.11 standard requires that an AP periodically send <mark>beacon frames</mark>, each of which includes the AP’s <mark>SSID and MAC address</mark>.
        2. Wireless devices, scan the <mark>11 channels</mark>, seeking beacon frames

    2. Request
        1.  the wireless device sends an <mark>association request frame</mark>
        2.  the AP responds with an <mark>association response frame</mark>
    3. Authenticate
        1. The host provides AP with some information.The AP typically communicates with an <mark>authentication server</mark> to verify these information, relaying information between the wireless device and the authentication server using a protocol such as <mark>RADIUS</mark>  or <mark>DIAMETER</mark>.
    4. Assign IP
        The host is assigned an IP address following <mark>DHCP protocol</mark>

- How 802.11 CSMA/CA Protocol Works:
    1. If initially the station senses the channel <mark>idle</mark>, it transmits its frame after a short period of time known as the <mark>Distributed Inter-frame Space (DIFS)</mark>; 
    2. Otherwise, the station chooses a random backoff value using <mark>binary exponential backoff</mark>  and counts down this value after <mark>DIFS</mark> when the channel is sensed <mark>idle</mark>. While the channel is sensed busy, the counter value remains <mark>frozen</mark>.
    3. When the counter reaches zero (note that this can only occur while the channel is sensed <mark>idle</mark>), the station transmits the <mark>entire frame</mark> and then waits for an acknowledgment.
    4. If an <mark>acknowledgment</mark> is received, the transmitting station knows that its frame has been correctly received at the destination station. If the station has another frame to send, it begins the CSMA/CA protocol at step 2. If the acknowledgment isn’t received, the transmitting station reenters the backoff phase in step 2, with the random value chosen from a <mark>larger interval</mark>.

    
- Because 802.11wireless LANs do not use collision detection, once a station begins to transmit a frame, it transmits the frame <mark>in its entirety regardless of collision</mark>.

- When the destination station receives a frame that <mark>passes the CRC</mark>, it waits a short period of time known as the <mark>Short Inter-frame Spacing (SIFS)</mark> and then sends back an acknowledgment frame.

- Why Does CDMA/CA Take Different Approach With CDMA/CA:In 802.11, if the two stations sense the channel busy, they both immediately enter <mark>random backoff</mark>, hopefully choosing <mark>different backoff values</mark>. If these values are indeed different, once the channel becomes idle, one of the two stations will begin transmitting before the other, and  the <mark>“losing station”</mark> will hear the <mark>“winning station’s”</mark> signal, <mark>freeze</mark> its counter, and refrain from transmitting until the winning station has completed its transmission

- Dealing With <mark>Hidden Terminals</mark>: <mark>RTS</mark> and <mark>CTS</mark>: the IEEE 802.11 protocol allows a station to use a short <mark>Request to Send (RTS)</mark> control frame and a short <mark>Clear to Send (CTS)</mark> control frame to reserve access to the channel:
    1. When a sender wants to send a DATA frame, it can first send an RTS frame to the AP, indicating the <mark>total time required to transmit the DATA frame and the acknowledgment (ACK) frame</mark>. 
    2. When the AP receives the RTS frame, it responds by <mark>broadcasting a CTS frame</mark>. This CTS frame serves two purposes: 
        - It gives the sender explicit <mark>permission</mark> to send. 
        - Instructs the other stations <mark>not to send</mark> for    the <mark>reserved duration</mark>.


![RTS_CTS](/images/computer_networking_topdown/RTS_CTS_.png)

- Although the RTS/CTS exchange can help reduce collisions, it also introduces delay and consumes channel resources. For this reason, the RTS/CTS exchange is only used (if at all) to reserve the channel for the transmission of a <mark>long DATA frame</mark>. In practice, each wireless station can set an RTS threshold such that the RTS/CTS sequence is used only when the frame is longer than the threshold.


- 802.11 frame has four address fields,each of which can hold a 6-byte MAC address, three address fields are needed for moving the network-layer datagram from a wireless station through an AP to a router interface. The fourth address field is used when APs ­forward frames to each other in ad hoc mode.  Since we are only considering infrastructure networks here, let’s focus our attention on the first three address fields. The 802.11 standard defines these fields as follows:
    1. Address 1 is the MAC address of the wireless station that is <mark>to receive the frame</mark>.
    2. Address 2 is the MAC address of the station that <mark>transmits the frame</mark>
    3. Address 3  contains the MAC address of <mark>gateway router</mark> of the subnet.

- Because acknowledgments can get lost, the sending station may send <mark>multiple copies of a given frame</mark>. The sequence number field in the 802.11 frame thus serves exactly the same purpose here at the link layer as it did in the transport layer.

- The duration value is included in the frame’s duration field to request for reserve the channel for a period of time.

- 802.11 Rate Adaptation:some 802.11 implementations have a rate adaptation capability that adaptively selects the underlying <mark>physical-layer modulation technique</mark> to use based on <mark>current or recent channel characteristics</mark>. 

- Power Management:A node is able to explicitly alternate between <mark>sleep and wake states</mark>.A node indicates to the access point that it will be going to sleep by setting the <mark>power-management bit</mark> in the header of an 802.11 frame to 1. A <mark>timer</mark> in the node is then set to <mark>wake up</mark> the node just before the AP is scheduled to send its beacon frame (recall that an AP typically sends a beacon frame every 100 msec). 

- In Cellular Network,The term cellular refers to the fact that the region covered by a cellular network is <mark>partitioned into a number of geographic coverage areas</mark>, known as <mark>cells</mark>.
- Each cell contains a <mark>base transceiver station (BTS)</mark> that transmits signals to and receives signals from the mobile stations in its cell. 


- The GSM standard for 2G cellular systems uses <mark>combined FDM/TDM (radio)</mark> for the air interface.In combined FDM/TDM systems, the channel is partitioned into a number of frequency sub-bands; within each sub-band, time is partitioned into frames and slots. Thus, for a combined FDM/TDM system, if the channel is partitioned into F sub-bands and time is partitioned into T slots, then the channel will be able to support $F\cdot T$ simultaneous calls.
- the <mark>mobile switching center (MSC)</mark> plays the central role in user authorization and accounting, call establishment and teardown, and handoff. 
- The role of the <mark>base station controller (BSC)</mark> is to allocate <mark>BTS radio channels</mark> to mobile subscribers, perform paging (finding the cell in which a mobile user is resident), and perform handoff of mobile users.
![cellular_2g](/images/computer_networking_topdown/cellular_2g.png)

- There are two types of nodes in the 3G core network: <mark>Serving GPRS Support Nodes (SGSNs)</mark> and <mark>Gateway GPRS Support Nodes (GGSNs)</mark>:
    1. An SGSN is responsible for delivering datagrams to/from the mobile nodes in the radio access network where the SGSN is attached. The SGSN interacts with the cellular voice network’s <mark>MSC</mark> for that area, providing user authorization and handoff, maintaining location (cell) information about active mobile nodes, and performing datagram forwarding between mobile nodes in the radio access network and a GGSN. 
    2. The GGSN acts as a <mark>gateway</mark>, connecting multiple SGSNs into the larger Internet. 

- The <mark>Radio Network Controller (RNC)</mark> typically controls several cell base transceiver stations.The RNC connects to both the circuit-switched cellular voice network via an <mark>MSC</mark>, and to the packet-switched Internet via an <mark>SGSN</mark>.

- A significant change in 3G UMTS over 2G networks is that rather than using GSM’s FDMA/TDMA scheme, UMTS uses a CDMA technique known as Direct Sequence Wideband CDMA (DS-WCDMA) within TDMA slots:TDMA slots, in turn, are available on multiple frequencies

![3g_network](/images/computer_networking_topdown/3g_network.png)


- Changes in 4G over 3G network:
    1. <mark>All-IP</mark> network architecture:the 4G architecture carries both  voice and data in <mark>IP datagrams</mark>.With 4G, the last vestiges of cellular networks’ roots in the telephony have disappeared.
    2. A clear separation of the 4G data plane and 4G control plane.
    3. A clear separation between the radio access network, and the all-IP-core ­network

- The principal components of the 4G architecture are as follows:
    1. The eNodeB is the logical descendant of the 2G base station and the 3G Radio Network Controller(a.k.a Node B) and again plays a central role here. Its data-plane role is to forward datagrams between UE (over the LTE radio access ­network) and the P-GW.UE datagrams are encapsulated at the eNodeB and tunneled to the P-GW through the 4G network’s all-IP enhanced packet core (EPC).
    2. The Packet Data Network Gateway (P-GW) allocates IP addresses to the UEs and performs QoS enforcement. As a tunnel endpoint it also performs datagram encapsulation/decapsulation when forwarding a datagram to/from a UE.
    3. The Serving Gateway (S-GW) is the data-plane mobility anchor point—all UE traffic will pass through the S-GW. The S-GW also performs charging/billing functions and lawful traffic interception.
    4. The Mobility Management Entity (MME) performs connection and mobility management on behalf of the UEs resident in the cell it controls. It receives UE subscription information from the HHS.
    5. The Home Subscriber Server (HSS) contains UE information including roaming access capabilities, quality of service profiles, and authentication information. 

![4g_network](/images/computer_networking_topdown/4g_network.png)

- LTE Radio Access Network:LTE uses a combination of frequency division multiplexing and time division multiplexing on the downstream channel, known as orthogonal frequency division multiplexing (OFDM):In LTE, each active mobile node is allocated one or more 0.5 ms time slots in one or more of the channel frequencies.

![lte](/images/computer_networking_topdown/lte.png)

- The permanent home of a mobile node (such as a laptop or smartphone) is known as the <mark>home network</mark>
-  The entity within the home network that performs the mobility management functions  on behalf of the mobile node is known as the <mark>home agent</mark>
-  The network in which the mobile node is currently residing is known as the <mark>foreign (or visited) network</mark>
-   the entity within the foreign network that helps the mobile node with the mobility management functions discussed below is known as a <mark>foreign agent</mark>.
-   A <mark>correspondent</mark> is the entity wishing to communicate with the mobile node

- How Indirect Routing Works:
    1. the correspondent simply addresses the datagram to the mobile node’s <mark>permanent address</mark> and sends the datagram into the network
    2.  Such datagrams are first routed, as usual, to the mobile node’s <mark>home network</mark>.
    3. The datagram is  forwarded to the <mark>foreign agent</mark>, using the mobile node’s COA
    4. The datagram is forwarded from the foreign agent to the <mark>mobile node</mark>
   
![indirect_routing](/images/computer_networking_topdown/indirect_routing.png)

- We’ll identify the foreign agent in that foreign network where the mobile node was <mark>first found</mark> as the <mark>anchor ­foreign agent</mark>.
- How Direct Routing Works:
    1. A correspondent agent in the correspondent’s network querys the home agent to learn the <mark>COA of the mobile node</mark>.
    2. The correspondent agent then tunnels datagrams directly to the mobile node’s COA.
    3. When the mobile node moves to a new foreign network, the mobile node registers with the new foreign agent, and the new foreign agent provides the <mark>anchor foreign agent</mark> with the mobile node’s new COA. 
    4. When the anchor foreign agent receives an encapsulated datagram for a departed mobile node, it can then re-encapsulate the datagram and forward it to the mobile node (step 5) using the new COA. 

![direct_routing](/images/computer_networking_topdown/direct_routing.png)

- The <mark>mobile IP standard</mark> consists of three main pieces:
    1. Agent discovery
    2. Registration with the home agent
    3. Indirect routing of datagrams

- Agent Discovery:A mobile IP node arriving to a new network learn the identity of the corresponding <mark>foreign or home agent</mark>.

- Agent discovery can be accomplished in one of two ways: via <mark>agent advertisement</mark> or via <mark>agent solicitation</mark>.
- With agent advertisement,  the agent periodically broadcasts an <mark>ICMP message</mark> with a <mark>type field of 9 (router discovery)</mark> on all links to which it is connected. The router discovery message contains the IP address of the router (that is, the agent), thus allowing a mobile node to learn the agent’s IP address.It also contains <mark>Care-of address (COA)</mark> fields providing a list of one or more care-of addresses mobile node to choose.
- With agent solicitation, a mobile node can <mark>broadcast</mark> an agent solicitation message, which is simply an <mark>ICMP message with type value 10</mark>. An agent receiving the solicitation will unicast an agent advertisement directly to the mobile node.
- Registration with the Home Agent:
    1. Following the receipt of a foreign agent advertisement, a mobile node sends a  <mark>registration message</mark> to the foreign agent carrying a <mark>COA</mark> advertised by the foreign agent, the address of the home agent (HA), the permanent address of the mobile node (MA)
    2. The foreign agent receives the registration message and records the mobile node’s permanent IP address.The foreign agent then sends a registration message to the <mark>home agent</mark>. 
    3. The home agent receives the registration request , binds the mobile node’s permanent IP address with the COA;  The home agent sends a mobile IP registration <mark>reply</mark>.
    4. The foreign agent receives the registration reply and then forwards it to the <mark>mobile node</mark>.Registration is complete.
![mobile_ip](/images/computer_networking_topdown/mobile_ip.png)

- How Routing Calls to a Mobile User Works In GSM:
    1. The correspondent dials the mobile user’s phone number.The call is routed from the correspondent through the PSTN to the <mark>home MSC</mark> in the mobile’s home network.
    2. The home MSC receives the call and interrogates the <mark>HLR</mark> to determine the location of the mobile user. In the simplest case, the HLR returns the <mark>mobile station roaming number (MSRN)</mark>,If HLR does not have the roaming number, it returns the address of the <mark>VLR</mark> in the visited network. In this case , the home MSC will need to query the VLR to obtain the roaming number of the mobile node. 
    3. Given the roaming number, the home MSC sets up the second leg of the call through the network to the MSC in the <mark>visited network</mark>. The call is completed, being routed from the correspondent to the home MSC, and from there to the visited MSC, and from there to the base station serving the mobile user.

- How the HLR obtains information about the location of the mobile user:
    1. When a mobile telephone is switched on or enters a part of a visited network that is covered by a new VLR, the mobile <mark>registers with the visited network</mark>.
    2. The visited VLR, in turn, sends a location update request message to the mobile’s <mark>HLR</mark>. This message informs the HLR of either the <mark>roaming number</mark> at which the mobile can be contacted, or the <mark>address of the VLR</mark>.
    3.  As part of this exchange, the VLR also obtains subscriber information from the HLR about the mobile and determines what services (if any) should be accorded the mobile user by the visited network

- A handoff occurs when a mobile station changes its association from one base station to another during a call:
    1. The old base station (BS) informs the visited MSC that <mark>a handoff is to be performed</mark> and the BS (or possible set of BSs) to which the mobile is to be handed off.
    2. The visited MSC initiates path setup to the new BS, allocating the resources needed to carry the rerouted call, and signaling the new BS that a handoff is about to occur.
    3. The new BS allocates and activates a radio channel for use by the mobile.
    4. The new BS signals back to the visited MSC and the old BS that the visited-MSC-to-new-BS path <mark>has been established</mark> and that the mobile should be informed of the pending handoff.
    5.  The mobile is informed that it should perform a handoff.  
    6.  The mobile and the new BS exchange one or more messages to fully activate the new channel  in the new BS. 
    7.  The mobile sends a <mark>handoff complete message</mark> to the new BS, which is forwarded up to the  visited MSC. The visited MSC then <mark>reroutes the ongoing call</mark> to the mobile via the new BS. 
    8.  The resources allocated along the path to the old BS are then <mark>released</mark>
   
![handoff](/images/computer_networking_topdown/handoff.png)

-  What happens when the mobile moves to a BS that is associated with a <mark>different MSC</mark> :
    1. GSM defines the notion of an <mark>anchor MSC</mark>. The anchor MSC is the MSC visited by the mobile <mark>when a call first begins</mark>; the anchor MSC thus remains <mark>unchanged</mark> during the call. 
    2. Throughout the call’s duration, the call is routed <mark>from the home MSC to the anchor MSC</mark>, and then <mark>from the anchor MSC to the visited MSC</mark> where the mobile is currently located.
![handoff_diff_msc](/images/computer_networking_topdown/handoff_multi_msc.png)




> # Chapter 8 Network Security

- Symmetric Key Encryption: encrypted communication required that the two communicating parties share a <mark>common secret</mark>

- How Block Cipher Works:
  
    1. In a block cipher, the message to be encrypted is processed in <mark>blocks of k bits</mark>.
    2. Block cipher uses a function  to break a k-bit block into <mark>n chunks</mark>, with each chunk consisting of <mark>k/n bits</mark>. 
    3. Each k/n-bit chunk is processed by an <mark>k/n-bit to k/n-bit table</mark>
    4. Next, the n output chunks are <mark>reassembled</mark> into a new k-bit block.
    5. The positions of the k bits in the block are then scrambled (permuted) to produce a k-bit output.
    6. This output is fed back to the k-bit input, where <mark>another cycle begins</mark>.

![block_cipher](/images/computer_networking_topdown/block_cipher.png)


- To avoid same ciphertext blocks originated from same cleartext blocks:The sender creates a <mark>random k-bit number r(i)</mark> for the ith block and calculates <mark>$c(i)=K_s( m(i) \oplus r(i))$</mark>,where block-cipher encryption algorithm with key S as $K_{s}$ , m(i) denote the ith plaintext block.

- In order to save overhead of sending random bits, block ciphers typically use a technique called <mark>Cipher Block Chaining (CBC)</mark>: 
    1. Before encrypting the message (or the stream of data), the sender generates a <mark>random k-bit string</mark>, called the <mark>Initialization Vector (IV)</mark>. Denote this initialization vector by c(0). The sender sends the IV to the receiver in <mark>cleartext</mark>.
    2.  For the first block, the sender calculates the exclusive-or of the first block of cleartext with the IV. It then runs the result through the block-cipher algorithm to get the corresponding ciphertext block; that is,$c(1)=K_S(m(1)\oplus c(0))$ . The sender sends the encrypted block c(1) to the receiver
    3.  For the ith block, the sender generates the ith ciphertext block from <mark>$c(i)= K_S(m(i)\oplus c(i−1))$</mark>


- Public Key Encryption:
    1. Suppose Alice wants to communicate with Bob.We will use the notation <mark>$K_B^+$</mark> and <mark>$K_B^-$</mark>  to refer to Bob’s <mark>public key</mark> and <mark>private keys</mark>,respectively. Alice first fetches Bob’s public key. Alice then encrypts her message, m, to Bob <mark>using Bob’s public key</mark> and a known (for example, standardized) encryption algorithm; that is, Alice computes <mark>$K_B^+(m)$</mark> 
    2. Bob receives Alice’s encrypted message and uses his <mark>private key</mark> and a known (for example, standardized) decryption algorithm to decrypt Alice’s encrypted message. That is, Bob computes <mark>$m=K_B^−(K_B^+(m))$</mark>


- How Does RSA Work:
    - Generate the public and private RSA keys:
        1. Choose two large prime numbers, p and q.
        2. Compute n=pq and z=(p-1)(q-1)
        3. Choose a number, e, less than n, that has no common factors (other than 1) with z. 
        4.  Find a number, d, such that  is exactly divisible (that is, with no ­remainder) by z. . Put another way, given e, we choose d such that:
        $$ e^d \ mod \ z \ = \ 1 $$ 
        5. The public key that Bob makes available to the world,$K_B^+$,, is the pair of numbers (n, e); his private key, $K_B^−$, is the pair of numbers (n, d).

    - Encryption:
        1. Suppose Alice wants to send Bob a bit pattern represented by the integer number m . To encode, Alice calculates ciphertext c is sent to Bob: 
        $$ c \ = \ m^e \ mod \ n $$ 
        2. To decrypt the received ciphertext message,  c, Bob computes
        $$ m=c^d \ mod \ n $$


- RSA is often used in practice in combination with symmetric key cryptography to <mark>deliver symmetric key</mark>(refered to as <mark>session key</mark>).

- How does Session Key work?

    1. Alice encrypts her message, m, with the <mark>symmetric key</mark>
    2. Encrypts the symmetric key with <mark>Bob’s public key</mark>,$K_B^{+}$
    2. Concatenates the encrypted message and the encrypted symmetric key to form a “package” 
    3. Sends the package to Bob’s.
    4. He uses his <mark>private key</mark>,$K_B^−$ to obtain the symmetric key,  $K_s$
    5. Bob uses the symmetric key $K_s$ to <mark>decrypt the message m</mark> 

![session_key](/images/computer_networking_topdown/session_key.png)





- A cryptographic hash function is required to have the following additional property: It is computationally infeasible to find any two <mark>different messages</mark> x and y such that $H(x)=H(y)$

- Using the <mark>shared secret s</mark>, message integrity can be performed as follows:

    1.  Alice creates message m, concatenates s with m to create $m+s$ , and calculates the hash $H(m+s)$ (for example with SHA-1). $H(m+s)$  is called the <mark>message authentication code (MAC)</mark>
    2.  Alice then appends the MAC to the message m, creating an extended message $(m,H(m+s))$, and sends the extended message to Bob.
    3.  Bob receives an extended message (m, h) and knowing s, calculates the MAC  $H(m+s)$. If $H(m+s)=h$, Bob concludes that everything is fine.

![integrity](/images/computer_networking_topdown/integrity.png)

- One nice feature of a MAC is that it <mark>does not require an encryption algorithm</mark>. 

- How Digital Signatures Work?
    1. Suppose that Bob wants to digitally sign a document, m.Bob simply uses his <mark>private key,$K_B^−$</mark>,to compute <mark>$K_B^−(H(m))$</mark>,where H is a <mark>cryptographic hash function</mark>.
    2. Alice takes Bob’s public key, $K_B^{+}$,and applies it to the digital signature,That is, she computes $K_B^+(K_B^−(H(m)))$,she produces $H(m)$.
    3. Alice runs the same cryptographic hash function on the original message m and gets $H'(m)$.She compares $H(m)$ with $H'(m)$ and if <mark>they are the same</mark> the signature is valid.

- If the original document, m, is ever modified to some alternate form, $m'$ , ́the signature that Bob created for m <mark>will not be valid</mark> for $m'$,since $H(m)$ and $H(m')$ will be different.

![digital_signature](/images/computer_networking_topdown/digital_signature.png)
![digital_signature_verification](/images/computer_networking_topdown/digital_signature_verification.png)


- Public key certification is certifying that a public key belongs to a specific entity.

- To verify that you have the actual public key of the entity (person, router, browser, and so on) with whom you want to communicate,Binding a public key to a <mark>Certification Authority (CA)</mark> and get a certificate.

- A <mark>nonce</mark> is a number that a protocol will use only <mark>once in a lifetime</mark>
-  Authentication Protocol
    1. Alice sends the message  to Bob.
    2. Bob chooses a nonce, R, and sends it to Alice.
    3. Alice encrypts the nonce using Alice and Bob’s <mark>symmetric secret key</mark>,$K_{A-B}$,  and sends the encrypted nonce,  $K_{A-B}^{-}(R)$, back to Bob. As in protocol ap3.1, it is the fact that Alice knows and uses it to encrypt a value that lets Bob know that the message he receives was generated by Alice. The nonce is used to ensure that <mark>Alice is live</mark>.
    4. Bob decrypts the received message. If the <mark>decrypted nonce equals the nonce he sent</mark>, then Alice is authenticated.


- How Does PGP Work?
    - Sender(Alice)

        1. Alice applies a <mark>hash function</mark>, H , to her message, m, to obtain a <mark>message digest</mark>. 
        2. Alice signs the digest with her private key $K_A^-$ to create a <mark>digital signature</mark>.
        3. Alice concatenates the original (unencrypted) message with the signature to create a package. 
        4. Alice selects a <mark>random symmetric session key, $K_S$</mark>.
        5. Alice encrypts her package with the <mark>symmetric key</mark>
        6. Alice encrypts the symmetric key with <mark>Bob’s public key,$K_B^+$</mark>.
        7. Alice concatenates the <mark>encrypted package</mark> and the <mark>encrypted symmetric key</mark> to form a "bigger package"
        8. Alice sends the "bigger package" to Bob.
    - Receiver(Bob)
        1. When Bob receives the package, he  uses his private key,$K_B^-$ to obtain the <mark>symmetric key, $K_S$</mark>.
        2. Bob uses the symmetric key $K_S$  to <mark>decrypt the package</mark>.
        3. Bob applies  Alice’s public key, $K_A^+$ to the <mark>signature</mark> 
        4. Bob compares the result of this operation with <mark>his own hash, H, of the message</mark>.If the two results are the same, Bob can be pretty confident that the message came from Alice and is unaltered.

![PGP1](/images/computer_networking_topdown/PGP1.png)
![PGP2](/images/computer_networking_topdown/PGP2.png)
![PGP3](/images/computer_networking_topdown/PGP3.png)


- SSL can be employed by any application that <mark>runs over TCP</mark>.

- SSL has three phases: handshake, key derivation, and data transfer.


- During the handshake phase:
    1. Bob needs to  establish a <mark>TCP connection</mark> with Alice
    2. Bob sends Alice a <mark>list of cryptographic algorithms it supports</mark>, along with a <mark>­client nonce</mark>.
    3. Alice chooses a <mark>symmetric algorithm</mark> (for example, AES), a <mark>public key algorithm</mark> (for example, RSA with a specific key length), and a <mark>MAC algorithm</mark>. then responds with her  choices, as well as a <mark>certificate</mark> and a <mark>server nonce</mark>.
    4. Bob then generates a <mark>Pre Master Secret (PMS)</mark> , encrypts the PMS with <mark>Alice’s public key</mark> to create the <mark>Encrypted Master Secret (EMS)</mark>, and sends the EMS to Alice.
    5. Alice <mark>decrypts</mark> the EMS with <mark>her private key</mark> to get the PMS.
    6. Using the <mark>same key derivation function</mark> (as specified by the SSL standard), Bob and Alice independently compute the <mark>Master Secret (MS)</mark> from the PMS and nonces. The MS is then sliced up to generate the two encryption and two MAC keys.
    7. The client sends a <mark>MAC of all the handshake messages</mark>.
    8. The server sends a <mark>MAC of all the handshake messages</mark>.
![ssl_almost](/images/computer_networking_topdown/ssl_almost.png)

- The <mark>nonce</mark> is used to prevent <mark>connection replay attack</mark>, which is replaying the sent records.(sequence numbers are used to defend against replaying individual packets during an ongoing session)

-  Alice and Bob use the MS to generate four keys:
    1. EB = session encryption key for data sent from Bob to Alice
    2. MB =  session MAC key for data sent from Bob to Alice
    3. EA =  session encryption key for data sent from Alice to Bob
    4. MA =  session MAC key for data sent from Alice to Bob

- The two encryption keys will be used to encrypt data; the two MAC keys will be used to verify the integrity of the data.


- How Does SSL Data Transfer Work?
    1. Suppose Bob is to send data. His data is represented by data streams in TCP . SSL breaks the data stream into <mark>records</mark>.
    2. Bob maintains a <mark>sequence number counter</mark>.To create the MAC, Bob inputs the <mark>record data along with the key $M_B$ and sequence number</mark>  into a hash function.The result MAC is appended  to each record.
    3. SSL <mark>encrypts</mark> the <mark>$record \ + \ MAC$</mark> using  his session encryption key <mark>$E_B$</mark>
    4. This encrypted package is then <mark>passed to TCP</mark> for transport over the Internet

- The Fields In A SSL Record:
    1. Type Field:The type field indicates whether the record is a handshake message or a message that contains application data.It is also used to close the SSL connection.
    2. Length Field:SSL at the receiving end uses the length field to extract the SSL records out of the incoming TCP byte stream


- SSL does not mandate that Alice and Bob use a specific symmetric key algorithm, a specific public-key algorithm, or a specific MAC.

- Truncation Attack:The intruder ends the session early with a TCP FIN.
- How To Prevent Truncation Attack:indicate in the <mark>type field</mark> whether the record serves to terminate the SSL session. (Although the SSL type is sent in the clear, it is <mark>authenticated at the receiver using the record’s MAC</mark>.)

- The <mark>IP security protocol</mark>, more commonly known as <mark>IPsec</mark>, provides security at the <mark>network layer</mark>

- <mark>Encapsulation Security Payload (ESP)</mark> protocol:The ESP protocol provides source authentication, data integrity, and confidentiality. 


- Before sending IPsec datagrams from source entity to destination entity, the source and destination entities create a network-layer logical connection. This logical connection is called a <mark>security association (SA)</mark>


-  An SA is <mark>unidirectional</mark> from source to destination. If both entities want to send secure datagrams to each other, then two SAs (that is, two logical connections) need to be established, one in each direction.


- SA State Information
    - A 32-bit identifier for the SA, called the <mark>Security Parameter Index (SPI)</mark>
    - The origin interface of the SA  and the destination interface of the SA. 
    - The type of encryption
    -  The encryption key
    -  The type of integrity check 
    -  The authentication key

- Whenever the gateway router  needs to construct an IPsec datagram for forwarding over this SA, it accesses the state information mentioned above to determine how it should authenticate and encrypt or decrypt the datagram.
- An IPsec entity stores the state information for all of its SAs in its <mark>Security Association Database (SAD)</mark>.





- Along with a SAD, the IPsec entity also maintains another data structure called the <mark>Security Policy Database (SPD)</mark>. The SPD indicates what types of datagrams (as a function of source IP address, destination IP address, and protocol type) are to be IPsec processed;



- IPsec Datagram Structure:

![ip_sec](/images/computer_networking_topdown/ipsec_datagram.png)


- The gateway router of the sending host uses the ­following recipe to convert “original IPv4 datagram” into an IPsec datagram:
    1. Appends to the back of the original IPv4 datagram  an <mark>“ESP trailer”</mark> field
    2. Encrypts the result using the algorithm and key specified by the SA
    3. Appends to the front of this encrypted datagram a field called <mark>“ESP header”</mark>; the resulting package is called the “enchilada”
    4. Creates an <mark>authentication MAC</mark> over the whole enchilada using the algorithm and key specified in the SA
    5. Appends the MAC to the back of the enchilada forming the payload
    6. Finally, creates a brand new IP header with all the classic IPv4 header fields, which it appends before the payload


-  The ESP header, which is sent in the clear and consists of two fields: the SPI and the sequence number field.

- IP addresses that are in the <mark>new IP header</mark> are set to the source and destination router interfaces at the two ends of the tunnels which is the gateway router of the sending host and receiving host.

- the protocol number in this new IPv4 header field is 50, designating that this is an IPsec datagram using the <mark>ESP protocol</mark>.

- Wired Equivalent Privacy (WEP):The IEEE 802.11 WEP protocol uses a <mark>symmetric shared key</mark> approach.
- WEP does not specify a key management algorithm.
- Authentication is carried out as ­follows:
1.  A wireless host requests authentication by an access point.
2.  The access point responds to the authentication request with a <mark>128-byte nonce value</mark>.
3.  The wireless host encrypts the nonce using the <mark>symmetric key</mark> that it shares with the access point.
4.  The access point <mark>decrypts</mark> the host-encrypted nonce.
5.  If the decrypted nonce matches the nonce value originally sent to the host, then the host is authenticated by the access point


- The WEP data encryption algorithm:A secret 40-bit symmetric key, $K_S$, is assumed to be known by both a host and the access point. In addition, a 24-bit Initialization Vector (IV) is appended to the 40-bit key to create a 64-bit key that will be used to encrypt a single frame:
    1. First a 4-byte <mark>CRC value</mark> is computed for the data payload
    2. The payload and the four CRC bytes are then encrypted using the RC4 stream cipher:XOR-ing the ith byte of data, $d_i$ , with the ith key $K_i^{IV}$ to produce the ith byte of ciphertext, $c_i$ :
    $$ ci=di \oplus k_i^{IV} $$

    3. The receiver takes the secret 40-bit symmetric key that it shares with the sender, appends the IV, and uses the resulting 64-bit key (which is identical to the key used by the sender to perform encryption) to <mark>decrypt</mark> the frame:
    $$ di=ci \oplus k_i^{IV} $$
![wep_protocol](/images/computer_networking_topdown/wep_protocol.png)



- Firewalls can be classified in three categories: <mark>traditional packet filters</mark>, <mark>stateful filters</mark>, and <mark>application gateways</mark>:
    1. Traditional Packet Filters:A traditional packet filter examines each datagram <mark>in isolation</mark>, determining whether the datagram should be allowed to pass or should be dropped based on package structure.
    2. Stateful filters actually track TCP connections, and use this knowledge to make ­filtering decisions:
        - Create a <mark>connection table</mark> to track  <mark>all ongoing TCP connections</mark>.(This is possible because the firewall can observe the beginning of a new connection by observing a three-way handshake (SYN, SYNACK, and ACK); and it can observe the end of a connection when it sees a FIN packet for the connection. )
        - the stateful filter includes a new column, <mark>“check connection”</mark> in its access control list to indicate that such connection should be <mark>checked by connection table</mark>.
        - When a user  sends a TCP SYN segment, the user’s TCP connection gets recorded in the connection table
        - On receiving a TCP packet, the firewall checks the connection table to see if this packet is part of an ongoing TCP connection, to decide whether to reject or accept the packet.
    3. Application Gateway: An application gateway is an application-specific server through which specific application data  must pass.Such a policy can be accomplished by implementing a combination of a packet filter (in a router) and a application gateway server:
        -  A filter configuration forces all outbound connections concernd with specific application to pass through the application gateway.
        - Consider an internal user wants to use the application to connect to the outside world. The user must first <mark>set up a  session with the application gateway</mark>.
        - An application running in the gateway, which listens for incoming sessions, prompts the user for a <mark>user ID and password</mark>.
        - When the user supplies this information, the application gateway checks to see if the user has permission . 
            - If not, the  connection from the internal user to the gateway is <mark>terminated</mark> by the gateway.
            - If the user has permission, then the gateway acts as a <mark>proxy server</mark> to relay messages between the user and the external host.

- Deep packet inspection:look beyond the header fields and into the actual <mark>application data</mark> that the packets carry.


- A device that generates alerts when it observes potentially malicious traffic is called an <mark>intrusion detection system (IDS)</mark>

- IDS systems are broadly classified as either <mark>signature-based systems</mark> or <mark>­anomaly-based systems</mark>:
    1. A signature-based IDS <mark>sniffs</mark> every packet passing by it, comparing each sniffed packet with the signatures in its database. If a packet (or series of packets) matches a signature in the database, the IDS generates an alert.
    2. An anomaly-based IDS creates a traffic profile as it observes traffic in normal operation. It then looks for packet streams that are <mark>statistically unusual</mark>







