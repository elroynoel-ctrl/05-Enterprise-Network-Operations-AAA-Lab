# Network Design

## Devices and roles

| Device | Role | Important address |
|---|---|---|
| R1 | Main-site router and inter-VLAN gateway | `10.0.12.1/30` |
| ACCESS-SWITCH | Main-site access switch | `192.168.99.2/24` |
| NMS-SERVER | DHCP, DNS, NTP, Syslog, SNMP manager, AAA | `192.168.99.10/24` |
| ADMIN-PC | Administrative workstation | `192.168.99.20/24` |
| USER-PC | Main-site endpoint | `192.168.10.20/24` |
| R2 | Branch router and TACACS+ test target | `10.0.12.2/30` |
| SW2 | Branch switch and RADIUS test target | `192.168.199.2/24` |
| BRANCH-PC | Branch endpoint | DHCP; observed `192.168.20.100` |

The topology label says `ACCESS-SWITCH`; the captured IOS hostname remained `Switch`. This mismatch is preserved as an observed naming issue.

## Routing and switching

- R1 provides gateways for VLANs 10 and 99 using subinterfaces.
- R2 provides gateways for VLANs 20 and 199 using subinterfaces.
- VLAN 999 is native on router-facing trunks and has no Layer 3 address.
- R1 and R2 use reciprocal static routes across `10.0.12.0/30`.
- R2 relays branch DHCP broadcasts to `192.168.99.10`.

## Management services

The NMS server centralizes DNS, NTP, Syslog, SNMP management, RADIUS, and TACACS+. Devices point to `192.168.99.10`. DNS includes `nms.careerhq.local` mapped to that address.

## AAA design

SW2 tests RADIUS authentication and EXEC accounting. R2 tests TACACS+ authentication, default EXEC authorization, and EXEC accounting. Both method lists place `local` after the centralized method for server-unavailable break-glass access.
