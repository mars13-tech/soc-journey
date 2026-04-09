# Networking Cheat Sheet — SOC L2 Reference

## OSI Model
| Layer | Name | Protocol/Example | SOC Relevance |
|---|---|---|---|
| 7 | Application | HTTP, DNS, FTP | Most attacks happen here |
| 6 | Presentation | SSL/TLS, JPEG | Encryption/decryption |
| 5 | Session | NetBIOS, RPC | Session hijacking |
| 4 | Transport | TCP, UDP | SYN flood, port scanning |
| 3 | Network | IP, ICMP | IP spoofing, routing |
| 2 | Data Link | Ethernet, ARP | ARP spoofing, MAC flooding |
| 1 | Physical | Cables, WiFi | Physical access attacks |

## TCP 3-Way Handshake
Client → Server: SYN
Server → Client: SYN-ACK  
Client → Server: ACK
Attack: SYN Flood = send millions of SYN, never complete = server exhausted

## Key Protocols
- DNS Port 53 — translates domain to IP — Attack: DNS poisoning, tunneling
- DHCP Port 67/68 — assigns IP to devices — Attack: Rogue DHCP server
- ARP — maps IP to MAC — Attack: ARP spoofing (MITM)
- HTTP Port 80 — unencrypted web — Attack: MITM, injection
- HTTPS Port 443 — encrypted web — Attack: SSL stripping, cert forgery
- SMB Port 445 — file sharing — Attack: EternalBlue, ransomware spread
- RDP Port 3389 — remote desktop — Attack: Brute force, BlueKeep

## Ports Every SOC Analyst Knows
21=FTP | 22=SSH | 23=Telnet | 25=SMTP | 53=DNS   
80=HTTP | 110=POP3 | 143=IMAP | 443=HTTPS | 445=SMB   
1433=MSSQL | 3306=MySQL | 3389=RDP | 5985=WinRM | 8080=HTTP-alt
