---
title: "Week 1"
---

# Introduction

## **What is a Database?** 

- Represents some aspect of the real world
- A logically coherent collection of data with some inherent meaning
- Designed, built and populated with data for a specific purpose
- Has an intended group of users, and some preconceived applications in which these users are interested

## Database System vs. DBMS
 
 ![|400](https://remnote-user-data.s3.amazonaws.com/udoGFcr7CEHlYnKWD2CTq7w7-KE0bOYMe3656h5GCU9WCz2WEulOLdBI2QRBxYbiJfS5jODVu3kdJWKB44iAWClGz8CHS_OQIW-rHsiaGIj3ovfyM6sQRVcu5AvLLK6m.png) 
## **DBMS allows the user to**

Define the database
- Specifying the data types, structures and constraints for the data to be stored

Construct the database
- Store the data on some storage medium that is controlled by the DBMS

Manipulate the database
- Querying to retrieve specific data, updating to reflect changes in the model of the real world, and generating reports from the data

## **What should the DBMS do?**

- Support sharing by multiple users
- Allow complex relationships between objects to be represented
- Permit multiple views of the data
- Control or eliminate redundancy
- Be self-describing/contain its own catalogue for metadata
- Facilitate backup and recovery
- Support data abstraction
- Promote **program-data independence**
- Control concurrent access to data
- Store data
- Restrict unauthorised access
- Offer various interfaces for data retrieval and manipulation
- Support sharing and integration of data between multiple applications
- Enforce integrity constraints on the data

# DBMS Architecture

## **DDL vs DML**

### DDL

Data Definition Language

Used for
- Manipulating database schema
- Creating tables, indices

### DML

Data Manipulation Language

Used for
- Updating table contents
- Queries

## **DBMS Interfaces**

Casual Users
- Interactive Query
 
 ![|400](https://remnote-user-data.s3.amazonaws.com/dpWR5UIsVlO8oXEj5DSsldkKvcyBvP3LP-zQvcOf45R4beLgVAA3030RfHff9ugBINA5lURbJJ2rjbsnnQ9yyq3xLpsT2tlct2OAJ0IVi4uHsPG3nwJ47-QAgtAHNPv4.png) 
Applications Programmers
- Application Programs

Database Administrators
	- DDL Statements
	- Privileged Commands

## **DBMS Components**

![|400](https://remnote-user-data.s3.amazonaws.com/n5HzvEh9tRysPSiLkRcjU-GzlHxOs8k9Idp4PGmzkRVQ43BiA176g0MhzZbUWvojdLUhatM4u_OPdmDH2H1zBjj2krWq3oUUqJF6MG3UedjpnwIs-9tHHhbLmRfHJDQj.png) 

## **System Catalogue**   

System Catalogue - Contains metadata about stored data and schemas

![|400](https://remnote-user-data.s3.amazonaws.com/L0IRqNjJK9g1fhWfErNLuaXLWtnO9_C8aOTtDFO-oaAwv-Aghw_ZIfNxvURKgjNq5JRr-KFub-I-LPGEmDegosgjwQhGXXVzCtiprdqzq-LHdC_qZi-xS62eUe75SYzv.png)  

Contains metadata about stored data and schemas 

Such as
- Names and sizes of files
- Names and data types of data items
- Statistical information 
- Mappings between schemas
- Constraints
- Storage details of files

## **DDL Compiler**   

Processes schema definitions 

Stores schema descriptions in the system catalogue 

![|400](https://remnote-user-data.s3.amazonaws.com/fwXLop3n0taWUWPGHoCK7kofVIV_zRmBir83FQdWeefxMiBKGvy45X09vM2uWZd170mfhdLxbVBgByvxye3VO1mPQt8J2bYPDZDlHLdGfa_IowT_4BMPy_hezgaPXx93.png)  

## **Query Compiler**   

Parses and validates queries 

Compiles queries to internal form (query plan) 

![|400](https://remnote-user-data.s3.amazonaws.com/DlLMUoRIuUNkllwE6YRC88cWpaM4WvOvaFbcFa6bCKsNeEYpgWDZ63Tjik2rduFDsesddDsDl1TDryC4CAWSmkjZTKsQppAPycVDajw3lNOMRQ8zp0eGc-SDmJbbsnKC.png)  

Passes compiled queries to query optimiser 

## **Query Optimiser**   

Generates executable code 

Eliminates redundancies 

![|400](https://remnote-user-data.s3.amazonaws.com/fCVV9LQbt8orOUHGisu9xejYScetOd6l3oRxg5XB-i_lNkMwM_Cu0v6qYY6vCwkPRchT4a3g2LoR4FsAD1ZQL5D_qW5vamh8bF4Jdhd683OOwEq3V7yV8kDGvcZ0ZUjh.png)  

Consults System Catalogue for statistical and other information 

Query Optimiser

Identifies appropriate algorithms and indexes used to implement operations 

Rearranges and reorders operations within query plan 

## **Precompiler**

Extracts DML commands from application programs and sends them to the DML Compiler

![|400](https://remnote-user-data.s3.amazonaws.com/8n0hko3npMXoFtjDH9XPRPQBcxKKJx5qUjjdSw9dXVS9SAU3df2AEu2XX4s903WhUI4nwGEsYcuOBbDGKNyZOKaPl9BXZCHqFAIf50jOJupZL5pb9mFhNfwXWsaik9pD.png)  

## **DML Compiler**   

![|400](https://remnote-user-data.s3.amazonaws.com/3SxZzLkJdsKXgn8-LnVvcUav8cFd4nkygpCno65i6SddJiTd5cytolqUpUj-zbTCYGa7UEyQ_5x1Mgr1FyPNXNKhDn1OFlF_0TKUPgAN1--alTrpiDM2ihHE6c8QyeBk.png)  

Compiles DML into executable code that can be sent to the Runtime Database Processor

## **Runtime Database Processor**   

![|400](https://remnote-user-data.s3.amazonaws.com/sJlXklQsNdGWwkDuHw9t4bPglsMi_21OnOn1w82pmx_rGORkSElmft0FT8vN9meKh4cXyEeLqnF8A0mROB08s1mm8guVfiEbsFNNBmASYvJbRijrAH4KSAWoRtcVPIIT.png)  

Executes query plans from the Query Optimiser

Accesses database through Stored Data Manager

Executes privileged commands 

## **Stored Data Manager**   

![|400](https://remnote-user-data.s3.amazonaws.com/Ef-czN30434zqzqfT_8UrOF-NFtSB0FmiqbsA7bD_R2GEgFaUHTKqM881iZFOauvA1YZVaJg4AO4klfdlz9Ne07LAGPB1xHoDavopkBLVu_Gp7G6eTy6pdoR8Xyh4xfc.png)  

Controls access to information on disc, using basic operating system services 

Manages shared buffer pool (available main memory used for transferring data to and from disc)

## **Other Component Modules**

Loading Utility - Loads files into DB

Backup Utility - Dumps DB to secondary storage (usually tape)

Recovery Utility - Deals with failure using backup information

File Reorganisation Utility - Improves performance

Performance Monitoring - Provides statistics for DBA to decide whether to reorganise

# Data Types

## **Temporal Data**

### Characteristics of Time

#### Time structure

- Directed acyclic graph
- Branching time
- Linear
- Periodic/cyclic

#### Boundedness of Time

- Time origin exists
- Unbounded
- Bounded at both ends

## **Time Density**

### Dense

Timeline is isomorphic to the **rational numbers** 
- Rational numbers have a partial order

Between each pair of chronons is a **infinite** number of other chronons 

### Continuous

Timeline is isomorphic to the **real numbers** 
- Real numbers have a total order

Between each pair of chronons is a **infinite** number of other chronons

### Discrete
Between each pair of chronons is a **finite** number of other chronons

Timeline is isomorphic to the **integers** 
- Integers have a total order

Timeline is composed of fixed periods called **chronons** 

## **Storing Times in a Database**

Various times may be associated with an event that appears in a database

Potential times
- *Valid Time* of a fact↔When the fact becomes true in reality
- Bitemporal↔Both *Valid Time* and *Transaction Time*
- *Transaction* Time of a fact↔When the fact is current in the database, and can be retrieved

## **SQL Extensions**

TSQL includes
- Retrieval of timestamps
- Retrieval of temporally ordered information
- Using the TIME-SLICE clause to specify a time domain
- A `WHEN` clause
- Using the `GROUP BY` clause for modified aggregate functions

The TSQL `WHEN` Clause
- Format of the `SELECT ... WHEN` statement
```SQL
SELECT { select-list }
FROM { list of relations }
WHERE { where-clause }
WHEN { temporal clause }
```

Temporal comparison operators
- FOLLOWS/PRECDES
- EQUIVALENT
- OVERLAPS
- BEFORE/AFTER
- ADJACENT
- DURING

## **Spatial Data**

### Characteristics
- Data volumes may be very large
- Data objects may be highly complex
- Access is likely to be through specialised graphical front ends; operator skills are key
- Query processing will (probably) not be performed using SQL
- Performance is not easy to achieve
- Data may be held in real time

### Applications
- Computer Aided Design (CAD)
- Computer generated graphics
- Geographic Information Systems (GIS)

### Operations include
- Overlap
- Containment
- Length
- Centre
- Intersect

### Data types include
- Points
- Vectors
- Regions
	- Quadrangles
	- Boxes
	- Polynomial surfaces

## **Multimedia Data**

### Image Databases

Mainstream DB vendors now adding
- Support for BLOBs
- Access using QBIC
- QBIC↔Query by Image Content

An image database needs to provide support for
- Image analysis and pattern recognition
- Spatial reasoning and image information retrieval
- Image structuring and understanding

### Image Data

BLOBs - Binary Large Objects

Images are classified as BLOBs

### Video Data

Most **consuming** format
- Frames typically played back at 24-30 fps
- Each frame can consume over a megabyte
- Images stored as a sequence of frames 

To integrate video and audio, interleaved file structure incorporate time sequencing of audio/video playback
- Microsoft AVI
- Apple Quicktime

### Textual Data
Text data is essentially unstructured, an index of some kind needs to be built
- Or automatically by building a inverted list of every significant word in the database
- By a human operator

XML (and predecessor SGML) allow a programmer to create portable documents that contain structured data

Could be
- Already in machine-readable form
- Or read using OCR techniques

CLOBs - Character Large Objects
CLOBs are now commonly supported by vendors
- Provision of text search and retrieval facilities
- Able to store and handle text documents in addition to standard data

Markup languages give some structure to a document

### Audio Data
MIDI
Consist of a sequence of instructions
- Note_On
- Note_Off
- Increase_Volume

- More compact than digitised audio
- Interpreted by a synthesiser
- MIDI↔Musical Instrument Digital Interface

Digitised Sound
- Consumes large amounts of storage
- Stored in various formats such as WAV or MP3
- Compression techniques normally used