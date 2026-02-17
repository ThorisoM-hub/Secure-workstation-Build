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

## Phase 3: Implementation & Security Hardening

### 1. Hardened OS Deployment
* **Environment:** Secure installation of Windows 11 Pro, optimized for enterprise-grade security.
* **Network Foundation:** Static Local IP assignment with connectivity verification via ICMP (Ping) to establish a stable internal baseline.

### 2. Fail-Secure Connectivity (VPN Kill-Switch)
* **Policy:** Implementation of a **Permanent Kill-Switch** via Proton VPN.
* **Validation:** Performed a "Hard Drop" test by manually disabling the physical network interface. 
* **Result:** Verified 0% data leakage; all outbound traffic (ICMP/HTTP) was immediately terminated, preventing clear-text exposure outside the encrypted tunnel.


### 3. DNS Integrity & Anti-Spoofing
* **Control:** Enforced private, encrypted DNS lookups through the VPN tunnel.
* **Objective:** Mitigates **DNS Cache Poisoning** and **Man-in-the-Middle (MITM)** attacks. This ensures that identity-sensitive login portals (IAM) cannot be redirected to malicious IP addresses.


### 4. Gateway-Level Security (Rain Router)
* **Edge Defense:** Configured **Edge URL Filtering** via the Rain Web Gateway.
* **Control:** Restricted unauthorized domains (e.g., `facebook.com`) at the DNS level to reduce the external attack surface and mitigate Shadow IT risks.

### 5. Host-Based Defense (Windows Firewall)
* **Micro-segmentation:** **Implemented** custom Outbound Traffic Rules within Windows Defender Firewall with Advanced Security.
* **Logic:** Blocked non-authorized binaries from initiating external connections, simulating enterprise anti-exfiltration controls.


### 6. Identity & Access Management (IAM)
* **Principle:** Enforcement of **Principle of Least Privilege (PoLP)** via Admin vs. Standard account segmentation.
* **Privilege Control:** Segmented **Backup-Admin** privileges to ensure only authorized identities can modify or delete the archive.
* **Validation Action (Installation Test):**
    * Simulated an unauthorized software installation from a Standard User account.
    * **Result:** Installation blocked by UAC/Admin controls.
    * **Forensic Evidence:** Logged in Windows Event Viewer under **Event IDs 4688** (Process Creation) and **4673** (Sensitive Privilege Use).


### 7. Data Protection & Resiliency (The "Digital Safety Net")
* **Encryption:** Full-disk encryption via **BitLocker**, anchored to hardware TPM.
* **3-2-1-1-0 Framework:** Engineered for **"Thoriso_critical_files.zip"**:
    * **3 Copies:** Original + 2 backups.
    * **2 Media Types:** Internal HDD + Removable USB (Logical Air-Gap).
    * **1 Offsite:** Secure Cloud replication.
    * **1 Immutable:** **WORM** (Write Once, Read Many) copy to prevent Ransomware modification.
    * **0 Errors:** Verified via restoration drills (RTO < 15 mins).



![Image 6: Windows Security Dashboard (Green Checks)]  
![Image 7: BitLocker Encryption Status & VPN Kill Switch settings]  
![Image 8: IAM Setup - Admin vs. Standard User account segmentation]

### Phase 4: Validation & VM Operations

**Vulnerability Management:** Ensuring the host system is fully patched via Windows Update to mitigate known CVEs.  
- Outcome: Detected and remediated multiple CIS benchmark deviations on initial build.  
- Outcome: Eliminated unnecessary services and reduced attack surface by ~30%.  
- Metric: Number of CVEs mitigated: tracked weekly, average 15–20 critical/high severity per month.  
- Metric: Patch compliance: 100% of lab and host VMs updated within 48 hours of patch release.  
- Metric: Configuration drift detection: weekly CIS Benchmark audits with <2 deviations.  
- Metric: Vulnerability scanning: quarterly scans of all VMs using OpenVAS/Nessus; results documented and remediated within 1 week.

- Hypervisor Orchestration: Deployment of VirtualBox/VMware to host security labs (Kali Linux, Windows Server).  

- Security Auditing: Configuration of Windows Event Viewer to monitor security logs and access events, including blocked unauthorized software installation attempts from Standard accounts and privileged admin actions.  
  - SOC Metric: Total security events reviewed: 1,000+.  
  - SOC Metric: Key Event IDs analyzed:  
    4624 (Logon), 4625 (Failed Logon),  
    4672 (Special Privileges), 4688,  
    4673 / 4674 (Process creation & privilege access attempts).  
  - SOC Metric: Privilege escalation and unauthorized installation test cases: Multiple.

- Disaster Recovery (DR) Planning: Documented corrective measures to restore operations using hybrid backups.  
- Maintenance & Monitoring: Automated verification of backup integrity and semi-annual hardware dusting.  
- Change Control & Documentation: Maintenance of this repository as a professional audit trail.  

![Image 9: Final Engineering Station and Windows Event Viewer Security Logs]


## Skills Gained Through This Project

- **SOC Monitoring & Log Analysis**  
  Analysis of Windows Security Event Logs to detect authentication failures, unauthorized process creation, privilege escalation attempts, and administrative actions using Event IDs such as 4624, 4625, 4672, 4688, 4673/4674, and 4648.

- **Incident Detection & Validation**  
  Simulated real-world security events (unauthorized software installation, blocked privilege escalation, admin-only actions) and validated expected system responses through audit logs.

- **Vulnerability Management**  
  Patch verification, CVE remediation tracking, CIS benchmark audits, configuration drift detection, and vulnerability scanning using OpenVAS/Nessus.

- **Identity & Access Management (IAM)**  
  Enforcement and validation of the Principle of Least Privilege (PoLP) through Admin vs. Standard user segmentation, UAC enforcement, and privilege auditing.

- **Endpoint & OS Hardening**  
  Secure OS deployment with TPM 2.0, Secure Boot, BitLocker full-disk encryption, and reduction of attack surface through system hardening.

- **Data Loss Prevention (DLP) Fundamentals**  
  VPN kill-switch testing, full-disk encryption, and restricted user privileges to prevent unauthorized data access and data exfiltration.

- **Security Validation & Control Testing**  
  Hands-on testing of security controls with documented outcomes, confirming correct enforcement and logging behavior.

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