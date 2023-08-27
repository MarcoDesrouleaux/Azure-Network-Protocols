<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

## Introduction
This guide walks you through the process of setting up and using WireShark to monitor network traffic on Azure Virtual Machines (VMs). By the end, you'll understand how to capture and analyze packets within your Azure environment.

## Prerequisites
- An active Microsoft Azure account
- WireShark installed on your local machine
- Basic knowledge of network monitoring and Azure VMs

## Environments and Technologies Used
- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

## Operating Systems Used
- Windows 10 (21H2)
- Ubuntu Server 20.04

## Step 1: Set Up Your Azure VM
1. Log in to your Azure portal.
2. Navigate to "Create a resource" > Create 2 "Virtual Machines".
3. Launch VM1 with Remote Desktop Connection if you have Windows.
<table>
<tr>
<td>
<img src="https://i.imgur.com/u34ST6M.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/P066O34.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>

## Step 2: Install WireShark on Azure VM
2. Download and install WireShark on the VM.
3. Configure WireShark according to your monitoring needs.
<table>
<tr>
<td>
<img src="https://i.imgur.com/oixcf9e.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/SMR5xJy.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>
<table>
<tr>
<td>
<img src="https://i.imgur.com/zZwWOBL.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/XK9C9mZ.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>

## Step 3: Configure Capture Settings

### 3.1 Start Capturing Traffic
1. Still in WireShark, click 'Start' to begin capturing packets.
2. You can stop the capture at any time by clicking 'Stop.'
3. Let's start filtering for ICMP (Internet Control Messaging Protocol) traffic. (It's the protocol that ping uses).
4. We'll test it by pinging the Private IP address of VM2 with Windows PowerShell.
5. Request on WireShark will also indicate that it's timed out.
<table>
<tr>
<td>
<img src="https://i.imgur.com/YYk1mUN.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/Lk15Eak.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>
<img src="https://i.imgur.com/WtOWTE5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

### 3.2 Initiating Perpetual Ping From VM1 to VM2 to stop ICMP traffic to Come Through  (Nonstop Ping)
To initiate perpetual ping, we'll use the following command for our Windows VM1: "ping -t [IP Address or Hostname]".
A perpetual ping is used to continuously monitor network connectivity.
<img src="https://i.imgur.com/UwV04Xy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

### 3.3 Changing the FireWall on VM2 to Not Allow ICMP Traffic to Come Through by Using Network Security Group (NSG)
1. To block ICMP traffic on VM2's FireWall, we'll go to the Network Security Groups (NSG) on our Microsoft Azure Account.
2. We'll then open the VM2-nsg page.
3. Open to edit the Inbound Security Rules to create a new rule that will deny inbound ICMP traffic to block the pings coming from VM1.
4. Once we create the new rule, the ping should immediately start to time out because it will be blocked by VM2's FireWall.
5. Once you allow ICMP traffic from VM2, the "request timed out" should stop.
6. On Windows PowerShell, type command: Control-C to stop.
<table>
<tr>
<td>
<img src="https://i.imgur.com/MTiV9FV.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/TExTbH7.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>
<table>
<tr>
<td>
<img src="https://i.imgur.com/61TROc0.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/Yvvu9Wg.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>
<table>
<tr>
<td>
<img src="https://i.imgur.com/aAs4BOi.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/FIKScYU.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>
<table>
<tr>
<td>
<img src="https://i.imgur.com/3miJrhV.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/P9tgDIF.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>
<table>
<tr>
<td>
<img src="https://i.imgur.com/B3CTGo5.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/RiqQObm.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>

### Step 4: Observe Secure Shell (SSH) Traffic
1. To connect to VM1 to VM2, copy VM2 Private IP address and type ssh (Username)@(IP Address). Our is ssh Azureuser@10.0.0.5
2. On Windows PowerShell, type "yes", then type password and press enter. (Password will be invisible on Windows PowerShell).
<table>
<tr>
<td>
<img src="https://i.imgur.com/lFK4OyK.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/joIRX5u.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>
<table>
<tr>
<td>
<img src="https://i.imgur.com/lFK4OyK.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/SMR5xJy.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>

### Step 5: Observe DHCP Traffic
<table>
<tr>
<td>
<img src="https://i.imgur.com/oixcf9e.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/SMR5xJy.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>

### Step 6: Observe DNS Traffic
<table>
<tr>
<td>
<img src="https://i.imgur.com/oixcf9e.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/SMR5xJy.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>

### Step 7: Observe RDP Traffic
<table>
<tr>
<td>
<img src="https://i.imgur.com/oixcf9e.png" alt="Image 1 Description" width="100%"/>
</td>
<td>
<img src="https://i.imgur.com/SMR5xJy.png" alt="Disk Sanitization Steps" width="100%"/>
</td>
</tr>
</table>

## Conclusion
You have successfully set up WireShark on an Azure VM and captured network traffic for analysis. This knowledge is a stepping stone for advanced network monitoring in Azure.
