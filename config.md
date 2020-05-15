# Configure MPLS Using GNS3
![](/images/topologi.PNG)
## IP Address Configuration
The first thing to do before configuring MPLS is that you must first configure IP addressing.
### R1
R1#conf t.
R1(config)#int fa1/0.
R1(config-if)#ip add.
R1(config-if)#ip address 172.16.1.1 255.255.255.0.
R1(config-if)#no sh.
R1(config-if)#ex.
R1(config)#int fa0/0.
R1(config-if)#ip add.
R1(config-if)#ip address 172.16.3.1 255.255.255.0.
R1(config-if)#no sh.
R1(config-if)#ex.
R1(config)#ex.
R1#wr.
### R2
R2#conf t.
R2(config)#int fa0/0.
R2(config-if)#ip address 172.16.1.2 255.255.255.0.
R2(config-if)#no sh.
R2(config-if)#ex.
R2(config)#int fa1/0.
R2(config-if)#ip address 17.10.10.1 255.255.255.240.
R2(config-if)#no sh.
R2(config-if)#ex.
R2(config)#int fa1/1.
R2(config-if)#ip add.
R2(config-if)#ip address 10.20.20.1 255.255.255.240.
R2(config-if)#no sh.
R2(config-if)#ex.
R2(config)#ex.
R2(config)#int lo0.
R2(config-if)#ip address 12.12.1.1 255.255.255.0.
R2(config-if)#no sh.
R2(config-if)#ex.
R2(config)#ex.
R2#wr.
### R3
R3#conf t.
R3(config)#int fa0/0.
R3(config-if)#ip add.
R3(config-if)#ip address 17.10.10.2 255.255.255.240.
R3(config-if)#no sh.
R3(config-if)#ex.
R3(config)#int fa1/0.
R3(config-if)#ip add.
R3(config-if)#ip address 10.30.30.1 255.255.255.240.
R3(config-if)#no sh.
R3(config-if)#ex.
R3(config)#int lo0.
R3(config-if)#ip address 12.12.2.1 255.255.255.0.
R3(config-if)#no sh.
R3(config-if)#ex.
R3(config)#ex.
R3#wr.
### R4
R4#conf t.
R4(config)#int fa0/0.
R4(config-if)#ip add.
R4(config-if)#ip address 10.20.20.2 255.255.255.240.
R4(config-if)#no sh.
R4(config-if)#ex.
R4(config)#int fa1/0.
R4(config-if)#ip add.
R4(config-if)#ip address 83.40.40.1 255.255.255.240.
R4(config-if)#no sh.
R4(config-if)#ex.
R4(config)#ex.
R4(config)#int lo0.
R4(config-if)#ip address 12.12.3.1 255.255.255.0.
R4(config-if)#no sh.
R4(config-if)#ex.
R4(config)#ex.
R4#wr.
### R5
R5#conf t.
R5(config)#int fa0/0.
R5(config-if)#ip add.
R5(config-if)#ip address 10.30.30.2 255.255.255.240.
R5(config-if)#no sh.
R5(config-if)#ex.
R5(config)#int fa1/0.
R5(config-if)#ip add.
R5(config-if)#ip address 83.40.40.2 255.255.255.240.
R5(config-if)#no sh.
R5(config-if)#ex.
R5(config)#int fa1/1.
R5(config-if)#ip add.
R5(config-if)#ip address 172.16.2.1 255.255.255.0.
R5(config-if)#no sh.
R5(config-if)#ex.
R5(config)#ex.
R5(config)#int lo0.
R5(config-if)#ip address 12.12.4.1 255.255.255.0.
R5(config-if)#no sh.
R5(config-if)#ex.
R5(config)#ex.
R5#wr.
### R6
R6#conf t.
R6(config)#int fa0/0.
R6(config-if)#ip add.
R6(config-if)#ip address 172.16.2.2 255.255.255.0.
R6(config-if)#no sh.
R6(config-if)#ex.
R6(config)#int fa1/0.
R6(config-if)#ip add.
R6(config-if)#ip address 172.16.4.1 255.255.255.0.
R6(config-if)#no sh.
R6(config-if)#ex.
R6(config)#ex.
R6#wr.
### PC1
PC1> ip 172.16.3.2 172.16.1.1 24.
PC1 : 172.16.3.2 255.255.255.0 gateway 172.16.1.1.
### PC2
PC2> ip 172.16.4.2 172.16.4.1 24.
PC1 : 172.16.4.2 255.255.255.0 gateway 172.16.4.1.
**Note !!** Confused by configuration on a PC? So IP (ip address) (ip gateway) (prefix). 
## OSPF Configuration
If you have made an IP address for each router and PC. Then next do the OSPF configuration.
### R2
R2(config)#router ospf 1.
R2(config-router)#network 17.10.10.0 0.0.0.15 area 0.
R2(config-router)#network 10.20.20.0 0.0.0.15 area 0.
R2(config-router)#network 12.12.1.1 0.0.0.255 area 0.
R2(config-router)#ex.
R2(config)#ex.
R2#wr.
### R3
R3(config)#router ospf 1.
R3(config-router)#network 17.10.10.0 0.0.0.15 area 0.
R3(config-router)#network 10.30.30.0 0.0.0.15 area 0.
R3(config-router)#network 12.12.2.1 0.0.0.255 area 0.
R3(config-router)#ex.
R3(config)#ex.
R3#wr.
### R4
R4(config)#router ospf 1.
R4(config-router)#network 10.20.20.0 0.0.0.15 area 0.
R4(config-router)#network 83.40.40.0 0.0.0.15 area 0.
R4(config-router)#network 12.12.3.1 0.0.0.255 area 0.
R4(config-router)#ex.
R4(config)#ex.
R4#wr.
### R5
R5(config)#router ospf 1.
R5(config-router)#network 10.30.30.0 0.0.0.15 area 0.
R5(config-router)#network 83.40.40.0 0.0.0.15 area 0.
R5(config-router)#network 12.12.4.1 0.0.0.255 area 0.
R5(config-router)#ex.
R5(config)#ex.
R5#wr.
## MPLS Configuration
If you have configured OSPF, then you can configure MPLS.
### R2
R2(config)#mpls label protocol ldp.
R2(config)#mpls ldp session protection.
R2(config)#mpls ldp router-id lo0.
R2(config)#ip cef.
R2(config)#router ospf 1.
R2(config-router)#mpls ldp autoconfig area 0.
R2(config-router)#ex.
R2#wr.
### R3
R3(config)#mpls label protocol ldp.
R3(config)#mpls ldp session protection.
R3(config)#mpls ldp router-id lo0.
R3(config)#ip cef.
R3(config)#router ospf 1.
R3(config-router)#mpls ldp autoconfig area 0.
R3(config-router)#ex.
R3(config)#ex.
R3#wr.
### R4
R4(config)#mpls label protocol ldp.
R4(config)#mpls ldp session protection.
R4(config)#mpls ldp router-id lo0.
R4(config)#ip cef.
R4(config)#router ospf 1.
R4(config-router)#mpls ldp autoconfig area 0.
R4(config-router)#ex.
R4(config)#ex.
R4#wr.
### R5
R5(config)#mpls label protocol ldp.
R5(config)#mpls ldp session protection.
R5(config)#mpls ldp router-id lo0.
R5(config)#ip cef.
R5(config)#router ospf 1.
R5(config-router)#mpls ldp autoconfig area 0.
R5(config-router)#ex.
R5(config)#ex.
R5#wr.
## See Configuration Status
If you have configured MPLS, then you can check it in a way.
### Check Route Status
show ip route.
Then it will produce like this.
 ![](/images/ip route.PNG)
### Check Interface Status
show ip interface brief.
Then it will produce like this.
 ![](/images/int br.PNG)
### Check MPLS Status
show mpls ldp neighbor detail.
Then it will produce like this.
 ![](/images/status mpls.PNG)
### Check MPLS Forwarding Status
show mpls forwarding-table.
Then it will produce like this.
 ![](/images/status-forwarding-mpls.PNG)

Hope it is useful, happy learning and staying enthusiastic.