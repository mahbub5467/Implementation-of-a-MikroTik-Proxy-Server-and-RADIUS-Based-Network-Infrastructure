# Validation checklist

- [ ] Verify MikroTik LAN/WAN/bridge/VLAN interfaces and addresses.
- [ ] Verify DNS `8.8.8.8`, remote DNS setting, DHCP servers and IP pools.
- [ ] Verify WAN masquerade, default route and RIP configuration.
- [ ] Repeat and record ping to `8.8.8.8`.
- [ ] Verify NPS RADIUS client IP and shared secret locally.
- [ ] Verify `Secure Wireless Connections` policy, group condition and time restrictions.
- [ ] Verify PEAP/EAP-MSCHAPv2, VLAN 20 attributes and accounting log.
- [ ] Verify UniFi AP adoption, WPA2-Enterprise, RADIUS 1812/1813 and VLAN 20.
- [ ] Verify CCProxy services, account, forbidden-sites filter, authentication prompt and logs.

Record date, software version, actual observed result, Pass/Fail/Not tested, and sanitized evidence. Only mark tests passed after repeating them.
