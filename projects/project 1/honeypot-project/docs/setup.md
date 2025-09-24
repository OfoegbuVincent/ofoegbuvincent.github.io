
# Cowrie Honeypot Setup Guide 🛠️

This document explains how I installed and configured [Cowrie](https://github.com/cowrie/cowrie), an SSH/Telnet honeypot designed to capture attacker activity.  

---

## 1. Prerequisites

- Ubuntu 24.04.3 LTS (or similar Linux environment)  
- Python 3.10+  
- Git installed  
- Non-root user with `sudo` privileges  

📸 *Screenshot Placeholder: Upgrading and Updating System (e.g., `Sudo apt-get update && sudo apt-get upgrade -y`)*  
`![Update and Upgrade Linux](../screenshoots/update_linux.png)`  

---

## 2. Clone the Cowrie Repository

```bash
git clone https://github.com/cowrie/cowrie
cd cowrie
