# Troubleshooting Notes

## Authentication list mismatch

R2's VTY initially referenced `SSH-RADIUS`. It was corrected and verified:

```ios
line vty 0 4
 login authentication SSH-TACACS
!
show running-config | section ^line
```

## Named EXEC authorization unavailable

Packet Tracer accepted creation of a named list but lacked `authorization exec` under line configuration. The compatible solution was:

```ios
aaa authorization exec default group tacacs+ local if-authenticated
```

## Startup filtering unavailable

The simulated IOS rejected piped `show startup-config | section ...`. The complete `show startup-config` command was used.

## PDU Details unavailable

Simulation mode showed protocol events, but detailed AAA fields could not be opened. Screenshots prove protocol visibility and path traversal—not the semantic classification of every exchange.

## Hardening observations

- R1 and the access switch have bare `login` statements without a documented VTY password or SSH-only method.
- The access switch hostname remains `Switch` despite its topology label.
- Replace SNMPv2c with SNMPv3 in production.
- Restrict management access with ACLs and source-interface controls where supported.
