Task 1 - Network Reconnaissance 

This task focuses on identifying open ports in a local network using Nmap and understanding the scanning process using Wireshark.

Objective
- Perform a port scan on the local network using **Nmap**.
- Use Wireshark to observe SYN packets sent during the scan.
- Understand how attackers use port scanning to find vulnerabilities.

Tools Used

Nmap -  to scan IPs and discover open ports  
Wireshark - to monitor and analyze packet data   
Windows CMD / Terminal - To run Nmap commands     

 
Step 1: Find Your IP Address

- Open Command Prompt.
- Run: ipconfig(command)

- Found my IP as:
IPv4 Address: 192.168.214.19
Subnet Mask: 255.255.255.0
- Therefore, my network range is:  
192.168.214.0/24

Step 2: Nmap TCP SYN Scan

- Ran the following command in CMD:
nmap -sS 192.168.214.0/24 -oN scan_results.txt

This performed a stealth TCP SYN scan on all 256 IPs in my local network.

Step 3: Devices Found and Their Status
PS C:\Users\Pallavi> nmap -sS 192.168.214.0/24 -oN scan_results.txt
Starting Nmap 7.97 ( https://nmap.org ) at 2025-08-04 20:08 +0530
Nmap scan report for 192.168.214.178
Host is up (0.15s latency).
All 1000 scanned ports on 192.168.214.178 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
MAC Address: 92:75:8A:BB:EE:78 (Unknown)

Nmap scan report for 192.168.214.189
Host is up (0.018s latency).
All 1000 scanned ports on 192.168.214.189 are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)
MAC Address: 9E:2F:58:C5:0D:31 (Unknown)

Nmap scan report for 192.168.214.19
Host is up (0.0024s latency).
Not shown: 995 closed tcp ports (reset)
PORT     STATE SERVICE
- `80/tcp` - HTTP (Web Service)
- `135/tcp` - MSRPC (Windows RPC)
- `445/tcp` - Microsoft-DS (SMB File Sharing)
- `2323/tcp` - 3d-nfsd (Network File System)
- `8090/tcp` - opsmessaging (Messaging/Management Service)

Step 4: Observations & Security Risks

| Port | Service       | Risk                            |
|------|---------------|---------------------------------|
| 80   | HTTP          | Unencrypted, could leak data    |
| 445  | SMB File Share| Common target for ransomware    |
| 135  | MSRPC         | Used internally, avoid exposing |
| 2323 | 3d-nfsd       | Uncommon, could be suspicious   |
| 8090 | opsmessaging  | Ensure it's needed; could be abused |

- The other two devices had all ports filtered, likely protected by firewalls.
- My system has multiple open ports that should be reviewed.


 Step 5: Wireshark Packet Analysis

 What I Did:
- Opened "Wireshark"
- Selected my "Wi-Fi interface"
- Clicked "Start Capture"
- Ran the same Nmap command in CMD
- Stopped capture after scan finished
- Applied this filter:
"tcp.flags.syn == 1"


What I Observed:
- Saw "SYN packets" sent from my computer (`192.168.214.19`)
- Some replies were "SYN+ACK", showing the port was open
- Confirmed how Nmap uses SYN scanning to find live ports

 Step 6: Learning Outcomes

-  Learned to use Nmap to detect open ports
-  Understood TCP 3-way handshake (SYN, SYN-ACK)
-  Understood why unused ports should be closed
-  Practiced filtering SYN packets using Wireshark
-  Understood basics of reconnaissance and port-based vulnerability


