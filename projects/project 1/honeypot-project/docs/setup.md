
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

## 3. Install Dependencies

Cowrie requires several packages and libraries. I Installed them using:

```bash
sudo apt install -y git python3-venv python3-pip build-essential libssl-dev libffi-dev libpython3-dev authbind

```
📸 *Screenshot Placeholder: Intsalled Dependencies
![Install Dependencies](../screenshoots/dependencies.png)

## 4. Create a Non-root User With Sudo Privileges
This minimizes the attack surface by isolating cowrie to that user. 
```bash
sudo adduser --disabled-password <user>
```
📸 *Screenshot Placeholder: Add a Non-root User
![Added a Non-root User](../screenshoots/addeduser.png)

## 5. Clone the Cowrie Repository

With the non-root user created, the next step is to clone the official [Cowrie repository](https://github.com/cowrie/cowrie) from GitHub.  

Switch to the non-root user (replace `cowrie` with the username you created):  
```bash
sudo su - cowrie
```
Then clone the repository:
```bash
git clone https://github.com/cowrie/cowrie.git
cd cowrie
```

📸 *Screenshot Placeholder: Add a Non-root User
![Added a Non-root User](../screenshoots/clonedcowrie.png)

