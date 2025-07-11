# nmap-labs
# 🛠️ Nmap Practice Lab – Localhost Scans

## 🖥️ Environment
- **Device**: My own laptop
- **Operating System**: Ubuntu
- **Network**: Guest Wi-Fi (isolated)
- **Target**: `127.0.0.1` (localhost)

All scans were performed against `127.0.0.1`, the loopback interface of my own machine. This ensures the lab is safe, ethical, and legally compliant.

---

## 🔍 Scans Performed

### 1. 🔹 Basic Port Scan
```bash
nmap 127.0.0.1
```
**Purpose**: Scans the top 1000 most common TCP ports to find which are open.

**Result Summary**:
- Discovered 1 open port (631/tcp — IPP)

---

### 2. 🔹 Service Version Detection
```bash
nmap -sV 127.0.0.1
```
**Purpose**: Identifies services running on open ports and attempts to determine their version.

**Result Summary**:
- Port 631: CUPS 2.4 printing service detected

---

### 3. 🔹 Default Scripts + Service Detection
```bash
nmap -sV --script=default 127.0.0.1
```
**Purpose**: Runs default scripts based on detected ports and services. These scripts gather metadata such as:
- HTTP titles
- SSL certificates
- Robots.txt entries

**Result Summary**:
- Port 631: Detected CUPS web interface
- Retrieved robots.txt and title info
- Displayed self-signed SSL certificate metadata

---

### 4. 🔹 Full Port Scan (optional/longer)
```bash
nmap -p- 127.0.0.1
```
**Purpose**: Scans all 65,535 TCP ports to detect services running on uncommon ports.

**Result Summary**:
- No unexpected ports found beyond port 631

---

### 5. 🔹 OS Detection (Fingerprinting)
```bash
sudo nmap -O 127.0.0.1
```
**Purpose**: Attempts to identify the operating system of the target by analyzing subtle differences in how it responds to network probes.

**Why Use `sudo`?**  
The `-O` (OS detection) feature often needs **root privileges** to send and analyze low-level TCP/IP packets for accurate fingerprinting.

**Result Summary**:
- OS detection was attempted but may have been unreliable due to limited port availability
- Nmap typically needs at least one open and one closed port to make an accurate OS guess
- On `127.0.0.1`, results may be vague (e.g., "Linux-based OS (general purpose)")

---

## 📁 Output Files

All full scan results are saved in:

```
localhost-scan.txt
```

Use the `-oN` flag to generate the file:
```bash
nmap -sV --script=default 127.0.0.1 -oN localhost-scan.txt
```

(Optional: Save other outputs to `localhost-os-detect.txt`, `localhost-p-all.txt`, etc.)

---

## 🧠 Reflections

This mini-lab taught me:

- Nmap can gather detailed service metadata even on local-only services
- Loopback scans are a safe and useful way to learn about local services
- The `--script=default` option dynamically runs scripts based on detected ports and services
- OS detection with `-O` can provide high-level system info, but needs more open/closed ports to be accurate

---

## ⚠️ Safety Note

This lab was conducted entirely on my own machine using the loopback IP (`127.0.0.1`).  
No unauthorized devices or public IPs were scanned.
