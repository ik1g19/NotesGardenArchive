# Dockers
## Setting up a new Project
Suitable for backend
- nodeJS
- express API

DB
- MongoDB

Frontend
- Apache

## Docker vs Hypervisors
Hypervisors are mostly used to virtualise development

Dockers are mostly used to virtualise deployment

Dockers are small linux code
- They require some kind of operating system which can support a docker daemon

On top of this are the containers, which are a combination of the application and the libraries that the application needs

![|400](https://remnote-user-data.s3.amazonaws.com/jk2VlZNAUThsyyAyXhI4TN1x9VSB3QiEXneoUc1GG-sDZBhMWTAsbfRV_p2WPc79Ov09QaWvjjKsosZGJz6K3yMnfxaXlN0fsCnvxI_RuWRmyEtthEeEzLy-QUPiRbdc.png) 

## How Dockers Work
Both containers are run for frontend and backend

![|400](https://remnote-user-data.s3.amazonaws.com/sh7wDQ2GXuv-6t8yK3HMvqaDvums11KEpP3SJI-h1ksrWHlQ8sx75hoNDhgEDWwNKSzbcGwpV6L55-L04iYz8UpbZT93yuirhwqt3gvLi9NCDfvTztxW2kW7kQ5R8Zb_.png) 

## Container Contains
- Networking
- Processes
- Dependencies
- Code
- Config
 
## Service Delivery Platform

![|400](https://remnote-user-data.s3.amazonaws.com/MTphwWV8AuHmylEz2HsRkq6P2ySy6mK7dVJthH6CGwQupb-N4UKqPRiDJXRzwb4Oc2OU-dgkRRjMIF2uso8u6IZoh5JPycE_alZKGdwEHzMNn7d7zHK9ByX6EKXC6t01.png) 

The orchestration helps manage a large number of docker containers at once
 
## With One Container
- Help dockers discover each other and other services
- Allocate resources
- You can start, stop and restart containers if they fail
 
## Docker Vulnerabilities
### Software Vulnerability
Container Escape - The attacker gains full control of the host and can try to attack resources in the internal network segment
- This can allow the attacker to deploy a malicious container inside the production environment

# Yet More Vulnerabilities
## The Basics of Mapping
When you have an application to test, you need to understand it
- Where does it take user input
- What features are present
- What pages does it have
- What forms does it have
 
## Different Forms of Input
- URL Parameter - User-filled parameter that is part of the URL itself but not a GET parameter
	- e.g. /groups/studentscoutsandguides/
- GET Parameter - After the ? in the URL, a key - value pair
	- e.g. /search?q=Scouts
- POST Data - Form fields which are submitted with name - value pairs

## Manipulating EXIF
exiftool allows you to manipulate EXIF data in images
- Allows us to embed code in an image while leaving it a valid image
 
## Cross-Site Request Forgery
Tricking your browser into doing something you didn't intend to do

Your browser sends your session whenever it makes a request to that website
- Even if the request comes from another website

What you're looking for
- The absence of CSRF tokens in forms
- Insecure GET actions
- GET-based actions
- Unprotected forms

### Same Site Cookie Policy
Allows you to decide when setting a cookie whether it should be sent when the request originates from another site

But not entirely
- The Lax default still allows GET requests from following a link

Means CSRF is not a prominent threat

The new standard is that the default is restricted

Made the majority of CSRF disappear 

## Server-Side Request Forgery
The server may be on the inside of the network

The server can access internal resources

Getting the server to make a request
- Or something that connects to another site
- For example, via an API call
 
## Internal Information Exposure
Error reporting, debug information, unexpected behaviours

How does the application and framework handle error reporting?

How does the application handle unexpected errors and faults?

You are trying to create those faults, situations and errors
 
## Information leakage
Doing something unexpected can lead to details about the server or database

The attacker needs information
- The more information, the easier the attack

NVD contains all the vulnerabilities for all the different software versions
 
## Finding Leftover Files
Look for variations

Look for common files with common names
- e.g. testing, phpinfo, info, debug
 
## Parameter Manipulation
What inputs are you able to find

What types are you able to find

What happens when you give invalid types

What happens when you miss out information

What happens when you give invalid information

Client-side validation is insufficient
- A client can send any response it wants to the server, regardless of client-side validation
### Techniques
- Leaving out input all together
- Adding decimals
- Out of range
- Executing commands
- Adding new parameters
- Overflowing the input
- Injection
- Different data types

## Application Logic
Similar to Parameter manipulation

Breaking the application logic

Look for
- Multiple-step processes
- User input processing, not just queried/stored
 
## Out of Date Software
Running old software that has vulnerabilities

Look for
- Out of date components or underlying software
- Out of date software
- Signs of the software being used
- Signs of the version being used
- Vulnerabilities in the version that can be exploited remotely

### National Vulnerability Database
- Database of known vulnerabilities in software
- Searchable
- CVE Numbers - Unique identifiers for vulnerabilities
 
## File Inclusion
### Good file to aim for
passwd contains local usernames

On Linux systems calling ../ at the root directory does nothing so you can add as many as you want

Are there any places where a file is dynamically included by the URL

Looking for
- Places where files from the file system are included, based on user input

Can you change what is included to something you shouldn't

Look in 'Network' section of developer panel to find included external resources
 
## Open Redirects
Can recognise a redirect by looking for 3xx status codes

Can recognise a redirect with input by looking at the request

Look for redirects in the application which pass the redirect through the URL
 
 
# Virtual Machines
## Virtualization Types
- Hardware virtualization
- Server virtualization
- Storage virtualization
- Software virtualization
- OS virtualization
 
## Virtualization Tools

![|400](https://remnote-user-data.s3.amazonaws.com/-_lLtrTjN9lETsTbakNKWtYSPdazwUaf3L-o8uQNGw0Qo02HAnA6aDTmHP-TQ9DS6WgEX3FEWJs1uGxf7aV7qnQvfBW3MxLweN1lvfEBGaohGDDFWRJ_tO12fTQROPBl.png) 
 
## Hypervisors

![|400](https://remnote-user-data.s3.amazonaws.com/2QydkWvpDvayTOH8---wy7_akZfe3wHBtcTGkgWYbKW8crgMifOrCwwJE9c_f_odjOXsU3Gfn6aOqzafBZ7HlDwcux4L6ZcdCyOws2zNw1zuMBneN7FF_IPpMYZejgYg.png)

![|400](https://remnote-user-data.s3.amazonaws.com/BS7vqjvMrILRv8H3-3mSRcP8Xo02crzCoXGcCiYAeBOG-0EKGAxuRzDviwB3aa-SDYLGOxInxDTqr9-3ZuRdIc-EiLj6i0lcLBSUPzbTWx80EK8XSLRDAZFHcYeAHklU.png)

Capable hardware can virtualize many instances at once

Hypervisor virtualizes the hardware to install an OS and then an application
 
## Workstation Hypervisors
VMWare
- Commercial
VirtualBox
- Open Source
 
## Enterprise Hypervisors
Such as VMWare

Will often provide GUI for additional support

![|400](https://remnote-user-data.s3.amazonaws.com/6ug83LICKb31E47eU4zSFxGPrwZZrsmYTrxvy_QNxNzLn991nczBgOkL2D8BRK42Np-Xjc5PNk1WckpjbwKm1JMtbKySx8rBe90hY2e5RK9uDxvRKGqaTueXFvVvg6BH.png) 

## Hypervisors - Pass-Through

![|400](https://remnote-user-data.s3.amazonaws.com/f26BggGHvfAHHKb2tUdjbOK_P5qO_sOQNs7eoIqbcQhi4snTxnMSHYbzCwzbQ3Ff1zmcjNcCrFxTy60CNx2qYN-ChUXYcsdOeEPOo0WZpV9PFwdnoP_efFnxixfsvnl9.png) 

You can pass through actual hardware to a virtual machine
- e.g. A GPU
 
## Virtual Machine Vulnerabilities
- Virtual Machine Escape - The process of a program breaking out of a virtual machine and interacting with the host operating system
- Hyperjacking - Involves installing a malicious, fake hypervisor that can manage the entire server system
- Meltdown - Instead of attacking the hypervisor, you go from one instance of a virtual machine into another, bypassing the hypervisor and getting into the hardware
	- Breaks the most fundamental isolation between user applications and the operating system. The attack allows a program to access the memory of other programs on the operating system
- Spectre - Breaks the isolation between different applications. Allows an attacker to trick error-free programs, which follow best practises, into leaking information. Safety checks of these best practises increase the attack surface and may make applications more susceptible to Spectre

# Infrastructure as Code
 
## DevOps
### Development
- Developers
- Quality assurance
- Front end

### Operations
- Database admins
- Network admins
- System admins
 
## Combining Operations and Development

![|400](https://remnote-user-data.s3.amazonaws.com/2h1mhM8VRD5EfzUCNTgpYGRwmMLLAKAZrhqxBwGcqGXdNApgR4b11LhES7glKoLMDqPwkp3TyyEJbkYfPkKViPoKT_-hoOYtAb651CUz4_vTV5R85lDhvN2qylKLwDKU.png) 

## Infrastructure Creation
### Automatically Provisioned vs Manually Provisioned 
Reduction in adding new bugs vs Introduces new bugs 

You can change it easily vs You cannot change it easily 

Infrastructure can be relocated vs Infrastructure can not be relocated 

Infrastructure is written using a high-level programming language vs Infrastructure is written using an operations manual 

One employee can manage a big infrastructure vs A team may be needed to manage a small infrastructure 

Infrastructure is designed using code vs Infrastructure is designed using graphs 

Infrastructure can be tested and review like code vs Infrastructure can be tested and reviewed  after deployment 

Development speed increases vs Slows development speed 

You can repeat it exactly vs You cannot repeat it exactly 


Artifact - What gets versioned, tested and deployed

Procedures (ala Imperative) -  An approach where the commands to produce a desired state are defined and executed 
- e.g. Bash script

Functions (aka Declarative) - Where you define the desired state and the tool conforms the system to the model of your desired state
- e.g. SQL queries, makefiles
 
## Service Delivery Platform
### Application

![|400](https://remnote-user-data.s3.amazonaws.com/-3NxAkOn7x79xIH8WiSmbj-y28Esakir9-y_892RZRu84KNCrwzsD7T_5ZL_7SFxCx_xTNW7Skb5uZvAXKf4qmWquorgQlw6c7RsrESJNojTMDwgFniT3LZdC6SQSImT.png) 

Typical application development scenario

### Infrastructure

![|400](https://remnote-user-data.s3.amazonaws.com/bZ4xNYF-AXj5gOI2kz3NZ_8ACjbXAmV6aX_KCMH3HX44jPGE5cW0EnS5Z_vb9Np2PpLU6iVKCObSFYJtiBkMs3Z4sJ9-aRQ7C48c_BxgCZ0FzHKj7OcCcjILRL2e3F1t.png)

### Tieing both Application and Infrastructure together

![|400](https://remnote-user-data.s3.amazonaws.com/1XQhcVPfRpmPgNz3dn7JsqFHJO46OxW93cgcvR8G57Igp-PjPbO57A_yoa9LLRsrr-YGc8Z09W-CWqkEitt_09N8FfOMC2gQINeVrNEoDlh_fSEHYb5woKVex8lnYLEE.png)

## Provision, Deployment, Orchestration and CM
Provisioning - The process of making a server ready for operation, including hardware, OS, system services and network connectivity

Deployment - The process of automatically deploying and upgrading applications on a server

Orchestration - The act of performing coordinated operations across multiple systems. Initial provisioning is done once and then the system runs for a long time, being able to control and upgrade a running system is critical

Configuration Management (CM) - The act of maintaining and upgrading application and application dependencies

![|400](https://remnote-user-data.s3.amazonaws.com/mUIgQUjTYUwMnHh3e7R-wAwBTiLmv22ssaPRKIbioCFp05i1m8TB0TePHtpfpxtX4oGzb4esfSj16OOPfhvHSZDFGw1fX5eeMX7TLBH4MtE-YHe5yLcZNqQosn14iDej.png) 

# Cloud Services

## Security By Design
The implementation of multiple security measures to protect the most valuable resource on your network

### Involves
1. Network
2. Code
3. People
 
## Security Myths
1. The cloud is secure by design
2. The cloud is unsecure by design
3. Someone else's platform means its someone else's problem
 
## Security Terms
1. Monitoring practises↔Storage analytics and security logs
2. Identify/Access control↔RBAC, MFA and password policies
3. Network security↔VPNs and network security groups
4. Store security↔Data encryption, client-side encryption and key vaults
 
## On Premises Computing vs. Cloud Computing
1. Provisions→Manually provisioned vs. Self-provisioned
2. Hardware→Dedicated hardware vs. Shared hardware
3. Capacity→Fixed capacity vs. Elastic capacity 
4. Expenses→Capital & operational expenses vs. Operational expenses
5. Managed by→Managed via sysadmins vs. Managed via APIs
 
## The Five Essential Characteristic of Cloud Computing
1. On-demand self-service
2. Share/pooled resources
3. Broad network access
4. Scalable and elastic
5. Metered by use
 
## Cloud Benefits
1. Cost efficiencies
	- Zero up front captial costs
	- Scale as system grows
2. Time efficiencies
	- Create virtual resources instead of physical
	- Offers substantial elasticity and scalability
3. Power efficiencies
	- Will be able to easy measure power consumption use by algorithms
4. Improved process control
	- Quick recovery
5. Improved security
6. "Unlimited" capacity
 
# Cloud Service Deployment Models

- **Public**: Cloud infrastructure is available to the general public, owned by the organization selling cloud services.
  ![Public Cloud](https://remnote-user-data.s3.amazonaws.com/ROc01LKoZvza49wK9MsZkRXYOLL2zEV3R7kijzdQjeef6f7MA7GMdx82Xw27-vo15jA74K2ZmKj7GWsszcTWeHTmpCfwwUAy2uWDtsm0WN4oEoNxD-sh6PDNtBzn2-WS.png)
  
- **Private**: Cloud infrastructure for a single organization only, maybe managed by the organization or a third party, on or off the premise.
  ![Private Cloud](https://remnote-user-data.s3.amazonaws.com/4lv6S2Cai5XUMmnr-hmXDG7yoU261hzx4KYswfCWKPKwudajljsuf_G3-aR4MZ_uybzDGZyei4tYnUUzY8jllodf6V2jNGzzKKk0bxhYnkxeiTjZvFr6C8xvhM6H2YLn.png)
  
- **Community**: Cloud infrastructure shared by several organizations that have shared concern, managed by org or third party.
  ![Community Cloud](https://remnote-user-data.s3.amazonaws.com/L9ZbVwdcfmes_ly5orOWR_MNrqUJMYUeqe9DJoCfTM1WU8LG5vAbnk3s4FPrnsseXyNP3iNZuMt5RHWumP0EVA4-VJViUh9IYjsU0Ewp9WYy1xbMUNR-ngWFeb0-9lfL.png)
  
- **Hybrid**: Combination of cloud types.
  ![Hybrid Cloud](https://remnote-user-data.s3.amazonaws.com/thlZ3OFs16d5X8x1XV8twkmRgKXjaF18taJ-w2pxF6haJcEj6NRM2aDsUeE-g_A47JPiX7I57SWQ20p7AKU2RVk9PSazxfdiDJ_7aOXoerRxpDamDzrYAosRs5hrTbqY.png)

# CSA Cloud Reference Model

![CSA Cloud](https://remnote-user-data.s3.amazonaws.com/MbAOuo5G5Ft80S430bYMARsdSYGY-X20Fx6grW_6GHfVxMQYhGhM8VtJL_o9qB_OfRwQ79PGSYMBh8wh0HOR-_9K2zg_2HNMV0RxeBOFa0D-nCPYTfoLhB2uwsw6EKLS.png)

# Main Service Delivery Models

- **IaaS (Infrastructure as a Service)**:
  ![IaaS](https://remnote-user-data.s3.amazonaws.com/XYnio51ldAWEaWwjyOR5fiN8Av5yGhnkW570kdPLiGkAqU8FCM3ssMCLyphnhD_5Ha2yj3nxeLMThjyP8jeLlmYiqun4HFVThLGsd5S_DWiUzZegx5uvQefUFddnWhY6.png)
  - Consumer can provision computing resources within provider's infrastructure upon which they can deploy and run arbitrary software, including OS and applications.
  - Examples:
    - Virtual machines
    - Virtual networks

- **PaaS**:
  ![PaaS](https://remnote-user-data.s3.amazonaws.com/oy4gkjY_irDEgbODZFKHtoZnkQiwsIB7zjHMBHqrChaH81flpqnSOjjg0LGSgqZl4Zo-Bod6JI9XiEb2SyLqk-7Ukh__gOJ03sQQXBG94sueD0RdcVpaG5w5CP1F9NTd.png)
  - Consumer can create custom applications using programming tools supported by the provider and deploy them onto the provider's cloud infrastructure.
  - Examples:
    - Auto elastic
    - Continuous integration

- **SaaS**:
  ![SaaS](https://remnote-user-data.s3.amazonaws.com/4lb8ITOGR0kqTSTTY30IA485xoC_fV-XpCchv4aT5YjCQqaAcsxZfxnq9rpILKHrjFCv0CCoN_5P0AtSpNLBUTOmJK5B3zmeLR6TJLRO1rDVbMVXPXnBx8H3D7PVqLdy.png)
  - Consumer uses provider's applications running on provider's cloud infrastructure.
  - Examples:
    - Built for cloud
    - Uses PaaS

# Continued Vulnerabilities

## Insecure Upload

- Techniques:
  - Filename: Does it change the file name you give it?
  - MIME types: The browser sends this.
  - File extensions: Can you confuse it?
    - Double extensions
    - Zip files
  - Content - a valid image:
    - Embedding what you want in it, e.g. EXIF headers.
    - If you upload a php file as a jpg, it won't get sent to the PHP processor to execute unless you have the ability to run things on the server in another way.

- Insecure upload functionality
- File Upload Vulnerabilities:
  - Server commonly checks the MIME type of the file. The browser is not trusted. The MIME type is sent by the browser.
  - Look for upload forms, send unexpected content.
  - Users could upload arbitrary content to your website. They could execute code on your server. They could set up their own phishing site on your domain.

# More Web Vulnerabilities

## Phishing

- Type of Phishing:
  - Server Hijacking: Manipulating the legitimate website to steal information.
  - Client Hijacking: Manipulating your computer to steal information.
  - Impersonation:
    - Setting up false websites to steal information.
    - Sending false emails/messages.
    - Using phishing kits/reverse proxy sites.
  - Take HTML from a good site, modify it to make it malicious.


## Impersonation

- Set up a website that looks like the legitimate website.
- Add forms to collect login information or other personal information, in the same manner as the legitimate site.
- Trick the user into visiting the website.
- Techniques:
  - Modify the downloaded website to point to the phishing collector.
  - Write an email linking to the website.
  - Send the email to as many people as possible.
  - Set up a phishing collector.
  - Download the legitimate website.
  - Upload the website onto the internet.
  - Try to disguise the website to make it look like the legitimate website.
- Phishing Collector:
  - Stores it for the person running the phish to collect later.
  - Retrieves the username, password or any confidential information entered on the site.
  - Redirects the user back to a legitimate page so they don't realize they've been phished.

## Server Hijacking

- Cross-site Scripting and Phishing:
  - Typically:
    - Add a new form to the page that we control and hide everything else.
    - Change the form on the page to point to the phishing collector or
  - We can use HTML code to change what the browser displays, even after the page has loaded.
  - This JavaScript code gets all forms on the page and redirects all their actions to the phishing collector.
  ![Server Hijacking](https://remnote-user-data.s3.amazonaws.com/npzyHLk4JNMWy-pqNzygiK7a1FKrR5aMNnMERVD0306vm3mXck6dNkN10cwu1srpQnM1pmJ3zziq_-AySyVhH5v9jkFsnKqt98VQMv6t42dz4kO_mIYHcf3Mdk_Pruql.png)
  - Typically involves changing the forms on a website to point to the phishing collector instead of where they should.
  - Techniques:
    - Create code to modify the website to point to the phishing collector.
    - Find an exploit somewhere on the website.
    - Create and send out an email pointing to the exploited legitimate website.
    - Set up a phishing collector.
  - Three major forms of server hijacking:
    - Direct compromise: Gaining access to the server and being able to rewrite files and manipulate them directly.
    - Cross-site scripting: Allows us to "reprogram" the website by injecting additional code.
    - Open redirects: Being able to "bounce" through a legitimate website to the phishing website, so it looks legitimate.
  - Exploiting a legitimate website to turn it into a phish.

## Information Exposure

- When sensitive information is accidentally exposed by an application:
  - May be application data: Leaked resources, version information, configuration details.
  - May be user data: User information.
  - May be deployment information: URLs or structure.
- As a black box tester, you need to scrutinize all outputs from the application for any information you can use:
  - Headers.
  - Testing files.
  - HTML source code.
  - Other directories.
  - Backup files.

## Authorisation Bypass

- Sometimes it is possible to bypass the authorization checks:
  - Missing authorization throughout the process: Some applications check authorization at the start of the process but not all the way through - sometimes you can jump in by bypassing the initial check.
  - "Safe" areas: Some applications have safe areas where it is presumed everything inside has already passed authorization checks, but this isn't always the case.
  - Authorization by omission: Some applications hide administrative controls from non-administrative users but do not enforce the check.
- Techniques:
  - Can guess a URL to gain access to something you shouldn't.
  - Use the URLs you've seen so far to guess.
- When authorization is not implemented properly.

## Insecure Cookies

- Cookies are used by applications to store client-side information:
  - Typically a session or user key.
  - Required so the application continues to know who you are after you've logged in.
  - When you log in, you typically get set a cookie containing some form of key which identifies you.
- Cookies are sent in the headers with every request you make.
- Cookies can be insecure:
  - If someone can forge or steal a cookie, they can become another user without ever needing their password.
- Techniques:
  - How do they change with different user accounts?
  - Can you manipulate or change them?
  - What values do they have?
  - What cookies are being set?
- Cookies ⇒ View Cookie Information (Web Developer Toolbar).
- Application ⇒ Cookies in the DevTools.

# The Big Three

## Languages of the Web

- Server-side:
  - Many more...
  - Ruby.
  - PHP.
  - .NET.
  - Server-side JavaScript (e.g. Node).
  - Python.
  - Java.
  - Perl.
  - Go.
- Communication:
  - JSON.
  - Raw.
  - XML.
- Client-side:
  - JavaScript.
  - CSS: Stylesheets.
  - WebAssembly (Wasm).

## On-Going Communications

- AJAX Polling:
  - Short: Make requests to the server on a timer.
  - Long: Server waits for something to happen.
- Simple AJAX/XHR (XMLHttpRequest): Open a connection to the server, send a message, get a response closing the connection.
- WebRTC:
  - Allows for real-time and peer-to-peer communication.
  - Typically used for high bandwidth applications where reliability isn't key, e.g. Video/audio streaming.
- WebSockets: Bidirectional communication over a TCP socket to the server. Now the best option.

## The Biggest Web Application Security Threats

- Cross-site Scripting: Injecting client-side code to manipulate a page.
- SQL Injection: Injecting data into a database to manipulate a DB query.
- HTML and Parameter Manipulation:
  - Manipulating what the client sends to the server.
  - Sending the unexpected.

## Cross-Site Scripting

- The normal process:
  - This is controlled by the application.
  - This HTML is then rendered and displayed by the browser.
  - Normally it is the server and applications job to generate HTML.
- How cross-site scripting breaks this:
  - Users are able to inject new HTML code (thus scripts) into pages in a way that can be executed by other users.
- Two major types:
  - Stored: Where a user input is written or stored and later displayed back as the result of a query.
  - Reflected: Where a user input to a page can be populated with XSS and gets output as a result when that page displays.
- Examples:
  - Server Form.
  - Example 1:
    - Server:
    ![Example 1](https://remnote-user-data.s3.amazonaws.com/8pLrO19Y63pEdlh5eY38bCSmdqP4eCbFYkqTh8IvyVAcuL_ifsQYA6F9MHB6kiNKXhHsoS_IkUAiwyJptI5WHq_zTcsjrqifm1OBRc5TOirLkvuxn2BvkvNlqeAkS0ho.png)
    - Client: My username is `<strong>Oli< /strong>`
  - Example 2:
    - Client: My username is `<script>alert(1); < /script>`
    - Server:
    ![Example 2](https://remnote-user-data.s3.amazonaws.com/fMe0fydjo0UsiwO1PQkrtfTzsbGAduElQ6EUu-NReKOXqVOiWdYoy5yMlBbfm4lfN7vx85F7GcVgOdEcLtW_diUw5zmSuPU921XxMdbqWfMzXJPOXO1efLaMEqh5jKfq.png)
    - Now we have found a vulnerability.
    ![Vulnerability](https://remnote-user-data.s3.amazonaws.com/h8M56DRuCog467S8wOkhiyuHAka18uxfXPNnU3j8f3Qahpqu92VKrRvY7Glvuau81H5t30yk-cRO_glNsVkfBfv3b22EscAeZlYfYfa8IBa4YfBs-F5xo6ZaXsKoPr7J.png)
- Can be found using the XSS locator (polyglot).

## Once a vulnerability has been found

- You can include external javascript:
  - Botnet control.
  - Bitcoin mining.
  - Malware or compromise.
- You can run any javascript:
  - Control or manipulate the page in any way.
  - Control or manipulate the user's browser.
  - Get the current content of the authentication cookie.
  - Make requests as if we were the user's browser:
    - As if logged in.
  - Make outgoing requests.

## SQL Injection

- Manipulating the query sent between the server and the database (using SQL).
- Insert something into the query to change it.
- Example:
  - Input: `Bob"; DROP TABLE users; ‒`
  - Query: `SELECT * FROM users WHERE username="Bob"; DROP TABLE users; ‒"`
- Example 2:
  - Input:
    - Username: Oli
    - Password: `something' OR '1='1`
  - Query: `SELECT * FROM users WHERE username='Oli' AND password='something' OR '1'='1'`
- Example 3:
  - Input:
    - Password: something
    - Username: `Oli' ‒`
  - Query: `SELECT * FROM users WHERE username='Oli' ‒ AND password='something'`

## HTML and Parameter Manipulation

- Manipulating the inputs that the client sends to the server.
- Using:
  - The URL itself and its parameters.
  - Forms and their parameters.
  - JavaScript server requests & API calls.
  - Communication.
- How to do parameter manipulation:
  - Using the browser:
    - Inspect and modify using the developer tools.
  - Using client-side scripting:
    - Execute code in the console.
  - Downloading and modifying:
    - Download the source code, make local changes.
  - Using extensions:
    - Web developer toolbar.
  - Using scripts.
  - Using tools.

# Tools and Techniques 2

## Writing Secure Code

- Consistent.
- Logical.
- Tested.
- Easy to understand.
- In one place.
- Documented.
- Maintainable.

# Introduction to RobPress

## PHP Files

- Anything not in PHP tags is output directly (HTML).
- Use `<?php... ?>` tags to execute PHP code.
- Use `<?= .. ?>` to output PHP code (echo).
![PHP Files](https://remnote-user-data.s3.amazonaws.com/ED4cuhpToQSKhYDbwiifOqGr_qQC8n3tNFclKn_xvciqm_6lHNpT3i6QyHkF3vWaOBef5t5BZxc8CfjSHL6NbCid4XNzZBEvlNZz8dIHEOEp5IB2b__HTLPpbyNBOqD-.png)

## Functions

- Define a function using function keyword.
- Optional parameters are assigned default values using =.
![Functions](https://remnote-user-data.s3.amazonaws.com/vBxnwPFjD2zNGM6BMn-7RzxFUPdGl6dSqY9oWAEvWiFghEKEgN_Pabql1W1_9hSoaZZ308l2_Czle-zveIn7MjL6qVV4VTNXuzN0tWOqN_zYFsgsC0HKAkEctG1wJJTb.png)

## Variables

![Variables](https://remnote-user-data.s3.amazonaws.com/j9apfpD5Y0hCh_2lwl8vKqKgsVJ1O5_H29TPNNnW81IO2MfqwJmlUt9qxSigy902QltrFpGolmYDhoHDRoDZwBKsNH5BQSY9rKzVX-W5XdQZJJDOWkBATScy02KwtgIs.png)

## Arrays

- Create an array.
- Arrays can be numeric.
- Or associative (like hashmaps).
- Arrays can be initialised.
  - Or for associative arrays.
- Other array syntax.

## Built-in Variables (Arrays)

- `$_GET` - URL parameters.
- `$_POST` - Posted form values.
- `$_SERVER` - Information about the request which was made.

## Seeing inside Variables

- `print_r($variable)` or `var_dump($variable)`.
![Inside Variables](https://remnote-user-data.s3.amazonaws.com/2wqlo-llBKjDUBUKcQUrPpCHarjt5Fs8AhhoiT1UZKubfCtQO_UstETMNKaWW8xKWWk-LY1Rx3Xp5hE3pcux2N4PzoJ1vj3su13F6EpTSq2m0Ffa2YEd-CIBSzjUWB_2.png)

## Conditions

![Conditions](https://remnote-user-data.s3.amazonaws.com/PrpxJvAA2qJO0qVB2obzVv-BvLQ2poJgguoLA3_y9afd1yG1Ytqb8Vav1DU48wr3y3OalSKNM_Xu9_Qr34IjK7wwK7iJIaDxpRHk2_fiiI5uL67yugBeydg0NseB6VfM.png)
- You can also use conditions in short tags.
![Short Tags](https://remnote-user-data.s3.amazonaws.com/-GvvXBkhoeJvsB9qrI_00eqXDQ19Rc_iUI8HRHhBn-hl76wF5yguQj498j73lxN4V7gjcWRmfEpyJdeisOlgQYoVStqgzdb6JnCP7Bpt00g5jRbXpb03Lt9-1_w6e6J6.png)

## Loops

- `foreach`.
![foreach](https://remnote-user-data.s3.amazonaws.com/5ZQDO8w96iQm0eKKJsPJBG2j-4zt_NyDKKzG-BY9c1uWS94OIa7lMEPdlemQqRWi0A2Dn4XElz3EOV0s2Hmb1hTsM6lujrlvBmcOBXh6f9t3W_KycABBoB-wARJ2RIx5.png)
- Iterating through both keys and values.
![Iterating](https://remnote-user-data.s3.amazonaws.com/d-TSrljdU4kAlJdYR5C-vuTFbTI4eeHQCFEJMzE6XhC2YVfz-AMlahDPZLuXt3De03Jp5OeTnn4KpSkIcEEIkX-3cnI9RYrXyaFzofNkJA9qB5SDczcR01ASEKGtvsTC.png)
- Special syntax for loops using short tags.
![Short Tags for Loops](https://remnote-user-data.s3.amazonaws.com/KrXJEvm5B8HD4zcsCO_OYrw50i119bEVn0ZWmbnz-0yuicdHrvj8yAH3ZIBPZdgw41i-tsXNe8iktZrQFlpJ86KTuXTQsKa2NSHbFv1RqTvbxVylKrFWlH-_h_ScmapK.png)

## FatFree

- Maps URLs to PHP functions.
![FatFree](https://remnote-user-data.s3.amazonaws.com/FJOnFtD03dBnAc67ESoQA65bPKnPAEB_uPg2bf5gZTJ7PkCMrjHfusSBKJil1qOAqvAxtdgwJh21wj6YkUjweGLStG9s2I3lXk-94v-fe49ZW-qnMYvNNCI4-Tpj7JGv.png)

## Main Areas of RobPress

- Public:
  - Blog.
  - User.
  - Page.
- Private - Admin:
  - Comments.
  - Posts.
  - Settings.
  - Page.
  - Users.
  - Categories.

## Accessing the RobPress Database
- **Local**: 
- **Remote**: 

## Using FatFree to Automatically Provide an MVC Structure
![MVC Structure 1](https://remnote-user-data.s3.amazonaws.com/ZdBQuHPbTXtycxz5zcZCIYnNuFg-cP-8RKQ4CRLMxnbrUAapYPcD1cjSazH_qz3CHPg0VsSkII-ByTuEWdj7uTIc9Mx9cnMgRH2-atExahi7lVNQBETimXurQ77lTBcN.png)

![MVC Structure 2](https://remnote-user-data.s3.amazonaws.com/xX8z3SobsFN2aGRFmrlZ6YxD99zfhgsfHsPWW05IP4hhlCjWyY9Jl24-2Q-9KtN_tyMUVTBm8za-fdCtZuiN81RSuN1JwRxToFkWScG9hEfP9l5STdiz1yxm7zD6GkFq.png)
### Example
![Example 1](https://remnote-user-data.s3.amazonaws.com/qYb5WJea37pCLbIaalbtIxywF7w5Jq_n8Ww-q4O1Yd7J-5M5_-Qc6QPKDvVS7p7qnfITxhqqmaVUkQdZo7PjCCpPXM_4Qlu7oX976ZoVItG8RVcCpFN0ChFFfZsOC5sn.png)

![Example 2](https://remnote-user-data.s3.amazonaws.com/hxm36A4wd27xWyFrkvsgDUZN9SrHaE_547OHP67HL_cALjRfmAEivp0M-gQ_BRabuSxX9nkeysQUiqjUhlGCWU6TEf2Wu5TZrXzFHx8rpJ5zcCY2zDfygN7DimgR8Goh.png)
- `$f3` is the fatfree object.
- `PARAMS.3` accesses the third parameter (third bit of the URL).

## Using FatFree to Create Forms
![Form 1](https://remnote-user-data.s3.amazonaws.com/MD2zeat3WrbZXEzLhRce7j_FRZxVcZVBxIO644BiLqDIYuWytLreS13iWIXtL8tg9SAZKP2mE8_U0y7rKnlXMPlB3wRLz-S8CayeGLW9rivxpZ7OJErExLds46ULTFXW.png)

![Form 2](https://remnote-user-data.s3.amazonaws.com/o_cOvQB-pHbOmTbqt2SagoDJD_p4c-CjZj2Ooi7zfOvDGrW95XnxGkoZKcM8Fa2V-WQeIjkErSH_geKwF2A77l5X_Z3jSpTLuodcoshG-DlWdT11gxOf5fjw48UFA9UL.png)

![Form 3](https://remnote-user-data.s3.amazonaws.com/e6Ylg3KFsdtcfAKEMFoe_a6XAw2W_6_zXOVNl5Q2GHh0Ct9Btynq-c2HHWj-0hBd_qRD7Su6XsngZQgmoNaIu4NR9hUzuHCEwjmgZjxvwU_JNqKD4K31EOTdQvzAkli9.png)

## Templates can take Variables
- Maps `$variablename` inside the template to the `$variable` in the code.
![Template Variable 1](https://remnote-user-data.s3.amazonaws.com/MV92ThwaN95K-e4ETDRRPBY44glfoXm0rVU59sG5hD7qtCwGs26qfeCDqwF5W2gBHfZBhJchG6pEbLvZHvlgwRs9o0_FrFW4BrcHSHLP7yo3YXB74QbMMOsJ5ve3SQLk.png)
![Template Variable 2](https://remnote-user-data.s3.amazonaws.com/1kF_ldr9b2NI4Z6d1M01ENHOr0qvH8gBWLS8bFy2hpD9X52okefTinJAPozhbg-4F6NQfSQwpAR4LAp1SAaEiD_R65kXZxf3LDFjhokaki28sB43QksmqggJ8T1aHMh1.png)

## Models
- Model is a field on that controller.
  - It loads any of the models from that, which have functions.
- `$this` refers to the current controller.
### Model functions which all models have
- Will return a single result.
- Will return an array of results.
### Examples
![Model Example 1](https://remnote-user-data.s3.amazonaws.com/ZYiEmDh-VltHs98nbVizHVGQUdsYnpduV5YrjC28nENNMQqxJghJLp_4S1_xp-UOljH0ivXqW4A2T5FgZc6q12DRpR2K29KiypOOpoADXFj-HcFHwlWVwAiXeK7_Tex6.png)
### How are Results Returned?
- What is a DB mapped object.
  - But it also has functions attached to it for manipulation.
    - So you can also manipulate the database with it.
    - `$user - > id=5; $user⇒save();`
  - Like an array, can access using array/object notation.
    - `$user['id']` or `$user - > id`
- Multiple Results - An array of DB mapped objects.
- 1 Result - A single DB mapped object.
### Model Examples
#### Single Result - View a Blog Post
![Single Result](https://remnote-user-data.s3.amazonaws.com/pdvA77gUEUqq5XmhPIIBhbExHhhSk4ASGsZBWtEzM8p0Ou4Z9JSEzPepagbz9limlV5g0KHmIxVUoOjrPFHT1_14mDxixwEi9JstiVoffJIphJHmK-OENsppOxfBKmP7.png)
#### Multiple Result - Get all the Users
![Multiple Result](https://remnote-user-data.s3.amazonaws.com/TzZcW3-QB33meMgPNEjCviU6CKisLs74q4DGFhGbwcZENGijljtf2Z4UXQ_42Q_YCjz3ltt53EQ-KLLRia_750wvUJJ2GazT8006o7JYCB8aWMqTw4_f_u7Paw0aEtJc.png)

## The Security of the Web
### HTTP Requests
#### HTTP Verbs
- GET - Read
- POST - Create (or update/modify/delete/..)
- PUT - Update/Replace
- PATCH - Update/Modify
- DELETE

### Server Responses
#### 2xx - Success
- 200 - OK
#### 4xx - Client error
- 404 - Not found
- 400 - Bad request
- 403 - Forbidden
- 401 - Unauthorised
- 405 - Method not allowed
- 418 - I'm a teapot
#### 5xx - Server error
- 503 - Service unavailable
- 500 - Internal server error
#### 3xx - Redirect
- 304 - Not Modified (Cached)
- 302 - Found (Moved temporarily) (or 307)
- 301 - Moved permanently (or 308)
#### 1xx - Informational

### GETing by Hand
#### Methods
- 
- 
- 

### Passing in User Input
#### Using GET
- GET query parameters
  - 
#### Using POST
- POST form data
  - 

## Testing for Infrastructure as Code
### InfoSec Triangle
![InfoSec Triangle](https://remnote-user-data.s3.amazonaws.com/ZlGWYN_4nw2_QCNBBze9NTeHAoKfrvrhSLZVTQ46k4wn-rdMUkKQw3mxwKEW6LKKhz-1jOGi1vF1MiwP2R7gD8DF_RVObYXEmb5QacajdT7x1p4QkHoMoBIb3sF22rBT.png)
- Reducing the functionality in software reduces its attack surface area.
- Need to find the balance between functionality and usability for optimal security.
- Varies on a case by case basis, can find the sweet spot by communicating with customers, testing and prototyping.
![Balance](https://remnote-user-data.s3.amazonaws.com/P8xwmKnnB5svZqpS5NbTRdkUVTvvz8Vz8IsmM8JucWYlkU_6YNzHAk8fconWe-3RbbFNlSkoO_LGDO-uhmfRp5ukXX9JVPtftHff-mPcHZABLjnPe4m8dWCMCfo_8-30.png)

### Vulnerability
- The weakness that enables a threat to be successful.

### Threat
- A circumstance or event that could damage the confidentiality, integrity or availability of information or information systems.

## Cloud Vulnerabilities
### Example Threat Analysis
![Example Threat Analysis](https://remnote-user-data.s3.amazonaws.com/X-PwtkZZcnLkeEoUpLanKImnFzdm08JFqxGNv55X3mCE0B8oS8Ql4vif6P0yi_T2jy5hbuo40mglNeQeuU9FNw0S-7rQFKhpnXmWvv29B0QH-6gJMWwOfCbOhhFLJAeV.png)

### Supply Chain Risks
![Supply Chain Risks](https://remnote-user-data.s3.amazonaws.com/xOlHyulgGw8jIvD6l__qnpIqbEMWu3mYS6NaSBvQQFyNgKf26SbeZ3nmtui6BJwxyqEBnzuu_9KE-CkjXhzgr3eiPUmM46iAvN5p7UXIeOGAbFXZoSm2uhz6C3L39l11.png)

### Summary of Cloud Computing Threats
- Incident analysis and forensic support
- Business continuity and resiliency
- Regulatory compliance
- Infrastructure security
- User privacy and secondary usage of data
- Non-production environment exposure
- User identity federation
- Accountability and data ownership
- Multi-tenancy and physical security
- Service and data integration

### Accountability and Data Ownership
![Accountability and Data Ownership](https://remnote-user-data.s3.amazonaws.com/3oNU4fk41w-izJch0npAP31kW96bsbpwMo31-IC8PnszCeVtgJpifhj2Qo6sHYl9Js0W5Ydz_LoyAcENN7mUB8GT4IK3zIJfeY3__sy-HdYFXTJPzRLdikhwOQmhrC7S.png)
#### Things to consider
- Who owns the data
- How to encrypt it
- How to destroy it
- Where to store it (isolation _)
- Consider data toxicity

### User Identity Federation
- Identity providers
  - Open ID (Oauth)
  - SAML
  - Access Control Design
- One user identity can be used to login to multiple systems.
- Provides less control over user lifecycle.
- Improves user experience.
![User Identity Federation](https://remnote-user-data.s3.amazonaws.com/m5SGxJ_H4lLK-SD5cAuM_cByohXtjk3Lucw2vti_-eAjAm91ATs5GCQZJzYjAphSzOz9NEWd_2r9mvr-UknO3a4MWNJaFwBCidywxPxhxjx1o7nQQvE8WYbTIGXtQu8O.png)

### Regulatory Compliance
- Data perceived secure in one region is not assumed secure by another.
- Data stored in the US may not comply with EU law.
- Lack of transparency in the implementation makes it difficult for data owners to demonstrate compliance to owners.
- Lack of consistent global standard for handling data.
- Use a cloud vendor who understands and applies solutions for the various data protection laws.
  - They should also know how to handle cross-jurisdiction data protection requirements.

### Business Continuity and Resiliency
- Need to make sure that Security Level Agreements (SLAs) cover data resilience, protection, privacy and that the vendor has a robust disaster recovery process in place.

### User Privacy and Secondary Usage of Data
$$\begin{bmatrix}
\text{User Priority} & \text{Providers Priority}\\
\text{Keep personal data safe} & \text{Push out the liability to user via privacy and acceptable use policy}\\
&\text{Build additional services on user behaviour}\\
&\text{Do the minimum to achieve compliance}\\
&\text{Keep their social application more open}
\end{bmatrix}$$
#### Things you can do
- Encrypt storage
- Anonymise personal information
- Terms of service with providers

### Service and Data Integration
#### Data in Transit
- Authentication
- Authorization
- Accounting
- Protected using SSL/TLS
#### Data at Rest
- Protected using Encryption keys
- Confidentiality
- Integrity
- Availability

### Multi-tenancy and Physical Security
- Inadequate logical separations
- Co-mingled tenant data
- Malicious or ignorant tenants
- Shared service, single point of failure
- Uncoordinated change controls and misconfigurations
- Performance risks
#### Threats
- Side channel attacks
## Open Redirects
￼￼￼￼￼￼￼
​￼￼￼￼￼Reference Diagrams￼￼
​￼￼￼What categories do you need
####1. Define hosts - machines
####2. Define network - how connected together
####3. Define stakeholders - the people
​￼￼￼Basic reasoning
￼￼Reuse the diagram
￼￼Illustrate threats
￼￼Show impact on assets
￼￼Show impact on stakeholders
￼￼Manager infrastructure
​￼￼￼Advanced reasoning
￼￼Show forbidden relationships
￼￼Add monitoring nodes
￼￼Identify host assets that need to stretch
​￼￼￼Identify persistent assets
- 
​￼￼￼￼￼What is Policy￼￼ ↓ 
###1. ^^￼￼Network policy￼￼^^^^:^^  
###2. ‒you can measure
###3. ^^￼￼Code practise￼￼^^^^:^^  
###4. ‒If you are building
###5. ^^￼￼People Guidance￼￼^^^^:^^  
###6. ‒If you can't measure
- 
​￼￼￼Policy↔A statement that reflects the rules that everyone should abide by
- 
​￼￼￼￼￼Good policies are organized as follows￼￼ ↓ 
###1. Purpose
###2. Policy compliance
###3. Date tested
###4. Date updated
###5. Contact
- 
​￼￼￼￼￼Frameworks￼￼ ↓ 
###1. ^^￼￼Security Frameworks￼￼^^ #￼￼Frameworks￼￼
###2. ‒We mean compliance, such as: #￼￼Frameworks￼￼
###3. ‒‒^^ISO 27001^^ 
###4. ‒‒^^NIST^^ 
###5. ‒‒^^BSI ^^
###6. ^^￼￼Security Models￼￼^^  
###7. ‒We mean models, such as:
###8. ‒‒^^IoT^^ 
###9. ‒‒^^Blockchain^^ 
###10. ‒‒^^Cloud^^ 
- 
- 
​￼￼￼￼￼Measuring Security￼￼ ↓ 
###1. ^^The SANS Endpoint Security Maturity Model Curve^^
###2. Level 1:
###3. ‒Random, or Disorganised
###4. Level 2:
###5. ￼￼￼￼￼ - Scanning other tenants
- Cross-tenant attacks
- DoS
- Architecting for multi-tenancy
- Data encryption (per tenant)
- Controlled and coordinated change management
- Ability to audit the provider administrative access
- Third party assessment

### Incident Analysis and Forensic Support
- Cloud computing can make the forensic analysis of security incidents more difficult.
  - This is because audits and events may be logged to data centres across multiple jurisdictions.
- In the event of a data breach, you must understand how to identify and manage critical vulnerabilities so you respond to the incident as quickly and effectively as possible.
#### Investigator Teams
![Investigator Teams](https://remnote-user-data.s3.amazonaws.com/WKZpPq6K-mOC5PSnWsMoxGGhLwIIvAyiUHMS1MK-jVvvSuGKYCP1xKXqLEXAS9ahTCfRUkw18yHAihiVWDxJS_VX3G_OzFwncEwHcUHyae6ZY6y8nBLtNMSSuyAtM5Pr.png)
- Check your Cloud vendor policy on handling, evaluating and correlating event logs across jurisdictions.
  - Is there technologies in place, such as virtual machine imaging, to help in the forensic analysis of security incidents?

### Infrastructure Security
#### SANS Endpoint Security Maturity Model Curve
![SANS Endpoint Security Maturity Model Curve](https://remnote-user-data.s3.amazonaws.com/I_qx6clPu6FiguqHEBYgPBqYjo4cUMfL2lC37t_wAxjBsM5dI_pCvpSUyDY66oMS0nYJ9knUvlrK3V5TtV-GwTjqmTMHOVLi4OBFWp-Ihrkjl0-EKoXrHRKH_6uj6q62.png)
#### Cybersecurity Capability Maturity Model (C2M2)/Maturity Indicator Levels (MILs)
![C2M2/MILs](https://remnote-user-data.s3.amazonaws.com/K7CrYAK-dnLqiOYMwGMHDx7aErEeelYagNfAoNZxpz9oIffnchEhiWKNrVf15Kpp5avxYyg34aBHylapNHwe1MDyQs83vX60RcLPuPZygyQ59nI6hxLP_1KMtt01bUp1.png)

### Non-Production Environment Exposure
- Don't use the cloud to develop concepts or tests.
- Always use Multi-Factor Authentication.
- Treat any pre-production environment or data as top secret.

# Service Level Agreements

## Service Level Agreement (SLA)
The part of a contract which defines exactly what services a service provider will provide and the required level or standard for those services.

## SLA Objectives
- Improve performance
- Save costs
- Provide access to technologies
- Provide access to skills

## Description of the Services
- The SLA should include a detailed description of the services.
- Each individual service should be defined.

## Performance Standards
- In practice, it may be impossible, unnecessary or very expensive to achieve performance standards at the highest level at the request of a customer.
- The service provider may argue that service levels should be set deliberately low in order to guarantee that the service can be delivered at a competitive price.

## Compensation/Service Credits
- Often achieved through the inclusion of a service credit regime. Where the service provider fails to achieve the agreed performance standards, the service provider will pay or credit the customer an agreed amount, which should act as incentive for improved performance.
- For the SLA to have any "bite", failure to achieve service levels needs to have a financial consequence for the service provider.

## Critical Failure
Solution to critical failure includes:
- A right for service credit
- A right to sue for damages
- A right for the customer to terminate the agreement if service delivery becomes unacceptably bad.

## Service
A means of delivering value to customers by facilitating outcomes customers want to achieve without the ownership of specific costs and risks.

## Elements of a Good SLA
- Performance standards
- Overall objectives
- Description of the services
- Compensation/Service credits
- Critical failure

## Service Level Management
![Service Level Management Image](https://remnote-user-data.s3.amazonaws.com/Lvmflx3KeeDxjlQ0K9oyWxXrzCzHEYNO2T6l0vUX5gKiV30Xg3aRygQofz6NMwRpKfv464s7J2MrpHpZp4mb5H0LHH6Mv8tH79joiDxJddJF3mxZt-4pV3cYf1b0L9zl.png)

# Tools and Techniques

## The Process of Penetration Testing
1. Scoping
   - Agree on what is being tested
   - Define boundaries
2. Gather information
3. Identify vulnerabilities
4. Exploit
5. Post-Exploit
6. Report

## Burp Suite
- Burp Suite is an intercepting proxy.
- As you browse, everything passes through it. It:
  - Collects information
  - Allows you to track what you have done
  - Allows you to review previous requests and responses
  - Allows you to manipulate everything
- ![Burp Suite Image](https://remnote-user-data.s3.amazonaws.com/0jUBwszGgDyBaXmAEuT2x6myuX7PfAUQuYtc87ZRns79u6avCpne6aM9Spxd9nhEdip6BLbxTO6wcqP82tCHr3WAqBzxKYYGd40bDHdqZEJQLiQQBAWNht-vao1c6asV.png)
- Set up:
  - Set up Burp Suite as the proxy
  - Install the certificate
- Sending a page to intruder allows you to run attacks:
  - Insert \$\$ around fields you want to run the attack on
  - Fuzzing - Long lists of inputs which are known to lead to potential vulnerabilities
- SQLMap:
  - Provides access to the whole database once an injection hole has been found

# Vulnerability Fixing

## Make a Test Controller
- Can test things without breaking anything else

## Output Variables and Terminate
- Use `var_dump` and `print_r`
- Use `die()` to stop anything else being processed

## SQL Injection
- Look for:
  - Database queries
  - Model access, SQL keywords
- Think about:
  - How are the queries being constructed
  - Where are parameters coming from
  - Are there direct queries
- How to fix it:
  - Ensure inputs into queries are safe and expected
  - Ensure queries are being constructed correctly
- Use `grep` to search through the code to find where to look:
  - Keywords: database, query, PDO, sql

## Information Exposure
- Look for:
  - Files exposed to the web that shouldn't be
  - Files or functions that are around that shouldn't be
- Think about:
  - What is being used and what isn't
  - If its not being used, why is it there?
  - Does it need to be used, but not publicly?
- How to fix it:
  - If theres no reason, get rid of it
  - If it doesn't need to be public, it shouldn't be public
- Using `grep`:
  - `.bak` files are backup files
  - `__find__` will output a list of all files in all folders, including hidden files

## Cross-Site Scripting/XSS
- Look for:
  - Inputs where data is stored and later displayed
  - Are there other places where HTML is combined with user input
  - Can any HTML characters be used in that data
  - Inputs which are outputs
  - Can you manipulate that HTML
- Think about:
  - What should acceptable input be
  - Should the output be encoded
- How to fix:
  - Reject or throw away invalid input
  - Encode HTML into normal characters
  - Strip HTML tags that shouldn't be allowed
- Will mostly be in templates and views:
  - Create/use a function to prepare unsafe input for display
  - Use everywhere its displayed in templates
  - Do validation on **input**:
    - Don't allow special characters in the first place
  - Do escaping on **output** not on **input**:
    - Preserve the original input in the database
  - Remove/Escape HTML where it's not needed:
    - E.g. a username#### 
  - Limit/Restrict HTML where it is needed
- Use libraries such as HTML purifier

![|400](https://remnote-user-data.s3.amazonaws.com/Iz5vTnOGIMTnJZKRiEfovS9_gXdmBTlEhRnT0YMzjaSF2JIwWzwNC7jgnSeVK0Jksuoay0GQffXxYiBOkAlIUK0EmQNqfY6vGKdaLV8_tv1x_PGI5Idl_ruA7v9tK0EB.png) 

User input being directly written out, allowing for XSS

![|400](https://remnote-user-data.s3.amazonaws.com/mcLkmS2F-H6q7hlV8KH4y_ENWN6SXzPjII3uWJxbKBUw03aR4uCXWPuxeem_gSIxJDsYgqwPb5bxcA1jj3Sc6j9fZCmMdxCwwOeAwokByi1OFN2TUYhAbUNYh66gDbqv.png)
### Example

![|400](https://remnote-user-data.s3.amazonaws.com/hVYLOLlHvVeP6Z5Wacx7UPNA4ocfHMcnvSPab8UmSvFa-d-0vrr1x03kGDtMkbCGt6Me8uouLpAr3uaWlr5NmNe_QVRAPLpKbiKk_0CfDet9RgrMXWk57KSeBwyL50Fr.png) 

h() escapes HTML and safe() limits HTML

![|400](https://remnote-user-data.s3.amazonaws.com/9ejLBL02lhOejGlopq8HozQja1j--lgeTKkFHQmYNGzvQc1mv8Y6zq0_tz0lkuKM0y4b9qwGd_zgOUXVQ51syu0Kqm8Rz0ESxKD8u3INm94p95oSurPUvutMuwJ498wQ.png) 

Turns to

![|400](https://remnote-user-data.s3.amazonaws.com/Xwx3CIkS9yVvsfQEFtzx_I-KRf1efa2fGDfnq_G1KIwsP_0NPF3FyzbsmDJrpJ5omTgiUvnWGhcKHUVUBAXSqW5Y-1LQgAdN69kxKjp7oWG8d18QmZ4QGhYw_Pu3b7oV.png)

# Insecure Upload

## Look for
- Parts of code that handle uploading

## Think about
- What do you want to allow
- What does the user have control over
- How could the tests be bypassed
- How to reject what you don't allow

## How to fix
- Perform tests on every uploaded file to ensure they are exactly what you want

## Uploads in PHP involved the move_uploaded_file function

## Find instances of use
![|400](https://remnote-user-data.s3.amazonaws.com/snIydDBQB5i47OIVMyME-VOHtroDaCcV9bZdDvejwBCaPGaJtie0ESWDAJGp9-BF96Un0xpEGIqXjaEJKR750a2wkxIpQRbvCV4jOvCEsSrbqNMnBt_nMA8fcKAYN-Bw.png)

## Add functions to test for files being valid
- Check extension
  - Use pathinfo
- Use .htaccess to restrict what happens to uploads
- Check file type
- Check MIME
  - Its in the array
- Use a whitelist
- Add function to handle saving correctly
  - Generating a new name for the file

# Cross-Site Request Forgery

## Look for
- Unprotected forms
- Insecure GET actions

## Think about
- Does this need to be CSRF protected
  - Any actions which change state

## How to fix
- Make forms unique so they can't be copied
  - Use a token
- You want global CSRF protection
  - You don't want to have to do it on every form

![|400](https://remnote-user-data.s3.amazonaws.com/RXyqvlXfChselJSpXHwRS-_4WwZ7cCb8BkLVX3jYvSVVqnyOSPnA1hv-l9SWRJHEgX_jxl2HzfmkQWcE-_yPunzdR2kyrC8hyXNgS3i2t1jTOGGlu0aL8Vql4xsdvo0x.png)

- Then add global code to verify the tokens
- `start` is called every time a form is created, is a good place to add a token to a form

## GET
- Look for GET requests that perform an action
- Are there URLs you can go to directly which change state
- GET should never change state
- Can you perform actions where you shouldn't be able to

## POST

# Authorisation Bypass

## Look for
- Actions that require authorisation

## Think about
- How the authorisation is given
- What authorisation those actions require

## How to fix
- Ensure for every action requiring authorisation, the action fails without authorisation

## Log in as different levels of user
- Try the same actions with different levels of access
- Is it possible to do actions you shouldn't be able to
- Just one function that checks access for a level

# Internal Information

## Look for
- How does the application and framework handle error reporting
- How does the application handle unexpected errors and faults

## Think about
- Separating your development and live environment
- Do you want to throw away the error information or keep it somewhere

## How to fix
- Handle errors and faults correctly, don't make error information public

# Parameter Manipulation

## Look for
- Any form fields

## Think about
- What validation is being done
- Is it possible to get data in that shouldn't be there

## How to fix
- Ensure, before any processing is done, you only ever have exactly what you expect
  - Throw away the rest

![|400](https://remnote-user-data.s3.amazonaws.com/sVxGjNPiCdJPAPXyTmTsWRhjpH2TD9oMcnok-i20qg1-FSq7FNwy8mj8Lt_Bu625vX90eNq3z-8X-CNOPn-lK5wEhUhFoLZd2Z6MirLZmUvWuhT86OdJsq5jbOfTezFI.png)

- Do validation at the model level

![|400](https://remnote-user-data.s3.amazonaws.com/vupvVDVdolOpkoniC0kfHqi7ofSonYhwqf2Rq7mISdwOmHe86X4MzbWuo8e7OTLEgJZMj3yBnV8rt_gIP3gwpKo5zOcbhCYvUMrng2K8XnFRzT1Xmziv50yZsfhyQPvs.png)

# Application Logic

## Look for
- Is there application logic the users can affect through user input

## Think about
- How to ensure the integrity of any multi-step processes or functions or actions
- How can you protect the logic

## How to fix
- Keep state server-side
- Ensure unexpected actions cannot have unexpected consequences
- Individually check if each input is invalid, so that the logic can only be followed if every single input is valid

![|400](https://remnote-user-data.s3.amazonaws.com/-V_TdV_weuUX_zeJL-XUIgyWHW_rWzyw3KpJM5peKpMHt1wVSHRy01o4iuPl7mvy8Ku-JaNpOAxAGpUTBUG0SQ6Bt882uG2Op6WwR31HOOwOY2TPq7Uw_N_JOYMI9xoP.png)

![|400](https://remnote-user-data.s3.amazonaws.com/BoJQMbDHweDnnP-IUVn31TCtWCzR078YkDmp3NPilgUMjFjRQsBbPJKmC1N8NympnUEnPA7jMZkBZw43vrV-s7Izv8CrfkXc4NsIO86xmzuPC0FdVdgI8Z2FSd18CRIy.png)

# Out of Date Software
- Look for out of date software and components, apply patches and install updates

# File Inclusion

## Look for
- The Network section of the Developer Panel
  - What external resources are being included
- Places in which files from the file system are included
- Are there places where a file is dynamically included by the URL

## How to fix
- Restrict the subset of allowable included files

![|400](https://remnote-user-data.s3.amazonaws.com/KxV_MGjFWbEKC4wnr9vezmBjGry5vMEGRw9fEiVboBrbpDPW90FUEWcQB5DQ6iaQQKfKuf_pp_ex8STz1ZOTs4G597Srafg99eWKWbY3fgUmGy8FLjePAwWBsxRfoqkS.png)

![|400](https://remnote-user-data.s3.amazonaws.com/cRfnefhWMqBglILjaHp4taajONI49FQ4_tYTzJDMR39-Fe8fCt4pqEAeh8buFSCfKHq8ltx1REDym59ht5CiJHCPeE4OmgTfPrk1eEKHm4Y0qWTJv1zR2L5sdyFxA8Uz.png)

![|400](https://remnote-user-data.s3.amazonaws.com/gMYxt8L22j-r3tA-6dVie001rV9-7YG67oHN4-IErCsCMIyETESr2dMqZQF7tMirGenPZhQSTktupgjD8fr6rAgrgjoBcFC22cEav0ZDp7O2kGv-zul6E_pX606pb6le.png)

![|400](https://remnote-user-data.s3.amazonaws.com/sBLDWvetbZpSIODzXDh2TS_tjDnqaAaUTCuWiUMygvM7BetZ5TFIzwhLNpW_vfXWCjye2f9X0KTOS-VeiTSB0nsCYRXcLr9Xs_TiX9q5UtUpJX7L5d_S8BMdZrYHRMSc.png)

# Cookies and Sessions

## Cookies
- Used for 'remembering' you back to the site later
- For stuff that does matter
  - Store it properly
    - Generate a token, that corresponds to something inside your database, so that you can lookup the token and find the user in a way that is unguessable and unpredictable
- But must not be possible to construct a cookie to log in to an account you shouldn't
- Need to be enough to log you in without your username and password
- More persistent than sessions
- For stuff that doesn't matter
  - Store in the cookie directly
    - E.g.
      - What theme are you currently using
      - How are you sorting your table

## Sessions
- The session ID is all that protects your server side data and your identity to the website
- Make sure it cannot be guess, predicted or manipulated
- You have a session ID on the client, which links you to the data store on the site, on the server
- Have a limited life
- Make sure your session is handled correctly

# Insecure Cookies and Sessions

## Insecure Sessions
- What happens when you log out and back in

![|400](https://remnote-user-data.s3.amazonaws.com/n1nj4-dZWkFwlF3KndrAppg0iafac0XV83IS32AyYK5aT5TsvP8SuwNQo8pjNQta-NuTTK8YfK6CzJCfYhTJMgT4p6JknFJMzi8fTMIXH8fGL93WVrSBNTHOwrVRpc8u.png)
- Can you log back in with an old session
- StatusMessage
  - Stores messages in the sessions on one page
  - Displays messages from the sessions in another page
  - If this is not working, then the sessions have been broken
![|400](https://remnote-user-data.s3.amazonaws.com/xI_NjdPoGZue22VCpUjGAAd3TbBEzGlmElQT71gYuaiO_f9IJW48B7nf1adIKT_JX4QvMkPX_mNCJLD13LGbAPaL20AZytHW-Rij2h_88xH1VZYeFALqn3QWDgMXkKfi.png)

![|400](https://remnote-user-data.s3.amazonaws.com/6J7UEfojAcCVznBE6hqdGNNQ2a2hXjuKi53y2rhKxVX0SxfI1vpxBzQ4l2si9qc_RJzFA_86hZmff5k0hvnJ3Xh-eTOV5RF3JduUh640StDrNfEIDPoDAudGghrENu0-.png)

![|400](https://remnote-user-data.s3.amazonaws.com/vWslpv1Ze6cZrce32ASH1dlVs13Bj0g_YUAvvoZgNPg7wPwJojf5eld84m16UdQ4XFN4aCe0mnh9xmnQwIxdi-UM4Re_gPuSZ9lLxoN7d1zs_bTE1z7bzKnJF5L0W57E.png)
- Could you guess another users sessions
![|400](https://remnote-user-data.s3.amazonaws.com/E_O8T-KCE7e-8_oe_TaMeHISW_Ry7WeNjsnkIq0aY5WcxODT9mJxI8rk6ViMZ_RJL02EeouxZfIJSeTXr3Ne7UlouDpKiQ2pfh135Aqf6uqZZ3Ck-lZzH7eByvpTez26.png)
- Look how the session is stored
![|400](https://remnote-user-data.s3.amazonaws.com/m9xdlFqkHJSFx4jHW-LswcvSeVEZ2OWd2Qdtu_7MAjMGFXrfUGaF4WI5BaLFJRmsIVoY-0Ty1-Pr31ftvYjmuo9c8KvsG2KbdUFpZsWpF3-stguksQvQF0M1o4MxlfDD.png)

## Insecure Cookies
![|400](https://remnote-user-data.s3.amazonaws.com/FJXqFgTRdvucYqXZcHrfOT9y0j46NpbBqo-ax29JIeOYEvwdR1HOmyYWn4eSiwArsoWoZ0bj5RXRQZ5yZ_3iVpCVBW0gNZvUdiQaj1ZTV-ND4U6-7qeRs4I3KhtwRQoG.png)

![|400](https://remnote-user-data.s3.amazonaws.com/zPKC_DtWSnqBL9Pef5K2pCF-M7FEN43WPJ5LsU3suG1DK7dQfZZuO1TFg2i2KNr2dRMcq-kUvaLuP3bKynzCXTBJGwmqDkmloTgW637yikQVeUA1s5elSwoOgvqFmE8l.png)

![|400](https://remnote-user-data.s3.amazonaws.com/S1jzFjKXc9hXStBZJw0-ZM8i1EEDT0WabYPwn3phRZjzhQRAkpfXkTJeXGSPnB_cg_NGQ_C67Uehf9RCVQkMXNkBjAZyiBGdr1VaIdTpde1QOx74oab-AYCSN41OyTKa.png)

![|400](https://remnote-user-data.s3.amazonaws.com/wDuzYkjzl5Y9wj1RSKdBlqFGBBfRKPRcwzQLrZOSNT-0gD0Msprc4QzFbH04mqi-YfQP2fWRUZs4sEEz273OaSFxtJQlJT8rSVDfreUuz_fR1VK5WbnZ6DyEDD4DSKYI.png)

# Open Redirects

## Look for redirects
- Can these URLs be redirected to other pages maliciously?

## $f3 -> reroute is used for redirecting
- Look for places where reroute is used with user input
  - ![|400](https://remnote-user-data.s3.amazonaws.com/XRr0odrGkOa7kj6qMjYeya-jwqLzeQOitlAmVAyG7zwUFbrk8rT30R3hK0e3sGQX66Q2EPDxm5EThU5mio2n8Y_ijO7BXw-5Pj5SDH1OjNawHw313DXEYBZ7ATx2VSDu.png)

# Email Functionality
- ![|400](https://remnote-user-data.s3.amazonaws.com/n767HyB7xP7a5sfv1m9uhphl6u5ygxAFhmJJ5gE_yqYcs07h_qphZU3jxwpDzVaRVIrrT3h6C2fVdgjctis1pSGME3l8W1TgZbF8QEuyeUK1dvnvtyzDw-M_aqAI7RHo.png)

# Brute Force

## How to fix
- Captcha
- IP blocking
- Don't annoy the users
- Use a library to help with captchas
- Add new things to the database
  - Make a model to handle the data
  - A table of blocked IPs
  - Create a utility class to handle it
- Find the IP address with `$_SERVER['REMOTE_ADDR']`

# Landscape and Policy

# Reference Diagrams - Host Assets
- Host assets are typically equipment that have an operating system and do not typically include firmware
  - ![|400](https://remnote-user-data.s3.amazonaws.com/3dyeN805cFU9oZYQ19rgMMKTrFzBUjrzhDPsKpovEyAOJgXYHQ0Xki9KjBz0P66wOTe_UFzak8a9zv0uwCDY9zjgshkXsckP07X14gxAnAMWJ1T-jPDliHHjalEfMYL1.png)

# Reference Diagrams - Network Assets
- Network assets are any asset that enable communication
  - ![|400](https://remnote-user-data.s3.amazonaws.com/Nk0qXXh9OUP6zLwKZAwnskNDnQ07NBFav7sf_1osIadWsz6GiTV21qXrjoH0DQRI7dFCtzbIerZRM_nyDGg5YKbMHlS07KOYEkm_UDhuQJbMT8oZS4sg7UM5HoK4snpn.png)

# Reference Diagrams - Stakeholders
- Stakeholders are persons involved in the day to day operation of the organization
  - ![|400](https://remnote-user-data.s3.amazonaws.com/KQ0zxReKU-h4yOn1K-EkwrbI9D3Wal0fLBbKBgWexPCkkC4QfvWEljOAj9cz0mdTODS21XgvznnSkbKPZJy4GTy6IGMRn_0V7HO2GgFDmbMOWATScYAmeL3ha4gliTuf.png)

# Threat Analysis
1. Attack model driven
2. Compliance driven
3. ![|400](https://remnote-user-data.s3.amazonaws.com/JIXJiQYQBlcHxgPBdwslg9cQBYWS6yl4KjcXtGlmwfANNvJN6gvfS6jtELYfnZjz-Kj6yditg5VdixL-vCVp0GwrpPuRhC48SGNi8Z-2TB6FDitqriMumTaGmY-vP3G8.png)

# Measuring Security
- SANS Endpoint Security Maturity Model Curve
  - ![|400](https://remnote-user-data.s3.amazonaws.com/eh2-YylNuD4yNper9SbXkUMtRDFmAr_XftvUT7kiMAjZHQzg1If040P_ZvcH8Gh7PcBO3xD22UPbKmRm7jFjtZPbS5m_ddBQmkjy7pGq1bVy8guaAKU2elm9QdeVBFvp.png)
- Cybersecurity Capability Maturity Model (C2M2) Maturity Indicator Levels (MILs)
  - ![|400](https://remnote-user-data.s3.amazonaws.com/1U56uQb8whS1ULaphxKCNzLJhMHxRD6CQxpsMidus_QG0BkGRnXuz1XXcis7iM5Re6_T24e_QmDtJf1qweMUKVt0f2xldg4cmFAiz2bKis4d2_4TBLbNCfzfSV9UErzk.png)

# Typical Reference Diagram
- ![|400](https://remnote-user-data.s3.amazonaws.com/hBojSeXmRuFypIDQ_HE3_0EkN_e1StLgE2-jjJ2-EwrFb4vZQFP6tmcbxMJFHuGX9MVA9OeuTcN2jxIuzX0E5xx0E1IJbtajhOiaV9ZowQNEcG6rVJ-8FJZ11l0qHQ5W.png)
- ![|400](https://remnote-user-data.s3.amazonaws.com/3ilmxK5C-c6qqW_E-HDkFtGwfw7UKL8FiCC5i6VZwDzaL07KEIWxvSCjlnzfR5WIK7LdmuHUrydDm4ob2-f-hRjB0-JVaXxPNVNVkfb2JiQ-TgtxYGbuNdptAHL-5n0g.png)
- ![|400](https://remnote-user-data.s3.amazonaws.com/zwCt1GVmgdP1QQ5QCPo7l5JNh2ZaBuJKhywVn0FF75m55uYkt_jVMIsOTOkLkpsjvaNe3YsLGmXf65nWAxoGMPWZ_oowiwYUYHbRn8UEelwgD5_AVzNT733F6gSA3rvZ.png)

# Reference Diagrams
## What categories do you need
1. Define hosts - machines
2. Define network - how connected together
3. Define stakeholders - the people

## Basic reasoning
- Reuse the diagram
- Illustrate threats
- Show impact on assets
- Show impact on stakeholders
- Manager infrastructure

## Advanced reasoning
- Show forbidden relationships
- Add monitoring nodes
- Identify host assets that need to stretch
- Identify persistent assets

# What is Policy
- Policy↔A statement that reflects the rules that everyone should abide by

# Good policies are organized as follows
1. Purpose
2. Policy compliance
3. Date tested
4. Date updated
5. Contact

# Frameworks
1. **Security Frameworks**
   - We mean compliance, such as: 
     - ISO 27001
     - NIST
     - BSI
2. **Security Models**
   - We mean models, such as:
     - IoT
     - Blockchain
     - Cloud

# Measuring Security
1. The SANS Endpoint Security Maturity Model Curve
2. Level 1:
   - Random, or Disorganised
3. Level 2:
   - ![|400](https://remnote-user-data.s3.amazonaws.com/LO63qD2b9d9y_Sb2vJT-T4zGPCc8OEyCDLTfJeWY_px4FX7Zj523gFRKradqyqv3JBf9QLAwx9QHMPERUpDoMhTVXx6ccPG8QwqPbXi0IumPCJJuj-mHVDzbozUoie_w.png)
