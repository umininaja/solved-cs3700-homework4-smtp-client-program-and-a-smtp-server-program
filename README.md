Download Link: https://assignmentchef.com/product/solved-cs3700-homework4-smtp-client-program-and-a-smtp-server-program
<br>
<strong>Part I : </strong>Write a <strong><em>SMTP client program</em></strong> and a <strong><em>SMTP server program</em></strong> to implement the following simplified SMTP protocol based on TCP service. Please make sure your program supports multiple clients. You must use the port assigned to you and you may hard code it in both client and server programs.

<ul>

 <li>“<strong>Telnet &lt;your server’s ip address&gt; &lt;port&gt;</strong>” can be used to test your SMTP server program first (especially those “503” responses), then your SMTP client can be tested using your SMTP server program.</li>

 <li><strong>SMTP Client Program</strong> (NOT a TELNET client!!!):

  <ol>

   <li>Display a message to ask the user to input the Host Name (or ip-address) of your SMTP server.</li>

   <li>Buildup the TCP connection to your SMTP server with the Host Name input by User at the given port. Catch the exception, terminate the program, and display error messages on the standard output if any. Wait for, read, and display the “220” response from the SMTP server.</li>

   <li>Display prompt messages on the standard output to ask the user to input sender’s email address, receiver’s email address, subject, and email contents, respectively. Since there may be multiple lines in email contents, the prompt message displayed by your Client program MUST prompt the ending signature pattern like “.” on a line by itself.</li>

   <li>Use the user inputs collected above in Step 3 for the following 3-phase data transfer procedure (see step 3 on server side). In each of the following steps a. through e., display the <strong>RTT (round-trip-time)</strong> of each conversation in millisecond (e.g., RTT = 212.08 ms).

    <ol>

     <li>Send the “HELO &lt;sender’s mail server domain name&gt;” command (e.g., HELO xyz.com) to the SMTP server program, wait for server’s response and display it on the standard output.</li>

     <li>Send the “MAIL FROM: &lt;sender’s email address&gt;” command to SMTP server, wait for SMTP server’s response and display it on the standard output.</li>

     <li>Send the “RCPT TO: &lt;receiver’s email address&gt;” command to the SMTP server program, wait for SMTP server’s response and display it on the standard output.</li>

     <li>Send the “DATA” command to the SMTP server program, wait for SMTP server’s response and display it on the standard output.</li>

     <li>Send the Mail message to the SMTP server. The format of this Mail message MUST follow the format detailed on the <strong>slide titled “Mail message format”</strong>. Wait for SMTP server’s response and display it on the standard output.</li>

    </ol></li>

   <li>Display a prompt message to ask the User whether to continue. If yes, repeat steps 3 through 5. Otherwise, send a “QUIT” command to the SMTP server, display SMTP Server’s response, close TCP connection, and terminate the Client program.</li>

  </ol></li>

 <li><strong>SMTP Server Program</strong>: (server’s ip or client’s ip can be its dns name below.) 1. Listen to the given port and wait for a connection request from a SMTP Client.

  <ol start="2">

   <li>Create a new thread for every incoming TCP connection request from a SMTP client. Send the “220” response including server’s ip address or dns name to the SMTP client.</li>

   <li>Implement the following 3-phase data transfer procedure (see step 4 on client side):

    <ol start="5">

     <li>Wait for, read, and display the “HELO …” command from the SMTP client. If the incoming command is NOT “HELO …”, sends “503 5.5.2 Send hello first” response to the SMTP client and repeat step 3.a.</li>

     <li>Send the “250 &lt;server’s ip&gt; Hello &lt;client’s ip&gt;” response to the SMTP client.</li>

    </ol></li>

  </ol></li>

</ul>

<ol start="5">

 <li>Wait for, read, and display the “MAIL FROM: …” command from the SMTP client. If the incoming command is NOT “MAIL FROM: …”, sends “503 5.5.2 Need mail command” response to the SMTP client and repeat step 3.c.</li>

 <li>Send the “250 2.1.0 Sender OK” response to the SMTP client.</li>

 <li>Wait for, read, and display the “RCPT TO: …” command from the SMTP client. If the incoming command is NOT “RCPT TO: …”, send “503 5.5.2 Need rcpt command” response to the SMTP client and repeat step 3.e.</li>

 <li>Send the “250 2.1.5 Recipient OK” response to the SMTP client.</li>

 <li>Wait for, read, and display the “DATA” command from the SMTP client. If the incoming command is NOT “DATA”, send “503 5.5.2 Need data command” response to the SMTP client and repeat step 3.g.</li>

 <li>Send the “354 Start mail input; end with &lt;CRLF&gt;.&lt;CRLF&gt;” response to the SMTP client.</li>

 <li>Wait for, read, and display the Mail message from the SMTP client line by line. (hint: “.” is the ending signature.)</li>

 <li>Send the “250 Message received and to be delivered” response to the SMTP client.</li>

</ol>

<ol start="4">

 <li>Repeat Step 3 until the “QUIT” command is read. Upon receiving “QUIT”, send the “221 &lt;server’s ip&gt; closing connection” response to the SMTP client and go to Step 5.</li>

 <li>Close all i/o streams and the TCP socket for THIS Client, and terminate the thread for THIS client.</li>

</ol>

<strong> </strong>

<strong>Part II: Test your programs on the Virtual Servers in the cloud and your laptop/home computer. </strong>

<strong>Warning</strong>: to complete this part, especially when you work at home, you must first (1) <strong>connect to GlobalProtect </strong>using your NetID account (please read “<strong>how to connect to GlobalProtect …</strong>” at <u>https://msudenver.edu/vpn/</u>); then (2) <strong>connect to the virtual servers cs3700a and cs3700b</strong> using <strong><em>sftp</em></strong> and <strong><em>ssh</em></strong> command on MAC/Linux or <strong><em>PUTTY</em></strong> and <strong><em>PSFTP</em></strong> on Windows.




<table width="720">

 <tbody>

  <tr>

   <td colspan="2" width="720">ITS only supports GlobalProtect on MAC and Windows machines.  If your home computer has a different OS, it is your responsibility to figure out how to connect to cs3700a and cs3700b for programming assignments and submit your work by the cutoff deadline.  Such</td>

  </tr>

  <tr>

   <td width="320">issues cannot be used as an excuse to request any extension.</td>

   <td width="400"><strong> </strong></td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<ol>

 <li>MAKE a directory “<strong>HW4</strong>” under your home directory on <strong>cs3700a</strong>.msdenver.edu and <strong>cs3700b</strong>.msudenver.edu, a subdirectory “<strong>server</strong>” under “<strong>HW4</strong>” on <strong>msudenver.edu</strong>, and a subdirectory “<strong>client</strong>” under “<strong>HW4</strong>” on <strong>cs3700b.msudenver.edu</strong>.</li>

 <li>UPLOAD and COMPILE the <strong><em>server</em></strong> program under “<strong>HW4/server</strong>” and the <strong><em>client</em></strong> program under “<strong>HW4/client</strong>” on the VMs.</li>

 <li>TEST <strong><em>the</em></strong> <strong><em>server program</em></strong> running on <strong>cs3700a</strong>.msudenver.edu together with <strong><em>a client program</em></strong> running on your laptop or lab computer and <strong><em>another client program</em></strong>, simultaneously, running on <strong>cs3700b</strong>.msudenver.edu to test all the possible cases.</li>

 <li>SAVE a file named <strong><em>txt</em></strong> under “<strong>HW4/client</strong>” on <strong>cs3700b</strong>.msudenver.edu, which captures the outputs of your <strong><em>client</em></strong> program when you test it. You can use the following command to redirect the standard output (stdout) and the standard error (stderr) to a <strong>file</strong> on UNIX, Linux, or Mac, and view the contents of the file</li>

</ol>

<strong>java prog_name_args | tee testResultsClient.txt //copy stdout to the .txt file  //if you want, you may also use “script” command instead of the “tee” command </strong>

<strong>     //to write both stdin and stdout into testResultsClient.txt while testing your </strong>

<strong>      //client program on cs3700a.  For how to use “script”, see  </strong>

<strong> //</strong> <strong><u>https://www.geeksforgeeks.org/script-command-in-linux-with-examples/</u></strong><strong>  //or Google “script command in Linux” if the above link is broken. </strong>

<strong>cat file-name     //display the file’s contents.    </strong>