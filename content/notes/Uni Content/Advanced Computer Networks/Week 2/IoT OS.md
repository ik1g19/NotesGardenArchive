---
title: "IoT OS"
---

# **Reasons to use an OS**
- Device independence
- Services
	- Timers
	- Threads
- An OS provides drivers, networking and HAL 
	- HAL↔Hardware Abstraction Layer
- ! 
# **Example OS'**
- Zephyr 
- Riot-OS
- Mbed
- OpenWSN
- tinyOS (old)
- Contiki ⇒ Contiki-NG
- FreeRTOS
- LiteOS
- Arduino
- Linux (Ubuntu Core)
- The Cloud (various Linux flavours)
# **Zephyr**
- Open source  
- Supports many boards
- Bluetooth
- Low energy
- WiFi
- 6LowPAN over 802.15.4    
- CoAP
- IPv4 and IPv6 
- Ethernet
- USB
- CAN
- Thread
# **Mbed**
- For ARM-based systems
- Has an optional RTOS
- Apache 2.0 open source 
# **Riot-OS**
- Medium sized open source project
- Low memory footprint
	- ~3kB RAM #3kB Flash
- Internet standards
- C or C++
- Can develop on Linux to start with
- Pre-emptive multi-threading
- Deterministic scheduling
- Low latency interrupts
- Supports >100 boards
- RIOT Structure
	- ! 
# **Hello World**
- TinyOS
	- ! 
- Contiki
	- ! 
- RIOT
	- ! 
# **Contiki-NG**
- Original Contiki was in use before RIOT
- Contiki-NG inherits lots of code/capabilities
- Runs on fewer boards than RIOT
	- ARM and MSP430 mainly
- Has a 6LoWPAN-CoAP stack
# **Ubuntu Core**
- More secure and reliable
	- By being minimal and transactional
	- Small
- Uses Snaps rather than debian packages
	- Snaps↔Signed sandboxed packages
- Used in commercial devices
	- Screenly
	- Nextcloud
	- Car subsystems
