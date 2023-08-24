---
title: "IEEE 802.11_ Wi-Fi"
---

# **IEE 802.11**   
- Set of standards that cover physical specifications (PHY) and MAC for Wireless Local Area Networks (WLANs)
- Intended to be a replacement for wired Ethernet 
- Sits in the Network Access layer of the TCP/IP model
## **History**
#### 802.11a 
- 1999
- 1.4Mb/s at 5.4GHz 
- [[#OFDM]]
#### 802.11b 
- 1999
- 11Mb/s at 2.4GHz
- [[#DSSS]]
#### 802.11g 
- 2003
- 54Mb/s at 2.4GHz
- [[#OFDM]]
#### 802.11n 
- 2009
- 600Mb/s at 5GHz
- [[#MIMO]], [[#OFDM]]
#### 802.11ac 
- 2013
- 1733Mb/s at 5GHz
- [[#Mu-MIMO]], [[#OFDM]]
#### 802.11ax 
- 2021
- 2402Mb/s at 5GHz
- [[#Mu-MIMO]], [[#OFDMA]]
- High efficiency wireless
- Improved efficiency in dense environments, e.g. lots of people streaming
### How has Wi-Fi Improved
- Better modulation and spectrum usage
	- DSSS to OFDM
- Wider channels
- Better spatial performance
- Better digital modulation 
	- From , Quadrature Phase Shift Keying and 16/64 Quadrature Amplitude Modulation (802.11g)
	- To 256-QAM (802.11ac) and 1024-QAM (802.11ax)
## **DSSS** 
- **D**irect **S**equence **S**pread **S**pectrum
- Send a wide wave continuously - may lose some of it
- Spread across the frequency domain
- Redundant bits of data (chips) added to the representation of 0's and 1's
	- Spreading ratio↔Ratio of chips to data
		- More chips means more immune to interference 
- 1 to 2 Mbps
### HR-DSSS  
- High-Rate Direct Sequence Spread Spectrum
- Allowed 5.5 and 11 Mbps 
## **FDM**  
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819181453.png|400]]
- Frequency Division Multiplexing
- Multiple transmitters transmit over multiple frequencies simultaneously
- Guard bans are used between each frequency to avoid signal overlap 
## **OFDM** 
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819181532.png|300]]
- Orthogonal Frequency Division Multiplexing
- Data transmitted in parallel on multiple carriers 
- Carriers can be densely packed, saving bandwidth
- Adding Orthogonalisms 
- Sub-carriers are orthogonal to each other
	- The peak of one subcarrier coincides with with the null of an adjacent subcarrier
## **Comparing DSSS and OFDM**
#### DSSS 
- Uses the entire allocated frequency
- Lower in throughput
#### OFDM    
- Sends the signal using multiple frequencies
- Allows for a higher data rate
#### OFDM is better
- Which is why 802.11a and 802.11g were faster than 802.11b
## **OFDMA**  
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220819181715.png|350]]
- OFDM with Multiple Access
- Allows us to send traffic to multiple clients per stream 
- Not every packet of data being sent or received will consume the entire available bandwidth 
- Separating slices of time and sub-channels between users
- Increased efficiency for short data frames
## **Beamforming**  
- Focus RF towards a client
- Targets medium range 
- Introduce in 802.11n 
#### Process  
- Announcement
- NDP
	- Null Data Packet
- Measurements returned
- Beamforming
## **MIMO** 
- Multiple-Input and Multiple-Output
- Single pair of devices can send/receive multiple data streams with different coding 
#### Mu-MIMO 
- Multi-user MIMO
- Parallelises for multiple clients in the spatial domain 
# **Wi-Fi**
- Wi-Fi lacks mechanisms to mitigate interference
## **Multiple Access**
### Ethernet  
#### CSMA/CD  
- Carrier Sense Multiple Access/Collision Detection
- If a collision occurs, detect it, terminate it, retransmit
- Much less of a concern in switched networks
### Wi-Fi  
#### CSMA/CA  
- Carrier Sense Multiple Access/Collision Avoidance
- Reduce the possibility of collisions in the first place
- Make sure the channel is clear before sending a packet
- Or wait and try again
## **2.4 GHz**  
- Crowded space
- Three non-overlapping 22 MHz channels (802.11b)
- Two 40MHz channels (802.11n)
## **5 GHz**  
- More bandwidth
- Has worse penetration than 2.4 GHz
## **DFS**  
- Dynamic Frequency Selection
- Avoids interference with radar by listening for radar activity and avoiding occupied channels
- Adds cost and complexity
- Slows down initial boot on relevant channels
- Susceptible to false triggers that boot users off channels
## **802.11ad**  
- Operates on 60 GHz
- Useful for very local networking
- Wireless displays
## **802.11ay**  
- Development on 802.11ad
- Operates on 60 GHz 
## **Target Wake Time**
- Wi-Fi is not battery friendly
- In the old method (802.11b)    
	- Clients sleep between AP beacons
- In the new method (from 802.11ah)   
	- Client and AP negotiate when a client can access the spectrum
	- Clients can sleep more
# **Tags**
FILE TAGS: 802.11_WiFi