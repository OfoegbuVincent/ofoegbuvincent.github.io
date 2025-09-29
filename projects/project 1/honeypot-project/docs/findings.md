
# Findings from Honeypot Project

This document summarizes key lessons learned while deploying and experimenting with the Cowrie honeypot. The goal is to capture technical insights, defensive strategies, and areas for future improvement.

## 1.  Deception Reveals Adversary TTPs
- Honeypots act as  deception tools , exposing attacker  Tactics, Techniques, and Procedures (TTPs)  in a safe, controlled environment.  
- Cowrie logs revealed brute-force attempts, command executions, and scanning behavior.  
-**Lesson Learned**:  Deception technology provides defenders with early-warning signals and valuable threat intelligence.

## 2.  Principle of Least Privilege
- A dedicated  service account  was created to run Cowrie instead of using root.  
- Password login for this account was disabled, ensuring only key-based or controlled access was possible.  
-**Lesson Learned**:  This enforces the  principle of least privilege, reducing the attack surface and mitigating brute-force risks against service accounts.  
- This setup also demonstrates the concept of a  jump server/bastion host, where one hardened account is used to access another administrative service account.


## 3.  Weak Passwords in Brute-Force Attempts
- Logs showed constant brute-force activity using common/default passwords .  
- **Lesson Learned**:  
  - Accounts, especially administrative accounts, require strong, unique passwords .  
  - Multi-Factor Authentication (MFA) adds an additional layer of protection.  
  - Weak password hygiene remains a top attack vector for threats.

## 4. Firewall Controls Prevent Pivoting
- Firewall rules restricted outbound connections to essential services only (e.g., DNS, HTTP/HTTPS). 
- **Lesson Learned**:  Without these controls, a compromised honeypot could be abused as a pivot point for lateral movement or outbound attacks.  
- Outbound restrictions ensure the honeypot is only an observation point, not a launchpad.


## 5. Limits of Manual Log Monitoring
- Using `tail -f` to monitor Cowrie logs was useful but not scalable or sustainable.  
-  **Lesson Learned**:  Manual inspection quickly becomes impractical.  
-  Next Phase Driver:  This limitation is directly driving the next stage of the project — deploying a  dedicated centralized logging server with ELK (Elasticsearch, Logstash, Kibana) and Filebeat  for real-time monitoring and visualization.


## 6. Log Integrity & Tamper Resistance *(Consideration)*
-  Context:  While I did not observe attackers tampering with logs during this phase, it is a known adversary behavior.  
-  **Lesson Learned**:  Logs should be forwarded off-host to prevent tampering and preserve forensic integrity.  
-  Next Phase Driver:  This consideration further motivates the move toward a centralized ELK stack, ensuring logs are secured and cannot be altered locally.


## 7. Importance of Network Segmentation *(Consideration)*
-  Context:  In this project, the honeypot was not fully segmented into a DMZ or separate VLAN.  
-  **Lesson Learned**:  Best practice is to place honeypots in  isolated network segments  to prevent any compromise from spreading to production systems.  
-  Next Phase Driver:  As the project scales, combining segmentation with centralized ELK monitoring will enhance both security and visibility.


## 8. High Noise from Automated Scans *(Research Insight)*
-  Context:  I did not run automated scans or correlation during this phase, but research shows that most honeypots attract a high volume of background noise from internet bots and scanners.  
-  **Lesson Learned**:  Analysts must separate  background scanning activity from more targeted TTPs to avoid alert fatigue.  
-  Next Phase Driver:  ELK dashboards will provide the necessary visualization and filtering capabilities to distinguish noise from high-value events.

## 9. Threat Intelligence Value
- Captured IOCs (e.g., brute-force passwords, attacker IPs, executed commands) are valuable for threat intelligence.  
-  **Lesson Learned**:  Honeypots are not just deception tools but also threat intelligence feeds, contributing to blacklists, password dictionaries, and defensive playbooks.  



## 10. Legal & Ethical Considerations
- Honeypots attract real attackers, which raises legal and ethical responsibilities .  
-  **Lesson Learned**:  
  - The honeypot must not be abused to attack others.  
  - Logs and attacker data must be handled responsibly and in compliance with policies/regulations.  
- Isolation, strict egress rules, and ethical data use are essential for safe deployment.



# Next Steps
The findings point toward the next phase of this project:  
- Deploy a dedicated centralized log server with ELK, Filebeat, and Kibana to scale monitoring and preserve log integrity.  
- Explore network segmentation to further harden the honeypot environment.  
- Continue leveraging honeypots as threat intelligence feeds to enrich defenses.  
