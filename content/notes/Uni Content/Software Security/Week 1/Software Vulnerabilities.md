---
title: Software Vulnerabilities
---
**Buffer Overflow** - We can overflow a buffer meant to manipulate data and overwrite arbitrary memory addresses, this can be used maliciously by overwriting the original program's code with our own code

# CIA Triad

**C**onfidentiality **I**ntegrity **A**vailability

![|150](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221170325.png)

Each vulnerability can harm one or more CIA properties

# Lifecycle of a Vulnerability

1. Software released from a vendor (with the unknown vulnerability)
2. Vulnerability discovered by an attacker and exploit released
3. Vulnerability discovered by vendor
4. Public dissemination of the vulnerability
5. Antiviruses start revealing the exploit
6. Patch released by the vendor
7. Exploit mitigation deployed on all affected systems

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221165336.png)
Attacks performed in the period $t_e-t_0$ are called zero-day (nobody can notice)
Attacks performed in the period $t_0-t_a$ are publicly performed
The closer an attack is performed to zero day, the higher the probability of success

# Storing and Cataloguing Vulnerabilities

**CVE** - Common Vulnerabilities and Exposures

CVE Vulnerabilities
- Identified by unique string **CVE**-**year**-**number**
- Describing page contains
	- Description
	- URL to a detailed page
	- Date of creation

## Example - Heartbleed

Bad input validation in OpenSSL

![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221170605.png)

## Example - Shellshock

Could enable an attacker to cause Bash to execute arbitrary commands
Executable remotely

Bash allows to export environment functions and variables making those available for a child shell
![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221170919.png)

An attacker with access to .bashrc can insert the following environment function
![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221170957.png)
Every time a victim opens a shell the evil_command will be executed

## Shellshock vs. Heartbleed

Heartbleed allows to steal confidential data but Shellshock can remotely execute arbitrary code

# CVSS - Common Vulnerability Scoring System

CVSS is a free and open industry standard for assessing the severity of computer system security vulnerabilities

## CVSS Score

Score assigning formula consists of 3 sets of metrics

Base Metrics
- Is it easy to exploit?
- What is the impact?
Temporal Metrics
- Is a patch available?
- Is an exploit available?
Environmental Metrics
- What are consequences on safety?
- How many systems are vulnerable?

# CWE

Used to catalogue **weakness** and **related score**

# Difference between CWE and CVE

![|600](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221171545.png)