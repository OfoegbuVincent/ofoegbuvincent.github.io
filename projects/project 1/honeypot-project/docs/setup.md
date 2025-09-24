
# Cowrie Honeypot Setup Guide 🛠️

This document explains how I installed and configured [Cowrie](https://github.com/cowrie/cowrie), an SSH/Telnet honeypot designed to capture attacker activity.  

---

## 1. Prerequisites

- Ubuntu 24.04.3 LTS (or similar Linux environment)  
- Python 3.10+  
- Git installed  
- Non-root user with `sudo` privileges  

📸 *Screenshot Placeholder: Upgrading and Updating System (e.g., `Sudo apt-get update && sudo apt-get upgrade -y`)*  
![Update and Upgrade Linux](../screenshoots/update_linux.png)  

---

## 2. Update Firewall Rules

Before running Cowrie, configure the firewall to allow necessary outbound and loopback traffic. Example using `iptables`:
```bash
# Default policy: drop all outgoing traffic
sudo iptables -P OUTPUT DROP

# Allow loopback interface
sudo iptables -A OUTPUT -o lo -j ACCEPT

# Allow established and related connections (conntrack)
sudo iptables -A OUTPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# Allow DNS (UDP port 53)
sudo iptables -A OUTPUT -p udp --dport 53 -j ACCEPT

# Allow HTTP (TCP port 80) and HTTPS (TCP port 443)
sudo iptables -A OUTPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A OUTPUT -p tcp --dport 443 -j ACCEPT
```
📸 *Screenshot Placeholder: Updating Firewall Rules
![Update Firewall Rules](../screenshoots/firewallrules.png)
