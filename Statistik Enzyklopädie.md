#Statistik #Zusammenfassung #Mathe



## Probabiblity Theory


Probability is a measureof uncertainty of the occurence of an event. 
With an event being all desired outocmes out of all possible outcomes.

Mathematically, the *Probability P(A)* of an event A out of all outcomes $\Omega$ as 
$$
P(A) = {\frac{|A|}{|\Omega|}}
$$

The principle is, that you suppose there are *n* possible outcomes, each equally likely. For k desired outcomes, the probability of a desired outcome is k/n.


## Sets

![[Pasted image 20261029105915.png]]


### Rules of sets

![[Pasted image 20261029105923.png]]

### Venn Diagrams
![[Pasted image 20261029105954.png]]

### Cartesian product

The cartesiann product of two sets A and B is the set of all ordered paris.
$$
A \times B = \{(a,b): a \in A \wedge b \in B\}
$$
![[Pasted image 20261029110155.png]]


## Inclusion-Exclusion Principle
![[Pasted image 20261029110215.png]]

The same goes for 3 finite sets

$$

  |A \cup B \cup C| = |A| + |B| + |C| - |A \cap B| - |A \cap C| - |B \cap C| + |A \cap B \cap C|

$$



$$

  \left| \bigcup_{i \in I} A_i \right|
  = \sum_{\emptyset \neq J \subseteq I} (-1)^{|J|+1}
    \left| \bigcap_{j \in J} A_j \right|

$$

using $I = \{1, 2, \ldots, n\}$ and sum over all non-empty index subsets $J \subseteq I$.


### Example
![[Pasted image 20261029110849.png]]



## Combinatorics

### Factorial

$$
n! = n(n-1)(n-2) \cdots 3 \cdot 2 \cdot 1
$$
With $0! = 1$

### Binomial Coefficient

$n,k \in \mathbb{N}_{0}$ with $0 \leq k \leq n$


$$
\binom{n}{k} = \frac{n!}{k!\,(n-k)!}
$$


n choose k

### Product Rule

If there are n ways to perform action 1 follows by m ways to perform action 2, there
are $n \cdot m$ ways to perform action 1 followed by action 2.

For example consider 8 participants in a tournament. How many ways are there to awarded gold silver and bronze medals? 
$$
8 \cdot 7 \cdot 6 = 336
$$


### Permutation without repetition

A permutation is a rearrangement of distinct elements. Ordered!

The sequence (1,2,3) can rearranged with 3! 

Another example:

How many different shuffles of a poker deck are there? 52!

### Variation without repetition

Variation without repetition are ordered selections of k different elements out of n. Ordered!

By the product rule we get: 

$$
n(n-1) \cdots (n-k+2)(n-k+1) = \frac{n!}{(n-k)!} = k! \binom{n}{k}
$$

### Combination without repetition

A combination without repetition is a selection of k elements out of n elements. Or it can also be seen as: a subset of size k from a set of size n. Unordered


$$
n(n-1) \cdots (n-k+2)(n-k+1) = \frac{n!}{k!(n-k)!} = \binom{n}{k}
$$

#### Example
In poker, a hand consists of 5 cards out of a set of 52 cards. How many different hands are there? 
$$\binom{52}{5}$$

---

### Permutation with repetition

A permutation with repetition is a rearrangement of n elements consisting of k distinct elements. Ordered.

All 30 permutations of n = 5 (1,1,2,2,3) out of k = 3 different elements. There are n! permutations of n elements. Each $n_{i}$ times repetition of the same element is overcounted by $n_{i}!$ With $n_{1}+n_{2}+\dots+n_{k} =n$ we get the count:

$$
\frac{n!}{n_{1}!n_{2}!\cdots n_{k}!}
$$

#### Example 
![[Pasted image 20261029114001.png]]

There are 13 suits


### Variation with repetition

Variations with repetition are ordered repeated selections of k elements out of n. Ordered!

$$
n^k
$$
k might be bigger than n

An example: 

A 64 bit unsiged integer is a sequence of 64 zeroes or ones.
How many numbers can be represented?  $2^{64}$


### Combination with repetition

Combinations with repetition are repeated selections of k elements out of n. Or it can be seen as: size k multi-sets of elements from a set of size n. Unordered!

![[Pasted image 20261029114417.png]]
![[Pasted image 20261029114424.png]]
![[Pasted image 20261029114434.png]]

Those are the combination without replacement of k elements out of n-1+k

$$
\binom{n-1+k}{k}
$$

Which is the number of combinations of k elements out of n with replacement


#### Example
![[Pasted image 20261029114538.png]]


---
![[Pasted image 20261029114836.png]]




## Probability spaces


![[Pasted image 20261029114851.png]]
![[Pasted image 20261029114858.png]]
![[Pasted image 20261029114914.png]]

## Discrete Probability Spaces
