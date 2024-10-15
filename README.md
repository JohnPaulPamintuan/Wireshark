<h1>Analyzing HTTP/S and RDP Traffic with Wireshark</h1> 

<h2>Project Description:</h2>
In this project, we use Wireshark to capture and analyze network traffic, focusing on HTTP/S (Hypertext Transfer Protocol/Secure) and RDP (Remote Desktop Protocol) traffic. The objective is to identify and dissect common web traffic, including both secure and insecure web communications, as well as monitor RDP sessions, which are often used for remote access to systems and can be a target for attacks.<br/>

<h2>Tools Used:</h2>

- <b>Wireshark</b>: A network protocol analyzer for capturing and inspecting traffic at a granular level.
- <b>Browser</b>(for HTTP/S traffic): Any web browser to generate traffic.
- <b>Remote Desktop Client</b> (for RDP traffic): Used to generate RDP traffic.

<h1>Step-by-Step Implementation</h1>

<h2><ins>1.HTTP Traffic Analysis</ins></h2>

- Begin capturing traffic in Wireshark by clicking the green Start Capture button after selecting the network interface.
- Open your browser and navigate to an HTTP website (e.g., http://example.com).
- top the capture once sufficient traffic is generated.
- Use the following filter in Wireshark to focus on HTTP traffic:
  <img src="https://i.imgur.com/Q99f0YI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h2><ins>2. Analyzing HTTP Traffic</ins></h2>

- Examine the HTTP GET and POST requests captured by Wireshark:
   - <b>GET</b>: Requests data from the server (e.g., retrieving a webpage).
   - <b>POST</b>: Submits data to the server (e.g., form submission).

       - <b><ins>Examples of HTTP Request:</ins><b/>
          - <b>*GET /index.html HTTP/1.1*</b>
          - <b>*Host<b>: example.com*</b>
          - <b>*User-Agent: Mozilla/5.0*</b>

        - <ins>Example HTTP Response:</ins>
          - <b>*HTTP/1.1 200 OK*</b>
          - <b>*Content-Type: text/htm*</b>

- Use the "Follow TCP Stream" feature to see the entire conversation between the client and server.
- Look at the HTTP request headers (e.g., User-Agent, Host, Accept) and response headers (e.g., Content-Type, Status Code).
- Identify if any sensitive data (e.g., usernames or passwords) is sent in plain text.
  - Example filter in Wireshark to capture HTTP requests:
   <img src="https://i.imgur.com/n4wsxXD.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>


<h2><ins>3. Capturing HTTPS Traffic</ins></h2>

- Start another capture and navigate to an HTTPS website (e.g., https://example.com)
- Stop the capture once sufficient traffic is generated.
- Filter for TLS traffic in Wireshark to examine HTTPS communication:
  <img src="https://i.imgur.com/n4wsxXD.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>




- <b>Other examples of Tcpdump Packet Filtering:</b>

	- <ins><b>*host*</b></ins> will filter visible traffic to show anything involving the designated host.

       <img src="https://i.imgur.com/oJHHKxN.png" height="130%" width="80%" alt="Disk Sanitization Steps"/>


  - <ins><b>*src and dest*</b></ins> are modifiers. We can use them to designate a source or destination host or port and <ins><b>*Utilizing Source With Port as a Filter.*</b></ins>

     <img src="https://i.imgur.com/RNkMYk3.png" height="130%" width="80%" alt="Disk Sanitization Steps"/>
     <img src="https://i.imgur.com/Q4cBh2I.png" height="130%" width="80%" alt="Disk Sanitization Steps"/>

   -  <ins><b>*proto*</b></ins> will filter for a specific protocol type. (ether, TCP, UDP, and ICMP as examples).
   -  <ins><b>*port*</b></ins> is bi-directional. It will show any traffic with the specified port as the source or destination.

       <img src="https://i.imgur.com/BnS36fc.png" height="130%" width="80%" alt="Disk Sanitization Steps"/>
       <img src="https://i.imgur.com/thajDeo.png" height="130%" width="80%" alt="Disk Sanitization Steps"/>
       <img src="https://i.imgur.com/7jrsoKr.png" height="130%" width="80%" alt="Disk Sanitization Steps"/>
       
       

   - <ins><b>*less and greater*</b></ins> can be used to look for a packet or protocol option of a specific size.

     <img src="https://i.imgur.com/IKaTf8g.png" height="130%" width="80%" alt="Disk Sanitization Steps"/>
     <img src="https://i.imgur.com/HYcVD9Y.png" height="130%" width="80%" alt="Disk Sanitization Steps"/>
     
     

   - <ins><b>*and &&*</b></ins> can be used to concatenate two different filters together. for example, src host AND port.
   - <ins><b>*or*</b></ins> allows for a match on either of two conditions. It does not have to meet both. It can be tricky.
   - <ins><b>*not*</b></ins> is a modifier saying anything but x. For example, not UDP.

     <img src="https://i.imgur.com/JcgsKpC.png" height="130%" width="80%" alt="Disk Sanitization Steps"/>
     <img src="https://i.imgur.com/m6fMmrg.png" height="130%" width="80%" alt="Disk Sanitization Steps"/>
     <img src="https://i.imgur.com/WBrtF35.png" height="130%" width="80%" alt="Disk Sanitization Steps"/>

  
<h2><ins>3. Basic Analysis with TCPdump</ins></h2>

- After capturing the traffic, use TCPdump to analyze specific packets directly from the terminal.
- View the contents of the <b>.pcap</b> file:
  
   <img src="https://i.imgur.com/D5P15oy.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
- To filter for TCP packets with the SYN flag set (indicating new connection attempts):
   <img src="https://i.imgur.com/ixoWbwR.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
- To see all packets with the FIN flag (indicating connection terminations):
   <img src="https://i.imgur.com/yfg94fA.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>

<h2><ins>4. Inspecting TCP Three-Way Handshake</ins></h2>

- Identify the TCP three-way handshake in the captured data by filtering for packets with the SYN, SYN-ACK, and ACK flags.
- The three-step process looks like:
  - SYN from the client to initiate a connection.
  - SYN-ACK from the server to acknowledge the request.
  - ACK from the client to establish the connection.
 
- Example filter to capture this sequence:

 <img src="https://i.imgur.com/jhwYuR9.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
