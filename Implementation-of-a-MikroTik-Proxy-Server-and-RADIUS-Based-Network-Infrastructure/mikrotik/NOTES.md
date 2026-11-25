# MikroTik RouterOS — report-derived notes
- Interfaces shown: LAN, WAN, `bridge1`, `vlan20`, `vlan30`, `vlan40`, `vlan50`.
- WAN address shown: `163.47.37.228/29`.
- LAN address shown: `10.10.10.1/24`.
- DNS: `8.8.8.8`; remote requests enabled.
- DHCP services and IP pools configured for LAN/VLANs; Figure 8.8 shows `vlan20`.
- Source NAT masquerade uses WAN as outbound interface.
- Default route `0.0.0.0/0` via WAN inspected.
- Successful ping to `8.8.8.8` shown.
- RIP enabled on LAN; `10.10.10.0/24` included; figure indicates RIP v1/v2.
- Chapter 11 identifies VLAN 20 as `20.20.20.0/24`, gateway `20.20.20.1`.

The report does not provide a full RouterOS export or every VLAN's subnet/pool. Do not invent a ready-to-paste config.
