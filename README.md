<h1>Analyzing HTTP/S and RDP Traffic with Wireshark</h1> 

<h2>Project Description:</h2>
In this project, we use Wireshark to capture and analyze network traffic, focusing on HTTP/S (Hypertext Transfer Protocol/Secure) and RDP (Remote Desktop Protocol) traffic. The objective is to identify and dissect common web traffic, including both secure and insecure web communications, as well as monitor RDP sessions, which are often used for remote access to systems and can be a target for attacks.<br/>

<h2>Tools Used:</h2>

- <b>Wireshark</b>: A network protocol analyzer for capturing and inspecting traffic at a granular level.
- <b>Browser</b>(for HTTP/S traffic): Any web browser to generate traffic.
- <b>Remote Desktop Client</b> (for RDP traffic): Used to generate RDP traffic.

<h1>Step-by-Step Implementation</h1>

<h2><ins>1.HTTP Traffic Analysis</ins></h2>



[linkedin]: https://linkedin.com/in/johnpaulpamintuan/</br>
- Begin capturing traffic in Wireshark by clicking the blue Start Capture button </br><img width="22px" src="https://www.pngkit.com/png/detail/365-3657626_wireshark-icon.png"/> after selecting the network interface.
- Open your browser and navigate to an HTTP website (e.g., http://example.com).
- top the capture once sufficient traffic is generated.
- Use the following filter in Wireshark to focus on HTTP traffic:

  <img src="https://i.imgur.com/7oKwmUF.png" height="70%" width="80%" alt="Disk Sanitization Steps"/>

  <img src="https://imgur.com/NNATNjH.png" height="70%" width="80%" alt="Disk Sanitization Steps"/>

  <img src="https://imgur.com/KvOh3Zd.png" height="70%" width="80%" alt="Disk Sanitization Steps"/>
  

<h3>Analyzing HTTP Traffic</h3>

- Examine the HTTP GET and POST requests captured by Wireshark:
  - <b>GET</b>: Requests data from the server (e.g., retrieving a webpage).
  - <b>POST</b>: Submits data to the server (e.g., form submission). 
    - <ins>Examples of HTTP Request:</ins>
    	- <b>*GET</b> /index.html HTTP/1.1*
     	- <b>*Host</b>: example.com*
      	- <b>*User-Agent</b>: Mozilla/5.0*
       
    - <ins>Example HTTP Response:</ins>
	- <b>*HTTP/1.1 200 OK*</b>
 	- <b>*Content-Type</b>: text/htm*
    

  

- Use the <ins>"Follow TCP or HTTP Stream"</ins> feature to see the entire conversation between the client and server.
- Identify if any sensitive data (e.g., usernames or passwords) is sent in <ins>plain text</ins>.
- Look at <ins>the HTTP request headers</ins> (e.g., User-Agent, Host, Accept) and response headers (e.g., Content-Type, Status Code).
  - Example filter in Wireshark to capture HTTP requests:
    <img src="https://i.imgur.com/SLZRSPI.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
    <img src="https://i.imgur.com/kacqKSc.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
    <img src="https://i.imgur.com/3AJSspn.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
    
<h2><ins>2. Capturing HTTPS Traffic</ins></h2>

- Start another capture and navigate to an HTTPS website (e.g., https://msn.com)
- Stop the capture once sufficient traffic is generated.
- Filter for TLS traffic in Wireshark to examine HTTPS communication:
  <img src="https://i.imgur.com/NkChUBo.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
  <img src="https://i.imgur.com/BQeVwnH.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
  

<h3>Analyzing HTTPS Traffic</h3>

- While HTTPS encrypts the content, you can still analyze the TLS handshake process in Wireshark, which involves:
  - <b>Client Hello</b>: Client initiates the connection and proposes cryptographic options.
  - <b>Server Hello</b>: Server agrees to certain cryptographic options and sends a digital certificate.
  - <b>Key Exchange</b>: The client and server securely exchange keys to encrypt the session.
- Use Wireshark's <ins>"Follow TLS or TCP Stream"</ins> feature to view the initial handshake, which remains unencrypted.
- Example filter to find <ins>the TLS handshake</ins>:
   
   <img src="https://i.imgur.com/WM70aUy.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
   <img src="https://i.imgur.com/JcP1HGN.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
   <img src="https://i.imgur.com/ARjLhKg.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>

<h2><ins>3. Guided Lab: Decrypting RDP connections  </ins></h2>
<h2>Project Description:</h2>
In this lab, I'll be working with <b> Remote Desktop Protocol RDP</b> traffic. RDP is a protocol used for remotely connecting to Windows systems, i learn how to decrypt and analyze RDP traffic. If one has the required key utilized between the two hosts for encrypting the traffic and Wireshark can deobfuscate the traffic for us.<br/>

<h2>Resoruce:</h2>

- <b>RDP analysis zip file from Hack the box.
- Private Key: To decrypt RDP traffic.</b>

<h2>Program walk-through::</h2>

1. <b>Open the rdp.pcapng file in Wireshark</b>: Unzip the zip file included in the optional resources and open it in Wireshark.
	<img src="https://i.imgur.com/daUQVWn.png" height="100%" width="85%" alt="Disk Sanitization Steps"/>
	<img src="https://i.imgur.com/eT1gjLe.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
2. <b>Analyze the traffic included</b> Take a minute to look at the traffic. Notice there is a lot of information here. We know our focus is on RDP, so let's take a second to filter on rdp and see what it returns. 
	<img src="https://i.imgur.com/rJ0cXKP.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
	  - As it stands, not much can be seen, right? This is because RDP, by default, is utilizing TLS to encrypt the data, so we will not be able to see anything that happened with RDP traffic. How can we verify its existence in this file? One way is to filter on the well-known port RDP uses typically.

3. <b>Filter on port 3389 to determine if any RDP traffic encrypted or otherwise exists.</b>
 	<img src="https://i.imgur.com/DsruLla.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
	- We can at least verify that a session was established between the two hosts over TCP port 3389.

4. <b>Provide the RDP-key to Wireshark so it can decrypt the traffic.</b>

   - <ins>To apply the key in Wireshark:</ins>
  	 - go to Edit → Preferences → Protocols → TLS
  	 - On the TLS page, select Edit by RSA keys list → a new window will open.
   	 - Import An RDP Key
   
   	<img src="https://i.imgur.com/rk6SmnW.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
 	<img src="https://i.imgur.com/jnH0DcK.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
  	<img src="https://i.imgur.com/sEBY27y.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
  
5. When filtering once again on RDP, we should see some traffic in the display. <b>RDP In The Clear</b>:
	<img src="https://i.imgur.com/eK97jQw.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
	
   - From here, we can perform an <b>analysis of the RDP traffic</b>. We can now <ins>follow TCP streams</ins>, export any potential objects found, and anything else we feel necessary for our investigation. This works because we acquired the RSA key used for encrypting the RDP session.  
	<img src="https://i.imgur.com/FjYqKWE.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>

<h2>Analysis:</h2>

- The first packet of the three-way handshake, we can see the host who initiated the connection is 10.129.43.27. Which user account was used to initiate the RDP connection?
- When filter on tcp.port == 3389, we can see a record labeled Ignored Unknown Record. If we examine the ASCII, it will show us a username.

	<img src="https://i.imgur.com/T65Xojz.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>

<h2>Summary:</h2>

- This lab was to serve as an example of what Wireshark can do with captured data and its plugins. Wireshark's capability to ingest information and illuminate the obscure is robust. Having the ability to decrypt data after ingestion is a powerful capability. This concept could be applied to any protocol that utilizes encryption as long as we have the key that will be utilized to establish the connections.
