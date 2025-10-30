


# Vulnerability Assessment Report  
**Prepared for:** MuLearn Bootcamp  

---

## 1. Introduction

This document presents a systematic analysis of a virtual machine vulnerable to several known security flaws. The exercise involved setting up the VM in VirtualBox, identifying exposed services, investigating weaknesses, and exploiting a significant vulnerability to gain remote access. The report details each step, tools used, and insights gathered—aiming to be understandable to readers new to penetration testing.

---

## 2. Environment and Setup

The virtual machine was imported as an OVA file into VirtualBox and configured with a host-only network to limit accessibility to the attacker’s machine.

- **Attacking System:** Kali Linux  
- **Target VM:** Ubuntu-based system with known vulnerabilities  
- **Network:** Host-only adapter ensuring isolated test environment

IP addresses in use during assessment:  
- Kali: 192.168.56.102  
- Target VM: 192.168.1.9

---

## 3. Reconnaissance and Network Scanning

### 3.1 Identifying Open Ports and Services

To gather information on running services, a full TCP port scan was performed with version detection enabled. This approach helps uncover potential entry points and their software versions.

- Command executed:

  ```
  nmap -sV -p- 192.168.1.9
  ```

- Key findings included:
  - FTP server running ProFTPD 1.3.5 on port 21
  - SSH accessible on port 22
  - Web server (Apache) on port 80
  - Other services like Samba, MySQL, and Jetty also detected

![Network and port scan](Screenshot-323.jpg)

---

### 3.2 Examining Web Server and Applications

The next step involved investigating the HTTP service for website content and application structure.

- A scan using Nmap scripts revealed enabled directory listing on Apache.
- Accessing the target URL in a browser displayed:
  - Folders such as `chat/`, `drupal/`
  - Application files like `payroll_app.php`
  - The popular admin panel `phpmyadmin/`

This visibility greatly aids attackers in mapping the environment and identifying potential attack vectors.

![Web directory enumeration 1](Screenshot-318.jpg)  
![Web directory enumeration 2](Screenshot-302.jpg)

---

## 4. Identifying Exploitable Vulnerabilities

### 4.1 Researching FTP Server Flaws

The detected ProFTPD version 1.3.5 is known to have a remote code execution flaw via its `mod_copy` module.

- Using Searchsploit and Metasploit, the existence of an exploit targeting this vulnerability was confirmed.
- The exploit allows attackers to transfer arbitrary files into web directories, enabling remote shell execution.

Commands verifying exploit availability:

```
searchsploit ProFTPD 1.3.5
```

```
msf6 > search ProFTPD 1.3.5
```

![Exploit research 1](Screenshot-326.jpg)  
![Exploit research 2](Screenshot-325.jpg)

---

## 5. Exploitation and Post-Compromise Actions

### 5.1 Gaining Remote Command Execution

With Metasploit’s `proftpd_modcopy_exec` module, a reverse shell was successfully created back to the attacker’s machine.

- Essential settings included the target IP, the writable web directory path, and a Perl reverse shell payload.
- After launching the exploit, a remote shell prompt was obtained as the `www-data` user.
- Listing the web content directory confirmed access to important folders and files.

![Successful exploitation](Screenshot-329.jpg)

---

## 6. Analysis and Recommendations

The exploit underscores how unpatched software and misconfigurations can seriously jeopardize system security.

- **Urgently patch or replace vulnerable services** like ProFTPD to prevent unauthorized access.
- **Disable Apache directory listing** to avoid unintentionally revealing sensitive files.
- **Limit access to administration interfaces** (e.g., phpMyAdmin) through proper authentication and network segmentation.
- Regular vulnerability scanning and prompt remediation reduce risk of compromise.

---

## 7. Conclusion

By following methodical reconnaissance and leveraging known exploits, the assessment demonstrated the risks associated with outdated software and exposed service configurations. This exercise reinforces best practices in patch management, service restriction, and infrastructure monitoring.

---

**Screenshots Referenced:**  
- Network and port scan: Screenshot-323.jpg  
- Web directory enumeration: Screenshot-318.jpg, Screenshot-302.jpg  
- Exploit research and availability: Screenshot-326.jpg, Screenshot-325.jpg  
- Successful exploitation: Screenshot-329.jpg

---
```

