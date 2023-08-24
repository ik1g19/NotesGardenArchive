---
title: "Network Monitoring"
---

# **Network Monitoring**
Metrics to monitor to indicate a security breach  
 - Traffic metadata
 - Traffic payloads
 - ARP/NDP tables
 - Routes
 - Switch port utilisation
 - Firewall logs
 - DNS entries and queries
## **Network Flow Monitoring**
A way to collect [[#Metadata]] about traffic for analysis
### Metadata
 - IP source and destination
 - Protocol(s) and port
 - Packets count and data total
### Effectiveness
Network flow monitoring can help spot anomalies with appropriate tools
 - Build a profile of good/bad traffic
 - Spot out-of-profile or known-bad traffic
Helpful after an attack for finding other compromised systems
Can also be useful for network capacity monitoring
### NetFlow
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220826205621.png|300]]
Three-component system
#### Flow exporter 
A device that records network flow it sees and forwards data to a flow collector
#### Flow collector  
Stores and pre-processes data sourced from one or more [[#Flow exporter|flow exporters]]
#### analysis  
Performs analysis and visulisation of flow data stored in a flow collector
## **Packet Capture**  
Capture all network traffic and payload data for analysis
Provides more insight but  
- Takes up a lot of space
- Processing can take a lot of resources
- Potential privacy issues
Abundance of tools for implementation
## **Monitor Location**
### Edge Monitoring  
Misses local problems
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220826210030.png|300]]
### Local Monitoring  
Generates a lot more data
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220826210046.png|300]]
## **Sniffing**
To sniff packets, you need to see them
- In packet switched networks, packets are only sent to relevant hosts
- So we monitor traffic with **Switch Mirror Ports** and **Network Taps**
## **ARP/NDP Tables**
A client access port should have one, or a small number of, MAC/EUI-64 address(es) associated with it
### Signs of Issues
- You _suddenly_ get a lot of MAC/EUI-64 addresses appearing on a single port
- You _suddenly_ get a lot of MAC/EUI-64 addresses appearing on a multiple ports
- You have _important_ MAC/EUI-64 addresses appearing where they aren't meant to be
## **Automated Monitoring Tools**
Manually looking through logs and dumps is tedious and error prone
- LibreNMS
- Zabbix
- Prometheus
- AKiPS
- PRTG
- Solarwinds
# **Intrusion Detection**
## **I**ntrusion **D**etection **S**ystem  
Automatically monitors a network for malicious activity or policy violations
Automatic notifcation/alerting of potential problems
### How [[#I ntrusion D etection S ystem|IDS]] work
Match traffic and packets against rules
- Signature database
	- Known exploits, SQL injection strings etc.
- Reputation/blacklists
- Protocol anomalies
- Traffic anomalies
#### challenges  
- False positives
	- Identifying legitimate behaviour as an attack
- False negatives
	- Failing to identify an attack
# **Intrusion Prevention**
Takes [[#I ntrusion D etection S ystem|IDS]] a step further
Automatically responds to detected problems
- Block problem traffic
- Block suspected user accounts
- Segregate compromised hosts
- Trigger an incident response process
- Increase level of network monitoring
# **[[#I ntrusion D etection S ystem|IDS]]/[[#Intrusion Prevention|IDP]] Tools**
- Snort
- Suricatta
- Zeek
# **Benefits of an [[#I ntrusion D etection S ystem|IDS]]/[[#Intrusion Prevention|IDP]]**  
- Automatically detect (and potentially prevent) attacks not stopped by other measures
- Log information, allow auditing
	- Record information about specific events
- Identify problems with security policies
- Document existing threats
- Deter violations
- Produce reports
# **Limitations of an [[#I ntrusion D etection S ystem|IDS]]/[[#Intrusion Prevention|IDP]]**  
- Configuration and maintenace
- Performance issues
- False positive/false negative balance
- Ineffective against newly published attacks
- Less effective against targeted attacks
- Can't be relied on
	- Can't compensate for holes in security
# **Darknets and Honeypots**
## **Darknets**
Using unused IP address space to monitor for unexpected network activity
## **Honeypots**
Specific decoy systems set up to allow an attack to observe and respond
- Divert attacker from the critical systems
- Collect information about the attacker and their methods
- Encourage the attacker to stay long enough to document/respond
## **Trap and Trace**
Honeypot and an alarm
# **Slides**
![[notes/Uni Content/Advanced Computer Networks/PPTXs/comp3210-Network-Monitoring-2022.pdf]]
# **Tags**
FILE TAGS: NetworkMonitoring