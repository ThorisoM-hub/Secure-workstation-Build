# Secure Workstation Build & Hardened Infrastructure Project
## Table of Contents
1. [Project Overview](#project-overview)
2. [Architecture & Hardware](#architecture--hardware)
3. [Implementation & Hardening](#implementation--hardening)
4. [Security Validation & Testing](#security-validation--testing)
5. [Monitoring & SOC Operations](#monitoring--soc-operations)
6. [Data Resilience & Backup](#data-resilience--backup)
7. [SDLC Methodology](#sdlc-methodology)
8. [Skills Gained](#skills-gained)
9. [Target Roles](#target-roles)

---

## Project Overview
This project documents the end-to-end security hardening and deployment of a performance-optimized workstation. I transitioned from a performance-limited Celeron system to a security-optimized Ryzen environment specifically architected to support high-density virtualization for Identity & Access Management (IAM) and SOC (Security Operations Center) labs.

### The Transformation: Celeron Bottleneck vs. Ryzen Solution
![Image 1: Collage – Old Celeron Laptop vs. New MSI/Ryzen Engineering Build]

* VM boot times reduced by approximately 60–70%
* Lab stability improved from intermittent crashes to 24/7 sustained operation
* Capacity increased from 1–2 limited VMs to 3–5 stable VMs simultaneously

[Watch the Technical Execution Video on YouTube]
Chapters: Architecture, Firmware Hardening, OS Security, VPN Data Leak Prevention (DLP), and VM & configuration drift checks, including CIS benchmark audits and remediation of misconfigurations.

---

## Demonstrated Scenarios & Technical Validations

### Authentication & Privilege Auditing
* **Brute-force simulations:** Events logged and reviewed in Windows Event Viewer. Established a rigorous monitoring baseline by auditing Event IDs 4624 (Success) and 4625 (Failure), reviewing a volume of 1,000+ security events to distinguish authorized behavior from potential IOCs.
* **Privilege escalation detection:** Validated enforcement of the Principle of Least Privilege (PoLP). Confirmed via Event IDs 4672, 4688, and 4673/4674 that Standard User accounts triggered "Access Denied" logs during unauthorized installation attempts.

![Image 8: IAM Setup - Admin vs. Standard User account segmentation]

### Network & Data Leak Prevention (DLP)
* **VPN kill-switch leak testing:** Performed a "Hard Drop" test by disabling the physical network interface; verified via Command Prompt ("General failure" results) the immediate termination of all outbound traffic (ICMP/HTTP) to prevent clear-text leakage.
![Image 9: Windows Command Prompt showing "General failure" during VPN Hard-Drop test]

* **Host-Based Defense (Windows Firewall):** Implemented custom Outbound Traffic Rules. 
![Image 10: Windows Firewall - Custom Outbound Rules for Micro-segmentation]

---

<details>
<summary><b>Click to Expand: Security Logic & Defensive Analogies</b></summary>

### Security Logic: What these controls protect against

**1. The "Security Guard at the Exit" (Data Theft / Egress Filtering)**
* **Non-Technical:** Like a bank guard checking every bag at the exit; if you don't have an "Authorized to Carry" badge, you can’t leave.
* **Technical:** This is Egress Filtering. By controlling outbound traffic, we stop Data Exfiltration. Even if malware bypasses entry, it cannot "phone home" to an attacker’s server.

**2. The "Approved Employee List" (Imposter Employee / Binary Whitelisting)**
* **Non-Technical:** The building manager only lets 5 specific employees use the office phone. If your name isn't on the list, you can't call out.
* **Technical:** This is Application-Level Micro-segmentation. It stops "Living-off-the-Land" (LotL) attacks where hackers use built-in tools like PowerShell to reach the web.

**3. The "Firewalled Rooms" (Spread of Fire / Lateral Movement)**
* **Non-Technical:** In a hotel, if a fire starts in the kitchen, steel doors slam shut to keep smoke from reaching guest rooms.
* **Technical:** This is Host-Based Micro-segmentation. It prevents Lateral Movement. If one application is hacked, the attacker is "trapped" and cannot probe other devices.

**4. The "Broken Remote Control" (Backdoor Entry / Reverse Shell)**
* **Non-Technical:** A thief sneaks in and tries to use a remote to open the garage, but you’ve removed the batteries. He’s stuck inside and can't coordinate with his team.
* **Technical:** This prevents Reverse Shells. Blocking unauthorized binaries from initiating external connections kills this "inside-out" connection.

### Critical Blind Spots: What Windows Firewall Cannot Do
As a SOC Analyst, it is vital to understand where a tool's power ends:
* **Lack of Deep Packet Inspection (DPI):** It looks at the envelope (IP/Port) but not inside.
* **Evasion via Process Injection:** Malware hijacks a "good" process (like explorer.exe) already allowed online.
* **Administrative Bypass:** An attacker with Local Admin rights can simply disable the firewall.

</details>

---

## Technical Manifest: 18-Step Roadmap

<details>
<summary><b>Click to Expand: Phase 1 & 2 (Architecture & Systems Integration)</b></summary>

### Phase 1: Architecture & Asset Management (FIS Standards)
1. Project Initiation: Final system integration of the MSI workstation.
2. Requirements Analysis: Comparative analysis of Celeron vs. Ryzen architectures.
3. Hardware Asset Management: Structured inventory tracking (NIST 800-53 standard).
4. Logical Network Design: Cisco Packet Tracer diagramming (Latency: <1ms local).

### Phase 2: Physical & Systems Integration
5. Layer 1 Infrastructure: Deployment of physical Cat6 Ethernet.
6. Firmware Hardening: Establishing Hardware Root of Trust via TPM 2.0 and UEFI Secure Boot.
7. Hardware Validation: Sustained CPU temp under load: 65–72°C. Zero POST/memory faults.
8. Electrical Hardening: Implemented external Surge Safe Power Protection.
![Image 4: Physical PC Interior/Cabling]
![Image 5: BIOS Screen showing TPM 2.0 & Secure Boot ENABLED]

</details>

<details>
<summary><b>Click to Expand: Phase 3 (Implementation & Hardening)</b></summary>

9. Hardened OS Deployment.
10. Network Configuration (ICMP verification).
11. Fail-Secure Connectivity (VPN Kill-Switch).
12. DNS Anti-Spoofing & Integrity: Enforced Private Encrypted DNS via VPN.
13. Gateway-Level Security (Rain Router): Edge URL Filtering.
14. Host-Based Defense: Custom Windows Firewall Outbound Rules.
15. Layer 2 DNS-Layer Defense: Integrated NextDNS for C2 Threat Intelligence, Newly Registered Domain (NRD) blocking, and DGA protection.
![Image 11: NextDNS Analytics - Blocking C2 and NRD attempts]
16. Layer 3 Behavioral Monitoring: Sysmon integration for Process Injection detection.
![Image 12: Sysmon Event ID 3 - Capturing unauthorized network connection attempt]
17. Vulnerability Assessment: Nessus Essentials scans to find unpatched software.
![Image 13: Nessus Scan Results - Clean Baseline]

</details>

---

## Phase 4: Validation & SOC Operations

### Virtualization Deployment (The Technical Sandbox)
* **Hypervisor Integration:** Successfully deployed multi-node environment on Ryzen 6C/12T platform.
* **Multi-OS Provisioning:**
    * **Node 1 (Kali Linux):** Offensive node for internal assessments.
    * **Node 2 (Ubuntu Desktop/Server):** Linux admin and syslog monitoring (Fintech-targeted).
    * **Node 3 (Windows 10 Hardened):** Target for security control validation and GPO.
* **Resource Management:** Optimized allocation for concurrent operation.
* **Network Segmentation:** Isolated via Virtual NAT/Host-Only adapters.

### SOC Auditing & Incident Monitoring
* established monitoring baseline; total security events reviewed: 1,000+.
* Key Event IDs: 4624, 4625, 4672, 4688, 4673/4674.
* **Continuous Maintenance:** Patch Compliance (100% remediation within 48h) and weekly policy audits.

### Data Resiliency (3-2-1-1-0 Framework)
* **3 Copies:** Original + 2 backups.
* **2 Media Types:** Internal HDD + External USB (Air-Gap).
* **1 Offsite:** Secure Cloud replicate.
* **1 Immutable:** "Locked" WORM copy.
* **0 Errors:** Restoration drills proving RTO < 15 minutes.

---

## Skills Gained & Target Roles
* SOC Monitoring & Log Analysis (Event IDs, Sysmon)
* Vulnerability Management (Nessus, Patch Verification)
* IAM (Principle of Least Privilege, Admin/Standard segmentation)
* Endpoint Hardening (TPM, BitLocker, Egress Filtering)

**Target Roles:** Junior SOC Analyst, Vulnerability Management Analyst, IAM Analyst, Junior Security Engineer.

---
**Visual Evidence Finalized**
![Image 9: Final Engineering Station and Windows Event Viewer Security Logs]
![Image 10: Multi-Node Lab Orchestration - VMware showing Kali, Ubuntu, and Windows 10 Nodes]


