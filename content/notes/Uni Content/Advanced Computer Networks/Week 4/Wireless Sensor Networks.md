---
title: "Wireless Sensor Networks"
---

# **Wireless Sensor Networks**  
- Autonomous networks of low-power wireless sensors
## **Examples**  
### Berkeley & Intel bird nest monitoring

![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220818192228.png|300]]

- Via small sensor nodes

### Volcano monitoring

![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220818192405.png|300]]

- Cheap, small sensors used by Harvard in Equador

### Agriculture

![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220818192530.png|300]]

### Geo-sensors for monitoring forests

![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220818192625.png|300]]

### Argo Floats

![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220818192714.png|300]]

- Communicate data via satellite
- Typical lifetime is 150 cycles/4-5 years 
 
# **Power-Aware Routing**    
- WSNs spread routing around to prevent overloading one node
- Other considerations 
	- TX vs RX power use
	- Start-up time from sleep/off (typically ms)
	- Media Access Control (MAC) in dense nets
	- "Overhearing" wastes power
	- Single point of failure with one base station/sink
 
# **Listen-Sleep Media Access Protocols** 
## **Typical MAC Protocol**

![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220818192851.png|400]]

- May need synchronisation
- Can sometimes use a low-power preamble listen
 
# **Multi-hop Routing** 

![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220818193516.png|400]]

- Power required to transmit in a single hop 
	- $E_{\text{single-hop}}(k,d)=kE_{elec}+k(nd)^2E_{amp}$ 
- Power required to transmit in  **n**  short hops 
	- $E_{\text{multi-hop}}=n(kE_{elec}+kd^2E_{amp})+(n-1)kE_{elec}$
	-  **n**  transmits and  **n-1**  receives
- Basic principle is {{large amount of power to do massive range}} vs {{everyone suffering power drain to pass packets on}}     
 
# **Low-Energy Adaptive Clustering Hierarchy (LEACH)** 

![[notes/Uni Content/Advanced Computer Networks/Images/Pasted image 20220818193557.png|400]]

- Sometimes single-hop will be better than multi-hop and vice versa
- We have only considered total energy
- Form clusters of sensors around local temporary cluster-heads
 
# **Environmental Sensor Networks**

- Comprises an array of sensor nodes and a communications system which allows their data to reach a server

## **Properties** 

- Enable data that would previously be impossible to collect to be gathered
- Send data regularly without human intervention
- Typically wireless
- Battery powered

### May have 
- Solar
- Wind generation
- Other energy harvesting

#### Kirk Stuff
- Glacsweb Probes
	- 173 MHz radio transceiver
	- Senors
		- Temp
		- Pressure
		- Strain
		- Conductivity
		- Accelerometer
	- GWpacket and protocols
- IoT and Standards
	- Emerging standards mean IP can be used everywhere
		- Application
			- CoAP - Data
			- UDP - Transport
			- RPL - Routing
			- 6LowPAN - Network
			- IEEE 802.15.4 - Data Link
			- 868 MHz - Physical Layer 
- ![](local://C:/Users/isaac/remnote/remnote-615c4b5e9f997400356d29fa/files/Q21pTQitJ36F2YtKrEWkTfJ9Z7TPAXnOO8qjUZ2wfAN4AgzGVDwJdvJ9f53Wo6XGlO9OVBOeD4MLJHRommWA1LF24hahkWVv3ikJ1ApUWzgipVA28SAEGZHq_pIWW6p5.png) 
	- Code in the estate GETs the data from each node
	- In the previous version nodes POSTed their data
- Communication
	- Always on
	- Gateway tries to pull every hour LMAO
	- Each node has a global IPv6address
	- Can be pinged to check if connected
	- ![](local://C:/Users/isaac/remnote/remnote-615c4b5e9f997400356d29fa/files/7kkS9DkhWyDDhXbSa8f6HHPKr_lRprRD2tu2_AOTfSdfKr3aFp826HTZCQ9DNwtNPvxtb7o4n6VAwIKgtsJi8Q6FuhGzVyLI4TjrdxYzp3sEnuB_XvsyNwyE4bXqGLw3.png) 
- CoAP
	- Like a binary HTTP/web-protocol
	- Uses UDP packets - less network traffic
	- Low power
	- Nodes can reply to URI requests
		- ![](local://C:/Users/isaac/remnote/remnote-615c4b5e9f997400356d29fa/files/XnH69LRhZC1DemAi_B9uFLRcs3LnqQMXKozLESpj-Mun_fNGHwPgErnMRzzFfPtroDoHVQYDgqSMNnXWL2VnR2aauNWYZ-ze7Ck2LlhNlT52gJGtVe4audwjoKb1f2n0.png)
	- Can be used to discover what nodes can do
		- ![](local://C:/Users/isaac/remnote/remnote-615c4b5e9f997400356d29fa/files/TbjZFTvyAv7EENbMKgn-Em4y3gzqGk0wJeIaC4uxrbl-RPK-NpZ4tQYCpoRta_lnJvgtj06OY1_ztkJ5YWUCfTFPIaM96NFoxFRLnDE6lBAaiz9hdnqcm3jckHQP2NPI.png) 
- Gateway/Border Router
	- Mini ITX running Ubuntu
	- Nodes connected over USB
	- Estate's satellite ISP
	- SIXXS Iv6 tunnel
 
# **Published Sensor Networks** 
## **Oxford Flood Network**
- LoRaWAN
- Integrates with The Things Network
- Uses small, low-cost ultrasound sensors to detect water surface
- NB wireless is used to link the sensors to a local communications hub
- Data is aggregated and sent over TV white space

## **Calderdale Flood Project**
- Nodes communicate with LoRaWAN gateways over LP wireless 
- Gateways forward packets over UDP to a message broker 
- Data is then stored in a DB

## **Mountainsensing**
- 6LoWPAN
- Each node has unique IPv6 address
- Estate system GETs data from each sensor node using Constrained Application Protocol
- Estate uses IPv6 tunnel and sat links to communicate to server

## **Fresh Water Real-Time Monitoring** 
- Sensor nodes installed randomly
- Sensor devices connected to Coordinator Device using multi-hop data transfer
- Data then sent to remote data base server through commercial GSM provider networks