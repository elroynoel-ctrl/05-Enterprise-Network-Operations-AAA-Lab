# Verification and Test Results

## Commands

```ios
show ip interface brief
show interfaces trunk
show vlan brief
show ip route
show running-config | section ^aaa
show running-config | section ^line
show running-config | section radius
show running-config | section tacacs
show privilege
show clock
show startup-config
```

Endpoint checks:

```text
ipconfig /all
ping 192.168.99.10
nslookup nms.careerhq.local
ssh -l <AAA_USER> 192.168.199.2
ssh -l <AAA_USER> 10.0.12.2
```

## Test matrix

| Test | Target | Expected | Observed |
|---|---|---|---|
| Valid RADIUS credentials | SW2 | Central login succeeds | Pass |
| Invalid RADIUS password | SW2 | Rejection; no local fallback | Pass |
| RADIUS unavailable | SW2 | Local break-glass succeeds | Pass |
| RADIUS restored | SW2 | Central login works again | Pass |
| Valid TACACS+ credentials | R2 | Central login succeeds | Pass |
| Invalid TACACS+ password | R2 | Rejection; no local fallback | Pass |
| TACACS+ unavailable | R2 | Local break-glass succeeds | Pass |
| TACACS+ restored | R2 | Central login works again | Pass |
| Privilege elevation | R2 | `enable`, then privilege 15 | Pass |
| TACACS+ traffic visibility | Simulation | Events traverse R2–NMS path | Pass |
| RADIUS accounting records | Server-PT | Start/stop records visible | Not exposed |
| TACACS+ PDU classification | Simulation | Identify AAA function | Detail unavailable |

## Interpretation

`group ... local` is failover, not a bypass for rejected credentials. Local authentication is attempted when the centralized method cannot respond, not when it responds with a denial.

Packet Tracer entered user EXEC after login. `enable` and `show privilege` confirmed privilege 15. Production TACACS+ can assign privileged EXEC through returned authorization attributes; that was not demonstrated here.
