---
title: "Week 6"
---
# Transactions and Concurrency

## Concurrency
- In a multi-user DBMS, many users may use the system concurrently.
- Stored data items may be accessed concurrently by user programs.
- Transaction: A logical unit of work that changes the contents of a database.

## Serial vs Serialisable
- Serial Transactions: Transactions running one at a time, with no overlap.
- Serialisable Transactions: Transactions behaving as if they were serial, but may be executed concurrently.
- Transactions should be **serialisable**.

## Atomicity
- System failure partway through a transaction may leave the database in an inconsistent state.
- Atomic Transactions: Operations within the transaction are either all executed successfully or not executed at all.

## Transaction Problems

### Basic Database Access Operations
- `read(X)`: Reads a database item $X_d$ into a program variable $X_T$ in transaction $T$.
- `write(X)`: Writes the value of program variable $X_T$ in transaction $T$ into the database item $X_d$.

### The Lost Update Problem
- Two transactions have operations interleaved so that some DB items are incorrect.
- ![Lost Update Problem Image](https://remnote-user-data.s3.amazonaws.com/0xJ0zQWiYuTxK70k057DPCr_45QcjNdOEHOK5R_HVvJ8VkEmbq9bxTzRW4YTIMYdLgUJkn_o1eYE5ilv56DPHk3vyb3zgOnQMgHfq_A8KjqzzdsmCuR08vTbtdbBbDVR.png)

### The Temporary Update (Dirty Read) Problem
- One transaction updates a DB item and then fails, item is accessed before reverting to its original value.
- ![Dirty Read Problem Image](https://remnote-user-data.s3.amazonaws.com/_xj32PT1u5jVbu4CDC1RC9QVE4aaXSErqGjYD2q2_iE75arAN4Q5uR3Q3Z-YM8Ncv3ChYFk1ZI0Id8MYYLqaxdFNYfozXre8zcHKjr5VY3gN58rz6trm1YKAgdUPBIhq.png)

### The Incorrect Summary Problem
- One transaction calculates an aggregate summary function on multiple records while other transactions update records.
- Aggregate function may read some values before they are updated, and some after.
- ![Incorrect Summary Problem Image](https://remnote-user-data.s3.amazonaws.com/pcPGl8nxHrpxhriYHkj7sVZcYJFfjd6pDjg_UaKb4EvL9QYnlAOt-0d5AXO1jImylX0iWlsOq2nOHdhV9mwULpzWO5VTlkrmJq0mj_1azbjdISjVdJZjI36ISpc4Z_CM.png)

### The Unrepeatable Read Problem
- One transaction reads an item twice, while another changes the item between the two reads.
- ![Unrepeatable Read Problem Image](https://remnote-user-data.s3.amazonaws.com/AFU1LfahEdOPB7x7eBfK1E9HXu3Gxf8rcKGlqlijDPadsbfW8BpAgTpt6bQXe2ipFiyGShdUFx71K-BvYOesejm87STeUIz2y2uCCSZwvB2NvMVwzTTV7gAUnXtcwHKR.png)

## Transaction Processing
- When a transaction is submitted for execution, the system must ensure that:
  - All operations in the transaction are completed successfully, with effect recorded permanently in the database, or
  - There is no effect on the database or other transactions.
- Transactions may be **read-only** or **update**.

## Transaction Life Cycle
- ![Transaction Life Cycle Image](https://remnote-user-data.s3.amazonaws.com/mBsOI0E1BMu1PPnYJ9kz8221N6ydydaSSJBOZ9zZnj70WzHFZ6LRnsyCSmWgRdc3Q_t9JJurGL9s0fXUeX-nxG0YmS1V2x5B4oO0gTKktgdi_LamsrVUTBc1PlQfFeml.png)

## ACID

### ACID Properties
- Atomicity: A transaction is either performed completely or not at all.
- Consistency: Correct transaction execution must take the database from one consistent state to another.
- Isolation: A transaction should not make updates externally visible (to other transactions) until committed.
- Durability: Once database is changed and committed, changes should not be lost because of failure.

### Schedules
- A schedule **S** of **n** transactions is an ordering of the operations of the transactions, subject to the constraint that for each transaction **T** that participates in **S**, the operations in **T** must appear in the same order in **S** that they do in **T**.
- Two operations in a schedule are conflicting if:
  - They belong to different transactions and
  - They access the same data item and
  - At least one of the operations is a write().
- A schedule is serial if:
  - For each transaction **T** in the schedule, all operations in **T** are executed consecutively (no interleaving).
- A schedule **S** of **n** transactions is serialisable if:
  - It is equivalent to some serial schedule of the same **n** transactions.
- Two schedules are result equivalent if they produce the same final state on the database.
- Two schedules are conflict equivalent if the order of any two conflicting operations is the same in both schedules.

### Non-Serial and Non-Serialisable Schedule
- ![Non-Serial and Non-Serialisable Schedule Image](https://remnote-user-data.s3.amazonaws.com/qN4OQunO6Jih9YMpd4TCNE-mfbtGQOEj5uftKQR_jGrbldRtVJlzY7eUNDkA1SsQ7rkjVwEgS4u02GfKroyC8P73SHuOXZ1rGtNrcxNcLaRhUbYD9M4DSQpFMt9lapr-.png)

### Non-Serial but Serialisable Schedule
- ![Non-Serial but Serialisable Schedule Image](https://remnote-user-data.s3.amazonaws.com/WaAFPrF-sqkYr8h3VNaugDfllkb7_mmgvxihq7xjB1d6LWbX4N0kXGPUy-h6N_LgEVHB7Qp88dGFAysMvvrLJJgtwHwhRHXEWslOi8OQ_J27zxfIUiMPJ8yVffX7C7_R.png)

## Locking
- Locks are used to synchronise access by concurrent transactions to a database.

### Modes
- Shared: For reading.
- Exclusive: For writing.

### Lock Operations
- `lock-shared(X)`: Attempt to acquire a shared lock on X.
- `lock-exclusive(X)`: Attempt to acquire an exclusive lock on X.
- `unlock(X)`: Relinquish all locks on X.

### Lock Outcome
- ![Lock Outcome Image](https://remnote-user-data.s3.amazonaws.com/SvTjpr85orvCQwLoDnMDurcUE-En2x_Prhpif98imVo9gOy1vIWSfY1-LN9YmpltaZZEsp9GbR2p9DyivkJFvyPKIuvmoTmZg8qoFqoeQ3AcrBrxnq1XPSCoEPD3FswO.png)
- The result of an attempt to obtain a lock is either:
  - Grant lock (able to access the item).
  - Wait for lock to be granted (not yet able to access item).
  - Abort.

### Locking Rules
- Must issue `lock-shared(X)` or `lock-exclusive(X)` before a `read(X)` operation.
- Must issue `lock-exclusive(X)` before a `write(X)` operation.
- Must issue `unlock(X)` after all `read(X)` and `write(X)` operations are completed.
- Cannot issue `lock-shared(X)` if already holding a lock on **X**.
- Cannot issue `lock-exclusive(X)` if already holding a lock on **X**.
- Cannot issue `unlock(X)` unless holding a lock on **X**.

### Lock Conversion
- Rules may be relaxed in order to allow lock conversion.
  - A `lock-shared(X)` may be upgraded to a `lock-exclusive(X)`.
  - A `lock-exclusive(X)` may be downgraded to a `lock-shared(X)`.

### Locking, by itself, isn't enough for non-serial schedules.

## Two-Phase Locking (2PL)
- Extra rules for handling locks:
  - All locking operations precede the first unlock operation in a transaction.
  - Locks are only released after a transaction commits or aborts.

### Two Phases
- Guarantees serializable transactions.

#### Growing Phase
- Obtain locks.
- Access data items.

#### Shrinking Phase
- Release locks.

# Deadlock  #Db 
When two or more transactions are waiting for each other to release a lock on an item

![Deadlock Image](https://remnote-user-data.s3.amazonaws.com/FBCAi_uI6NbuXKo5JekgFD8cM0muFwLiO5Zcz2ZRQFQ8UxSDwBe8BFa8LQDS3gWg16xBF2lCx7vNsdsVgAuzFuUGmgxRdLbfAE2wIAuspXbbFi4Bxk9P2lOgY9tkjFgG.png)

## Conditions for deadlock to occur
- Concurrency: Two processes claim exclusive control of one resource
- Hold: One process continues to hold exclusively controlled resources until its need is satisfied
- Wait: Processes wait in queues for additional resources while holding resources already allocated
- Mutual dependency

## Dealing with Deadlock
### Deadlock Prevention
- Every transaction locks all items it needs in advance, if an item cannot be obtained, no items are locked
- Transactions updating the same resources are not allowed to execute concurrently

### Deadlock Detection
- Wait-for graph
	- ![Wait-for graph Image](https://remnote-user-data.s3.amazonaws.com/rzhWKROsrr_L7POjqyVWPyTgJ7vv8lDYr9_v_tOYViPmqhQux8f0pIbwjXZoOAFv-qBMxVNUE2wP-1QgJntOOhM6LNQkiFV6HuoLHlf6Fnt4hR5e9kS8HixBBL1HKmIF.png)
	- Representation of **interactions between transactions**   #Db
	- Directed graph containing:
		- A vertex for each transaction that is currently executing
		- An edge from T1 to T2 if T1 is waiting to lock an item that is currently locked by T2
	- Deadlock exists iff **the Wait-For Graph contains a cycle**   #Db
- Timeouts:
	- If a transaction waits for a resource for longer than a given period (the timeout), the system assumes that the transaction is deadlocked and aborts it

# Granularity and Concurrency
- Coarser granularity gives **lower** degree of concurrency
- Finer granularity gives **higher** overhead

# Timestamps
Alternative to locks

Timestamps are **unique identifiers for transactions**

$TS(T)$ → Transaction start time

Each resource **X** has:
- A read timestamp $read-TS(X)$:
	- $read-TS(X)$ ↔ Set to the most recent timestamp of the most recent read transaction that accessed resource **X**
- A write timestamp $write-TS(X)$:
	- $write-TS(X)$ ↔ Set to the most recent timestamp of the most recent write transaction that accessed resource **X**

## Timestamp Ordering
- Transactions are ordered based on their **timestamps**
- For each resource accessed by conflicting operations, the order in which the resource is accessed must not violate the serialisability order

## Basic Timestamp Ordering
$TS(T)$ is compared with $read-TS(X)$ and $write-TS(X)$:
- Has this item been read or written before transaction **T** has had an opportunity to read/write?
- Ensure that timestamp ordering is not violated

If timestamp ordering is violated, **transaction is aborted and resubmitted with a new timestamp**

#### **write(X)** ↓ 
```bash
if TS(T) >= read-TS(X) and TS(T) >= write-TS(X)
then
#execute write(X)
#set write-TS(X) to TS(T)
else
#abort and rollback T
``` 

![|400](https://remnote-user-data.s3.amazonaws.com/fLeHkAUBkoe3Qk8YXQyL2ptla3XAb1XC12Zgn62kZJQ0G0WXFhE-zdHUHKuTVLktm3xvNcvSnVKgZDi65V1VZ6p-J5IkaZp-or6NM1tCWBF2hbfkLg5fScgqOCop-kvf.gif) 
#### **read(X)** ↓ 
```bash
if TS(T) >= write-TS(X)
then
#execute read(X)
#set read-TS(X) to max(TS(T), read-TS(X))
else
#abort and rollback T
``` 

#### Dirty Read  ↓ 
- Transaction updates a DB item and then fails
- Item is accessed before reverting to original value
- ![|400](https://remnote-user-data.s3.amazonaws.com/Iwnqtiyt2It7ckKadfG1_vUr_ygMSFTjkoQipxtibtcyfaPWSdm5omJluAOKU2e82sxxJiNuf2LmMBGnxc7c1MBr9YG88nDp73DBl3SiJ8bXa7iQ2jWVTnOe9kZagPDx.png)  
	- We can address dirty reads by adding a commit bit **commit(X)** that indicates whether the most recent transaction to write to **X** has been committed

 **read(X)** for Dirty Read
```bash
if TS(T) >= write-TS(X)
then
#if commit(X) is true
#then
##execute read(X)
##set read-TS(X) to max(TS(T), read-TS(X))
#else
##delay execution until commit(X) is true
else
#abort and rollback T
```

**write(X)** for Dirty Read
```bash
if TS(T) >= read-TS(X) and TS(T) >= write-TS(X)
then
#execute write(X)
#set commit(X) to false
#set write-TS(X) to TS(T)
else
#abort and rollback T
``` 

### Thomas' Write Rule ↓ 

Modification of Basic Timestamp Ordering that rejects fewer write operations

Weakens the checks for **write(X)** so that obsolete write  operations are ignored

Does not enforce serialisability
#### Write Rule 

```bash
if TS(T) >= read-TS(X) and TS(T) >= write-TS(X)
then
#execute write(X)
#set commit(X) to false
#set write-TS(X) to TS(T)
else if TS(T) >= read-TS(X) and TS(T) < write-TS(X)
#if commit(X) is true
##ignore write(X)
#else
##delay execution until commit(X) is true
else
#abort and rollback T
```

# Timestamp Ordering
## Transactions are ordered based 

# Advanced Transactions

## Flat Transactions
- Basic building block
- Only one level of control by the application
- All-or-nothing (Commit or abort)
- Simplest type

## Long Duration Transactions
- More susceptible to failure (and rollback not acceptable)
- May lock and access many data items (increases chance of deadlock)

## Savepoints
- An identifiable point in a flat transaction representing a partially consistent state which can be used as an internal restart point for the transaction
- Used for **deadlock handling** 
- Savepoints may be persistent
  - Following a system crash, restart active transactions from their most recent savepoints
- ![Image](https://remnote-user-data.s3.amazonaws.com/5t9sONgpIItjtzfoqkAo8Uc20egEmWQ1YLXrWoBxwMzDQPXxc_NjXmYFWhTAwEB70sgKZCC_LxkbyBd6b1-Va_DdzAVeRnHVHIdlHInUxap-yLteThKAYQnNxz965jTm.png)

## Chained Transactions
- Transactions broken into sub-transactions which are executed serially
- On chaining to the next sub-transaction
  - Commit results
  - Keep (some) locks
- Cannot **rollback to previous sub-transaction**
- ![Image](https://remnote-user-data.s3.amazonaws.com/2sxIZElIW72NMqIIPWzYGe9vXoT2OcagYOpSF1EkZK1HBdMJyPj_01-Zq4WbxQ2-tOHbZidEqRoxXUPgy9Fd904TCuJ1ehNbKZleHR7B_jUBwb-T7Af2UlDaEJjP56-h.png)

## Savepoints vs Chained Transactions
- Both allow **substructure to be imposed on a long-running application program**
  - Database context is preserved
  - Cursors are kept
- Commit vs Savepoint
  - Chained→Rollback only to previous 'savepoint'
  - Savepoints→Can rollback to arbitrary savepoint
- Locks
  - **Chained transactions** free unwanted locks
- Work Lost
  - **Savepoints** more flexible than **flat transactions**, as long as the system does crash
- Restart
  - **Chained transactions** can restart from most recent commit, as long as no processing context hidden in local programming variables
- Both organise **work into a sequence of actions**

## Nested Transactions
- Transaction forms a hierarchy of sub-transactions
- Sub-transactions may abort without **aborting their parent transaction**
- Rules for Nested Transactions
  - Commit Rule
    - The commit of a sub-transaction makes the results accessible only to the parent
    - The final commit happens only when all ancestors finally commit
  - Rollback Rule
    - If any [sub]transaction rolls back, all of its sub-transactions roll back
  - Visibility Rule
    - Changes made by a sub-transaction are visible to its parent
    - Objects held by a parent can be made accessible to sub-transactions
    - Changes made by a sub-transaction are not visible to its siblings
- ![Image](https://remnote-user-data.s3.amazonaws.com/qQQidx5WRfK2jBGnWi5UjdhsjDF7bLZIIBIcspXJFTnV3_jEkApREXxkmPdB5ZnBE4RjnSJ-ORSj6GNYsRPLGjODOwEzc-dbkhGwJWj7OT1Z4V8nkhB4U2eTL-f4tqml.png)
- Observations
  - Sub-transactions are not fully equivalent to flat transactions
    - Atomic
    - Consistency preserving
    - Isolated
    - Not durable, because of the commit rule
  - Nesting and program modularisation complement each other
    - Well designed module has clean interface and no global variables
    - If it touches the database, the database is a large global variable
    - If the module is protected as a sub-transaction, then database changes are kept clean too
  - Nested transactions permit intra-transaction parallelism

## Emulating Nesting with Savepoints
- ![Image](https://remnote-user-data.s3.amazonaws.com/sgKPLJekYxK2zj9Ojhv-6NoaLnJhdC6WPIB-847OHlLt9VTFL7ox3znWesys9WoJw0q32GIFPlPJKCe-yf5Qze1rM6aeB71wTeUftvpMjZ9T70XqG1nGyqpKDiH2iJke.png)
- Observations
  - Using savepoints is **more flexible** than nested transactions for internal recovery as **you can roll back further**
  - True nested transactions are needed in order to run sub-transactions in parallel
    - Emulating with savepoints need 'sub-transactions' to be run in strict sequence
  - True nested transactions can pass locks selectively
    - More flexible than savepoints

## Sagas
- A collection of actions (flat transactions) that form a long duration transaction
- Execution based around notion of compensating transactions
  - Inverse of actions that allow them to be selectively rolled back
  - Used to recover from partial execution
- Sagas specified as a **digraph**
  - Nodes are either actions or the terminal nodes abort and complete
  - One node is designated the start
  - Paths in graph represent **sequences of actions**
    - Paths leading to abort are **sequences of actions that cause the overall transaction to be rolled back**
    - Paths leading to complete are **successful sequences that make persistent changes to the database**
- Saga Execution
  - Each action $A$ has a compensating transaction $A^{-1}$
  - Assume if $A$ is an action and $\alpha$ is a sequence of legal actions, then $A\alpha A^{-1}\equiv \alpha$
  - If execution of a saga leads to abort, roll back the saga by executing the compensating transactions

# Logging and Recovery

## input(X)
- Copy the disk block containing database item **X** into a buffer frame
- ![Image](https://remnote-user-data.s3.amazonaws.com/AZPY0sr8q70o4hQsJyqmiuNn6_Luv3W2JHxX76g376vK9fZFu-h_kd1awYw9cE1tJZ9ZoDDHeTt23iZ9YR4UrgQb1EXJvQtbHQcMB6uuBmU_bRKzo7FDUK4HelORU9cu.png)

## read(X)
- Read a database item **X** into a local variable
- If the block containing **X** is not already in a buffer frame, first **input(X)**
- ![Image](https://remnote-user-data.s3.amazonaws.com/9lAEPqNLuo-6yxVxvfpdEo4osp2V_pwuBQTqsZa8BkaBeQ0_5ft5BrZlclZDlySqUyZUh-A_JJG-4WYogrSowSOSPBsHgX57cy45j4iEmYfdR8-6JF3cCvFURdU80AAF.png)

## write(X)
- Write the value of local variable into database item **X** in a buffer frame
- ![Image](https://remnote-user-data.s3.amazonaws.com/zvpPVfPKmJOfMZtdblUfL-7s2wXNNJr3-V8aYd9KBK38bHF9wmrk4Bvfl_LvmGN2_Yf7w5Kl21paqbAB7J9dMo3Efh-8yO6jx3I_R6XVo4kXwyN_1rpAZsALtw-awiOD.png)

## output(X)
- Copy the block containing **X** from buffer frame to disk
- ![Image](https://remnote-user-data.s3.amazonaws.com/5d2YKHPGwMhS3jAaKwJH5_upcM9aSIoraGNorisPJwiWEAIIY_LaHthc45g1nacBj6akwP7YA2i1fif0NUgBtBpKBQFkLvmD4UP80qQyeoRmb6IUhsZj7hJrlaIO01jQ.png)

## Logging
- Persistent record of changes made during a transaction
- Log manager uses **append-only** files to record events

### Log Records
- **< start T >** →Transaction **T** has started execution
- **< abort T >** →Transaction **T** could not complete successfully, no changes made by **T** will be copied to disk
- **< commit T >** →Transaction **T** has completed successfully and will make no further changes to database items

### Undo Logging
- Repair a database following a system crash by undoing the effects of transactions that were incomplete at the time of the crash
- Introduces a new record type to record changes
  - **< T, X, old >** →Transaction **T** has changed database item **X** from its old value
- Rules
  - U1: If transaction **T** modifies database item **X**, then a log record of the form **< T, X, old >** must be written to disk before the new value of **X** is output to disk
  - U2: If a transaction **T** commits, then its **< commit T >** log record must be written to disk only after all database items changed by **T** have been output to disk
- Example
  - ![Image](https://remnote-user-data.s3.amazonaws.com/tSAFD2QgnQQW6TGtdyep-bRiN6ysl0gR-hZHoYffKMdD96uYD3setsV1lolag1lMVYAp91x2Uv5VBZLPzbNRdxlwF-47Ar2__uOjpP9ZpcK-ztAEuFL1BWYjrmesZeNg.png)
  - X_m is value in memory buffer
  - X_d is value in disc

### Recovery with Undo Logging

#### With Checkpointing
- Introduce a periodic checkpoint in the log
  - Only need to search backwards through the log to the most recent checkpoint
  - Before the checkpoint, all transactions have **committed or aborted** 
- Disadvantage of this approach: Must scan the entire log
- New log record type:
  - **< ckpt >** → The database has been checkpointed
- Process:
  1. Stop accepting new transactions
  2. Wait until all active transactions commit/abort and write **< commit T > / < abort T >** to the log
  3. Flush log
  4. Write **< ckpt >** to log
  5. Flush log
  6. Resume accepting transactions
  - ![Image|400](https://remnote-user-data.s3.amazonaws.com/M1KttrN-QJr-1T5Vs6kLxVXpT5ekXu-drXceiF5KIm_pZF2YDd2e_XlxINcUk-vw819tSjueWx4AnuFTgXM796t_eB9AjhTfkdcjthh42feobXY5hdYhkO_Zo2cZct-u.gif)

#### Nonquiescent Checkpointing
- Need to stop transaction processing while checkpointing
  - Allow new transactions to enter the system during **the checkpoint** 
  - System may appear to **stall** 
- New log record types:
  - **< start ckpt (T_1...T_n) >** → Checkpoint starts. T_1 ... T_n are active transactions that have not yet committed 
  - **< end ckpt >** → Checkpoint ends
- Process:
  1. Write **< start ckpt (T_1...T_n) >** to log and flush log
  2. Wait until \(T_1\)...\(T_n\) have all committed or aborted
  3. Write **< end ckpt >** to log and flush log 
  - ![Image|400](https://remnote-user-data.s3.amazonaws.com/rbhPcMibLM5hqdxR028mWmYiwqah_WXLkCFbFdxWDdH1ySzykJiUpzsB4Q6yzuPQASjimcjnr3ngLtk0dwbCwAJYd819ufaXoDp2EiXGp9FfuTAKK_ev0Jg3Ul2LGmRT.png)

#### Recovery with Checkpointed Undo Logging
- Two cases for recovery depending on latest checkpoint log record:
  1. **< end ckpt >** appears latest 
     - ![Image|400](https://remnote-user-data.s3.amazonaws.com/JkL1RusysYRMCumVqdGChlgvzXp-GU9PPYIGW5Nr3aDqwuhOxOiAqN2CVSgo82TSdsJ6nOBpsJ5aTwJo2NJ1PVmsbrhi_M5EsZksjgsktt6PItvjr1B8rM88INl4M-J2.png)
     - All incomplete transactions began after the previous **< start ckpt (...) >**
     - Disregard the log before the previous **< start ckpt (...) >**
  2. **< start ckpt (T_1...T_n) >** appears latest 
     - Disregard the log before the start of the earliest incomplete transaction
     - System crash occurred during checkpoint
     - Incomplete transactions are those encountered after the **< start ckpt (...) >** and those of \(T_1\)...\(T_n\) that were not committed before the crash
     - ![Image|400](https://remnote-user-data.s3.amazonaws.com/yfP933fBuewfhDWciSUka2qicExou_n0k3bWFMsUgk4PuJgn3TOu9-9j0PmmZlEBceGNePwMcbBibzJjl61_B7XNr8pIaCMW93zQemBeDH7eYjX30iNx2R7LFCaBQ4-X.png)

### Redo Logging
- Write **< commit T >** log record to disk before changed values are written to disk
- Issues with Undo Logging:
  - If a transaction **T** commits, then its **< commit T >** log record must be written to disk only after all database items changed by **T** have been written to disk
  - Potentially causes more disk i/o operations
- Example:
  - ![Image|400](https://remnote-user-data.s3.amazonaws.com/6T2yqOOpbuxOxcmHvNQA4KwwHFzox1DFwPr6mWqxlxn7nglPR6X3Cw7BqqR0lS8bgyPHsGKcXVnwVE5kfP1lJHaYQ4ddKchNX_tOLCVPkf4hkLYC1ZSoVH5zllXjF1MP.png)

#### Recovery with Redo Logging
- ![Image|400](https://remnote-user-data.s3.amazonaws.com/fs7clV_MO74AHricv-qGsBEDIh8oYPFkQlD1B-w_cweGv_pmbj75u0uj0qMWqGKw1b-q_olDZvNmDOtBAVLT8v2pjULU-iLlPEVefonRoKA5hM4XFxhSSaPto7UWb3mQ.png)

#### (Non-quiescent) Checkpointing with Redo Logging
- Recovery with Checkpointed Redo Logging:
  - Two cases for recovery depending on latest checkpoint log record:
    1. **< end ckpt >** appears latest
       - ![Image|400](https://remnote-user-data.s3.amazonaws.com/V3H8bnSxCjPlKB5zt1gPeEuvgl14t2u6gI1vp_U1T_YvVFjxjlds_PjULiTLqoECZruvVUAaAUWSElSL9elhC3cI71da_lpQsMC3V9h-Osrb8p05KKgKfMPJi8A20pCD.png)
       - Ignore every value written by transactions that committed before the corresponding **< start ckpt () >** has been written to disk
       - Any transaction named in the checkpoint start, or which has started since, may have changes that have not been written to disk (even if the transaction has committed)
    2. **< start ckpt (T_1...T_n) >** appears latest
       - Can't tell whether committed transactions to this checkpoint had their changes written to disk
       - Search back to the previous **< end ckpt >**, find its corresponding **< start ckpt () >** and treat as if **< end ckpt >** appears latest
       - ![Image|400](https://remnote-user-data.s3.amazonaws.com/gp1GVzxUqwGPUEjGvRctvKao1pYxk7KovkN7Es_iV2aX6P-nmehnFdqG1KYQG1fP0P0chb2oN7gXK3fnFW3HOKjZ-jlFbAGLQ0Osg7MuDMut_zFZCgwnZhZlj5md3r_6.png)
- ![Image|400](https://remnote-user-data.s3.amazonaws.com/TlpVrAi0FZXVbWfLBJUrx3E3GK2KXfymqlbGzh8NjP3pGHe-whpndT9NmK4V0d3qDFnJrzdcWHPRYsTzGQsQk3vxVdi9bhrS0WSeMo1LXIozwKHqF8lZiS-6oZimOzNa.png)
- Write to disk all database items that have been written to buffers but not yet to disk, by transactions that have already committed
- Write log record **< end ckpt >** and flush log
- Write log record **< start ckpt (T_1...T_n) >**, where \(T_1\)...\(T_n\) are uncommitted, and flush log

#### Redo Logging Rule
- R1: Before modifying a database item **X** on disk, all log records related to the modification (**< T, X, new >**, **< commit T >**) must be written to disk
- Ignore incomplete transactions, repeat changes made by committed transactions
- If no **< commit T >** record has been written, no changes by **T** have been written to disk
- New record type to record changes:
  - **< T, X, new >** → Transaction **T** has changed database item **X** to a new value

### Undo/Redo Logging
#### Undo/Redo Logging Rules
- UR2: A **< commit T >** record must be flushed to disk as soon as it is written to log
- UR1: Before transaction **T** modifies any database item **X** on disk, the update record **< T, X, old, new >** must be written to disk

#### Recovery with Undo/Redo Logging
- Redo all committed transactions from oldest to newest
- Undo all incomplete transactions from newest to oldest
- ![Image|400](https://remnote-user-data.s3.amazonaws.com/lww3Xo0vgHMOvNhQhGqk4GRjCFChtWWksQJBAb6-KKeK0ug4kQxDvrQ9NcSGYAEHm_tg7Jl6geI2tgs608GlNZyKoR9JRdkELVjDwew6N3msiOu48StibNRgB2lrFz6J.png)

#### Checkpointing with Undo/Redo Logging
- Write **< end ckpt >** to log and flush log
- Write to disk all dirty buffers (i.e. those with one or more changed database items, not just those from committed transactions)
- Write **< start ckpt (T_1...T_n) >** to log and flush log
- Introduces a new record type to record changes:
  - **< T, X, old, new >** → Transaction **T** has changed database item **X** from an old value to a new value

#### Aims to address issues with both undo and redo logging
- Undo logging may increase **number of disk i/o operations**
- Redo logging requires that **all modified blocks be kept in buffers until the transaction commits and the logs flushed**
