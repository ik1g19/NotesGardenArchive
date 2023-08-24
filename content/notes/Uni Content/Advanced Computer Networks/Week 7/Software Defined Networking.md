---
title: "Software Defined Networking"
---

# **Software Defined Network** 
- A network in which the control plane is physically separate from the data plane 
 ## **Control Plane**
 ![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220817181238.png|300]]
- Computes the paths that the packets will follow
- Laymans Terms - Determines how and where packets are forwarded (needs non-local information, not fast)
 
### The Two Abstractions
- Figure out the network topology
- Configure forwarding states for the switches
 
## **Management Plane**
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220817181414.png|300]]
- Group of applications that provides functions to implement network control and operation logic 
- Sets the weights in the node graph

## **Data Plane**
- Processing and delivery of packets with local forwarding state
- Switch router looks at the packet header and the forwarding state and makes the forwarding decision
### Abstraction Layers   
#### Application Layer  
- Application and mnemonic names
#### Transport Layer  
- Reliable (or unreliable) transport
#### Network Layer  
- Best-effort global packet delivery
#### Link Layer  
- Best-effort local packet delivery
#### Physical Layer  
- Physical transfer of bits
 
##  _**SDN Motivation**_     
- Introduces abstractions/modularity to control plane
- Makes the network open and programmable 
 
##  _**Control Plane Abstractions**_  
- SDN introduces two control plane abstractions 
	- Figure out the network topology
	- Configure forwarding states for the switches

## **Network Virtualisation**
- Introduce new abstraction and new SDN layer
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220817181711.png|300]]
### Abstraction
- Virtual Topology - Allows operator to express requirements and policies   
### Layer
- Network Hypervisor
	- Implements the Virtual Topology
	- Decouples the control program from the physical network

##  _**Does SDN simplify the network?**_     
- Does not eliminate complexity 
-  Hypervisors are still complicated code 

##  _**What SDN achieves**_     
- Simplifies interface for control program
- Pushes complexity into reusable code
 
## **Planes, Layers and Architecture** 
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220817182633.png|500]]
### Management Plane
1. <mark class="pink">Network applications</mark>
### Control Plane 
2. <mark class="green">Northbound API (e.g. Java)</mark>
3. <mark class="green">Network OS</mark>
4. <mark class="green">Network Hypervisor</mark>
### Data Plane    
5. <mark class="blue">Southbound API (e.g. OpenFlow)</mark> 
6. <mark class="blue">Infrastructure</mark>

## **OpenFlow Basics**    
- Matches arbitrary bits in headers
- Performs action depending on the contents of header 
	- Forward to port(s), drop, send to controller
	- Overwrite header with mask
	- Forward at specific bit-rate

## **Virtualisation for Multi-Tenant Datacenter**    
- Want to allow each tenant to specify virtual topology 
- Which defines their individual policies and requirements 
- Hypervisor takes individual tenant virtual topologies 
- Computes configurations to implement all simultaneously  

## **SDN in Smart Grid Resilience**    
- Establish dynamic routes from a control centre to grid devices - reduces time window in which attacker can inject malicious commands
- Used to reset switches or recompute routing if compromised switches are detected
###  Security Risks
- Compromised SDN controller could issue malicious SDN control messages to undermine network performance

# **Intent Based Networking (IBN)**
- Emerging technology
- Administrators send a request to tell network what outcome they want (intent), but do not need to code and execute individual tasks manually
- Provide IBN system high level business policies and network will be automatically configured to implement them
- IBN = SDN + AI

# **SDN**
![[notes/Uni Content/Advanced Computer Networks/PPTXs/SDN.pdf]]