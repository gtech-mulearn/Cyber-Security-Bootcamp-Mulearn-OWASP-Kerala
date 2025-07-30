# TryHackMe Room Report: *Further Nmap*

**Room Link:** [https://tryhackme.com/room/furthernmap](https://tryhackme.com/room/furthernmap)
**Completed By:** DILSHADN  
**Platform:** TryHackMe  
**Tools Used:** Nmap via CLI on Kali Linux  
**Difficulty Rating:** ★★★★★★★★★☆ (9/10)

---

## Note

This room was completed by me approximately a years ago and at the time I did not document the steps or take screenshots. This report is being written retroactively as part of a structured learning task. While screenshots are not included, I have included detailed technical reflections and explanations based on what I practiced and learned while completing the room.

---

## Room Objective

The “Further Nmap” room on TryHackMe is designed to help learners go beyond the basic `nmap -sV` usage and explore deeper scanning capabilities of Nmap. This includes working with scripts, alternate scan types, versioning, and enumeration methods that are essential for any penetration tester.

---

## Environment

* **OS Used**: Kali Linux
* **Nmap Interface**: Command-Line (CLI)
* **Tools**: Only Nmap (no Zenmap or third-party wrappers)

---

## Room Walkthrough Summary

Each task in the room covers an advanced aspect of Nmap scanning. Here's a summary of what was covered:

### Task 1: TCP Connect vs SYN Scans

Learned the difference between:

* `-sT` (TCP Connect) — a full handshake, more detectable.
* `-sS` (SYN Stealth) — half-open scan, stealthier and faster.

### Task 2: UDP Scanning

Used:

```bash
nmap -sU <IP>
```

Observed how much slower UDP scanning is and how some services (like DNS or SNMP) may only be discovered through UDP ports.

### Task 3: Service Versioning

Used:

```bash
nmap -sV <IP>
```

Learned how Nmap uses probes and matches for banner grabbing and version detection.

### Task 4: Aggressive Scan

Command:

```bash
nmap -A <IP>
```

This bundled OS detection, version detection, traceroute, and script scanning. Great for quick recon but noisy.

### Task 5: Default Scripts

Command:

```bash
nmap -sC <IP>
```

Learned that `-sC` runs the **default NSE (Nmap Scripting Engine)** scripts. These can identify things like:

* HTTP titles
* SSL cert info
* FTP anonymous access
* SMB versions

### Task 6: OS Detection

Used:

```bash
nmap -O <IP>
```

Nmap compares network behavior to an internal database to guess the target OS — though not always 100% accurate.

### Task 7: NSE Scripts

Used:

```bash
nmap --script <script-name> <IP>
```

Learned how to use custom and category-based scripts, e.g.:

```bash
nmap --script vuln <IP>
nmap --script http-title <IP>
```

---

## Reflection & Takeaways

Completing this room gave me a much deeper understanding of what Nmap is capable of beyond just `-sV`. Before doing this room, I was only using the basic flags, but after completing it:

* I learned how **UDP** and **SYN** scans behave differently.
* Understood how **OS detection** and **versioning** help in the early recon phase.
* Got hands-on experience using the **NSE scripting engine**, which is incredibly powerful when combined with categories like `auth`, `vuln`, `discovery`, etc.
* I mastered how to **chain multiple options** like `-A -sC -O` efficiently in real-world recon.

---

## Final Thoughts

Even though I completed the room in a single session long ago, I still remember how valuable it was to my foundational understanding of Nmap. The hands-on tasks and targeted questions helped me **master Nmap’s core usage in offensive security**.

