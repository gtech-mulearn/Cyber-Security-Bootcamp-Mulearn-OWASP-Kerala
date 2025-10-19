
# Recent Malware Incidents — Summary, Attack Methods, and Mitigation


## 1) Asahi Group — Ransomware causing nationwide supply disruption (October 2025)
**What happened:** Asahi Group — one of Japan’s largest beverage companies (maker of Asahi Super Dry) — suffered a ransomware cyberattack in early October 2025 that forced the company to suspend domestic automated ordering, shipping and call-center systems and caused widespread supply disruptions and threatened shortages in stores and restaurants. 

**Attack method:** Initial public reporting describes the incident as a ransomware-driven system compromise that disrupted logistics and order-processing systems. Asahi publicly limited technical details to reduce further risk; no definitive public attribution or ransomware brand had claimed responsibility at the time of reporting. citeturn1news30turn1search20

**Mitigation & resolution steps:**
- Asahi suspended affected automated services and moved to manual processing for some orders to reduce immediate customer impact while isolating affected systems. citeturn1news28  
- The company engaged law enforcement and cyber-response investigations; they limited public technical details during the active response (a common practice to avoid tipping off attackers). 
- Public reporting indicates recovery activities were ongoing at time of coverage; organizations facing similar incidents typically restore from known-good backups, rebuild affected systems, and harden access controls and third-party connections as part of remediation (Asahi’s public statements emphasized restoration and investigation). 

---

## 2) Marks & Spencer (M&S) — Major ransomware incident (April–May 2025)
**What happened:** In April 2025 M&S detected a "highly sophisticated and targeted" cyber incident that severely disrupted online ordering, in-store systems (contactless payments / click-and-collect) and other services, costing the company hundreds of millions of pounds and disrupting operations for many weeks. M&S confirmed that some customer personal data was taken. 

**Attack method (technical summary):**
- Public reporting and subsequent company testimony indicate attackers used social‑engineering against third‑party contractors and IT help-desks to obtain credentials or to reset accounts, enabling lateral movement into M&S systems. Attackers are reported to have exfiltrated Active Directory data (NTDS.dit) in earlier stages, allowing credential harvesting and privilege escalation. Media and M&S leadership attributed involvement to a collective using DragonForce ransomware (deployed by groups such as Scattered Spider). 

**Mitigation & resolution steps taken:**
- Immediate containment: M&S suspended online orders and took affected systems offline to contain spread and limit further data exposure. citeturn2search0  
- Forensics & external responders: The company engaged cybersecurity experts and law enforcement; they scanned ~600 systems as part of the recovery and remediation process.  
- Recovery approach: M&S restored services in phases (clothing online sales resumed first; click-and-collect and other services returned later), rebuilt compromised services, and updated procedures for third‑party access and help‑desk workflows to reduce social‑engineering risk. Later public testimony indicated M&S was focusing on hardening identity and third‑party controls. 

**Outcome / status:** Recovery was staged over several weeks; direct financial impact was material (~£300m estimated hit to operating profit), and the public disclosures emphasized improved third‑party controls and help‑desk procedures as a central remediation priority. 

---

## 3) Genea (Australian IVF provider) — Termite ransomware / data theft (February 2025)
**What happened:** Genea, a major Australian fertility/IVF provider, experienced a February 2025 cybersecurity incident in which attackers accessed and later published sensitive patient data (hundreds of gigabytes up to ~700–940 GB reported by different sources). The ransomware/extortion group calling itself "Termite" claimed responsibility and published samples of stolen records on leak sites. Genea took legal and remedial actions and notified affected patients and authorities. 

**Attack method:** Public analysis and reporting indicate an intrusion that led to data exfiltration (the goal appeared to be extortion and publication of sensitive healthcare records). Analyses of Termite and similar gangs show they leverage a mix of: credential compromise, exploitation of exposed services or weak remote-access controls, and post‑compromise exfiltration and encryption. Splunk and other security teams later published technical breakdowns of Termite TTPs consistent with these steps. 

**Mitigation & resolution steps:**
- Legal injunction and law‑enforcement notification: Genea sought a court injunction to criminalise access to the published data and reported the incident to regulatory bodies and police. 
- Notification & support: Genea published incident updates, contacted affected patients, and offered support and guidance (identity‑protection recommendations) while engaging external incident response experts. citeturn3search0turn3search2  
- Operational response: Genea isolated impacted systems, conducted a full investigation, and coordinated with national cyber authorities; affected patients were advised to monitor for fraud and to follow identity-protection steps. Public reporting noted concerns about delayed communications and retention of historic data (which Genea addressed during their updates). 

---

## Short comparative takeaways (high-level)
- **Common vectors:** Social engineering (help‑desk targeting and third‑party compromise) and credential/exposed-service compromise remain predominant initial access methods. All three incidents highlight the risk of human-targeted attacks and third‑party supply chain vectors.  
- **Effective mitigations observed:** Rapid containment (taking services offline), engaging external IR and law enforcement, rebuilding from clean backups, legal/notification steps for data privacy, and hardening third‑party access and help‑desk workflows.  
- **Operational impact:** Ransomware and data‑theft incidents continue to impose large operational and financial costs and long recovery windows — underscoring that resilience planning (backups, identity safeguards, third‑party controls, and IR playbooks) is essential. 

---

## Sources (selected)
- Reuters reporting on Asahi Group outage and M&S impacts.   
- The Guardian coverage of Asahi and Genea incidents.   
- Bitdefender / BleepingComputer / TechCrunch on the Genea / Termite disclosure and technical notes.   
- Splunk analysis of Termite ransomware TTPs.  
- Multiple technical and news analyses of the M&S attack, social‑engineering help‑desk abuse, and DragonForce/Scattered Spider involvement (Reuters, Specops, and follow‑up Reuters testimony). 

---

