# VLAN Configurations

<h2>Description</h2>
Confgiure VLANs for each department.

<h2>Environments Used </h2>

- <b>Cisco Packet Tracer</b> (2.2.43) <br />

- <b>Cisco IOS PT1000 Software, Version 12.2(28) <br />

<h2>Diagram </h2>
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
