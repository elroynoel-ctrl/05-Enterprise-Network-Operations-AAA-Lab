# RADIUS versus TACACS+

| Dimension | RADIUS | TACACS+ |
|---|---|---|
| Lab target | SW2 | R2 |
| Typical transport | UDP | TCP |
| Lab port | UDP 1645 | TCP 49 |
| Encryption model | Password field protected; most attributes exposed | Encrypts packet body |
| AAA separation | Authentication and authorization commonly coupled | Authentication, authorization, accounting separated |
| Command authorization | Limited device-administration fit | Strong fit for per-command policy |
| Common use | Network access and device login | Administrative device access |
| Lab accounting visibility | Config accepted; no usable record exposed | Events visible; purpose not classifiable |

## Operational conclusion

RADIUS demonstrated centralized login and fallback behavior on the switch. TACACS+ was the better conceptual fit for router administration because it separates AAA functions and supports granular command authorization in production. Packet Tracer was adequate for configuration practice and behavioral tests, but not complete accounting validation.
