# Week 1: System Planning and Setup

## 1. System Architecture Diagram

[Insert your diagram here - use draw.io]

**Explanation:**
- **Host Machine:** My Windows 11 laptop running VirtualBox
- **Workstation VM:** Ubuntu Desktop with GUI for administration
- **Server VM:** Ubuntu Server (headless) accessed via SSH
- **Network:** Host-only adapter for secure internal communication

## 2. Distribution Selection Justification

### Why Ubuntu Server 22.04 LTS?
- **Beginner-friendly:** Extensive documentation and community support
- **Long-Term Support (LTS):** Security updates until 2027
- **Industry Standard:** Widely used in cloud and enterprise environments
- **Headless by Default:** Perfect for server operations without GUI overhead

### Alternatives Considered:
- **CentOS Stream:** More enterprise-focused but less beginner-friendly
- **Debian:** Extremely stable but slower update cycle
- **Fedora Server:** Cutting-edge features but shorter support lifecycle

## 3. Workstation Configuration Decision

**Chosen Option:** Ubuntu Desktop VM (Option A)

**Reasons:**
1. **Graphical Interface:** Easier to manage files, take screenshots, and use tools
2. **Isolation:** Keeps my host machine clean and separates coursework environment
3. **Learning Progression:** Simulates real-world remote administration from a separate system
4. **Consistency:** Both VMs use Ubuntu, reducing compatibility issues

## 4. Network Configuration

### VirtualBox Settings:
- **Adapter 1:** NAT (for internet access)
- **Adapter 2:** Host-only Adapter (for VM-to-VM communication)

### IP Addresses Discovered:
- **Workstation VM:** 192.168.56.101
- **Server VM:** 192.168.56.102

[Screenshot: VirtualBox Network Settings]
[Screenshot: ip addr output from both VMs]

## 5. System Specifications

### Workstation VM Specifications:
[Screenshot: uname -a output]
**Kernel:** 5.15.0-xx-generic x86_64

[Screenshot: free -h output]
**Memory:** 4GB total, XX available

[Screenshot: df -h output]
**Disk:** 25GB total, XX used

[Screenshot: lsb_release -a output]
**OS:** Ubuntu 22.04.3 LTS

### Server VM Specifications:
[Screenshot: uname -a output]
**Kernel:** 5.15.0-xx-generic x86_64

[Screenshot: free -h output]
**Memory:** 2GB total, XX available

[Screenshot: df -h output]
**Disk:** 20GB total, XX used

[Screenshot: lsb_release -a output]
**OS:** Ubuntu 22.04.3 LTS

## Challenges & Solutions

**Challenge 1:** VMs couldn't communicate initially
**Solution:** Enabled host-only adapter on both VMs

**Challenge 2:** Server installation didn't show SSH option
**Solution:** Realized I needed to press Spacebar to select OpenSSH server

**Challenge 3:** IP addresses weren't showing
**Solution:** Rebooted VMs and network services

## What I Learned This Week
1. Virtualization allows running multiple OS on one machine
2. Headless servers have no GUI, reducing resource usage
3. Host-only networking isolates VMs for security
4. Ubuntu Server is specifically designed for remote administration
5. SSH is essential for managing headless systems

---

**Next Week:** Planning security measures and testing methodology
