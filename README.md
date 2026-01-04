# Secure Workstation Build & Hardened Infrastructure Project

## Project Overview
This project documents the end-to-end security hardening and deployment of a performance-optimized workstation. I transitioned from a performance-limited Celeron system to a security-optimized Ryzen environment specifically architected to support high-density virtualization for Identity & Access Management (IAM) and SOC (Security Operations Center) labs.

### Added Context & Scope
* **Host system resources:** 16GB DDR4 RAM, 6C/12T CPU
* **Active lab usage:** 3–5 concurrent virtual machines
* **Typical hypervisor utilization during SOC scenarios:** 65–85% CPU, ~12–14GB RAM in use
* **Purpose-built for:** Continuous SOC investigations, IAM testing, vulnerability analysis, and CTF simulations

---

## The Transformation: Celeron Bottleneck vs. Ryzen Solution
![Image 1: Collage - Old Celeron Laptop vs. New MSI/Ryzen Engineering Build]

### Measured Performance Outcome
* **VM boot times:** Reduced by approximately 60–70%
* **Lab stability:** Improved from intermittent crashes to 24/7 sustained operation
* **Capacity:** Increased from 1–2 limited VMs to 3–5 stable VMs simultaneously

---

## Full Project Video Walkthrough
[Watch the Technical Execution Video on YouTube]

**Chapters:** Architecture, Firmware Hardening, OS Security, VPN Data Leak Prevention (DLP), and VM Orchestration.

### Demonstrated Scenarios
* Authentication failure & brute-force simulations
* Privilege escalation detection via Windows security logs
* VPN kill-switch leak testing
* Vulnerability patch verification & configuration drift checks

---

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

## SDLC Methodology (Project Lifecycle)
Drawing from my **Financial Information Systems (FIS)** qualification, I applied the Systems Development Life Cycle (SDLC) to manage the project flow from concept to completion. This ensures a professional, requirements-driven foundation suitable for audited corporate and financial environments.

> **Operational Benefit:** The SDLC approach enabled traceability between requirements, controls, testing results, and documented outcomes — closely mirroring real SOC change-management workflows.

| SDLC Phase | Technical Project Application |
| :--- | :--- |
| **1. Planning** | Defined project scope to support high-density virtualization; set requirements for 6C/12T architecture and 16GB DDR4 RAM. |
| **2. Analysis** | Conducted hardware gap analysis; identified that legacy Celeron architecture lacked SLAT/VT-x support (NPT/AMD-V). |
| **3. Design** | Developed logical system architecture; utilized Cisco Packet Tracer to map the connection between the Rain Router and host via Cat6. |
| **4. Implementation** | Managed physical component assembly and Thermal Management; executed OS deployment and established Layer 1 physical link. |
| **5. Testing** | Performed Verification & Validation (V&V); conducted Hardware stress-testing (POST/MemTest86) and validated TPM 2.0/UEFI integrity. |
| **6. Maintenance** | Established Continuous Monitoring via Windows Event Viewer (Logging) and automated patch management. |

![Image 2: Detailed SDLC Model Diagram]

---

## Technical Manifest: 17-Step Technical Implementation Roadmap

### Phase 1: Architecture & Asset Management (FIS Standards)
1. **Project Initiation:** Final system integration of the MSI high-performance workstation.
2. **Requirements Analysis:** Comparative analysis of Celeron vs. Ryzen architectures to justify upgrades.
3. **Hardware Asset Management:** Structured inventory tracking and lifecycle management (NIST 800-53 standard).
4. **Logical Network Design:** Utilizing Cisco Packet Tracer to diagram the network path from the Rain Router to the Host via Cat6 cabling.
   * *Metric:* Average lab traffic latency over Cat6: <1ms local network latency.
   * *Metric:* Network stability: 0 packet loss during sustained testing sessions.

![Image 4: Components Procurement & Cisco Packet Tracer Network Diagram]

### Phase 2: Physical & Systems Integration
5. **Layer 1 Infrastructure:** Deployment of physical Cat6 Ethernet cabling to the Rain Router to ensure a stable, high-bandwidth link.
6. **Firmware Hardening:** Establishing a Hardware Root of Trust via TPM 2.0 and UEFI Secure Boot to prevent bootkit attacks.
7. **Hardware Validation:** Verification of vitals, RAM speeds, and thermal stability under high virtualization load.
   * *Validation:* Sustained CPU temperature under load: 65–72°C.
   * *Validation:* Zero POST or memory faults after 12-hour stress test.

![Image 5: Physical PC Interior/Cabling]
![Image 6: BIOS Screen showing TPM 2.0 & Secure Boot ENABLED]

### Phase 3: Implementation & Security Hardening
8. **Hardened OS Deployment:** Secure installation of Windows Pro, optimized for enterprise-grade security features.
9. **Network Configuration:** Local IP assignment and connectivity verification via ICMP (Ping) through the Cat6 link.
10. **Identity & Access Management (IAM):** Enforcement of Principle of Least Privilege (PoLP) via Admin vs. Standard account segmentation.
11. **Data-at-Rest Encryption:** Full-disk encryption via BitLocker, anchored to the hardware TPM module.
12. **Network Perimeter Defense:** Host-based firewall configuration and VPN with Kill Switch to prevent IP leaks.
13. **Vulnerability Management:** Ensuring the host system is fully patched via Windows Update to mitigate known CVEs.
    * *Outcome:* Detected and remediated multiple CIS benchmark deviations on initial build.
    * *Outcome:* Eliminated unnecessary services and reduced attack surface by ~30%.

![Image 7: Windows Security Dashboard (Green Checks)]
![Image 8: BitLocker Encryption Status & VPN Kill Switch settings]
![Image 9: IAM Setup - Admin vs. Standard User account segmentation]

### Phase 4: Validation & VM Operations
14. **Hypervisor Orchestration:** Deployment of VirtualBox/VMware to host security labs (Kali Linux, Windows Server).
15. **Guest OS Hardening:** Patching and securing guest environments to maintain a "Clean-Room" lab state.
16. **Security Auditing:** Configuration of Windows Event Viewer to monitor security logs and access events.
    * *SOC Metric:* Total security events reviewed: 1,000+.
    * *SOC Metric:* Key Event IDs analyzed: 4624 (Logon), 4625 (Failed Logon), 4672 (Special Privileges).
    * *SOC Metric:* Privilege escalation test cases: Multiple successful detections.
17. **Change Control & Documentation:** Maintenance of this repository as a professional audit trail and version-controlled log.

![Image 10: VirtualBox running Kali Linux & Windows Server]
![Image 11: Final Engineering Station and Windows Event Viewer Security Logs]

