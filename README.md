# Enterprise Hybrid Architecture: Infrastructure Core, Virtualization Redundancy & Automated Lifecycle Operations

## 📌 Project Architecture & Design Overview
This repository delivers an end-to-end blueprint for a production-ready, highly secure **Windows Server Enterprise Infrastructure** bound under the corporate Active Directory domain `zohdy.local`. 

The architecture is explicitly designed to eliminate single points of failure (SPOF) by leveraging **Windows Server Core** headless virtualization nodes, automated failover replication fabrics, deterministic software-defined networking, multi-tenant storage security layers, localized patch distribution loops, and systematic disaster recovery verification workflows.

---

## 🛠️ Deep-Dive Infrastructure Components

### 1. Headless Virtualization & High Availability (Hyper-V & Server Core)
* **Minimalist Host Architecture:** Multi-node infrastructure incorporates a headless deployment model via **Windows Server 2022 Standard (Server Core Edition)** on the secondary node `CORE2`. Managed dynamically via the bare-metal `SConfig` CLI utility to slash computing overhead and enforce a minimized attack surface.
* **Hyper-V Replica Fabric:** Orchestrated an asynchronous virtual machine replication engine between the primary directory server (`PDC-SRV`) and the dedicated Server Core replica target (`CORE2`), verifying real-time synchronization of production instances (`vm-Gui-hyper-v-replica`) for immediate high-availability failover.

### 2. Deterministic Name Resolution & IP Lifecycle Management (DNS/DHCP)
* **Automated Network Scopes:** Managed the corporate subnet (`192.168.1.0/24`) using dynamic DHCP servers. Hard MAC-to-IP reservations are strictly configured (e.g., locking client `PC-01.zohdy.local` to `192.168.1.100`) to provide persistent cryptographic network identities.
* **Hierarchical DNS Forward Lookup Zones:** Engineered a granular DNS schema hosting production root lookup trees along with auxiliary corporate lookup spaces (`omar.com`, `zohdy1.com`). Active host configuration contains precise static Host (A) bindings for directory control planes and web backends (`pdc-srv -> 192.168.1.2`, `websrv -> 192.168.1.4`, `webhr -> 192.168.1.6`) alongside canonical CNAME abstractions (`www`, `web`).

### 3. Role-Based Storage Governance & Micro-Segmented File Shares
* **Advanced NTFS Permissions Matrix:** Provisioned cross-departmental file spaces (`\\PDC-SRV\HR-Data`) mapped to distinct Active Directory Security Groups (`ZOHDY\HR-Group`). Access Control Lists (ACLs) are strictly configured to isolate operational access loops.
* **Hidden Multi-Tenant Shares:** Implemented secure network shares utilizing hidden administrative dollar-sign syntax (`\\PDC-SRV\new rooming$`, `\\PDC-SRV\home$`) to abstract high-risk internal shares from unauthorized user endpoint scans.
* **Resource Quota Enforcement:** Deployed active volume-level NTFS hard disk quotas to bound distributed user directories to a maximum allocation cap of `2 GB`, tracking usage profiles with systematic early warning logs triggered at `1.8 GB`.
* **Dynamic Share Mounting:** Implemented targeted Active Directory Group Policy Preferences (GPP) to seamlessly and programmatically mount network storage repositories as local persistent client system drives (`H:`) on user initialization.

### 4. Configuration Baselines & Active Directory GPO Enforcement
* **Mandated User Workspace Environments:** Enforced unified organizational enterprise branding and locked machine compliance parameters targeting designated active directory Organizational Units (OUs) like `Sales`.
* **Universal GPO Path Resolution:** Deployed centralized desktop wallpaper path mappings through administrative templates, enforcing a common corporate background utilizing highly available network UNC paths (`\\pdc-srv\background\bg.jpg`).

### 5. Automated Bare-Metal Provisioning & Local Patch Management (WDS/WSUS)
* **Automated OS Ingestion (WDS via PXE):** Configured Windows Deployment Services (WDS) acting as an active PXE-boot server. It stages clean architectural deployment images (`Windows 10 Pro x64`) across the local area network to support rapid, low-touch bare-metal provisioning loops.
* **Bandwidth-Optimized Patch Ecosystem (WSUS):** Deployed a local Windows Server Update Services (WSUS) endpoint to classify, manage, cache, and approve update packages and critical security hotfixes, ensuring absolute network perimeter patch compliance without consuming external WAN pipelines.

### 6. Corporate Web Delivery & Managed Fleet Printing (IIS Engine)
* **Multi-Tenant IIS Web Farms:** Leveraged Internet Information Services (IIS) to operate multiple corporate web delivery nodes (`hr site`, `sales site`, `web6`). Implemented custom socket multi-binding targeting specialized port access vectors (`192.168.1.4:7777`) serving dedicated local HTML application targets.
* **Centralized Fleet Printing Infrastructure:** Established a unified enterprise print server topology via Print Management. Deployed secure isolated print driver layers (e.g., `Dell 1230c Color Laser Printer GDI`) over active network-shared endpoints.

### 7. Administrative Diagnostics & Disaster Recovery Assurance
* **Disaster Recovery Backup Fabrics:** Designed a scheduled **Windows Server Backup** policy performing daily automated bare-metal volume captures and Active Directory system-state preservation tasks at `12:00 AM` targeting local isolated arrays (`D:`).
* **PowerShell Remote Diagnostics:** Staged administrative troubleshooting pipelines by invoking direct Remote Assistance invitations across the CLI (`msra /offerra`). This maps secure, authenticated administrative pathways to remote system endpoints (`192.168.1.100`) via domain-vetted credentials.

---

## 📊 Empirical Evidence & Project Artifacts

> 💡 **Architectural Note:** All underlying configuration states, console outputs, and enterprise deployment verifications are fully cataloged within the local repository repository environment.

### I. Comprehensive Infrastructure Verification Gallery

To review the live deployment states, active directory lookups, policy enforcement screens, and headless virtualization frames, reference the verified production artifacts chronologically below:

| Artifact Reference | Production System Documentation Frame |
| :--- | :--- |
| **System Identity & Drive Mapping** | ![Infrastructure Frame 1](images/1755191177235_2.jpg) |
| **Active Hard Volume Disk Quotas** | ![Infrastructure Frame 2](images/1755191188175.jpg) |
| **WDS PXE Boot Ingestion Core** | ![Infrastructure Frame 3](images/1755191186137_2.jpg) |
| **WSUS Central Patch Topologies** | ![Infrastructure Frame 4](images/1755191188221_2.jpg) |
| **IIS App Pool Multi-Site Hierarchy** | ![Infrastructure Frame 5](images/1755191191396.jpg) |
| **Active Port-Binding Application Target** | ![Infrastructure Frame 6](images/1755191185668_2.jpg) |
| **Windows Server Backup Execution Logs** | ![Infrastructure Frame 7](images/1755191191517_2.jpg) |
| **PowerShell Remote Diagnostics CLI** | ![Infrastructure Frame 8](images/1755191192824.jpg) |
| **Printer Subsystem Management** | ![Infrastructure Frame 9](images/1755191192598.jpg) |
| **Server Core Headless Node (SConfig)** | ![Infrastructure Frame 10](images/1755191193026_2.jpg) |
| **Authenticated RDP Identity Handshake** | ![Infrastructure Frame 11](images/1755191193209_2.jpg) |
| **NTFS Directory Access Control Lists (ACL)** | ![Infrastructure Frame 12](images/1755191194141_2.jpg) |
| **DNS Database Forward Lookup Zones** | ![Infrastructure Frame 13](images/1755191195074_2.jpg) |
| **Hyper-V Replica Synchronization Fabrics** | ![Infrastructure Frame 14](images/1755191195834_2.jpg) |
| **Universal GPO Workspace Enforcements** | ![Infrastructure Frame 15](images/1755191196053_2.jpg) |
| **Print Management Driver Subsystems** | ![Infrastructure Frame 16](images/1755191197948_2.jpg) |

---
  ![Disk Quotas](images/1755191188175.jpg)
  ![IIS Dashboard](images/1755191191396.jpg)
