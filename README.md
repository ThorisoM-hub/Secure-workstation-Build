
# Secure Workstation Build & Hardened Infrastructure Project




---

### Project Overview & "The Transformation"
This project documents the end-to-end security hardening and deployment of a performance-optimized workstation. I transitioned from a legacy Celeron system to a security-optimized AMD Ryzen (6C/12T) environment specifically architected to support High-Density Virtualization for Identity & Access Management (IAM) and SOC (Security Operations Center) labs.

* Performance Delta: VM boot times reduced by approximately 60–70%.
* Stability: Transitioned from intermittent crashes to 24/7 sustained uptime.
* Capacity: Scaled from 1–2 limited VMs to 3-5 stable concurrent VMs.

---

### Technical Execution Video
[Watch the 30-Minute Technical Masterclass on YouTube](YOUR_LINK_HERE)
*Timestamps provided in video description for: Architecture, Firmware Hardening, VPN Kill-Switch Testing, and SOC Auditing.*

---

### Table of Contents (Interactive)
1. Architecture Summary
2. SDLC Methodology
3. Demonstrated Scenarios & Technical Validations
4. Phase 4: Validation & SOC Operations (The Sandbox)
5. 18-Step Technical Manifest (Deep Dive)
6. Skills Gained & Target Roles

---

### Architecture Summary
| Component | Implementation |
| :--- | :--- |
| CPU | AMD Ryzen 5 (6C/12T) |
| Memory | 16 GB DDR4 (Optimized for Virtualization) |
| Firmware Security | TPM 2.0, UEFI Secure Boot (Root of Trust) |
| Encryption | BitLocker (TPM-bound Full Disk Encryption) |
| Host OS | Windows 10/11 Pro (Hardened Baseline) |
| Hypervisor | VMware Workstation / VirtualBox |
| Network | Cat6 Physical Link to Rain Web Gateway |

---

### SDLC Methodology (Project Lifecycle)
Drawing from my Financial Information Systems (FIS) qualification, I applied the Systems Development Life Cycle (SDLC) to manage the project flow. This ensures a professional, requirements-driven foundation suitable for audited corporate environments.



<details>
<summary><b>Click to Expand: SDLC Project Mapping</b></summary>

| SDLC Phase | Technical Project Application |
| :--- | :--- |
| 1. Planning | Defined scope for high-density virtualization; requirement setting for 6C/12T architecture. |
| 2. Analysis | Conducted hardware gap analysis; identified Celeron lack of SLAT/VT-x support. |
| 3. Design | Developed logical system architecture; mapped network path via Cisco Packet Tracer. |
| 4. Implementation | Physical assembly, Thermal Management (65–72°C), and Hardened OS deployment. |
| 5. Testing | Verification & Validation (V&V); Hardware stress-testing and TPM integrity checks. |
| 6. Maintenance | Continuous Monitoring via Windows Event Viewer and automated patch management. |

</details>

---

### Demonstrated Scenarios & Technical Validations
These scenarios represent the "Proof of Work" for SOC and IAM roles.

* Authentication & Brute-Force Monitoring: Audited 1,000+ security events (Event IDs 4624/4625) to distinguish between authorized behavior and potential IOCs.
* IAM Privilege Escalation Detection: Validated enforcement of Principle of Least Privilege (PoLP). Confirmed via Event IDs 4672/4688 that Standard User accounts triggered "Access Denied" for unauthorized software installs.
* VPN Kill-Switch Leak Testing: Performed a "Hard Drop" test by disabling the physical network interface; verified via CMD ("General failure") the immediate termination of all outbound traffic (ICMP/HTTP).
* Egress Intelligence & C2 Mitigation: Integrated NextDNS Threat Intelligence to simulate connections to malicious domains. Verified 100% block rate for Command & Control (C2) callbacks.
* Behavioral Detection (Sysmon): Implemented Sysmon to capture advanced telemetry (Event ID 3), detecting "Living-off-the-Land" (LotL) techniques hidden in trusted processes.
* Data Resiliency (3-2-1-1-0): Engineered a professional data framework. Demonstrated an RTO of <15 minutes through restoration drills of "Thoriso_critical_files.zip".



---

### Phase 4: Validation & SOC Operations
This section confirms the live operational status of the virtualization lab.

#### Virtualization Deployment (The Technical Sandbox)
* Hypervisor Integration: Successfully deployed a multi-node environment on the Ryzen platform.
* Node 1 (Kali Linux): Offensive node for internal vulnerability assessments.
* Node 2 (Ubuntu Desktop): Infrastructure node for mastering Linux SysAdmin (Fintech-specific).
* Node 3 (Windows 10 Hardened): Primary target for GPO enforcement and auditing.
* Network Segmentation: Isolated lab environment via Virtual NAT/Host-Only adapters to prevent production cross-contamination.

#### SOC Auditing & Maintenance
* Configuration Drift: Weekly manual audits of local security policies.
* Patch Compliance: 100% remediation rate for critical OS vulnerabilities within 48 hours.
* Change Control: All system modifications are documented in this repository as a permanent audit trail.

---

### Technical Manifest: 18-Step Roadmap
This section contains the deep-dive technical heart of the project.

<details>
<summary><b>Click to Expand: Full 18-Step Implementation Details</b></summary>

#### Phase 1: Architecture & Asset Management
1. Project Initiation: Final system integration of the MSI workstation.
2. Requirements Analysis: Comparative analysis of Celeron vs. Ryzen architectures.
3. Asset Management: Inventory tracking (NIST 800-53 standard).
4. Logical Design: Cisco Packet Tracer diagramming (Latency: <1ms local).

#### Phase 2: Physical & Systems Integration
5. Layer 1 Infrastructure: Cat6 Ethernet deployment.
6. Firmware Hardening: TPM 2.0 & UEFI Secure Boot activation.
7. Hardware Validation: 12-hour stress test (Zero POST/Memory faults).
8. Electrical Hardening: MOV suppression via external Surge Protection.

#### Phase 3: Implementation & Security Hardening
9. Hardened OS Deployment: Secure Windows Pro installation.
10. Network Configuration: ICMP connectivity verification.
11. Fail-Secure Connectivity: Proton VPN Permanent Kill-Switch implementation.
12. DNS Anti-Spoofing: Enforced Encrypted DNS to mitigate MITM attacks.
13. Gateway-Level Security: Edge URL Filtering via Rain Web Gateway.
14. Host-Based Defense: Custom Outbound Firewall Rules for Micro-segmentation.
    * Analogy: The "Security Guard at the Exit" (Egress Filtering).
    * Analogy: The "Approved Employee List" (Binary Whitelisting).
15. Critical Blind Spot Analysis: Documented limitations of Stateful Firewalls (Lack of DPI).

#### Phase 4: Advanced Behavioral Layers
16. NextDNS C2 Filtering: Real-time blocking of "Bad Neighborhoods" and NRDs.
17. Sysmon Integration: Behavioral logging for stealthy movement detection.
18. Nessus Vulnerability Assessment: Periodic credentialed scanning for unpatched risk.

</details>

---

### Skills Gained & Target Roles
* SOC Monitoring: Event Analysis, IOC detection, and Baseline Establishment.
* Vulnerability Management: Patching, CVE tracking, and CIS Benchmarks.
* IAM Specialist: PoLP enforcement, UAC auditing, and Identity Segmentation.
* Infrastructure Engineering: Hypervisor management, 3-2-1-1-0 Resilience, and HW Root of Trust.

Target Roles: Junior SOC Analyst, IAM Analyst, Junior Security Engineer, IT Systems Administrator (Fintech).

---

### Visual Evidence Gallery
* Image 1: Celeron vs. Ryzen Build Collage
* Image 9: VPN "Hard-Drop" General Failure Result
* Image 10: Multi-Node Lab Orchestration - VMware showing Kali, Ubuntu, and Windows 10 Nodes
* Image 13: Nessus Scan Clean Baseline Report

---
End of Documentation
