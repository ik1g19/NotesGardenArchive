---
title: "Week 4"
---

# Relational Algebra
Relations are represented as a subset of a **cartesian product of sets** 
![|400](https://remnote-user-data.s3.amazonaws.com/JMjPbR21ZsOBpqK9C2kRI8ZPZtaz1hRhAoMkvRMZ4--F8QpoXdH18OBYTA1JLNyX5hQ9WoQ17N__Af9vImtYNmumfknsZKKrkJ7Qu2ULjr2YaEOrIP9XQcJafLJ9xb2S.png) 

Basic Notation
- K-Tuple - An ordered sequence of **k** objects (need not be distinct)
- K-ary Relation↔A subset of a cartesian product of **k** sets i.e. $R\subseteq D_1\times D_2\times ...\times D_k$ 

**k** is called the **arity or degree** of the relation

$D_i$ is the domain "allowed" values for elements in the **i**th position of a tuple 
## Tuples and Attributes

$R\subseteq D_1\times D_2\times ...\times D_k$ is a set of k-tuples and can be seen as a table with **k** columns
### Example Relation

![|400](https://remnote-user-data.s3.amazonaws.com/fMhwYjrBl3DXjdRbjORgdn3Tr1Hl7pLS_UFmox70aYdvnxyfh_GQ3GR2NWP-IUkEsp4KshhJHCNlvqpPnU-_n8V0nzYYE17a6pMavHBV3eU7nE8uNisce6MkcRrc2wNi.png) 

![|400](https://remnote-user-data.s3.amazonaws.com/5UMMcqcjBAne7Fm8pHIkVv423zwMHgRcAVKOFS5Q6tIcTu8WnIX2lB4VlwonTCXiEGMhp9GXTyoofKArm55QpFZlM2eP8eSv7cO55ZZuX7fYb_e37kTmp9csg9ivw7l8.png) 

In the relational data model, we want to have names for the columns; called the **attributes** of the relation 

![|400](https://remnote-user-data.s3.amazonaws.com/RDzZXVVpsMQIEKg5zz8oLL2hAFA3ygZ1H-WRcNp_0IeCE1_NPooea5c6tRkbvrx9R_zS-Unxkau5Zjdf7_vPtGKyOgUMHzfr8cm20cVTlMzu5Q56Os8XBL1z4LE9hATH.png) 

In the **i**th column only values from $D_i$ are allowed
## Properties of Relations

A relation $R(A_1,...A_k)$ has the following properties

Each row represents a K-Tuple of R

The values of an attribute are all from **the same domain** 

Each attribute of each tuple in a relation contains **a single atomic value** 

The ordering of rows is **immaterial** 
- Relations are just sets

All rows are **distinct** 
- Relations are just sets

Named perspective
- The significance of each column is conveyed by the name we give it
- The ordering of the attributes is not significant

Unnamed perspective
- The ordering of attributes is significant (we can access columns by their positions)
## Relation Schemas and Relational Database Schemas

A k-ary relation schema $R(A_1,A_2,...,A_k)$ is 
- A relation name e.g. $R$

Its attributes
- An ordered sequence (A_1,A_2,...,A_k) of **k** attributes (unnamed perspective)
- Or a set of attribute name (named perspective)

A k-ary relation schema is **a template** for some k-ary relation

In a DBMS implementation, the schema gives a **more** precise definition of the types i.e. attribute domain

![|400](https://remnote-user-data.s3.amazonaws.com/xLvnxXY4P6j5BFthYfE_XrSAauk6swslot8nT8g2VPXm4NXBe_fFOvtzMHU-wHqtN_Y2v_o_I7aUvSxuzheD27IwyAUiYloX7GtWRuvCwpKdLHMUuzL7NDf_DwM4Km6l.png) 

An instance of a relation schema is a relation **conforming to the schema** 

A relational database schema is a set of relation schemas $R_i(A_1,A_2,...,A_{k_i})$

A relational database instance, or a database of a relational schema is a set of relations $R_i$ each of which is an instance of the relation schema $R_i$
## Relational Intension vs Extensions
### Intension

Relation schema

Relational database schema
### Extension

Relational database instance (i.e. database)

nstance of a relation schema
## Relational Algebra Operators
### Projection

Example

![|400](https://remnote-user-data.s3.amazonaws.com/lfQvKlpKAXikJAUOlMNg9mfwB_9b2ZDauWUyq4SXnshioGcGCekTqdcKpq306GNKLXLu1OnisUamWGzlXCsfKs1Ox-anSw07JUeXl-y8zWrLGQ7SsEUBihHlZ3YFqwOM.png) 

![|400](https://remnote-user-data.s3.amazonaws.com/W3kKQTjfRBFg2X1yM22WQaduhiYSgp6vsfLvYYlA6Wb6zBRKYXQjmD5rrMo54_Jc7vz72owT-bm3r3pUvhjwWA51QNpmW0ucLrvgmdsq3tp7T5tLRbM6BMf5zG8Q06Ws.png)

Or, using positions

![|400](https://remnote-user-data.s3.amazonaws.com/ydPb3jVigvdzWxO_zLKBDQpeRFqvkYrGV2zCBgvkfafrbkAir32naAU_X_ycBejN0dxl59b2f7U2-vQ_4XasrQVhi1UT3Mz-NepnjzGhkdpB3eM3NUiH4iep3SfJlHjN.png) 

Projection is a unary operation of the form $\pi_{<\text{attribute list}>}(<\text{relation name}>)$
- When projection is applied to **R** 
	- The remaining columns may be re-arranged according to the order in the  __attribute list__  
	- Any duplicate rows are also eliminated
	- It removes all columns whose attributes do not appear in the  __attribute list__  

A relational algebra expression is **a string obtained from relation schemas using relational algebra operators**
### Renaming
$\rho _{A/B}(S)$ is a relation with schema identical to **S** but the attribute name $A_i$ has been replaced by $B_i$

![|400](https://remnote-user-data.s3.amazonaws.com/IMSaNZOeW4vdJVwikuQBSfU3k4Pft2b4y_-8EDfwNSmXZAjdXLSgmNv6bmHZ9mlvgNAY14L8WXdmGBjKy9vNQxFCU_6vwkK9Bt317j8ewG76yCjQZsSNptjeZNbtXB0n.png) 

![|400](https://remnote-user-data.s3.amazonaws.com/h7kQJLB-q4zZRycaFs2Lhxvh-b2mp4Oxa_8Q7Xnw3cHO2iaE_TNUGwcRLhQjxCGdTjlkqWsbpWWuLHqbvwNfizxk8VRSBDhsaJdPrGoItFBxxpuPKYsonN3CFKH2T0dH.png) 

Rename multiple attributes using ',' in the subscript

![|400](https://remnote-user-data.s3.amazonaws.com/0778Z_9gA8BuIMo-oqr9IbHLwFCexVInnay1yq6rDxbRV9smksxk4Tv9vHwfGRaaS4NYgf0xKwy2gmi3VqHvciRaqbqH2lFO6neNbuGBz7ER0yi_xkgrIeVsN5qRc8LM.png) 
### Decomposing Complex Operations

We name intermediate expressions using the assignment operator \leftarrow

![|400](https://remnote-user-data.s3.amazonaws.com/ZiQnqkYOoht1z8WTl0SUbCWKYWpL7fnwaQ1mWCmjAoZzrE3OR2gwEW5HcF9cMiCBbKyAIjML0bHIfghDDPm4-fBYZTfBzWKBT61p7tVC5sHbEvdVrneOfdSsJTo8438c.png) 

We can combine relational algebra operations to build more complex expressions
### Rules for Group 1 Operators
#### Cartesian Product
- $R\times S \neq S\times R$
- $R\times (S\times T)=(R\times S)\times T$
- $R\times (S\text{ }\cup\text{ }R_iT)=(R\times S)\text{ }\cup\text{ }(R\times T)$ (distributivity law)
#### Union
- $R\text{ }\cup\text{ }S=S\text{ }\cup\text{ }R→Commutativity law$ (order is unimportant)
- R$\text{ }\cup\text{ }(S\text{ }\cup\text{ }T)=(R\text{ }\cup\text{ }S)\text{ }\cup\text{ }T→Associativity law$ (can drop parentheses) 
#### Difference
- $R-S\neq S-R$
### Selection
#### Algebraic Laws for Selection
- $\sigma_{\theta_1}(\sigma_{\theta_2}(R))=\sigma_{\theta_2}(\sigma_{\theta_1}(R))$
- $\sigma_{\theta_1}(\sigma_{\theta_2}(R))=\sigma_{\theta_1 \land \theta_2}(R)$
- $\sigma_\theta(R\times S)=\sigma_\theta(R)\times S if \theta$ mentions only attributes of R

Selection is a unary operation of the form $\sigma_{\theta}(R)$
- Returns the subset of **R** consisting of all rows that satisfy $\theta$
- Where **R** is a relation and \theta is a **condition or predicate** 
### Derived Relational Algebra Operations

#### Equijoin and Natural
- Natural Join - An equijoin over all the common attributes of the joined relations
	- One occurrence of each common attribute is removed from the resulting relation

Example

![|400](https://remnote-user-data.s3.amazonaws.com/7L4RHAbgI0c2kjF5tOq8Gar7kqv38LkLhsLme9mLWWZmUkqgOqsJRXFe6NBRBcdcO5QrIDzPRVgLiHutUxCG_cJPXKKJEF3SmKJ9bG9JJmcCWjcprV04oOmxGfoz-jU9.png) 
	- Let A_1,...,A_k be the common attributes of two relation schemas **R** and **S**

The natural join of **R** and **S**is
		- $R\bowtie S=\pi_{\text{<list>}}(\sigma_{R.A_1=S.A_1\wedge ... \wedge R.A_k=S.A_k}(R \times S))$
		- Where `<list>` contains all attributes of $R\times S$, except for $S.A_1,...,S.A_k$ (duplicate columns are eliminated)
- Equijoin - A theta join in which the only predicate operator used is equality (=)
#### Outer Join
- Right Outer Join
	- $R\text{ }⟖\text{ }S\equiv→S\cup*\text{ }(R\bowtie S)$  
- Full Outer Join
	- Example
		- ![|400](https://remnote-user-data.s3.amazonaws.com/0dem-V4-pRCgCQKC33R-uTsSjSJRHHpNoWHQKkSo1Np-gGU19U4_Z_EmHkBqzak_7OBaIkcl-W18Od84Pp3goAwgQbbdkOn6YtdcCY2YNmhcKy3bo534GRjlDUUnlpTT.png) 
	- $R\text{ }⟗\text{ }S\equiv→R\text{ }\cup*\text{ }S\cup*\text{ }(R\bowtie S)$
- Semijoin $(R\text{ }▷_F\text{ }S)$
	- Contains all the tuples of **R** which are in the join of **R** and **S** with predicate **F**
	- $R\text{ }▷_F\text{ }S\equiv→\pi_A(R\bowtie_FS)$
	- Example
		- ![|400](https://remnote-user-data.s3.amazonaws.com/MfSBD-GF9Fbb21_5hu38vflykz0BNF_XeJYxyrGEFc4z6fZkbmkp19Kg2YNvMWQDQ8LknKtbRSZz7fpHLeAH4PIfagux-bPn8l_1STKoHvH_EtjD0jhPA4M_UqH3eT3o.png) 
- Left Outer Join $(R\text{ }⟕\text{ }S)$
	- A natural join which also includes tuples from **R** which do not have corresponding tuples in **S**
	- Derives from
		- Where
			- {<null, ... , null>} is a relation on attributes in **S** but not in **R**, that contains a single tuple
			- r_1,r_2,...,r_n are the attributes in **R**
		- $R \bowtie S\text{ }\cup\text{ }((R-\pi_{r_1,r_2,...,r_n}(R\bowtie S))\times\{\text{<null, ... , null>}\})$
		- or  $R \cup*(R\bowtie S)$
	- Missing values are set to null
	- Example
		- ![|400](https://remnote-user-data.s3.amazonaws.com/f8kv4M3bqtP9mRNQGJMStFLR3RBoz5Fc-CdyXBUliUf5GdY7C53RjuyVcTUl3TO1jCfLP9hSRPrk_Kme9VjxYn4i8dcGrxqM1CyR-w105NJkHAY6XGj_BMykPwVqtWmT.png) 
#### \Theta-Join
- Example
	- ![|400](https://remnote-user-data.s3.amazonaws.com/CjltQrOP8etUjEOWaKGD2iEJyQGaF0aYA9agOIyo-aB7ghQ6w9b-cMVVmvf6YQ41VLU1g1C28AY25QfkMnGRNUEhHSWT9COyi4Hr-s8dRvMSJVvASBJ0X0Wd4klBftE8.png)
- Shorthand notation is $\bowtie$ 
- A special query of the form $\sigma_{\Theta}(R\times S) $
- When we combine relations
- $R\bowtie_{F}S\equiv \sigma_{F}(R\times S)$

Some operations can be derived by other relational algebra operations
### Union

In another variant the attributes have to have the same name, we rename the attributes of **S** using the renaming operator

![|400](https://remnote-user-data.s3.amazonaws.com/FZug77or6TSuxxq3RnWT3YYTxt5WxMsBca50b9AuoM45AJe64MF9nKyGzcGMG22CX9yq0SnSaA3wfBFUI2cP2RgYDbRRwDuWDDUIIlJbRZp3IBswqU-PyzcbZLNd3S0-.png) 

Both arguments to the union must be relations of the same arity

For $R \text{ }\cup \text{ }S$ , returns relations in **R** or **S**

In one variant the attributes of **R** and **S** don't have to have the same name
- We give the attributes of the result new names
- ![|400](https://remnote-user-data.s3.amazonaws.com/qSFBbxwreL-EP3114ozrBZzhQRBX6gEjM8muntLnNWGEMTXh0kG7I5nniyoLoF_Ttj1SopMKF3fzVjs82OonhKV7XVz9ijiGzRQJFWgr33HE3FBOILoGPzpiroFxdrE1.png) 
### Set-Theoretic Operations
#### Difference
- In SQL, both union and difference require the same datatype
- Both arguments must have the same arity
- ![|400](https://remnote-user-data.s3.amazonaws.com/Y5Ewxz9n7Wsp1DcuhhWdwXd9NZKWCg--GjmIrydvzw9uAiKB5wm6trgUWlW3je0SpXPvEFWLGl3mGyYvNbFXIGCDdoI-8MIm0vjbzvZ5d7OsX6BVa_h5sKZHT6F23-MX.png) 
- For R-S, returns relations that are in **R** but not in **S** 
#### Cartesian Product

![|400](https://remnote-user-data.s3.amazonaws.com/nrZP7jIdCJSgvrJEoAPOXM8sFH4nzw2vPer4Aso6SZY9svZD7LBA-stQdrITTvRwL5zJ-ZseyL40OU6Whzdf_YCwSzDFQPxWu4syOKqSVjP-FLPSKEgt5UVf_n6mk6Qd.png) 
## Relational Transformations

Conjunctive selections cascade into individual selections

$\sigma_{p\wedge q\wedge r}(R)=\sigma_p(\sigma_q(\sigma_r(R)))$

Selection is commutative 
#### $\sigma_p(\sigma_q(R))=\sigma_q(\sigma_p(R))$

Only the last in a sequence of projections is required 
#### $\pi_L\pi_M...\pi_N(R)=\pi_L(R)$

Selection and projection are commutative (if the predicate only involves attributes in the projection list)

$\pi_{A_1,...,A_m}(\sigma_p(R))=\sigma_p(\pi_{A_1,...,A_m}(R))$

Cartesian product and theta join are commutative when using the named perspective

$R\times S=S\times R$

$R\bowtie_pS=S\bowtie_pR$

Selection distributes over theta join, if the predicate only involves attributes being joined

$\sigma_p(R\times S)=\sigma_p(S)\times\sigma_p(R)$

$\sigma_p(R\bowtie_rS)=\sigma_p(S)\bowtie_r\sigma_p(R)$

Projection distributes over theta join (if projection list can be divided into attributes of the relations being joined, and join condition only uses attributes from the projection list) 
#### $\pi_{L_1\cup L_2}(R\bowtie_r S)=\pi_{L_1}(R)\bowtie_r\pi_{L_2}(S)$
#### $\pi_{L_1\cup L_2}(R\bowtie_r S)=\pi_{L_1\cup L_2}(\pi_{L_1\cup M_1}(R)\bowtie_r \pi_{L_2\cup M_2}(S))$

Set union and intersection are commutative 
#### $R\cup S=S\cup R$
#### $R\wedge S=S\wedge R$

Selection distributes over set operations

$\sigma_p(R\cup S)=\sigma_p(R)\cup\sigma_p(S)$

$\sigma_p(R\wedge S)=\sigma_p(R)\wedge \sigma_p(S)$

$\sigma_p(R-S)=\sigma_p(R)-\sigma_p(S)$

Projection distributes over set union 
#### $\pi_L(R\cup S)=\pi_L(R)\cup\pi_L(S)$

Associativity of theta join and cartesian product

$(R\times S)\times T=R\times(S\times T)$

$(R\bowtie S)\bowtie T=R \bowtie(S\bowtie T)$

Associativity of set union and intersection

$(R\cup S)\cup T=R \cup(S\cup T)$

$(R\wedge S)\wedge T=R \wedge(S\wedge T)$
## Relational Algebra and SQL

```sql
SELECT Ri1.A1, ..., Rim.Am
FROM R1, ..., Rk
WHERE Θ
```


R_1, ..., R_k are distinct relation names (no repetitions) 

Each $R_{ij}.A_j$ is→an attribute of $R_{ij}$ $(1\leq ij \leq k)$ 

$\Theta$ is a **condition**
### SQL vs Relational Algebra
#### WHERE - Selection $\sigma$ 

SELECT↔$\sigma_{p\wedge q\wedge r}(R)=\sigma_p(\sigma_q(\sigma_r(R)))\sigma_{p\wedge q\wedge r}(R)=\sigma_p(\sigma_q(\sigma_r(R)))Projection \pi$ 
#### FROM - Cartesian Product
- Example
- ![|400](https://remnote-user-data.s3.amazonaws.com/trn1JfC2tJlfE797MPZMiUH0D4CRzrJCKfZVepgDhvRhitoDXKSrgn-MCkK3ZY_Z5KEwQQ6NkoUHqHTEulaQC7rxqtrKxuFXi07hYAsh-fHZkW_vNRtPrG1rF6BZtnU9.png) 
### Aliases in SQL

SQL allows for the renaming of attribute names in the SELECT list
- ![|400](https://remnote-user-data.s3.amazonaws.com/BfskpXGouPoMKfixR5uvKahcS6N46TYQ7SQ90kOTFMqDuj_O8_XB6gjqMbjJaBSR9PHgNTefSlwUZmzmzGVx_XakGxQJUYtRUyABuPxL95xdtIpnM2GzKM6yUjjT78uW.png)

SQL does not support referencing columns by position number

Aliases allow us to **give multiple names to a relation** 

SQL supports an aliasing mechanism

Aliases are created in the FROM list

The new names can be referenced in the SELECT list and in the WHERE clause
### Sets vs Multisets

Duplicates are not eliminated in SQL due to efficiency and necessity
- **DISTINCT** is used to eliminate duplicates
#### Operations on Multisets (Bags)
- If **R** is a multiset, then $\pi_X(R)$ is a multiset
- Cartesian Product (If $t\in R$ and $t'\in S$)
	- $\mu(tt',R\times S)=\mu(t,R)\text{ }\mu(t',S)$
##### Union R $\cup$ S
-$\mu(t,R\cup S)=\mu(t,R)+\mu(t,s)$
- Difference R-S
	-$\mu(t,R-S)=max\{\mu(t,R)-\mu(t,S),0\}$
- If **R** is a set, then $\sigma_{\Theta}(R)$ is a **set**
- If **R** is a multiset, then $\sigma_{\Theta}(R)$ is a **set**
- If **R** is a set, then $\pi_X(R)$ is a **multiset**
- Intersection $R\wedge S$
	- $\mu(t,R\wedge S)=min\{\mu(t,R),\mu(t,S)\}$
#### Multiset/Bag Semantics in SQL
- Relational algebra expressions take **relations as arguments and return relations** as values
	- All duplicates are eliminated in relational algebra
- SQL (SELECT, FROM, WHERE) does not eliminate duplicates unless explicitly requested
	- Takes **multisets as arguments and returns multisets** as values
	- May return a multiset, even if the arguments are sets

The multiplicity $\mu(x,B)$ of an element **x** in a multiset **B** is **the number of occurrences of that element in the multiset** 

Set - A collection of distinct objects

Multiset/Bag - A collection of not necessarily distinct objects

SQL is relationally complete

Relationally Complete - Can express all relational algebra queries