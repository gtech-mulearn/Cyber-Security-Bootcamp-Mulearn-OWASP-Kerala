# Malware Incident Research 

**Prepared:** 29 Sep 2025  
**Author:**  Richu Joseph

---

## 1) Kido International (Radiant) — Nursery chain data theft / extortion  
**Date reported:** 26–27 Sep 2025  
**Summary:** Criminals calling themselves *Radiant* claimed to have stolen personal data (names, photos, dates of birth, addresses, safeguarding reports) for thousands of children at Kido International nurseries in Greater London and posted sample profiles to a dark‑web leak site as proof. The group demanded payment and threatened further leaks. 

**Attack method (what happened):**
- Adversaries gained access to Kido's systems (Kido says the incident involved two third party systems used to process certain data) and exfiltrated sensitive files. Attackers used a standard data exfiltration + extortion (double extortion) approach: steal sensitive data and threaten public disclosure to coerce payment. 

**Mitigation / resolution steps taken or recommended:**
- Kido engaged external IT forensic specialists, notified affected families and regulators (ICO, Ofsted) and is cooperating with the Metropolitan Police. Authorities and security experts advised against paying ransoms and encouraged forensic containment, notification, and support for victims. Where third party services are involved, immediate vendor containment, credential rotation, and supply‑chain impact assessment were recommended. 

---

## 2) npm ecosystem — Qix maintainer compromise (mass supply‑chain malware)  
**Date reported:** 8–23 Sep 2025 (disclosed in early Sep 2025)  
**Summary:** An npm maintainer account (Qix) was phished, allowing attackers to publish malicious versions of widely used packages (including `chalk`, `debug` and others). The malicious updates included code that attempted to steal crypto‑wallet information / intercept cryptocurrency transactions and/or exfiltrate credentials. The event is one of the largest npm supply‑chain compromises in recent history and prompted widespread advisories.

**Attack method (what happened):**
- Initial access via a convincing phishing message that led to an attacker-controlled 2FA reset page; the attacker captured credentials/2FA and took over the maintainer account.  
- The attacker released malicious package versions that contained obfuscated JavaScript: browser transaction interception (replace destination wallet addresses), credential/2FA stealers, or scripts that attempted to harvest secrets from developer environments. Because these libraries are transitive dependencies, the blast radius was huge (billions of weekly downloads). 

**Mitigation / resolution steps taken or recommended:**
- npm and security teams rapidly revoked malicious releases and removed the compromised packages from the registry. CISA and other vendors published detection/mitigation guidance: rotate developer credentials, audit lockfiles (`package-lock.json`, `yarn.lock`), pin package versions to known-good releases, scan repositories and CI artifacts for infected packages, and restore from clean caches/artifacts where possible. Organizations were urged to review any client-side code that interacts with wallets.

---

## 3) Toppan Next Tech (TNT) — Ransomware affecting a printing/data vendor (DBS, Bank of China Singapore impact)  
**Date reported:** 1–7 Apr 2025 (disclosure April 2025)  
**Summary:** TOPPAN Next Tech (TNT), a third‑party printing and secure communications vendor in Singapore, suffered a ransomware attack that encrypted servers and led to potential exfiltration of customer statements/letters for clients including DBS Group and Bank of China (Singapore). Approximately 8,200 DBS customer statements and ~3,000 BoC statements were reported as potentially exposed. Core bank systems were not compromised. 

**Attack method (what happened):**
- Threat actor gained access to TNT systems (attack reported on or around 1 Apr 2025), deployed ransomware that encrypted servers and — according to preliminary investigations — extracted data (customer statements, names, addresses, some loan/account numbers). Because TNT handled printed correspondence for banks, the incident is a classic third‑party/vendor ransomware/data‑exfiltration case. 

**Mitigation / resolution steps taken or recommended:**
- TNT notified clients and authorities; DBS and BoC engaged regulators (MAS and CSA) and began customer outreach. TNT and authorities worked with, incident response experts to contain and investigate (disconnect infected systems, forensic analysis, notify Personal Data Protection Commission). Banks emphasized that deposit/transaction systems remained secure and rotated any exposed credentials where necessary. Recommended mitigations included tightening vendor risk, management (restrict vendor access, implement strong segmentation, require vendor cyber incident plans), accelerated customer notifications, and engagement with regulatory authorities for follow‑up. 

---

# Short conclusions and lessons learned (high level)
1. **Supply‑chain risk is a primary vector.** Third‑party vendors and open‑source maintainers extend attackers reach secure vendor practices and developer credential hygiene are critical. 
2. **Phishing + 2FA bypass remains effective.** Many large compromises start with targeted phishing that defeats multi‑factor setups (e.g., 2FA resets). Emphasize phishing-resistant MFA (hardware keys), credential rotation, and least privilege. 
3. **Rapid detection and coordinated response limit damage.** Quick takedown of malicious packages, vendor containment, regulator engagement, and public notification reduce blast radius and downstream harm.

---

# Sources
- Reuters - "London nurseries hit by hackers, data on 8,000 children stolen" (26 Sep 2025). https://www.reuters.com/world/uk/london-nurseries-hit-by-hackers-data-8000-children-stolen-2025-09-26/   
- The Guardian — "Kido nursery hackers threaten to publish more children's profiles" (26–27 Sep 2025). https://www.theguardian.com/technology/2025/sep/26/kido-nursery-hackers-radiant-threaten-publish-children-profiles   
- CISA — "Widespread supply chain compromise impacting npm ecosystem" (23 Sep 2025). https://www.cisa.gov/news-events/alerts/2025/09/23/widespread-supply-chain-compromise-impacting-npm-ecosystem   
- Palo Alto Networks Unit 42 — analysis of the npm supply‑chain incident. https://www.paloaltonetworks.com/blog/cloud-security/npm-supply-chain-attack/  
- NVD / CVE entry describing malicious update to `debug` package (Sept 2025). https://nvd.nist.gov/vuln/detail/CVE-2025-59144   
- Reuters — "Singapore's DBS, BoC customer data at risk after ransomware attack on vendor" (7 Apr 2025). https://www.reuters.com/technology/cybersecurity/dbs-vendor-ransomware-attack-potentially-exposes-8200-customer-statements-2025-04-07/   
- TOPPAN Holdings notice (8 Apr 2025) regarding unauthorized access at TNT. https://www.holdings.toppan.com/en/info/toppan_info20250408.pdf 

---
