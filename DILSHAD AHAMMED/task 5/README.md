# Task 5 — Recent Malware Incidents: Methods & Mitigations

## 1) Change Healthcare (UnitedHealth Group) — ALPHV/BlackCat Ransomware

**When:** February 2024  
**What happened:** The ALPHV/BlackCat ransomware group infiltrated Change Healthcare, disrupting pharmacy claims and billing across the U.S. healthcare system. UnitedHealth later confirmed a **\$22M ransom payment**. Reports and testimony indicate attackers used **stolen credentials to access a Citrix service that lacked MFA**, spent days inside the network, exfiltrated data, then deployed ransomware. ([The Wall Street Journal][1], [IBM][2])

**Attack method (kill chain):**

* Initial access via **valid credentials** to exposed **Citrix** access without MFA.
* **Internal reconnaissance + data exfiltration** over \~9 days.
* **Ransomware deployment** (ALPHV/BlackCat) to disrupt operations. ([The Wall Street Journal][1])

**Mitigation / resolution:**

* System restoration in phases; emergency financial support to providers.
* Post-incident actions: enforcing **MFA on remote access**, hardening identity controls, incident response and data-breach notifications. UHG publicly acknowledged the **\$22M** payment and ongoing remediation. ([IBM][2], [Hyperproof][3])

---

## 2) CDK Global — BlackSuit Ransomware (Auto Dealership Outages)

**When:** June 2024
**What happened:** **CDK Global**, IT backbone for >15,000 North American car dealerships, suffered a ransomware attack attributed to **BlackSuit**, forcing multi-day shutdowns of dealer systems (DMS, CRM, etc.). ([BlackFog][4], [TechTarget][5], [corvusinsurance.com][6])

**Attack method (kill chain):**

* Initial intrusion details not fully public; attributed to **BlackSuit** (linked by multiple researchers to prior Royal/Conti lineage).
* **Ransomware execution** on CDK’s core infrastructure led to broad service outages. ([BlackFog][4], [corvusinsurance.com][6])

**Mitigation / resolution:**

* **Network shutdown/segmentation**, staged restoration of core applications; public guidance that recovery would take **days**.
* Typical hardening steps (per incident reporting): tightened access controls, increased monitoring, and coordinated communications to dealerships. ([corvusinsurance.com][6], [TechTarget][5])

---

## 3) Polyfill.io Supply-Chain Malware (Web-wide Injection)

**When:** Disclosed June 2024 (malicious changes followed a February 2024 domain ownership change)
**What happened:** After **polyfill.io** was **sold to a new owner (Funnull)**, the CDN began serving **tampered polyfill.js** to websites that embedded it, injecting **malicious redirects and scam code** at scale (impacting 100k+ sites). Major browsers/ad platforms took countermeasures. ([Qualys][7], [The Hacker News][8], [Red Sift Blog][9])

**Attack method (kill chain):**

* **Supply-chain compromise** via ownership change of a widely used CDN domain/library.
* Sites hot-linking `cdn.polyfill.io` unknowingly **executed attacker-controlled JS** in users’ browsers (malvertising/redirects). ([The Hacker News][8])

**Mitigation / resolution:**

* Security vendors and Google **blocked/flagged** the domain; guidance to **remove polyfill.io references** and pin to **self-hosted or trusted mirrors**.
* Organizations audited their pages, implemented **Subresource Integrity (SRI)** where feasible, and migrated to vetted alternatives. ([The Hacker News][8], [Qualys][7])

---

## Key Takeaways & Defenses

* **Identity & MFA everywhere:** Both Change Healthcare and many large breaches start with valid credentials on remote access (Citrix/VPN). Enforce **MFA**, conditional access, continuous verification. ([The Wall Street Journal][1])
* **Third-party & supply-chain risk:** Don’t hot-link critical JS; **self-host** or use trusted CDNs with **SRI** + CSP. Continuously inventory external dependencies. ([Qualys][7], [The Hacker News][8])
* **Ransomware resilience:** Network segmentation, immutable/offline backups, EDR with script-abuse detection, rapid isolation, and tested restore procedures (CDK case). ([TechTarget][5])
* **Transparency & recovery:** Prompt disclosure, staged restoration, and regulatory reporting were central to resolution across cases (UHG/CDK). ([IBM][2], [corvusinsurance.com][6])

---

**Prepared By:** *DILSHAD AHAMMED N*

**Date:** Aug 14, 2025

[1]: https://www.wsj.com/articles/change-healthcare-hack-what-you-need-to-know-45efc28c?utm_source=chatgpt.com "UnitedHealth Hack: What You Need to Know"
[2]: https://www.ibm.com/think/news/change-healthcare-22-million-ransomware-payment?utm_source=chatgpt.com "Change Healthcare discloses USD 22M ransomware payment - IBM"
[3]: https://hyperproof.io/resource/understanding-the-change-healthcare-breach/?utm_source=chatgpt.com "Understanding the Change Healthcare Breach - Hyperproof"
[4]: https://www.blackfog.com/cdk-global-ransomware-attack/?utm_source=chatgpt.com "CDK Global Ransomware: What Happened and How It Impacted ..."
[5]: https://www.techtarget.com/whatis/feature/The-CDK-Global-outage-Explaining-how-it-happened?utm_source=chatgpt.com "The CDK Global outage: Explaining how it happened - TechTarget"
[6]: https://www.corvusinsurance.com/blog/cdk-global-incident-june-2024?utm_source=chatgpt.com "The Impact of the CDK Global Incident | June 2024 - Corvus Insurance"
[7]: https://blog.qualys.com/vulnerabilities-threat-research/2024/06/28/polyfill-io-supply-chain-attack?utm_source=chatgpt.com "Polyfill.io Supply Chain Attack: What You Need to Know - Qualys Blog"
[8]: https://thehackernews.com/2024/06/over-110000-websites-affected-by.html?utm_source=chatgpt.com "Over 110,000 Websites Affected by Hijacked Polyfill Supply Chain ..."
[9]: https://blog.redsift.com/news/understanding-the-polyfill-io-domain-attack/?utm_source=chatgpt.com "Understanding the polyfill.io domain attack - Red Sift Blog"
