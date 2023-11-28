# VLAN Configurations

<h2>Description</h2>
Confgiure VLANs for each department.

<h2>Environments Used </h2>

- <b>Cisco Packet Tracer</b> (2.2.43) <br />

- <b>Cisco IOS PT1000 Software, Version 12.2(28) <br />

<h2>Diagram </h2>
<img src="https://i.imgur.com/iMHVkxl.png" height="80%" width="80%" />

<h2>Walk-through:</h2>
Configurations IP addresses on PCs and cable connections between SW1 and R1. <br />
R1(config)#int l0 <br />
R1(config-if)#ip address 1.1.1.1 255.255.255.255 (loopback interface IP address will always be OSPF device identifier from other routers routing tables) <br />
- Alternatively, to enable OSPF on selected interfaces run 'ip ospf 1 area 0' from interface config mode. <br />
R1(config-if)#router ospf 1 (OSPF process ID doesn't need to match between routers) <br />
R1(config-router)#net 0.0.0.0 255.255.255.255 area 0 (OSPF "0.0.0.0 255.255.255.255" includes all addresses) <br />
R1(config-router)#passive-interface l0 (prevents interface from needlessly sending OSPF messages) <br />
R1(config-router)#default-information originate (configures R1 as autonomous system boundary router) <br />
R1(config-router)#exit <br />
R1(config)#ip route 0.0.0.0 0.0.0.0 203.0.113.2 (default route to ISP) <br />
<img src="https://i.imgur.com/tHeU3fH.png" height="80%" width="80%" /> <br />
<br />
<br />
