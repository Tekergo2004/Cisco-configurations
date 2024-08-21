# PPPoe

> [!NOTE]
> Deafult configuration of PPPoe

## Server

```cisco
ip local pool PPPOEPool 35.44.12.1 35.44.12.30
```


```cisco
username client password Passw0rd
```

```cisco
interface Virtual-Template1
 mtu 1492
 ip unnumbered Loopback0
 peer default ip address pool PPPOEPool
 ppp authentication pap chap
exit
```

```cisco
bba-group pppoe global
 virtual-template 1
exit
```

## Client

```cisco
interface Dialer1
 mtu 1492
 ip address negotiated
 encapsulation ppp
 dialer pool 1
 ppp pap sent-username customer password 0 Passw0rd
 ppp ipcp route default
```
