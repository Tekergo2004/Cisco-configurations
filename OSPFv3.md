# OSPFv3

> [!NOTE]
> Enable ipv6 routing

```cisco
ipv6 unicast-routing
```

> [!NOTE]
> Enable OSPFv3 on interfaces, you have to give IP address to your interfaces or just enable ipv6 and use link local, but then you have to give first link local and normal IPv6 address to your loopback interface

```cisco
int lo0
no sh
ip add 10.8.8.1 255.255.255.255
ipv6 add fe80:2:2::2:2 link-local
ipv6 add 2001:db8:8:8::1
ipv6 ospf 42 area 0
exit

int range g0/0-4
ipv6 enable (or assign other IPv6 address)
ipv6 ospf 42 area 0
no sh
exit
```


> [!NOTE]
> Enable password authentication, you have to do it on every ospf interface

```cisco
router ospfv3 42
area 10 authentication ipsec spi 256 md5 0 1234567891234567912345678912345
```
