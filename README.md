# Secure Workstation Build & Hardened Infrastructure Project

## Table of Contents
1. [Project Overview](#project-overview)
2. [Architecture & Hardware](#architecture-summary)
3. [Demonstrated Scenarios & Validations](#demonstrated-scenarios--technical-validations)
4. [SDLC Methodology](#sdlc-methodology-project-lifecycle)
5. [Technical Manifest (18-Step Roadmap)](#technical-manifest-18-step-roadmap)
6. [Security Logic & Analogies](#security-logic-what-these-controls-protect-against)
7. [Defense-in-Depth Analysis](#defense-in-depth-solving-the-loopholes)
8. [Phase 4: Validation & SOC Operations](#phase-4-validation--soc-operations)
9. [Skills Gained](#skills-gained-through-this-project)
10. [Target Roles](#target-roles-this-project-prepares-me-for)

---

<a name="project-overview"></a>
## Project Overview
This project documents the end-to-end security hardening and deployment of a performance-optimized workstation. I transitioned from a performance-limited Celeron system to a security-optimized Ryzen environment specifically architected to support high-density virtualization for Identity & Access Management (IAM) and SOC (Security Operations Center) labs.

### The Transformation: Celeron Bottleneck vs. Ryzen Solution
![Image 1: Collage – Old Celeron Laptop vs. New MSI/Ryzen Engineering Build]
* **VM boot times:** Reduced by approximately 60–70%.
* **Stability:** Improved from intermittent crashes to 24/7 sustained operation.
* **Capacity:** Increased from 1–2 limited VMs to 3–5 stable VMs simultaneously.

[Watch the Technical Execution Video on YouTube]

**Chapters:** Architecture, Firmware Hardening, OS Security, VPN Data Leak Prevention (DLP), and VM & configuration drift checks, including CIS benchmark audits and remediation of misconfigurations.

---

<a name="demonstrated-scenarios--technical-validations"></a>
## Demonstrated Scenarios & Technical Validations

* **Authentication & Brute-Force Monitoring:** Established a baseline by auditing 1,000+ security events (Event IDs 4624/4625) to distinguish authorized behavior from IOCs.
* **Privilege Escalation Detection:** Enforced PoLP by verifying "Access Denied" logs (Event IDs 4672, 4688, 4673/4674) when Standard Users attempted unauthorized installs.
* **VPN Kill-Switch Leak Testing:** Performed "Hard Drop" tests; verified immediate termination of all outbound traffic (ICMP/HTTP) via Command Prompt "General failure" results.
* **Vulnerability & Configuration Audits:** Conducted CIS benchmark audits with a 100% remediation rate for critical vulnerabilities within 48 hours.
* **Data Loss Prevention (DLP):** Integrated BitLocker, VPN kill-switches, and custom Outbound Firewall Rules to block unauthorized data exfiltration.
* **Architecture Validation:** Confirmed system vitals (65–72°C) and established Hardware Root of Trust via TPM 2.0 and UEFI Secure Boot.
* **Egress Intelligence:** Validated NextDNS Threat Intelligence with a 100% block rate for C2 callbacks and Newly Registered Domains (NRDs).
* **Behavioral Monitoring:** Deployed Sysmon to detect "Living-off-the-Land" (LotL) techniques and process injection hidden in trusted processes.
* **Proactive Assessment:** Ran Nessus Essentials scans and applied "Compensating Controls" via Firewall rules before official patches were released.

---

<a name="architecture-summary"></a>
## Architecture Summary
| Component | Implementation |
|-----------|----------------|
| CPU | AMD Ryzen (6C/12T) |
| Memory | 16 GB DDR4 |
| Firmware Security | TPM 2.0, UEFI Secure Boot |
| Host OS | Windows 10/11 Pro (Hardened) |
| Hypervisor | VirtualBox / VMware |
| Guest OS | Kali Linux, Windows Server |
| Network | Cat6 Ethernet to ISP Gateway |
| Encryption | BitLocker (TPM-bound) |

---

<a name="sdlc-methodology-project-lifecycle"></a>
## SDLC Methodology (Project Lifecycle)
Drawing from my Financial Information Systems (FIS) qualification, I applied the SDLC to manage the project flow from concept to completion.

| SDLC Phase | Technical Project Application |
|------------|-------------------------------|
| 1. Planning | Defined project scope for high-density virtualization; 6C/12T architecture. |
| 2. Analysis | Conducted gap analysis; identified Celeron lacked SLAT/VT-x support. |
| 3. Design | Developed logical architecture; mapped network path via Cisco Packet Tracer. |
| 4. Implementation | Physical assembly and Thermal Management; Layer 1 physical link. |
| 5. Testing | Performed V&V; Hardware stress-testing and TPM/UEFI integrity validation. |
| 6. Maintenance | Continuous Monitoring via Windows Event Viewer and automated patch management. |

---

<a name="technical-manifest-18-step-roadmap"></a>
## Technical Manifest: 18-Step Roadmap

<details>
<summary><b>Click to View: Phases 1, 2, and 3 (Architecture to Hardening)</b></summary>

### Phase 1: Architecture & Asset Management (FIS Standards)
* Project Initiation: Final system integration of the MSI workstation.
* Requirements Analysis: Celeron vs. Ryzen comparative analysis.
* Hardware Asset Management: NIST 800-53 standard tracking.
* Logical Network Design: Cisco Packet Tracer diagramming (Latency: <1ms local).

### Phase 2: Physical & Systems Integration
* Layer 1 Infrastructure: Cat6 Ethernet deployment.
* Firmware Hardening: TPM 2.0 & UEFI Secure Boot.
* Hardware Validation: 65–72°C load temp; Zero POST/memory faults (12hr test).
* Electrical Hardening: Surge Safe Power Protection (MOV suppression).

### Phase 3: Implementation & Security Hardening
* Hardened OS Deployment.
* Network Configuration: Local IP/ICMP verification.
* Vulnerability Management: Configured Auto-Intelligence Updates for zero-days.
* Fail-Secure Connectivity: Proton VPN Permanent Kill-Switch.
* DNS Integrity: Enforced Private Encrypted DNS to mitigate MITM.
* Gateway Security: Edge URL Filtering (Rain Web Gateway).
* Host-Based Defense: Custom Outbound Firewall Rules (Micro-segmentation).

</details>

---

<a name="security-logic-what-these-controls-protect-against"></a>
## Security Logic: What these controls protect against

<details>
<summary><b>Click to View: Defensive Analogies & Blind Spots</b></summary>

**1. The "Security Guard at the Exit" (Data Theft / Egress Filtering)**
* Non-Technical: Like a bank guard checking every bag at the exit.
* Technical: This is Egress Filtering. Stops Data Exfiltration even if malware bypasses initial entry.

**2. The "Approved Employee List" (Imposter Employee / Binary Whitelisting)**
* Non-Technical: Only 5 specific employees can use the phone.
* Technical: Application-Level Micro-segmentation. Stops LotL attacks (e.g., PowerShell reaching the web).

**3. The "Firewalled Rooms" (Spread of Fire / Lateral Movement)**
* Non-Technical: Hotel steel doors slam shut to keep smoke from reaching rooms.
* Technical: Host-Based Micro-segmentation. Traps attackers in one process.

**4. The "Broken Remote Control" (Backdoor Entry / Reverse Shell)**
* Non-Technical: A thief tries to use a remote with no batteries.
* Technical: Prevents Reverse Shells by blocking unauthorized binaries from "opening a door" to the outside.

### Critical Blind Spots: What Windows Firewall Cannot Do
* **Lack of DPI:** It cannot see inside authorized HTTPS requests.
* **Process Injection:** Malware can hijack trusted processes (explorer.exe).
* **Administrative Bypass:** Local Admin rights can disable the firewall.
* **Memory Attacks:** Cannot see Buffer Overflows inside the RAM.

</details>

---

<a name="defense-in-depth-solving-the-loopholes"></a>
## Defense-in-Depth: Solving the Loopholes

<details>
<summary><b>Click to View: Threat & Defense Mapping Tables</b></summary>

### Layer 2 & 3 Integration
* **NextDNS:** Handles C2 Threat Intelligence, NRD Blocking, and DGA Protection.
* **Sysmon:** Behavioral logging for process injection detection.
* **Nessus:** Proactive identification of unpatched software for Compensating Controls.

| Windows Firewall Limitation | Secondary Solution | How it Solves the Problem |
|-----------------------------|-------------------|---------------------------|
| Encrypted Data Exfiltration | NextDNS | Blocks malicious destination by reputation. |
| Process/Code Injection      | Sysmon  | Logs unauthorized interactions. |
| Admin Bypass                | Standard User Policy | Prevents modification of rules. |

| Threat (Simple Name) | Technical Threat | Defense Mechanism |
|----------------------|------------------|-------------------|
| The "Phone Home"     | C2               | Egress Filtering  |
| The "Imposter"       | LotL / LOLBins   | Binary Blocking   |
| The "Spread of Fire" | Lateral Movement | Micro-segmentation|

</details>

---

<a name="phase-4-validation--soc-operations"></a>
## Phase 4: Validation & SOC Operations

<details>
<summary><b>Click to View: Lab Virtualization & Monitoring Metrics</b></summary>

### Virtualization Deployment
* **Node 1 (Kali Linux):** Offensive security and penetration testing.
* **Node 2 (Ubuntu Desktop):** Linux SysAdmin and syslog monitoring.
* **Node 3 (Windows 10):** Security control validation and GPO target.
* **Segmentation:** Isolated via Virtual NAT/Host-Only adapters.

### SOC Auditing & Incident Monitoring
* **Event Volume:** 1,000+ security events reviewed.
* **Key Event IDs:** 4624, 4625, 4672, 4688, 4673, 4674.
* **IAM Control:** Simulated unauthorized installation from Standard User; verified "Access Denied" and proper UAC logging.

### Maintenance & Compliance
* **Configuration Drift:** Weekly manual audits of security policies.
* **Patch Compliance:** 100% remediation of critical OS vulnerabilities.
* **DR Planning:** Restoration drills via hybrid backups (Cloud/Local).

</details>

---

<a name="data-protection-backup--storage-solutions-the-digital-safety-net"></a>
<a name="data-resilience--backup"></a>
## Data Resiliency Execution (3-2-1-1-0 Framework)
* **3 Copies:** Original project files + 2 backup versions.
* **2 Media Types:** Primary Host HDD (Internal) and Removable USB Media (External/Air-Gap).
* **1 Offsite Replicate:** Archives synced to a secure Cloud location.
* **1 Immutable:** A "locked" copy (WORM) to prevent lateral ransomware.
* **0 Errors:** Restoration Drills proving RTO <15 minutes.

---

<a name="skills-gained-through-this-project"></a>
## Skills Gained Through This Project

<details>
<summary><b>Click to View: Full Technical Skills Catalog</b></summary>

* **SOC Monitoring & Log Analysis:** Windows Security Event Log Analysis (Event IDs 4624, 4625, 4672, 4688, etc).
* **Vulnerability Management:** Nessus scanning, CVE remediation, and CIS benchmarks.
* **IAM:** PoLP enforcement and Admin/Standard user segmentation.
* **Endpoint Hardening:** TPM 2.0, Secure Boot, and BitLocker encryption.
* **Network Security:** VPN kill-switch testing, DNS Anti-Spoofing, and Egress Filtering.
* **Behavioral Analysis:** Sysmon telemetry for process injection and LotL detection.

</details>

---

<a name="target-roles-this-project-prepares-me-for"></a>
## Target Roles This Project Prepares Me For

<details>
<summary><b>Click to View: Professional Alignment</b></summary>

* **SOC Analyst (Tier 1 / Junior)**
* **Vulnerability Management Analyst (Junior / Entry-Level)**
* **IAM / Access Management Analyst (Junior)**
* **Junior Security Engineer / Associate Security Engineer**
* **Junior Threat Hunter**

</details>

---
### Visual Evidence
![Image 6: Windows Security Dashboard (Green Checks)]
![Image 7: BitLocker Encryption Status & VPN Kill Switch settings]
![Image 9: Final Engineering Station and Windows Event Viewer Security Logs]
![Image 10: Multi-Node Lab Orchestration - VMware Workstation Pro]

 