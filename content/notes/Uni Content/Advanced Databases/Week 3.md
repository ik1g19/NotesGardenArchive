---
title: "Week 3"
---

# Access Structures

## Index Basics

Relations are stored in **files** 

Files are stored as collections of **blocks** 

How do we find tuples that match some criteria?
- Indexes
	- ![|400](https://remnote-user-data.s3.amazonaws.com/cYW1kNWAQxVEQQwTHZFdWCqHEXmnVjzVWCOuG0Jy6OJglOxlvKQdsUBRVE6aGRQabrDKWG-daxQd91MAThs0puHd_JIJMSzQ6fglbXIwTWLVXLo_tJH0zDFCr3kk1l0L.png) 

### Indexing Trade Offs
Maintaining an index costs time
- When entries are added to the relation, index must be updated 
- Index must be maintained to make good use of resources

The trade off is between
- Speed of updating the database
- Rapid access when retrieving data

### Sequential Files
Common to leave free space in each block to allow for later insertions 

Tuples are then distributed among blocks in that order

Tuples of a relation are sorted by their primary key

Blocks contain records that correspond to **tuples in the relation** 

## Dense Index

![|400](https://remnote-user-data.s3.amazonaws.com/zYCAkNBpVTntFOyoDyr9C7gXs1wiCVDYRJMirTS7gwuF94wrvsmKOYpB2C1ba9HHMicV-jaSptiQGtpsdrsmGhRZx5Jq0y2NcoTf0FIWOWSdrcR28riVP_1ZDIAepPba.png)

Sequence of blocks holding only keys and pointers to records 

One key/pointer pair for every record in data file 

Blocks of index are in the same order as those of the data file

Key-pointer pair much smaller than record

Fewer blocks than data file, fewer disk accesses

Keys are sorted, so can use **binary search** 

Can keep in **main memory** if small enough (no disk accesses)

## Sparse Index

![|400](https://remnote-user-data.s3.amazonaws.com/vyMN1X9rVvXRtG1I0StMbq1bp4XI5cC-PYwgSFZnBTSHAkCC6F4k8NzlHii515Kl_aWf_NfqISovHq7-oVwrlGlZ4zD24x5RJp855RTbGFIYyT-tlnZ6blo7XXY2zHAh.png)  

One key/pointer pair for every block in data file 

Can only be used if data file is sorted by search key

Uses less space than dense index

Potentially takes longer to find key than dense index

## Multi-level Index

Can create a third level index, but in general prefer B-trees

Use sparse index over the first index
- Can't be a dense index (would use the same number of blocks as the index being indexed)

Index file may cover many blocks

May still need many disk accesses

![|400](https://remnote-user-data.s3.amazonaws.com/iMC8Uu_btJxJLLojyRnyuW-w3eWLPolasrF_rZuxnPzF5wfQ5vcusvIMUta-FYgAGzw4Xkq8qRtgNYFZP2GdsZh608Rwwa5N2CBQUn2ViUatr7xwy9DUxMLh0FeLlQO2.png) 

## Notes on Pointers
If the file is contiguous, then we can omit pointers
- Compute offset from block size and key position
	- e.g. Assuming 1 kB per block and a pointer to block with key k1, to get block with key k3, use offset of (3-1)\*1 = 2kB

Block pointers (as used in sparse indexes) can be smaller than record pointers (used in dense indexes)
- Physical record pointers consist of a block pointer and an offset

## Sparse vs. Dense Tradeoff
Sparse
- Less index space per record, can keep more of index in memory
- Better for insertions

Dense
- Needed for secondary indexes
- Can tell if a record exists without accessing file

## Duplicate Keys
### Dense Index Approach #1

![|400](https://remnote-user-data.s3.amazonaws.com/CZr4obxuvRzNexHDOuop8C_OG9jj1nsukqxiOetsUtV0QTH1uHmBneeFSRi_o7o7DX48ptr1tqRD1XL9jw9YGxUAEubOe_nGE76vG-fJG1yoS-lDBukmabOcAaYc3d_4.png) 

There is an entry in the index for every record

### Dense Index Approach #2

![|400](https://remnote-user-data.s3.amazonaws.com/pdf_ibWK8nAuOHCoAr-QmKnLUodU10Ds-q8_vHjACZplZuR9A5lgaf8d_aiSdhWTf0Y_Fo7YXyZuDvOchZ3rygxD_CpmeE3XHgLXpt8a9sdMUTBKSYSqNrIquAfgZ4fN.png) 

There is an entry in the index for the first of each distinct record

Requires a smaller index 

### Spare Index Approach #1 ↓ 

![|400](https://remnote-user-data.s3.amazonaws.com/Ny5Pya7gQPJ2LTOPdPosgQmjKvHxztbdF4SPsKjG6Q_Xsvpw8selqcSKLygnCAZ0qz6UqRXBkNcktir7ljhvsSD1C9Nmhg_kpXRdRmBSnnTfgqn0FxPNOPmqqb19owvW.png) 

Can miss records

### Sparse Index Approach #2 

![|400](https://remnote-user-data.s3.amazonaws.com/cfhBxWfdwUNbZpBUvppALgqxqHFjZfWhEbAdr5Ciq0uVwRqzW1OrR2sI0dVtVsmS8jqsRXix34jvQvj5MqZzBq1lZdHu1b4L33LbZAm62pLdZUIWhop3Zq2XV8yENHfN.png) 

Index contains first new key from each block

Can exclude sequences of blocks with repeated keys by only pointing to the first instance of each value

![|400](https://remnote-user-data.s3.amazonaws.com/410-QQIsdio3Tl-h1YO_NA9WvLeeJ7CWW-yH7_Zd4igENz4nOrO-ySKCccCKUtGLJkGl8R52vc04ajmysimqWQmt7QirZvUNqQj-7AGkfsi5g3UrG6xI_oYXuCPgOBRh.png) 

## Deletion from Sparse Index

![|400](https://remnote-user-data.s3.amazonaws.com/BQoAn9WzVP0ylkx6_HDKisT973kn6UkZ_7ymAbklI5XcnHSj__AHUNXmDrmHb_0tuykXMZrAxpi44anDHsbTlw1OibcAUJQm42oJdZhMYjkKWXjUag8mKQatLe7jOKZC.gif) 

## Deletion from Dense Index

![|400](https://remnote-user-data.s3.amazonaws.com/Dt6jEi74BEh_rC5QEqnqw_GBtQfQaYFf1U8SiNpg9he0lL5bC9FNQmYDMV3RQJWS4_ZZYdiv4_w9IXO2NkLl4c2y3kxttZ4XuwW3cTRy4r4jpqxZj9jQaYXR1SVsx3Zq.gif) 

## Insertion into Sparse Index

![|400](https://remnote-user-data.s3.amazonaws.com/ur_P26efRp_A3kSRoA_PB68LhEKESRT3VK9e_fcNuagigZApT0LHRSvMZd7UbMtgumiuTUktJ2gbcaBc9ojVPfMtb_izqQ2Z_lgT7eVn_X7nFKlpzAbHeOujrNTs1Is6.gif) 

## Secondary Indexes

Unlike a primary index, does not determine placement of records in data file

Location (order) of records may have been decided by a primary index on another field

Secondary indexes are always **dense** 

Pointers are record pointers, not block pointers

![|400](https://remnote-user-data.s3.amazonaws.com/7fvFkd7bqP2kRuB-QN45yQ9iM0cz_Cb3vF4BMtxMxo5K1n0NxQFc4wvDxos8R0rQHlwElsx69jTwrE6xCukkkVsHg_pHk-rc-xYFZpHvT0mRLJOypoTU-nZRX9hJpW1G.png) 

Secondary indexes need to cope with duplicate values in the data file

#### Solution #1 - Repeated Entries

![|400](https://remnote-user-data.s3.amazonaws.com/PQ2tF1maoeB1srnOdTeFQjwrY3qLOWhxJODY5_NJGLE2wrl-Hj0C9LNHmtEtZURn6lMwzGAH89dNIDlKfNASaBTgP4xySEG5BLVhbw9BwPkh-xLc7OnDrBHYstAdyN4a.png) 

Problems
- Excess disk space
- Excess search time

#### Solution #2 - Drop Repeated Keys
![|400](https://remnote-user-data.s3.amazonaws.com/Cu18PnlCeaVB14UYo8Mm8g9-mEQph8J4Jm-jJxrlekY73iAjd66bS2u_EJ59bTT7uCftIjcY7-tIyLvshCdRICddSQxoqEn0Q4KAId-yvhy375zTImpAfienNVc5D8TK.png) 
Problems
- Variable size records in index

#### Solution #3 - Chain Records with Same Key

![|400](https://remnote-user-data.s3.amazonaws.com/28z9G8O2vqQ3U-h1KPSoVmN9h_tuI7hTQDEdjejlGA4lebq9ScNLrHtvmIhvAZeU8EB8t9HRZ5cxBFeOiJuzRsOjgJRtqkJcwbyGkgEuoFCJuyZWMSX9b2Px4VR2CBak.png) 
Problems
- Need to add fields to records
- Need to follow chain

#### Solution #4 - Indirection via Buckets of Pointers

![|400](https://remnote-user-data.s3.amazonaws.com/1K-LLDMC7Wtocr-Wdm3h9CnSPtndVcAQxUwm1kzoQCFzy-sYc-67bEpzrbzRYhlu-WLPoqXADjVmzxioMSnLHMEI5Ee3q_DByYPvufhD4o-s4RUw6tD9ineX_Aegu74u.png) 

Advantages
- Don't need to examine the data file
- If we have multiple secondary indexes on a relation, we can calculate conjunctions by taking intersections of buckets

## Conventional Indexes

### Advantages
- Simple
- Index is sequential file and good for scans

### Disadvantages
- And/Or lose sequentiality and balance
- Inserts expensive

## B+ Trees

Most widely used tree-structured indexes

### B+ Tree Deletion

Coalescing is often not implemented as it is considered too hard and not worth it

#### Case 4 - Case 2 - Coalesce with Sibling or Case 3 - Re-Distribute Keys at non-leaf

![|400](https://remnote-user-data.s3.amazonaws.com/xvN6TU-ckTqnCMlxf4AJiXVz1azTk01W90lmC2TXyDjE5NkYNqACykqCMjVb9o475yCwsW2br9L_dkjcXeIzJMLh_mS-VDY6L9d2bqzkJDuQeIvYrb6PXf7vSnhVP0zE.gif) 

#### Case 2 - Coalesce with Sibling 

![|400](https://remnote-user-data.s3.amazonaws.com/3V3TSslNJnY1ppbED9GxFxzNojSDOuoiujOpemQi8A7bwds-W-yr4_3_QPUYqgt3ROKzK7oPwKwT2BMmlm23etUEe1-hxFgKZrx4oV7TdZkKinPQJT1U4FmkGg6ttfit.gif) 

#### Case 1 - Simple Case

#### Case 3 - Re-Distribute Keys

### B+ Tree Arithmetic

Using:
- b - **Block size** (bytes)
- k  - **Key length** (bytes)
- r  - **Record length** (bytes)
- p  - **Block pointer**
- u  - **Initial node occupancy**, to allow for expansion

A leaf node in a primary index can accommodate **lp** records 
- Where  __lp__  = $\lfloor \frac{(b-p)}{r} \rfloor$

For a secondary index:
- A leaf node initially points at **ls \* u** records 
- A non-leaf node initially points to **i \* u** blocks 
- 2 levels of non-leaf nodes initially point to **(ls\*u)(i\*u)^2** records 
- 1 level of non-leaf nodes initially points to **(ls \* u)(i \* u)** records 

For a primary index:
- 1 level of non-leaf nodes initially points to **(lp \* u)(i \* u)** records  
- A non-leaf node initially points to **i \* u** blocks  
- Each leaf initially contains **lp \* u** records  
- 2 levels of non-leaf nodes initially point to
	- **(lp\*u)(i\*u)^2**records  
	- **(i\*u)^2** blocks  

A leaf node in a secondary index can accommodate **ls** records
- Where  __ls__  =$\lfloor \frac{(b-p)}{(k+p)} \rfloor$

A non-leaf node could accommodate __i__ entries 
- Where  __i__  =$\lfloor \frac{(b-p)}{(k+p)} \rfloor$

### Balanced multi-way tree
Yields consistent performance

Sacrifices sequentiality

### B+ Tree Insertion
#### Case 4 - New root

![|400](https://remnote-user-data.s3.amazonaws.com/bopR3ZbRsUsFuDJZHhvmCZhXuu4PKEkCUp6vEF7ZpJqt9zFpdAtpY_96acCJMAiD-hYBDX_nVkyy9sOYe611gqB6zVcOYe83d7PDrHyfV1C07H1SWHXzI7PSpphGYl8U.gif) 

#### Case 3 - Non-leaf overflow 

![|400](https://remnote-user-data.s3.amazonaws.com/EbOAYd5hrfazHvaiBLqgMuK9YegfgjuYtD37rE0fMSsU_W7Jc0IO7070d3J6sLgppv8IkpeHHWJjm_Xv3ZUKt9EFewBRGn5_XLS1m5duyYQUPMl2XJYx0MII9uVbD3dw.gif) 

#### Case 2 - Leaf overflow 

![|400](https://remnote-user-data.s3.amazonaws.com/pzNQjnKemY1MTuLqj75RYaFO8BjfwxnPiIWpjD0fTU3o7BEomeNK0XenfwxxG5rTYcTx8wTxtm6lMUI--kW4F_O7IKTPNMP8st39EnfW4ycgAVD_ixHpJzpkbLjyDZpH.gif) 

#### Case 1 - Space available in leaf 

![|400](https://remnote-user-data.s3.amazonaws.com/qPNUcpiD6LB9Tlh2NQGlUexkdEOBr6qT6xA4yWu0ODj6fCEXU3jo7SpxvJIn_j3JaWm5ZVrXdZNpkLQuGuyfcdpXAEQtcbn4e7FL65LFQ0ISWQOAOZjwpoZqRG_mOYPg.gif) 

### B+ Trees vs Static Indexed Sequential Files
#### DBA does not know
- How full to load pages of new index
- When to reorganise

#### B+ Trees
- Concurrency control is harder
- Consume more space
- Blocks are not contiguous
- Fewer disk accesses for static indexes, even allowing for reorganisation

### B+ Trees Rules 
All leaves same distance from root (balanced trees)

Number of pointers/keys for B+tree of order n 

![|400](https://remnote-user-data.s3.amazonaws.com/72WR9yGaPb7ZCGwW_88BzfyQpgC4zs0uFU_dgaTxKuEaEg6kGVSBOwduy9M8vm-6ekrIeHrMIWUamN7jM1gZpJL8WPuvKRPBtnRKNMUhLjxEevpm30nbbhYW4lZgJDit.png) 

Pointers in leaves point to records except for "sequence pointer"

![|400](https://remnote-user-data.s3.amazonaws.com/zjPOG8tSZir_oufj3UnJcK-OyTuX-QeeEgbLc_K118DF8j3ALoIjZ2qyUvi0zy6Mr2itbsvWiGX3U5EeK8AGgZhKo_poSTerjXonhhi24e4qpwTLcMUa9FlqoYvy7ljR.png) 

#### Leaf Nodes
- If the index is a primary index
	- Leaf nodes are records containing data, stored in the order of the primary key
	- The index provides an alternative to a sequential scan
	- ![|400](https://remnote-user-data.s3.amazonaws.com/O4OCg6X-pe902HoLDFdZAx9XBy7qaBIvk_Fmr50XZlP5Qir0xJGfqfOzRBFIhQ6dAQUl7z63ft6oFwblfem3SIrY4R57-BcCnspKw_ToZc0dK237xT3-GeC2O6HJHMJL.png)

- If the index is a secondary index ↓ 
	- Leaf nodes contain pointers to the data records
	- Data can be accessed in the sequence of the secondary key
	- A secondary index can point to any sort of data file, for example one created by hashing

#### Non-leaf Nodes
- Root node typically kept in memory
	- Entrance point to index - used as frequently as any other node
	- Some nodes from second level may also be kept in memory

![|400](https://remnote-user-data.s3.amazonaws.com/AJxyzFaEUqmdgEHCwQfjfHImDsy1OPKPFswzZ73BSOpkkLd1hW2Is9_sEcwSYY4eSAtme3CBQIB5XdjZXVo3LIDIDKeE74kszhjEA8x08myRnMuMWo-ALd_QXHsjspka.png) 

#### Node Size
- Each node is of fixed size and contains
	- **n** keys 
	- **n + 1** pointers

#### Minimum Nodes
- Don't want nodes to be too empty (efficient use of space)
	- Leaf -$\lfloor (n+1)/2\rfloor$ pointers 
	- Non-leaf - $\lceil \frac{(n+1)}{2}\rceil$ pointers 

Minimum Nodes Example (n=3):

![|400](https://remnote-user-data.s3.amazonaws.com/Vng7pQgZNi4X7ve88IjpGwf2PwLJ4wQw9FXKuVxsVMZX_8COQ6rAsPG-d26p7mxfZ1YbOlB9kK94rl8X5-4SbEfwItvEvbAZa_d4xM26Koz8zxbDcTgT1SO4WbCB6eRf.png) 
## Hashing
### Main memory hash table
Value is used to select a **bucket from a bucket array** 

Bucket array contains **linked lists of records** 

Hash function  **h()**  takes a key and computes an integer value 

### Secondary storage hash table
Stores **many more** records than a main memory hash table

Bucket array consists of **disk blocks** 

### Hashing Approach #1

![|400](https://remnote-user-data.s3.amazonaws.com/4wXNx3b1ju-tfHGFYshIVHGkhooeyV-zDS37t6m43b42fAWh9lfx2WcN2dD4-kf6OpCWVwS8MvRDZXo_OT1TWbskQ4qeg-AzFB3NTcLzjo_k3dwnAHhOL29MCSzKP6Xi.png) 

Has function calculate block pointer directly, or as offset from first block

Requires bucket blocks to be in fixed, consecutive locations

### Hashing Approach #2

![|400](https://remnote-user-data.s3.amazonaws.com/HINHg3DgUSR0fBYIfnF55qVUKsK68kbuDFHqYlZh3y-ZBmBNYiRmHgMS2cSHIlB_IaVC6Buwdr4uFoHB0qIqaKhI1Azdbs-M-NlShPqlKymNCkv82tvZGNfHoLaNjKUP.png) 

Hash function calculates offset in array of block pointers

Used for 'secondary' search keys

### Good Hash Functions
Good hash functions have **the same expected number of keys** per bucket 

Keys are kept sorted in buckets if **CPU time is critical and inserts/deletes are relatively infrequent** 

### Hashing Example

![|400](https://remnote-user-data.s3.amazonaws.com/ApwBHDVzoxIc_Ki7CmKh0naJZOOboSw_d4QLKQyQoig_33Pmdrc3YWvvVjmlAtJrdTl2NfX2gVwG3lGTIHpWZdkXGbL-SON7mthozQZirk9MWGqbCNsdImK3sE0SFmOH.gif) 

### Rule of Thumb
Space utilisation should be between **50% and 80**%

Utilisation = **#keys used / total \#keys that fit** 

If < **50**%, wasting space

If > **80**%, overflows significant

### Dynamic Hashing

Used to cope with **growth** 

#### Linear Hashing

![|400](https://remnote-user-data.s3.amazonaws.com/_-7kAl3vP7fRQRSWax7tUf71oBj81M48u0mUCotr0hOdEx6mN5ZtKo9gqukANGyZS456Iq9s8-OV0aCQmcQRE7bmSNBSkWif4mpuE6Af9WxkrEDEd68My7oJH6zAAQQP.png) 

Combination of two ideas
- Use  **i**   least significant bits of hash
- Hash file grows incrementally and linearly
	- Unlike extensible hash file, which periodically doubles

##### Example

![|400](https://remnote-user-data.s3.amazonaws.com/xw7Rgs09zfRditPwz_YYui4M6kN0VHoD98mstiGSxnk6PXbWOzxcJNhem7PfZt3ZldKDuUgN34oFp03xKAEGxx2Qc4t7jSSUwHzEnxSiWsrLTecTE6qpHwRzBcG2b7qv.gif) 

Lookup Rule
- m is the greatest suffix associated with any bucket 
  
When to expand file?
- If U > threshold, then increase  **m**  ( and potentially  **i** ) 
- Utilisation (U) = \#used slots / total \#slots

##### Disadvantages
- Can still have overflow chains

##### Advantages
- Can handle growing files with less wasted space and no full reorganizations
- No indirection like extensible hashing

#### Extensible Hashing
##### Disadvantages
- Directory doubles in size
	- Suddenly increases in disk accesses
- Indirection
	- Not bad if **directory in memory** 

##### Deletion
- No merging of blocks
- (Reverse insert procedure)
- Merge blocks and cut directory if possible

##### Combination of two ideas
- Use  i of  b  bits output by hash function, where  __i__  grows over time

![|400](https://remnote-user-data.s3.amazonaws.com/2iUHZ8KQIZqKYQDNxf1pU18dKKRS_n_ozRfuYyWjMesvMYAzMmsFplGhti_ch4KGPxE8KUl01-h4MYlp2t61cbL4tQ8-wbu2J2KoCWbBX0z_HkRfuSm1j5k4T8D_ja6s.png) 

- Use a directory

![|400](https://remnote-user-data.s3.amazonaws.com/LW5_MB2V7F0z4sAqpmt0bKL_g5FBQxc5hmnHnDDFH3Z2yaJ-jikbKHcw7HqCUpOt9dhn-TJ5XWc-t21989zgKnDzNjwG4Zju5G_njJrW5PXhyOeOaqbm_yDjVTsZ4CY6.png) 

##### Example

![|400](https://remnote-user-data.s3.amazonaws.com/e-CYk338s-1BRAfed33AuKTjUw9ZpKK-9e_9TVg6fE1xFM9tFsnrqGOq6oV4I28qBt8zz_nphFi43VFDdjiiWYBXj8lopRC8UKwm82kH_4DMpHRtge4zpAl_vxyccF4g.gif) 

##### Overflow Chains
Chaining overflow blocks when many records have duplicate keys

![|400](https://remnote-user-data.s3.amazonaws.com/ozZ7oQlSM33IiUDlmE9mSB5AizlS6ehgc0J4SThWC4HF2dpyROCTqfvlDHmcKyc-kAgRT1wW5Zrk9lmTEGDrhnAy-yaXiY9hGlbq-eZBqMt53acT3a3HXDGnI16Qx44F.png) 

##### Advantages
- Can handle growing files with less wasted space and no full reorganizations

## Indexing vs Hashing
Hashing is good for **probes** given a key

Indexing (including B-Trees) is good for **range searches** 

# Multidimensional Access Structures

## One dimensional indexes
Assume a single search key

Require a single linear order for keys (B-trees)

Require that the key be completely known for any lookup (hash tables)

## Applications of Multidimensional Access Structures
### Geographic Information Systems
Nearest-neighbour queries

Range queries

Partial match queries

## Grid Files

![|400](https://remnote-user-data.s3.amazonaws.com/u6HUicGE4avUkuvbY39MR2ybgTZWVZJg7ZqITl4SpaPvMjt_RIILAjMYSTtKXT5rTZMvkPi57fHjymQnVhA0bVQjGEs801YTnlzLeuiWDap_MkB4c9bTi-w9KyBB-sI6.png) 

Each region is associated with a pointer to a bucket of record pointers

Partition multidimensional space with a grid

Fixed number of regions
- Overflow buckets used to increase bucket size as necessary

Grid lines partition space into **stripes** 

Intersection of **stripes from different dimensions define regions** 

**Attribute values** for a record determine the region and therefore the bucket

### Advantages
- Good for multiple-key search
- Supports partial-match, range and nearest-neighbour queries

### Disadvantages
- Space, management overhead
- Need partitioning ranges that evenly split keys

## Partitioned Hash

![|400](https://remnote-user-data.s3.amazonaws.com/hETPqr9jSI0dYbjEMQpdBa7qi14BnM0MjB0gNa9pvm7lAfOMkGOf03ejDQtSrY6UIIFX4U5w_hfGVwOEwGRv9OEhjc-UxaRe9ym5qbCQDMr4uynwTRwiqTKjRxngSES-.png) 

Hash function takes a list of attribute values as arguments

Bits of hash value divided between attributes

Effectively a hash function per attribute

### Examples

![|400](https://remnote-user-data.s3.amazonaws.com/CYdJfkY8zvhZy5vfi9bHtkNtt0xhQpvk15MOGru6EZl3lZTfPAikDf5Dd2RpyBasGSiq66iAlXeE2RnjXCbeSLyiYaTXBFootUar8hpDbb7xVmnB_XUYVtlA4kaPwz-n.gif) 

### Advantages
- Good hash function will evenly distribute records between buckets
- Supports partial-match queries

### Disadvantages
- No good for nearest-neighbour or range queries

## KD-Trees
Multidimensional binary search tree

Each node splits the k-dimensional space along a hyperplane

Nodes contain
- An attribute value pair
- A pair of pointers

All nodes at the same level discriminate for the same attribute 

Levels rotate between attributes of all dimensions

### Example

![|400](https://remnote-user-data.s3.amazonaws.com/aE8McSblNWRnwwZlzre9ZiVN2vAE1Rp-FEzIHr-9bWJod37l4pqsvEovEC-dzbKLnzmAZsMayqm11liUbj4fXmGPQGxxNqsUpbiBXlZHPxjE6Fu_y48xch7r9v5hDR_t.png) 

### Partial Match Queries
If we know the value of the attribute, we can choose which branch to explore

If we don't know the value of the attribute, we must explore all branches

### Adapting KD-Trees to Secondary Storage
The average path length from root to leaf is $\log_2n$

Disk accesses should be kept as few as possible
- Approaches
	- Group nodes in blocks
	- Multiway nodes (split values into n ranges)

## Quad-Trees
### Region Quad-Tree
Each partition divides the space into four equal area sub-regions
- ne, nw, se, sw

Split regions if they contain more records than will fit into a block

![|400](https://remnote-user-data.s3.amazonaws.com/w8jhHMP4o-Kt70TsTEuwNihaHQNiij8y6P8eQfgvQGxCD0RijuUUIlGSuCY21_xMTnYObFRn_Ft6Hr3ks6zef1jD30jSIQQstxQouGKJyk7R_HzxJP70UleiQjp1298d.png) 

Operations similar to those for [KD-Trees](Advanced Databases/Week 3/Multidimensional Access Structures/KD-Trees.md) 

### Point Quad-Tree

![|400](https://remnote-user-data.s3.amazonaws.com/DMVOht21glVHEwWAJlPt3X15ZBcfR04mBZ_jRa-JTYH9FYugoAT2dZusXd7G_K2gfk_seTei9UBmbvjZ8CgMRq06vfpn1ffQH9us3xJ3QLcMjHSfZxmunn0DRWd-nTDv.png) 

Partitions are not equal area
- Split lines centred on data points
- ne/nw/se/sw sub-regions

Otherwise equivalent to [Region Quad-Tree](Advanced Databases/Week 3/Multidimensional Access Structures/Quad-Trees/Region Quad-Tree.md)

## R-Trees

![|400](https://remnote-user-data.s3.amazonaws.com/ksGJOH2ILYBpYAXDY2HL26Y54Le6IFdzzOOCaKOXV-DtQli3nhehfnPgqmKctJsiWr2eW-gdFXVBdN73utiqFEnFuTGzIQdpU-u_AiX3uMImcaDUzEyhGq1UNIUrfyNd.png) 

Used to represent data that consists of k-dimensional data regions

Internal nodes of tree represent regions that contain data regions

Regions typically defined as top-right, bottom-left coordinates

## UB-Trees
### Z-Region Partition

![|400](https://remnote-user-data.s3.amazonaws.com/hfNsK3Of2Diu85RbGEo1cU_IGpXet7CLUAxq_sV_NjHVBNFZ4wSfFu0VenUyYJ89gCgUEGBmmli1zqDZw9BYY5cWs9lm3UNZzCGR-tpKD54yPgDBWennuolBSjfEu9ds.png) 

Z-Regions→Z-curve partitioned into contiguous regions
- May not be contiguous regions in the multidimensional space

A leaf node contains pointers to records whose attribute value locate them within the associated Z-region

[Z-Regions](Advanced Databases/Week 3/Multidimensional Access Structures/UB-Trees/Z-Region Partition/Z-Regions.md) mapped to leaf nodes of a B+tree

### When Querying
When querying, identify regions of n-dimensional space (e.g. segments of 1-dimensional line) that intersect with query rectangle

Partition ranges and index using a B+Tree

![|400](https://remnote-user-data.s3.amazonaws.com/DXgCfCOIJLh0TlyECsOOs4f2LDrunS-EO_yxHuzDAjQCOJvum_egZ3F5qEZJ8gPFNa0ZvcRqn7ekRuyPKgF60IphnC_YqNDtsbIzlTtmQ4gsvIUfmPGTomIRSUd60EWX.png) 

Map n-dimensional space onto a 1-dimensional line using a fractal space-filling curve

### Z-Index
- $y=y_1y_2$
- $x=x_1x_2$

Order of points on Z-curve given by bit-interleaving the positions on the axes
- $\text{z-index}=y_1x_1y_2x_2$

![|400](https://remnote-user-data.s3.amazonaws.com/lbP-ccpPQbl3BimO4DlYvsUwPFtBQWn39im4TL95uJ3iN31BTFG93cFBoM3_d9y9YMNYwNvwpccuPrwPEpoc_B1GsXeb1_2NYIaVIbjD5OpntYKzyJ8PLMu1gRuxX59E.png) 

Map domain of each attribute onto n-bit integer

### Querying UB-Trees
Algorithm identifies [Z-Regions](Advanced Databases/Week 3/Multidimensional Access Structures/UB-Trees/Z-Region Partition/Z-Regions.md) that intersect with the query rectangle

![|400](https://remnote-user-data.s3.amazonaws.com/itTv9ewkQ8OmhwVcSrT-tr-dKQoZAxtM0zX79-r28RyA_tu0NU6xndlLWXui8P3bXYzerqJqhCzGeBDOU4iS16AI9x_U2eh1dC28yRR3jIJu1fBR_O8o1Ud80wmLIk88.png) 

Multidimensional range query can be considered as a k-dimensional rectangle

## Bitmap Indexes
Collection of bit-vectors used to index an attribute
- One bit-vector for each unique attribute value
- One bit for each record

### Advantages
- Efficient answering of partial-match queries

### Compression
Bit-vectors are typically sparse, with few 1 bits
- Run-length encoding of bit-vectors to reduce stored size
- Large amount of wasted space

Bitwise operations must be applied to original bit-vectors
- Can decode RLE bit-vectors one run at a time

### Querying index involves combining bit-vectors with bitwise operations (&, |)
A 1 in the  **i**th position indicates that record  **i**  is a match

#### Example

![|400](https://remnote-user-data.s3.amazonaws.com/SBogJweGUk5AXLquy6X0UFbpfd0eezf0XsEoPAI-lEebG91W0KvlV20wJPi5xfpdPavKS_q9FBZIf9h7GPKpfiKHvfNM4dFQdjUGXqaR3C1AW6cMFJEkBucj3gPRxA2T.png) 

![|400](https://remnote-user-data.s3.amazonaws.com/VO6bnYuA4bsh5aMdtSqIiaUeUNdDcJ1OnRnzbMM9sBgAI_2unkkuD_JbuzALDvS676IPmtDEumkTW-boiOLNmBLYm8U32ALa-VAXoDYo-ez7NTn1nsdHq4iIZUW-qqYq.png) 

### Disadvantages
- Requires fixed record numbers
- Changes to data file require changes to bitmap index