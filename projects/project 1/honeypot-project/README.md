# Cowrie Honeypot Setup 🕵️‍♂️

This repository documents my journey setting up and experimenting with [Cowrie](https://github.com/cowrie/cowrie), an SSH/Telnet honeypot that logs brute force attacks and attacker interactions.  

This is **Phase 1** of the project: installing and running Cowrie successfully.  
Future phases will integrate Cowrie with the ELK stack (Elasticsearch, Logstash, Kibana) for advanced log analysis and visualization.  


## Repository Structure

.
├── README.md
├── screenshots/
│   └── (Cowrie logs, terminal sessions, etc.)
└── docs/
    ├── setup.md       # Step-by-step installation and configuration
    ├── operations.md  # Running and testing Cowrie
    └── findings.md    # Observations from captured activity

## Getting Started

If you want to replicate my setup, start with the **Setup Guide**:  
📄 [docs/setup.md](docs/setup.md)  

## Documentation

- [Setup Guide](docs/setup.md) – Installation & configuration steps  
-  [Operations Guide](docs/operations.md) – Running, testing, and maintaining Cowrie  
- [Findings](docs/findings.md) – Attacker behavior and logs observed  

## Screenshots

Screenshots of Cowrie in action are stored in the [`screenshots/`](screenshots) folder.  


## Disclaimer

This project is for **educational and research purposes only**.  
Do not expose this honeypot to the public internet without proper isolation, monitoring, and safety measures.  

##  Coming Soon

- Integration with Filebeat & ELK stack for visualization  
- Automated log forwarding  
- Trend analysis and attacker behavior dashboards

