<p align="center">
<img src="https://i.imgur.com/VHNGlvQ.png"/>
</p>

<h1>Setting up A Firewall Configuration </h1>
This project tutorial outlines, observes, and will walk through the steps to perform a perpetual/nonstop ping from Windows 10 VM to Linux Ubuntu VM vs. a Firewall Configuration within Linux Ubuntu, instantaneously preventing ping traffic from entering its system and network. Firewall configuration is the process of setting up rules and security settings to determine what traffic is allowed to pass through on a network. They are normally set up to protect a computer device, system or network from unauthorized access, malicious activity, and other security threats.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Wireshark
- Powershell

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
- Linux Ubuntu

<h2>List of Prerequisites</h2>

- Computer Desktop/Laptop
- Wifi Connection
- Azure Account
- Powershell
- Wireshark

<h2>Firewall Configuration Steps</h2>
Step 1:
<p>
<img src="https://i.imgur.com/GpTdfWp.png"/>
</p>
<p>
Log on to Azure and go to Virtual Machines and start both the Windows10-vm and Linux Ubuntu Virtual Machines.
</p>
<br />
Step 2:
<p>
<img src="https://i.imgur.com/USy8uSg.png"/>
</p>
<p>
</p>
<br />
Log into the Windows10-vm in remote desktop with the credentials created in the windows10-vm configuration setup back in project 1.
<br />
</p>
</p>

Step 3:
<p>
<img src="https://i.imgur.com/KmRg28z.png"/>
</p>
<p>
Go to the start menu within the remote desktop and search for Wireshark. Click on and open the app.
</p>
<br />
Step 4:
<p>
<img src="https://i.imgur.com/Ig2Nx51.png"/>
</p>
<p>
Click on the ethernet tab.
</p>
<br />

Step 5:
<p>
<img src="https://i.imgur.com/XYURtyo.png"/>
</p>
<p>
Click on the blue shark symbol in the upper left hand side of the app to run a packet capture.
</p>
<br />
Step 6:
</p>
<p>
<img src="https://i.imgur.com/PyZvuBV.png"/>
</p>
<p>
Observe the packet capture taking place and the random sources of spam traffic. 
</p>
<br />
Step 7:
<p>
<img src="https://i.imgur.com/eMAeXwF.png"/>
</p>
<p>
Next, go back to Virtual Machines in Azure and click on Linux Ubuntu.
</p>
<br />
Step 8:
<p>
<img src="https://i.imgur.com/I8jsq3b.png"/>
</p>
<p>
Copy the private IP address of the Linux Ubuntu Virtual Machine. 
</p>
<br />
Step 9:
<p>
<img src="https://i.imgur.com/H8RlnPI.png"/>
</p>
<p>
Go back into Windows10-vm remote desktop and in the start menu look up Powershell. Click on and open up the app.
</p>
<br />

Step 10:
<p>
<img src="https://i.imgur.com/8bZG7wV.png"/>
</p>
<p>
In the Powershell app, ping the Linux Ubuntu private IP address. Type in ping 10.0.0.5 -t. Notice all of the replies that start coming from the linux vm to the windows10-vm within Powershell, but in Wireshark it may be hard to spot out due to all the spam traffic. Theres a way to fix this. 
</p>
<br />
Step 11:
<p>
<img src="https://i.imgur.com/ZiyzgYN.png"/>
</p>
<p>
To rid all the spam traffic within Wireshark, an ICMP filter will be applied by typing it in the search bar of the Wireshark app. Press enter and notice that all the spam traffic dissapears and only the source and destination traffic from the windows10-vm and linux ubuntu-vm are visible. All of the spam traffic has been filterd out. Also take note of the request/ reply column withing Wireshark. This is an idicator that there is a scuccessful connection between the two computers and no firewall block has been set in place. The next steps will walkthrough and observe the ICMP traffic with a firewall block configured within Linux Ubuntu to show you the difference without a fireblock vs. it with one.
</p>
<br />
Step 12:
<p>
<img src="https://i.imgur.com/eMAeXwF.png"/>
</p>
<p>
Go back in to Azure and go to Virtual Machines. Click on LinuxUbuntu. 
</p>
<br />
Step 13:
<p>
<img src="https://i.imgur.com/QAZOJzC.png"/>
</p>
<p>
Scroll down to networking and then click on Network settings. 
</p>
<br />
Step 14:
<p>
<img src="https://i.imgur.com/66T3357.png"/>
</p>
<p>
Look for and click on the LinuxUbuntu Network Security Group Link. 
</p>
<br />
Step 15:
<p>
<img src="https://i.imgur.com/NqJs52e.png"/>
</p>
<p>
Underneath Settings click on Inbound security rules.
</p>
<br />
Step 16:
<p>
<img src="https://i.imgur.com/dVBy5m8.png"/>
</p>
<p>
Click on the add button.
</p>
<br />
Step 17:
<p>
<img src="https://i.imgur.com/qBo6iJY.png"/>
</p>
<p>
Next, the Add inbound security rule page should pop up. For source keep as any, source port ranges;* for destination; any, for service;custom, for destination port ranges;* for protocol;ICMPv4.
</p>
<br />
Step 18:
<p>
<img src="https://i.imgur.com/KdSwv3D.png"/>
</p>
<p>
For Action click deny, Priority;290, and name can stay as is. Press Add.
</p>
<br />
Step 19:
<p>
<img src="https://i.imgur.com/Mj57Is7.png"/>
</p>
<p>
Now go back into Windows Powershell and notice requests begin to time out and within Wireshark all you see is a nonstop 'ping' of requests, no replies. This is the firewall block taking place preventing traffic from entering in the Linux Ubuntu network. It is no longer responding back to the windows10-vm. FYI:It can take anywhere from a few seconds or longer to see the firewall block take place. After observing the firewall block, it is now time to disable the firewall block to resume normal traffic between both computers.
</p>
<br />
Step 20:
<p> 
<img src="https://i.imgur.com/2CQAQSL.png"/>
</p>
<p>
Go back into Linux Ubuntu's Inbound Security Group and delete the rule that was set in place to configure the firewall block simply by pressing the trashcan icon on the right end side of the rule.
</p>
<br />
Step 21:
<p>
<img src="https://i.imgur.com/8pZIx88.png"/>
</p>
<p>
The Delete security rule box should pop up. Press yes. 
</p>
<br />
Step 22:
<p>
<img src="https://i.imgur.com/NWN5Z78.png"/>
</p>
<p>
After deleting the rule you should now see the traffic go back to normal with ping requests being sent from windows10-vm and ping replies sent back from Linux Ubuntu-vm.
</p>
<br />
Step 23:
<p>
<img src="https://i.imgur.com/R5eoldm.png"/>
</p>
<p>
To end the pings within Wireshark and Powershell simply type in Ctl-C in the command line of Windows Powershell and all pings should come to a complete halt.

This here concludes the project tutorial and observation on Setting up a Firewall Configuration.
</p>
<br />

