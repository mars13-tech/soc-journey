# Security Concepts — SOC L2 Reference

## CIA Triad
| Pillar | Definition | Attack | Log Evidence |
|---|---|---|---|
| Confidentiality | Authorized access only | Phishing, data breach | Unusual DB access at odd hours |
| Integrity | Data not tampered | Log clearing (Event 1102) | FIM alert, hash mismatch |
| Availability | Systems accessible | DDoS, ransomware | Traffic spike, 503 errors |

## Threat Actors
| Type | Motivation | Example |
|---|---|---|
| Nation-State | Espionage | APT28, Lazarus Group |
| Cybercriminal | Money | LockBit, REvil, FIN7 |
| Insider | Revenge/gain | Disgruntled employee |
| Hacktivist | Political | Anonymous |

## Malware Quick Reference
- Virus: attaches to files, user opens it
- Worm: self-spreads, no user needed (WannaCry = SMB 445)
- Trojan/RAT: disguised legit app, full remote control (Emotet)
- Ransomware: encrypts files, demands money (T1486)
- Spyware: silent screen/keystroke capture
- Rootkit: hides in kernel, makes malware invisible
- Keylogger: every keystroke captured (Agent Tesla)
- Botnet: C2-controlled army of infected machines (Mirai)

## Phishing Types
- Phishing = mass email
- Spear Phishing = specific target with personal details
- Whaling = C-suite executives only
- Vishing = voice/phone call
- Smishing = SMS text
- BEC = impersonate CEO, demand wire transfer
- Clone Phishing = real email duplicated, link swapped

## OWASP Top 10 (SOC View)
A01 Broken Access Control — 200 OK on admin by non-admin
A02 Crypto Failures — password in HTTP cleartext
A03 Injection — SQL keywords in URL, WAF alert, 500 errors
A04 Insecure Design — mass abuse of specific feature
A05 Misconfiguration — default creds, /admin exposed externally
A06 Vulnerable Components — CVE exploit pattern in IDS
A07 Auth Failures — 800 failed logins then 1 success same IP
A08 Data Integrity — new C2 connection after software update
A09 Logging Failures — no logs from critical server
A10 SSRF — internal IP or 169.254.x.x in request params
