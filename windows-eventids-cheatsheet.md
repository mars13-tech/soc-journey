# Windows Event IDs — SOC L2 Cheat Sheet

## CRITICAL — Memorize These First

| Event ID | Event Name | Severity | What to Look For |
|---|---|---|---|
| 4624 | Successful Logon | MEDIUM | Logon Type 3 (network) or 10 (RDP) from unusual IP |
| 4625 | Failed Logon | HIGH | 10+ failures from same IP = brute force |
| 4688 | Process Created | HIGH | cmd/powershell spawned by Office or browser |
| 4720 | User Account Created | CRITICAL | Any new account = possible persistence |
| 4732 | Added to Security Group | CRITICAL | Added to Administrators = privilege escalation |
| 4648 | Explicit Credential Logon | HIGH | Pass-the-hash indicator |
| 4672 | Admin Privileges Assigned | HIGH | SeDebugPrivilege = credential dumping prep |
| 4698 | Scheduled Task Created | HIGH | Persistence mechanism |
| 1102 | Audit Log Cleared | CRITICAL | Attacker covering tracks — escalate immediately |
| 4104 | PowerShell Script Block | HIGH | Encoded/obfuscated PS = almost always malicious |

## Logon Types (Event ID 4624)
| Type | Name | SOC Meaning |
|---|---|---|
| 2 | Interactive | Physical login — normal |
| 3 | Network | SMB/file share — watch for lateral movement |
| 4 | Batch | Scheduled task |
| 5 | Service | Service account |
| 10 | RemoteInteractive | RDP — always investigate |

## Suspicious Parent→Child Process Pairs
- winword.exe → cmd.exe = MACRO ATTACK
- chrome.exe → powershell.exe = DRIVE-BY DOWNLOAD  
- cmd.exe → powershell.exe -enc = ENCODED PAYLOAD
- mshta.exe → powershell.exe = LOLBIN ABUSE
- services.exe → unknown.exe = MALWARE SERVICE

## Splunk Queries
```
Brute Force: index=wineventlog EventCode=4625 | stats count by Source_Network_Address | where count > 10
Lateral Movement: index=wineventlog EventCode=4624 Logon_Type=3 | stats count by src_ip Account_Name
Macro Attack: index=wineventlog EventCode=4688 Creator_Process_Name=*WINWORD* New_Process_Name=*cmd*
New Admin: index=wineventlog EventCode=4732 Group_Name=Administrators
Log Clear: index=wineventlog EventCode=1102
```
