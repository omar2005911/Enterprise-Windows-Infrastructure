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

## 📊 Project Artifacts & Verification
> 💡 **Repository Note:** Detailed step-by-step console logs, active directory forward zones, group policies, and network interface screenshots are fully cataloged and accessible within the `images/` directory of this repository for active compliance audits.
