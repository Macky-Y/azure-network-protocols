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

- Press Ctrl+C to end continuous ping.

<p>
2. Filter By SSH
</p>













<p>
<img src="" height="80%" width="80%" />
</p>

<p>
<img src="" height="80%" width="80%" />
</p>

<p>
<img src="" height="80%" width="80%" />
</p>

<p>
<img src="" height="80%" width="80%" />
</p>

<p>
<img src="" height="80%" width="80%" />
</p>

<p>
<img src="" height="80%" width="80%" />
</p>

<p>
<img src="" height="80%" width="80%" />
</p>

<p>
<img src="" height="80%" width="80%" />
</p>

<p>
<img src="" height="80%" width="80%" />
</p>
