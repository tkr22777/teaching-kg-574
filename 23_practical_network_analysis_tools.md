# Practical Network Analysis Tools

## Overview

We'll explore essential networking tools for analyzing and troubleshooting networks from the physical layer to the application layer. This guide is organized by operating system to provide a focused reference for Windows, macOS, and Linux users, ensuring you can find the right commands for your environment.

---

## Linux

### Tool Installation

The following command will install a comprehensive set of networking tools on Debian-based distributions like Ubuntu.

```bash
# Update package list
sudo apt update

# Install essential networking tools
sudo apt install -y \
  net-tools \          # Classic network utilities (ifconfig, arp, netstat)
  iproute2 \           # Modern network utilities (ip, ss)
  iputils-ping \       # The ping utility for testing reachability
  traceroute \         # Trace the path packets take to a destination
  dnsutils \           # DNS query tools (dig, nslookup)
  curl \               # Transfer data with URLs (HTTP, FTP, etc.)
  wget \               # Download files from the web
  tcpdump \            # Command-line packet analyzer
  wireshark \          # Graphical packet analyzer
  nmap \               # Network scanner and security auditor
  iperf3 \             # Network bandwidth measurement tool
  nethogs \            # Monitor network traffic by process
  ethtool \            # Query or control network driver and hardware settings
  ipcalc               # IP subnet calculator
```

### Layer-by-Layer Tool Coverage

#### Physical Layer (Layer 1)

- **ethtool**: View network interface statistics, link speed, and duplex mode.
  - `ethtool eth0`
- **ip link / ifconfig**: Check the status of network interfaces.
  - `ip link show` (modern)
  - `ifconfig` (classic)

#### Data Link Layer (Layer 2)

- **ip neigh / arp**: View and manipulate the ARP cache to see IP-to-MAC address mappings.
  - `ip neigh show` (modern)
  - `arp -a` (classic)
- **VLAN & Switching**: Show VLAN configurations and bridge information.
  - `ip link show type vlan`
  - `brctl show`

#### Network Layer (Layer 3)

- **ping**: Test reachability and measure latency.
  - `ping 8.8.8.8`
- **traceroute**: Map the network path to a destination.
  - `traceroute google.com`
- **ip route**: View the routing table.
  - `ip route show`
- **ipcalc**: Calculate IP subnet details.
  - `ipcalc 192.168.1.0/24`

#### Transport Layer (Layer 4)

- **ss / netstat**: Display network connections and listening ports. `ss` is the modern replacement for `netstat`.
  - `ss -tunap`
  - `netstat -anp`
- **lsof**: List open files and identify which process is using a specific port.
  - `lsof -i :80`
- **nmap**: Scan for open ports and services on a remote host.
  - `nmap -sV 192.168.1.1`
- **netcat (nc)**: A versatile tool for testing port connectivity.
  - `nc -zv google.com 80-443`

#### Application Layer (Layers 5-7)

- **dig / nslookup**: Query DNS servers for record information. `dig` is more advanced.
  - `dig google.com MX`
  - `nslookup google.com`
- **curl**: Test web services and API endpoints.
  - `curl -I https://example.com`
- **openssl**: Test secure connections (TLS/SSL).
  - `openssl s_client -connect example.com:443`

### Specialized Tools

- **Wireless Networks**:
  - `iwconfig`: Configure wireless network interfaces.
  - `sudo iwlist wlan0 scan`: Scan for available Wi-Fi networks.
  - `nmcli device wifi list`: A modern tool for listing Wi-Fi networks.
- **Traffic & Bandwidth Monitoring**:
  - **tcpdump**: Capture packets from the command line.
    - `sudo tcpdump -i eth0 -w capture.pcap`
  - **nethogs**: Monitor bandwidth usage per process.
    - `sudo nethogs eth0`
  - **iperf3**: Measure network throughput.
    - Server: `iperf3 -s`
    - Client: `iperf3 -c server_ip`
- **Firewall Status**:
  - `sudo iptables -L -v -n` (for iptables)
  - `sudo firewall-cmd --list-all` (for firewalld)
  - `sudo ufw status verbose` (for UFW)

---

## macOS

### Tool Installation (Homebrew)

Use [Homebrew](https://brew.sh/) to install these tools. Many, like `ping` and `tcpdump`, are already built-in.

```bash
# Install Homebrew if not already installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install networking tools
brew install \
  nmap \               # Network scanner and security auditor
  wireshark \          # Graphical packet analyzer
  iperf3 \             # Network bandwidth measurement tool
  wget \               # Download files from the web
  speedtest-cli        # Command-line interface for testing internet bandwidth
```

### Layer-by-Layer Tool Coverage

#### Physical Layer (Layer 1)

- **ifconfig**: Check network interface status and configuration.
  - `ifconfig`
- **networksetup**: A command-line tool for configuring network settings.
  - `networksetup -listallhardwareports`

#### Data Link Layer (Layer 2)

- **arp**: View and manipulate the ARP cache.
  - `arp -a`

#### Network Layer (Layer 3)

- **ping**: Test reachability and measure latency.
  - `ping 8.8.8.8`
- **traceroute**: Map the network path to a destination.
  - `traceroute google.com`
- **netstat**: View the routing table.
  - `netstat -rn`

#### Transport Layer (Layer 4)

- **lsof**: List open files and identify processes using specific ports.
  - `lsof -i :80`
- **netstat**: Display active network connections.
  - `netstat -an`
- **nmap**: Scan for open ports and services on a remote host.
  - `nmap -sV 192.168.1.1`
- **netcat (nc)**: Test port connectivity.
  - `nc -zv google.com 80`

#### Application Layer (Layers 5-7)

- **dig / nslookup**: Query DNS servers.
  - `dig google.com`
  - `nslookup google.com`
- **curl**: Test web services and APIs (built-in).
  - `curl -v https://example.com`
- **openssl**: Test secure connections (built-in).
  - `openssl s_client -connect example.com:443`

### Specialized Tools

- **Wireless Networks**:
  - `airport`: A command-line tool for managing wireless connections.
    - Scan: `/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -s`
    - Info: `/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I`
- **Traffic & Bandwidth Monitoring**:
  - **tcpdump**: Capture packets from the command line (built-in).
    - `sudo tcpdump -i en0`
  - **nettop**: Display real-time network usage by process (built-in).
    - `nettop -m tcp`
  - **iperf3**: Measure network throughput.
    - Server: `iperf3 -s`
    - Client: `iperf3 -c server_ip`
- **Firewall Status**:
  - `sudo /usr/libexec/ApplicationFirewall/socketfilterfw --getglobalstate`

---

## Windows

### Tool Installation (Chocolatey & Built-in)

Many essential tools are built into Windows. For others, the [Chocolatey](https://chocolatey.org/) package manager is recommended.

```powershell
# Run PowerShell as Administrator

# Install Chocolatey package manager (if not installed)
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

# Install tools with inline explanations
choco install -y wireshark  # Graphical packet analyzer
choco install -y nmap       # Network scanner and security auditor  
choco install -y wget       # Download files from the web
choco install -y iperf3     # Network bandwidth measurement tool

# Note: curl, ping, tracert, nslookup, netstat, ipconfig are built-in.
# For advanced capabilities, Windows Subsystem for Linux (WSL) is recommended.
```

### Layer-by-Layer Tool Coverage

#### Physical Layer (Layer 1)

- **ipconfig**: The primary tool for viewing network adapter configuration.
  - `ipconfig /all`
- **netsh**: A command-line utility for managing network configurations.
  - `netsh interface show interface`

#### Data Link Layer (Layer 2)

- **arp**: View and manipulate the ARP cache.
  - `arp -a`
- **netsh**: Can show bridge adapter information.
  - `netsh bridge show adapter`

#### Network Layer (Layer 3)

- **ping**: Test reachability and measure latency.
  - `ping 8.8.8.8`
- **tracert**: Map the network path to a destination.
  - `tracert google.com`
- **route**: View the IP routing table.
  - `route print`

#### Transport Layer (Layer 4)

- **netstat**: Display active network connections and listening ports.
  - `netstat -ano`
- **Test-NetConnection**: A powerful PowerShell cmdlet for testing connectivity.
  - `Test-NetConnection -ComputerName google.com -Port 443`
- **nmap**: Scan for open ports and services on a remote host.
  - `nmap -sV 192.168.1.1`
- **TCPView**: A free GUI tool from Sysinternals for real-time connection monitoring.

#### Application Layer (Layers 5-7)

- **nslookup**: Query DNS servers.
  - `nslookup google.com`
- **Resolve-DnsName**: The modern PowerShell equivalent for DNS queries.
  - `Resolve-DnsName google.com -Type ALL`
- **curl**: A versatile tool for transferring data with URLs (built-in).
  - `curl.exe -I https://example.com`

### Specialized Tools

- **Wireless Networks**:
  - **netsh**: The primary command-line tool for managing Wi-Fi.
    - `netsh wlan show interfaces`
    - `netsh wlan show networks`
- **Traffic & Bandwidth Monitoring**:
  - **Resource Monitor**: A built-in GUI (`resmon.exe`) that shows real-time network activity per process.
  - **iperf3**: Measure network throughput.
    - Server: `iperf3 -s`
    - Client: `iperf3 -c server_ip`
- **Firewall Status**:
  - **netsh**:
    - `netsh advfirewall show allprofiles`
  - **PowerShell**:
    - `Get-NetFirewallProfile`

---

## Comprehensive GUI Tool: Wireshark

Wireshark is the world's foremost network protocol analyzer, available for all major operating systems. It allows you to see what’s happening on your network at a microscopic level.

**Essential Features:**
- **Capture and Display Filters**: Isolate the traffic you want to see.
- **Protocol Hierarchy**: View traffic distribution by protocol.
- **Follow Streams**: Reconstruct TCP/UDP conversations to see application data.

**Common Filters:**
```
# Filter by IP address
ip.addr == 192.168.1.100

# Filter by protocol
http
dns

# Filter by TCP port
tcp.port == 443

# Combination filter
ip.src == 192.168.1.100 && tcp.port == 443
```

---

## Practical Lab Exercises

### Exercise 1: Complete Network Diagnostics

**Scenario:** A website is unreachable. Use the tools for your OS to diagnose the issue step-by-step.

**Steps:**
1.  **Physical layer**: Check interface status (`ip link show` / `ifconfig` / `ipconfig /all`).
2.  **Network layer**: Test connectivity (`ping 8.8.8.8`, then `ping gateway_ip`).
3.  **Routing**: Check the path (`traceroute` / `tracert`).
4.  **Transport layer**: Check if the port is reachable (`nc` / `Test-NetConnection`).
5.  **Application layer**: Test the application protocol (`curl -v http://example.com`).
6.  **DNS**: Verify name resolution (`nslookup example.com`).

### Exercise 2: Bandwidth Analysis

**Goal:** Identify which application is consuming the most bandwidth.

**Steps:**
1.  **Monitor current connections** (`ss` / `netstat -an` / `netstat -ano`).
2.  **Monitor per-process bandwidth** (`nethogs` / `nettop` / Resource Monitor).
3.  **Capture traffic** with Wireshark and use `Statistics → Conversations` to find top talkers.
4.  **Test available bandwidth** between two systems with `iperf3`.

### Exercise 3: Security Audit

**Goal:** Perform a basic security check on your own machine.

**Steps:**
1.  **List listening ports** (`ss -ln` / `lsof -i -P` / `netstat -anob`).
2.  **Identify associated processes** for each open port.
3.  **Scan your machine** from another device on the network (`nmap -sV your_ip`).
4.  **Check firewall rules** using the commands for your OS.
5.  **Analyze unexpected traffic** with Wireshark.

---

## Quick Reference by Use Case

| Task | Linux/macOS | Windows |
|------|-------------|---------|
| Check IP config | `ip addr` / `ifconfig` | `ipconfig /all` |
| Test connectivity | `ping` | `ping` |
| Trace route | `traceroute` | `tracert` |
| DNS lookup | `dig` / `nslookup` | `nslookup` |
| View connections | `ss -tunap` / `netstat -an` | `netstat -ano` |
| Capture packets | `tcpdump` | Wireshark |
| Scan ports | `nmap` | `nmap` / `Test-NetConnection` |
| Test bandwidth | `iperf3` | `iperf3` |
| Monitor bandwidth | `nethogs` / `nettop` | Resource Monitor |
| Check route table | `ip route` / `netstat -rn` | `route print` |
| Check ARP cache | `ip neigh` / `arp -a` | `arp -a` |

---

## Best Practices

### When Using Network Tools

1. **Start Simple**: Begin with basic tools (ping, traceroute) before advanced tools
2. **Document Baseline**: Record normal network behavior for comparison
3. **Use Appropriate Privileges**: Some tools require root/administrator access
4. **Be Ethical**: Only scan networks you own or have permission to test
5. **Understand Output**: Learn to interpret results, not just run commands
6. **Cross-verify**: Use multiple tools to confirm findings
7. **Consider Impact**: Heavy scanning or traffic generation can affect network performance

### Tool Selection Strategy

1. **Built-in First**: Try OS-native tools before installing third-party software
2. **CLI for Automation**: Command-line tools for scripts and remote systems
3. **GUI for Exploration**: Graphical tools like Wireshark for learning and deep analysis
4. **Platform Consistency**: Learn cross-platform tools (curl, nmap) for transferable skills

---

## Troubleshooting Common Issues

### Tool Installation Problems

**Linux:**
- Update package lists: `sudo apt update`
- Check repository availability
- Use alternative package managers (yum, dnf, pacman)

**macOS:**
- Install Xcode Command Line Tools: `xcode-select --install`
- Install Homebrew: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

**Windows:**
- Run PowerShell as Administrator
- Set execution policy: `Set-ExecutionPolicy RemoteSigned`
- Check Windows Firewall isn't blocking downloads

### Permission Issues

**Linux/macOS:**
- Use `sudo` for privileged operations
- Add user to appropriate groups: `sudo usermod -aG wireshark $USER`
- Set capabilities: `sudo setcap cap_net_raw,cap_net_admin+eip /usr/bin/tcpdump`

**Windows:**
- Run Command Prompt or PowerShell as Administrator
- Install WinPcap or Npcap for packet capture
- Check User Account Control (UAC) settings

---

## Additional Resources

### Online Tools (No Installation)

- **dnschecker.org**: DNS propagation checker
- **mxtoolbox.com**: Email server testing
- **speedtest.net**: Bandwidth testing
- **ping.pe**: Multi-location ping and traceroute
- **ipinfo.io**: IP address information

### Learning Resources

- Wireshark documentation: wireshark.org/docs
- Nmap reference guide: nmap.org/book
- TCP/IP Guide: tcpipguide.com
- PacketLife cheat sheets: packetlife.net/library/cheat-sheets

### Certification-Relevant Tools

These tools align with industry certifications:
- **CompTIA Network+**: ping, traceroute, netstat, nslookup, ipconfig/ifconfig
- **Cisco CCNA**: Wireshark, packet tracer (simulation)
- **CEH**: nmap, Wireshark, tcpdump
- **CISSP**: Network security tools and analysis

