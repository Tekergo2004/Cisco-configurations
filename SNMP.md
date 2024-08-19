# SNMP

> [!NOTE]
> Set up connection to your SNMP server.

```cisco
snmp-server group ADMIN v3 priv
snmp-server user ADMIN ADMIN v3 auth md5 Passw0rd priv aes 256 Passw0rd
snmp-server location  <XYZ>
```
