# Certificates

> [!NOTE]
> Copy your `.pfx` file for using to your router. You have to create them on a server or use a router to be the CA.

```cisco
copy scp: flash:
```

```cisco
crypto pki trustpoint PAIN-CA
 enrollment terminal
 revocation-check none
 rsakeypair PAIN-CA
exit
```

```cisco
crypto pki import PAIN-CA pkcs12 flash:/IR1.pfx password Passw0rd
```

```cisco
crypto pki certificate map PAIN-CMAP 1
 issuer-name co pain fr s.a. root ca
exit
```

```cisco
crypto ikev2 proposal PAIN-IKE-PROP 
 encryption aes-cbc-256
 integrity sha512
 group 24
exit
```

```cisco
crypto ikev2 policy PAIN-IKE-POLICY 
 proposal PAIN-IKE-PROP
exit
```

```cisco
crypto ikev2 profile PAIN-IKE-PROF
 match certificate PAIN-CMAP
 authentication remote rsa-sig
 authentication local rsa-sig
 pki trustpoint PAIN-CA
exit
```

```cisco
crypto ipsec transform-set PAIN-TSET esp-aes 256 esp-sha512-hmac 
 mode tunnel
exit
```

```cisco
crypto ipsec profile PAIN-IPSEC-PROF
 set transform-set PAIN-TSET 
 set ikev2-profile PAIN-IKE-PROF
exit
```
