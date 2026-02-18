# Task 14: Linux Server Hardening & Secure Configuration

## Overview

This task focuses on implementing Linux server hardening techniques to secure a system against common attacks. The objective was to reduce the attack surface, enforce least privilege, secure remote access, configure firewall rules, disable unnecessary services, and validate system security posture using an automated audit tool (Lynis).

This exercise simulates real-world Linux server security configuration aligned with industry best practices and CIS benchmarks.

---

## Objective

- Review default Linux users, services, and open ports
- Enforce least privilege principle
- Disable root login and harden SSH
- Configure firewall rules
- Remove unnecessary services
- Secure file permissions
- Apply system updates and automatic patching
- Perform security audit using Lynis

---

## Environment

- Host OS: Windows 11
- Virtualization: Oracle VirtualBox
- Guest OS: Kali Linux
- Firewall: UFW (Uncomplicated Firewall)
- Audit Tool: Lynis

---

## Linux Hardening Checklist

### 1. User & Access Control

✔ Reviewed user accounts:

```bash
cat /etc/passwd
```

✔ Checked sudo group membership:

```bash
getent group sudo
```

✔ Applied Least Privilege Principle  
✔ Removed unnecessary users (if any)

---

### 2. Root Account Security

✔ Locked root account:

```bash
sudo passwd -l root
```

✔ Disabled SSH root login in:

```
/etc/ssh/sshd_config
```

Set:

```
PermitRootLogin no
```

Security Impact:
Prevents direct root-based attacks and brute-force attempts.

---

### 3. SSH Hardening

Edited:

```
/etc/ssh/sshd_config
```

Configured:

```
PermitRootLogin no
PasswordAuthentication no
```

Restarted SSH:

```bash
sudo systemctl restart ssh
```

Security Impact:
Prevents password-based brute force attacks.

---

### 4. Firewall Configuration (UFW)

✔ Enabled firewall:

```bash
sudo ufw enable
```

✔ Allowed only required service (SSH):

```bash
sudo ufw allow ssh
```

✔ Verified firewall status:

```bash
sudo ufw status verbose
```

Security Impact:
Restricts unauthorized inbound network traffic.

---

### 5. Open Port Review

Checked open ports:

```bash
sudo ss -tuln
```

Identified and validated necessary exposed services only.

Security Impact:
Reduces network attack surface.

---

### 6. Service Hardening

Listed running services:

```bash
systemctl list-units --type=service --state=running
```

Stopped unnecessary services:

```bash
sudo systemctl stop <service>
sudo systemctl disable <service>
```

Security Impact:
Prevents exploitation of unused or vulnerable services.

---

### 7. System Updates & Patch Management

Updated system:

```bash
sudo apt update
sudo apt full-upgrade -y
```

Enabled automatic security updates:

```bash
sudo apt install unattended-upgrades -y
sudo dpkg-reconfigure unattended-upgrades
```

Security Impact:
Mitigates vulnerabilities by applying latest patches.

---

### 8. File Permission Security

Verified sensitive files:

```bash
ls -l /etc/passwd
ls -l /etc/shadow
```

Ensured correct permissions:

```
/etc/passwd → 644
/etc/shadow → 640
```

Security Impact:
Prevents unauthorized access to credential data.

---

### 9. Log Monitoring

Reviewed authentication logs:

```bash
sudo cat /var/log/auth.log | tail
```

Checked login history:

```bash
last
```

Security Impact:
Improves visibility into authentication events and suspicious activity.

---

## Security Audit Using Lynis

Lynis is an open-source Linux security auditing tool used for compliance testing and vulnerability detection.

Installed and executed:

```bash
sudo apt install lynis -y
sudo lynis audit system
```

### Audit Areas Covered:

- Kernel security configuration
- Authentication mechanisms
- Password policies
- Firewall settings
- File permissions
- Installed packages
- Patch status
- Logging configuration
- Compliance alignment (CIS benchmarks)

### Audit Outcome:

- Identified potential misconfigurations
- Provided security warnings and suggestions
- Validated implemented hardening measures
- Improved overall system security score

Security Impact:
Ensures structured validation of hardening steps.

---

## Risk Reduction Summary

| Risk | Mitigation Implemented |
|------|------------------------|
| Brute-force attacks | Disabled root login & hardened SSH |
| Unauthorized privilege escalation | Enforced least privilege |
| Open port exploitation | Firewall configured |
| Service-based attacks | Disabled unnecessary services |
| Unpatched vulnerabilities | System fully updated |
| Credential exposure | Secured file permissions |

---

## Key Security Principles Applied

- Least Privilege
- Defense in Depth
- Attack Surface Reduction
- Secure Configuration Management
- Continuous Monitoring
- Patch Management

---

## Conclusion

The Linux server was successfully hardened by implementing structured security controls and validating configurations using the Lynis security audit tool. The attack surface was minimized, unnecessary services were removed, root login was disabled, and firewall protections were applied.

This task demonstrates practical skills in Linux system security, server hardening, and security auditing — essential competencies for SOC Analysts, System Administrators, and Security Engineers.

---

## Author

Mohammed Nihal  
Cyber Security Intern  
Kali Linux | Linux Hardening | SOC Preparation
