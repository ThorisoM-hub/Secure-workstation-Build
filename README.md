# Secure Workstation Build & Engineering Project

### Project Overview
This project documents the end-to-end engineering of a secure, high-performance workstation. I transitioned from a performance-limited Celeron system to a hardware-hardened Ryzen environment to support high-density virtualization for **IAM and SOC Operations**.

### The Transformation: Celeron Bottleneck vs. Ryzen Solution
![Image 1: Collage - Old Celeron Laptop vs. New MSI/Ryzen Engineering Build]

---

### Full Project Video Walkthrough
[Click here to watch the full Engineering Process on YouTube](INSERT_YOUR_YOUTUBE_LINK_HERE)
*Chapters: Architecture, BIOS Security, OS Hardening, VPN Kill Switch, and VM Orchestration.*

---

### SDLC Methodology (Project Lifecycle)
From my FIS qualification, I applied the Systems Development Life Cycle (SDLC) to manage the project flow from concept to completion. This ensures a professional, requirements-driven foundation.


| SDLC Phase | Project Application |
| :--- | :--- |
| **1. Planning** | Defined project scope, virtualization goals, and resource constraints. |
| **2. Analysis** | Conducted hardware gap analysis (Celeron vs. Ryzen) and requirements gathering. |
| **3. Design** | Developed logical system architecture and network mapping. |
| **4. Implementation** | Managed the procurement and physical rollout of the system. |
| **5. Testing** | Validated security configurations and system stability. |
| **6. Maintenance** | Established version control (GitHub) and ongoing vulnerability management. |

![Image 2: Detailed SDLC Model Diagram]

---

### Systems Engineering Lifecycle (Technical Execution)
The physical and technical build was governed by engineering lifecycle phases to ensure high availability and hardware-level security.

| Engineering Phase | Technical Execution |
| :--- | :--- |
| **1. Requirements Analysis** | Specifying 6C/12T CPU and 16GB RAM for multi-threaded VM operations. |
| **2. Physical Integration** | Component assembly, thermal management, and Layer 1 (Cat6) networking. |
| **3. System Security** | Establishing Hardware Root of Trust via TPM 2.0 and UEFI Secure Boot. |
| **4. Verification** | Hardware stress-testing (POST) and network connectivity validation (ICMP). |

![Image 3: Systems Engineering V-model lifecycle]

---

### Technical Manifest (17-Step Engineering Pipeline)

#### Phase 1: Architecture & Procurement (FIS Methodology)
1. **Project Initiation:** Final assembly of the MSI high-performance workstation.
2. **Requirements Analysis:** Comparative analysis of Celeron vs. Ryzen architectures to justify the upgrade.
3. **Asset Procurement:** Structured inventory management and budget tracking of components.
4. **Logical Design:** Architectural mapping of the network environment using Cisco Packet Tracer.
![Image 4: Components Procurement & Cisco Packet Tracer Network Diagram]

#### Phase 2: Physical & Systems Engineering Integration
5. **Layer 1 Infrastructure:** Integration of physical Cat6 cabling to ensure a 1Gbps "High-Availability" link.
6. **Firmware Security:** Configuration of **TPM 2.0 and UEFI Secure Boot** to establish a **Hardware Root of Trust**.
7. **Hardware POST & BIOS Validation:** Verification of system vitals, RAM speeds, and thermal stability.
![Image 5: Physical PC Interior/Cabling]
![Image 6: BIOS Screen showing TPM 2.0 & Secure Boot ENABLED]

#### Phase 3: Implementation & Security Hardening
8. **Secure OS Deployment:** Clean installation of Windows Pro, optimized for hardware-based security.
9. **Network Integration:** Static IP assignment and connectivity verification via ICMP (Ping).
10. **Identity & Access Management (IAM):** Implementation of the **Principle of Least Privilege (PoLP)** via Admin vs. Standard account segmentation.
11. **Data-at-Rest Protection:** Full-disk encryption via **BitLocker**, linked to the TPM 2.0 module.
12. **Perimeter Defense & VPN:** Configuration of Windows Defender Firewall and implementation of a **VPN with a Kill Switch** to prevent IP leaks during labs.
13. **Vulnerability Management:** Ensuring the host system is fully patched via **Windows Update** to mitigate known risks.
![Image 7: Windows Security Dashboard (Green Checks)]
![Image 8: BitLocker Encryption Status & VPN Kill Switch settings]
![Image 9: IAM Setup - Admin vs. Standard User account segmentation]

#### Phase 4: Validation & VM Operations
14. **Environment Orchestration:** Deployment of **VirtualBox/VMware** to host security labs.
15. **VM Security Hardening:** Running updates within the guest OS (Kali Linux) to ensure the lab environment is patched.
16. **Security Auditing:** Configuration of Windows Event Viewer to monitor security logs and access events.
17. **Change Control & Documentation:** Maintenance of this GitHub repository as a professional version-controlled log.
![Image 10: VirtualBox running Kali Linux & Windows Server]
![Image 11: Final Engineering Station and Windows Event Viewer Security Logs]
