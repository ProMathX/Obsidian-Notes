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

A discrete probability space is determined by the sample space being countable.
$$
\Omega = \{\omega_{1},\omega_{2},\omega_{3},\dots \}
$$
The probability mass function $P:\mathfrak{S} \to [0,1]$ is uniquely defined by the pribability of hte elementary events 

$$
p_{i} = P({\omega_{i}})
$$
![[Pasted image 20261029115739.png]]

#### Example 1
![[Pasted image 20261029120040.png]]

#### Example 2

Version 1
![[Pasted image 20261029121951.png]]

Version 2
![[Pasted image 20261029121958.png]]

#### Example 3 
![[Pasted image 20261029122521.png]]

#### Example 4
![[Pasted image 20261029122542.png]]

## Continuous Probability spaces

How long does a light bulb last?

Random experiment : take a lite bulb (all of the same making) and let it burn till it dies
Sample Sapce = $\Omega = [0, \infty\} \subset \mathbb{R}$, any non-negative real value

Probability: We now a continuum of possible outcomes!

Therefore we need the concept of probability density function and replace summation with integration.



## Rules of Probability

### Kolmogorov Axioms

From now on we assume $(\Omega, \mathfrak{S}, P)$ to be an arbitrary probability space.

1. Non-Negativity $$ P(A) \geq 0 \\ \forall A \in \mathfrak{S}$$
2. Unit-Measure $$P(\Omega) = 1$$
3. $\sigma$- Additivity: For any sequence of disjoint events $A_{i}$ holds $$P\left( \bigcup_{i=1}^{\infty} A_i \right) = \sum_{i=1}^{\infty} P(A_i)$$

### Rules

Given two events $A, B$ then $A^c$, $A \cap B$ and $A \cup B$ are also events and the following holds:

**(Finite) Additivity:** $A \cap B = \emptyset$ implies $P(A \cup B) = P(A) + P(B)$.

First set $A_1 = \Omega$ and $A_i = \emptyset$ for all $i \geq 2$, then

$$
P(\Omega) = P\left( \bigcup_{i=1}^{\infty} A_i \right) = P(\Omega) + \sum_{i=2}^{\infty} P(\emptyset)
$$

which implies $P(\emptyset) = 0$.

Now set $A_1 = A$, $A_2 = B$ and $A_i = \emptyset$ for all $i \geq 3$, then the $\sigma$-Additivity reduces to

$$
P(A \cup B) = P\left( \bigcup_{i=1}^{\infty} A_i \right) = \sum_{i=1}^{\infty} P(A_i) = P(A_1) + P(A_2) + \sum_{i=3}^{\infty} P(\emptyset) = P(A) + P(B).
$$

**Mutual Exclusivity:** $A \cap B = \emptyset$ implies $P(A \cap B) = 0$.

We already know that $P(\emptyset) = 0$, therefore $P(A \cap B) = P(\emptyset) = 0$.

**Complement:** $P(A^c) = 1 - P(A)$

$$
1 \overset{2}{=} P(\Omega) = P(A \cup A^c) \overset{3}{=} P(A) + P(A^c)
$$

**Inclusion-Exclusion Principle:** $P(A \cup B) = P(A) + P(B) - P(A \cap B)$

$$
\begin{align}
P(A \cup B) &\overset{3}{=} P(A \setminus (A \cap B)) + P(B) \tag{1} \\
P(A) &\overset{3}{=} P(A \setminus (A \cap B)) + P(A \cap B) \tag{2} \\
P(A \cup B) - P(A) &= P(B) - P(A \cap B) \tag{1 - 2}
\end{align}
$$

**Monotonicity:** $A \subseteq B$ implies $P(A) \leq P(B)$

$$
P(A) \overset{1}{\leq} P(A) + P(B \setminus A) \overset{3}{=} P(B)
$$

to list a few, Venn diagrams are useful for understanding.


---


### Conditional Probability


*Given more information changes the Probability*

*Conditional probability* answers the question of how the *probability of an event changes when we have additional information*.

**Conditional Probability:** The *conditional probability* of $A$ given $B$ if $P(B) > 0$ is *defined* by

$$
P(A \mid B) = \frac{P(A \cap B)}{P(B)}
$$

**Useless Information:** If $B = \Omega$ then $P(A \mid B) = P(A \mid \Omega) = P(A)$

**Disjoint Events:** If $A \cap B = \emptyset$ then $P(A \mid B) = 0$

**All Information:** If $A \supseteq B$ then $P(A \mid B) = 1$

---



*Example: Sum of dice knowing one*

What is the probability of the *sum of two 6-sided dice being 9*, denoted $S_9$, *given that one of the dice is a 5*, denoted $D_5$?

Setting up the sample space $\Omega = \{(1,1), (1,2), \ldots, (6,6)\}$ as all tuples of 1 to 6 then

$$
\begin{aligned}
S_9 &= \{(3,6), (4,5), (5,4), (6,3)\}, \\
D_5 &= \{(1,5), (2,5), (3,5), (4,5), (5,5), (6,5), (5,1), (5,2), (5,3), (5,4), (5,6)\}
\end{aligned}
$$

leading to

$$
P(S_9) = \frac{|S_9|}{|\Omega|} = \frac{1}{9}, \qquad P(D_5) = \frac{|D_5|}{|\Omega|} = \frac{11}{36}.
$$

Knowing one die is a 5 changes the probability of obtaining 9 as the sum of dice

$$
P(S_9 \mid D_5) = \frac{P(S_9 \cap D_5)}{P(D_5)} = \frac{2/36}{11/36} = \frac{2}{11}
$$

---

*Example: Sum of dice knowing one*

Intuition, assuming equal probability for elementary events.

What is the probability of the *sum of two 6-sided dice being 9*, denoted $S_9$, *given that one of the dice is a 5*, denoted $D_5$?

|       | 1 | 2 | 3 | 4 | 5 | 6 |
|:-----:|:-:|:-:|:-:|:-:|:-:|:-:|
| **1** | $(1,1)$ | $(1,2)$ | $(1,3)$ | $(1,4)$ | $\color{blue}{(1,5)}$ | $(1,6)$ |
| **2** | $(2,1)$ | $(2,2)$ | $(2,3)$ | $(2,4)$ | $\color{blue}{(2,5)}$ | $(2,6)$ |
| **3** | $(3,1)$ | $(3,2)$ | $(3,3)$ | $(3,4)$ | $\color{blue}{(3,5)}$ | $(3,6)$ |
| **4** | $(4,1)$ | $(4,2)$ | $(4,3)$ | $(4,4)$ | $\color{green}{(4,5)}$ | $(4,6)$ |
| **5** | $\color{blue}{(5,1)}$ | $\color{blue}{(5,2)}$ | $\color{blue}{(5,3)}$ | $\color{green}{(5,4)}$ | $\color{blue}{(5,5)}$ | $\color{blue}{(5,6)}$ |
| **6** | $(6,1)$ | $(6,2)$ | $(6,3)$ | $(6,4)$ | $\color{blue}{(6,5)}$ | $(6,6)$ |

$$
P(S_9 \mid D_5) = \frac{|S_9 \cap D_5|}{|D_5|} = \frac{|\{(4,5), (5,4)\}|}{|D_5|} = \frac{2}{11}
$$

### Independence

**Independence:** If for two events $A, B$ holds

$$
P(A \cap B) = P(A)\,P(B)
$$

then we say *A and B are independent*.[^1]

If $A$ and $B$ are independent (and $P(B) > 0$) then

$$
P(A \mid B) \overset{\text{(cond)}}{=} \frac{P(A \cap B)}{P(B)} \overset{\text{(ind)}}{=} \frac{P(A)\,P(B)}{P(B)} = P(A)
$$

The *reverse conclusion is also true*: if $P(A \mid B) = P(A)$ (and $P(B) > 0$) then $A \perp\!\!\!\perp B$.

[^1]: often written as $A \perp\!\!\!\perp B$ or $A \perp B$

---

*more than just two*

Three events $A, B, C$ we call *independent* if they are *pair-wise independent*

$$
P(A \cap B) = P(A)P(B), \quad P(A \cap C) = P(A)P(C), \quad P(B \cap C) = P(B)P(C)
$$

*and*

$$
P(A \cap B \cap C) = P(A)P(B)P(C)
$$

*Example: Some coins again*

Throwing a *fair coin three times*, we get

$$
\Omega = \{HHH, HHT, HTH, HTT, THH, THT, TTH, TTT\}
$$

Let $A_i$ *be the event that the $i$'th toss is heads*, for example

$$
A_1 = \{\boldsymbol{H}HH, \boldsymbol{H}HT, \boldsymbol{H}TH, \boldsymbol{H}TT\}, \text{ with } P(A_1) = \tfrac{1}{2}
$$

then

$$
P(A_i \cap A_j) = \frac{1}{4} = P(A_i)P(A_j), \qquad i, j \in \{1, 2, 3\} \text{ such that } i \neq j
$$

and

$$
P(A_1 \cap A_2 \cap A_3) = P(\{HHH\}) = \frac{1}{8} = P(A_1)P(A_2)P(A_3)
$$

meaning that *$A_1, A_2$ and $A_3$ are independent*.

---

*Example: Some coins again*

Throwing a *fair coin three times*, we get

$$
\Omega = \{HHH, HHT, HTH, HTT, THH, THT, TTH, TTT\}
$$

Now let $B_i$ be the event that the $i$'th toss is tails, for example

$$
B_2 = \{H\boldsymbol{T}H, H\boldsymbol{T}T, T\boldsymbol{T}H, T\boldsymbol{T}T\}, \text{ with } P(B_2) = \tfrac{1}{2}
$$

and $C_i$ the event that all but the $i$'th throw are identical, for example

$$
C_3 = \{\boldsymbol{HH}H, \boldsymbol{HH}T, \boldsymbol{TT}H, \boldsymbol{TT}T\}, \text{ with } P(C_3) = \tfrac{1}{2}
$$

then $A_1, B_2$ and $C_3$ are "pair-wise independent" but *not independent*, because

$$
\begin{aligned}
P(A_1 \cap B_2) &= P(\{HTH, HTT\}) = \tfrac{1}{4} = P(A_1)P(B_2) \\
P(A_1 \cap C_3) &= P(\{HHH, HHT\}) = \tfrac{1}{4} = P(A_1)P(C_3) \\
P(B_2 \cap C_3) &= P(\{TTH, TTT\}) = \tfrac{1}{4} = P(B_2)P(C_3) \\
P(A_1 \cap B_2 \cap C_3) &= P(\emptyset) = 0 \;\color{red}{\neq}\; \tfrac{1}{8} = P(A_1)P(B_2)P(C_3)
\end{aligned}
$$

---

### The Law of Total Probability

*Putting pieces together*

If *only the conditional probabilities and the probabilities of the conditional event are known*, the *total probability* of $A$ results from

$$
P(A) = P(A \mid B)P(B) + P(A \mid B^c)P(B^c).
$$

Given a *partition of the sample space* $\Omega$ that is a sequence $B_1, B_2, B_3, \ldots$ of pair-wise disjoint events $B_i \cap B_j = \emptyset$ for all $i \neq j$ and $\bigcup_{i=1}^{\infty} B_i = \Omega$, then

$$
P(A) = \sum_{i=1}^{\infty} P(A \cap B_i) = \sum_{i=1}^{\infty} P(A \mid B_i)P(B_i)
$$

![[Pasted image 20261029125511.png]]


---

### Bayes Theorem

*Reversing the Condition*

Rewriting the definition of *conditional probability* for $P(A) > 0$ and $P(B) > 0$ gives the *Multiplication theorems*

$$
\begin{aligned}
P(A \cap B) &= P(A \mid B)P(B) \\
P(A \cap B) &= P(B \mid A)P(A)
\end{aligned}
$$

which leads through equating both to

**Bayes Theorem**

$$
P(A \mid B) = \frac{P(B \mid A)P(A)}{P(B)}
$$

This is very powerful and allows to "turn around" the conditioning.

An entire branch of statistics called <u>Bayes Statistics</u> is (basically) built on this formula (and the Bayesian interpretation of it).

---


*Updating Beliefs*

The *Bayes Theorem* describes the probability of an event based on *prior knowledge (before observation)* and allows to update the prior knowledge after observation to the *posterior (after observation)*.

$$
{\color{green}P(A \mid B)} = \frac{P(B \mid A)\,{\color{blue}P(A)}}{P(B)}
$$

Combining the Law of Total Probability given a partition $H_1, H_2, \ldots$ of $\Omega$ with Bayes Theorem, we get the alternative form

$$
P(H_i \mid B) = \frac{P(B \mid H_i)P(H_i)}{P(B)} = \frac{P(B \mid H_i)P(H_i)}{\sum_{j=1}^{\infty} P(B \mid H_j)P(H_j)}
$$

where the events $H_i$ often referred to as *Hypothesis*. We call $P(H_i)$ *the prior* probability and $P(H_i \mid B)$ *the posterior* probability.

#### Example
![[Pasted image 20261029125439.png]]

![[Pasted image 20261029125448.png]]

---


## Discrete Distributions

A random variable $X$ is *discrete* if it takes a finite or countable set of values. Its *probability mass function* (p.m.f.) gives the probability of each value $x$ that $X$ may take

$$
f_X(x) = P(X = x).
$$

and is zero otherwise. The p.m.f. determines the probabilities of events described in terms of $X$ as

$$
P(X \in A) = \sum_{x \in A} f_X(x),
$$

where the sum is over all possible values $x$ in $A$. Values in $A$ that $X$ cannot take have probability zero and do not contribute.

**Example** (Sum of two dice). The outcomes are ordered pairs of die results, so

$$
\Omega = \{(⚀,⚀), (⚀,⚁), \ldots, (⚅,⚄), (⚅,⚅)\}.
$$

There are 36 equally likely outcomes. Define $X$ to be the sum of the two results:

$$
X : \Omega \to \mathbb{R}, \qquad X((a,b)) = a + b.
$$

For example, $X((⚀,⚃)) = 5$. Although $\Omega$ has 36 outcomes, $X$ takes only the values $2, 3, \ldots, 12$.

The event that the sum is at most 4 is

$$
[X \leq 4] = \{(⚀,⚀), (⚀,⚁), (⚀,⚂), (⚁,⚀), (⚁,⚁), (⚂,⚀)\}.
$$

Therefore,

$$
P(X \leq 4) = \frac{6}{36} = \frac{1}{6}.
$$

The p.m.f. of $X$ can be given by a table or by the formula

$$
f_X(x) = P(X = x) = \frac{\min(x - 1,\, 13 - x)}{36}, \qquad x \in \{2, 3, \ldots, 12\}.
$$

For instance,

$$
P(X \leq 4) = \sum_{x=2}^{4} f_X(x) = \frac{1}{36} + \frac{2}{36} + \frac{3}{36} = \frac{1}{6}.
$$

Once the p.m.f. is known, probabilities for $X$ can be calculated without the underlying probability space.

---

## Continuous Distributions

A random variable $X$ is *continuous* if its probabilities can be described by a *probability density function* (p.d.f. or *density*) $f_X$. The density is nonnegative, and its total area is 1:

$$
f_X(x) \geq 0, \qquad \int_{-\infty}^{\infty} f_X(x)\,dx = 1.
$$

For a random variable with density $f_X$, the probability of $X$ being in an interval $[a, b]$ is

$$
P(a \leq X \leq b) = \int_a^b f_X(x)\,dx.
$$

A consequence of the formulation as an integral is that endpoints inclusion do not change the probability:

$$
P(a \leq X \leq b) = P(a \leq X < b) = P(a < X \leq b) = P(a < X < b).
$$

**Example** (Waiting for the bus). Suppose a bus arrives every 10 minutes, and your arrival time is uniform between two consecutive bus arrivals. Let $X$ be your waiting time, in minutes. Under this simplified model, $X$ is uniformly distributed between 0 and 10, with density

$$
f_X(x) =
\begin{cases}
\frac{1}{10}, & 0 \leq x \leq 10, \\
0, & \text{otherwise.}
\end{cases}
$$

The probability of waiting between 2 and 5 minutes is

$$
P(2 \leq X \leq 5) = \int_2^5 \frac{1}{10}\,dx = \frac{3}{10},
$$

while the probability of waiting less than 5 minutes is

$$
P(X \leq 5) = \int_{-\infty}^{5} f_X(x)\,dx = \int_0^5 \frac{1}{10}\,dx = \frac{1}{2}.
$$

> An interesting consequence for continuous random variables is that any "infinitely precise" value has probability zero. What is the probability that you wait exactly $\pi = 3.1415\ldots$ minutes? We can express this as the limit of a $\pm\varepsilon$ interval around exactly $\pi$ minutes with $\varepsilon$ going to zero, that is
>
> $$
> P(X = \pi) = \lim_{\varepsilon \to 0} P(X \in [\pi - \varepsilon, \pi + \varepsilon]) = \lim_{\varepsilon \to 0} \int_{\pi - \varepsilon}^{\pi + \varepsilon} \frac{1}{10}\,dx = \lim_{\varepsilon \to 0} \frac{\varepsilon}{5} = 0.
> $$


---


# Links
- [Probability theory](https://en.wikipedia.org/wiki/Probability_theory?useskin=vector)
- [Conditional Probability](https://en.wikipedia.org/wiki/Conditional_probability?useskin=vector)
-  [Law of total probablity](https://en.wikipedia.org/wiki/Law_of_total_probability?useskin=vector)
- [Bedingte Wahrscheinlichkeit](https://de.wikipedia.org/wiki/Bedingte_Wahrscheinlichkeit?useskin=vector)
