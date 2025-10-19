# DDoS Threat Analysis Report: The HTTP/2 Rapid Reset Campaign (2023) 🛡️

## Overview of Recent DDoS Threat Landscape

The Distributed Denial of Service (DDoS) landscape in 2023 was characterized by unprecedented scale and sophistication, driven primarily by the exploitation of new vulnerabilities, the use of powerful Virtual Machine (VM) based botnets, and an increase in hacktivism related to geopolitical conflicts.

Key trends identified include:

* **Hyper-Volumetric Attacks:** Attacks peaking at record-breaking rates, often targeting infrastructure providers like Cloudflare and various application-layer services.
* **Targeting of Financial Services:** The financial sector saw a dramatic 154% increase in attacks between 2022 and 2023, making it the most targeted industry, largely due to hacktivist and geopolitical motives.
* **Gaming Sector Persistence:** Gaming and gambling companies remained frequent targets for both network-layer (L3/4) and application-layer (L7) attacks, often motivated by financial gain or disruption.

---

## Investigated Incident Summary: HTTP/2 Rapid Reset Attacks

This report focuses on the **hyper-volumetric DDoS campaign** that exploited the **HTTP/2 Rapid Reset vulnerability** (CVE-2023-44487) in 2023, which fundamentally changed the scale of application-layer DDoS attacks.

| Category | Analysis |
| :--- | :--- |
| **Target** | Cloudflare's infrastructure and its customers, along with other major vendors. The attacks also caused disruption to major services like Microsoft Azure, OneDrive, and Outlook. |
| **Technology Used** | **HTTP/2 Rapid Reset Flaw:** The core technique exploited a zero-day vulnerability in the HTTP/2 protocol, allowing attackers to rapidly create and reset streams within a single connection. This made it possible for each bot to generate thousands of requests per second. **VM-Based Botnets:** Attackers leveraged botnets built from **Virtual Machines (VMs)** hosted on cloud computing platforms. These VMs provided up to **5,000 times more attack force** per node compared to traditional IoT-based botnets. |
| **Attacker's Motive** | The specific actor and motive were generally unknown, but the sophistication and persistent nature of the campaign—launching thousands of hyper-volumetric attacks—suggested a desire to demonstrate capability, test defensive boundaries, or facilitate **ransom DDoS** campaigns. |
| **Overall Impact** | The campaign set a new world record for DDoS attack volume, peaking at **201 million requests per second (rps)**. This was roughly **three times larger** than the previous recorded peak. The attack campaign caused service disruptions across various critical internet services and forced the wider industry to collaborate on defensive countermeasures. |

---

## Defensive Strategies and Mitigation

The unique nature of the HTTP/2 Rapid Reset attack required specific, immediate and adaptive mitigation strategies:

1.  **Protocol-Specific Mitigation:** Defenders had to immediately deploy **purpose-built technology and emergency countermeasures** to specifically address the rapid creation and reset of HTTP/2 streams. This involved modifying how the protocol handled streams to prevent resource exhaustion.
2.  **Automated, Always-On Protection:** Since the attacks were frequent and massive, relying on automated, **machine learning-based detection and mitigation systems** was crucial. These systems automatically profiled legitimate traffic and flagged anomalies indicative of the malicious hyper-volumetric floods.
3.  **Rate Limiting and Traffic Shaping:** Implementing strict **rate limiting** policies was essential to restrict the number of requests allowed from a single source, thereby nullifying the advantage gained by the rapid reset technique.
4.  **Cloud-Based Scrubbing Capacity:** Leveraging large, distributed cloud-based DDoS protection services allowed organizations to absorb the terabit-scale volumetric floods before they reached the target server's infrastructure, scaling mitigation capacity on demand.