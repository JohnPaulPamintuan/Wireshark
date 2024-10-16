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
  

<h2><ins>2. Analyzing HTTP Traffic</ins></h2>

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
    
<h2><ins>3. Capturing HTTPS Traffic</ins></h2>

- Start another capture and navigate to an HTTPS website (e.g., https://msn.com)
- Stop the capture once sufficient traffic is generated.
- Filter for TLS traffic in Wireshark to examine HTTPS communication:
  <img src="https://i.imgur.com/NkChUBo.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
  <img src="https://i.imgur.com/BQeVwnH.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
  

<h2><ins>4.Analyzing HTTPS Traffic</ins></h2>

- While HTTPS encrypts the content, you can still analyze the TLS handshake process in Wireshark, which involves:
  - <b>Client Hello</b>: Client initiates the connection and proposes cryptographic options.
  - <b>Server Hello</b>: Server agrees to certain cryptographic options and sends a digital certificate.
  - <b>Key Exchange</b>: The client and server securely exchange keys to encrypt the session.
- Use Wireshark's <ins>"Follow TLS or TCP Stream"</ins> feature to view the initial handshake, which remains unencrypted.
- Example filter to find <ins>the TLS handshake</ins>:
   
   <img src="https://i.imgur.com/WM70aUy.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
   <img src="https://i.imgur.com/JcP1HGN.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
   <img src="https://i.imgur.com/ARjLhKg.png" height="120%" width="85%" alt="Disk Sanitization Steps"/>
  
