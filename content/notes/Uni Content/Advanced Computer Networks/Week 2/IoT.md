---
title: "IoT"
---

# **The Internet of Things** 
- Ubiquitous computing with a focus on objects
- Computing being distributed into the environment and physical objects

# **IoT Challenges**
##  _**Standardisation**_  
- Fragmented implementations between associations, standard bodies and governments

##  _**Big Data**_   
- IoT devices generate a lot of data
- How to choose which data to keep
- Balance of storing data vs analysing data and discarding
- How does this affect data centers and server technology

##  _**Data Security**_   
- Certification and regulation needed for technology, especially when health related
- Consumers need to be convinced their data is safe from misuse or theft
- IoT devices are generally unattended, easy to physically attack and easy to eavesdrop on
- Limited energy/computing capabilities for encryption

##  _**Connectivity**_  
- Security
	- How to encrypt traffic
	- How to ensure ports aren't vulnerable
- Power
	- IoT devices need to last as long as possible on as little battery as possible
- Reliability
	- What happens if there is no WiFi, LPWAN or cellular coverage

# **Communication Choices**  
- WiFi
- Bluetooth
- Zigbee
- 6LowPAN over 802.15.4
- Sigfox
- NB-IoT
- LoRaWAN
 
# **Architecture of Embedded IoT** 
##  _**Hardware**_ 
- Sensors
- Actuators
- Cameras
- Motors
- Power Supplies
 
##  _**Embedded Software**_ 
- Bare to Metal
- Operating Systems
- Drivers
 
##  _**Coms and Networks**_ 
- Point-point
- Mesh
- Range
- Bandwidth
- Power use
 
##  _**Cloud or Server**_ 
- Messaging
- Web services
- Linking
- Data
- Analytics
 
##  _**Applications**_  
- Web
- Android/iOS
- User Experience

# **WiFi**
#### Advantages
- Integrate with home networks easily
- Bandwidth and security 
 
#### Disadvantages
- Higher power 
 
# **Bluetooth**
#### Advantages
- Available on phones/tablets/laptops 
- On some existing devices like speakers etc
 
#### Disadvantage
- Short range
 
# **Zigbee**
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220818185648.png|300]]
- Protocol over 802.15.4 layer at 2.4GHz/868/915
- Payload up to 104 bytes 
- Uses mesh networking  
####  Advantages
- Scalable mesh networking
- Long battery life
#### Disadvantages
- Short range
- Payload sizes are 104 bytes, low transmission 

# **6LowPAN over 802.15.4**
#### Advantages     
- Supports IPv6
- Range 10-100m
- Excellent integration with the internet 
- Gains IPv6 characteristics
- Mesh networking
- Can use 2.4GHz or 868/900MHz bands
 
#### Disadvantages
- Needs a gateway/hub to LANWAN
- Less immunity to interference than WiFi

# **Narrow Band-IoT**
- Cellular 
- 700MHz, 800MHz, 900MHz
- 200 kbps approx
- Promises wide coverage
 
# **Sigfox**    
- Ultra Narrow Band cellular
- 868/915Mhz
- Low Power, Less than 25mW
- 100 bits per second i.e. slow 
- Range ~3-30km 
- Limited messaging per day
- Data package provided by operator
- Up to 140 messages per day
- Payload is only 12 bytes 
- Can transmit 4 messages of 8 bytes to the device each day

# **LoRaWAN**
![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220818190412.png|300]]
- Wide area low power network using gateways
- Gateways link together
#### Advantages
- Lots of security mechanisms 
- SS chirp modulation very robust

#### Disadvantages
- Up to 50 kbps, uses ISM 868/915MHz bands
- Payload limited to 100 bytes 
 
# **Global System for Mobile Communications**
- Standard to describe the protocols for digital cellular networks used by mobile devices
#### Advantages
- Existing architecture deployed over the world
- Maintenance is easier due to large number of network engineers at affordable costs
#### Disadvantages
- Existing GSM architecture is patented and requires a license
- Interference due to FTDMA
 
# **Handling Data** 
## **The Things Network**
- Trying to pull together IoT devices to allow intercommunication and IFTT type rules running locally
- To maintain privacy, data and decision making should operate locally within the home
- Mainly for LoRaWAN 

## **MQTT**  
- IBM/cars lightweight communication protocol for IoT devices
- Publish/subscribe
- Tend to use a message broker like mosquitto
- "Topics" published to broker which others can publish/subscribe
 
## **xively.com**  
- Data storage and visualisation
 
## **HyperCat**  
- A hypermedia catalogue format designed for exposing information about IoT assets on the web 
 
## **IBM Bluemix**  
- Cloud platform
- MQTT upload from devices
- Gains lots of analytics from IBM cloud 
