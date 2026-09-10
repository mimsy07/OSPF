# ✨ OSPF

<p>    This Network topology is designed to used multi-area OSPF routing protocol to provide efficient and dynamic communication between multiple routers and networks end users. Open Shortest Path First is a dynamic routing protocol that used COST as metric and Djikstra as Algorithm with an administrative distance of 110. OSPF allows router to exchange routing information in determining the best path available to reach the remote networks.

This topology divides into multi-areas with Area 0 serving as a backbone area, other areas are connected using Area Border Router (ABR) wherein the latter is a part of both Area 0 and also an Internal router itself, allowing it to share routing information between areas. This topology also includes an Autonomous System Boundary Router (ASBR) that redistribute or translating routing information from different routing protocol to our OSPF multi-area domain, allowing 2 different protocol to share routing information</p>

<h3>📓 Main Objective</h3>

  To implement a multi-Area OSPF network that enables dynamic routing and efficient communication between routers and end-user from different areas while providing scalable and faster automatic route convergence.


<h3>💪 Skills Demonstrated</h3>

1. Implementation of OSPF multi-area
2. Assigning different area to minimize the sharing of LSDB of router to a one ABR
3. Configuring Redistribution allowing an EIGRP protocol to share its remote network to the OSPF domain
4. Implementing OSPF Security Passive interface and Authentication interfaces
5. Assign IP address to the routers and PC
6. Configuring general routing configuration

<h3>Project Walk Through</h3>

<p align="center">
Network Diagram: <br/>
<img src="https://github.com/mimsy07/OSPF/blob/main/OSPF.png" height="80%" width="80%"/>
<br />

<h3>Routing table and Neighbor of each router</h3>

<h4><b>Area 0:</b></h4>
  
<img src="https://github.com/mimsy07/OSPF/blob/main/Area0.png" height="40%" width="40%"/>
<br />
<img src="https://github.com/mimsy07/OSPF/blob/main/A0%20neig.png" height="40%" width="40%"/>
<br />

<h4><b>Area 1:</b></h4>
  
<img src="https://github.com/mimsy07/OSPF/blob/main/Area1.png" height="40%" width="40%"/>
<br />

<h4><b>Area 2:</b></h4>
  
<img src="https://github.com/mimsy07/OSPF/blob/main/Area2.png" height="40%" width="40%"/>
<br />

<h4><b>Area 3:</b></h4>
  
<img src="https://github.com/mimsy07/OSPF/blob/main/Area3.png" height="40%" width="40%"/>
<br />

<h4><b>Area 4:</b></h4>
  
<img src="https://github.com/mimsy07/OSPF/blob/main/Area4.png" height="40%" width="40%"/>


<h2>Configuration</h2>

<br />
<h3>MAIN Router-ID 5.5.5.5</h3>
<br />
<p>OSPF Routing Protocol</p>

````
conf t
router ospf 100
router-id 5.5.5.5
network 172.16.29.0 255.255.255.252 area 0
````
<br />
<p>OSPF Security: Passive interface and Authentication(password= cisco)</p>

````
conf t
router ospf 100
passive-interface default
no passive-interface g6/0
no passive-interface g7/0
no passive-interface g8/0
no passive-interface g9/0
area 0 ospf authentication message-digest
exit
!
int g6/0
ip ospf message-digest-key 1 md5 cisco
exit
!
int g7/0
ip ospf message-digest-key 1 md5 cisco
exit
!
int g8/0
ip ospf message-digest-key 1 md5 cisco
exit
!
int g9/0
ip ospf message-digest-key 1 md5 cisco
exit

````
<h3>R1 Router-ID 1.1.1.1</h3>
<br />
<p>OSPF Routing Protocol</p>

````
conf t
router ospf 100
router-id 1.1.1.1
network 192.168.70.0 255.255.255.0 area 1
network 172.16.29.0 255.255.255.252 area 0
````
<br />
<p>OSPF Security: Passive interface and Authentication(password= cisco)</p>

````
conf t
router ospf 100
passive-interface default
no passive-interface g0/0
area 0 ospf authentication message-digest
exit
!
int g0/0
ip ospf message-digest-key 1 md5 cisco 

````
<br />
<h3>R2 Router-ID 2.2.2.2</h3>
<br />
<p>OSPF Routing Protocol</p>

````
conf t
router ospf 100
router-id 2.2.2.2
network 192.168.71.0 255.255.255.0 area 2
network 172.16.29.0 255.255.255.252 area 0
````
<br />
<p>OSPF Security: Passive interface and Authentication(password= cisco)</p>

````
conf t
router ospf 100
passive-interface default
no passive-interface g0/0
area 0 ospf authentication message-digest
exit
!
int g0/0
ip ospf message-digest-key 1 md5 cisco 

````

<br />
<h3>R4 Router-ID 4.4.4.4</h3><p>ASBR and ABR of Area 3</p>
<br />
<p>Create Loopback interface for EIGRP remote network</p>

````
int loopback 0
ip address 172.16.16.1 255.255.255.0
no shut
exit
!
int loopback 1
ip address 172.16.17.1 255.255.255.0
exit
!
int loopback 172.16.18.1 255.255.255.0
no shut
exit

````

<p>OSPF & EIGRP routing protocol implementaion</p>

````
conf t
router ospf 100
router-id 4.4.4.4
network 192.168.73.0 255.255.255.0 area 3
network 172.16.29.0 255.255.255.252 area 0
exit
!
router eigrp 100
network 172.16.16.0 255.255.255.0
network 172.16.17.0 255.255.255.0
network 172.16.18.0 255.255.255.0

````
<br />
<p>Redistribute EIGRP and OSPF</p>

````
router eigrp 100
redistribute ospf 100 metric 1 1 255 255 1
exit
!
router ospf 100
redistribute eigrp 100 subnets
exit
!
````
<br />
<p>OSPF Security: Passive interface and Authentication(password= cisco)</p>

````
conf t
router ospf 100
passive-interface default
no passive-interface g0/0
area 0 ospf authentication message-digest
exit
!
int g0/0
ip ospf message-digest-key 1 md5 cisco 

````
<br />
<h3>R3 Router-ID 3.3.3.3</h3>
<br />
<p>OSPF Routing Protocol</p>

````
conf t
router ospf 100
router-id 3.3.3.3
network 192.168.72.0 255.255.255.0 area 4
network 172.16.29.0 255.255.255.252 area 0
````
<br />
<p>OSPF Security: Passive interface and Authentication(password= cisco)</p>

````
conf t
router ospf 100
passive-interface default
no passive-interface g0/0
area 0 ospf authentication message-digest
exit
!
int g0/0
ip ospf message-digest-key 1 md5 cisco 

````












