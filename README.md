
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
*Chapters: Architecture, Firmware Hardening, OS Security, VPN Data Leak Prevention (DLP), and VM & configuration drift checks, including CIS benchmark audits and remediation of misconfigurations.*

---

## Demonstrated Scenarios & Technical Validations

<details>
<summary><b>Click to Expand: Authentication & Privilege Auditing (IAM)</b></summary>

* **Authentication failure & brute-force simulations:** Events logged and reviewed in Windows Event Viewer to validate detection and response. This includes establishing a rigorous monitoring baseline by auditing Event IDs 4624 (Success) and 4625 (Failure), reviewing a total volume of 1,000+ security events to distinguish between authorized behavior and potential Indicators of Compromise (IOCs).
* **Privilege escalation detection via Windows security logs:** Including blocked Standard User actions and Admin special privileges, demonstrating effective enforcement of the Principle of Least Privilege (PoLP). Validation was confirmed via Event IDs 4672, 4688, and 4673/4674, specifically verifying that Standard User accounts triggered "Access Denied" logs during unauthorized software installation attempts.

![Image 8: IAM Setup - Admin vs. Standard User account segmentation]

</details>

<details>
<summary><b>Click to Expand: Network Security & VPN Leak Prevention (DLP)</b></summary>

* **VPN kill-switch leak testing:** Performed a "Hard Drop" test by disabling the physical network interface; verified via Command Prompt ("General failure" results) the immediate termination of all outbound traffic (ICMP/HTTP) to prevent clear-text data leakage outside the encrypted tunnel.
![Image 9: Windows Command Prompt showing "General failure" during VPN Hard-Drop test]

* **Data Loss Prevention (DLP):** Enforced network-level and endpoint DLP controls through VPN kill-switch testing, full-disk encryption (BitLocker, TPM-bound), and restricted user privileges. This was further strengthened by implementing custom Outbound Traffic Rules in Windows Defender Firewall and Gateway-level URL Filtering (Rain Web Gateway) to simulate anti-exfiltration controls.
![Image 10: Windows Firewall - Custom Outbound Rules for Micro-segmentation]

</details>

<details>
<summary><b>Click to Expand: Egress Filtering & C2 Mitigation Testing</b></summary>

* **Egress Intelligence & C2 Mitigation Testing:** Validated the integration of NextDNS Threat Intelligence by simulating connections to known malicious domains and Newly Registered Domains (NRDs). Verified 100% block rate for Command & Control (C2) callbacks from authorized binaries, effectively closing the "Domain Fronting" loophole.
![Image 11: NextDNS Analytics - Blocking C2 and NRD attempts]

* **Behavioral Detection & Process Monitoring:** Implemented Sysmon (System Monitor) to capture advanced telemetry beyond standard Windows logging. Validated detection of "Living-off-the-Land" (LotL) techniques and potential process injection, ensuring visibility into malicious activity hidden within trusted system processes.
![Image 12: Sysmon Event ID 3 - Capturing unauthorized network connection attempt]

* **Proactive Vulnerability Assessment:** Executed credentialed vulnerability scans using Nessus Essentials/OpenVAS to identify unpatched software and configuration weaknesses. Successfully utilized Windows Firewall outbound rules as a "Compensating Control" to neutralize identified risks before official patches were deployed.
![Image 13: Nessus Scan Results - Clean Baseline & Remediation Report]

</details>

---

## Security Logic: Why These Controls Matter

<details>
<summary><b>Click to Expand: The Defensive Analogies (Non-Technical vs Technical)</b></summary>

### 1. The "Security Guard at the Exit" (Data Theft / Egress Filtering)
* **Non-Technical:** Like a bank guard checking every bag at the exit; if you don't have an "Authorized to Carry" badge, you can’t leave with anything.
* **Technical:** This is Egress Filtering. By controlling outbound traffic, we stop Data Exfiltration. Even if malware bypasses initial entry, it cannot "phone home" to an attacker’s server to send stolen passwords or files.

### 2. The "Approved Employee List" (Imposter Employee / Binary Whitelisting)
* **Non-Technical:** The building manager only lets 5 specific employees use the office phone. If your name isn't on the list, you can't call out.
* **Technical:** This is Application-Level Micro-segmentation. It shifts from "Blacklisting" (blocking known bad apps) to "Whitelisting" (only allowing authorized binaries). This stops "Living-off-the-Land" (LotL) attacks where hackers try to use built-in Windows tools like PowerShell to reach the web.

### 3. The "Firewalled Rooms" (Spread of Fire / Lateral Movement)
* **Non-Technical:** In a hotel, if a fire starts in the kitchen, steel doors slam shut to keep the smoke from reaching guest rooms.
* **Technical:** This is Host-Based Micro-segmentation. It prevents Lateral Movement. If one application is hacked, the attacker is "trapped" in that process and cannot probe or attack other devices on your local network.

### 4. The "Broken Remote Control" (Backdoor Entry / Reverse Shell)
* **Non-Technical:** A thief sneaks in and tries to use a remote to open the garage for his friends, but you’ve removed the batteries. He’s stuck inside and can't coordinate with his team.
* **Technical:** This prevents Reverse Shells. Attackers often run a script that "reaches out" to their computer to give them full remote control. Blocking unauthorized binaries from initiating external connections kills this "inside-out" connection.

</details>

---

## SDLC Methodology (Project Lifecycle)

<details>
<summary><b>Click to Expand: FIS Standards & SDLC Phase Mapping</b></summary>

Drawing from my Financial Information Systems (FIS) qualification, I applied the Systems Development Life Cycle (SDLC) to manage the project flow from concept to completion. 

| SDLC Phase | Technical Project Application |
| :--- | :--- |
| 1. Planning | Defined project scope to support high-density virtualization; set requirements for 6C/12T architecture and 16GB DDR4 RAM. |
| 2. Analysis | Conducted hardware gap analysis; identified that legacy Celeron architecture lacked SLAT/VT-x support (NPT/AMD-V). |
| 3. Design | Developed logical system architecture; utilized Cisco Packet Tracer to map the connection between the Rain Router and host via Cat6. |
| 4. Implementation | Managed physical component assembly and Thermal Management; executed OS deployment and established Layer 1 physical link. |
| 5. Testing | Performed Verification & Validation (V&V); conducted Hardware stress-testing (POST/MemTest86) and validated TPM 2.0/UEFI integrity. |
| 6. Maintenance | Established Continuous Monitoring via Windows Event Viewer (Logging) and automated patch management |

![Image 2: Detailed SDLC Model Diagram]

</details>

---

## Technical Manifest: 18-Step Roadmap

<details>
<summary><b>Click to Expand: Phase 1 & 2 (Architecture & Systems Integration)</b></summary>

### Phase 1: Architecture & Asset Management (FIS Standards)
* Project Initiation: Final system integration of the MSI high-performance workstation.
* Requirements Analysis: Comparative analysis of Celeron vs. Ryzen architectures to justify upgrades.
* Hardware Asset Management: Structured inventory tracking and lifecycle management (NIST 800-53 standard).
* Logical Network Design: Utilizing Cisco Packet Tracer to diagram the network path (Latency: <1ms local).
![Image 3: Components Procurement & Cisco Packet Tracer Network Diagram]

### Phase 2: Physical & Systems Integration
* Layer 1 Infrastructure: Deployment of physical Cat6 Ethernet for a stable, high-bandwidth link.
* Firmware Hardening: Establishing Hardware Root of Trust via TPM 2.0 and UEFI Secure Boot.
* Hardware Validation: Verification of vitals, RAM speeds, and thermal stability (65–72°C) under high virtualization load.
* Electrical Hardening: Implemented external Surge Safe Power Protection to provide MOV suppression.
![Image 4: Physical PC Interior/Cabling]
![Image 5: BIOS Screen showing TPM 2.0 & Secure Boot ENABLED]

</details>

<details>
<summary><b>Click to Expand: Phase 3 (Implementation & Security Hardening)</b></summary>

* Hardened OS Deployment.
* Network Configuration: Local IP assignment and connectivity verification via ICMP (Ping).
* Vulnerability Management (Patch Compliance): Completed full update cycle and configured Auto-Intelligence updates.
* Fail-Secure Connectivity (VPN Kill-Switch): Implementation of a Permanent Kill-Switch policy via Proton VPN.
* DNS Anti-Spoofing & Integrity: Enforced Private, Encrypted DNS via the VPN tunnel.
* Gateway-Level Security (Rain Router): Configured Edge URL Filtering.
* Host-Based Defense (Windows Firewall): Implemented custom Outbound Traffic Rules for micro-segmentation.

</details>

---

## Phase 4: Validation & SOC Operations

### Virtualization Deployment (The Technical Sandbox)
* **Hypervisor Integration:** Successfully deployed a multi-node virtualization environment using VMware/VirtualBox on the Ryzen 6C/12T platform.
* **Multi-OS Provisioning:**
    * **Node 1 (Kali Linux):** Configured as the offensive security and penetration testing node for internal assessments.
    * **Node 2 (Ubuntu Desktop/Server):** Deployed to master Linux systems administration, user permissions, and syslog monitoring (Targeting Fintech infrastructure requirements).
    * **Node 3 (Windows 10 Hardened):** Maintained as the primary target for security control validation and GPO enforcement.
* **Network Segmentation:** Isolated the lab environment via Virtual NAT/Host-Only adapters.

### SOC Auditing & Incident Monitoring
* established a monitoring baseline; total security events reviewed: 1,000+.
* Key Event IDs: 4624, 4625, 4672, 4688, 4673/4674.
* **Continuous Maintenance:** Performed service hardening by disabling non-essential background processes; maintained 100% patch remediation rate.

### Data Resiliency (3-2-1-1-0 Framework)
* **3 Copies:** Original project files + 2 backup versions.
* **2 Media Types:** Primary Host HDD (Internal) and Removable USB Media (External).
* **1 Offsite Replicate:** Archives synced to a secure Cloud location.
* **1 Immutable:** A "locked" copy (WORM) to prevent lateral ransomware movement.
* **0 Errors:** Restoration Drills to prove RTO <15 minutes.

---

## Skills Gained Through This Project

<details>
<summary><b>Click to Expand: Full Skills List</b></summary>

* **SOC Monitoring & Log Analysis:** Analysis of Windows Security Event Logs to detect authentication failures, unauthorized process creation, privilege escalation attempts, and administrative actions using Event IDs such as 4624, 4625, 4672, 4688, 4673/4674, and 4648.
* **Incident Detection & Validation:** Simulated real-world security events (unauthorized software installation, blocked privilege escalation, admin-only actions) and validated expected system responses through audit logs.
* **Vulnerability Management:** Patch verification, CVE remediation tracking, CIS benchmark audits & configuration drift detection. This includes the implementation of Automatic Security Intelligence Updates.
* **Identity & Access Management (IAM):** Enforcement and validation of the Principle of Least Privilege (PoLP) through Admin vs. Standard user segmentation, UAC enforcement, and privilege auditing.
* **Endpoint & OS Hardening:** Secure OS deployment with TPM 2.0, Secure Boot, BitLocker full-disk encryption, and reduction of attack surface through system hardening.
* **Network-Level Security:** Implementation of Fail-Secure connectivity through VPN kill-switch testing, DNS Anti-Spoofing (DoH), and Gateway-level URL Filtering.
* **Data Loss Prevention (DLP) Fundamentals:** VPN kill-switch testing, full-disk encryption, and restricted user privileges to prevent unauthorized data access and exfiltration.
* **Backup, Recovery & Resilience:** Implementation and validation of a 3-2-1-1-0 backup strategy, restoration testing, and ransomware-resilient design principles.
* **Threat Intelligence & DNS Security:** Integration of cloud-based threat feeds to block Command & Control (C2) infrastructure, Newly Registered Domains (NRDs), and Domain Generation Algorithms (DGA).
* **Advanced Behavioral Analysis:** Utilization of Sysmon (System Monitor) for deep-visibility behavioral logging to detect process injection and stealthy "Living-off-the-Land" (LotL) techniques.

</details>

---

## Target Roles This Project Prepares Me For

<details>
<summary><b>Click to Expand: Target Roles & Career Alignment</b></summary>

* **SOC Analyst (Tier 1 / Junior):** Prepared to monitor security alerts, analyze logs, identify suspicious activity, validate security controls, and escalate confirmed incidents. Special emphasis on detecting C2 callbacks and lateral movement.
* **Vulnerability Management Analyst (Junior / Entry-Level):** Prepared to support vulnerability scanning, patch management, configuration compliance, and remediation tracking. 
* **IAM / Access Management Analyst (Junior):** Prepared to analyze authentication and authorization events, validate privilege boundaries, and support access control enforcement.
* **Junior Security Engineer / Associate Security Engineer:** Prepared to assist with secure system builds, endpoint hardening, control validation, and security architecture support.
* **IT Technician / Junior Systems Administrator:** Prepared to support secure workstation builds, OS deployment, virtualization, monitoring, patching, and backup operations.
* **Junior Threat Hunter:** Equipped to proactively search for indicators of compromise (IoCs) within DNS logs and host-based behavioral logs using Defense-in-Depth layers.

</details>

---

### Visual Evidence Gallery
![Image 9: Final Engineering Station and Windows Event Viewer Security Logs]
![Image 10: Multi-Node Lab Orchestration - VMware Workstation Pro]
