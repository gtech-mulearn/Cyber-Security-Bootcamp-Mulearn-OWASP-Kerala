
# GitHub DDoS (Feb 28, 2018) — Summary

## 1) Target

GitHub’s public code hosting platform (github.com). The attack aimed its traffic at GitHub’s public-facing IP addresses and services. ([The GitHub Blog][1])

## 2) Technology used by the attacker

The attackers abused **open, unauthenticated Memcached servers** to perform a reflection/amplification DDoS. By sending small spoofed UDP requests to Memcached instances, each server replied with a much larger response aimed at GitHub — producing extremely large amplified traffic (the reported peak was ~1.35 Tbps and ~127M packets/sec). This memcached amplification method yields huge amplification factors and made the attack unusually powerful without needing a large botnet. ([The GitHub Blog][1])

## 3) Attacker’s motive

The public reporting did not identify a clear geopolitical or extortion motive; the attack appears to have been an attempt to cause disruption and demonstrate the effectiveness of memcached amplification. Some large DDoS incidents also include ransom/attention motives, but GitHub’s incident was primarily notable for the technique and scale rather than a disclosed ransom demand. ([Security Week][2])

## 4) Overall impact

* **Duration & disruption:** The volumetric peak was brief (minutes), but it caused intermittent service disruption. GitHub’s systems experienced strain before mitigation was applied.
* **Scale:** The attack peaked at ~1.35 Tbps and tens of millions of packets per second — one of the largest recorded DDoS events at the time.
* **Business impact:** Short-term availability issues and an operational incident that mobilized mitigation resources (Akamai/Prolexic). No long-term data breach was reported from this DDoS event. ([The GitHub Blog][1])

## 5) Defensive strategies that could have mitigated it

Practical mitigations (some were used by GitHub and its provider) include:

* **Use a robust scrubbing/CDN/DDoS mitigation provider** (GitHub routed traffic through Akamai Prolexic to scrub malicious traffic). ([enterprisetimes.co.uk][3])
* **Close or firewall Memcached (and other UDP-based cache) servers** so they are not publicly accessible; disable UDP for Memcached unless required and permitted. (The root cause was exposed Memcached instances.) ([WIRED][4])
* **Ingress filtering (BCP38) / anti-spoofing** to make IP spoofing harder for attackers — reduces efficacy of reflection attacks.
* **Rate limiting and network-layer filtering** at transit/peering points to drop obviously spoofed or oversized responses.
* **Network and application-layer capacity planning and playbooks** — automated detection and fast failover to mitigation providers (GitHub had rapid incident playbooks). ([Medium][5])

---

## Short takeaway

The GitHub memcached attack showed how misconfigured internet-facing services (memcached) + IP spoofing create low-effort, very high-impact DDoS vectors — fix exposure, apply anti-spoofing, and use professional scrubbing/CDN services to reduce risk. ([The GitHub Blog][1])

---

**Prepared By:** *DILSHAD AHAMMED N*

**Date:** Oct 4, 2025

[1]: https://github.blog/news-insights/company-news/ddos-incident-report/?utm_source=chatgpt.com "February 28th DDoS Incident Report"
[2]: https://www.securityweek.com/largest-ever-13tbps-ddos-attack-includes-embedded-ransom-demands/?utm_source=chatgpt.com "Largest Ever 1.3Tbps DDoS Attack Includes Embedded ..."
[3]: https://www.enterprisetimes.co.uk/2018/03/02/github-shakes-1-35tbps-ddos-attack/?utm_source=chatgpt.com "GitHub shakes off 1.35Tbps DDoS attack -"
[4]: https://www.wired.com/story/github-ddos-memcached/?utm_source=chatgpt.com "GitHub Survived the Biggest DDoS Attack Ever Recorded"
[5]: https://medium.com/%40mganeshram2005/%EF%B8%8F-case-study-github-ddos-attack-2018-3e9c9cd4be80?utm_source=chatgpt.com "️ Case Study: GitHub DDoS Attack (2018) | by Mganeshram"
[6]: https://www.a10networks.com/blog/5-most-famous-ddos-attacks/?utm_source=chatgpt.com "Five Most Famous DDoS Attacks and Then Some"
