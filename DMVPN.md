# DMVPN

> [!NOTE]
> This is a full configuartion for DMVPN, it's keys from <a href="https://github.com/Tekergo2004/Cisco-configurations/blob/main/IKEv2-IPSec.md">IKEv2-IPSec.md</a> and EIGRP is from <a href="https://github.com/Tekergo2004/Cisco-configurations/blob/main/EIGRP.md">EIGRP.md</a>

```cisco
interface Tunnel1
 ip address 10.200.1.1 255.255.255.0
 no ip redirects
 ip authentication mode eigrp 65100 md5
 ip authentication key-chain eigrp 65100 EIGRP
 ip nhrp authentication Passw0rd
 ip nhrp map multicast 65.23.77.1
 ip nhrp network-id 1
 ip nhrp nhs 10.200.1.254 nbma 65.23.77.1
 ipv6 address FDCC:AB:CD:1::1/64
 ipv6 enable
 no ipv6 redirects
 ipv6 eigrp 65100
 ipv6 authentication mode eigrp 65100 md5
 ipv6 authentication key-chain eigrp 65100 EIGRP
 ipv6 nhrp authentication Passw0rd
 ipv6 nhrp map multicast 65.23.77.1
 ipv6 nhrp network-id 1
 ipv6 nhrp nhs FDCC:AB:CD:1::DEF nbma 65.23.77.1
 ipv6 nhrp redirect
 tunnel source Dialer1
 tunnel mode gre multipoint
 tunnel key 1
 tunnel protection ipsec profile PAIN-IPSEC-PROF shared
exit
```

```cisco
interface Tunnel2
 ip address 10.200.2.1 255.255.255.0
 no ip redirects
 ip authentication mode eigrp 65100 md5
 ip authentication key-chain eigrp 65100 EIGRP
 ip nhrp authentication Passw0rd
 ip nhrp map multicast 65.23.77.3
 ip nhrp network-id 2
 ip nhrp nhs 10.200.2.254 nbma 65.23.77.3
 ipv6 address FDCC:AB:CD:2::1/64
 ipv6 enable
 no ipv6 redirects
 ipv6 eigrp 65100
 ipv6 authentication mode eigrp 65100 md5
 ipv6 authentication key-chain eigrp 65100 EIGRP
 ipv6 nhrp authentication Passw0rd
 ipv6 nhrp map multicast 65.23.77.3
 ipv6 nhrp network-id 1
 ipv6 nhrp nhs FDCC:AB:CD:2::DEF nbma 65.23.77.3
 ipv6 nhrp redirect
 tunnel source Dialer1
 tunnel mode gre multipoint
 tunnel key 2
 tunnel protection ipsec profile PAIN-IPSEC-PROF shared
```
