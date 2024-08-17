# HSRP configuration

## 1. step: Default (R1)

> [!NOTE]
> Default configuration for Cisco HSRP.

```cisco
int vlan 118
standby v 2
standby 1 prio 110
standby 1 ip 10.2.118.254
standby 1 authentication Passw0rd
standby 2 prio 110
standby 2 ipv6 fe80:2:118::1
standby 2 authentication Passw0rd
exit
```

```cisco
int vlan 202
standby v 2
standby 3 prio 110
standby 3 ip 10.2.202.254
standby 3 authentication Passw0rd
standby 4 prio 110
standby 4 ipv6 fe80:2:202::1
standby 4 authentication Passw0rd
exit
```

## 2. step: Tracking (on your active router - (R1)) 

> [!NOTE]
> Enchaned tracking configuration for HSRP.

```cisco
ip sla 1
icmp-echo 10.0.2.6
frequency 5
exit

ip sla 2
icmp-echo 2001:DB8:CAB:FFFF::2:3 source-ip 2001:DB8:CAB:FFFF::3:3
frequency 5
exit

ip sla 3
icmp-echo 10.0.2.10
frequency 5
exit

ip sla 4
icmp-echo 2001:DB8:CAB:FFFF::2:4 source-ip 2001:DB8:CAB:FFFF::3:3
frequency 5
exit
```

```cisco
ip sla schedule 1 life forever start-time now
ip sla schedule 2 life forever start-time now
ip sla schedule 3 life forever start-time now
ip sla schedule 4 life forever start-time now
```

```cisco
track 1 ip sla 1 reachability
exit

track 2 ip sla 2 reachability
exit

track 3 ip sla 3 reachability
exit

track 4 ip sla 4 reachability
exit
```

```cisco
int vlan 118
standby 1 preempt
standby 1 track 1 decrement 10
standby 1 track 3 decrement 10
standby 2 preempt
standby 2 track 2 decrement 10
standby 2 track 4 decrement 10
exit
```

```cisco
int vlan 202
standby 3 preempt
standby 3 track 1 decrement 10
standby 3 track 3 decrement 10
standby 4 preempt
standby 4 track 2 decrement 10
standby 4 track 4 decrement 10
exit
```

## 3. step: Configure more router (R2)

> [!NOTE]
> You will have at least on other Cisco router running HSRP, what will be your standby router.

```cisco
int vlan 118
standby v 2
standby 1 prio 100
standby 1 ip 10.2.118.254
standby 1 authentication Passw0rd
standby 2 prio 100
standby 2 ipv6 fe80:2:118::1
standby 2 authentication Passw0rd
exit
```

```cisco
int vlan 202
standby v 2
standby 3 prio 100
standby 3 ip 10.2.202.254
standby 3 authentication Passw0rd
standby 4 prio 100
standby 4 ipv6 fe80:2:202::1
standby 4 authentication Passw0rd
exit
```
