# RADIUS

```cisco
aaa new-model

radius server HQ-SVR1
 address ipv4 10.1.21.12 auth-port 1812 acct-port 1813
 key Passw0rd

aaa group server radius HQ-RADIUS
 server name HQ-SVR1

aaa authentication login default group HQ-RADIUS local
aaa authorization exec default group HQ-RADIUS local
```

> [!NOTE]
> Create backup user

```cisco
username backup priv 15 password Passw0rd
```
