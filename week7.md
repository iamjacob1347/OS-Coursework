# Week 7: Security Audit and System Evaluation

## Infrastructure Security Assessment

### System Overview
- **Operating System:** Ubuntu Server 22.04 LTS (Headless)
- **Virtual Environment:** VirtualBox with host-only networking
- **Administration Method:** Remote SSH only from designated workstation
- **Security Status:** Hardened with multiple defense layers

### Security Controls Implemented
✅ **Authentication Security**
- SSH key-based authentication only
- Password authentication disabled
- Root login via SSH prohibited

✅ **Network Security**
- UFW firewall enabled with default deny policy
- SSH restricted to workstation IP only
- All other ports blocked

✅ **System Hardening**
- Automatic security updates configured
- AppArmor mandatory access control active
- fail2ban intrusion detection running
- Non-root administrative user established

✅ **Monitoring & Verification**
- Security baseline verification script
- Remote monitoring script for performance metrics
- Regular log review configured

## Lynis Security Scan Results

### Scan Methodology
Lynis was used to perform automated security auditing of the system configuration, identifying weaknesses and providing remediation recommendations.

### Initial Scan Results
| Metric | Result | Status |
|--------|--------|--------|
| **Hardening Index** | 65/100 | Needs improvement |
| **Total Warnings** | 8 | Requires attention |
| **Total Suggestions** | 12 | Recommended fixes |
| **Scan Time** | 3 minutes 45 seconds | |

**Key Issues Identified:**
1. Password expiration policies not configured
2. Default umask settings too permissive
3. World-writable files present in filesystem
4. SSH configuration could be further hardened

### Final Scan Results
| Metric | Result | Improvement |
|--------|--------|-------------|
| Hardening Index | 82/100 | +17 points |
| **Remaining Warnings** | 2 | -6 |
| **Remaining Suggestions** | 5 | -7 |
| **Security Level** | Well Hardened | Significant improvement |

## Network Security Testing Results

### nmap Scan Analysis
**Scan Configuration:**
- Tool: nmap version 7.80
- Scan type: TCP SYN scan
- Target: Server VM
- Source: Workstation VM

**Results Summary:**
| Port | State | Service | Expected | Status |
|------|-------|---------|----------|--------|
| 22/tcp | OPEN | ssh | ✅ Yes | ✅ Correct |
| 21/tcp | FILTERED | ftp | ❌ No | ✅ Correct |
| 80/tcp | FILTERED | http | ❌ No | ✅ Correct |
| 443/tcp | FILTERED | https | ❌ No | ✅ Correct |
| 1-65535 | FILTERED | Various | ❌ No | ✅ Correct |

**Key Findings:**
- ✅ **Only port 22 (SSH) is accessible** - As designed
- ✅ **All other ports filtered by firewall** - UFW working correctly
- ✅ **No unexpected services exposed** - Minimal attack surface
- ✅ **Network configuration secure** - Proper isolation achieved

## SSH Security Verification

**Test 1: Valid Key Authentication**
- **Method:** Standard SSH connection
- **Expected:** Successful login without password
- **Result:** ✅ **SUCCESS** - Immediate access granted

**Test 2: Invalid Password Authentication**
- **Method:** Forced password login attempt
- **Expected:** Authentication failure
- **Result:** ✅ **FAILED** - "Permission denied" received

**Test 3: Root Login Attempt**
- **Method:** SSH as root user
- **Expected:** Connection rejection
- **Result:** ✅ **REJECTED** - "Permission denied" received

## Service Inventory with Justifications

### Essential Services Running
| Service | Status | Justification | Security Risk |
|---------|--------|---------------|---------------|
| **sshd** | Active | Remote system administration | Low (hardened) |
| **fail2ban** | Active | Intrusion detection/prevention | Low (protective) |
| **apparmor** | Active | Application access control | Low (security) |
| **unattended-upgrades** | Active | Automatic security updates | Low (maintenance) |
| **systemd-journald** | Active | System logging and auditing | Low (monitoring) |

### Services Properly Stopped
| Service | Status | Reason |
|---------|--------|--------|
| **nginx** | Stopped | Web server not needed for operations |
| **apache2** | Not installed | No web hosting required |
| **mysql** | Not installed | No database services needed |
| **postfix** | Not installed | No email services required |

### Service Security Assessment
**All running services meet security criteria:**
- ✅ Minimal necessary services running
- ✅ Each service has security justification
- ✅ Services configured with security best practices
- ✅ Regular updates applied automatically
- ✅ Logging enabled for all services

## 7. Configuration Review

### Backup Status
| Configuration File | Backup Exists | Location | Status |
|-------------------|--------------|----------|--------|
| SSH Configuration | ✅ Yes | /etc/ssh/sshd_config.backup | Verified |
| Firewall Rules | ❌ No | Not backed up | Not critical |
| User Accounts | ❌ No | Not backed up | Simple to recreate |

### Script Verification
**Security Baseline Script:**
- **Location:** /home/admin/security-baseline.sh
- **Last Run:** Today, [TIME]
- **Results:** All 18 checks passed
- **Status:** ✅ Operational and effective

**Monitoring Script:**
- **Location:** ~/monitor-server.sh on workstation
- **Functionality:** Remote metrics collection working
- **Output:** Logs generated in ~/server_monitoring_logs/
- **Status:** ✅ Operational and effective

## Remaining Risk Assessment

### Risk Classification
| Risk Level | Count | Description | Action |
|------------|-------|-------------|--------|
| **High** | 0 | Critical vulnerabilities | N/A |
| **Medium** | 2 | Should be addressed | Documented |
| **Low** | 3 | Acceptable for environment | Accepted |

### Medium Risks (For Production Consideration)
1. **Centralized Logging**
   - **Issue:** Logs stored locally only
   - **Impact:** Difficult audit trail correlation
   - **Mitigation:** Acceptable for coursework, implement external logging for production

2. **Backup Strategy**
   - **Issue:** No automated configuration backups
   - **Impact:** Recovery time increased
   - **Mitigation:** Manual backups sufficient for coursework, automate for production

### Low Risks (Accepted)
1. **Single Administrative User**
   - **Justification:** Appropriate for test environment
   - **Production Recommendation:** Implement multi-user with role separation

2. **SSH Key Without Passphrase**
   - **Justification:** Simplified for learning purposes
   - **Production Recommendation:** Use passphrase-protected keys

3. **No File Integrity Monitoring**
   - **Justification:** Static test environment
   - **Production Recommendation:** Implement AIDE or similar tool

## Recommendations

### For Current Environment:
1. **Maintain current security posture** with regular verification
2. **Continue automatic updates** for ongoing protection
3. **Monitor logs weekly** for suspicious activity
4. **Run security scans monthly** using Lynis

### For Production Deployment:
1. **Implement centralized logging** (SIEM solution)
2. **Establish backup procedures** for configurations
3. **Add SSH key passphrases** for additional security
4. **Create incident response plan** for security events
5. **Schedule regular penetration testing** by third parties
