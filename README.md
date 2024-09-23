# Network Analysis and Escalation in SOC Environment

## Project Overview

This repository contains a comprehensive walkthrough of a network analysis scenario involving a suspicious `pcap` file provided by a client in a SOC (Security Operations Center) environment. The project demonstrates step-by-step analysis using tools like **Wireshark** to identify malicious activities such as port scanning, reconnaissance, and a web shell attack. The project also includes recommendations for escalating findings to the client.

## Contents

- `pcap` File Analysis
- Identifying Malicious Activities
- Tools and Techniques
- Escalation Template for Client Reporting

## Prerequisites

Before starting this project, ensure you have the following:

- A Windows 10 environment or equivalent system.
- **Wireshark** installed.
- Basic knowledge of TCP/IP networking and security concepts.
- Understanding of HTTP, TCP, and protocol hierarchies.

## Step-by-Step Guide

### 1. Download and Extract the `pcap` File

1. Download the `pcap` file from the provided link.
2. Extract the file using the password: `BT`.
3. If prompted for another password during extraction, use: `infected`.

### 2. Open the `pcap` File in Wireshark

1. Launch **Wireshark**.
2. Open the extracted `pcap` file.
3. Go to **Statistics** -> **Capture File Properties** to get an overview of the captured data, such as timestamp and duration.

### 3. Analyze Protocol Hierarchy

1. Navigate to **Statistics** -> **Protocol Hierarchy**.
2. Identify key protocols like `SSH`, `DNS`, `HTTP`, and `SMB`.
3. Note any potential lateral movement opportunities or cleartext protocols for further analysis.

### 4. Check Conversations

1. Go to **Statistics** -> **Conversations**.
2. Select the `IPv4` tab and sort by `Bytes`.
3. Identify top conversations and any unusual port activity, especially high bytes transfer or repeated connections.

### 5. Investigate Suspicious IP and Port Activity

1. Switch to the **TCP** tab under `Conversations`.
2. Look for repeated connections from a single source port (indicative of a port scan).
3. Note down IPs and ports involved in the scan and any responses from the target system.

### 6. Filter HTTP Traffic for Further Analysis

1. Apply a filter for HTTP streams: 

http.request or http.response

2. Right-click on suspicious packets and select **Follow** -> **HTTP Stream** to view the complete communication.
3. Look for keywords like `POST`, `GET`, `login`, `upload`, and potential user credentials.

### 7. Decode and Analyze Post Requests

1. Identify `POST` requests that may contain file uploads or credential submission.
2. Use a URL decoder for any encoded values found in the streams to reveal plaintext data.

### 8. Identify and Confirm Web Shell Activity

1. Look for suspicious file uploads, such as `upload.php` or `db_functions.php`.
2. Verify the success of file uploads and any command execution attempts.

### 9. Analyze Command and Control (C2) Communication

1. Monitor any connections to external IPs or unusual ports (e.g., 4422).
2. Use the **Follow TCP Stream** option to see if there are any C2 communications or shell commands being executed.

### 10. Document Findings and Escalate

1. Compile a list of key findings, including:
- Source and target IP addresses.
- Port scanning details.
- Web shell activity and uploaded file names.
- Command execution attempts and successful callbacks.
2. Draft an escalation report for the client, detailing the attack vector, potential impact, and recommended remediation steps.

## Escalation Template

Subject: Escalation Report for Suspicious Activity - [Client Name]

Dear [Client],

We have completed our analysis of the provided pcap file and have identified several suspicious activities:

Port Scanning: The IP address 10.251.96.4 conducted a TCP SYN scan on the range 1-1024 on the target IP 10.251.96.5.
Reconnaissance Tools: The attacker used Gobuster v3.0.1 for directory enumeration and SQLmap v1.4.7 for SQL injection testing.
Web Shell Upload: A web shell named db_functions.php was uploaded to the server 10.251.96.5.
Command Execution: The attacker executed several commands, including retrieving user information and establishing a reverse shell connection on port 4422.
We recommend immediate isolation of the affected system and a comprehensive security review of the network.

Best regards,
[Your Name]
SOC Analyst, [Your Organization]


## Tools Used

- **Wireshark**: For network traffic analysis.
- **URL Decoder**: To decode URL-encoded strings.
- **TCP Stream Analysis**: For following and analyzing HTTP and TCP conversations.

## Further Reading

- [TCP SYN Scans](https://example.com)
- [Web Shell Detection and Mitigation](https://example.com)
- [Wireshark Display Filters](https://example.com)

## Conclusion

This project demonstrates how to effectively analyze a `pcap` file for suspicious activity and prepare an escalation report for a client. If you have any questions or feedback, feel free to contact me.

**Stay curious and do things differently!**

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
