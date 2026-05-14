<h1>OSPF and ACLs Lab Project</h1>

<h2>Overview</h2>
This project demonstrates the configuration and verification of dynamic routing using OSPF along with the implementation of Standard ACLs in a multi-router network environment using Cisco Packet Tracer.

The lab focuses on:

OSPF neighbor establishment and route advertisement
Inter-network communication testing
Traffic filtering using numbered and named ACLs
Network segmentation and access control policies
<br />


<h2>Technologies Used</h2>

- <b>Cisco Packet Tracer</b> 
- <b>Cisco IOS CLI</b>
- <b>OSPF Routing Protocol</b>
- <b>Standard Access Control Lists (ACLs)</b>
- <b>IPv4 Addressing</b>
- <b>ARP Verification</b>
- <b>ICMP Testing (Ping)</b>

<h2>Environments Used </h2>

- <b>Cisco Packet Tracer</b>

<h2>Objectives</h2>

- <b>OSPF Configuration</b> 
- <b>Configure OSPF on both routers</b>
- <b>Advertise all connected networks</b>
- <b>Verify OSPF-enabled interfaces</b>
- <b>Confirm learned routes in routing tables</b>
- <b>ACL Security Policies</b>

<h2>Implemented the following access policies:</h2>

- <b>Only PC1 and PC3 can access 192.168.1.0/24</b> 
- <b>Hosts in 172.16.2.0/24 cannot access 192.168.2.0/24</b>
- <b>172.16.1.0/24 cannot access 172.16.2.0/24</b>
- <b>172.16.2.0/24 cannot access 172.16.1.0/24</b>


<h2>Lab walk-through:</h2>

<p align="center">
Static IP addresses have been preconfigured for this lab <br/>
<img src="https://i.imgur.com/tB7coFM.png" height="80%" width="80%" alt="OSPF and ACLs"/>
<br />
<br />
R1’s OSPF configuration:
In global config mode, I used the command: router ospf 1, to configure the networks of the interfaces connected to the router.
Then, I configured every network so that the router activates ospf in every interface and they can be advertised to R2
  <br/>
<img src="https://i.imgur.com/C7LEICO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
