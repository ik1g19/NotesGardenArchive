---
title: "IPv6 Deployment and Transition"
---

# **Carrier-Grade NAT**  
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220818191613.png|300]]
- ISP subnet becomes a large private network
- Home routers are assigned private IPs
- Amount of required public addresses is reduced as well as cost
- Does not actually solve IPv4 exhaustion

# **Motivation for IPv6**  
- IPv4 exhaustion
- Direct addressability
	- End-to-end global addressing as intended
	- No more NAT
- Less complex networks
 
# **What is needed for IPv6 Deployment**  
- IPv6 address space
- IPv6 routing
- IPv6 firewalling
- DNS that serves IPv6
- IPv6 address allocation mechanism
 
# **DHCPv6**    
- Provides a managed way to allocate IPv6 addresses
	- And other information (search domain, tftp server)
- Prefix delegation makes automated sub-allocation of IPv6 address space possible

##  _**DHCPv6 Interaction**_  
- Client sends a SOLICIT over multicast
- Server responds with an ADVERTISEment of an address directly to the client
- Client sends a REQUEST for the advertised address over multicast
- Server sends a REPLY confirming the address allocation
 
##  _**DUIDs**_   
- Used to identify a host to the DHCPv6 server
	- In IPv4, this was traditionally the MAC address
- What about for
	- Dual-stack systems - Different IDs for IPv4 and IPv6
	- Dual-boot systems - Different DUIDs
	- OS reinstall - New DUID

# **Dual Stack Deployment**    
- Running both IPv4 and IPv6 protocols on the same equipment
- Devices have both IPv4 and IPv6 addresses
- Need to secure (e.g. firewall) both protocols
##  _**Applications in Dual Stack Environments**_     
- DNS returns IPv6 and IPv4 records
- Applications "choose" when to use IPv4 or IPv6 
	- Current preference is IPv6 if available
- Applications need to support IPv6 
 
##  _**Disadvantages**_     
- Essentially have two networks running in tandem 
- Potentially more issues to troubleshoot
- Double the IP configuration
- Overhead for DHCP, firewall, etc
- More hardware usage
- Doesn't actually free up IPv4 address space 
 
# **IPv6 Deployment Strategy** 
- Develop comprehensive address plan
- Is it possible to do an initial IPv6 deployment at the same time as a network upgrade
	- Reduced cost
##  _**Optimal deployment order**_   
- Start with IPv6 from ISP to your firewall
- Roll out some test nets
- IPv6 enable public-facing services
- IPv6 enable client devices
 
# **Case Study: Imperial College**  
- Have IPv6 support almost everywhere
##  _**Slow Process**_   
- 2003 - Started experimenting
- 2006 - Routers IPv6 enabled
- 2010 - Deployment to clients started
- 2011 - Server and service deployments
- 2013 - WiFi IPv6 enabled
- 2018 - Guest network IPv6 enabled
 
##  _**Deployment Decisions**_   
- Dual-stack
	- No case for IPv6 only at the time
	- Looking at IPv6-only going forward
- SLAAC rather than DHCPv6
	- DHCPv6 was not well supported when started
- Parity
	- Same network, same paths, same upstream
- Whole network
	- Same network provision everywhere
 
##  _**Deployment Drivers**_   
- eScience/HEP/CERN are moving to IPv6
	- Encouraged other HE institutions to deploy IPv6
- Imperial were going to run out of IPv4
- Do right and early for a low cost
- Preparing for surprise research requirements
- Didn't want to be last to implement
 
# **Case Study: Microsoft IT**  
- Had dual-stack in labs since 2011
- Push in retrofit in 2016 to put IPv6 everywhere
- Looking to move to IPv6 only but keep hitting roadblocks in IPv6 support
