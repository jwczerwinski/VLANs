# VLAN Configurations

<h2>Description</h2>
Confgiure VLANs for each department.

<h2>Environments Used </h2>

- <b>Cisco Packet Tracer</b> (2.2.43) <br />

- <b>Cisco IOS PT1000 Software, Version 12.2(28) <br />


<h2>Scenario 1 Diagram </h2>
<img src="https://i.imgur.com/iMHVkxl.png" height="80%" width="80%" />
<h2>Walk-through:</h2>
Configurations IP addresses and default gateways on PCs as well as cable connections between SW1 and R1. Configure R1 with IP addresses of the default gateways for each VLAN. <br />
R1(config)#int g0/0 <br />
R1(config-if)#ip address 10.0.0.62 255.255.255.192 <br />
R1(config-if)#no shut <br />
R1(config-if)#int g0/1 <br />
R1(config-if)#ip address 10.0.0.126 255.255.255.192 <br />
R1(config-if)#no shut <br />
R1(config-if)#int g0/2 <br />
R1(config-if)#ip address 10.0.0.190 255.255.255.192 <br />
R1(config-if)#no shut <br />
<img src="https://i.imgur.com/jcw1VE4.png" height="80%" width="80%" /> <br />
<br />
<br />
Configure SW1 with VLANs for each department and assign interfaces for each VLAN. <br />
SW1(config)#vlan 10  <br />
SW1(config-vlan)#name engineering  <br />
SW1(config-vlan)#int range f3/1, f4/1, g0/1  <br />
SW1(config-if-range)#switchport mode access  <br />
SW1(config-if-range)#switchport access vlan 10  <br />
SW1(config)#vlan 20  <br />
SW1(config-vlan)#name HR  <br />
SW1(config-vlan)#int range f5/1, f6/1, g1/1  <br />
SW1(config-if-range)#switchport mode access  <br />
SW1(config-if-range)#switchport access vlan 20  <br />
SW1(config)#vlan 30  <br />
SW1(config-vlan)#name Sales  <br />
SW1(config-vlan)#int range f7/1, f8/1, g2/1  <br />
SW1(config-if-range)#switchport mode access  <br />
SW1(config-if-range)#switchport access vlan 30  <br />
<img src="https://i.imgur.com/COdU4E8.png" height="80%" width="80%" /> <br />
<br />
<br />
Verify with tracert <br />
<img src="https://i.imgur.com/IiT8uut.png" height="80%" width="80%" /> <br />
<br />
<br />
<br />
<br />
<h2>Scenario 2 Diagram </h2>
<h2>Walk-through:</h2>
<img src="https://i.imgur.com/5S81MDm.png" height="80%" width="80%" /> <br />
Configure the switch interfaces connected to PCs as access ports in the correct VLAN. Configure the connection between SW1 and SW2 as a trunk, allowing only the necessary VLANs. Configure an unused VLAN as the native VLAN. <br />
SW1(config)#int range f0/3, f0/4 <br />
SW1(config-if-range)#switchport mode access <br />
SW1(config-if-range)#switchport access vlan 30 <br />
SW1(config-if-range)#int range f0/2,f0/1 <br />
SW1(config-if-range)#switchport mode access <br />
SW1(config-if-range)#switchport access vlan 10 <br />
SW1(config-if-range)#int g0/1 <br />
SW1(config-if)#switchport mode trunk <br />
SW1(config-if)#switchport trunk allowed vlan 10,20,30 <br />
SW1(config-if)#switchport trunk native vlan 999 <br />
SW2(config)#int g0/1-2 <br />
SW2(config-if)#switchport mode trunk <br />
SW2(config-if)#switchport trunk allowed vlan 10,20,30 <br />
SW1(config-if)#switchport trunk native vlan 999 <br />
SW2(config-if)#int range f0/1-3 <br />
SW2(config-if-range)#int range f0/1 <br />
SW2(config-if-range)#int f0/1 <br />
SW2(config-if)#switchport mode access <br />
SW2(config-if)#switchport access vlan 20 <br />
SW2(config-if)#int range f0/2-3 <br />
SW2(config-if-range)#switchport mode access <br />
SW2(config-if-range)#switchport access vlan 10 <br />
SW2(config-if-range)#vlan 30 <br />
<img src="https://i.imgur.com/qdyGMr4.png" height="80%" width="80%" /> <br />
<img src="https://i.imgur.com/7fl2yt6.png" height="80%" width="80%" /> <br />
<img src="https://i.imgur.com/3CBKh6J.png" height="80%" width="80%" /> <br />
<br />
<br />
Configure the connection between SW2 and R1 using 'router on a stick'. Assign the last usable address of each subnet to R1's subinterfaces. <br />
R1(config)#int g0/0.10 <br />
R1(config-subif)#encapsulation dot1q 10 <br />
R1(config-subif)#ip address 10.0.0.62 255.255.255.192 <br />
R1(config-subif)#no shut <br />
R1(config-subif)#int g0/0.20 <br />
R1(config-subif)#encapsulation dot1q 20 <br />
R1(config-subif)#ip address 10.0.0.126 255.255.255.192 <br />
R1(config-subif)#no shut <br />
R1(config-subif)#int g0/0.30 <br />
R1(config-subif)#encapsulation dot1q 30 <br />
R1(config-subif)#ip address 10.0.0.190 255.255.255.192 <br />
R1(config-subif)#no shut <br />
R1(config-subif)#int g0/0 <br />
R1(config-if)#no shut <br />
R1(config-if)#do show int <br />
<img src="https://i.imgur.com/F0yECwL.png" height="80%" width="80%" /> <br />
<br />
<br />
Verify with tracert <br />
<img src="https://i.imgur.com/DOltGiO.png" height="80%" width="80%" /> <br />

