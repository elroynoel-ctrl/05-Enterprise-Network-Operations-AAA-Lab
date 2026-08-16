# Configuration Guide

## Baseline services

```ios
interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
 ip helper-address 192.168.99.10

logging 192.168.99.10
ntp server 192.168.99.10
snmp-server community <SNMP_COMMUNITY> RO
```

## RADIUS on SW2

```ios
aaa new-model
aaa authentication login SSH-RADIUS group radius local
aaa accounting exec SSH-ACCOUNTING start-stop group radius
radius-server host 192.168.99.10 auth-port 1645
radius-server key <RADIUS_SHARED_SECRET>

line vty 0 4
 login authentication SSH-RADIUS
 accounting exec SSH-ACCOUNTING
 transport input ssh
line vty 5 15
 login authentication SSH-RADIUS
 accounting exec SSH-ACCOUNTING
 transport input ssh
```

## TACACS+ on R2

```ios
aaa new-model
aaa authentication login SSH-TACACS group tacacs+ local
aaa authorization exec default group tacacs+ local if-authenticated
aaa accounting exec SSH-TACACS-ACCOUNTING start-stop group tacacs+
tacacs-server host 192.168.99.10
tacacs-server key <TACACS_SHARED_SECRET>

line vty 0 4
 login authentication SSH-TACACS
 accounting exec SSH-TACACS-ACCOUNTING
 transport input ssh
```

Packet Tracer's R2 line configuration did not support applying a named `authorization exec` list. The default EXEC authorization list was used globally.

## Break-glass and persistence

```ios
username admin privilege 15 secret <LOCAL_ADMIN_SECRET>
enable secret <ENABLE_SECRET>
copy running-config startup-config
```

Fallback is intended for an unavailable AAA server. A reachable server's explicit rejection terminates the method list and does not proceed to `local`.

See `configs/` for complete sanitized configurations.
