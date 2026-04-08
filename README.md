# Ligolo-Ng: Advanced Network Pivoting & Double Tunneling Lab

Project Overview
This project demonstrates a high-level **Red Teaming technique** involving **Lateral Movement** and **Network Pivoting** in a multi-segmented lab environment. Using **Ligolo-Ng**, I established stealthy tunnels to bypass network boundaries and compromise targets deep within an internal infrastructure.

Lab Architecture
The environment is divided into three distinct zones to simulate a real-world enterprise network:
* **Network A (External):** Attacker machine (Kali Linux).
* **Network B (Internal DMZ):** First Pivot (Windows Server 2019).
* **Network C (Isolated Segment):** Final Target (Metasploitable2).

---

Step-by-Step Methodology

Phase 1: Initial Access & Setup
1. **Interface Prep:** Created a dedicated `tun` interface named `ligolo` on Kali Linux to handle the tunneled traffic.
2. **C2 Proxy:** Initialized the Ligolo-Ng proxy server on the attacker machine.
3. **Payload Delivery:** Hosted the `agent.exe` on an attacker-controlled server and downloaded it to the first target via a reverse shell.

Phase 2: Single Pivoting (Compromising Network B)
1. **Agent Callback:** Executed the agent on the Windows Server to call back to the Kali proxy.
2. **Routing:** Added a static IP route on Kali to forward all Network B traffic (192.168.148.0/24) through the Ligolo interface.
3. **Internal Recon:** Performed `nmap` and `netexec` scans to discover active hosts in the second segment.


Phase 3: Double Pivoting (Accessing Network C)
1. **Lateral Movement:** Leveraged `impacket-psexec` to jump from the first pivot to a Windows 10 machine in Network B.
2. **Double Tunneling:** Established a second tunnel through the Windows 10 machine to reach the isolated Network C.
3. **Final Objective:** Successfully scanned and interacted with the **Metasploitable2** instance (192.168.159.129).

