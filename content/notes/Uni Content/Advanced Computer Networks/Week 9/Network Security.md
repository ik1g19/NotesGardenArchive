---
title: "Network Security"
---

# **Network Attacks** 
## **Lockheed Martin's Cyber Kill Chain Model**    
- 7 stages in a cyber attack
- Not always the best tool as has steps that occur outside of your control 
	- Models such as Mandiant Cyber Attack Life Cycle focus on steps you can detect and prevent
### 1. Initial Compromise
- Aim - Execute malicious code on one or more of the target systems 

### 2. Initial Reconnaissance
- Scope out the target to identify   
	- IP addresses
	- Open ports
	- Services
	- Applications
	- Versions
	- Vulnerabilities
- Difficult to detect and protect against as {{it can blend in with normal traffic}}  
#### Reconnaissance Methods    
##### Port and Network scanning
##### Banner grabbing
##### Signature recognition
##### DNS brute forcing  
- Go looking for common subdomains to discover hosts/services 
- Can also use reverse DNS to find services
##### Dumpster diving  
- Organisations used to dispose a lot of sensitive information in normal waste
- Some corporate waste is still valuable in modern days, such as old IT equipment
##### Social engineering  
- Exploiting the human link
##### Man in the middle  
- Intercepting communications between two entities
##### Google & Shodan

### 3. Establish Foothold
- Aim - Gain some level of access/control over a target network/system 

### 4. Internal Recon
- Aim - Gain a more thorough understanding of the targets network and systems

### 5. Escalate Privileges
- Aim - Gain more control and access through increased privileges 

### 6. Move Laterally
- Aim - Gain more access to more systems 

### 7. Maintain Presence
- Aim - Establish persistent access 

### 8. Complete Mission
- Aim - Achieve overall goal 

# **Defending Against Attack**    
## **Cycle** 
- Assessment
- Protection
- Detection
- Response
 
## **Security Policies** 
- Identifies the rules and procedures for people and systems accessing a network and sets out the responsibilities of those managing the network
- Should be  
	- Organisation specific
	- Practical & enforceable
	- Regularly updated

## **User Education** 
- Train users to recognise threats
	- Phishing
	- Fake website
	- Potentially malicious downloads

## **On Going Maintenance** 
- Anything that connects to your network should be kept up to date
 
## **Regular Auditing** 
- Ensure policy exceptions are still required
- Is software/firmware acctually being updated
- Are users up to date with training
- Check network regularly
 
## **Don't Ignore Internal Threats**  
- Limit access to what is necessary
- Consider First Hop Security
- First Hop Security  
	- Defence against local/internal attacks 
	- Dealing with rogue responses (rogue DNS, DHCP, ARP, RA)
	- Key: Don't pass on un-trusted responses

## **Making use of Reputation** 
- IP/Domain reputation can help improve security
- Block or alert on access to DNS queries for  
	- IP addresses known for malware, botnets, spammers
	- Dodgy URLs, files, extensions, MIME types
- Consider {{geographic IP}} restrictions 
