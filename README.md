# ✨ OSPF

<p>    This Network topology is designed to used multi-area OSPF routing protocol to provide efficient and dynamic communication between multiple routers and networks end users. Open Shortest Path First is a dynamic routing protocol that used COST as metric and Djikstra as Algorithm with an administrative distance of 110. OSPF allows router to exchange routing information in determining the best path available to reach the remote networks.

This topology divides into multi-areas with Area 0 serving as a backbone area, other areas are connected using Area Border Router (ABR) wherein the latter is a part of both Area 0 and also an Internal router itself, allowing it to share routing information between areas. This topology also includes an Autonomous System Boundary Router (ASBR) that redistribute or translating routing information from different routing protocol to our OSPF multi-area domain, allowing 2 different protocol to share routing information</p>

<h3>📓 Main Objective</h3>

  To implement a multi-Area OSPF network that enables dynamic routing and efficient communication between routers and end-user from different areas while providing scalable and faster automatic route convergence.


<h3>💪 Skills Demonstrated</h3>

1. Implementation of OSPF multi-area
2. Assigning different area to minimize the sharing of LSDB of router to a one ABR
3. Configuring Redistribution allowing an EIGRP protocol to share its remote network to the OSPF domain
4. Assign IP address to the routers and PC
5. Configuring general routing configuration

<h3>Project Walk Through</h3>

<p align="center">
Network Diagram: <br/>
<img src="https://github.com/mimsy07/OSPF/blob/main/OSPF.png" height="80%" width="80%"/>
<br />

<h4>Routing table and Neighbor of each router</h4>

<p align="left">
Area 0: <br/>
<img src="https://github.com/mimsy07/OSPF/blob/main/Area0.png" height="80%" width="80%"/>
<br />
<img src="https://github.com/mimsy07/OSPF/blob/main/A0%20neig.png" height="80%" width="80%"/>
<br />
  
