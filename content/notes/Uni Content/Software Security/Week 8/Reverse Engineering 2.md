---
title: "Reverse Engineering 2"
---

# Reversing Process

Reversing sessions can be divided into two separate phases
- System-level reversing: large-scale observation of the earlier program
- Code-level reversing: more in-depth work

# System-Level Reversing

System-level reversing techniques help determine the general structure of the program and sometimes even locate areas of interest within it

System-level reversing involves running various tools on the program and utilising various operating system services to obtain information, inspect program executables, track program input and output

Most of this information comes from the operating system, because by definition every interaction that a program has with the outside world must go through the operating system
- Reversers must understand operating systems

# Code-Level Reversing

Code-level reversing techniques provide detailed information on a selected code chunk

Extracting design concepts and algorithms from a program binary
- It is a complex process that requires a mastery of reversing techniques along with a solid understanding of software development, the CPU, and the operating system

Code-level reversing observes the code from a very low-level, with every little detail of how the software operates
- Many of these details are generated automatically by the compiler and not manually by the software developer
- Reversers need a solid understanding of the low-level aspetcs of software

# Reverse Engineering Applications

Security-related reversing
- Malicious Software
- Reversing Cryptographic Algorithms
- Digital Rights Management
- Auditing Program Binaries

Software development-related reversing
- Interoperability
- Developing Competing Software
- Evaluation Software Quality and Robustness

## Malicious Software

Malicious software, shortly malware, spreads so much faster in a world where millions of users are connected to the Internet and use online services daily

Malware developers often use reversing to locate vulnerabilities in operating systems and other software
- Such vulnerabilities can be used to penetrate the system's defense layers and allow infection

Malware analysts dissect and analyse every malware that falls into their hands
- They use reversing techniques to trace every step the malware takes and assess the damage it could cause, how it could be removed from infected systems, and whether infection can be avoided altogether

## Cryptographic Algorithms

### Restricted

In restricted cryptographic algorithms, the secret is the algorithm itself - Once the algorithm is exposed, it is no longer secure

Reversing makes it very difficult to maintain the secrecy of the algorithm
- Once reversers get their hands on the encrypting or decrypting program, it is only a matter of time before the algorithm is exposed
- Because the algorithm is the secret, reversing can be seen as a way to break the cryptographic algorithm

### Key-Based

In key-based algorithms, the secret is a key
- Users encrypt and decrypt messages using keys
- The algorithms are usually made public, and the keys are kept private

This almost makes reversing pointless because the algorithm is already known

In order to decrypt an eccrypted message, you would have to either:
- Obtain the key
- Try all possible keys until you get to the correct key
- Look for a flaw in the algorithm that can be employed to extract the key or the original message
- E.g. side-channel analysis

## Digital Right Management

Digital information is incredibly fluid
- It is very easy to move around and can be very easily duplicated
- This fluidity means that once the copyrighted materials reach the hands of consumers, they can be moved and duplicated so easily that piracy almost becomes common practice

Traditionally, software companies have dealt with piracy by embedding copy protection technologies into their software
- These are additional pieces of software embedded on top of the vendor's software product that attempt to prevent or restrict users from copying the product
- These technologies are called digital rights management (DRM)

By using reversing techniques, a cracker can learn the inner secrets of the technology and discover the simplest possible modification that could be made to the program in order to disable the protection

## Auditing Program Binaries

One of the strengths of open-source software is that it is often inherently more dependable and secure
- Impartial software engineers inspect and approve open-source software
- Certain vulnerabilities and security holes can be discovered very early on

With proprietary software for which source code is unavailable, reversing becomes a viable (yet admittedly limited) alternative for searching for security vulnerabilities
- Reverse engineering cannot make proprietary software nearly as accessible and readable as open-source software
- But strong reversing skills enable one to view code and assess the various security risks it poses

## Reversing in Software Development

Reversing can be incredibly useful to software developers

For instance, software developers can employ reversing techniques to discover how to interoperate with undocumented or partially documented software

In other cases, reversing can be used to determine the quality of third-party code, such as a code library or even an operating system

It is sometimes possible to use reversing techniques for extracting valuable information from a competitor's product for the purpose of improving your own technologies

## Interopability

Interoperability is where most software engineers can benefit from reversing almost daily

When working with a proprietary software library or operating system API, documentation is almost always insufficient
- Regardless of how much trouble the library vendor has taken to ensure that all possible cases are covered in the documentation
- Users almost always find themselves scratching their heads with unanswered questions

Using reversing, it is possible to resolve many of these problems in very little time and with a relatively small effort

## Developing Competing Software

It would never make sense to reverse engineer the competitor's entire product

It is usually much easier to design and develop a product from scratch, or simply licence the more complex components from a third party

When it comes to highly complex or unusual components, they might be reversed and reimplemented in the new product
- But some legal implication

## Evaluating Software Quality & Robustness

Just as it is possible to audit a program binary to evaluate its security and vulnerability, it is also possible to try and sample a program binary in order to get an estimate of the general quality of the coding practices used in the program

Software vendors that don't publish their software's source code are essentially asking their customers to "just trust them"
- Buying a used car where you can't pop up the hood

Reversing would never reveal as much about the product's code quality and overall reliability as taking a look at the source code, but it can be highly informative

# Is Reversing Legal