# 🚨 Malware Traffic Analysis Report

## 1. Executive Summary

Analysis of the provided PCAP revealed that an internal host was infected and communicating with external malicious infrastructure. The traffic indicates the use of a Remote Access Trojan (RAT) leveraging HTTP for command-and-control (C2) communication. Evidence suggests abuse of NetSupport Manager as a RAT.

---

## 2. Victim Information

* Victim IP: 10.11.26.183
* Network Type: Internal (Private IP range)

---

## 3. Attacker Infrastructure

* Delivery IP: 193.42.38.139
* C2 IP: 194.180.191.64
* Malicious Domain: modandcrackedapk.com

---

## 4. Malware Communication Details

* Protocol: HTTP
* Endpoint: http://194.180.191.64/fakeurl.htm
* Method: POST
* User-Agent: NetSupport Manager/1.3

Observed commands:

* CMD=POLL → Beaconing / check-in
* CMD=ENCD → Encoded data exchange

Server Response:

* NetSupport Gateway/1.8 (Windows NT)

---

## 5. Indicators of Compromise (IOCs)

### IP Addresses

* 193.42.38.139
* 194.180.191.64

### Domain

* modandcrackedapk.com

### URI

* /fakeurl.htm

### User-Agent

* NetSupport Manager/1.3

---

## 6. Timeline of Events

| Time (Approx) | Event                                              |
| ------------- | -------------------------------------------------- |
| T1            | DNS query to modandcrackedapk.com                  |
| T2            | Domain resolved to 193.42.38.139                   |
| T3            | Initial communication with external infrastructure |
| T4            | Repeated HTTP POST requests to 194.180.191.64      |
| T5            | Continuous beaconing and encoded data exchange     |

---

## 7. Behavioral Analysis

* Repeated HTTP POST requests indicate persistent outbound communication
* Presence of encoded payloads suggests encrypted command/data exchange
* Use of NetSupport Manager indicates abuse of legitimate software for unauthorized remote access

---

## 8. MITRE ATT&CK Mapping

* T1071 – Application Layer Protocol (C2 over HTTP)
* T1219 – Remote Access Software (NetSupport RAT usage)

---

## 9. Conclusion

The internal host 10.11.26.183 is compromised and actively communicating with a command-and-control server. The traffic pattern, User-Agent, and command structure confirm the use of NetSupport Manager as a Remote Access Trojan (RAT).

---

## 10. Recommendations

* 🚫 Block IPs: 193.42.38.139, 194.180.191.64
* 🌐 Block domain: modandcrackedapk.com
* 🖥️ Isolate infected host immediately
* 🔍 Perform full endpoint forensic analysis
* 🔐 Reset credentials associated with the system
* 📡 Monitor network for similar C2 patterns

---
