# Query Processing

## Query Processing Chain

![Image](https://remnote-user-data.s3.amazonaws.com/greXqWglitCl9cxMWxhhsjEdFRduBHg7SBXmzWe6R9AQx8l54iOTtXfEDsemtwCBlHoBVTl6vpBBSqXQTfW25JT_nx-M6sk4-FnxdVvA76SnkHxRMA3EWgZOlNtvUQyP.png)

- Query optimisation takes place over **Selection of Logical Query Plan** and **Selection of Physical Query Plan**

![Image](https://remnote-user-data.s3.amazonaws.com/UcY7MesZn89gjaKM9CxD2LDOU1rWNLTdDl7EiVp7FKzMAqWAcLWBGOwf3yR1NfuT8j4iPBWnIF_91SSqLnie-4iLhMzWrVGLEmv43zGwBA7lCQ5_1IZ4OPfK3o37K9BN.png)

## Query Plans

### Logical Query Plan

- Operators taken from relational algebra
- Abstract
- Algebraic representation of query

### Physical Query Plan

- Algorithms selected for each operator in plan
- Execution order specified for operators

## Optimisation

- Need to start optimisation from **a** [Canonical Form](Advanced Databases/Week 5/Query Processing/Query Optimisation/Optimising Query Trees/Tree Structures and Canonical Form/Canonical Form.md)

### Optimisation Example

![Image](https://remnote-user-data.s3.amazonaws.com/gPmhaBVcvOkXcyJpgnK5Nt-nhOaYTxdR1DL8c-0WtzfEGikjSj-Lc2AdsNKWVQIGx-9v-tfaaDPqwnDgePAL8oaFDCera9oQ9ykeOlJqWPFdcRAsV30Zs4puH_kenX6c.png)

![Image](https://remnote-user-data.s3.amazonaws.com/trNIrPxSEDigQqbXGVNge8v9NmpVgzWJLgmvzBDeidHSGvm9ehZf9EUxzEBC4h39VN44e8cVFbWJateg-rfzC3kAOPagOvG_E7VdudqlSlczQH-ioIgdNvo0vzd06lWm.png)

![Image](https://remnote-user-data.s3.amazonaws.com/up2XD_VYt5OQCnICFeYeu3InFfyq_G2aIlXujf8XgAKlb7BzTg7lXx05wgXMxtKG8J20T52ADsPiwa98CVhwxmb8IE4_BKuibfNgHew0CzJ6yIUbO9l5wAK34RikghIX.png)

## Cost Estimation

- At this stage, no commitment to a particular physical plan
- Estimate the "cost" of each operator in terms of the size relations on which it operates
- Choose a logical query plan that minimises the size of the intermediate relations
- Assumes that the system catalogue stores statistics about each relation

### Statistics

- **T(R)** → Number of tuples in relation **R** (cardinality of **R**)
- **V(R,A)** → Number of distinct values for attribute **A** in relation **R**

### Scan

- Operation of reading all tuples of a relation
- **T(scan(R)) = T(R)**
  - For all **A** in **R**, **V(scan(R),A) = V(R,A)**

### Product

- $T(R\times S) = T(R)T(S)$
  - For all **A** in **R**, $V(R\times S,A) = V(R,A)$
  - For all **B** in **S**, $V(R\times S, B) = V(S,B)$

### Projection

- $T(\pi_A(R)) = T(R)$
  - For all **A** in **R** and $\pi_A(R)$, $V(\pi_A(R),A) = V(R,A)$
- Assumes projection does not remove duplicate tuples
  - So value counts remain the same

### Selection

#### Selection Case 1 (attr=val)

- $T(\sigma_{A=c}(R)) = \frac{T(R)}{V(R,A)}$
- $V(\sigma_{A=c}(R),A) = 1$
- Assumes all values of **A** appear with equal frequency

#### Selection Case 2 (attr=attr)

- $T(\sigma_{A=B}(R)) = \frac{T(R)}{max(V(R,A),V(R,B))}$
- $V(\sigma_{A=B}(R),A) = V(\sigma_{A=B}(R),B) = min(V(R,A),V(R,B))$
- Assumes all values of **A** appear with equal frequency
- Assumes all values of **B** appear with equal frequency

#### Further Selection

- Inequality
  - If we know the range of values in **A** and their distribution
    - As a first approximation, $T(\sigma_{A\neq c}(R)) = T(R)$
  - Typical inequality written to match less than half of a relation
    - As a rule of thumb, $T(\sigma_{A<c}(R)) = \frac{T(R)}{3}$
  - Alternatively
    - $T(\sigma_{A\neq c}(R)) = \frac{T(R)(V(R,A)-1)}{V(R,A)}$
  - Selection with inequalities and not equals require a more nuanced approach

### Conjunction and Disjunction

- $T(\sigma_{A=c1 \wedge B=c2}(R)) = \frac{T(R)}{V(R,A)V(R,B)}$
- $T(\sigma_{A=c1 \cup B=c2}(R)) = \frac{T(R)}{V(R,A)} + \frac{T(R)}{V(R,B)}$

![Image](https://remnote-user-data.s3.amazonaws.com/oJDlw1MNI6okxSPq1DwbUG7lH9TH-oYifJfYWCQBrRp0lI3_Zj-u6kRw56nlZhsAXSABjvrr8hbU8N13p3ljyt9DIBbyfjePU8HR-ROokOH5wvivHQaqpU5nTJY2H8hj.png)

### Join

- $T(R\bowtie_{A=B}S) = \frac{T(R)T(S)}{max(V(R,A),V(S,B))}$
- $V(R\bowtie_{A=B}S,A) = V(R\bowtie_{A=B}S,B) = min(V(R,A),V(S,B))$

### Further Join

- If there are multiple pairs of join attributes
  - $T(R\bowtie_{R1=S1\wedge R2=S2}S) = \frac{T(R)T(S)}{max(V(R,R_1),V(S,S_1))max(V(R,R_2),V(S,S_2))}$

### Further Statistics

- Distinct values assumes that each attribute value appears with equal frequency
  - Gives inaccurate estimates for joins and selects
  - Potentially unrealistic
- Other approaches based on histograms
  - Equal Width: Divide the attribute domain into equal parts, give tuple counts for each
  - Equal Height: Sort tuples by attribute, divide into equal-sized sets of tuples and give maximum value for each set
  - Most-Frequented Values: Give tuple counts for top-n most frequent values

![Image](https://remnote-user-data.s3.amazonaws.com/2Osos0EGFZ4dfDMdQUJnFHH9O9dv9KIy3w_15SVcii_z4bXcBsaiQF1JoHi-9iegBRBP39xxhtj7HwWE4uBqgLZ0MoSUuT8AOJYS--3MViJI7tKMxygpADmKBsaWEfaV.png)

## Query Optimisation

### Heuristic Approach

- Start with canonical form
- Move $\sigma$ operators down the tree
  1. Reorder subtrees to put most restrictive $\sigma$ first
- Combine $\times$ and $\sigma$ to create $\bowtie$
- Move $\pi$ operators down the tree

### Optimising Query Trees

- Reorder Joins
  - Reorder subtrees to put the most relations (fewest tuples) first
  - Adopt a greedy approach

![Image](https://remnote-user-data.s3.amazonaws.com/kTjVOAOiZkqHLNjE5xopkKo95jcpXtB7o-nzSp_pXKpuSMhsTCX_IOeL6HiarFx7EwpMuRdT6M5vogzVHl2wXsBbkTcpWRIUvqO760fP4HP59zZZsdgzVn6mlIQMq7jr.png)

![Image](https://remnote-user-data.s3.amazonaws.com/bVJxlX93896M4mnczvNqCF_iGjJ7YgCcYvIWVMZtWCGHgnpZl7O0FPePwmMfflKYrzzFDevHU1iHKB7ntP5Uf7O53183LfGLB06B-wu35LYvtOy-Nel8wPhi5UDKVaAt.png)

#### Tree Structures and Canonical Form

- Useful to only consider left-deep trees
  - Left deep trees work well with common join algorithms
    - Index
    - Nested-loop
    - One-pass
  - Fewer possible left-deep trees than possible bushy trees
    - Smaller search space when investigating join orderings
- Canonical Form
  - A conjunctive selection above the products and
  - A projection (of the output attributes) above the selection
  - A left-deep tree of products with

#### Result is Optimised Logical Query Plan

![Image](https://remnote-user-data.s3.amazonaws.com/fjGlNE3fKrFkM2XgN9PQbDME9_CWa8mLGfQOVIhJH6QFo6tQrAQ67Xn4GJeVNOSxupn_OEM1ACVqlwt7lPgy_qIK9Uuum3sjMR4cKwFT8ogZ5kKC9zUD68lNR0pBzTrV.png)

#### Move \(\pi\) Down

![Image](https://remnote-user-data.s3.amazonaws.com/yz1JXQu6LPxkORfM7BPow1DqVg1ZBiFIelj7OFR_uwMvllfi7y8yvNdOJhn-XstdApMFtraVtmQlnlStPwEgQVC2NL7xYFirn-e4cGD0t1PwIgFsToDJlGlYi9YrdLIV.png)

- If intermediate relations are to be kept in buffers, reducing the degree or arity of those relations allows us to use fewer buffer frames.

#### Move \(\sigma\) Down

![Image](https://remnote-user-data.s3.amazonaws.com/0KOI5r65fTymwbQEafWZiMAXnFgK1o9kxMQ_md-F4doR9VbSUfHfesxYl9JTAkIr4gkATBk6v4idL0_opNZgS6ROd3wuam53hAN9AsrneOZ6cMA6u-S0cPiLNda0-x-B.png)

- A selection of the form \(\sigma_{attr=val}\) can be pushed down to just above the relation that contains **attr**.
- A selection of the form \(\sigma_{attr1=attr2}\) can be pushed down to the product above the subtree containing the relations that contain **attr1** and **attr2**.

#### Start from Canonical Form

![Image](https://remnote-user-data.s3.amazonaws.com/M0Laa3OBgkX1Jr5mtEY1MthO6KBEhNJX3Ko0XIUu3KUiTw1tbC12KrbJ-R0_ctAi4Gs5AKR1RddfDuCEj_phujY1XyEsw0DBVxSQTN-2PiyQxe3r0YdGt7nk5lYj-iR7.png)

#### Create Joins

![Image](https://remnote-user-data.s3.amazonaws.com/nsunRB0nJ9v1zT14csNx5A7MSjyUdhvck58vcmvTF7elo8HDX0eBKQ8xMq8Mszdv-GU2zoMxMjR0PCuaN7TebaKmafez4OWUxsa2W7WDfqAIQBm2KIA2tc1V6JZom6W-.png)

- Combine \(\times\) with a \(\sigma\) immediately above to form \(\bowtie\).
- Uses the relational transformation \(\sigma_a(R\times S)\equiv R\bowtie_a S\).
  - Join is more efficient than product followed by selection.

![Image](https://remnote-user-data.s3.amazonaws.com/H-F5MIffk0TNkDliXKoYpljsU4v6PCQ45FXoxymUoYTT4BvgmfLxoUeZ2VAapgJt_qZ5D8FeclEqrEY3pNv7WKesXu7IP-jNFzKjdeGZMtYMJmdWMXEfDRY5A0ttTfC5.png)

## Physical-Plan Operators

- Algorithm that implements one of the basic relational operations that are used in query plans.

### Computation Model

- Need to choose good physical-plan operators.
- Key measure of cost is the number of disk accesses.
- Estimate the "cost" of each operator.

### Cost Parameters

- **M** → Main memory available for buffers (counted in blocks).
- **S(R)** → Size of a tuple of relation **R**.
- **B(R)** → Blocks used to store relation **R**.
- **T(R)** → Number of tuples in relation **R** (cardinality of **R**).
- **V(R,a)** → Number of distinct values for attribute **a** in relation **R**.

### Clustered File

- Tuples from different relations that can be joined (on particular attribute values) stored in blocks together.

![Image](https://remnote-user-data.s3.amazonaws.com/C1cC7w1lr_YXebx4uAp4kkX8D1oFITo3vtPeWl8a2OCwhmNrlkIwkIYFXZ6RDHdW27usFrkv2OxNzEmvymjJafB_R0YEyAgeVfK4ayVqPuIkCNl7Npv6tzUYSproE2oK.png)

### Clustered Relation

![Image](https://remnote-user-data.s3.amazonaws.com/fLrXE5uutCE3Dxlcwm1X9-t5MmQHiCsNcBBysgyBxKEZVGHjwdY7MseUiTCtD6vVey5A554Gqr4c20-0CYbTh0s9X2NfsXW08ZYZEFT9HGCsudajGhGScSGsle07Qs46.png)

- Tuples from relation are stored together in blocks, but not necessarily sorted.

### Clustering Index

![Image](https://remnote-user-data.s3.amazonaws.com/oPInVTKpSpZaLHZ31wgy9PYEeGJSuZofAQY0YNjsVNbZUFOyOeCUlxdHc0OU4AjFVWlmNAEhGUOgdC-3oYKXXiKPIIS3A5a_A3ipKoB8NmUCtBio4ux472YIC2Kcmg-v.png)

- Index that allows tuples to be read in an order that corresponds to physical order.

## Scanning

### Index Scan

- Retrieve blocks for **R**.
- Read only those tuples of a relation **R** that satisfy some predicate.
- An index exists on some attribute of **R**.

#### I/O Cost

- If not clustered → **T(R)** disk accesses.
- If clustered → B(R) + B(I_R) disk accesses.
  - B(R) >> B(I_R), so treat as only B(R).
- Use index to find all blocks holding **R**.

### Table Scan

#### I/O Cost

- If **R** is not clustered → **T(R)** disk accesses.
- If **R** is clustered → **B(R)** disk accesses.
- All blocks known to the system.
- Tuples arranged in blocks.
- Possible to get blocks one at a time.
- Read all of the tuples of a relation **R**.

## One-Pass Algorithms

- Read data from disk only once.
- Typically require that at least one argument fits in main memory.

### Unary (Tuple at a Time)

![Image](https://remnote-user-data.s3.amazonaws.com/Rj4Wv4shHf1n8FVo94Jbv2xu3YwA0LtFu8op3RcgMhN1YEW1a-j4fZyai0qgazO6n-S7nU8dp9jblh5MJEM7XBUgALSoMvvsx2J2Ik-Yk0sw-E7zoK_5gZRF7Y0E4Uv7.png)

- For each block of **R**:
  - Perform operation (select, project) on each tuple in block.
  - Copy block to input buffer.
  - Move selected/projected tuples to output buffer.

#### Cost

- Requires **M ≥ 1**.
- If operator is a select that compares an attribute to a constant and index exists for attributes used in select, **< B(R)** disk accesses.
- Generally **B(R)** or **T(R)** disk accesses depending on clustering.

### Unary (Full Relation)

![Image](https://remnote-user-data.s3.amazonaws.com/4U3htTPnZPI7dmDJX3mSnZgRG6v0vwYM13yNvTvONoE34yKN0FEzRdfdcpnzxmF-xKRJ0SAl0SakX4TKxGni-KjnVCc_wP7KljJmTG33AM1ch2A5lRndnCLEX_DH2udR.png)

- For each block of **R**:
  - Update accumulator.
  - Copy block to input buffer.
  - Move tuples to output buffer.

#### Duplicate Elimination

- Cost is **B(R)** disk accesses.
- Requires **M ≥ B(δ(R)) + 1** blocks of main memory.
  - **1** block for input buffer.
  - **M-1** blocks for accumulator.
- Accumulator implemented as in-memory data structure (tree, hash).
- For each block of **R**:
  - If tuple is not in accumulator:
    - For each tuple in block:
      - Copy to accumulator.
      - Copy block to input buffer.
      - Copy to output buffer.
- If fewer than **B(δ(R))** blocks available, thrashing likely.

#### Grouping

- Grouping operators: min, sum, avg, count, max.
- Output only when all blocks of **R** have been consumed.
- Cost is **B(R)** disk accesses.
- Accumulator contains per-group values.

## Binary (Full Relation)

- In general, cost is **B(R) + B(S)**.
  - **R**, **S** are operand relations.
- Requirement for one-pass operation: \(\min(B(R), B(S)) \leq M-1\).

### Join

- Two relations, **R(X,Y)** and **S(Y,Z)**, where **B(S) < B(R)**.
  - Uses main memory search structure keyed on **Y**.

## Nested-Loop Joins

- Assuming we're joining relations **R**, **S** on attribute **C**.
#### python
```python
for each tuple r in R
for each tuple s in S
if r.C = s.C then output r,s pair
```


### Factors that affect cost

1. Do indexes exist?
2. Are tuples of relation stored physically together? (clustered)
3. Are relations sorted by join attribute?

### Example

- Consider a join between relations $(R_1), (R_2)$ on attribute **C**.
  - ($T(R_2) = 5,000)$.
  - $(T(R_1) = 10,000)$.
  - $(M = 101)$ blocks.
  - $(S(R_1) = S(R_2) = 1/10)$ block.

#### Attempt #1: Tuple-based Nested Loop Join

- Relations not contiguous (not clustered).
  - One disk access per tuple.
- Cost for each tuple in \(R_1\) = cost to read tuple + cost to read \(R_2\).
- Total Cost = \(T(R_1) \times (1 + T(R_2)) = 50,010,000\) disk accesses.

#### Attempt #2: Block-based Nested Loop Join

- Changes:
  - Read all of inner relation $(R_2)$ (using 1 block) + join.
  - Use all available main memory $(M = 101))$.
  - Read outer relation $(R_1)$ in chunks of 100 blocks.
- Cost to read one 100-block chunk of$ (R_1) = (100 \times \frac{1}{S(R_1)} = 1,000)$ disk accesses.
- Cost to process each chunk = \(1,000 + T(R_2) = 6,000\).
- Total Cost = \(\frac{T(R_1)}{1,000} \times 6,000 = 60,000\) disk accesses.

#### Attempt #3: Join Reordering

- Changes:
  - Reverse the join order.
    - \(R_1\) becomes the inner relation.
    - \(R_2\) becomes the outer relation.
- Cost to read one 100-block chunk of $(R_2) = (100 \times \frac{1}{S(R_2)} = 1,000)$ disk accesses.
- Cost to process each chunk = $(1,000 + T(R_1) = 11,000)$.
- Total Cost =$(\frac{T(R_2)}{1,000} \times 11,000 = 55,000)$ disk accesses.

#### Attempt #4: Contiguous Relations

- Changes:
  - The tuples in each relation are contiguous (i.e., clustered).
- \(B(R_1) = 1,000\).
- Cost to read one 100-block chunk of \(R_2\) = 100 disk accesses.
- \(B(R_2) = 500\).
- Cost to process each chunk = \(100 + B(R_1) = 1,100\).
- Total Cost = $(\frac{B(R_2)}{100} \times 1,100 = 5,500)$ disk accesses.

#### Attempt #5: Merge Join

- Changes:
  - Both relations are contiguous and sorted by **C** (the join attribute).
- Total Cost = \(B(R_1) + B(R_2) = 1,500\) disk accesses.

![Image](https://remnote-user-data.s3.amazonaws.com/RM0LboPUn1cnSHG7w0vt8ZBp1NRb5fyOowshRdCE__ywTCdu5rNtq8rLmcqC4c25yLMCXnnKVsI0gdDm4lfOeM0eC7DLxADN_RJNGXphfzikLWY9Yz15dqceuEQOw8fU.png)


# Two-Pass Algorithms

## Improving on last example
- What if $R_1$ and $R_2$ aren't sorted by **C**

## Merge Sort
- Read all chunks + merge + write out
  - Cost
  - Sort cost $R_2 = 2,000$ disk accesses
  - Each tuple is read, written, read, written
  - Sort cost $R_1 = 4,000$ disk accesses
- ![|400](https://remnote-user-data.s3.amazonaws.com/52Ghi-prBmg3W9asNmyqfSYMZVcy1gczGVgQ7yfs9glbaVF2mD3VN-PnNI_bWragBzUKe2XFGWoMXAXEAhwBejvNjRd8SVcVLRAWWdqxm47iK11UKrvCoqAGQUKSYdPn.png) 
- For each 100 block chunk of **R**
  - Write to disk
  - ![|400](https://remnote-user-data.s3.amazonaws.com/amI7b2acz9Pf-g3iEZEJpG-tWt03L9wEoZIbfYIjPsiGi6lepkfm5Tizev9ZAob3CFgpiGRaAoVHmoawtIuOtB5dsGsp24MflbPc8EeBEGFJDlHMDNJj2jbQl3PlXmZW.png) 
  - Sort in memory
  - Read chunk

## Attempt #6: Merge Join with Sort
- If $R_1,R_2$ contiguous, but unordered
  - Total Cost = sort cost + join cost = $7,500$ disk accesses
  - Nested loop cost = $5,500$ disk accesses
  - So merge join does not necessarily pay off
- If $R_1=10,000$ blocks, contiguous
  - $R_2=5,000$ blocks, not-ordered
    - Merge join cost = $75,000$ disk accesses
    - Nested loop cost = $505,000$ disk accesses
    - So in this case merge join is better

## Attempt #7: Improved Merge Join
- Changes
- Do the entire files need to be sorted?
  - ![|400](https://remnote-user-data.s3.amazonaws.com/H-4htbu_YHdmc9NBB_SzCtnAiHfoBqk69h_tVu83hp9njiGDBWyfYJ5ABRPpjkNYNG9wTQ8bYg71PHlKSL8Hd8a2UKu2UHsA5TKzHhpVN0_BqE8GKYBt0xBD9aqtIxC1.png) 
- Read $R_1$ and write $R_1$ into runs
- Read $R_2$ and write $R_2$ into runs
  - Merge join
- Total Cost = $2,000 + 1,000 + 1,500 = 4,500$ disk accesses

## Two Pass Algorithms using Hashing
- Hash-Join
  - Read $R_2$ and write into buckets
  - The tuples in $R_1$ and $R_2$ are both hashed using the same hashing function on the join attributes
  - Join $R_1,R_2$
  - Total Cost = $3*(B(R_1)+B(R_2))=4,500$ disk accesses 
  - Read $R_1$ and write into buckets
- Partition relation into **M-1** buckets
  - In general
    - Hash tuple to bucket
    - When bucket is full, move to disk and reinitialise bucket
    - Read relation a tuple at a time

# Indexed Based Algorithms

## Attempt #8: Index Join
- Changes
  - Assume $R_2.C$ index exists; 2 levels
  - Assume $R_1$ contiguous, unordered
  - Assume $R_2.C$ index fits in memory
  - What if we have an index on the join attribute
- Cost = Reads: $500$ disk accesses
  - For each $R_1$ tuple# Query Processing

## Query Processing Chain

![Image](https://remnote-user-data.s3.amazonaws.com/greXqWglitCl9cxMWxhhsjEdFRduBHg7SBXmzWe6R9AQx8l54iOTtXfEDsemtwCBlHoBVTl6vpBBSqXQTfW25JT_nx-M6sk4-FnxdVvA76SnkHxRMA3EWgZOlNtvUQyP.png)

- Query optimisation takes place over **Selection of Logical Query Plan** and **Selection of Physical Query Plan**

![Image](https://remnote-user-data.s3.amazonaws.com/UcY7MesZn89gjaKM9CxD2LDOU1rWNLTdDl7EiVp7FKzMAqWAcLWBGOwf3yR1NfuT8j4iPBWnIF_91SSqLnie-4iLhMzWrVGLEmv43zGwBA7lCQ5_1IZ4OPfK3o37K9BN.png)

## Query Plans

### Logical Query Plan

- Operators taken from relational algebra
- Abstract
- Algebraic representation of query

### Physical Query Plan

- Algorithms selected for each operator in plan
- Execution order specified for operators

## Optimisation

- Need to start optimisation from **a** [Canonical Form](Advanced Databases/Week 5/Query Processing/Query Optimisation/Optimising Query Trees/Tree Structures and Canonical Form/Canonical Form.md)

### Optimisation Example

![Image](https://remnote-user-data.s3.amazonaws.com/gPmhaBVcvOkXcyJpgnK5Nt-nhOaYTxdR1DL8c-0WtzfEGikjSj-Lc2AdsNKWVQIGx-9v-tfaaDPqwnDgePAL8oaFDCera9oQ9ykeOlJqWPFdcRAsV30Zs4puH_kenX6c.png)

![Image](https://remnote-user-data.s3.amazonaws.com/trNIrPxSEDigQqbXGVNge8v9NmpVgzWJLgmvzBDeidHSGvm9ehZf9EUxzEBC4h39VN44e8cVFbWJateg-rfzC3kAOPagOvG_E7VdudqlSlczQH-ioIgdNvo0vzd06lWm.png)

![Image](https://remnote-user-data.s3.amazonaws.com/up2XD_VYt5OQCnICFeYeu3InFfyq_G2aIlXujf8XgAKlb7BzTg7lXx05wgXMxtKG8J20T52ADsPiwa98CVhwxmb8IE4_BKuibfNgHew0CzJ6yIUbO9l5wAK34RikghIX.png)

## Cost Estimation

- At this stage, no commitment to a particular physical plan
- Estimate the "cost" of each operator in terms of the size relations on which it operates
- Choose a logical query plan that minimises the size of the intermediate relations
- Assumes that the system catalogue stores statistics about each relation

### Statistics

- **T(R)** → Number of tuples in relation **R** (cardinality of **R**)
- **V(R,A)** → Number of distinct values for attribute **A** in relation **R**

### Scan

- Operation of reading all tuples of a relation
- **T(scan(R)) = T(R)**
  - For all **A** in **R**, **V(scan(R),A) = V(R,A)**

### Product

- $T(R\times S) = T(R)T(S)$
  - For all **A** in **R**, $V(R\times S,A) = V(R,A)$
  - For all **B** in **S**, $V(R\times S, B) = V(S,B)$

### Projection

- $T(\pi_A(R)) = T(R)$
  - For all **A** in **R** and $\pi_A(R)$, $V(\pi_A(R),A) = V(R,A)$
- Assumes projection does not remove duplicate tuples
  - So value counts remain the same

### Selection

#### Selection Case 1 (attr=val)

- $T(\sigma_{A=c}(R)) = \frac{T(R)}{V(R,A)}$
- $V(\sigma_{A=c}(R),A) = 1$
- Assumes all values of **A** appear with equal frequency

#### Selection Case 2 (attr=attr)

- $T(\sigma_{A=B}(R)) = \frac{T(R)}{max(V(R,A),V(R,B))}$
- $V(\sigma_{A=B}(R),A) = V(\sigma_{A=B}(R),B) = min(V(R,A),V(R,B))$
- Assumes all values of **A** appear with equal frequency
- Assumes all values of **B** appear with equal frequency

#### Further Selection

- Inequality
  - If we know the range of values in **A** and their distribution
    - As a first approximation, $T(\sigma_{A\neq c}(R)) = T(R)$
  - Typical inequality written to match less than half of a relation
    - As a rule of thumb, $T(\sigma_{A<c}(R)) = \frac{T(R)}{3}$
  - Alternatively
    - $T(\sigma_{A\neq c}(R)) = \frac{T(R)(V(R,A)-1)}{V(R,A)}$
  - Selection with inequalities and not equals require a more nuanced approach

### Conjunction and Disjunction

- $T(\sigma_{A=c1 \wedge B=c2}(R)) = \frac{T(R)}{V(R,A)V(R,B)}$
- $T(\sigma_{A=c1 \cup B=c2}(R)) = \frac{T(R)}{V(R,A)} + \frac{T(R)}{V(R,B)}$

![Image](https://remnote-user-data.s3.amazonaws.com/oJDlw1MNI6okxSPq1DwbUG7lH9TH-oYifJfYWCQBrRp0lI3_Zj-u6kRw56nlZhsAXSABjvrr8hbU8N13p3ljyt9DIBbyfjePU8HR-ROokOH5wvivHQaqpU5nTJY2H8hj.png)

### Join

- $T(R\bowtie_{A=B}S) = \frac{T(R)T(S)}{max(V(R,A),V(S,B))}$
- $V(R\bowtie_{A=B}S,A) = V(R\bowtie_{A=B}S,B) = min(V(R,A),V(S,B))$

### Further Join

- If there are multiple pairs of join attributes
  - $T(R\bowtie_{R1=S1\wedge R2=S2}S) = \frac{T(R)T(S)}{max(V(R,R_1),V(S,S_1))max(V(R,R_2),V(S,S_2))}$

### Further Statistics

- Distinct values assumes that each attribute value appears with equal frequency
  - Gives inaccurate estimates for joins and selects
  - Potentially unrealistic
- Other approaches based on histograms
  - Equal Width: Divide the attribute domain into equal parts, give tuple counts for each
  - Equal Height: Sort tuples by attribute, divide into equal-sized sets of tuples and give maximum value for each set
  - Most-Frequented Values: Give tuple counts for top-n most frequent values

![Image](https://remnote-user-data.s3.amazonaws.com/2Osos0EGFZ4dfDMdQUJnFHH9O9dv9KIy3w_15SVcii_z4bXcBsaiQF1JoHi-9iegBRBP39xxhtj7HwWE4uBqgLZ0MoSUuT8AOJYS--3MViJI7tKMxygpADmKBsaWEfaV.png)

## Query Optimisation

### Heuristic Approach

- Start with canonical form
- Move $\sigma$ operators down the tree
  1. Reorder subtrees to put most restrictive $\sigma$ first
- Combine $\times$ and $\sigma$ to create $\bowtie$
- Move $\pi$ operators down the tree

### Optimising Query Trees

- Reorder Joins
  - Reorder subtrees to put the most relations (fewest tuples) first
  - Adopt a greedy approach

![Image](https://remnote-user-data.s3.amazonaws.com/kTjVOAOiZkqHLNjE5xopkKo95jcpXtB7o-nzSp_pXKpuSMhsTCX_IOeL6HiarFx7EwpMuRdT6M5vogzVHl2wXsBbkTcpWRIUvqO760fP4HP59zZZsdgzVn6mlIQMq7jr.png)

![Image](https://remnote-user-data.s3.amazonaws.com/bVJxlX93896M4mnczvNqCF_iGjJ7YgCcYvIWVMZtWCGHgnpZl7O0FPePwmMfflKYrzzFDevHU1iHKB7ntP5Uf7O53183LfGLB06B-wu35LYvtOy-Nel8wPhi5UDKVaAt.png)

#### Tree Structures and Canonical Form

- Useful to only consider left-deep trees
  - Left deep trees work well with common join algorithms
    - Index
    - Nested-loop
    - One-pass
  - Fewer possible left-deep trees than possible bushy trees
    - Smaller search space when investigating join orderings
- Canonical Form
  - A conjunctive selection above the products and
  - A projection (of the output attributes) above the selection
  - A left-deep tree of products with

#### Result is Optimised Logical Query Plan

![Image](https://remnote-user-data.s3.amazonaws.com/fjGlNE3fKrFkM2XgN9PQbDME9_CWa8mLGfQOVIhJH6QFo6tQrAQ67Xn4GJeVNOSxupn_OEM1ACVqlwt7lPgy_qIK9Uuum3sjMR4cKwFT8ogZ5kKC9zUD68lNR0pBzTrV.png)

#### Move \(\pi\) Down

![Image](https://remnote-user-data.s3.amazonaws.com/yz1JXQu6LPxkORfM7BPow1DqVg1ZBiFIelj7OFR_uwMvllfi7y8yvNdOJhn-XstdApMFtraVtmQlnlStPwEgQVC2NL7xYFirn-e4cGD0t1PwIgFsToDJlGlYi9YrdLIV.png)

- If intermediate relations are to be kept in buffers, reducing the degree or arity of those relations allows us to use fewer buffer frames.

#### Move \(\sigma\) Down

![Image](https://remnote-user-data.s3.amazonaws.com/0KOI5r65fTymwbQEafWZiMAXnFgK1o9kxMQ_md-F4doR9VbSUfHfesxYl9JTAkIr4gkATBk6v4idL0_opNZgS6ROd3wuam53hAN9AsrneOZ6cMA6u-S0cPiLNda0-x-B.png)

- A selection of the form \(\sigma_{attr=val}\) can be pushed down to just above the relation that contains **attr**.
- A selection of the form \(\sigma_{attr1=attr2}\) can be pushed down to the product above the subtree containing the relations that contain **attr1** and **attr2**.

#### Start from Canonical Form

![Image](https://remnote-user-data.s3.amazonaws.com/M0Laa3OBgkX1Jr5mtEY1MthO6KBEhNJX3Ko0XIUu3KUiTw1tbC12KrbJ-R0_ctAi4Gs5AKR1RddfDuCEj_phujY1XyEsw0DBVxSQTN-2PiyQxe3r0YdGt7nk5lYj-iR7.png)

#### Create Joins

![Image](https://remnote-user-data.s3.amazonaws.com/nsunRB0nJ9v1zT14csNx5A7MSjyUdhvck58vcmvTF7elo8HDX0eBKQ8xMq8Mszdv-GU2zoMxMjR0PCuaN7TebaKmafez4OWUxsa2W7WDfqAIQBm2KIA2tc1V6JZom6W-.png)

- Combine \(\times\) with a \(\sigma\) immediately above to form \(\bowtie\).
- Uses the relational transformation \(\sigma_a(R\times S)\equiv R\bowtie_a S\).
  - Join is more efficient than product followed by selection.

![Image](https://remnote-user-data.s3.amazonaws.com/H-F5MIffk0TNkDliXKoYpljsU4v6PCQ45FXoxymUoYTT4BvgmfLxoUeZ2VAapgJt_qZ5D8FeclEqrEY3pNv7WKesXu7IP-jNFzKjdeGZMtYMJmdWMXEfDRY5A0ttTfC5.png)

## Physical-Plan Operators

- Algorithm that implements one of the basic relational operations that are used in query plans.

### Computation Model

- Need to choose good physical-plan operators.
- Key measure of cost is the number of disk accesses.
- Estimate the "cost" of each operator.

### Cost Parameters

- **M** → Main memory available for buffers (counted in blocks).
- **S(R)** → Size of a tuple of relation **R**.
- **B(R)** → Blocks used to store relation **R**.
- **T(R)** → Number of tuples in relation **R** (cardinality of **R**).
- **V(R,a)** → Number of distinct values for attribute **a** in relation **R**.

### Clustered File

- Tuples from different relations that can be joined (on particular attribute values) stored in blocks together.

![Image](https://remnote-user-data.s3.amazonaws.com/C1cC7w1lr_YXebx4uAp4kkX8D1oFITo3vtPeWl8a2OCwhmNrlkIwkIYFXZ6RDHdW27usFrkv2OxNzEmvymjJafB_R0YEyAgeVfK4ayVqPuIkCNl7Npv6tzUYSproE2oK.png)

### Clustered Relation

![Image](https://remnote-user-data.s3.amazonaws.com/fLrXE5uutCE3Dxlcwm1X9-t5MmQHiCsNcBBysgyBxKEZVGHjwdY7MseUiTCtD6vVey5A554Gqr4c20-0CYbTh0s9X2NfsXW08ZYZEFT9HGCsudajGhGScSGsle07Qs46.png)

- Tuples from relation are stored together in blocks, but not necessarily sorted.

### Clustering Index

![Image](https://remnote-user-data.s3.amazonaws.com/oPInVTKpSpZaLHZ31wgy9PYEeGJSuZofAQY0YNjsVNbZUFOyOeCUlxdHc0OU4AjFVWlmNAEhGUOgdC-3oYKXXiKPIIS3A5a_A3ipKoB8NmUCtBio4ux472YIC2Kcmg-v.png)

- Index that allows tuples to be read in an order that corresponds to physical order.

## Scanning

### Index Scan

- Retrieve blocks for **R**.
- Read only those tuples of a relation **R** that satisfy some predicate.
- An index exists on some attribute of **R**.

#### I/O Cost

- If not clustered → **T(R)** disk accesses.
- If clustered → B(R) + B(I_R) disk accesses.
  - B(R) >> B(I_R), so treat as only B(R).
- Use index to find all blocks holding **R**.

### Table Scan

#### I/O Cost

- If **R** is not clustered → **T(R)** disk accesses.
- If **R** is clustered → **B(R)** disk accesses.
- All blocks known to the system.
- Tuples arranged in blocks.
- Possible to get blocks one at a time.
- Read all of the tuples of a relation **R**.

## One-Pass Algorithms

- Read data from disk only once.
- Typically require that at least one argument fits in main memory.

### Unary (Tuple at a Time)

![Image](https://remnote-user-data.s3.amazonaws.com/Rj4Wv4shHf1n8FVo94Jbv2xu3YwA0LtFu8op3RcgMhN1YEW1a-j4fZyai0qgazO6n-S7nU8dp9jblh5MJEM7XBUgALSoMvvsx2J2Ik-Yk0sw-E7zoK_5gZRF7Y0E4Uv7.png)

- For each block of **R**:
  - Perform operation (select, project) on each tuple in block.
  - Copy block to input buffer.
  - Move selected/projected tuples to output buffer.

#### Cost

- Requires **M ≥ 1**.
- If operator is a select that compares an attribute to a constant and index exists for attributes used in select, **< B(R)** disk accesses.
- Generally **B(R)** or **T(R)** disk accesses depending on clustering.

### Unary (Full Relation)

![Image](https://remnote-user-data.s3.amazonaws.com/4U3htTPnZPI7dmDJX3mSnZgRG6v0vwYM13yNvTvONoE34yKN0FEzRdfdcpnzxmF-xKRJ0SAl0SakX4TKxGni-KjnVCc_wP7KljJmTG33AM1ch2A5lRndnCLEX_DH2udR.png)

- For each block of **R**:
  - Update accumulator.
  - Copy block to input buffer.
  - Move tuples to output buffer.

#### Duplicate Elimination

- Cost is **B(R)** disk accesses.
- Requires **M ≥ B(δ(R)) + 1** blocks of main memory.
  - **1** block for input buffer.
  - **M-1** blocks for accumulator.
- Accumulator implemented as in-memory data structure (tree, hash).
- For each block of **R**:
  - If tuple is not in accumulator:
    - For each tuple in block:
      - Copy to accumulator.
      - Copy block to input buffer.
      - Copy to output buffer.
- If fewer than **B(δ(R))** blocks available, thrashing likely.

#### Grouping

- Grouping operators: min, sum, avg, count, max.
- Output only when all blocks of **R** have been consumed.
- Cost is **B(R)** disk accesses.
- Accumulator contains per-group values.

## Binary (Full Relation)

- In general, cost is **B(R) + B(S)**.
  - **R**, **S** are operand relations.
- Requirement for one-pass operation: \(\min(B(R), B(S)) \leq M-1\).

### Join

- Two relations, **R(X,Y)** and **S(Y,Z)**, where **B(S) < B(R)**.
  - Uses main memory search structure keyed on **Y**.

## Nested-Loop Joins

- Assuming we're joining relations **R**, **S** on attribute **C**.
#### python
```python
for each tuple r in R
for each tuple s in S
if r.C = s.C then output r,s pair
```


### Factors that affect cost

1. Do indexes exist?
2. Are tuples of relation stored physically together? (clustered)
3. Are relations sorted by join attribute?

### Example

- Consider a join between relations $(R_1), (R_2)$ on attribute **C**.
  - ($T(R_2) = 5,000)$.
  - $(T(R_1) = 10,000)$.
  - $(M = 101)$ blocks.
  - $(S(R_1) = S(R_2) = 1/10)$ block.

#### Attempt #1: Tuple-based Nested Loop Join

- Relations not contiguous (not clustered).
  - One disk access per tuple.
- Cost for each tuple in \(R_1\) = cost to read tuple + cost to read \(R_2\).
- Total Cost = \(T(R_1) \times (1 + T(R_2)) = 50,010,000\) disk accesses.

#### Attempt #2: Block-based Nested Loop Join

- Changes:
  - Read all of inner relation $(R_2)$ (using 1 block) + join.
  - Use all available main memory $(M = 101))$.
  - Read outer relation $(R_1)$ in chunks of 100 blocks.
- Cost to read one 100-block chunk of$ (R_1) = (100 \times \frac{1}{S(R_1)} = 1,000)$ disk accesses.
- Cost to process each chunk = \(1,000 + T(R_2) = 6,000\).
- Total Cost = \(\frac{T(R_1)}{1,000} \times 6,000 = 60,000\) disk accesses.

#### Attempt #3: Join Reordering

- Changes:
  - Reverse the join order.
    - \(R_1\) becomes the inner relation.
    - \(R_2\) becomes the outer relation.
- Cost to read one 100-block chunk of $(R_2) = (100 \times \frac{1}{S(R_2)} = 1,000)$ disk accesses.
- Cost to process each chunk = $(1,000 + T(R_1) = 11,000)$.
- Total Cost =$(\frac{T(R_2)}{1,000} \times 11,000 = 55,000)$ disk accesses.

#### Attempt #4: Contiguous Relations

- Changes:
  - The tuples in each relation are contiguous (i.e., clustered).
- \(B(R_1) = 1,000\).
- Cost to read one 100-block chunk of \(R_2\) = 100 disk accesses.
- \(B(R_2) = 500\).
- Cost to process each chunk = \(100 + B(R_1) = 1,100\).
- Total Cost = $(\frac{B(R_2)}{100} \times 1,100 = 5,500)$ disk accesses.

#### Attempt #5: Merge Join

- Changes:
  - Both relations are contiguous and sorted by **C** (the join attribute).
- Total Cost = \(B(R_1) + B(R_2) = 1,500\) disk accesses.

![Image](https://remnote-user-data.s3.amazonaws.com/RM0LboPUn1cnSHG7w0vt8ZBp1NRb5fyOowshRdCE__ywTCdu5rNtq8rLmcqC4c25yLMCXnnKVsI0gdDm4lfOeM0eC7DLxADN_RJNGXphfzikLWY9Yz15dqceuEQOw8fU.png)


# Two-Pass Algorithms

## Improving on last example
- What if $R_1$ and $R_2$ aren't sorted by **C**

## Merge Sort
- Read all chunks + merge + write out
  - Cost
  - Sort cost $R_2 = 2,000$ disk accesses
  - Each tuple is read, written, read, written
  - Sort cost $R_1 = 4,000$ disk accesses
- ![|400](https://remnote-user-data.s3.amazonaws.com/52Ghi-prBmg3W9asNmyqfSYMZVcy1gczGVgQ7yfs9glbaVF2mD3VN-PnNI_bWragBzUKe2XFGWoMXAXEAhwBejvNjRd8SVcVLRAWWdqxm47iK11UKrvCoqAGQUKSYdPn.png) 
- For each 100 block chunk of **R**
  - Write to disk
  - ![|400](https://remnote-user-data.s3.amazonaws.com/amI7b2acz9Pf-g3iEZEJpG-tWt03L9wEoZIbfYIjPsiGi6lepkfm5Tizev9ZAob3CFgpiGRaAoVHmoawtIuOtB5dsGsp24MflbPc8EeBEGFJDlHMDNJj2jbQl3PlXmZW.png) 
  - Sort in memory
  - Read chunk

## Attempt #6: Merge Join with Sort
- If $R_1,R_2$ contiguous, but unordered
  - Total Cost = sort cost + join cost = $7,500$ disk accesses
  - Nested loop cost = $5,500$ disk accesses
  - So merge join does not necessarily pay off
- If $R_1=10,000$ blocks, contiguous
  - $R_2=5,000$ blocks, not-ordered
    - Merge join cost = $75,000$ disk accesses
    - Nested loop cost = $505,000$ disk accesses
    - So in this case merge join is better

## Attempt #7: Improved Merge Join
- Changes
- Do the entire files need to be sorted?
  - ![|400](https://remnote-user-data.s3.amazonaws.com/H-4htbu_YHdmc9NBB_SzCtnAiHfoBqk69h_tVu83hp9njiGDBWyfYJ5ABRPpjkNYNG9wTQ8bYg71PHlKSL8Hd8a2UKu2UHsA5TKzHhpVN0_BqE8GKYBt0xBD9aqtIxC1.png) 
- Read $R_1$ and write $R_1$ into runs
- Read $R_2$ and write $R_2$ into runs
  - Merge join
- Total Cost = $2,000 + 1,000 + 1,500 = 4,500$ disk accesses

## Two Pass Algorithms using Hashing
- Hash-Join
  - Read $R_2$ and write into buckets
  - The tuples in $R_1$ and $R_2$ are both hashed using the same hashing function on the join attributes
  - Join $R_1,R_2$
  - Total Cost = $3*(B(R_1)+B(R_2))=4,500$ disk accesses 
  - Read $R_1$ and write into buckets
- Partition relation into **M-1** buckets
  - In general
    - Hash tuple to bucket
    - When bucket is full, move to disk and reinitialise bucket
    - Read relation a tuple at a time

# Indexed Based Algorithms

## Attempt #8: Index Join
- Changes
  - Assume $R_2.C$ index exists; 2 levels
  - Assume $R_1$ contiguous, unordered
  - Assume $R_2.C$ index fits in memory
  - What if we have an index on the join attribute
- Cost = Reads: $500$ disk accesses
  - For each $R_1$ tuple
    - If match, read $R_2$ tuple: 1 disk access
    - Probe index - free

    - If match, read $R_2$ tuple: 1 disk access
    - Probe index - free
