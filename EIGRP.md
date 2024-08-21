# EIGRP

> [!NOTE]
> Eigrp configuration

```cisco
key chain EIGRP
 key 1
  key-string Passw0rd
```

```cisco
router eigrp 65100
 network 10.3.119.0 0.0.0.255
 network 10.3.203.0 0.0.0.255
 network 10.200.1.0 0.0.0.255
 network 10.200.2.0 0.0.0.255
 network 10.255.10.1 0.0.0.0
 eigrp stub connected summary
 redistribute ospf 42
```

```cisco
int g0/0
#ip authentication key-chain eigrp 65100 EIGRP
```


> ez a parancs meg kell
```cisco
no ip hori
```
