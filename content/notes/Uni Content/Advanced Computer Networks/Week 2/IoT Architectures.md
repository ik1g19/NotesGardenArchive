---
title: "IoT Architectures"
---

# **Typical IoT Hardware Elements**  

- PSU
- MCU
- Coms
- Power Source
- I/O
- Storage
- Sensors
- Actuators
- Switched Mode Regulator
- Battery
- Radio Transceiver
- Flash
# **Hardware Architecture** 

- A lot depends on which MCU family is chosen
- System on Chip is commonly used
	- System on Chip - Has a microcontroller on board and a radio
- ESP8266 based systems include WiFi and Bluetooth
# **Internet Connected Things**

- Many systems need a gateway 
	- Communications hub, border-router or gateways link low power hardware to the outside world
	- Gateway is often more powerful Linux-based hardware
	- Things may not use IP
		- e.g. LoRaWAN, BTIe 
# **Basic Software Elements** 

- OS/Drivers 
	- Operating System or Bare-Metal
	- Hardware Abstraction Layer
	- Networking
	- Security/Encryption
	- I/O interfaces
	- Sensor drivers
	- Timers, RTC functions
	- Power supply functions
- Objects 
	- Object behaviour code
	- Coms/Network Stack
	- Data Storage
	- Power Management
- Fog/Edge 
	- Data processing and/or Decision making in the node, border/edge node or Cloud
	- Edge node can be the border to the  main internet and provide data services
	- Cache is common to reduce traffic to the objects
- Network 
	- Internet/GSM/communications network
	- Can be IP based
	- Security mechanisms
- Cloud 
	- User interface
	- Data storage
	- Data processing/analytics
	- Access mechanisms
#  Networks

- WiFi/Ethernet
- Low Power Wide Area Networks
- Low Power IPv6 Networks
- Stars
- Meshes
# Data Protocols

- Describes the data and mechanisms
	- e.g. RESTfull
- Systems need to use a data protocol regardless of the type of network 
