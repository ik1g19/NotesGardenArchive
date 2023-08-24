---
title: "IEEE 802.15.4 and 6LoWPAN"
---

# **IEE 802.15.4** 
- Standard that covers physical specifications (PHY) and MAC for LR-WPANs
- Sits in the Network Access layer of the TCP/IP model 
- Layer 1 and Layer 2 of the OSI 7-layer model
## **Applications** 
- Wireless Sensor Networks / Environmental Sensor Networks
- Industrial communications and control
- Home automation
- Health monitoring
- Smart metering
- Asset & inventory tracking
- Intelligent agriculture

## **Alternatives and Performance** 
#### Application
- 802.15.4 - Monitoring and Control 
- Bluetooth - Device Connectivity 
- GPRS/3G - Wide-area Voice and Data
- 802.11 (WiFi) - High-speed internet    
#### Battery Life
- 802.15.4 - Years 
- Bluetooth - Weeks
- GPRS/3G - Days
- 802.11 (WiFi) - Hours    
#### Bandwidth
- 802.15.4 - '<' 250 Kbps
- Bluetooth - '<' 24 Mbps
- GPRS/3G - '<' 100 Mbps
- 802.11 (WiFi) - '<' 1300 Mbps     
#### Range
- 802.15.4 - '<' 100m
- Bluetooth - 1 - 100m
- GPRS/3G - Kilometres
- 802.11 (WiFi) - '<' 100m    
#### Advantages 
- 802.15.4 - Low power, low cost 
- Bluetooth - Ubiquity, convenience
- GPRS/3G - Range, existing infrastructure
- 802.11 (WiFi) - Speed, ubiquity    
## **Device Types** 
- PAN Coordinator - The network's overall controller   
- Coordinator - Provides synchronisation services to other devices
###  Full Function Device
- Can function as a PAN Coordinator or Coordinator
- Can associate with multiple other devices at once

###  Reduced Function Device
- Cannot function as a PAN Coordinator or Coordinator
- For very simple applications
	- e.g. Light switch or PIR sensor
- Can only associate with one FFD at a time

## **Network Topologies** 
### Star Topology    
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819175005.png|300]]
- All communications are to/from the PAN Coordinator
#### Benefits
- Home automation
- PC peripherals
- Games
- Personal healthcare

### Peer-to-Peer
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819175053.png|300]]
- All devices in range of each other can communicate directly
- Basis of Mesh networking
- Allows more complex network formations 
#### benefits  
- Industrial control/monitoring
- WSNs

## **Addressing**
- Each device has a universal 64-bit address
	- Can also have a short 16-bit address
		- Only valid within the PAN 
		- Allocated by the PAN co-ordinator at association

## **Frame Structure**  
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819175530.png|300]]
- Low complexity 
- SHR and PHR are PHY dependant
### PPDU (PHY Protocol Data Unit)
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819175612.png|300]]
#### Preamble
- Length is PHY dependent
	- O-QPSK modulation uses an 8-symbol, 4-byte preamble
	- BPSK modulation uses a 32-symbol, 4-byte preamble
	- ASK modulation uses a 2-symbol, 5-byte preamble
---
- SFD - Start of Frame Delimiter
- Len - 7-bit frame length
- PSDU - PHY Service Data Unit

### PSDU (PHY Service Data Unit)
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819175749.png|500]]
- General MAC frame format is used for data transmission
- ACK frame contains  
	- Frame control
	- Sequence number
	- CRC 
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819175815.png|200]]

###  Compared to Ethernet
#### 802.15.4 Header
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819175918.png|200]]
- Data Frame - 25 bytes + Preamble
	- When using PAN ID compression and 64 bit addresses
- ACK Frame - 7 bytes + preamble
#### Ethernet Header  
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819175957.png|300]]
- 19 bytes + Preamble

## **Example Devices/Deployment** 
- Smart lightbulbs
- Zolertia Z1
- Mountain Sensing
 
## **Higher Layers** 
### Zigbee
- Specifies Internet layer and Application layer
- Facilitates Mesh networking and Tree (multi-hop) networking
 
### WirelessHART  
- Wireless Highway Addressable Remote Transducer Protocol
- Intended for industrial wireless sensing applications 
- Mesh architecture  
	- Self-organising
	- Self-healing
	- Time-synchronised
- Specifies everything above the Network Access Layer
 
### 6LoWPAN
- IPv6 over Low power Wireless Personal Area Networks 
- Alternative to IPv4/IPv6 at the Internet layer of the TCP/IP model
- Layer 3 of the OSI 7-layer model
- Allows IPv6 packets to be sent over 802.15.4 networks 
- Extrapolates IPv6 address from 802.15.4 address if possible
- Smallest possible header is significantly smaller than full IPv6 header
	- 6LoWPAN is 2 bytes and full IPv6 is 40 bytes

## **Decoding** 
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819180147.png|350]]]]
- Need to decode the Frame Control to know the header format
### Frame Control
- 61 DC is the Frame Control
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819180241.png|350]]
- It tells us this packet
	- Is a data frame
	- Requires an ACK
	- Uses PAN ID compression
	- Is an 802.15.4 frame
	- Uses 64-bit source and destination addressing
- From this we know it has a 21 byte 802.15.4 header 
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819180316.png|350]]
- Destination address is c1 0c 00 00 00 00 0f ee
- Source address is c1 0c 00 00 00 00 10 05
### 6LoWPAN Decoding
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819180344.png|350]]
- 41 tells us that an uncompressed IPv6 header follows
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819180359.png|350]]
### Host-to-Host
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819180438.png|350]]
- The IPv6 header told us that a UDP header followed 
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819180509.png|250]]
### The Payload
- 70 bytes of header for 8 bytes of payload
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819180540.png|350]]
### The Reply
- Same 802.15.4 header, with addresses reversed
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819180607.png]]
- 6LoWPAN header is compressed to two bytes
	- First 3 bits of dispatch indicate IPHC header
	- Last 5 bits are usurped for encoding information about compression
- 30 bytes of header for 28 bytes of payload

## **RPL**  
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819180652.png|500]]
- Routing Protocol for Low-Power and Lossy Networks
- Works out routing over Mesh networks
- Allows for multi-hop networks
- Create tree-like topologies
	- Destination-oriented directed Acyclic Graphs (DODAGs)
- Each node is assigned a distance-dependant rank
- Uses ICMPv6 for control messages