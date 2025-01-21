# DMVPN

> [!NOTE]
> In this configuration I provide DMVPN Phase 3 configuration, with IPSEC IKEv2 security using PSK.


```cisco
hostname HUB

crypto isakmp policy 1
  authentication pre-share

crypto isakmp key KKK-DMVPN address 0.0.0.0     
   
crypto ipsec transform-set trans2 esp-sha512-hmac esp-3des
  mode transport

crypto ipsec profile DMVPN
  set transform-set trans2

interface Tunnel1
  ip address 10.0.0.1 255.255.255.0
  ip mtu 1400
  ip nhrp authentication test
  ip nhrp map multicast dynamic
  ip nhrp network-id 100000
  ip nhrp holdtime 600
  delay 1000
  tunnel source g0/0
  tunnel mode gre multipoint
  tunnel key 100000
  tunnel protection ipsec profile DMVPN
exit
```

```cisco
hostname Spoke<n>

crypto isakmp policy 1
  authentication pre-share

crypto isakmp key KKK-DMVPN address 0.0.0.0 0.0.0.0       

crypto ipsec transform-set trans2 esp-3des esp-sha512-hmac 
  mode transport

crypto ipsec profile DMVPN
  set transform-set trans2

interface Tunnel1
  ip address 10.0.0.<n+1> 255.255.255.0
  ip mtu 1400
  ip nhrp authentication test
  ip nhrp map multicast <Hub public ipv4 address>
  ip nhrp map <Hub tunnel ipv4 address> <Hub public ipv4 address>
  ip nhrp network-id 100000
  ip nhrp holdtime 300
  ip nhrp nhs <Hub tunnel ipv4 address>
  delay 1000
  tunnel source g0/0
  tunnel mode gre multipoint
  tunnel key 100000
  tunnel protection ipsec profile DMVPN
  no ip split-horizon eigrp 100
  no ip next-hop-self eigrp 100
exit

router eigrp 100
  network 10.0.0.0 0.0.0.255
  network 192.168.<n+1>.0 0.0.0.255
```
