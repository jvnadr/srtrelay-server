<p>We then want to update and upgrade our linux distribution using the following commands</p>

<pre>
<span style="font-family:Courier New,Courier,monospace">apt-get update
apt-get dist-upgrade</span></pre>

<p>Now that is done, we want to install the dependencies for our relays.</p>

<pre>
<span style="font-family:Courier New,Courier,monospace">apt-get install nano build-essential git tcl libssl1.0-dev nodejs npm usb-modeswitch libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev cmake joe screen</span></pre>

<p>&nbsp;</p>

<hr />
<p><strong>BE SURE TO CLEAR IP TABLES</strong></p>

<p>Check the firewall routes.</p>

<pre>
<span style="font-family:Courier New,Courier,monospace">iptables -L -n</span></pre>

<p>Create script to clear our existing IP routes. This will set all the policies to accept, clears out the table and the firewalls.</p>

<pre>
sudo nano iptables-clear.sh</pre>

<p>In this script enter the following data:</p>

<pre>
<span style="font-family:Courier New,Courier,monospace">#!/bin/bash
iptables-save &gt; iptables.backup
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -F
iptables --flush</span></pre>

<p>We will provide executable rights to this script and run it using the following commands:</p>

<pre>
<span style="font-family:Courier New,Courier,monospace">chmod +x iptables-clear.sh
./iptables-clear.sh</span></pre>

<p>Next when we check the IP tables, they will be clear and all the policies are set to accept.</p>

<pre>
<span style="font-family:Courier New,Courier,monospace">iptables -L -n</span></pre>

<hr />
<p>&nbsp;</p>

<h1>Building an SRT Relay</h1>

<p>&nbsp;</p>

<p>Build the SRT relay:</p>

<pre>
<span style="font-family:Courier New,Courier,monospace">git clone https://github.com/jvnadr/srtrelay-server.git
cd srt
./configure
make</span></pre>

<p>&nbsp;</p>

<p>Setup an SRT relay script which we will then run when we want to stream SRT.</p>

<p><span style="white-space:pre-wrap">Create a new shell script</span></p>

<pre>

<span style="font-family:Courier New,Courier,monospace">sudo nano srt-relay.sh </span>
</pre>

<p>&nbsp;</p>

<p>this will create a blank script file. In this script file we will enter our script contents</p>

<pre>

<span style="font-family:Courier New,Courier,monospace">#!/bin/bash
/home/ubuntu/srt/srt-live-transmit -st:yes &quot;srt://0.0.0.0:5005?mode=listener&amp;lossmaxttl=40&amp;latency=2000&quot; &quot;srt://0.0.0.0:5006?mode=listener&quot; 1&gt; /home/ubuntu/srt-output1.log 2&gt; /home/ubuntu/srt-error1.log &amp; </span></pre>

<p>&nbsp;</p>

<p>This script starts SRT live transmit. It listens on port 5005 for the incoming singal from your phone or encoder and listeners on port 5006 for OBS. It them pipes any output error log into a file.</p>

<p>We must make the srt-relay.sh script an executable for it to run on the instance. for this we run:</p>

<pre>

<span style="font-family:Courier New,Courier,monospace">chmod +x srt-relay.sh #make file executable
ls #check directory for the file
./srt-relay.sh #this will start the SRT relay</span>
</pre>

<p>&nbsp;</p>

<p>Next we want the SRT relay to send the video data to a destination for further encoding or viewing.</p>

<p>&nbsp;</p>
