---
title: "Week 8"
---
# Parallel Databases

## I/O Bottleneck

- Access time to **secondary storage (hard disks)** dominates performance of DBMSes
- Parallel Databases increase I/O bandwidth by spreading data across a number of disks
  - Have the ability to split processing of data and access to data across **multiple processors** and **multiple disks**

## Parallel Architectures

### Monolithic Architecture

![Monolithic Architecture Image](https://remnote-user-data.s3.amazonaws.com/9ab8b42rC-RcMOeKCb-PHBkorY6ZWXedrj709t-7RMvnT1YFED79atGfUEm4rQ9L1SuyEDW1-4mnjTzVi5Tynut7AEEhA6oM5R_f-BQ5_Rpok6m_Yq1LxL_q52pkhJyd.png)

- Single Processor (P)
  - Tasks may be interleaved
  - Not true parallelism
- Single bank of memory (M)
  - Used by transactions
  - Buffer pool for staging data to/from disc
- Single disc

### Shared Memory Architecture

![Shared Memory Architecture Image](https://remnote-user-data.s3.amazonaws.com/hLB9mIr60tkUXpNmIdz73M6IdN0MeJ1KzaQFaiqjJ_fZlzciXd6dUPpjuRjV0njM4bdgdc2eH90KRE0LwIkjKVtj1TznQ03JRZmp_WEliOSuErEOIrpPxID4wjfQRB4l.png)

- Tightly coupled
- Symmetric Multiprocessor (SMP)
- Software
  - **Less** complex database software
  - **Limited** scalability
  - **Single** buffer
  - **Single** database storage

### Shared Disc Architecture

![Shared Disc Architecture Image](https://remnote-user-data.s3.amazonaws.com/LywK5DbzeewRSBH4sovm_3aS1w2x_99lIsTMPE-LeritPRcDNuId5KQ76uchJHd6Ed__b8cBSd1HWlrmMAG4zbbge-MuSCAxyp974VdBHcdnOlUSNFN1dt8WYpHJB0pV.png)

- Loosely coupled
- Distributed memory
- S=Switch
- Software
  - Avoids **memory bottleneck**
  - Same page may be in **more than one buffer at once - can lead to incoherence**
  - Needs **global locking mechanism**
  - **Single logical** database storage
  - Each processor has its own **database buffer**

### Shared Nothing Architecture

![Shared Nothing Architecture Image](https://remnote-user-data.s3.amazonaws.com/NiXpvaaBllOUaDMvM6wcVTdBQf3IMV4e-yktoR2YdMig0aVCl3MtT0trXiNhnHStQWuGROm3MLdEQpIVr-pmRhg3rtB69FBnCTzhBWZjQcMBdXfWvpvyOhzeCeBY4Bm7.png)

- Massively parallel
- Loosely coupled
- High speed interconnect (between processors)
- Software
  - Each processor owns part of the data
  - Each processor has its own database buffer
  - One page is only in **one local buffer** - no **buffer incoherence**
  - Needs:
    - Distributed deadlock detection
    - Multiphase commit protocol
    - To break SQL requests into multiple sub-requests
- Challenges:
  - Partitioning the data
  - Keeping the partitioned data balanced
  - Splitting up queries to get the work done
  - Concurrency control and avoiding distributed deadlock
  - Dealing with node failure

## Parallel Query Processing

- Dividing up the work
![Parallel Query Processing Image](https://remnote-user-data.s3.amazonaws.com/AGkV--Scx2xXjQcazlEZ6wuvOfjT6g48yTZnvdx4MYbtLaeLyOy-Leb-sLmAQ7XjC0rDUeuSkedmE5jBQSFUiVgSlbEoHOX56daiHcPUYzn3WteckMGu7u5fRFkxqYg-.png)

### Inter-Query Parallelism

- Different queries/transactions execute on different processors
  - Improves **throughput**

### Intra-Query Parallelism

#### Intra-Operator (Horizontal) Parallelism

- Operators decomposed into different operator instances, which perform the same operation on different subsets of data
![Intra-Operator Parallelism Image](https://remnote-user-data.s3.amazonaws.com/Hi_RyYAM8TWFeCfAgWLkvJPw5i7VCYR8HEjgsMwhwgeJhw54j-Bz0xRoVJotR699NYzBuR2xYyLijVZqNmL8Xwhn2jTktCS3vI2g56K_MOUopa8Fy3O3LXHWC3qigZPM.png)

#### Inter-Operator (Vertical) Parallelism

- Operations are overlapped
- Pipeline data from one stage to the next without materialisation

#### Bushy (Independent) Parallelism

- Subtrees in query plan are executed concurrently

## Intra-Operator Parallelism

### Partitioning

- Decomposition of operators relies on data being partitioned across **the servers that comprise the parallel database**
- Partitions should aim to **spread I/O load evenly across servers**

#### Range Partitioning

![Range Partitioning Image](https://remnote-user-data.s3.amazonaws.com/z-TDze1FggyBtYW7bstU2ed0yiaiI53jTgr6em7Gm1QOGys3B_ue-oU651jWM3fHYWmikoSKvATNP_YwgHtyFz8B9R9HCgkobT_4JV9VxFIS6xLOVsn05OYmtJVVcGej.png)

#### Hash Partitioning

![Hash Partitioning Image](https://remnote-user-data.s3.amazonaws.com/it8xYMz__t-NKydAagoR-Fmr3VkwGtNYDDFEYLO8-zZ28nZxOl0IitaO9BLl8E1jl5UyVaHAf64yhxGtwGbuRip7kP-4rdQmI7S7GxCYLuOx-8fRtPKMHviMDqz0VGKl.png)

#### Schema Partitioning

![Schema Partitioning Image](https://remnote-user-data.s3.amazonaws.com/wGeNsZ-Mqdj4Rzw84WWNPwaTLKwMRh5boVAeGF32xWq-5xln8F2_MNAIl4HetWtkhHL9o2ZEy5QO3xmzFMTPBEoF7YDDuub-33Or15aqctk2KzJIX8JJ9vsDyQZ4eYop.png)

#### Rebalancing Data

![Rebalancing Data Image](https://remnote-user-data.s3.amazonaws.com/n62w-RBleaBKBNmcYfL5xM0AO5JLTrjbJXAgcsnNkQ5Juvr1jOUAVjuefvpFN5hw3fUNZY_ZdIMXpnBfA0uDeekh0iWDgEJeam9g3zPf5xNAxt3ZofBdi48BrIe1obco.png)

### Example Query: $SELECT c1, c2 FROM t WHERE c1>5.5$

Assuming: 100,000 rows, predicates eliminate 90% of the rows

#### Data Shipping

![Data Shipping Image 1](https://remnote-user-data.s3.amazonaws.com/mKBGx81j-l7GO960ZI0C0Sa6VyOozbs27x0RBB_FElDQCYkoBHO8ssyneXamiVI6efswP9sfJIrX6E6P8HT9k1WAUVZ89aaunrJ2wGbmnKyDB9tbl_vxQZMJEYmxgUhN.png)
![Data Shipping Image 2](https://remnote-user-data.s3.amazonaws.com/uZiUh_mrsQ5oAD7AGFkjMRvCYDjnr_TS6Cri5N8i6t1GpUdcE8JTtV70XQGzlQ3gBMrqKzRGhevq7XxX8y8o4Yb0JYVbcBcyLBZ9ls7OuMaaIUxzGruedlomMx2q6VNp.png)

#### Query Shipping

![Query Shipping Image 1](https://remnote-user-data.s3.amazonaws.com/HxHvD7yHlscSLKmRSizMs8vOTmVQf4s7Vao3GdtL_dzqBYd0cv4cXCk6goZV1XhDuh0PQXw0kHciGyEVOZcO2mdhFOF4EnP6oB5LTyarw78bdr5ytyB_2k9wK-qxYgXR.png)
![Query Shipping Image 2](https://remnote-user-data.s3.amazonaws.com/MQk9tVB8SQ7v41rdL7kkPZPjEtg5W6lqJANTYdS56EOFQ-5DlRzOv8tWuRg3OlACQ3NJH3-U7pGu9P8lc9MwKa187x3_IxwXBgzhwPjVlbW9qSCTR5vLYcLpx7p37xcm.png)

- Benefits:
  - Network traffic is minimised
  - For basic database operators, code developed for serial implementations can be reused

## Inter-Operator Parallelism

- Allows operators with a producer-consumer dependency to be executed concurrently
- Results produced by producer are pipelined directly to consumer
- Consumer can start before producer has produced all results
- Best suited to single-pass operators
![Inter-Operator Parallelism Image](https://remnote-user-data.s3.amazonaws.com/phRVbL4vEB2a-PThOcT16hivaLZLoNJ-OJFd58AY1p1_HFw_NnCXiHJ5dRNB7M40mEd-H8KkYIFByfGXDLq6M0zMJD5bdM0IFzhei87QnPwYzr4l1olBOQpXMOmrTXB7.png)

### Intra-Inter-Operator Parallelism

![Intra-Inter-Operator Parallelism Image](https://remnote-user-data.s3.amazonaws.com/ejtj_P2ScbCK88iSZ1Km1jW0rKd_PJGWYvV5psYtx-NewkODRZ6xaadP9C-Hi3tM9GAmrMWOAQA65p6c5Tu7mOpffWgGxrFPEcyczb48qF-naoChQuKEYphDLCS46arh.png)

## Volcano Architecture

### Exchange Operator

Inserted between the steps of a query to:
- Pipeline results
- Direct streams of data to the next step(s), redistributing as necessary

#### Example Query
![Example Query Image 1](https://remnote-user-data.s3.amazonaws.com/3CgLHF3E4K_2lIDbvsBJs4aWALdRotWqw-X0VDUuyFYv5hCJQzIvLVJUK56uNJkJeeomB2eJ3n2u1dY9xR9tY0nCjE4QMfeEnzM8OkmYhMO35vQ9fjuMdoXkrxpScT7c.png)
![Example Query Image 2](https://remnote-user-data.s3.amazonaws.com/DrX1op7yfGSVnRl2MsDVQ2k4ZIRjSLp84h_PGkbS3CU1y-klLP8VVcVuhh3dz1Oo7QAGk5Oxrx835q51w3IJllfFo9adbc4B94uF06p3MAGGDyCKgsQYokvloaQVMLxq.png)
![Example Query Image 3](https://remnote-user-data.s3.amazonaws.com/rseSFoe5_rpP5a8qy2Xb-fOntbkB9AVMVBpszAipJISpZYWA7gNEnduzWxqmoQawYacM4HcjNfqUcVOF9pXrUZHlq_GYw8HCm7Xzz3_0C-oqBfRDzx1B0BbnVicXsEdu.png)
![Example Query Image 4](https://remnote-user-data.s3.amazonaws.com/qyZBh0OlePwrxmKtzKDAUyyywajR7fFKDZWB9U3MLtyCwu8o11wr8wrdXFpYwNLfdwjPU2D955clMbOesdTtOapI5zgDEMaX_jfMtltYrR0-g8BFkKKMVim5_hUxm-xd.png)
![Example Query Image 5](https://remnote-user-data.s3.amazonaws.com/9o6EjKyDUBFpyIQsUTwMZjcLGdn8_LeMjcSyZ6XKliAOad1ppzSxKv3IAHTCZHHmEcCNjFaMxC4qjGR2MCPkwY9yXQdBsnE5J985B0V5ODZS0h11CwGKXXR0BZa8ggsM.png)

## Bushy Parallelism

Execute subtrees concurrently
![Bushy Parallelism Image](https://remnote-user-data.s3.amazonaws.com/5jYUHxoP4wtwnInvFJUh4tHYqPwNsahFVsivnaEaVwxUzX7dTH-3mpyoxq_kwCE8nzq9fXzXtY7SztkOYkb6AgNk56oS6gAdQvTchdVQaSxfbsb-2zTUlToNqj7j8qNj.png)

## Parallel Query Processing

![Parallel Query Processing Image](https://remnote-user-data.s3.amazonaws.com/EjayCtrjmFg5TiO8LXj7LhJ--HsRPxscMSULQ-7XBnz5tYiPClpGY0etdT-3yQ4JctnOYDXg2EB8gVz5TD1rIq4cR41jccwxIa3I4aj0utvfhFi17iEOWM0pTE8M8XsF.png)

### Enquiry/Query without Join

1. Count matching tuples in each partition
2. Pass counts to coordinator
3. Sum counts and return
4. How many customers live in the UK?
![Enquiry/Query without Join Image](https://remnote-user-data.s3.amazonaws.com/67Bn5jqY_dVUbaqsINrDmJOXmxM5SfKGciugS8bAln3FhqaAvCaPaqfWm3trpNkYVLqNo79wfPVY3Zv9kf4rf5ycoAc3iibSXP1vEZ5gKbINE7XbZaZ3SAeVtR2wh_ZA.png)

### Co-located Join

- ORDER, CUSTOMER partitioned on CKEY
- Therefore corresponding entries are on the same node

1. Join CUSTOMER and ORDER on each partition
2. Pass joined relations to coordinator
3. Take union and return
4. Which customers placed orders in July?
![Co-located Join Image](https://remnote-user-data.s3.amazonaws.com/Di627c9KKUXeUb8uQAM1qfc6R6GfkGAOIfte3QeYtKFqIlGiqFgBDy21NvWh1aMragoBrQ3jx1YoV0rKl0Cg5Xwbj7TjwCys_qOushf0Drwz3Hw6k2PMUV-bU_tXiqa6.png)

### Directed Join (Parallel Associative Join)

- ORDER partitioned on OKEY
- CUSTOMER partitioned on CKEY

1. Scan ORDER on each partition
2. Send tuples to appropriate CUSTOMER node based on ORDER.CKEY
3. Join ORDER tuples with each CUSTOMER fragment
4. Send joined relations to coordinator
5. Take union and return
- Which customers placed orders in July?
![Directed Join Image](https://remnote-user-data.s3.amazonaws.com/qM8gClzgnh7ed93FFwpj8UUmYyuWt_TSqCJhi_TDmYn5bQM8GUD6qvKJRLKsbsy8zpcQRSjB9JT2KNOSkz8bGNd-KVrdXPeiwhtsRMXk4bOGPByMRqzZWwhf1tG6xng1.png)

### Broadcast Join (Parallel Nested Loop Join)

- SUPPLIER partitioned on SKEY
- CUSTOMER partitioned on CKEY
- Join on CNATION=SNATION

1. Scan SUPPLIER on each partition
2. Send tuples to all CUSTOMER nodes
3. Join SUPPLIER tuples with each CUSTOMER fragment
4. Send joined relations to coordinator
5. Take union and return
6. Which customers and suppliers are in the same country?
![Broadcast Join Image](https://remnote-user-data.s3.amazonaws.com/aqNur4HE1l5A0HpGf2wYkFuBFwnTJdU2SAXAPELATO6-aLDZ37gkCse8gSSKx_p6Lepp3KwcdALnLi8M5t5vC7Y557otWlMoAjGDB_9BDl2h5izfgvfaoUAWRuY0Deyc.png)

### Repartitioned Join (Parallel Hash Join)

- SUPPLIER partitioned on SKEY
- CUSTOMER partitioned on CKEY
- Join on CNATION=SNATION

1. Scan SUPPLIER, CUSTOMER
2. Repartition on *NATION and send to appropriate worker for Task 3
3. Join SUPPLIER tuples CUSTOMER tuples
4. Send joined relations to coordinator
5. Take union and return
6. Which customers and suppliers are in the same country?
![Repartitioned Join Image](https://remnote-user-data.s3.amazonaws.com/qBkQObhtziJpyPzsQ4LZ1M-35tsZrFwSkTLlB_tE7OmNP4Z-dguzQKoYBkVFKOyUVNITYrfL2jvdZLX2hW7He_uAtd17o6rk5DOmbTNRUSQF34gWu5Q3xNLDJLh7WnXz.png)

## Concurrency Control

### Concurrency and Parallelism

- A single transaction may update data in several different places
- Multiple transactions may be using the same (distributed) tables simultaneously
- One or several nodes could fail
- Requires concurrency control and recovery across multiple nodes for:
  - Locking and deadlock detection
  - Two-phase commit to ensure 'all or nothing'

#### Locking and Deadlocks

- With Shared Nothing architecture, each node is responsible for **locking its own data**
- No global locking mechanism

##### Resolving Deadlocks

- Timeout T2, after wait exceeds a certain interval
  - Interval may need random element to avoid both transactions giving up at the same time and trying again
- Rollback T2 to let T1 proceed
- Restart T2, which can now complete

##### Approach used by DB2

- Each node maintains a local 'wait-for' graph
- Distributed deadlock detector (DDD) runs at the catalogue node for each database
- Periodically, all nodes send their graphs to the DDD
- DDD records all locks found in wait state
- Transactions becomes a candidate for termination if found in same lock wait state on two successive iterations

### Reliability

**Two-phase commit protocol (2PC)** is used to ensure that Atomicity is preserved 

#### Two-Phase Commit (2PC)

- Coordinator: Site that manages the global transactions
- Participants: Separate sites that execute local transactions

##### Phase 1: Voting

1. Coordinator sends "prepare T" message to all participants
2. Participants respond with either "vote-commit T" or "vote-abort T"
3. Coordinator waits for participants to respond within a timeout period

##### Phase 2: Decision

1. If all participants return "vote-commit T" (to commit), send "commit T" to all participants. Wait for acknowledgements within timeout period
2. If any participant returns "vote-abort T", send "abort T" to all participants. Wait for acknowledgements within timeout period
3. When all acknowledgements received, transaction is complete
  - If a site does not acknowledge, resend global decision until it is acknowledged

##### Normal Operation

![Normal Operation Image](https://remnote-user-data.s3.amazonaws.com/A9t-mNzkaZTQYdzuUxMrQjb0mcSCfshZbzx6vR4FVdz_H8g4Q7Y_vlVvVVRgzmS4k2Jh7kE8p33GkpOkzQJhQMeAyGuVfyl9ZK8-zjtD2tP5Dd2wzpzfzeIaT-ToK7-B.png)

##### Aborted Transaction

![Aborted Transaction Image 1](https://remnote-user-data.s3.amazonaws.com/uACLnjNc6Z6auEzX0U7jWhjuaiuA0GI3vxncxC20ruYsid4342LhUZbyfCmMpwHAVlIG_ITqT5i_2VJnxQ9yfSBhFg4VaG1vyXuN5TpJA5ZyvQgJ5gsvO07ctzVOzeIY.png)
![Aborted Transaction Image 2](https://remnote-user-data.s3.amazonaws.com/sw31BoOg9faJZg3JRKc3vqTVKvtMhzuyQYl-KkY-Ijy-2o8CNLIpOBQxhG71xK5ajiZLMsDRhW4rGeAyi15bL0wg3jly7-12fUy71WmbGRvlnX8xWVjcMPdS6u_ZayRw.png)

# Distributed Databases

## Horizontal Fragmentation

Each fragment contains a subset of the tuples of the global relation
![Horizontal Fragmentation Image](https://remnote-user-data.s3.amazonaws.com/RH6v1RQ-bm5_ZpWa2IxnhXoUxI2ynOzRoQzRw1aoHDI0Z1cOIqX2N_e_BNUvZRQ-iDVUesS_AeqYiOmr3DFRPwQa3lhqlATmbqqn6ja4bU_75eqvh13gSKGk5pl9_8Be.png)

## Vertical Fragmentation

Each fragment contains a subset of the attributes of the global relation 
![Vertical Fragmentation Image](https://remnote-user-data.s3.amazonaws.com/uKrmhEKuXvRwky8a4g9QlASHpwvaJ4Nk8-4HwCANZvAohKgbcEq8jNW9O0AW_oJKzbWheTdqjFGE_7Sw6qyIw1BKYo8cluS2Jwi7x-T7-T0eW3759o1AB6HN6l9UGLOf.png)

## Reduction for Horizontal Fragmentation 

![Reduction for Horizontal Fragmentation Image](https://remnote-user-data.s3.amazonaws.com/TImwLmcyqm8OFboF0kB-4YrTSce0ezw7cqYbifhs3SUmqePDVFcbsGsNOzFLoSrFga2535lPgpy5HshxPGxG8ncm1e68FpVdD2AzDU2so52Bu0Tod3193Pc6fc4WTfaB.png)

## Horizontal Selection Reduction 

![Horizontal Selection Reduction Image](https://remnote-user-data.s3.amazonaws.com/kQcx3KSme6XEPgZBlflS2v_RCCKjIg6JMcnRMLPQ4ZqN8-HNogO9khbH0Ee0PKJC4evroTQnZyQxvoaHcw-qqDYm4uOIQhewNW6baqIBQBXPXADSnmU9j53tCST0U83U.png)

## Horizontal Join Reduction 

![Horizontal Join Reduction Image](https://remnote-user-data.s3.amazonaws.com/yz7w7PbBiIqwakLXQSR_Kv548YTWcsLXznCsmfpTkO2fz890exR7eEllMmZ2M2LgEq4ikb0k9xaorJxCsOtE0f0MkF0SNf_nVNVMv1sDj8lbPm2D0G_evqyM3xAwMT4L.png)

## 2PC 

### Linear 2PC 

Second phase from the participants to the coordinator. Participants may unilaterally abort. First phase from the coordinator to the participants.
![Linear 2PC Image](https://remnote-user-data.s3.amazonaws.com/YAip-RMb2HgumIvFFeE7MGLeO0JzKWxqX16f6645pnxoZhhnrLE-AsRlWEYmhu9X5a0NlWH6qsCXwsxDDbBdz9WpuA5ASMVWVffT1DC1NhuU6EJGfjzQ2nZKEQ1vsAaw.png)

### Centralised 2PC 

Communication only between the coordinator and the participants.
![Centralised 2PC Image](https://remnote-user-data.s3.amazonaws.com/vEXDfpK3V5L1NNoqazeTeP5fbNLO1gsgRY_FP8xFyfit0r6w5Wim_wkQGhCBlalAGeHa7DNXW5xnCbZxSsVRULPa14j7BtbynwlBDcTxd7F5GVhmvFcoeIz9l_37UCbt.png)
