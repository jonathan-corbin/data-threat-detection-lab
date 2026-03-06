# ad-threat-detection-sentinel

A hands-on lab simulating real-world attacks across Active Directory, Microsoft 365, and cloud data stores — with Microsoft Sentinel detection rules built for each. Aligned with Managed Data Detection and Response (MDDR) analyst work.

---

## Lab Overview

This lab simulates a small enterprise environment with Active Directory, Windows endpoints, and Microsoft Sentinel as the SIEM. Each module covers a real attack technique, a KQL detection rule, and a written incident response walkthrough.

**Skills practiced:** Active Directory, Microsoft Sentinel, KQL, Windows Event Logs, Incident Triage, Threat Detection

**Cert alignment:** SC-200 (Microsoft Security Operations Analyst), CySA+

---

## Environment Setup

| Component | Details |
|---|---|
| Domain Controller | Windows Server 2022, Active Directory DS |
| Workstation | Windows 10/11 VM (domain-joined) |
| Attacker Machine | Kali Linux |
| SIEM | Microsoft Sentinel (Azure free trial) |
| Log Forwarding | Azure Monitor Agent (AMA) |

See [`setup/`](./setup/) for full build instructions.

---

## Attack & Detection Modules

### 1. Password Spraying
- **Technique:** MITRE ATT&CK T1110.003
- **Simulated with:** Custom PowerShell script
- **Detection:** Event ID 4625 — multiple failed logons across accounts
- **KQL:** [`detections/password-spray.kql`](./detections/password-spray.kql)
- **Writeup:** [`writeups/password-spray.md`](./writeups/password-spray.md)

---

### 2. Kerberoasting
- **Technique:** MITRE ATT&CK T1558.003
- **Simulated with:** Impacket `GetUserSPNs.py` / Rubeus
- **Detection:** Event ID 4769 — Kerberos service ticket requested with RC4 encryption
- **KQL:** [`detections/kerberoasting.kql`](./detections/kerberoasting.kql)
- **Writeup:** [`writeups/kerberoasting.md`](./writeups/kerberoasting.md)

---

### 3. Lateral Movement (Pass-the-Hash)
- **Technique:** MITRE ATT&CK T1550.002
- **Simulated with:** Mimikatz
- **Detection:** Event ID 4624 Type 3 logon + anomalous source IP
- **KQL:** [`detections/lateral-movement.kql`](./detections/lateral-movement.kql)
- **Writeup:** [`writeups/lateral-movement.md`](./writeups/lateral-movement.md)

---

### 4. Insider Threat — Abnormal Data Access
- **Technique:** MITRE ATT&CK T1078
- **Simulated with:** User account accessing file shares outside normal behavior
- **Detection:** Sentinel UEBA + custom KQL for abnormal access volume
- **KQL:** [`detections/insider-threat.kql`](./detections/insider-threat.kql)
- **Writeup:** [`writeups/insider-threat.md`](./writeups/insider-threat.md)

---

### 5. Brute Force (RDP)
- **Technique:** MITRE ATT&CK T1110.001
- **Simulated with:** Hydra
- **Detection:** Event ID 4625 + 4624 sequence on RDP port
- **KQL:** [`detections/rdp-brute-force.kql`](./detections/rdp-brute-force.kql)
- **Writeup:** [`writeups/rdp-brute-force.md`](./writeups/rdp-brute-force.md)

---

## Repo Structure

```
mddr-home-lab/
├── README.md
├── setup/
│   ├── domain-controller.md
│   ├── sentinel-setup.md
│   └── log-forwarding.md
├── attacks/
│   ├── password-spray/
│   ├── kerberoasting/
│   ├── lateral-movement/
│   ├── insider-threat/
│   └── rdp-brute-force/
├── detections/
│   ├── password-spray.kql
│   ├── kerberoasting.kql
│   ├── lateral-movement.kql
│   ├── insider-threat.kql
│   └── rdp-brute-force.kql
└── writeups/
    ├── password-spray.md
    ├── kerberoasting.md
    ├── lateral-movement.md
    ├── insider-threat.md
    └── rdp-brute-force.md
```

---

## MITRE ATT&CK Coverage

| Technique ID | Name | Tactic |
|---|---|---|
| T1110.003 | Password Spraying | Credential Access |
| T1558.003 | Kerberoasting | Credential Access |
| T1550.002 | Pass-the-Hash | Lateral Movement |
| T1078 | Valid Accounts | Persistence / Defense Evasion |
| T1110.001 | Brute Force: RDP | Credential Access |

---

## Author

Jonathan Corbin — Field Tech transitioning to cybersecurity
CompTIA Security+ | CySA+ (in progress) | OSCP (in progress)
[LinkedIn](https://www.linkedin.com/in/corbinjonathan/) | [GitHub](https://github.com/jonathan-corbin)
