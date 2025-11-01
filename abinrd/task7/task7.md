# 7.3 Tbps DDoS Attack

In mid-May 2025, Cloudflare blocked the largest DDoS attack ever recorded: a staggering **7.3 terabits per second**.

The attack targeted a Cloudflare customer, a **hosting provider** that uses Magic Transit to defend their IP network. Hosting providers and critical Internet infrastructure have increasingly become targets of DDoS attacks, as reported in Cloudflare’s DDoS threat report.

The total amount of data sent to the target was **37.4 terabytes**, delivered in **less than a minute**. In context, 37.4 TB roughly equals:

- 9,350 high-definition movies  
- Over 9 million songs  
- 12.5 million photos  

The attack primarily exploited **User Datagram Protocol (UDP)** due to its fast, handshake-free delivery, commonly used for real-time applications like video streaming, online gaming, and virtual meetings. This makes UDP floods one of the most common tools in DDoS campaigns.

---

## Attack Details

- **Average destination ports targeted:** 21,925  
- **Peak destination ports per second:** 34,517  
- **Source IPs:** >122,145 spanning 5,433 Autonomous Systems in 161 countries  
- **Primary attack vectors:** UDP flood, QOTD reflection, Echo reflection, NTP reflection, Mirai UDP flood, Portmap flood, RIPv1 amplification  
- **Percentage of UDP traffic:** 99.996%  
- **Top source countries:** Brazil, Vietnam, Taiwan, China, Indonesia, Ukraine, Ecuador, Thailand, USA, Saudi Arabia  

---

## Attack Types Summary

| Attack Type | Protocol / Port | Mechanism | Prevention / Mitigation | Caution |
|------------|----------------|-----------|------------------------|---------|
| UDP Flood | UDP / Various | High volume of UDP packets to saturate network or appliances | Cloud-based volumetric DDoS protection, rate-limiting, drop unwanted UDP traffic | Aggressive filtering may disrupt VoIP, gaming, or VPN traffic |
| QOTD Reflection | UDP / 17 | Spoofed requests to QOTD servers amplify traffic | Disable QOTD service, block UDP/17, drop abnormal spikes | QOTD is obsolete; safe to disable |
| Echo Reflection | UDP/TCP / 7 | Echo protocol reflects spoofed traffic | Disable Echo service, block TCP/UDP port 7 | Obsolete diagnostic tool; safe to disable |
| NTP Reflection | UDP / 123 | Exploits `monlist` on old NTP servers | Disable `monlist`, restrict NTP queries to trusted IPs, filter UDP/123 | Blocking UDP/123 too broadly may affect time sync |
| Mirai UDP | UDP / Various | IoT botnet floods with random/service-specific UDP packets | Secure IoT devices, update firmware, monitor outbound traffic | Rate-limiting may impact legitimate UDP services |
| Portmap | UDP / 111 | RPC-based reflection attack | Disable if unnecessary, restrict access via ACLs | May disrupt RPC apps like NFS |
| RIPv1 | UDP / 520 | Spoofed routing updates to flood networks | Disable RIPv1, use authenticated RIPv2, block untrusted UDP/520 | Validate legacy routing before changes |

---

## Attacker Motives

While Cloudflare did not publicly attribute the attack to any group, likely motives include:

- **Testing attack capacity:** attackers may probe Cloudflare and hosting infrastructure limits.  
- **Ransom / extortion:** Q2 2025 saw an increase in ransom-DDoS attempts.  
- **Disruption / geopolitical / competitive:** hitting a hosting provider can affect many downstream customers.

---

## Overall Impact

- **Direct victim impact:** Attack was absorbed by Cloudflare without downtime, but such bursts can require operational response.  
- **Broader ecosystem impact:** Hyper-volumetric attacks strain upstream ISPs, increase mitigation costs, and highlight the need for distributed scrubbing and high-capacity networks.  
- **Record-breaking significance:** 7.3 Tbps is the largest publicly reported DDoS attack, showcasing the growth trend of hyper-volumetric attacks.

---

## Detection and Mitigation

### Distributed Mitigation
- Target IP advertised via **Cloudflare Anycast**, routing traffic to the closest data center.  
- Mitigation occurred across **477 data centers in 293 locations worldwide**.  

### Autonomous Detection
- All services run in every data center, enabling **fully autonomous detection and mitigation**.  

### Real-Time Fingerprinting
- Packets sampled from **Linux kernel XDP** using **eBPF**.  
- **dosd** (Denial of Service Daemon) analyzes packet patterns, header anomalies, and traffic heuristics.

---

## Defensive Strategies / Best Practices

- **Cloud-based protection:** Deploy volumetric DDoS scrubbing and CDN solutions.  
- **Rate-limiting:** Apply smart thresholds for UDP and other protocols.  
- **Ingress filtering / BCP38:** Prevent IP spoofing to reduce reflection/amplification attacks.  
- **Disable legacy services:** QOTD, Echo, Portmap, RIPv1, and NTP `monlist` if unused.  
- **Network visibility:** Monitor traffic patterns, ASNs, and ports in real-time.  
- **Incident playbooks:** Include BGP blackholing, upstream ISP coordination, and threat intelligence feeds.  
- **IoT security:** Update devices, change passwords, and monitor outbound traffic.  

---

## Key Takeaways

1. **Automation is critical:** Hyper-volumetric attacks can overwhelm human response.  
2. **Edge distribution matters:** Anycast spreads load and mitigates impact.  
3. **Prevent abuse at the source:** Patch vulnerable services and deploy anti-spoofing.  
4. **Layered defenses:** Combine cloud scrubbing, network filtering, and real-time analytics.  
5. **Operational preparedness:** Incident playbooks and threat intelligence reduce downtime and operational cost.  

---

