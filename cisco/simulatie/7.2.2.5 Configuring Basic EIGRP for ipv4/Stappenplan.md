## Configuring Basic EIGRP for ipv4

- 3 routers en 3 pc's maken
- Tussen de routers seriële DCE verbindingen maken
- Tussen de routers en de computers een copper cross-over verbinding

#### ip configuratie pc A: 
```
192.168.1.3 255.255.255.0
gateway: 192.168.1.1
```
#### ip configuratie pc B:
```
192.168.2.3 255.255.255.0
gateway: 192.168.2.1
```
#### ip configuratie pc C: 
```
192.168.3.3 255.255.255.0
gateway: 192.168.3.1
```
#### in router 1
```
en
conf t
hostname R1
int g0/0
ip add 192.168.1.1 255.255.255.0
no shutdown
int s0/0/0
ip add 10.1.1.1 255.255.255.252
clock rate 128000
no shutdown
int s0/0/1
ip add 10.3.3.1 255.255.255.252
no shutdown
```

#### in router 2
```
en
conf t
hostname R2
int g0/0
ip add 192.168.2.1 255.255.255.0
no shutdown
int s0/0/0
ip add 10.1.1.2 255.255.255.252
no shutdown
int s0/0/1
ip add 10.2.2.2 255.255.255.252
clock rate 128000
no shutdown
```
#### in router 3
```
en
conf t
hostname R3
int g0/0
ip add 192.168.3.1 255.255.255.0
no shutdown
int s0/0/0
ip add 10.3.3.2 255.255.255.252
clock rate 128000
no shutdown
int s0/0/1
ip add 10.2.2.1 255.255.255.252
no shutdown
```
#### Connectiviteit testen:
```
(in enabled mode) ping 192.168.3.3
ping 10.3.3.1
```
#### in router 1:
```
router eigrp 10
network 10.1.1.0 0.0.0.3
network 192.168.1.0 0.0.0.255
network 10.3.3.0 0.0.0.3
```
#### in router 2:
```
router eigrp 10
network 192.168.2.0 0.0.0.255
network 10.1.1.0 0.0.0.3
network 10.2.2.0 0.0.0.3
```
#### in router 1
```
en
conf t
router eigrp 10
network 192.168.3.0 0.0.0.255
network 10.3.3.0 0.0.0.3
network 10.2.2.0 0.0.0.3
```
#### Pingen van pc-A naar pc-B
ping 192.168.2.3

#### Pingen van pc-A naar pc-B
```
ping 192.168.3.3
```
#### in router 1:
```
show ip eigrp neighbors
show ip route eigrp
```
#### in router 1:
```
show ip eigrp topology
show ip route eigrp
conf t
int s0/0/0
bandwidth 2000
int s0/0/1
bandwidth 64
show ip route eigrp
```
#### in router 2
```
en
conf t
int s0/0/0
bandwidth 2000
int s0/0/1
bandwidth 2000
```
#### in router 3
```
en 
conf t
int s0/0/0
bandwidth 64
int s0/0/1
bandwidth 2000
show interface s0/0/0
show interface s0/0/1
```
#### in router 2
```
show ip route eigrp
```
#### in router 1
```
en
conf t
router eigrp 10
passive-interface g0/0
```
#### in router 2
```
en
conf t
router eigrp 10
passive-interface g0/0
```
#### in router 3
```
en
conf t
router eigrp 10
passive-interface g0/0
```




