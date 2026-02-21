# Secure Workstation Build & Hardened Infrastructure Project

## Table of Contents
1. [Project Overview](#project-overview)
2. [Demonstrated Scenarios & Technical Validations](#demonstrated-scenarios--technical-validations)
3. [Architecture Summary](#architecture-summary)
4. [SDLC Methodology (Project Lifecycle)](#sdlc-methodology-project-lifecycle)
5. [Technical Manifest: 18-Step Roadmap](#technical-manifest-18-step-roadmap)
6. [Phase 4: Validation & SOC Operations](#phase-4-validation--soc-operations)
7. [Skills Gained Through This Project](#skills-gained-through-this-project)
8. [Target Roles This Project Prepares Me For](#target-roles-this-project-prepares-me-for)

---

<a name="project-overview"></a>
## Project Overview
This project documents the end-to-end security hardening and deployment of a performance-optimized workstation. I transitioned from a performance-limited Celeron system to a security-optimized Ryzen environment specifically architected to support high-density virtualization for Identity & Access Management (IAM) and SOC (Security Operations Center) labs.

**The Transformation: Celeron Bottleneck vs. Ryzen Solution**
![Image 1: Collage – Old Celeron Laptop vs. New MSI/Ryzen Engineering Build]
* VM boot times reduced by approximately 60–70%
* Lab stability improved from intermittent crashes to 24/7 sustained operation
* Capacity increased from 1–2 limited VMs to 3–5 stable VMs simultaneously

<a name="technical-execution-video"></a>
## [Watch the Technical Masterclass (30 min Video)](#)

**Video Chapters:**
* **Phase 1:** Architecture & Hardware Justification (Celeron vs. Ryzen)
* **Phase 2:** Firmware Hardening, OS Deployment & VPN Kill-Switch Testing
* **Phase 3:** IAM Validation, SOC Monitoring & Vulnerability Remediation
* **Phase 4:** Data Resiliency & 3-2-1-1-0 Backup Restoration Drills

---

<a name="demonstrated-scenarios--technical-validations"></a>
## Demonstrated Scenarios & Technical Validations

<details>
<summary><b>Click to Expand: Summary of Technical Testing & Evidence</b></summary>

* **Brute-Force & Auth Monitoring:** Audited **1,000+ security events** via **Event IDs 4624 (Success) and 4625 (Failure)** to establish a behavioral baseline and identify potential IOCs.
* **Privilege Escalation & IAM:** Enforced **PoLP** by validating blocked actions via **Event IDs 4672, 4688, and 4673/4674**; verified Standard User "Access Denied" logs during unauthorized install attempts. ![Image 8: IAM Setup - Admin vs. Standard User account segmentation]
* **VPN Kill-Switch (DLP):** Conducted "Hard Drop" testing by disabling physical interfaces; verified **0 clear-text leakage** via Command Prompt "General failure" results. ![Image 9: Windows Command Prompt showing "General failure" during VPN Hard-Drop test]
* **Vulnerability Management:** Maintained a **100% remediation rate** for critical vulnerabilities; verified all Security Intelligence Updates within **48 hours** of release per CIS benchmarks.
* **Network Micro-segmentation:** Implemented **outbound firewall rules** and Rain Web Gateway URL filtering to block unauthorized binary exfiltration. ![Image 10: Windows Firewall - Custom Outbound Rules for Micro-segmentation]
* **Hardware Integrity:** Validated system stability under high load (sustained **65–72°C**) and established **Hardware Root of Trust** via TPM 2.0 and UEFI Secure Boot.
* **Network Performance:** Validated logical paths via Cisco Packet Tracer, ensuring **<1ms local latency** and **0% packet loss** over Cat6.
* **Data Resiliency:** Applied **3-2-1-1-0 framework**; confirmed business continuity via restoration drills proving an **RTO of <15 minutes**.
* **Egress Intelligence:** Achieved **100% block rate** for Command & Control (C2) callbacks and Newly Registered Domains (NRDs) using NextDNS. ![Image 11: NextDNS Analytics - Blocking C2 and NRD attempts]
* **Advanced Telemetry:** Deployed **Sysmon** to detect "Living-off-the-Land" (LotL) techniques and process injection (Event ID 3) that bypass standard logging. ![Image 12: Sysmon Event ID 3 - Capturing unauthorized network connection attempt]
* **Proactive Defense:** Performed credentialed **Nessus/OpenVAS scans**; utilized Firewall outbound rules as "Compensating Controls" for unpatched vulnerabilities. ![Image 13: Nessus Scan Results - Clean Baseline & Remediation Report]

</details>


## Architecture Summary

| Component | Implementation |
| :--- | :--- |
| **CPU** | AMD Ryzen (6C/12T) |
| **Memory** | 16 GB DDR4 |
| **Firmware Security** | TPM 2.0, UEFI Secure Boot |
| **Host OS** | Windows 10/11 Pro (Hardened) |
| **Hypervisor** | VirtualBox / VMware |
| **Guest OS** | Kali Linux, Windows Server |
| **Network** | Cat6 Ethernet to ISP Gateway |
| **Encryption** | BitLocker (TPM-bound) |

---

<a name="sdlc-methodology-project-lifecycle"></a>
## SDLC Methodology (Project Lifecycle)

<details>
<summary><b>Click to Expand: FIS SDLC Phase Details</b></summary>

Drawing from my Financial Information Systems (FIS) qualification, I applied the Systems Development Life Cycle (SDLC) to manage the project flow from concept to completion. This ensures a professional, requirements-driven foundation suitable for audited corporate and financial environments.

| SDLC Phase | Technical Project Application |
| :--- | :--- |
| **1. Planning** | Defined project scope to support high-density virtualization; set requirements for 6C/12T architecture and 16GB DDR4 RAM. |
| **2. Analysis** | Conducted hardware gap analysis; identified that legacy Celeron architecture lacked SLAT/VT-x support (NPT/AMD-V). |
| **3. Design** | Developed logical system architecture; utilized Cisco Packet Tracer to map the connection between the Rain Router and host via Cat6. |
| **4. Implementation** | Managed physical component assembly and Thermal Management; executed OS deployment and established Layer 1 physical link. |
| **5. Testing** | Performed Verification & Validation (V&V); conducted Hardware stress-testing (POST/MemTest86) and validated TPM 2.0/UEFI integrity. |
| **6. Maintenance** | Established Continuous Monitoring via Windows Event Viewer (Logging) and automated patch management |

![Image 2: Detailed SDLC Model Diagram]

</details>

---

<a name="technical-manifest-18-step-roadmap"></a>
## Technical Manifest: 18-Step Roadmap

<details>
<summary><b>Click to Expand: Phases 1, 2, and 3 (Full 18-Step Manifest)</b></summary>

### Phase 1: Architecture & Asset Management (FIS Standards)
* Project Initiation: Final system integration of the MSI high-performance workstation.
* Requirements Analysis: Comparative analysis of Celeron vs. Ryzen architectures to justify upgrades.
* Hardware Asset Management: Structured inventory tracking and lifecycle management (NIST 800-53 standard).
* Logical Network Design: Utilizing Cisco Packet Tracer to diagram the network path from the Rain Router to the Host via Cat6 cabling.
    * Metric: Average lab traffic latency over Cat6: <1ms local network latency.
    * Metric: Network stability: 0 packet loss during sustained testing sessions.
![Image 3: Components Procurement & Cisco Packet Tracer Network Diagram]

### Phase 2: Physical & Systems Integration
* Layer 1 Infrastructure: Deployment of physical Cat6 Ethernet for a stable, high-bandwidth link.
* Firmware Hardening: Establishing Hardware Root of Trust via TPM 2.0 and UEFI Secure Boot.
* Hardware Validation: Verification of vitals, RAM speeds, and thermal stability under high virtualization load.
    * Validation: Sustained CPU temperature under load: 65–72°C.
    * Validation: Zero POST or memory faults after 12-hour stress test.
    * Electrical Hardening: Implemented external Surge Safe Power Protection to provide MOV suppression.
![Image 4: Physical PC Interior/Cabling] ![Image 5: BIOS Screen showing TPM 2.0 & Secure Boot ENABLED]

### Phase 3: Implementation & Security Hardening
* **Hardened OS Deployment:** Secure installation of Windows Pro, optimized for enterprise security.
* **Network Configuration:** Local IP assignment and connectivity verification via ICMP (Ping).
* **Vulnerability Management (Patch Compliance):** Completed a full Windows Update cycle and configured Automatic Security Intelligence Updates to mitigate Zero-Day exploits and known CVEs.
* **Fail-Secure Connectivity (VPN Kill-Switch):** Implementation of a Permanent Kill-Switch policy via Proton VPN. Performed a "Hard Drop" test by disabling the physical network interface; verified via Command Prompt ("General failure" results) the immediate termination of all outbound traffic (ICMP/HTTP) to prevent clear-text data leakage outside the encrypted tunnel.
* **DNS Anti-Spoofing & Integrity:** Enforced the use of Private, Encrypted DNS via the VPN tunnel to mitigate DNS Cache Poisoning and Man-in-the-Middle (MITM) attacks. This ensures that identity-related traffic (login portals) cannot be redirected to malicious IP addresses.
* **Gateway-Level Security (Rain Router):** Configured Edge URL Filtering via the Rain Web Gateway. Restricted unauthorized domains (e.g., facebook.com) at the DNS level to reduce the external attack surface and mitigate Shadow IT risks.
* **Host-Based Defense (Windows Firewall):** Implemented custom Outbound Traffic Rules within Windows Defender Firewall with Advanced Security. Implemented micro-segmentation by blocking specific non-authorized binaries from initiating external connections, simulating anti-exfiltration controls.

### Security Logic: What these controls protect against
This defensive setup transitions the workstation to a "Zero Trust" posture by controlling not just who enters, but what is allowed to leave. Below is the breakdown of the specific threats neutralized by these firewall rules:

**1. The "Security Guard at the Exit" (Data Theft / Egress Filtering)**
* Non-Technical: Like a bank guard checking every bag at the exit; if you don't have an "Authorized to Carry" badge, you can’t leave with anything.
* Technical: This is Egress Filtering. By controlling outbound traffic, we stop Data Exfiltration. Even if malware bypasses initial entry, it cannot "phone home" to an attacker’s server to send stolen passwords or files.

**2. The "Approved Employee List" (Imposter Employee / Binary Whitelisting)**
* Non-Technical: The building manager only lets 5 specific employees use the office phone. If your name isn't on the list, you can't call out.
* Technical: This is Application-Level Micro-segmentation. It shifts from "Blacklisting" (blocking known bad apps) to "Whitelisting"(only allowing authorized binaries). This stops "Living-off-the-Land" (LotL) attacks where hackers try to use built-in Windows tools like PowerShell to reach the web.

**3. The "Firewalled Rooms" (Spread of Fire / Lateral Movement)**
* Non-Technical: In a hotel, if a fire starts in the kitchen, steel doors slam shut to keep the smoke from reaching guest rooms.
* Technical: This is Host-Based Micro-segmentation. It prevents Lateral Movement. If one application is hacked, the attacker is "trapped" in that process and cannot probe or attack other devices on your local network.

**4. The "Broken Remote Control" (Backdoor Entry / Reverse Shell)**
* Non-Technical: A thief sneaks in and tries to use a remote to open the garage for his friends, but you’ve removed the batteries. He’s stuck inside and can't coordinate with his team.
* Technical: This prevents Reverse Shells. Attackers often run a script that "reaches out" to their computer to give them full remote control. Blocking unauthorized binaries from initiating external connections kills this "inside-out" connection.

### Critical Blind Spots: What Windows Firewall Cannot Do
As a SOC Analyst, it is vital to understand where a tool's power ends. While Windows Firewall is powerful, it has "invisible" gaps:
* Lack of Deep Packet Inspection (DPI):The firewall is "Stateful"—it looks at the label on the envelope (IP/Port) but not inside. If a hacker hides stolen data inside an authorized HTTPS request, the firewall lets it pass.
* Evasion via Process Injection: Malware hijacks a "good" process (like explorer.exe) already allowed to go online. Since the identity is trusted, the firewall cannot tell the process has been hijacked from the inside.
* Administrative Bypass: As a host-based defense, an attacker with Local Admin rights can simply run a command to disable the firewall.
* IP Spoofing & Memory Attacks: It trusts source information provided by the network card and cannot see "Buffer Overflows" happening entirely inside the RAM.

### Layer 2: DNS-Layer Defense (Network Infrastructure Intelligence)
Tooling: NextDNS (Cloud-Based Intelligence Layer) Since Windows Firewall handles the "What" (the program), NextDNS was implemented to handle the "Where" (the destination), acting as the "Intelligence Agency" for the workstation.
* C2 Threat Intelligence (The "Bad Neighborhood" Filter): NextDNS maintains a massive, real-time list of Command & Control (C2) "Bad Neighborhoods."
* Newly Registered Domain (NRD) Blocking: A proactive Vulnerability Management control. By blocking any domain created in the last 30 days, I neutralized the "disposable" infrastructure hackers use for phishing.
* DGA (Domain Generation Algorithm) Protection: NextDNS uses AI to recognize "gibberish" machine-generated names and blocks them automatically.
* Anti-Stealth Toggles: Enabled protection against DNS Rebinding and Cryptojacking.

### Layer 3: Behavioral Monitoring & Vulnerability Assessment
* Behavioral Logging (Sysmon): Logs Process Injection and lateral movement, providing visibility to detect stealthy movement that the firewall trusts.
* Vulnerability Assessment (Nessus Essentials/OpenVAS): Implemented periodic scanning to find unpatched software. This allows for Compensating Controls—blocking specific binaries in the firewall until a patch is available.

### Defense-in-Depth: Solving the Loopholes
The following table illustrates how the secondary layers (NextDNS, Sysmon, Nessus) solve the specific problems that Windows Firewall cannot address alone.

| Windows Firewall Limitation | Secondary Solution | How it Solves the Problem |
| :--- | :--- | :--- |
| Encrypted Data Exfiltration | NextDNS (DPI/Reputation) | Blocks the malicious destination even if the data is encrypted. |
| Process/Code Injection | Sysmon (Behavioral) | Logs unauthorized interactions between "good" apps and malicious code. |
| Admin Bypass | Standard User Policy | Prevents an attacker from modifying or disabling firewall rules. |
| Zero-Day "Memory" Attacks | Nessus (Vulnerability Scanning) | Identifies unpatched apps so they can be hardened before exploitation. |
| Domain Fronting | NextDNS (AI Detection) | Detects unusual DNS requests that bypass IP-based firewall rules. |

### Threat & Defense Technical Summary

| Threat (Simple Name) | Technical Threat | Defense Mechanism | How it Protects You |
| :--- | :--- | :--- | :--- |
| The "Phone Home" | C2 (Command & Control) | Egress Filtering / NextDNS | Stops malware from contacting the hacker's server. |
| The "Imposter Employee" | LotL / LOLBins | Binary-Level Blocking | Prevents built-in tools (PowerShell) from being used maliciously. |
| The "Backdoor Entry" | Reverse Shell | Auth. Connection Rules | Prevents an internal script from "opening a door" to the outside. |
| The "Spread of Fire" | Lateral Movement | Micro-segmentation | Traps a hacker in one "box" so they can't jump to other devices. |
| The "Data Thief" | Exfiltration | Anti-Exfiltration / NRD | Blocks unauthorized apps or new domains from stealing your data. |

### Identity & Access Management (IAM)
Enforcement of Principle of Least Privilege (PoLP) via Admin vs. Standard account segmentation.
* IAM Control: Segmented Backup-Admin privileges to ensure only authorized identities can modify or delete the archive.
* Validation Action – Unauthorized Software Installation Test:Simulated an unauthorized software installation from a Standard User account to validate enforcement of the Principle of Least Privilege. The installation was blocked by UAC/admin controls (logged in Event Viewer: Event ID 4624 (Logon), Event ID 4625 (Failed Logon), Event ID 4672 (Special Privileges), Event ID 4688 (Process Creation), and Event IDs 4673 / 4674 (Sensitive Privilege Use / Privilege Object Access Denied)).

### Data-at-Rest Encryption & Protection
* Full-disk encryption via BitLocker, anchored to hardware TPM.
* Data Protection: Backup & Storage Solutions (The "Digital Safety Net"): I engineered a professional 3-2-1-1-0 Data Resiliency Framework for "Thoriso_critical_files.zip":
    * 3 Copies: Original project files + 2 backup versions.
    * 2 Media Types: Primary Host HDD (Internal) and Removable USB Media (External/Logical Air-Gap).
    * 1 Offsite Replicate: Archives synced to a secure Cloud location.
    * 1 Immutable: A "locked" copy (WORM) to prevent lateral ransomware movement.
    * 0 Errors: Restoration Drills to prove RTO <15 minutes.

![Image 6: Windows Security Dashboard (Green Checks)] ![Image 7: BitLocker Encryption Status & VPN Kill Switch settings] ![Image 8: IAM Setup - Admin vs. Standard User account segmentation] ![Image 9: Windows Command Prompt showing "General failure" during VPN Hard-Drop test] ![Image 10: Windows Firewall - Custom Outbound Rules for Micro-segmentation] ![Image 11: NextDNS Analytics - Blocking C2 and NRD attempts] ![Image 12: Sysmon Event ID 3 - Capturing unauthorized network connection attempt] ![Image 13: Nessus Scan Results - Clean Baseline & Remediation Report]

</details>

---

<a name="phase-4-validation--soc-operations"></a>
## Phase 4: Validation & SOC Operations

<details>
<summary><b>Click to Expand: Virtualization & Monitoring Metrics</b></summary>

### Virtualization Deployment (The Technical Sandbox)
* Hypervisor Integration: Successfully deployed a multi-node virtualization environment using VMware/VirtualBox on the Ryzen 6C/12T platform to simulate a corporate enterprise network.
* Multi-OS Provisioning:
    * Node 1 (Kali Linux): Offensive security and penetration testing node.
    * Node 2 (Ubuntu Desktop/Server): Linux systems administration, user permissions, and syslog monitoring.
    * Node 3 (Windows 10 Hardened): Maintained as the primary target for security control validation and GPO enforcement.
* Resource Management: Optimized hardware allocation to ensure concurrent operation of all three nodes.
* Network Segmentation: Isolated the lab environment via Virtual NAT/Host-Only adapters.

### SOC Auditing & Incident Monitoring
* Security Event Analysis: Established a monitoring baseline by auditing system logs.
* SOC Metric - Event Volume: Total security events reviewed: 1,000+.
* SOC Metric - Key Event IDs Analyzed: 4624 (Success) / 4625 (Failed), 4672 (Admin Privileges), 4688 (New Process), 4673 / 4674 (Sensitive Privilege Use).
* SOC Metric - Defensive Validation: Documented multiple test cases for Privilege Escalation and Unauthorized Installation attempts.

### Continuous Maintenance & Compliance
* Attack Surface Management: Performed service hardening by disabling non-essential background processes.
* Patch Compliance: Maintained a 100% remediation rate for critical OS vulnerabilities by verifying all updates within 48 hours.
* Metric - Configuration Drift: Conducted weekly manual audits of local security policies.

### Disaster Recovery (DR) & Documentation
* Disaster Recovery (DR) Planning: Documented corrective measures to restore operations using hybrid backups.
* Resiliency Audit: Verified backup integrity through restoration drills using the 3-2-1-1-0 framework.
* Maintenance & Monitoring: Implemented automated verification of backup integrity and scheduled semi-annual hardware maintenance.
* Change Control: All system modifications and security policy updates are documented within this repository.

### Phase 4: Visual Evidence
![Image 9: Final Engineering Station and Windows Event Viewer Security Logs] ![Image 10: Multi-Node Lab Orchestration - VMware Workstation Pro]

</details>

---

<a name="skills-gained-through-this-project"></a>
## Skills Gained Through This Project

<details>
<summary><b>Click to Expand: Full Skills List</b></summary>

* **SOC Monitoring & Log Analysis:** Analysis of Windows Security Event Logs to detect failures and unauthorized actions using Event IDs such as 4624, 4625, 4672, 4688, 4673/4674, and 4648.
* **Incident Detection & Validation:** Simulated real-world security events and validated expected system responses through audit logs.
* **Vulnerability Management:** Patch verification, CVE remediation tracking, CIS benchmark audits & configuration drift detection.
* **Identity & Access Management (IAM):** Enforcement and validation of the Principle of Least Privilege (PoLP) through Admin vs. Standard user segmentation.
* **Endpoint & OS Hardening:** Secure OS deployment with TPM 2.0, Secure Boot, BitLocker encryption, and reduction of attack surface.
* **Security Validation & Control Testing:** Hands-on testing of security controls with documented outcomes.
* **Network-Level Security:** Implementation of Fail-Secure connectivity through VPN kill-switch testing, DNS Anti-Spoofing (DoH), and Gateway-level URL Filtering.
* **Data Loss Prevention (DLP) Fundamentals:** VPN kill-switch testing, full-disk encryption, and restricted user privileges to prevent unauthorized data access.
* **Virtualization & Lab Operations:** Deployment and management of VirtualBox/VMware environments.
* **Backup, Recovery & Resilience:** Implementation and validation of a 3-2-1-1-0 backup strategy and restoration testing.
* **[New] Threat Intelligence & DNS Security:** Integration of threat feeds to block C2 infrastructure, NRDs, and DGA.
* **[New] Advanced Behavioral Analysis:** Utilization of Sysmon for deep-visibility behavioral logging.

</details>

---

<a name="target-roles-this-project-prepares-me-for"></a>
## Target Roles This Project Prepares Me For

<details>
<summary><b>Click to Expand: Role Alignment</b></summary>

* **SOC Analyst (Tier 1 / Junior):** Prepared to monitor security alerts, analyze logs, and validate security controls. Special emphasis on detecting C2 callbacks and lateral movement.
* **Vulnerability Management Analyst (Junior / Entry-Level):** Prepared to support vulnerability scanning, patch management, and configuration compliance.
* **IAM / Access Management Analyst (Junior):** Prepared to analyze authentication events, validate privilege boundaries, and support access control.
* **Junior Security Engineer / Associate Security Engineer:** Prepared to assist with secure system builds, endpoint hardening, and control validation.
* **IT Technician / Junior Systems Administrator:** Prepared to support secure workstation builds, OS deployment, virtualization, and backup operations.
* **[New] Junior Threat Hunter:** Equipped to proactively search for indicators of compromise (IoCs) within DNS logs and host-based behavioral logs.

</details>




