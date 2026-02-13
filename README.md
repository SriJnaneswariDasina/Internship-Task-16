# Internship-Task-16

🔐 Task 16 – Incident Response & Security Breach Simulation (Linux)
📌 Overview

This project demonstrates a practical implementation of the Incident Response lifecycle by simulating and handling a security breach scenario on Kali Linux.

The simulated attack involved multiple failed SSH login attempts (Brute Force Attack). The incident was detected through log analysis, contained using firewall rules, eradicated through system hardening, and documented with a complete incident report.

🎯 Objective

Simulate a security incident (Repeated SSH failed login attempts)

Analyze authentication logs

Identify suspicious activity and attacker IP

Classify the incident

Contain the threat

Eradicate root cause

Restore and secure the system

Document incident timeline and actions taken

🖥️ Environment Used

OS: Kali Linux

Service: OpenSSH

Logging System: systemd journal (journalctl)

Firewall: UFW (Uncomplicated Firewall)

Optional Tool: Fail2Ban

Note: Kali Linux stores authentication logs in systemd journal instead of /var/log/auth.log.

🚨 Incident Simulation

Multiple failed SSH login attempts were generated using:

ssh fakeuser@localhost


Incorrect passwords were entered multiple times to simulate a brute-force attack.

🔍 Log Analysis

Authentication logs were analyzed using:

sudo journalctl -u ssh


Filtering failed login attempts:

sudo journalctl -u ssh | grep "Failed password"


Extracting attacker IP:

sudo journalctl -u ssh | grep "Failed password" | awk '{for(i=1;i<=NF;i++) if($i=="from") print $(i+1)}' | sort | uniq -c

🛑 Containment

Firewall enabled:

sudo ufw enable


Blocked attacker IP:

sudo ufw deny from <attacker_ip>


Verified firewall status:

sudo ufw status

🧹 Eradication & Hardening
1️⃣ System Update
sudo apt update && sudo apt upgrade -y

2️⃣ Disable Root Login

Edited SSH configuration:

sudo nano /etc/ssh/sshd_config


Changed:

PermitRootLogin no


Restarted SSH:

sudo systemctl restart ssh

3️⃣ Installed Fail2Ban (Brute Force Protection)
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban

🔄 Recovery

Monitored logs in real-time:

sudo journalctl -u ssh -f


No further suspicious activity observed.

📊 Incident Classification

Attack Type: SSH Brute Force Attack

Severity Level: High

Impact: Unauthorized access attempt

Risk: Potential credential compromise

📝 Incident Response Phases Followed

Preparation

Identification

Containment

Eradication

Recovery

Lessons Learned

🎓 Learning Outcomes

Practical understanding of Incident Response lifecycle

Log analysis using journalctl

Firewall configuration and containment

Root cause analysis

System hardening techniques

Security monitoring

🔐 Preventive Recommendations

Enable SSH key-based authentication

Disable password authentication

Change default SSH port

Use strong password policies

Install Fail2Ban

Regularly monitor authentication logs

📌 Final Outcome

The simulated SSH brute-force attack was successfully detected, analyzed, contained, and mitigated using Linux security tools. This task demonstrates hands-on experience in incident handling and system hardening.
