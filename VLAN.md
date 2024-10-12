# VLAN

## Create VLANs

> [!NOTE]
> Creating VLANs is an easy method, but if you will use more VLANs create a talbe containing the numbers, the names and the ip addresses. It is recommend to use uppercase letters in the name.

```cisco
vlan 100
name MANAGEMENT
exit
```

## Create VLAN interfaces

> [!NOTE]
> It's used for management, and on L3 switches for Inter-VLAN routing.

```cisco
int vlan 100
no sh
ip address 10.10.100.1 255.255.255.0
ipv6 enable
ipv6 address 2001:10:10:100::1/64
exit
```

## Configuring access switchports

> [!NOTE]
> Configuring access ports.

```cisco
int range g0/1-24
sw mode acc
sw acc vl 200
exit
```

## Configuring trunk switchports

> [!NOTE]
> Configure a port on each site. It is recommend to use other than the default native VLAN, and allow just your VLAN-s over the trunking.

```cisco
int t0/1
sw mode trunk
sw trunk al vl 100,101,102
sw trunk nat vl 99
```

> [!NOTE]
> If you get an error because of dot1q encapsulation then you can switch to that with the following command. 

```cisco
int t0/1
sw trunk enc dot1q
```

