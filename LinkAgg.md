# Link Aggregation

## PAGP

> [!NOTE]
> Cisco Link aggregation protocol

> [!IMPORTANT]
> SW1's configuration

```cisco
int range g0/1-2
channel-group 1 mode auto
exit
```

```cisco
int po1
sw mode trunk
sw trunk al vl 100,101,102
sw trunk nat vl 99
exit
```

> [!IMPORTANT]
> SW2's configuration

```cisco
int range g0/1-2
channel-group 1 mode desireable
exit
```

```cisco
int po1
sw mode trunk
sw trunk al vl 100,101,102
sw trunk nat vl 99
exit
```

## LACP

> [!NOTE]
> The non propiretary protocol for creating EtherChannel. (used commonly)

> [!IMPORTANT]
> SW1's configuration

```cisco
int range g0/1-2
channel-group 1 mode active
exit
```

```cisco
int po1
sw mode trunk
sw trunk al vl 100,101,102
sw trunk nat vl 99
exit
```

> [!IMPORTANT]
> SW2's configuration

```cisco
int range g0/1-2
channel-group 1 mode passive
exit
```

```cisco
int po1
sw mode trunk
sw trunk al vl 100,101,102
sw trunk nat vl 99
exit
```
