# -Report-on-Network-Vulnerabilities
## Objective

The purpose of this report is to assess network security based on the provided screenshots and tools used to identify vulnerabilities. This report includes vulnerabilities identified using various tools such as Nmap, Nikto, Wireshark, Netcat, Zenmap, and OpenVAS.



## Tools and Findings

### Nmap

**Usage:**  
Nmap is used for port scanning and OS detection in this report by running specific scripts.  
- For scanning a local network: `nmap <target-IP>`
- For OS detection: `nmap -o <target-IP>`
- For vulnerability scanning: `nmap --script vuln <target-IP>`

**Findings:**  
- Identified multiple operating systems, including Linux.
- Detected vulnerability to denial of service (DoS) as shown in the provided screenshot.

---

### Netcat

**Usage:**  
Netcat searches for open ports that could serve as potential entry points for attackers.  
- Command: `nc -zvu <target-IP> 20-100`

**Findings:**  
- Open ports detected: 20 (FTP), 21 (FTP), 22 (SSH), 80 (HTTP), and others between the range 20-100.

---

### Wireshark Traffic Analysis

**Findings:**
1. **TCP Retransmissions:**  
   - Multiple TCP retransmissions were noted between `10.0.2.4` and `10.0.2.15`.
   - **Impact:** This could indicate network performance issues or even Denial of Service (DoS) attacks.

2. **Suspicious UDP Traffic:**  
   - Detected UDP traffic from `10.0.2.4` to `10.0.2.15`.
   - **Impact:** Could be indicative of UDP flooding or misuse.

---

### Nikto Web Server Scan

**Usage:**  
Nikto scans a selected web server or application using the command: `nikto -h <target-IP or domain>`

**Findings:**  
- **Outdated Apache Version:** Apache/2.4.18 is outdated (current is at least 2.4.54).
- **Missing X-Frame-Options Header:** The site is vulnerable to Clickjacking attacks.
- **Outdated PHP Version:** The web server is running PHP version 5.4.5, which is outdated.

---

### OpenVAS and Zenmap

**Note:**  
Could not use OpenVAS and Zenmap due to installation issues and packet-related errors.

---

## Recommendations

1. **Patch and Update All Services:**
   - Upgrade Apache, PHP, and other outdated services to their latest versions to mitigate exposure to known vulnerabilities.

2. **Secure ARP Traffic:**
   - Implement measures like static ARP entries or dynamic ARP inspection (DAI) to protect against ARP spoofing.

3. **Implement Strong Authentication and Encryption:**
   - Enforce SSH authentication using public key cryptography.

4. **Monitor for Anomalies:**
   - Investigate any anomalies in the network such as TCP retransmissions, frequent ARP requests, and suspicious UDP traffic.
