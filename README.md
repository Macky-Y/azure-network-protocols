<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>READ ME BEFORE STARTING</h2>

<p>
This will not include a tutorial on creating a VM in Azure since I already created a tutorial in the previous repositories, refer to my previous repositories if you want to learn how to create VMs. This will only focus on Azure Network Protocols and observe Network Traffic ✌️. Before we start this lab, make sure you create 2 VMs, one for windows and one for ubuntu.
</p>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (2 Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Steps to do before Analyzing and Observing Network Traffic</h2>

<p>
1. First, remote login to Windows VM and follow these steps to download and install wireshark. We will use wireshark to analyze and observe traffic in the network.
</p>

<p>
2. Open your browser and go to <ins>google.com</ins> and search for <ins>wireshark download</ins>. Click the first link.
</p>

<p>
<img src="https://i.imgur.com/H3h0WPY.png" height="80%" width="80%" />
</p>

<p>
3. Click <ins>Windows Installer (64-bit)</ins> to download the file.
</p>

<p>
<img src="https://i.imgur.com/Qda9qYT.png" height="80%" width="80%" />
</p>

<p>
4. Open the downloaded wireshark file to install it. Click <ins>Next</ins>.
</p>

<p>
<img src="https://i.imgur.com/Kb5sbmZ.png" height="80%" width="80%" />
</p>

<p>
5. Click <ins>Noted</ins>.
</p>

<p>
<img src="https://i.imgur.com/XbxIxH2.png" height="80%" width="80%" />
</p>

<p>
6. Click <ins>Next</ins> in the following prompt.
</p>

<p>
<img src="https://i.imgur.com/h7B6Tch.png" height="80%" width="80%" />
</p>

<p>
<img src="https://i.imgur.com/RfLwOcZ.png" height="80%" width="80%" />
</p>

<p>
<img src="https://i.imgur.com/xk7NahX.png" height="80%" width="80%" />
</p>

<p>
<img src="https://i.imgur.com/uaQ1qNg.png" height="80%" width="80%" />
</p>

<p>
<img src="https://i.imgur.com/kJNPW7c.png" height="80%" width="80%" />
</p>

<p>
7. Click <ins>Install</ins>.
</p>

<p>
<img src="https://i.imgur.com/bccHxnV.png" height="80%" width="80%" />
</p>

<p>
8. Click <ins>I Agree</ins>.
</p>

<p>
<img src="https://i.imgur.com/y1M5QHy.png" height="80%" width="80%" />
</p>

<p>
9. Click <ins>Install</ins>.
</p>

<p>
<img src="https://i.imgur.com/2D9Yz2F.png" height="80%" width="80%" />
</p>

<p>
10. Click <ins>Next</ins>.
</p>

<p>
<img src="https://i.imgur.com/vsn2X1C.png" height="80%" width="80%" />
</p>

<p>
11. Click <ins>Finish</ins> in this last 2 prompts.
</p>

<p>
<img src="https://i.imgur.com/Ku8H1YK.png" height="80%" width="80%" />
</p>

<p>
<img src="https://i.imgur.com/7PoUJ7b.png" height="80%" width="80%" />
</p>

<p>
12. Now open <ins>Wireshark</ins>. You will be see this page. Follow the steps in the picture.
</p>

<p>
<img src="https://i.imgur.com/GVZFPJ3.png" height="80%" width="80%" />
</p>

<p>
13. You will now see this screen.
</p>

<p>
<img src="https://i.imgur.com/eL4DXRA.png" height="80%" width="80%" />
</p>


<h2>Actions and Observations</h2>

<p>
1. Filter By ICMP
</p>

- You will notice that there are a lot of traffics showing in our network, let's filter it so we can only observe ICMP. Do these steps to filter the traffic.

<p>
<img src="https://i.imgur.com/R2NlOUH.png" height="80%" width="80%" />
</p>
  
- You will notice that all the traffics are filtered and there are not traffics showing in wireshark.
- Now we will navigate to <ins>portal.azure.com</ins> and find VM2's private IP address and ping it to observe the ICMP traffic. Ping is a command used to test network connection.
- Click VM2.

<p>
<img src="https://i.imgur.com/CDAbFCy.png" height="80%" width="80%" />
</p>

- Copy the <ins>Private IP Address</ins>. We will ping this IP Address.

<p>
<img src="https://i.imgur.com/wjAbmWN.png" height="80%" width="80%" />
</p>

- Open Windows PowerShell and ping VM2's Private IP Address.

<p>
<img src="https://i.imgur.com/aYeZ7Z2.png" height="80%" width="80%" />
</p>

- As you probably noticed, wireshark detected ICMP traffic after we ping the Private IP Address of VM2.
- Now our Wireshark looks like this, VM1 is sending request to VM2, VM2 is replying to VM1's request, meaning our network is working since both of them are communicating.

<p>
<img src="https://i.imgur.com/caw437R.png" height="80%" width="80%" />
</p>

- Now let's ping VM2 continuously using the <ins>-t</ins> command and let's observe what Microsoft Azure's NSG does when we block ICMP traffic.

<p>
<img src="https://i.imgur.com/Tk85Jr8.png" height="80%" width="80%" />
</p>

- Follow these steps to block ICMP traffic in VM2.

<p>
<img src="https://i.imgur.com/gs8SZ3d.png" height="80%" width="80%" />
</p>

- Select VM2-nsg.

<p>
<img src="https://i.imgur.com/axwwWVc.png" height="80%" width="80%" />
</p>

<p>
<img src="https://i.imgur.com/SPi7WW8.png" height="80%" width="80%" />
</p>

<p>
<img src="https://i.imgur.com/iiqZFCH.png" height="80%" width="80%" />
</p>

- You might be wondering why we chose 200 as the Priority, we can choose any number as long as it goes before 300 since ssh's priority is set to 300 and we don't want ssh to bypass our ICMP blocking rule.
- Now we go back to our VM1 and check the ping status.
- As you can see, it says request timed out, meaning VM2-nsg is blocking ICMP traffic. NSG acts like a firewall, it controls and monitors outgoing and incoming traffics. Look at our wireshark also, it only says request since VM2 is not replying due to blocking of ICMP.

<p>
<img src="https://i.imgur.com/bEdVN0P.png" height="80%" width="80%" />
</p>

<p>
<img src="https://i.imgur.com/T6QRPrR.png" height="80%" width="80%" />
</p>

- Now let's allow ICMP traffic again to VM2-nsg and observe what will happen. Follow these steps to enable ICMP traffic.

<p>
<img src="https://i.imgur.com/XJ0CfJX.png" height="80%" width="80%" />
</p>

<p>
<img src="https://i.imgur.com/Dp6Lf9M.png" height="80%" width="80%" />
</p>

- Now let's go back to our VM1 and observe our ping and wireshark.
- You will see that VM2 is replying again to VM1's request.

<p>
<img src="https://i.imgur.com/wG24prx.png" height="80%" width="80%" />
</p>

<p>
<img src="https://i.imgur.com/HJ8tHci.png" height="80%" width="80%" />
</p>

- Go back to PowerShell and press Ctrl+C to end continuous ping.

<p>
2. Filter By SSH
</p>

- Now we will observe and analyze traffic in SSH.
- Filter Wireshark to SSH only.

<p>
<img src="https://i.imgur.com/6RaZBMY.png" height="80%" width="80%" />
</p>

- Open PowerShell again and let's SSH to VM2 using private IP Address.

<p>
<img src="https://i.imgur.com/yV5z3Qr.png" height="80%" width="80%" />
</p>

- Notice after hitting <ins>Enter</ins> in our PowerShell Command, Wireshark detected a traffic in SSH.

<p>
<img src="https://i.imgur.com/kAbvBIW.png" height="80%" width="80%" />
</p>

- Type <ins>Yes</ins> and hit Enter.

<p>
<img src="https://i.imgur.com/6mn3ope.png" height="80%" width="80%" />
</p>

- After we hit Enter, Wireshark detected more traffic in SSH. The PowerShell tells us that we are connected to VM2 via SSH.

<p>
<img src="https://i.imgur.com/EIVAy52.png" height="80%" width="80%" />
</p>

- These are all the traffics that Wireshark detected.

<p>
<img src="https://i.imgur.com/2Mr8GWU.png" height="80%" width="80%" />
</p>

- More traffic will be detected once we used some of the terminal commands in the SSH.

<p>
<img src="https://i.imgur.com/tmBkR2y.png" height="80%" width="80%" />
</p>

<p>
<img src="https://i.imgur.com/bTJ1zdH.png" height="80%" width="80%" />
</p>

<p>
3. Filter by DHCP
</p>

- Type <ins>exit</ins> in PowerShell to exit in SSH.
- Filter wireshark to DHCP.
- We will renew our IP and observe Wireshark.

<p>
<img src="https://i.imgur.com/Wo9DTGr.png" height="80%" width="80%" />
</p>

- Press Enter.
- We were expecting to see a broadcast address since we renewed our IP Address but in this case it automatically gave us an IP Address. DHCP is a protocol that assigns you a new IP Address automatically.
- As you probably guessed, Wireshark will detect a DHCP traffic after we pressed Enter key.

<p>
<img src="https://i.imgur.com/wmhVBHp.png" height="80%" width="80%" />
</p>



<p>
3. Filter by DNS
</p>

- Now let's filter by DNS. Set the filter to DNS in wireshark. DNS is an IP Address converted to readable format for humans since it is easier to memorize Domain Names rather than IP Addresses.
- Open PowerShell and we will use <ins>nslookup</ins> command to observe DNS traffic in wireshark.
- Press Enter.

<p>
<img src="https://i.imgur.com/5nXL70d.png" height="80%" width="80%" />
</p>

- PowerShell gave us the IP Address of google.

<p>
<img src="https://i.imgur.com/9UCkfHk.png" height="80%" width="80%" />
</p>

- Observing the traffic at wireshark, it gave us a lot of traffic and all of these traffic are being used by google and our network which were detected by Wireshark.

<p>
<img src="https://i.imgur.com/57i8Ipr.png" height="80%" width="80%" />
</p>

<p>
4. Filter by RDP
</p>

- Now for our final observation, we will filter Wireshark to RDP or Remote Desktop Protocol, it uses port 3389 so we will use <ins>tcp.port == 3389</ins> to filter RDP traffic only.
- Once we filter Wireshark to RDP, Wireshark is showing a lot of traffics and constantly updating since we are using a VM, every keystroke, mouse movement is also transmitting in the traffic.

<p>
<img src="https://i.imgur.com/8qqrh1r.png" height="80%" width="80%" />
</p>

<h4>This concludes the observation and analysis of network traffic, I hope you learned something new ☺️</h4>
