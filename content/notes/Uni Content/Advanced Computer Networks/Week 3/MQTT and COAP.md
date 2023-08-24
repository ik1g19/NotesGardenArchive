---
title: "MQTT and COAP"
---

# **MQTT**
    - By IBM in 90s
    - ! 
    - Designed to be smaller packets and less overhead than HTTP
    - Messages are published to a broker
    - Clients subscribe to data streams
    - MQTT topics are hierarchical 
    - Example JSON message over MQTT
        - ! 

# **Constrained Application Protocol**
**Efficient in low power IoT systems  **
## **RESTful - Makes interoperability with the web simple**
## **Features** 
	- More modern lightweight design than MQTT
	- Prefers UDP 
	- Binary format for protocol
	- DTLS security option
	- Block transfers
	- Resource discovery
	- Push notification
	- Cache model
	- Multicast support

## **CoAP Header**
	- ! 
		- V→Version
		- T→Type
		- Tkl→Token length
		- Code→Method (1-10) e.g. GET, or response code (40-255) like HTTP
		- ID→Helps match messages
		- Token→Used to match responses
		- Option→Can mean payload is a URL string
		- Payload→Can be anything
## ****
## ** _**Options Header**_   **
	- ! 
	- Defines the content type
## ****
## ** _**Request Examples**_  **
	- ! 
	- Note response can ACK and contain the payload
## ****
## ** _**Confirmable Bit Deals with Packet Loss**_  **
	- ! 
	- Client wanted an ACK so resends a last request
	- Note use of message ID to keep track of responses
## ****
## ** _**Slow Responses**_  **
	- ! 
	- So ACK can be given immediately, then the payload later
## ****
## ** _**CoAP Proxy/Cache**_  **
	- ! 
	- Allows nodes to sleep and the proxy can reply with cached values
## ****
## ** _**Observation**_  **
	- ! 
	- Nodes can push updated values
## ****
## ** _**Block Transfers**_  **
	- ! 
	- Larger data blocks can be sent in chunks and re-built at the client
	- Don't forget this is UDP so it is fast but packets can be lost
## ****
## ****Resource Discovery** **
	- GET .well-known/core  
		- Provides a CoRE  description of the resources on the node
		- ! 
	-  _**CoRE**_  
		- (Link Format) is a standard for defining resources
		- So IoT objects can be added and their resources discovered automatically
		- For example, nodes can POST their CoRE data to a resource discovery and can update it with a PUT or DELETE
## ****
## ****Multicast**  **
	- !
	- Can multicast queries to multiple devices
## ****
## ** _**Using CoAP**_  **
	- Coapthon3  
		- Python library
		- Lets you run a server
		- And send messages with a client example
	- LibCoap  
		- C library
		- Has a command line coap-client that's useful
## ****
## ** _**Tradfri**_  **
	- Can test CoAP with IKEA Tradfri devices
