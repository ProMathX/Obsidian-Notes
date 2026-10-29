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


