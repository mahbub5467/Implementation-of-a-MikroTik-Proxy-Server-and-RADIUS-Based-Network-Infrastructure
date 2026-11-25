# CCProxy 8.0
- Version shown as CCProxy 8.0 (unregistered); main window controls include Start, Stop, Options, Account, Register, Monitor, Hide, Help.
- Services noted: Mail, DNS, Port Map.
- Ports: HTTP/RTSP 808; Secure 808; FTP(Web) 808; SOCKS/MMS 1080; FTP 2121; Telnet 23; News 119.
- Local IP auto-detected: `192.168.106.1`.
- Enabled account/group `LAN`; IP/range `192.168.106.1`; password enabled but omitted; unlimited connections and bandwidth (-1).
- Allowed services: WWW, Mail, Telnet, FTP, SOCKS, Others.
- Web filter `WebFilter-1`; Site Filter enabled; Forbidden Sites: `*.facebook.com`, `facebook.com`, `fb.com`.
- Connection window showed 30 connections, 1 user, user `LAN`, HTTPS CONNECT entries to port 443 including `www.youtube.com`.
- Chrome prompted for credentials for `http://192.168.106.1:808`.

This evidences explicit proxy use by the tested browser, not transparent interception or forced routing of all network traffic.
