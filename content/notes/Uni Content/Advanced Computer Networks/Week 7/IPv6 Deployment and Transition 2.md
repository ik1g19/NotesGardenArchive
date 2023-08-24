---
title: "IPv6 Deployment and Transition 2"
---

# **Tunnelling**    
- The encapsulation of IPv6 packets in IPv4 packets between two destinations

## **6in4**    
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220817184232.png|300]]
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220817184249.png|300]]
- IPv6 packet with a IPv4 header in front
- Can be difficult to forward   

## **Teredo**    
- Encapsulates IPv6 in IPv4 UDP packets
- Operates without cooperation of the local network 
- Can only provide a single IPv6 address per tunnel endpoint
- Uses servers and relays
### Servers    
- Set up the connection
- Detects NAT configuration 
- Helps establish a connection between a Teredo client & relay 
- Is what the client talks to to keep the connection alive 
### Relays    
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220817184524.png|500]]
- Forward traffic between IPv6 hosts and the Teredo client
1. ICMPv6 Echo Client > Destination Server
2. Server forwards ICMPv6 echo to destination
3. Destination replies to nearest Teredo relay
4. Relay sends Teredo 'bubble' to Server
5. Server forwards Teredo bubble to client
6. Client sends bubble back to Relay (thus establishing a connection to the relay)
7. Relay forwards ICMP reply to Client
8. Client can then start communicating with Destination via Relay

## **VPNs**    
- Can be configured to tunnel IPv4 and IPv6 using TCP or UDP 
	- IPv6 over an IPv4 network
	- IPv4 over an IPv6 network
- Encryption overhead 

## **NAT64**    
- IPv4 addresses embedded in a specific IPv6 prefix
- Last 32-bits taken as the IPv4 address
- 152.78.118.51 becomes 64:ff9b: :152.78.118.51 
- NAT64 gateway translates packets with the prefix to IPv4 
- Limits connections to a client-server model using UDP, TCP and ICMP 
 
## **DNS64**    
- DNS server synthesises a AAAA (IPv6) record for a domain that only has A (IPv4) records
- Combine with NAT64 for a whole solution   
 
## **NAT64/DNS64** 
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220817184645.png|400]]   

## **464XLAT**    
- Limited IPv4 connectivity across an IPv6-only network 
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220817184745.png|400]]
- Uses two translators
### **C**ustomer-side Trans**lat**or (**CLAT**)    
- Converts IPv4 to IPv6 
- Stateless
### **P**rovider-side Trans**lat**or (**PLAT**)    
- Converts IPv6 to IPv4 
- Stateful

## **Dual-Stack Lite (DS-Lite)**    
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220817185050.png]]
- Allows service providers to migrate to an IPv6 access network without changing IPv4 end-user software
- IPv4 tunnelled and transmitted over an IPv6 tunnel
- Tunnelled IPv6 is decapsulated and undergoes private-public IPv4 translations by NAT
- Encapsulation can run directly on a client device 
- Common deployment is to run DS-Lite to the **C**ustomer-**P**remises **E**quipment router