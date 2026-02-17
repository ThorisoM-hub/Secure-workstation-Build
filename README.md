# Secure Workstation Build & Hardened Infrastructure Project

## Project Overview

This project documents the end-to-end security hardening and deployment of a performance-optimized workstation. I transitioned from a performance-limited Celeron system to a security-optimized Ryzen environment specifically architected to support high-density virtualization for Identity & Access Management (IAM) and SOC (Security Operations Center) labs.

## The Transformation: Celeron Bottleneck vs. Ryzen Solution

![Image 1: Collage – Old Celeron Laptop vs. New MSI/Ryzen Engineering Build]

- VM boot times reduced by approximately 60–70%  
- Lab stability improved from intermittent crashes to 24/7 sustained operation  
- Capacity increased from 1–2 limited VMs to 3–5 stable VMs simultaneously  

[Watch the Technical Execution Video on YouTube]

**Chapters:** Architecture, Firmware Hardening, OS Security, VPN Data Leak Prevention (DLP), and VM & configuration drift checks, including CIS benchmark audits and remediation of misconfigurations, demonstrating continuous system security monitoring.

## Demonstrated Scenarios

- Authentication failure & brute-force simulations: events logged and reviewed in Windows Event Viewer to validate detection and response.
- Privilege escalation detection via Windows security logs: including blocked Standard User actions and Admin special privileges, demonstrating effective enforcement of the Principle of Least Privilege.
- VPN kill-switch leak testing: to ensure secure connectivity and prevent data leaks during network interruptions.
- Vulnerability patch verification & configuration drift checks: including CIS benchmark audits and remediation of misconfigurations, demonstrating continuous system security monitoring.
- Data Loss Prevention (DLP): enforced network-level and endpoint DLP controls through VPN kill-switch testing, full-disk encryption (BitLocker), and restricted user privileges to prevent unauthorized data exfiltration and access.

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

## SDLC Methodology (Project Lifecycle)

Drawing from my Financial Information Systems (FIS) qualification, I applied the Systems Development Life Cycle (SDLC) to manage the project flow from concept to completion. This ensures a professional, requirements-driven foundation suitable for audited corporate and financial environments.

| SDLC Phase | Technical Project Application |
|------------|-------------------------------|
| 1. Planning | Defined project scope to support high-density virtualization; set requirements for 6C/12T architecture and 16GB DDR4 RAM. |
| 2. Analysis | Conducted hardware gap analysis; identified that legacy Celeron architecture lacked SLAT/VT-x support (NPT/AMD-V). |
| 3. Design | Developed logical system architecture; utilized Cisco Packet Tracer to map the connection between the Rain Router and host via Cat6. |
| 4. Implementation | Managed physical component assembly and Thermal Management; executed OS deployment and established Layer 1 physical link. |
| 5. Testing | Performed Verification & Validation (V&V); conducted Hardware stress-testing (POST/MemTest86) and validated TPM 2.0/UEFI integrity. |
| 6. Maintenance | Established Continuous Monitoring via Windows Event Viewer (Logging) and automated patch management |

![Image 2: Detailed SDLC Model Diagram]

## Technical Manifest: 18-Step Roadmap

### Phase 1: Architecture & Asset Management (FIS Standards)

- Project Initiation: Final system integration of the MSI high-performance workstation.  
- Requirements Analysis: Comparative analysis of Celeron vs. Ryzen architectures to justify upgrades.  
- Hardware Asset Management: Structured inventory tracking and lifecycle management (NIST 800-53 standard).  
- Logical Network Design: Utilizing Cisco Packet Tracer to diagram the network path from the Rain Router to the Host via Cat6 cabling.  
  - Metric: Average lab traffic latency over Cat6: <1ms local network latency.  
  - Metric: Network stability: 0 packet loss during sustained testing sessions.  

![Image 3: Components Procurement & Cisco Packet Tracer Network Diagram]

### Phase 2: Physical & Systems Integration

- Layer 1 Infrastructure: Deployment of physical Cat6 Ethernet for a stable, high-bandwidth link.  
- Firmware Hardening: Establishing Hardware Root of Trust via TPM 2.0 and UEFI Secure Boot.  
- Hardware Validation: Verification of vitals, RAM speeds, and thermal stability under high virtualization load.  
  - Validation: Sustained CPU temperature under load: 65–72°C.  
  - Validation: Zero POST or memory faults after 12-hour stress test.  
  - Electrical Hardening: Implemented external Surge Safe Power Protection to provide MOV suppression.  

![Image 4: Physical PC Interior/Cabling]  
![Image 5: BIOS Screen showing TPM 2.0 & Secure Boot ENABLED]

### Phase 3: Implementation & Security Hardening

* **Hardened OS Deployment:** Secure installation of Windows Pro, optimized for enterprise security.
* **Network Configuration:** Local IP assignment and connectivity verification via ICMP (Ping).
* **Vulnerability Management (Patch Compliance):** Completed a full **Windows Update cycle** and configured **Automatic Security Intelligence Updates** to mitigate Zero-Day exploits and known CVEs.
* **Fail-Secure Connectivity (VPN Kill-Switch):** Implementation of a **Permanent Kill-Switch** policy via Proton VPN. Performed a "Hard Drop" test by disabling the physical network interface; verified immediate termination of all outbound traffic (ICMP/HTTP) to prevent clear-text data leakage outside the encrypted tunnel.
* **DNS Anti-Spoofing & Integrity:** Enforced the use of **Private, Encrypted DNS** via the VPN tunnel to mitigate **DNS Cache Poisoning** and Man-in-the-Middle (MITM) attacks. This ensures that identity-related traffic (login portals) cannot be redirected to malicious IP addresses.
* **Gateway-Level Security (Rain Router):** Configured **Edge URL Filtering** via the Rain Web Gateway. Restricted unauthorized domains (e.g., `facebook.com`) at the DNS level to reduce the external attack surface and mitigate Shadow IT risks.
* **Host-Based Defense (Windows Firewall):** Implemented custom **Outbound Traffic Rules** within Windows Defender Firewall with Advanced Security. Implemented micro-segmentation by blocking specific non-authorized binaries from initiating external connections, simulating anti-exfiltration controls.
* **Identity & Access Management (IAM):** Enforcement of Principle of Least Privilege (PoLP) via Admin vs. Standard account segmentation.
    * **IAM Control:** Segmented **Backup-Admin** privileges to ensure only authorized identities can modify or delete the archive.
    * **Validation Action – Unauthorized Software Installation Test:**
        Simulated an unauthorized software installation from a Standard User account to validate enforcement of the Principle of Least Privilege. The installation was blocked by UAC/admin controls (logged in Event Viewer: Event ID 4624 (Logon), Event ID 4625 (Failed Logon), Event ID 4672 (Special Privileges), Event ID 4688 (Process Creation), and Event IDs 4673 / 4674 (Sensitive Privilege Use / Privilege Object Access Denied)), confirming effective separation between Admin and Standard user privileges.
        While logged in as an Admin account, I performed a system shutdown (Event ID 4672 – Special Privileges), which completed successfully, demonstrating that Admin accounts can perform elevated tasks while Standard users cannot.


* **Data-at-Rest Encryption:** Full-disk encryption via BitLocker, anchored to hardware TPM.
* **Data Protection: Backup & Storage Solutions (The "Digital Safety Net"):**
    I engineered a professional **3-2-1-1-0 Data Resiliency Framework** for **"Thoriso_critical_files.zip"**:
    * **3 Copies:** Original project files + 2 backup versions.
    * **2 Media Types:** Primary Host HDD (Internal) and Removable USB Media (External/Logical Air-Gap).
    * **1 Offsite Replicate:** Archives synced to a secure Cloud location.
    * **1 Immutable:** A "locked" copy (WORM) to prevent lateral ransomware movement.
    * **0 Errors:** Restoration Drills to prove RTO <15 mins.


![Image 6: Windows Security Dashboard (Green Checks)]  
![Image 7: BitLocker Encryption Status & VPN Kill Switch settings]  
![Image 8: IAM Setup - Admin vs. Standard User account segmentation]
 ![Image 9: Windows Command Prompt showing "General failure" during VPN Hard-Drop test]
## Phase 4: Validation & SOC Operations

### SOC Auditing & Incident Monitoring
* **Security Event Analysis:** Established a rigorous monitoring baseline by auditing system logs to distinguish between authorized behavior and potential IOCs (Indicators of Compromise).
* **SOC Metric - Event Volume:** Total security events reviewed: **1,000+**.
* **SOC Metric - Key Event IDs Analyzed:**
    * **4624** (Successful Logon) / **4625** (Failed Logon)
    * **4672** (Administrative/Special Privileges Assigned)
    * **4688** (New Process Creation)
    * **4673 / 4674** (Sensitive Privilege Use & Privilege Access attempts)
* **SOC Metric - Defensive Validation:** Documented multiple test cases for **Privilege Escalation** and **Unauthorized Installation attempts**, confirming that PoLP (Principle of Least Privilege) controls successfully triggered "Access Denied" events.

### Continuous Maintenance & Compliance
* **Attack Surface Management:** Performed service hardening by disabling non-essential background processes, reducing the host's potential exploit vectors.
* **Patch Compliance:** Maintained a 100% remediation rate for critical OS vulnerabilities by verifying all security updates within 48 hours of release.
* **Metric - Configuration Drift:** Conducted weekly manual audits of local security policies to ensure no deviations from the hardened baseline.

### Disaster Recovery (DR) & Documentation
* **Disaster Recovery (DR) Planning:** Documented corrective measures to restore operations using hybrid backups (Cloud/Local), ensuring data availability and business continuity.
* **Resiliency Audit:** Verified backup integrity through restoration drills, ensuring data availability using the **3-2-1-1-0 framework**.
* **Maintenance & Monitoring:** Implemented automated verification of backup integrity and scheduled semi-annual hardware maintenance (physical dusting and thermal optimization).
* **Change Control:** All system modifications and security policy updates are documented within this repository as a permanent audit trail for professional review.

---

### Phase 4: Visual Evidence

![Image 9: Final Engineering Station and Windows Event Viewer Security Logs]

## Skills Gained Through This Project

- **SOC Monitoring & Log Analysis**  
  Analysis of Windows Security Event Logs to detect authentication failures, unauthorized process creation, privilege escalation attempts, and administrative actions using Event IDs such as 4624, 4625, 4672, 4688, 4673/4674, and 4648.

- **Incident Detection & Validation**  
  Simulated real-world security events (unauthorized software installation, blocked privilege escalation, admin-only actions) and validated expected system responses through audit logs.

- **Vulnerability Management**  
  Patch verification, CVE remediation tracking, CIS benchmark audits &configuration drift detection.This includes the implementation of Automatic Security Intelligence Updates to mitigate Zero-Day exploits.


- **Identity & Access Management (IAM)**  
  Enforcement and validation of the Principle of Least Privilege (PoLP) through Admin vs. Standard user segmentation, UAC enforcement, and privilege auditing.

- **Endpoint & OS Hardening**  
  Secure OS deployment with TPM 2.0, Secure Boot, BitLocker full-disk encryption, and reduction of attack surface through system 
- **Security Validation & Control Testing**  
  Hands-on testing of security controls with documented outcomes, confirming correct enforcement and logging behavior.
* **Network-Level Security**
    Implementation of **Fail-Secure connectivity** through VPN kill-switch testing, **DNS Anti-Spoofing (DoH)**, and **Gateway-level URL Filtering**. Enforced network-level controls using **custom Windows Defender Firewall outbound rules and micro-segmentation** to block non-authorized binaries from initiating external connections.

* **Data Loss Prevention (DLP) Fundamentals**
    VPN kill-switch testing, full-disk encryption, and restricted user privileges to prevent unauthorized data access and data exfiltration. Enforced endpoint controls to ensure sensitive data remains within the encrypted environment and is protected from unauthorized exfiltration.

- **Virtualization & Lab Operations**  
  Deployment and management of VirtualBox/VMware environments to support SOC and security testing labs.

- **Backup, Recovery & Resilience**  
  Implementation and validation of a 3-2-1-1-0 backup strategy, restoration testing, and ransomware-resilient design principles.

---

## Target Roles This Project Prepares Me For

This project was intentionally designed to align with real-world SOC and security operations responsibilities:

- **SOC Analyst (Tier 1 / Junior)**  
  Prepared to monitor security alerts, analyze logs, identify suspicious activity, validate security controls, and escalate confirmed incidents.

- **Vulnerability Management Analyst (Junior / Entry-Level)**  
  Prepared to support vulnerability scanning, patch management, configuration compliance, and remediation tracking.

- **IAM / Access Management Analyst (Junior)**  
  Prepared to analyze authentication and authorization events, validate privilege boundaries, and support access control enforcement.

- **Junior Security Engineer / Associate Security Engineer**  
  Prepared to assist with secure system builds, endpoint hardening, control validation, and security architecture support.

- **IT Technician / Junior Systems Administrator**  
  Prepared to support secure workstation builds, OS deployment, virtualization, monitoring, patching, and backup operations.