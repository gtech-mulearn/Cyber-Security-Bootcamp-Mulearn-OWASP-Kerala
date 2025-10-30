# Incident Overview: Record-Breaking 22.2 Tbps DDoS Attack

---

## Incident Details

### Target

- **Victim**: An undisclosed customer of Cloudflare (kept private for security reasons)  
- **Protector**: Cloudflare, whose automated systems detected and mitigated the attack before causing service disruption

### Technology Used

- **Attack Type**: Hyper-volumetric UDP (User Datagram Protocol) flood  
- **Sources**: Hundreds of thousands of compromised devices, including IoT devices and virtual machines on cloud providers  
- **Peak Traffic**: 22.2 terabits per second (Tbps) and 10.6 billion packets per second (Bpps)  
- **Duration**: Approximately 40 seconds  

### Attacker’s Motive

- Exact motive unknown; possible motivations include:
  - **Financial extortion**: Ransom DDoS (RDDoS)  
  - **Hacktivism**: Political or ideological reasons  
  - **Competitive advantage**: Disrupting rival services  
  - **Demonstration of capability**: Testing cyber defenses  

### Overall Impact

- **Customer Experience**: No service disruption or downtime due to Cloudflare's mitigation  
- **Wider Internet Community**: Highlighted the increasing scale and intensity of DDoS threats, showing the need for sophisticated, automated defenses

### Defensive Strategies

Cloudflare successfully mitigated the attack using a multi-layered, automated approach:

1. **Global Anycast Network**  
   - Traffic dispersed across Cloudflare’s worldwide data centers, preventing any single node from being overwhelmed  
2. **Automated Detection**  
   - Machine learning analyzes network traffic in real-time to detect malicious patterns  
3. **Real-Time Mitigation**  
   - Automatically generates and deploys “fingerprints” to drop malicious packets within seconds without affecting legitimate traffic  
4. **Low-Level Packet Filtering**  
   - Advanced kernel-level filtering with eBPF and XDP inspects and drops malicious packets efficiently with minimal resource use
