# Week 1: System Planning and Setup

## System Architecture Diagram

<img width="261" height="521" alt="Week1SystemArchDiagram drawio" src="https://github.com/user-attachments/assets/634b857b-c014-43a9-9aac-f55095db634b" />


**Explanation:**
- **Host Machine:** Windows computer running VirtualBox
- **Workstation VM:** Ubuntu Desktop with GUI for administration
- **Server VM:** Ubuntu Server (headless) accessed via SSH
- **Network:** Host-only adapter for secure internal communication

## Distribution Selection Justification

### Why Ubuntu Server 22.04 LTS?
- **Beginner-friendly:** Extensive documentation and community support
- **Long-Term Support (LTS):** Security updates until 2027
- **Industry Standard:** Widely used in cloud and enterprise environments
- **Headless by Default:** Perfect for server operations without GUI overhead

### Alternatives Considered:
- **CentOS Stream:** More enterprise-focused but less beginner-friendly
- **Debian:** Extremely stable but slower update cycle
- **Fedora Server:** Cutting-edge features but shorter support lifecycle

## Workstation Configuration Decision

**Chosen Option:** Ubuntu Desktop VM

**Reasons:**
1. **Graphical Interface:** Easier to manage files, take screenshots, and use tools
2. **Isolation:** Keeps my host machine clean and separates coursework environment
3. **Learning Progression:** Simulates real-world remote administration from a separate system
4. **Consistency:** Both VMs use Ubuntu, reducing compatibility issues

## 5. System Specifications

### Tested the following commands:
- **System Info** uname -a
- **Memory Info:** free -h
- **Disk Space:** df -h
- **Network Info:** ip addr
- **OS Version:** lsb_release -a

<img width="643" height="481" alt="Screenshot 2026-01-12 at 02 55 10" src="https://github.com/user-attachments/assets/b23ef120-d993-4c2d-b8bc-e63d3a57195f" />

## Challenges & Solutions

**Challenge 1:** VMs couldn't communicate initially
- **Solution:** Enabled host-only adapter on both VMs

**Challenge 2:** Server installation didn't show SSH option
- **Solution:** Realized I needed to press Spacebar to select OpenSSH server

**Challenge 3:** IP addresses weren't showing
- **Solution:** Rebooted VMs and network services

