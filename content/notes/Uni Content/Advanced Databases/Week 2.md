---
title: "Week 2"
---
# Data Storage

## **Storage Organisation**

### The Memory Hierarchy

#### ![|400](https://remnote-user-data.s3.amazonaws.com/790H96pqTwXe87FP-fF2IR63fF4ouzgtgyLzesnkCPQtxdSgNknnKIXbtmS7STWhnM4Rl52i_ml7nUYIja1zKNUK3d9enZgKL4t5wrquQ7bPgbbSef6URDyTa85nXd8m.png) 
#### Cache
- Volatile storage
- Limited capacity
- Very expensive
- Hierarchical
- Typical capacities and Access times
	- L2→~10^5 bytes, 5-10 cycles
	- L1→~10^4 bytes, <5 cycles
	- Registers→~10^1 bytes, 1 cycle
- Very fast

#### Tertiary Storage
- Very cheap
- Typical access time→ $10^1-10^2$s
- Very slow
- Typical capacity→10^{13}-10^{17} bytes
- Very large capacity
- Non-volatile storage

#### Secondary Storage
- Non-volatile storage
- Typical capacity→10^{11}-10^{12} bytes
- Typical access time→10^{-3} s (10^6 cycles) 
- Large capacity
- Slow
- Cheap

#### Main Memory
- Typical access time→10^{-8} s (20-30 cycles) 
- Fast
- Affordable
- Volatile storage
- Medium capacity
- Typical capacity→10^9-10^{10} bytes

## **Secondary Storage**

### Hard Disk Drives

#### Typical Storage medium for databases

#### ![|400](https://remnote-user-data.s3.amazonaws.com/8h-pM9sYNhEVZCWLgJ1nlaEN-F046PXi8GUzN5q7hWIW9VUcA0hDDFwyS_SowtQOGIU_Nm0Lq3su43xl9fX1r0hX4JWjnIK5sGUTHqZiWNFO4VQaj9Xmxl6fUGogvleD.png) 
#### Disk Structure

![|400](https://remnote-user-data.s3.amazonaws.com/KzwA2Uj2N2HXcQFwrlw937Nxxb-IGwfMDVRltn97EOSUikyJve7l-P2o7gsw3435JTsBah_VzlixRO2nSQuAvVr1MEKj-_eCmXZEh6bcuIRTiNgWXouccqjL25g5GMXr.png)

#### Zone Bit Recording

![|400](https://remnote-user-data.s3.amazonaws.com/X60VKbc8Q1TzCRLGqdjHnyM8peG-MMJldCCwgw1PkoxoqMsyvhaI3mbButgr0VP3qsaJb7zsM36-iAyfKCtb9yWq46NoH6etccAtop4jP0wREQ1pRb1whdBXn8CSVbL5.png) 

Tracks closer to the disc edge are longer than those closer to the axis

Bit densities vary in order to ensure a constant number of bits per sector

Instead, we can vary the number of sectors per track (depending on track location)
- A hybrid of constant linear velocity (CLV) and constant angular velocity (CAV)
- Improves overall storage density

#### Disk Sector Format

![|400](https://remnote-user-data.s3.amazonaws.com/lXX0vgj3hB9JIr09qJGlLcYdpBMh8hbYmn9_1ZdNVQU1hh6benTJu2zS1l7fwRq7Q1HeEl9nJSXdZH9Ao6AWA24i8Gq3ScZNTOLPBLzJcVaOmCacOnOqBZv0TTiHIOCk.png)

Terms
- Gap↔Separator between sectors
- Sync↔Indicates start of sector
- Address Mark↔Indicates sector's number/location
- ECC↔Error Correcting Code (may be distributed)

For 4k Advanced Format
- Gap+Sync+Mark = **15** bytes
- Data = **4096** bytes
- ECC = **100** bytes
- **2 . 7**% overhead 

#### Disk Access Time: Reading

![|400](https://remnote-user-data.s3.amazonaws.com/yA1CVmesqLWX__Cc3r6Ve99ZNit3m0G3vsa7z2N2cqPzJY-1BMr8vE2xI8YVy3NSlKduf5_rth--bkqroDV91_aGr5EO6w5EoJBfM8JdVeoH3xhtMx-scT2iwFB1jRYc.png) 

Access Time = **Seek Time + Rotational Delay + Transfer Time** 

#### Seek Time
Time taken for head assembly to move to a given track

![|400](https://remnote-user-data.s3.amazonaws.com/XkgwIl3aKMvYKxItwJKA8OmErWBFXarYqN9MFKUqn7kgIli6__xpi5HqgAJDFNt4xJcF5ZEpUtvFbf0CH5J6j6S8hi70Utxb6S9D_C6vL0aeNBuV3jE4ZIIEAT-iEJSB.png) 

Average Seek Time Range
- **4**ms for high end drives
- **15**ms for mobile devices

#### Rotational Delay (Latency)

![|400](https://remnote-user-data.s3.amazonaws.com/ZfSpiTUBPxDP2fToVu1_HnXofsJRyJhv2DTMB_heZsZqHd5U0gnCRXs8CSNqS32u75juqPmk5D-Efi93v3zrpLTh9I7JUV5sVF_RON5lhcHwRnmoW9uQ-ZBA09m224Oz.png) 

![|400](https://remnote-user-data.s3.amazonaws.com/Y238Em7A4r-yHiGWatBQh-nVMGZGWIjeE-DdPlx5ivhNsnWB25nehX3O07mJz48F7syTXZKZC6IUvQuimq9q7-qitTs596Vs1GYR9GI_ONZ-2xMN5oz5ExnKaLe3a105.png) 

- Average delay→time for 0.5 rev

#### Transfer Time
- Transfer Time = **Block Size / Transfer Rate** 

#### Sequential Access
- Access Time = **(Block Size / Transfer Rate) + Negligible Costs** 
	- Negligible Costs
		- Switch to adjacent cylinder occasionally
		- Skip inter-block gap

Switch track (within same cylinder)
- In general, **sequential I/O is much less expensive than random I/O**

#### Disk Access Time: Writing
- Costs similar to those for reading, unless we wish to verify data
	- Verifying requires that→we read the block we've just written
- Access Time = **Seek Time + Rotational Delay (1/2 rotation) + Transfer Time (for writing) + Rotational Delay (full rotation) + Transfer Time (for verifying)** 

#### Disk Access Time: Modifying
- Read block
- Write block
- Access Time = Seek Time + Rotation Delay (1/2 rotation) + Transfer Time (for reading) + Rotational Delay (full rotation) + Transfer Time (for writing) + Rotational Delay (full rotation) + Transfer Time (for verifying)
- Verify block (optional)
- Modify in memory

#### Block Addressing
- Cylinder-head-sector
	- Physical location of data on disk
	- ZBR causes problems (sectors vary by tracks)
- Logical Block Addressing

###### Blocks located by integer index
- Allows remapping of bad blocks
- HDD firmware maps LBA addresses to physical locations on disk

#### Block Size Selection
- The size of blocks affects I/O efficiency
	- Big blocks **increase** the amount of irrelevant data read
		- If you're trying to read a single record in a block, larger blocks force you to read more data
	- Big blocks **reduce** the costs of access
		- Fewer seeks (seek time + rotational delay) for the same amount of data

### Solid State Drives
- Typically based on **NAND flash** memory
- Typically **smaller** maximum size than HDD
- **More** expensive than HDD
	- Getting cheaper over time
- Considerably **higher** I/O performance than HDD
- **Asymmetric read/write performance (writes are slower)**
- Limited number of **program-erase cycles (~100,000)**

## **Buffer Management**

![|400](https://remnote-user-data.s3.amazonaws.com/S9jK-vxd0mBVQuFMVbtbxIUbTN5WKfSM7gy-Bltps3nGiIiYjMKdGcgn8TeNwbaoJJ1tAEOaDRDnga0TF9RlnuMv7pomT_94fIXhUz69ALMsb3lHGK6ooavJMqUeiMVx.png) 

Buffer pool organised into **frames** 
- **Size of database block + Metadata** 

Far more blocks of secondary storage than space in main memory
- Need to be selective about what's kept in memory

### Buffer Metadata

#### Each frame in the buffer pool has
- A Pin Count
	- Pin Count↔Number of current users of the block in that frame
- A Dirty Flag
	- Dirty Flag↔1 if the copy in the buffer has been changed, 0 otherwise
- An Access Time
	- Access Time↔Optional - used for LRU replacement
- A Loading Time
	- Loading Time↔Optional - used for FIFO replacement
- A Clock Flag
	- Clock Flag↔Optional - used for Clock replacement

### Buffer Replacement Strategies
A frame will not be selected for replacement until→its Pin Count is 0
If there's more than one frame with a pin count of 0→use a replacement strategy to choose the frame to be replaced
- Clock↔Cycle through each buffer in turn, if a buffer hasn't been accessed in a full cycle then mark it for replacement (Approximation of LRU))
- FIFO↔(First in First Out) Select the frame with the oldest loading time
- LRU↔(Least Recently Used) Select the frame with the oldest access time

### Single Buffering
Read B1 ⇒  Buffer
Process data in Buffer
Read B2 ⇒ Buffer
Process data in Buffer...

#### ![|400](https://remnote-user-data.s3.amazonaws.com/POgbKUbhfKRyz2zRXTUM6PMlilpCJZRaOy47xuZEO2zzt_31eIlRQZTUysSgHQH90nkiGZRth8hqmMZwwvzvjBtqX-yOnFSa43fwr0v0DBtxzfVXUY4mfMgnfGzd7q9N.gif) 
#### Single Buffering Cost
- Single Buffer Time =** **$n(R+P)$ 
	- Where
		- $P$→Time to process a block
		- R→Time to read a block
		- n→Number of blocks

### Double Buffering

#### Double Buffering Cost
- If time to process a block > time to read a block then
	- Double Buffer Time =**R + nP** 

#### Use a pair of buffers

![|400](https://remnote-user-data.s3.amazonaws.com/Ti3NB9bf-kbZxr2ZCt0XL0CrXGOMGZEUbvTEqFb3lj6rbmlIAIHqlz2WrOmUwHGN7YVoNfr85TPbaS4MRNpGdPX9UaQTkMQUQkkwBiKUIJ97w4Zyn8HcuUyJVgDgGvtU.gif) 

- While reading a block and writing into buffer A
- Process block previously read into buffer B
- After block read into A, process A and read next block into B

## The Five Minute Rule

Data referenced every five minutes should be memory resident

### Assuming a block is accessed every X seconds 
CD=$\frac{\$D}{XI}$
- Where
	- XI→The IOs the unit can do in X seconds
	- CD→Cost if we keep that block on disk
	- I→Number of IOs that unit can perform per second

### Assuming a block is accessed every $X$ seconds
$CM=\frac{\$M}{P}$
- Where
	- CM→Cost if we keep that block in RAM
	- \$M→Cost of 1MB of RAM
	- $P$→Number of pages in 1MB RAM 

### If CD is smaller than CM
Otherwise, keep in memory

Keep block on disk

### Break even point is when
CD = CM

### Examples

#### Using 1997 Numbers

![|400](https://remnote-user-data.s3.amazonaws.com/xQaei4fDAX05jRoLGTf96QTMfiNRmBFnJbGfhoEAr9PvPG1ydl51-aXFyikEf29h0jzkbSETFqpMaOv75BQJ3HQ_afwWsEn3MO6KanxOejxyOwBdorXPr0grxJrveXjK.png) 

#### Using 2016 Numbers

![|400](https://remnote-user-data.s3.amazonaws.com/o3eLQmCKvwLM5Mt6zNRi-gjgPCenb2n9DcJwq05NX0z-rCfJz_KhxzFUA47374lXPL7b850alyjD2Th445SZTZ1pbzm7LvL1n25EPbWg08rRpCaUYzaeF5xW3X1JVXUI.png) 

#### Using 2007 Numbers

![|400](https://remnote-user-data.s3.amazonaws.com/zAty2a75O1CdLepl4HE5DzEPutITbTqmNjSkkrvgcHKKbt8Hpe6uwbZnwbBUcOMOsLE2266V2u7CRyL95uBvBJEsjyh3-_yXc34r2XxDGXrpSidsOAA9JssvysxAb9MF.png) 

![|400](https://remnote-user-data.s3.amazonaws.com/PFm4vN7jILKgGoJcUR9467Ke_gZNJO7PpeIuaYO6X_HD67MP0aIV6xtHFYRyReoCT_aGa2SVsXBszUZv2A5bCG8J2Z36GDbLr3Mp59NsydzwM8cljIw6UJ30zFuVIlgm.png) 

## **Disk Organisation**

### Data Items

#### Representing Times
- **Seconds since midnight** (integer) 
- ISO8601 times
	- HHMMSSFF (8 characters, to represent fractional seconds)
	- HHMMSS (6 characters)

#### Representing Characters
- Various coding schemes such as
	- utf-8
	- ASCII

#### Representing Numbers
- Real Numbers
	- m bits for exponent
	- Floating point
	- n bits for mantissa
	- 1 bit sing
- (Short) Integer→2 bytes

#### Representing Dates
- Days since a given date (integer)
	- 1st Jan 1900
	- 1st Jan 1970 (UNIX epoch)
- ISO8601 dates
	- Ordinal dates→YYYYDDD (7 characters)
	- Calendar dates→YYYYMMDD (8 characters)

#### Representing Booleans
- 1 byte per value
	- False - 00000000
	- True - 11111111

#### Representing Bit Arrays

![|400](https://remnote-user-data.s3.amazonaws.com/iSJSlT3dxWIoMpoIk8VYD8DBLD9IOyvMdtefF_-tiLpvQT6Zcbo-xwNQlCChxkllL0aUguvC6aDLxObuAjsKu_11JUCNiw9GETs86M1XtofT5iYcvx5jczDWNSwAcNqh.png) 

#### Representing Strings
Length given

![|400](https://remnote-user-data.s3.amazonaws.com/juyfvfvI-q7HboT-aHp4L5vpHmSt2pMV23zVu_0jfR99OIrRTlqlBG8XU9_KZyFD-ZX5Sz_1T28q9Vmi4mklN7CSj6GcfFLSB02aZHlBe93YOeyGgADTQG1uwqICY9tM.png) 
Fixed length

![|400](https://remnote-user-data.s3.amazonaws.com/bW5e7gl41XzLCi9VKrIGRVmWcKErIayoov_M02pIMGLMthGafQy3KqBLuQEnWroLrAqr1TInAxnAP4comE7vvovPnadpcqe8rJbkwyUEntUISAiwKSsVvZL9RlpPhbDa.png) 

Null terminated:

![|400](https://remnote-user-data.s3.amazonaws.com/j3Duq4GS2q-ak6S1QEj9sekyb41Bb1Fx2FR5c1AgcC8qRv4cT0ByC3JD7NbuqwuwKX4wqA1XAFe_34csYdz4WjtsvYi9M_xPIw2U1SM9BqwvHRU_d7mIzsxmBJcnH0eq.png) 

### Records

#### Fixed Format Records
Example
	- ![|400](https://remnote-user-data.s3.amazonaws.com/2AJuCsHD_jIsmXxpHP0HLP8she4T2XQQPswtwyTuhCHBEN-LTBcH-GxBsh_rHdoUwHeL2rnmW3Lh2pwN9Cu1_vI_VyvbxP8nbr99nu0gn0rFKLszYMqKeCaBg9Li7uAj.png) 
Schema describes the structure of records
	- Order in record
	- Types of fields
	- Number of fields
	- Meaning of each field

Record format that **does** contain a schema 

Fields - Related data items 

Collection of Fields

#### Record Headers
- Data at the beginning of a record that describes the record
	- Such as
		- Record length
		- Timestamp
		- Record type (points to schema)
- Intermediate between fixed and variable format

#### Variable Format Records
Example
	- ![|400](https://remnote-user-data.s3.amazonaws.com/sWjWPbbYRDumAe2rrqbGSU0O51ctPTSC5oXNYtHfUtaaBFjDLTyPYQAoIaWmACTXyNlqQyP2hNbPa0I9ca6e2IkaSEh-gT4-LINWrjjvFl33UKIlrahKTYKNy0Fao07F.png) 
May **waste space** compared to fixed format records

Record format that **does not** contain a schema
	- The **record itself** contains the format

Useful for
	- Repeating fields
	- Evolving formats
	- Spare records

#### Blocks
**Records** are stored in blocks in memory

A collection of blocks makeup a **file** 

##### Block Header
Data at the beginning that describes the block

May contain
	- Pointer to free space
	- Record directory
	- This block ID
	- File ID (or RELATION or DB ID) 
	- Timestamp
	- Pointer to other similar blocks
	- Type of block

##### Placing Records in Blocks
Considerations
- Indirection
- Sequencing
- Separating record
- [Spanned Records ](Advanced Databases/Week 2/Data Storage/Disk Organisation/Blocks/Spanned Records.md) vs. [Unspanned Records ](Advanced Databases/Week 2/Data Storage/Disk Organisation/Blocks/Unspanned Records.md) 

##### Separating Records in a Block
Approaches
- Give record lengths (or offsets)
	- Within each record
	- In block header
- Use fixed length records - no need to separate
	- Use a special marker to indicate record end

#### Spanned Records 
Records may be split between blocks  

![|400](https://remnote-user-data.s3.amazonaws.com/CEMbeTe62yKKrykKE2au9zwfTJS3oISNy-8wt1iiUcKyVXvwzQzAXzs0TbxUEXpNNCdRuPtpDv1nUnj7a-iUZTdeBADQFh_Db3NxJ2JD3Pa5u4h3DYy24kZuUclun5Oa.png)  

#### Unspanned Records 
Each record must fit within a single block 

![|400](https://remnote-user-data.s3.amazonaws.com/VjE-0mMcQegvgC1sA-hbkAKlGHDvs4m0CgpVWjq2PG7KTwtS8BSyk5aoMooe3d4Z8vGZGpvV-lBV4Z7KJRcGCOXIPvKtEqLVW6nNrx6kxfJA1HtScu-3g9OzRsfLkj9d.png)  

#### [Spanned Records ](Advanced Databases/Week 2/Data Storage/Disk Organisation/Blocks/Spanned Records.md) vs. [Unspanned Records ](Advanced Databases/Week 2/Data Storage/Disk Organisation/Blocks/Unspanned Records.md) 
**Unspanned records** are much simpler, but may waste space
**Spanned records are essential if record size > block size** 

#### Sequencing
Makes it possible to **efficiently read records in order** 

Ordering records in file (and block) by some key value

##### Sequencing Options
Next record physically contiguous

![|400](https://remnote-user-data.s3.amazonaws.com/abeVc2S3BR_3bcLKVo4EuHhOXa6SxSo4f7vN8bGXvLVp1bmAP98fp8HDqiuUHLY5U7jzBpxDZFpl4RhGlWSa8M-KgSNxeARP3PigVsOqkySQrmetKPkfAk-T_V-mEHcO.png) 

Linked records

![|400](https://remnote-user-data.s3.amazonaws.com/rZBK36a1ASNlsSODoNcTnYaT9i6ldEAMtyuYJb-C_pzquXfk_GrvwltiikzSMGzPJqeoubOvWZSKet7t3WfVl-WMfhoTX4Wn_tg60E4tGhDEybAOftd7NE71C-mWdS2m.png) 

#### Indirection

##### Indirect Addressing

![|400](https://remnote-user-data.s3.amazonaws.com/1Nw_lVV6oLjtG08_GSD37AFwwSpThpPWWgH8l9ps75O7f5_TuuE9fe8fZZiCorTPSEmu-QJNKlLZ3tcFCnBarHewvzZa5yfD7C8S-YA4JxQ4x1IuyWy7xlo1cv6PQasf.png) 

How to refer to records

##### Physical Addressing

![|400](https://remnote-user-data.s3.amazonaws.com/5h9Q7RTZVpB-DFbkL7-CfC92I7shC22HZNldX62TCQ6iDLK1xI6O3fxx6f-oL_v0qB_dX-TkOa2faMwRL_MsLouZvRmUQ_ikEo0xZNQ_8T6r4pE8Jf0z95CvoUkB3ZAM.png) 

##### Indirection in Block
Records can be shifted within block without changing record ID
Access to a given record ID is fast - only a single block access needed
![|400](https://remnote-user-data.s3.amazonaws.com/9DnEcTNJCoJJRueRphu8oH4FnsCy-nSD27IqG_Icsp2izE0bEhob44mS9JRS7iVr8vRpauMeaqL1SLkR2lVOX3CHDz3qxnpOv_Dq5UjWj0HhJYnnBZTW8On-HeLfoVJj.png) 

#### Address Management
Every block and record has two addresses
- A database address (when in secondary storage)
- A memory address (when copied into a buffer)

##### Translation Table
When in a buffer, using **only memory addresses** is more efficient 

Maps database addresses to memory addresses

![|400](https://remnote-user-data.s3.amazonaws.com/gf0gv7ALODA9wJjuIbeful4N9H-H0DUFuLpbP_u3zygDCsLh3SbGM-kAGLpvs2XAvaaMBFGio3Xwr9XhTxeQ1qmD1tvgar783X2wMbcNL5dzb2RvEr0EpVBPIcAWyDzH.png) 

##### Pointer Swizzling
General term for techniques used to translate database address space to virtual memory address space

Translation Table is used to **convert pointers** (and to record the conversion)

Swizzling

![|400](https://remnote-user-data.s3.amazonaws.com/lod_q8pNMl62w3u8BkWyh8bgbisvAXEXmfUs0Zb6JJGbHcWK0BK0oxymM1p2Z3K6rP12uYusf7WNEhz92OJHHIP5SDcbH1E1Nf4ELyl7kHiQs5v0UqsK3yDVHvq37P-y.gif) 

###### Swizzling Strategies
Automatic
- Replace pointers in blocks with new entires
- As soon as block brought into memory, locate all pointers and addresses and enter them into translation table

No Swizzling ↓ 
- Use Translation Table to map pointers on each dereference

On Demand
- Leave all pointers unswizzled when block is brought into memory
- Swizzle pointers only when dereferenced

Swizzled pointers typically consist of
	- One bit to indicate whether the pointer is a database address or a memory address
	- A database or memory pointer, as appropriate

###### Unswizzling
Rewrite memory addresses as database addresses
- Reverse of the swizzling operation

Done by using the Translation Table in the reverse direction

The Unswizzling-Unpinning Relationship
- However, a block may be pinned if there are swizzled pointers that point to that block
- In order to unpin the block (to allow the frame to be reused), we need to unswizzle any pointers to that block
- Blocks in the buffer pool are pinned to indicate that some part of the DBMS is using their contents

#### Insertion and Deletion

##### Deletion
Or mark space as deleted

###### Deletion Marking
May need a chain of deleted record (for re-use)

Need a way to mark deleted records, such as
- Delete field
- In map
- Special characters

###### Deletion Considerations
How do we deal with dangling pointers?

Tombstones
- Leave a mark in a map or old location
- Physical IDs
	- ![|400](https://remnote-user-data.s3.amazonaws.com/-rKO6VQfwywOsnPen3zhIkfkB_OpCox9NIk9Pw-gonVw_LwyyBPX3muDuRMgiFhF2Q3drEZESRbafPUNd5wp4cSmYviHIZMJXClr1HHwAjRtb7c9aDE3WTWSRhxFY8LI.png) 
- Logical IDs
	- ![|400](https://remnote-user-data.s3.amazonaws.com/sWeunCCmyh7BdBba0gG6Vcur31EDnSItkALcOqq9byfMQapPNNShkslyBgVs6PD-QsDn0kepnXPD8347fNdo57K9MHCGmeaeWT-wYREatl4r7To8OKTOGkBCG4xq4B6u.png) 

Immediately reclaim space

##### Insertion
Records in Sequence
- Not too hard if free space is "close by"
- Or use overflow

Records not in Sequence
- Harder when records are variable size
- Insert new record at end of file or in deleted slot

Insertion Considerations
- How often should we reorganise files
- How much free space to leave
	- In each cylinder?
	- In each track?
	- In each block?
- 