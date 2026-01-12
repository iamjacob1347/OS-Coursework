# Week 2: Security Planning and Testing Methodology

## Performance Testing Plan

### My 7-Week Progressive Testing Approach:

**Week 1 (Completed):** System Setup Testing
- Tested: Virtual machines creation and basic connectivity
- Verified: Network communication between Workstation and Server
- Tools used: `ip addr`, `ping`, VirtualBox networking

**Week 2 (Current):** Planning Phase
- Researching security concepts and testing methodologies
- No technical testing this week

**Week 3:** Application Installation Testing
- **Test:** Install various applications via SSH for future performance testing
- **Measure:** Installation success/failure, time taken, disk space used
- **Tools:** `apt install`, `time` command, `df -h` for disk monitoring
- **Example command:** `time sudo apt install stress-ng`

**Week 4:** Security Implementation Testing  
- **Test:** SSH key authentication setup and verification
- **Test:** Firewall configuration and rule enforcement
- **Measure:** Connection success rates, unauthorized access blocking
- **Tools:** `ssh-keygen`, `ssh-copy-id`, `ufw`, `nmap` for port scanning
- **Goal:** Ensure only my workstation can SSH to server

**Week 5:** Monitoring and Script Testing
- **Test:** Security baseline script functionality
- **Test:** Remote monitoring script accuracy
- **Measure:** Script execution time, monitoring data accuracy
- **Tools:** Custom bash scripts, `cron` for scheduling, manual verification
- **Goal:** Automate security checks and performance monitoring

**Week 6:** Application Performance Testing
- **Test:** How installed applications perform under different loads
- **Measure:** CPU usage, memory consumption, response times
- **Tools:** `stress-ng` for load generation, `htop` for monitoring, `time` for timing
- **Applications:** To be selected in Week 3 based on resource usage types

**Week 7:** Security Audit and Final Testing
- **Test:** Overall system security after all implementations
- **Measure:** Lynis security score, open ports, service vulnerabilities
- **Tools:** `lynis audit system`, `nmap`, manual security checklist review
- **Goal:** Achieve security score >80 and verify all security controls work

## Security Configuration Checklist

### SSH Hardening:
- Disable password authentication
- Enable key-based authentication only
- Change default SSH port (optional)
- Disable root login over SSH
- Configure idle timeout limits
- Use strong encryption algorithms

### Firewall Configuration:
- Enable UFW (Uncomplicated Firewall)
- Allow SSH only from Workstation IP (192.168.56.101)
- Deny all other incoming connections
- Configure logging for firewall events
- Test firewall rules with nmap scan

### Mandatory Access Control:
- Research and choose between SELinux or AppArmor
- Install chosen MAC system
- Configure basic policies
- Document enforcement modes
- Test with violation attempts

### Automatic Updates:
- Configure unattended-upgrades package
- Set automatic security updates only
- Configure update notifications
- Test update mechanism
- Document update schedule

### User Privilege Management:
- Create non-root administrative user
- Configure sudo privileges carefully
- Set password policies
- Implement least privilege principle
- Remove unnecessary users

### Network Security:
- Configure host-only network isolation
- Disable unnecessary network services
- Configure TCP wrappers if needed
- Implement intrusion detection (fail2ban)
- Regular network scanning from workstation

## Threat Model

### Threat 1: Brute Force SSH Attacks
**Description:** Attackers repeatedly try common passwords to gain SSH access
**Impact:** Unauthorised access, system compromise
**Mitigation Strategies:**
1. Implement key-based authentication (eliminates password guessing)
2. Configure fail2ban to block IPs after failed attempts
3. Use strong passphrase for SSH keys
4. Change default SSH port to reduce automated scans
**Implementation:** Week 4 in SSH hardening

### Threat 2: Unauthorised Service Access
**Description:** Attackers exploiting vulnerable services running on server
**Impact:** Data theft, system takeover, malware installation
**Mitigation Strategies:**
1. Implement firewall to block all unnecessary ports
2. Use mandatory access control (AppArmor/SELinux) to restrict services
3. Regular security updates to patch vulnerabilities
4. Disable all unused services and daemons
**Implementation:** Week 4 in firewall, Week 7 in service audit

### Threat 3: Privilege Escalation
**Description:** Regular user gaining root/admin privileges through exploits
**Impact:** Complete system compromise, data destruction
**Mitigation Strategies:**
1. Implement strict sudo privileges (least privilege principle)
2. Regular security updates to patch privilege escalation vulnerabilities
3. Use mandatory access control to limit damage scope
4. Regular security scanning with Lynis
**Implementation:** Week 4 in user management)

## Next Steps
- **Week 3:** Install test applications based on this performance plan
- **Week 4:** Begin implementing security checklist items
- **Week 5:** Complete advanced security implementations
- **Week 6:** Execute performance testing per this methodology
- **Week 7:** Validate security implementations against threat model
