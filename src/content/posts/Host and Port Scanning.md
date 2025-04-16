---
title: Host and Port Scanning
published: 2025-04-08
description: A simple note about linux.
tags: [Markdown, Blogging]
category: Nmap
draft: false
---
## Port States and Their Meanings

When scanning ports, Nmap can identify six different states that tell us about the target system:

1. **Open**: This means a service is actively accepting connections on this port. It could be TCP, UDP, or SCTP connections.
2. **Closed**: The port is shown as closed when the target responds with a RST (Reset) flag, indicating no service is running on that port.
3. **Filtered**: Nmap can't determine if the port is open or closed because either:
          - No response is received from the target
  - An error code is received


4. **Unfiltered**: This only happens during TCP-ACK scans and means the port is accessible but its state can't be determined.
5. **Open|Filtered**: When no response is received for a port, Nmap marks it as open|filtered, suggesting possible firewall protection.
6. **Closed|Filtered**: This only occurs in IP ID idle scans and indicates it was impossible to determine if the port is closed or filtered by a firewall.

## How Port States Are Determined

Let's look at how Nmap determines these states through packet exchange:

1. **SYN Scan (-sS)**:
          - Nmap sends a SYN packet to the target port
  - If the port is open, the target responds with SYN-ACK
  - If closed, the target responds with RST
  - If filtered, no response is received


2. **Connect Scan (-sT)**:
          - Sends a SYN packet to the target port
  - If open, target responds with SYN-ACK
  - Nmap completes the handshake with ACK
  - Then sends RST to close the connection
  - If closed, target responds with RST


3. **UDP Scan (-sU)**:
          - Sends empty UDP datagram to the port
  - If closed, target responds with ICMP Port Unreachable
  - If open, target might respond (but not always)
  - If filtered, no response is received



## Practical Scanning Examples

1. **Basic TCP Port Scan**:
```bash
sudo nmap 10.129.2.28 --top-ports=10
```


This scan shows:
  - Open ports (22/ssh, 25/smtp, 80/http, 110/pop3)
  - Closed ports (21/ftp, 23/telnet, 443/https)
  - Filtered ports (139/netbios-ssn, 445/microsoft-ds)


2. **Version Detection**:
```bash
sudo nmap 10.129.2.28 -Pn -n --disable-arp-ping --packet-trace -p 445 --reason -sV
```


This reveals:
  - Service versions (Samba smbd 3.X - 4.X)
  - Workgroup information (WORKGROUP)
  - Host details (Ubuntu)



## Best Practices for Scanning

1. **Scan Selection**:
          - Use appropriate scan types for your needs:
                    - SYN scan (-sS) for speed and stealth
    - Connect scan (-sT) for accuracy
    - UDP scan (-sU) for UDP ports


  - Consider network conditions and timing


2. **Port Selection**:
          - Scan specific ports when known (-p 22,25,80)
  - Use ranges for related services (-p 22-445)
  - Use --top-ports for common ports
  - Scan all ports (-p-) when thoroughness is required


3. **Scan Optimization**:
          - Disable unnecessary features:
                    - -Pn (disable host discovery)
    - -n (disable DNS)
    - --disable-arp-ping


  - Use --packet-trace for troubleshooting
  - Use --reason for detailed state information


4. **UDP Scanning Considerations**:
          - Expect longer scan times
  - Understand that "open|filtered" is common
  - Look for ICMP responses for closed ports
  - Be patient with timeouts



Understanding these scanning methods and their implications is crucial for effective network discovery. The choice of scanning technique depends on your goals, network conditions, and the information you need to gather.


## Understanding Host Discovery

Host discovery is the process of identifying which systems are active on a network. It's a crucial first step in network penetration testing that helps us understand our target environment.

## How Host Discovery Works

When we perform host discovery, Nmap uses different methods to determine if a host is alive:

1. **ICMP Echo Requests**:
          - Sends ICMP echo request packets to the target
  - Waits for ICMP echo reply responses
  - Most common and reliable method
  - Can be blocked by firewalls


2. **ARP Requests**:
          - Used for local network scanning
  - Sends ARP "who-has" requests
  - Waits for ARP replies
  - More reliable on local networks
  - Cannot cross network boundaries


3. **TCP SYN Requests**:
          - Sends TCP SYN packets to common ports
  - Waits for SYN-ACK or RST responses
  - More stealthy than ICMP
  - Can bypass some firewalls



## Practical Examples

1. **Basic Network Scan**:
```bash
sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
```


This command:
  - Scans the entire 10.129.2.0/24 network
  - Uses `-sn` to disable port scanning
  - Saves results in all formats
  - Shows only active hosts


2. **Single Host Discovery**:
```bash
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace
```


This shows:
  - Host status (up/down)
  - Response time
  - MAC address
  - Detailed packet information



## Understanding Results

When analyzing host discovery results, look for:

1. **Host Status**:
          - "Host is up" indicates active system
  - Response time shows network latency
  - MAC address reveals hardware vendor


2. **Packet Tracing**:
          - Shows exact packets sent and received
  - Helps understand response patterns
  - Useful for troubleshooting



## Best Practices

1. **Scan Selection**:
          - Use appropriate discovery methods for your network
  - Consider network topology
  - Think about detection avoidance needs


2. **Result Analysis**:
          - Document all findings
  - Verify results with multiple methods
  - Look for patterns in responses


3. **Tool Usage**:
          - Use `-sn` to disable port scanning
  - Enable packet tracing for troubleshooting
  - Save results for later comparison



Host discovery is the foundation of network penetration testing. Understanding how it works and interpreting its results correctly is essential for identifying potential targets and planning further testing strategies.