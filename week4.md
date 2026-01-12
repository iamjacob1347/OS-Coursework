# **Week 4: Initial System Configuration & Security Implementation**

## **1. SSH Key-Based Authentication Configuration**

First thing I did was generate SSH keys on my workstation to replace password login. I used ssh-keygen to create a 4096-bit RSA key pair, then copied the public key to the server with ssh-copy-id. This way I can login without typing a password every time, which is way more secure than using regular passwords.

Then I hardened the SSH configuration by disabling password authentication completely. I edited the /etc/ssh/sshd_config file to change PasswordAuthentication from "yes" to "no" and also disabled root login. After saving the changes, I restarted the SSH service with sudo systemctl restart ssh to make everything take effect.

## **2. Firewall Configuration**

I set up the firewall to lock down my server and only allow my workstation to connect. First I checked the status with sudo ufw status and saw it was inactive, so I enabled it with sudo ufw enable. I configured it to deny all incoming connections by default, then added a specific rule to allow SSH only from my workstation's IP address.

To make sure everything worked, I tested the firewall by running sudo ufw status verbose to see all the rules. I also used nmap -p 22 [server IP] from my workstation to verify that port 22 (SSH) was the only port open. The firewall is now only letting my workstation through, blocking everything else.

## **3. User Privilege Management**

I checked what users exist on the system to make sure only necessary accounts are there. Using cat /etc/passwd | grep -E "(admin|root)" I could see both the root user and my admin account. I verified my admin user has the right permissions by running id admin and sudo -l -U admin.

Turns out my admin user is properly set up with sudo privileges, which means I can run administrative commands when needed but I'm not logged in as root all the time. This is good security practice - using a regular account most of the time and only elevating privileges when necessary.

## **4. SSH Access Evidence**

Now came the fun part - testing if my security changes actually work! First I tried logging in normally with ssh admin@[server IP] and it worked perfectly without asking for a password. That means the key authentication is working. Then I tested to make sure password login was really disabled.

I tried connecting with ssh -o PreferredAuthentications=password -o PubkeyAuthentication=no which forces password authentication, and it failed like it should. Even when I typed my password, it said "Permission denied" - exactly what we want! This proves password login is properly disabled.

## **5. Configuration Files Comparison**

Before changing anything, I made a backup of the original SSH configuration file. I used sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.backup to save a copy just in case something went wrong. Then I could compare the before and after versions using sudo diff.

The comparison showed exactly what changed: two lines were modified. The #PasswordAuthentication yes became PasswordAuthentication no and #PermitRootLogin prohibit-password became PermitRootLogin no. This clear before/after comparison proves exactly what security changes I made.

## **6. Firewall Documentation**

I documented the complete firewall setup to show exactly what rules are in place. Running sudo ufw status numbered displays all the rules with numbers, and mine shows just one rule allowing my workstation IP to connect on port 22. Everything else is blocked by the default deny policy.

I also checked what application profiles are available with sudo ufw app list, and it showed OpenSSH as the only available profile. This confirms that the firewall is properly configured and only allowing SSH connections from my specific workstation.

## **7. Remote Administration Evidence**

To prove I can actually manage everything remotely, I ran several commands from my workstation. First I tested basic commands with ssh admin@[IP] "whoami && hostname && date" which worked perfectly. Then I checked system resources by running ssh admin@[IP] "free -h && df -h" to see memory and disk usage.

Finally, I verified all my security settings from my workstation by running ssh admin@[IP] "sudo grep -i 'PasswordAuthentication\|PermitRootLogin' /etc/ssh/sshd_config" and ssh admin@[IP] "sudo ufw status". Both commands confirmed that password authentication is disabled and the firewall is active - all done remotely without touching the server directly.

## **Implementation Process**

### **Requirements**
- No direct console access to Server VM
- All commands executed through SSH sessions
- Configuration files edited using nano over SSH
- Service management performed remotely

### **Step-by-Step Approach**
- SSH Key Setup: Generated keys on Workstation, transferred to Server  
- SSH Hardening: Disabled password authentication and root login  
- Firewall Configuration: Enabled UFW and restricted SSH access  
- User Verification: Confirmed admin user privileges  
- Testing: Verified all security controls were operational  

---

## **Challenges and Solutions**

### **Challenge 1: SSH Connection During Configuration**
**Problem:** Risk of locking out SSH access  
**Solution:**
- Kept existing SSH session open
- Tested a new SSH session before closing the original
- Created configuration backups before changes

### **Challenge 2: UFW Blocking Current Session**
**Problem:** Firewall rules could block the active SSH connection  
**Solution:**
- Added Workstation IP rule before enabling UFW
- Verified rules prior to firewall activation
- Tested connectivity after each change

### **Challenge 3: Service Restart Timing**
**Problem:** SSH service restart could interrupt access  
**Solution:**
- Completed all configuration changes first
- Performed a single service restart
- Verified SSH service availability afterward
