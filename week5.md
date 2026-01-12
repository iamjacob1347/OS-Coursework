# **Week 5: Advanced Security and Monitoring Infrastructure**

## **1.  Implement Access Control with AppArmor**

I set up AppArmor which is like a security guard for applications on my server. It controls what programs can do by putting them in "profiles" - some can only access certain files or run specific commands. I installed it, checked it was running with 37 security profiles active, and tested it by switching the SSH profile between learning mode and enforcement mode to see how it works.

## **2. Firewall Configuration**

I made sure my server gets security patches automatically so hackers can't exploit old bugs. Using the "unattended-upgrades" package, I set it up to check for and install security updates daily without me having to do it manually. I tested it with a dry-run to see what updates would be installed and checked the logs to confirm it's working properly.

## **3. Configure fail2ban for Intrusion Detection**

I installed fail2ban to catch hackers trying to brute force their way into my server. It watches the login logs and if someone fails too many times (I set it to 3 attempts), it automatically blocks their IP address for an hour. I tested it by intentionally failing SSH logins to see it work, and checked the status to see banned IPs.

## **4. Create Security Baseline Verification Script**

I wrote a script called security-baseline.sh that checks ALL my security settings automatically. It runs through everything from Weeks 4 and 5 - SSH, firewall, users, AppArmor, updates, and fail2ban - and gives me a clear ✓ or ✗ for each check. I can run it anytime from my workstation to make sure nothing got accidentally changed or broken.

## **5. Create Remote Monitoring Script**

I created monitor-server.sh that lives on my workstation and checks the server's health remotely. It connects via SSH and grabs all the important metrics - CPU usage, memory, disk space, network stats, and service status - then saves everything to organized log files. Now I can monitor my server with one command instead of logging in and running a bunch of separate checks each time.
