Download Link: https://assignmentchef.com/product/solved-cs69012-assignment3-file-transfer-protocol-design
<br>
In this assignment you need to implement file transfer protocol on top of TCP sockets.  There will be a server and multiple clients communicating with the server. Each client process will open a new connection with the server. Use select to handle multiple client requests.

FTP Commands and there functionality

<ol>

 <li>RETR : This command causes the remote host to initiate a data connection and to send the requested file over the data connection.</li>

 <li>STOR : This command causes to store a file into the current directory of the remote host.</li>

 <li>LIST : Sends a request to display the list of all files present in the directory.</li>

 <li>ABOR : This command tells the server to abort the previous FTP service command and any associated transfer of data.</li>

 <li>QUIT : This command terminates a USER and if file transfer is not in progress , the server closes the control connection.</li>

 <li>DELE : This command deletes a file in the current directory of server.</li>

</ol>




<h2>Problem</h2>




Write two separate C programs one for TCP server (handles requests from multiple servers) and one for client.

Your server program will use the SELECT system call to handle multiple clients. Multiple clients should be simultaneously able to communicate with the server.

You need to implement file transfer protocol between server and client. You should assume the files data structure to be ‘FILE STRUCTURE’ (i.e. file as a contiguous stream of bytes without internal structure). You may have a single process to handle both control and data communication, at server and client.




Working of server and client is as follows:

<ol>

 <li>Server accepts connections from clients.</li>

 <li>Server receives control information like FTP commands over this connection.</li>

 <li>Server checks for valid commands, and executes them if there is no error.</li>

 <li>Server creates a new data connection with the client for sending data information.</li>

</ol>

Only one file can be sent over one data connection.

<ol start="5">

 <li>The same control connection remains active throughout the user session.</li>

 <li>Client receives the response and displays it to the user.</li>

</ol>




Implement the following ftp commands:

<ol>

 <li>RETR &lt;filename&gt;</li>

 <li>STOR &lt;filename&gt;</li>

 <li>LIST</li>

 <li>ABOR</li>

 <li>QUIT</li>

 <li>DELE &lt;filename&gt;</li>

</ol>

<strong> </strong>

<h2>Sample Scenario</h2>




<table width="624">

 <tbody>

  <tr>

   <td width="279">Server</td>

   <td width="169">Client 1</td>

   <td width="176">Client 2</td>

  </tr>

  <tr>

   <td width="279">./server 500</td>

   <td width="169"> </td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279">Server running</td>

   <td width="169"> </td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279"> </td>

   <td width="169">./client 127.0.0.1 500</td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279">Connected to client 1</td>

   <td width="169">Connected to server</td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279"> </td>

   <td width="169">LIST</td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279">LIST command received from client 1</td>

   <td width="169"> </td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279">Sending list of files to client 1</td>

   <td width="169">A.txt B.txt</td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279"> </td>

   <td width="169"> </td>

   <td width="176">./client 127.0.0.1 500</td>

  </tr>

  <tr>

   <td width="279">Connected to client 2</td>

   <td width="169"> </td>

   <td width="176">Connected to server</td>

  </tr>

  <tr>

   <td width="279"> </td>

   <td width="169"> </td>

   <td width="176">RETR A.txt</td>

  </tr>

  <tr>

   <td width="279">RETR command received from client 2</td>

   <td width="169"> </td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279">Sending file A.txt to client 2</td>

   <td width="169"> </td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279"> </td>

   <td width="169"> </td>

   <td width="176">Received file A.txt</td>

  </tr>

  <tr>

   <td width="279"> </td>

   <td width="169">QUIT</td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279">QUIT command received from client 1</td>

   <td width="169"> </td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279">Client 1 disconnected</td>

   <td width="169">Disconnected from server</td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279"> </td>

   <td width="169"> </td>

   <td width="176">QUIT</td>

  </tr>

  <tr>

   <td width="279">QUIT command received from client 2</td>

   <td width="169"> </td>

   <td width="176"> </td>

  </tr>

  <tr>

   <td width="279">Client 2 disconnected</td>

   <td width="169"> </td>

   <td width="176">Disconnected from</td>

  </tr>

  <tr>

   <td width="279"> </td>

   <td width="169"> </td>

   <td width="176">server</td>

  </tr>

 </tbody>

</table>

<strong> </strong>