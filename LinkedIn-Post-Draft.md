# LinkedIn Post Draft

I recently completed an enterprise network operations lab in Cisco Packet Tracer 9.0.1 while reviewing the direction of Cisco's announced CCNA v2.0 objectives.

The topology combines VLAN segmentation, router-on-a-stick, static routing, DHCP relay, DNS, NTP, Syslog, SNMP, and SSH with centralized administrative access using both RADIUS and TACACS+.

The most valuable part was testing behavior—not just entering commands:

- Valid centralized AAA authentication
- Explicit credential rejection versus server unavailability
- Local break-glass fallback
- EXEC authorization and privilege elevation
- Accounting configuration and simulator limitations
- Packet-flow verification in Simulation mode

One key takeaway: a local method at the end of an AAA method list is not a bypass for rejected credentials. It is used when the centralized server is unavailable. I also documented where Packet Tracer could show TACACS+ traffic but could not expose enough PDU or server-log detail to validate each accounting exchange.

The project repository includes a network design, sanitized configurations, verification matrix, troubleshooting notes, a RADIUS-versus-TACACS+ comparison, and CCNA v2.0 skill mapping.

This exercise reinforced an operations mindset: configure, test success, test failure, preserve recovery access, verify evidence, and state the limits of what the platform proves.

#Cisco #CCNA #PacketTracer #NetworkEngineering #Cybersecurity #RADIUS #TACACS #AAA #EnterpriseNetworking #CareerDevelopment
