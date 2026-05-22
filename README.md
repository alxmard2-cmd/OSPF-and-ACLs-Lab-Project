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
<img src="https://i.imgur.com/C7LEICO.png" height="80%" width="80%" alt="OSPF and ACLs"/>
<br />
<br />
Then I used the command “show ip ospf interface” to verify that ospf is active in the interfaces (G0/0, G0/1, S0/0/0) <br/>
<img src="https://i.imgur.com/urAhqzl.png" height="80%" width="80%" alt="OSPF and ACLs"/>
<br />
<br />
Configuration of R2’s OSPF following the same process for the networks 192.168.1.0 and 192.168.2.0 and 203.0.113.0: <br/>
<img src="https://i.imgur.com/6Oa2ZOr.png" height="80%" width="80%" alt="OSPF and ACLs"/>
<br />
<br />
Confirmation that R1 has learnt new routes with OSPF by using the command “show ip route”: <br/>
<img src="https://i.imgur.com/iOb0oQe.png" height="80%" width="80%" alt="OSPF and ACLs"/>
<br />
<br />
Ping SRV1 (192.168.1.100) from PC1 to check if the routers are routing the traffic correctly.
The first Ping fails because of the ARP process but the next 3 are successful.
  <br/>
<img src="https://i.imgur.com/l7zWsAb.png" height="80%" width="80%" alt="OSPF and ACLs"/>
<br />
<br />
Ping from PC3 to SRV2. The first one fails because of ARP but the next 3 are successful. <br/>
<img src="https://i.imgur.com/ljjWmmj.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>
I write the commands for the first ACL (For PC1 and PC3 to be the only ones permitted to access SRV1): <br/>
Commands: <br/>
R2(config)#ip access-list standard TO_192.168.1.0/24<br/>
R2(config-std-nacl)#permit 172.16.1.1<br/>
R2(config-std-nacl)#permit 172.16.2.1<br/>
R2(config-std-nacl)#deny any<br/>
 <br/>
<p align="center">
<img src="https://i.imgur.com/XG5Vry6.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>Then, for the ACL to take effect I apply it on the interface (G0/0):<br/>
	Commands:<br/>
	R2(config-std-nacl)#int g0/0<br/>
R2(config-if)#ip access-group TO_192.168.1.0/24 out<br/>
 <br/>
 <p align="center">
<img src="https://i.imgur.com/4Wvq1oN.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>
Now, I configured the next ACL (For the interface G0/1 to deny the hosts from the network 172.16.2.0/24):<br/>
	Commands:<br/>
R2(config)#ip access-list standard TO_192.168.2.0/24<br/>
R2(config-std-nacl)#deny 172.16.2.0 0.0.0.255<br/>
R2(config-std-nacl)#permit any<br/>
 <br/>
 <p align="center">
<img src="https://i.imgur.com/ZXki8WQ.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>
Then, I apply the ACL to the G0/1’s interface outbound traffic:<br/>
	Commands: <br/>
	R2(config-std-nacl)#int g0/1 <br/>
R2(config-if)#ip access-group TO_192.168.2.0/24 out <br/>
  <br/>
<p align="center">
<img src="https://i.imgur.com/nueynSi.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>
Configuration of ACLs from R1 to be configured as close as possible to the destination. Standard Numbered ACLs are used for this part of the lab.<br/>
Commands:<br/>
R1(config)#access-list 1 deny 172.16.1.0 0.0.0.255<br/>
R1(config)#access-list 1 permit any<br/>
 <br/>
<p align="center">
<img src="https://i.imgur.com/iyM29Zd.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>
ACL 1 is applied to the g0/1 interface for the router to block the outbound traffic coming from 172.16.1.1<br/>
Commands:<br/>
R1(config)#int g0/1<br/>
R1(config-if)#ip access-group 1 out<br/>
 <br/>
<p align="center">
<img src="https://i.imgur.com/gsz5DV3.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>
Another ACL is created to block the traffic comming from 172.16.2.0/24 to g0/0 and permit the rest of the traffic. <br/>
<p align="center">
<img src="https://i.imgur.com/QCTwodA.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>The ACL is then applied to R1’s g0/0 interface:  <br/>
<p align="center">
<img src="https://i.imgur.com/4EOFBA1.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>
Now a few pings are tried to confirm the ACLs were configured properly: <br/>
From PC1 to SRV1 there is connection.
  <br/>
<p align="center">	
<img src="https://i.imgur.com/YSvcjSZ.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>
</p>But when I ping from PC2 to SRV1 the destination is unreachable, so the firs ACL is working well. <br/>
<p align="center">	
<img src="https://i.imgur.com/4c1mjwf.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>
</p>Now, I ping from PC3 (172.16.2.1) to SRV2 (192.168.2.100) and the destination is unreachable as expected: <br/>
<p align="center">	
<img src="https://i.imgur.com/xbfp2XF.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>
</p>Then, I try to ping from PC2 to PC4 and the destination is not reachable neither, so the ACLs are working as expected:<br/>
<p align="center">	
<img src="https://i.imgur.com/JfomjBB.png" height="80%" width="80%" alt="OSPF and ACLs"/>
</p>

<h2>Project Outcome:</h2>
<h3>Successfully implemented:</h3>

- <b>Fully functional OSPF routing between routers</b> 
- <b>Secure traffic filtering policies using ACLs</b>
- <b>Controlled inter-network communication</b>
- <b>End-to-end network validation</b>


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
