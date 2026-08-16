# Lessons Learned

- AAA method order matters. Local fallback follows server unavailability, not an authoritative rejection.
- Authentication and privilege are separate decisions. Successful SSH did not automatically grant privileged EXEC in this simulation.
- Default method lists may be necessary when a simulated platform lacks the corresponding line-level command.
- Configuration acceptance does not prove telemetry. Accounting commands were accepted, yet complete records could not be verified.
- Evidence needs precise claims. TACACS event screenshots prove traffic and path, not each message's purpose without PDU details.
- Public portfolio labs need a security review. Hashes, shared keys, community strings, server users, and `.pkt` contents may reveal credentials.
- Simulator limitations define what should be retested in Cisco Modeling Labs or production-equivalent IOS.

## Recommended next iteration

Rebuild the AAA portion in Cisco Modeling Labs with redundant AAA servers, modern server-group syntax, SNMPv3, management ACLs, SSH source-interface controls, command authorization, and server-side accounting log verification.
