# Task 5 - Recent Malware Incidents

## 1. **Lumma Infostealer Takedown**

**Date / Timeframe:** March–May 2025

**Attack method:**

- The Lumma infostealer malware had infected over 394,000 Windows computers.
- It operated via phishing campaigns: attackers would trick users into downloading malware (often via email links or malicious attachments) and once installed, Lumma would exfiltrate sensitive information (passwords, financial data, crypto wallet info, etc.).
- It used a command‑and‑control (C2) infrastructure to receive updates and exfiltrate data.

**Impact:**

- Large scale infection, widespread use in criminal campaigns.
- Used by multiple threat actors, integrated into other attacks (e.g. phishing) to amplify damage.

**Mitigation / Resolution:**

- An international coalition of law enforcement agencies and tech companies disrupted the malware’s infrastructure: over 2,300 domains used for command‑and‑control were seized.
- This significantly hampered its ability to receive commands, distribute payloads, and exfiltrate data.
- Since then, its prevalence has been reduced, though experts caution that infostealers in general remain a large, ongoing threat.

---

## 2. **WinRAR Zero‑Day Vulnerability (CVE‑2025‑8088) Exploited by Russian‑linked Group RomCom**

**Date / Timeframe:** Discovered in 2025; vulnerability fixed in WinRAR version 7.13.

**Attack method:**

- There was a zero‑day vulnerability (CVE‑2025‑8088) in WinRAR, involving directory traversal, which allowed attackers to plant malicious files into Windows autorun directories. This makes it possible for malware to execute automatically on startup.
- Exploitation was done via spear‑phishing emails which carried RAR archives embedding backdoors. The victim opens the RAR, and the backdoor gets installed.

**Impact:**

- Because the autorun directory exploit allows persistent execution, even after a reboot, this gives the attacker strong footholds.
- Targets included organizations (particularly linked to Ukraine, and Western organizations supporting Ukraine) per reports.

**Mitigation / Resolution:**

- WinRAR issued an update (version 7.13) which patched the vulnerability.
- Because WinRAR lacks an automatic update mechanism, users had to manually download and install the fixed version.
- Advisories were published by security researchers; users and organizations were urged to update immediately.

---

## 3. **Oracle E‑Business Suite (EBS) Remote Code Execution Vulnerability Exploited by Cl0p Ransomware Group**

**Date / Timeframe:** Vulnerability noted in August 2025; emergency patch issued recently (October 2025).

**Attack method:**

- Oracle’s E‑Business Suite (EBS) had a critical vulnerability, tracked as CVE‑2025‑61882, which allowed *unauthenticated remote code execution*. This means an attacker could execute arbitrary code on EBS systems accessible from the internet without valid credentials.
- The Cl0p ransomware gang was exploiting this vulnerability to extract sensitive data from affected systems, and then demand ransom.
- Since exploit code was publicly available, risk increased for unpatched systems.

**Impact:**

- Organizations running Oracle EBS systems were at serious risk, especially if those systems were internet‑facing. Data breach vs. ransomware threat.
- Because the attack is unauthenticated, even systems without user accounts exposed could be compromised.

**Mitigation / Resolution:**

- Oracle released an emergency security patch to fix CVE‑2025‑61882.
- Security advisories from agencies (FBI, UK National Cyber Security Centre etc.) urged organizations to patch immediately, monitor for indicators of compromise.
- Organizations were advised to review their Oracle EBS systems, particularly those exposed to the internet, check whether data exfiltration had already occurred, harden access controls, and apply the patch.

## References:

- [1] https://www.wired.com/story/lumma-stealer-takedown-disrupted?utm_source=chatgpt.com
- [2] https://www.tomshardware.com/tech-industry/cyber-security/newly-discovered-winrar-exploit-linked-to-russian-hacking-group-can-plant-backdoor-malware-zero-day-hack-requires-manual-update-to-fix?utm_source=chatgpt.com
- [3] https://www.itpro.com/security/oracle-patches-ebs-amid-extortion-attacks?utm_source=chatgpt.com


