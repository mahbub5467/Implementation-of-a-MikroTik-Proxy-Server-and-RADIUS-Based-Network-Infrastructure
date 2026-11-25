# Chapter 07 to the End — Complete Report-Based Documentation

Source: *Final internship report.pdf*, printed report pages 82–139 (PDF pages 97–154). This file follows the report's order and records all substantive implementation steps, figure evidence, values, and the final references. Minor spelling/numbering inconsistencies in the source are noted rather than silently corrected.

## Chapter 07 — RADIUS Server Management (NPS)
**Report pages 82–100; Figures 7.1–7.18**

### 7.1–7.4 Background, purpose, objectives and requirements
NPS on Windows Server is used as the RADIUS service for centralized Authentication, Authorization and Accounting (AAA), particularly for Wi-Fi/802.1X. The chapter's stated objectives are:
1. Install and configure NPS as a RADIUS server.
2. Integrate NPS with Active Directory Domain Services (AD DS).
3. Create domain users and a wireless access group.
4. Configure RADIUS clients (MikroTik and wireless access point).
5. Create a wireless authentication Network Policy.
6. Assign VLAN using RADIUS attributes.
7. Enable accounting and logging.

Requirements named: Windows Server evaluation installation, AD DS, DNS Server, DHCP Server, Network Policy and Access Services, MikroTik router / wireless access point, and Wi-Fi client test devices.

### 7.5 Install the NPS role
Server Manager → Manage → Add Roles and Features → Role-based or feature-based installation → choose destination server → Network Policy and Access Services → complete wizard → Install.
Evidence: Figure 7.1 initial Server Manager dashboard; 7.2 after role installation; 7.3 role selection.

### 7.6 Verify Active Directory domain
Open Active Directory Users and Computers (ADUC), inspect domain structure and domain properties, and verify domain and forest functional levels.
Evidence: Figures 7.4 and 7.5.

### 7.7–7.9 Create users and wireless security group
- Create domain users in the selected OU using ADUC → New → User.
- Create a Security Group named `wireless users`.
- Add `user1`, `user2`, `user3`, and `user4` to the group.
Evidence: Figures 7.6–7.9 (user list, group, membership and adding members).

### 7.10 Open NPS
Server Manager → Tools → Network Policy Server; confirm local NPS console is available.
Evidence: Figure 7.10.

### 7.11 Register MikroTik as RADIUS client
NPS (Local) → RADIUS Clients and Servers → RADIUS Clients → New. Client name/device: MikroTik; IP address: `10.10.10.253`; configure a manually entered shared secret. The secret is intentionally not reproduced here.
Evidence: Figure 7.11.
**Note:** the prose names MikroTik as the configured client; the chapter's objectives also mention the access point as a RADIUS client, while the explicit step and figure provide the MikroTik address.

### Network Policy — “Secure Wireless Connections”
Create/enable the policy named `Secure Wireless Connections`; set Access Permission to Allow access; select “Ignore user account dial-in properties”.
Conditions:
- NAS Port Type: `Wireless – IEEE 802.11`
- Windows group: `TEST\\wireless users`
Evidence: Figures 7.12–7.14.

### 7.13 Time restrictions
Policy Properties → Constraints → Day and Time Restrictions; configure the permitted/denied schedule shown in Figure 7.15. The report does not transcribe exact hours/days, so do not invent them.

### 7.14 Authentication methods
Enable Microsoft Protected EAP (PEAP), using EAP-MSCHAPv2 as the secured password method. The report also lists MS-CHAPv2 and MS-CHAP under optional/less-secure methods.
Evidence: Figure 7.16.

### 7.15 RADIUS VLAN attributes
Configured standard attributes:
- `Framed-Protocol = PPP`
- `Service-Type = Framed`
- `Tunnel-Medium-Type = 802`
- `Tunnel-Pvt-Group-ID = 20`
- `Tunnel-Type = Virtual LANs (VLAN)`
Evidence: Figure 7.17.

### 7.16 Accounting and logging
NPS → Accounting → Configure Accounting → log to a text file on the local computer.
Evidence: Figure 7.18.

## Chapter 08 — Implementation of New Network Infrastructure
**Report pages 101–112; Figures 8.1–8.14**

### 8.1 Interface and VLAN setup
MikroTik RouterOS used for LAN/WAN, bridge, VLAN interfaces, IP addressing, DNS, DHCP, NAT, routing and connectivity testing. Figure 8.1 shows LAN, WAN, bridge and VLAN interfaces `vlan20`, `vlan30`, `vlan40`, `vlan50`.

### 8.2 IP addressing
- WAN address shown: `163.47.37.228/29` (Figure 8.4).
- LAN address shown: `10.10.10.1/24` (Figure 8.5).
- Address list includes LAN, VLAN and WAN addresses (Figure 8.2).
The report does not list every VLAN interface address in this chapter.

### 8.3 Bridge
Create and run `bridge1` to combine physical ports into a logical interface / internal LAN switching function. Figures 8.3 and 8.6.

### 8.4 DNS
DNS server set to `8.8.8.8`; remote DNS requests enabled. Figure 8.7.

### 8.6 DHCP
DHCP servers configured for LAN and VLAN interfaces; Figure 8.8 specifically shows DHCP configuration for `vlan20`. DHCP distributes IP, gateway and DNS parameters. (The source jumps from section 8.4 to 8.6; no 8.5 heading is present in the extracted report.)

### 8.7 NAT
Configure source NAT masquerade with outbound interface WAN to permit internal LAN/VLAN clients to access external networks. Figure 8.9.

### 8.8 IP pools
Create distinct address pools for LAN and VLAN subnets. Figure 8.10.

### 8.9 Routing
Inspect route list, default route `0.0.0.0/0` via WAN, and connected VLAN routes. Report states both dynamic and static route information is present. Figure 8.11.

### 8.10 Connectivity test
MikroTik terminal ping to `8.8.8.8` succeeds in the report. Figure 8.12.

### 8.11 Terminal verification
Use `/ip address print` and `/ip route print` to inspect assigned addresses and routing table. Figure 8.13.

### 8.12 RIP
RIP enabled on LAN interface; network `10.10.10.0/24` included; Figure 8.14 indicates RIP v1/v2. This documents configuration, not proof of a multi-router RIP adjacency.

## Chapter 09 — UniFi WPA2-Enterprise / RADIUS
**Report pages 113–121; Figures 9.1–9.9**

1. Create/access Ubiquiti administrative account for UniFi management (Figure 9.1).
2. Select UAP-AC-Pro in UniFi Controller and start adoption (Figure 9.2).
3. Confirm adoption progress/status (Figure 9.3).
4. Create wireless network / SSID (Figure 9.4). SSID value is not transcribed in report.
5. Set security to WPA2-Enterprise and select a RADIUS profile (Figure 9.5).
6. Assign a VLAN ID to the wireless network (Figure 9.6); architecture chapter identifies this as VLAN 20.
7. Configure RADIUS profile with server IP, shared secret, authentication UDP port `1812`, accounting enabled and accounting UDP port `1813` (Figure 9.7). Server IP and secret are not reproduced.
8. Review UniFi topology to see AP and wireless clients (Figure 9.8).
9. Review client list, IP addresses, connection type and client status (Figure 9.9).

## Chapter 10 — Proxy Server (CCProxy 8.0)
**Report pages 122–128; Figures 10.1–10.6**

### 10.1 Main window
Opened CCProxy 8.0 (unregistered). Main controls shown: Start, Stop, Options, Account, Register, Monitor, Hide, Help; green activity graph indicates proxy is running/ready. Figure 10.1.

### 10.2 Services and ports
Enabled services noted in report include Mail, DNS and Port Map. Ports shown:
| Service | Port |
|---|---:|
| HTTP/RTSP | 808 |
| Secure | 808 |
| FTP(Web) | 808 |
| SOCKS/MMS | 1080 |
| FTP | 2121 |
| Telnet | 23 |
| News | 119 |
Local IP auto-detection enabled; displayed address `192.168.106.1`. Figure 10.2.

### 10.3 Account
Account/group name `LAN`; enabled; password enabled (actual password not included); IP address/range `192.168.106.1`; unlimited connections (`-1`) and unlimited upload/download bandwidth (`-1`). Allowed services shown: WWW, Mail, Telnet, FTP, SOCKS, Others. Web Filter `WebFilter-1` enabled. Figure 10.3.

### 10.4 Web filtering
Filter `WebFilter-1`; Site Filter enabled; Forbidden Sites selected. Block entries: `*.facebook.com`, `facebook.com`, `fb.com`. Figure 10.4.

### 10.5 Connection information
Captured view shows 30 connections and 1 user; username `LAN`; IP `192.168.106.1`; HTTPS CONNECT entries to port 443, including `www.youtube.com`. Figure 10.5.

### 10.6 Browser proxy authentication
Chrome displays a prompt that proxy `http://192.168.106.1:808` requires username and password. This demonstrates that the browser was configured to use the explicit proxy and that authentication was requested. Figure 10.6.

**Scope qualification:** The evidence supports explicit proxy use by the tested browser. It does not alone establish transparent proxying or enforcement of all network traffic through CCProxy.

## Chapter 11 — Network Architecture
**Report pages 129–134; Figure 11.1**

### 11.1 Architecture components
The report lists:
1. Wireless clients/users
2. UniFi Access Point (UAP-AC-Pro)
3. MikroTik Router (RouterOS)
4. Windows Server NPS (RADIUS)
5. CCProxy Server (content filtering and monitoring)
6. Internet / ISP connection

Figure 11.1 illustrates wireless users, MikroTik routing, RADIUS authentication and CCProxy filtering.

### 11.2 VLAN 20 wireless segmentation
- VLAN ID: `20`
- Subnet: `20.20.20.0/24`
- MikroTik gateway: `20.20.20.1`
The report says this logically isolates wireless users from other internal networks.

### 11.3 WPA2-Enterprise + RADIUS flow
1. Wireless client joins the SSID configured for VLAN 20.
2. UniFi AP forwards authentication request to Windows NPS using RADIUS.
3. NPS validates credentials, typically via Active Directory or local user database.
4. Successful authentication grants wireless access.

### 11.4 MikroTik routing, DHCP and NAT
- DHCP assigns a VLAN 20 client address after successful authentication.
- Router routes traffic between VLAN 20 and required network segments and towards proxy / Internet gateway.
- Source NAT masquerade on WAN enables private VLAN 20 addresses to access external networks.

### 11.5 CCProxy integration
CCProxy role is described as web filtering/content restriction, user activity monitoring/reporting, bandwidth monitoring and Internet access policy enforcement. The architecture text says wireless web traffic is directed through CCProxy; however, Chapter 10's explicit browser proxy prompt is the concrete evidence of explicit proxy use. Do not claim transparent enforcement unless separately tested.

### 11.6 End-to-end flow as stated in report
1. Wireless Client → UniFi AP (Wi-Fi via VLAN 20)
2. UniFi AP → NPS (RADIUS authentication)
3. Successful authentication → MikroTik DHCP assigns IP
4. Client traffic → MikroTik (routing + NAT)
5. MikroTik → CCProxy (filtering + monitoring)
6. CCProxy → Internet (filtered access)

## Chapter 12 — Conclusion
**Report page 136**
The report concludes with internship learning: practical experience, communication and working with people, professional growth, understanding of computer network systems, and acknowledgement that the project/report may still have limitations despite best efforts.

## References
**Report pages 138–139; all 16 references**
1. ElProCus (2020), “Network devices in computer network: Different types” — https://www.elprocus.com/what-are-network-devices-and-their-types/
2. Fortinet (2021), “What is a DMZ and why would you use it?” — https://www.fortinet.com/resources/cyberglossary/what-is-dmz
3. GeeksforGeeks (2017), “Types of network topology” — https://www.geeksforgeeks.org/types-of-network-topology/
4. Imperva (2021), “What is OSI model? 7 layers explained” — https://www.imperva.com/learn/application-security/osi-model/
5. IPXO (2021), “What is a subnet mask? A beginner’s guide to subnetting” — https://www.ipxo.com/blog/what-is-subnet-mask/
6. Kaspersky (2021), “What is an IP address? Definition and explanation” — https://www.kaspersky.com/resource-center/definitions/what-is-an-ip-address
7. McCauley (2019), “What is a computer network?” — https://www.fieldengineer.com/blogs/what-is-a-computer-network
8. Microsoft Learn, “Network Policy Server (NPS)” — https://learn.microsoft.com/en-us/windows-server/networking/technologies/nps/nps-top
9. Microsoft Learn, “RADIUS authentication and accounting (NPS)” — https://learn.microsoft.com/en-us/windows-server/networking/technologies/nps/nps-radius-clients
10. MikroTik, RouterOS documentation — https://help.mikrotik.com/docs/
11. Network Encyclopedia, “Cabling” — https://networkencyclopedia.com/cabling/
12. ScienceDirect Topics (2018), “Routing protocol – An overview” — https://www.sciencedirect.com/topics/computer-science/routing-protocol
13. Ubiquiti, UniFi Network documentation — https://help.ui.com/
14. University of South Florida (2013), “Chapter 4: Cabling” — https://fcit.usf.edu/network/chap4/chap4.htm
15. Wikipedia contributors (2021), “Regional Internet Registry” — https://en.wikipedia.org/wiki/Regional_Internet_registry
16. Williams (2020), “Types of computer network: What is LAN, MAN and WAN” — https://www.guru99.com/types-of-computer-network.html

## Report figure/evidence index (complete from Chapter 7 onward)
- Chapter 7: Figures 7.1–7.18 (18 figures), PDF pages 101–115.
- Chapter 8: Figures 8.1–8.14 (14 figures), PDF pages 117–127.
- Chapter 9: Figures 9.1–9.9 (9 figures), PDF pages 129–136.
- Chapter 10: Figures 10.1–10.6 (6 figures), PDF pages 138–143.
- Chapter 11: Figure 11.1, PDF page 146.
Total: 48 numbered figures in Chapters 7–11.

## Items intentionally not asserted
- No Kaspersky deployment/configuration is documented in these chapters; Kaspersky appears only as a reference about IP addresses.
- No actual credentials/shared secrets are reproduced.
- No full RouterOS export or complete per-VLAN address pool table is provided.
- No exact NPS time window or UniFi SSID is transcribed.
- No throughput, failover, penetration-test, or production-readiness result is claimed.
