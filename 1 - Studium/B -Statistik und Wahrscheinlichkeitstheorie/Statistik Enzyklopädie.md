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



Discrete & Continuous Distributions * **Relationship between Cumulative Distribution Function (c.d.f.) & Probability Density Function (p.d.f.):**  Cumulative Distribution Function: $F_X(x) = P(X \le x)$ 
Density Function as Derivative of c.d.f.: $$f_X(x) = \frac{d}{dx} F_X(x)$$ * **Discrete Distributions:** Described by the Probability Mass Function (p.m.f.) $f_X(x) = P(X = x)$. Probabilities are obtained via summation. * **Continuous Distributions:** Described by a Probability Density Function (p.d.f.) $f_X(x) \ge 0$ where total area $\int_{-\infty}^{\infty} f_X(x) \, dx = 1$. $$P(a \le X \le b) = \int_a^b f_X(x) \, dx$$


 Standard Normal Distribution $\mathcal{N}(0, 1)$ * **Density Function (p.d.f.):** $$f_X(x) = \frac{1}{\sqrt{2\pi}} \exp\left(-\frac{x^2}{2}\right)$$ * **Gaussian Integral Identity:** $\int_{-\infty}^{\infty} e^{-x^2/2} \, dx = \sqrt{2\pi}$ ### Gamma Distribution $\Gamma(\alpha, \beta)$ * **Definition via Gamma Function:** $$\Gamma(p) = \int_0^\infty t^{p-1} e^{-t} \, dt \quad \left(\text{with } \Gamma\left(\frac{3}{2}\right) = \frac{\sqrt{\pi}}{2}\right)$$ Frequently used to model waiting times and sums of exponentially distributed variables. 
 
 Chi-Squared Distribution $\chi^2(k)$ * A special case of the Gamma distribution. It describes the distribution of the sum of $k$ squared independent standard normal random variables.
 
  Absolute Value of a Normal Variable ($Y = |X|$ / Folded Normal Distribution) * Due to the symmetry of the normal distribution, density doubles for non-negative values: $$f_{|X|}(x) = \begin{cases} 2 f_X(x) = \sqrt{\frac{2}{\pi}} \, e^{-\frac{x^2}{2}}, & \text{for } x \ge 0 \\ 0, & \text{for } x < 0 \end{cases}$$
Extreme Values: Maximum of Random Variables ($Y = \max(X_1, X_2)$) * For independent and identically distributed ($i.i.d.$) random variables, the c.d.f. of the maximum is: $$F_Y(y) = P(\max(X_1, X_2) \le y) = P(X_1 \le y \land X_2 \le y) = P(X_1 \le y) \cdot P(X_2 \le y) = (F_X(y))^2$$

<br>

---
(AI GENERATED SOURCED FROM WIKIPEDIA)
## Cumulative Distribution Function (CDF) / Verteilungsfunktion

The **cumulative distribution function (CDF)** / _Verteilungsfunktion_ of a real-valued random variable $X$ is the probability that $X$ takes a value _less than or equal to_ $x$:

$$ F_X(x) = P(X \leq x), \qquad x \in \mathbb{R} $$

It works for _every_ random variable, discrete or continuous. That is its big advantage over the p.m.f. / p.d.f.

> [!note] Convention The "$\leq$" is a convention (some literature uses "$<$"). For discrete distributions the difference matters, e.g. when using tables of the binomial or Poisson distribution. Notation: capital $F$ for the CDF, lower-case $f$ for the p.m.f. / p.d.f. The normal distribution has its own symbols: $\Phi$ (CDF) and $\varphi$ (density).

### Properties / Eigenschaften

Every CDF is

1. **non-decreasing** / _monoton wachsend_: $x \leq y \Rightarrow F_X(x) \leq F_X(y)$
2. **right-continuous** / _rechtsseitig stetig_
3. has the limits $\displaystyle \lim_{x \to -\infty} F_X(x) = 0$ and $\displaystyle \lim_{x \to \infty} F_X(x) = 1$

Conversely, every function with these three properties is the CDF of some random variable.

Probabilities of intervals follow directly:

$$ P(a < X \leq b) = F_X(b) - F_X(a) $$

The size of a jump equals the point probability: $P(X = x) = F_X(x) - \lim_{t \uparrow x} F_X(t)$. For continuous $X$ there are no jumps, therefore $P(X = x) = 0$ (see the $\pi$-minutes example above).

### Discrete vs. Continuous

||**Discrete** / _diskret_|**Continuous** / _stetig_|
|---|---|---|
|Describes by|p.m.f. / _Wahrscheinlichkeitsfunktion_ $f_X(x) = P(X=x)$|p.d.f. / _Dichtefunktion_ $f_X(x) \geq 0$|
|CDF from it|**sum** $\displaystyle F_X(x) = \sum_{x_i \leq x} f_X(x_i)$|**integral** $\displaystyle F_X(x) = \int_{-\infty}^{x} f_X(t),dt$|
|Shape of the CDF|step function / _Treppenfunktion_|continuous curve, often S-shaped|
|Back to the density|$f_X(x_i) = F_X(x_i) - F_X(x_{i-1})$|$\displaystyle f_X(x) = \frac{d}{dx}F_X(x)$ (where the derivative exists)|

The relation _density = derivative of the CDF_ is the **Fundamental Theorem of Calculus** / _Hauptsatz der Differential- und Integralrechnung_.

### Examples

**Sum of two dice (discrete).** The p.m.f. $f_X(x) = \frac{\min(x-1,,13-x)}{36}$ gives the CDF by accumulating:

|$x$|2|3|4|5|6|7|8|9|10|11|12|
|:--|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|$36 \cdot F_X(x)$|1|3|6|10|15|21|26|30|33|35|36|

For example $P(X \leq 4) = F_X(4) = \frac{6}{36} = \frac{1}{6}$, as computed before. Between the integers $F_X$ is constant, e.g. $F_X(4.7) = F_X(4)$.

**Waiting for the bus (continuous uniform).** For $X \sim \mathcal{U}(0, 10)$:

$$ F_X(x) = \begin{cases} 0, & x < 0, \ \frac{x}{10}, & 0 \leq x \leq 10, \ 1, & x > 10. \end{cases} $$

Now the probability of waiting between 2 and 5 minutes is just a difference, no integral needed:

$$ P(2 \leq X \leq 5) = F_X(5) - F_X(2) = \frac{1}{2} - \frac{1}{5} = \frac{3}{10} $$

**Exponential distribution** / _Exponentialverteilung_ with rate $\lambda > 0$:

$$ f_X(x) = \lambda e^{-\lambda x}, \qquad F_X(x) = 1 - e^{-\lambda x} \qquad (x \geq 0) $$

### Complementary CDF / Survival Function

_How likely is it that $X$ is above a level?_

$$ \bar{F}_X(x) = P(X > x) = 1 - F_X(x) $$

This is called the **complementary CDF (ccdf)** / _Komplementäre Verteilungsfunktion_, the **tail distribution**, or in survival analysis the **survival function** / _Überlebensfunktion_ (in engineering: _reliability function_ / _Zuverlässigkeitsfunktion_). It is also what a **one-sided p-value** is: the probability of a test statistic at least as extreme as the observed one, $p = 1 - F_T(t_{\text{obs}})$.

### Quantile Function / Quantilfunktion (Inverse CDF)

If $F$ is strictly increasing and continuous, then for $p \in (0,1)$ there is exactly one $x_p$ with $F(x_p) = p$. The map $p \mapsto x_p$ is the **quantile function** / _Quantilfunktion_ (inverse distribution function):

$$ F^{-1}(p) = x_p $$

If $F$ has jumps or flat parts, the **generalized inverse** is used: $F^{-1}(p) = \inf{x : F(x) \geq p}$.

- $F^{-1}(0.5)$ is the **median** / _Median_
- $F^{-1}(0.95)$ is the **95th percentile** / _95%-Quantil_
- $F^{-1}(0.25)$, $F^{-1}(0.5)$, $F^{-1}(0.75)$ are the **quartiles** / _Quartile_ (see the section on expectation and variance)

**Inverse transform sampling / Inversionsmethode:** if $U \sim \mathcal{U}(0,1)$, then $F^{-1}(U)$ has the CDF $F$. So uniform random numbers can be turned into _any_ distribution (a way to generate **pseudo-random numbers** / _Pseudozufallszahlen_). For the exponential distribution:

$$ X = F^{-1}(U) = -\frac{\ln(1-U)}{\lambda} $$

The full method with proof, discrete examples and limits follows in its own section below.

### Empirical CDF / Empirische Verteilungsfunktion

From a sample $x_1, \ldots, x_n$ the CDF can be estimated by the fraction of observations $\leq x$:

$$ \hat{F}_n(x) = \frac{1}{n} \sum_{i=1}^{n} \mathbf{1}_{{x_i \leq x}} $$

It is a step function that converges to the true $F$ as $n \to \infty$. The **Kolmogorov–Smirnov test** is based on the largest distance between two such CDFs (or between $\hat{F}_n$ and a theoretical $F$).

### Joint CDF / Gemeinsame Verteilungsfunktion

For two random variables:

$$ F_{X,Y}(x,y) = P(X \leq x,; Y \leq y) $$

$X$ and $Y$ are independent iff $F_{X,Y}(x,y) = F_X(x),F_Y(y)$ for all $x, y$. This connects back to the section on independence.

---

## Inverse Transform Sampling / Inversionsmethode

Also called _inversion sampling_, _inverse probability integral transform_ or **Smirnov transform** / _Smirnov-Transformation_. It is a basic method for **pseudo-random number sampling** / _Erzeugung von Pseudozufallszahlen_: from uniform random numbers on $(0,1)$ it produces random numbers of _any_ distribution whose CDF is known. It is used to simulate systems that are hard to analyze with formulas, e.g. in **queueing theory** / _Warteschlangentheorie_.

**Intuition:** pick a random _proportion_ $u$ of the area under the density curve and return the number $x$ such that exactly this proportion of the area lies to the left of $x$. The far tails contain very little area, so they are rarely chosen.

### Quantile function (generalized inverse) / Quantilfunktion (verallgemeinerte Inverse)

For a CDF $F$ and a probability $p \in (0,1)$ the **$p$-quantile** / _$p$-Quantil_ is

$$ F^{-1}(p) = \inf{x \in \mathbb{R} : F(x) \geq p} $$

If $F$ is strictly increasing and continuous, this is the ordinary **inverse function** / _Umkehrfunktion_. The infimum is needed for CDFs that are _not injective_, e.g. the step function of a discrete random variable.

### Simulation Lemma / Simulationslemma

> [!abstract] Statement Let $F$ be a CDF and $U \sim \mathcal{U}(0,1)$. Then $$ X = F^{-1}(U) \quad\text{has the CDF } F. $$

_Proof._ Because $F$ is right-continuous, the following equivalence holds:

$$ F^{-1}(u) \leq x \iff u \leq F(x) $$

Therefore

$$ P(X \leq x) = P\bigl(F^{-1}(U) \leq x\bigr) = P\bigl(U \leq F(x)\bigr) = F(x), $$

since $P(U \leq t) = t$ for $t \in [0,1]$. $\square$

_Intuition for strictly increasing $F$:_ we look for a strictly monotone $g$ with $P(g(U) \leq x) = F(x)$. Now $P(g(U) \leq x) = P(U \leq g^{-1}(x)) = g^{-1}(x)$, so $g^{-1} = F$ and $g = F^{-1}$.

### Algorithm / Ablauf

1. Draw $u$ from the **standard uniform distribution** / _Standard-Gleichverteilung_ $\mathcal{U}(0,1)$.
2. Find the generalized inverse $F^{-1}$ of the desired CDF.
3. Compute $x = F^{-1}(u)$. This $x$ is a realization of a random variable with CDF $F$.

### The reverse direction: Probability Integral Transform / Wahrscheinlichkeitsintegraltransformation

For a _continuous_ random variable $X$ with CDF $F$, the transformed variable is uniform:

$$ F(X) \sim \mathcal{U}(0,1), \qquad\text{because}\quad P(F(X) \leq u) = P\bigl(X \leq F^{-1}(u)\bigr) = F\bigl(F^{-1}(u)\bigr) = u $$

So inversion sampling is exactly the inverse of this transform.

### Continuous examples / Stetige Beispiele

**Exponential distribution** with $F(x) = 1 - e^{-\lambda x}$. Solving $u = F(x)$ gives

$$ x = F^{-1}(u) = -\frac{\ln(1-u)}{\lambda} $$

Since $1 - U$ is also uniform on $(0,1)$, it is enough to compute

$$ x = -\frac{\ln u}{\lambda} $$

(this is also the reason why $-2\ln U \sim \chi^2(2)$, see the chi-squared section).

**Weibull distribution** / _Weibull-Verteilung_ with $F(x) = 1 - e^{-(x/\lambda)^k}$ for $x \geq 0$ ($\lambda$ scale, $k$ shape):

$$ x = \lambda,(-\ln u)^{1/k} $$

More examples (each with $u \sim \mathcal{U}(0,1)$):

|Distribution / _Verteilung_|CDF $F(x)$|Sample $x = F^{-1}(u)$|
|---|---|---|
|Uniform / _Gleichverteilung_ on $[a,b]$|$\dfrac{x-a}{b-a}$|$a + (b-a),u$|
|Exponential / _Exponentialverteilung_|$1 - e^{-\lambda x}$|$-\dfrac{\ln u}{\lambda}$|
|Weibull|$1 - e^{-(x/\lambda)^k}$|$\lambda(-\ln u)^{1/k}$|
|Cauchy|$\dfrac12 + \dfrac{\arctan x}{\pi}$|$\tan!\bigl(\pi(u - \tfrac12)\bigr)$|

**Simulated waiting times (exponential, $\lambda = 2$ requests per time unit).** The gaps between requests to a server are exponentially distributed with mean $\frac{1}{\lambda} = 0.5$. Summing up the gaps gives the arrival times. While the _gaps_ are exponential, the _number of requests per time interval_ follows a **Poisson distribution** / _Poisson-Verteilung_.

**Random walk / Irrfahrt:** with $U \sim \mathcal{U}(0,1)$ the shifted number $U - 0.5$ is uniform on $(-0.5, 0.5)$ and can be used as a step length that goes forwards or backwards depending on its sign.

### Discrete examples / Diskrete Beispiele

For a discrete distribution the CDF is a **step function** / _Treppenfunktion_ and is just a finite sum of point probabilities. Inversion means: _return the smallest $x$ with $F(x) \geq u$._

**Coffee pots / Kaffeekannen.** A pot is OK (value 1) with probability 0.75, defective (value 2) with probability 0.25. So

$$ F(x) = 0 ;(x<1), \qquad F(x) = 0.75 ;(1 \leq x < 2), \qquad F(x) = 1 ;(x \geq 2) $$

Draw $u$: if $u \leq 0.75$ the pot gets the value 1, otherwise 2. For $u = 0.39 \to 1$, $u = 0.93 \to 2$. In the long run this gives 75 % ones and 25 % twos.

**Bank counter / Bankschalter (Poisson, $\lambda = 1.2$ customers per minute).**

|$x$ (customers per minute)|0|1|2|3|4|5|
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
|$f(x) = P(X = x)$|0.301|0.361|0.217|0.087|0.026|0.006|
|$F(x) = P(X \leq x)$|0.301|0.663|0.879|0.966|0.992|0.998|

Lookup in the $F$ row: $u = 0.63 \to x = 1$ (since $0.301 < 0.63 \leq 0.663$), $u = 0.93 \to x = 3$, $u = 0.04 \to x = 0$.

_Why simulate at all?_ If on average 1.2 customers arrive and 1.5 can be served per minute, one might expect no queue. The simulation shows that queues of several people still appear: serving capacity that is unused in quiet minutes cannot be saved for later (there are no negative customer numbers).

### Limits and alternatives / Grenzen und Alternativen

- The method needs the **quantile function**. For many distributions it is **not available in closed form** or too expensive to compute, because integrating the density analytically is impossible for most densities.
- **Normal distribution:** $\Phi^{-1}(u) = \sqrt{2},\operatorname{erf}^{-1}(2u-1)$ has no elementary expression. Typical values:

|$u$|0.5|0.975|0.995|0.999999|
|:--|:-:|:-:|:-:|:-:|
|$\Phi^{-1}(u)$|0|1.95996|2.5758|4.75342|

Alternatives are the **Box–Muller transform**, the **ziggurat algorithm**, or **rejection sampling** / _Verwerfungsmethode_. However, the quantile function of the normal distribution can be approximated very precisely with polynomials, and the statistics software R nowadays uses inversion as its default for normal random numbers.

- **Multivariate normal:** independent standard normal samples $z$ are correlated by multiplying with the **Cholesky factor** / _Cholesky-Zerlegung_ $L$ of the covariance matrix $\Sigma = LL^\top$: $x = \mu + Lz$.

### Extension: truncated distributions / Gestutzte Verteilungen

To sample $X$ conditioned on $a < X \leq b$ without rejecting anything, draw $u$ uniformly from $(F(a), F(b))$ instead of $(0,1)$ and still use $x = F^{-1}(u)$.

_Software:_ UNU.RAN (C), Runuran (R), `scipy.stats.sampling` (Python).

---

## Expectation, Variance & Moments / Erwartungswert, Varianz & Momente

Quick reference (Kurzfassung) for the numbers that describe a distribution. Short reminder of what the p.m.f. / p.d.f. must satisfy:

- **Discrete** / _diskret_, p.m.f. / _Wahrscheinlichkeitsfunktion_ $p(a) = P(X = a)$: always $0 \leq p(a) \leq 1$ and $\sum_a p(a) = 1$.
- **Continuous** / _stetig_, p.d.f. / _Dichtefunktion_ $f(x)$: $f(x) \geq 0$ and $\int_{-\infty}^{\infty} f(x),dx = 1$. Probabilities need an integral: $P(c \leq X \leq d) = \int_c^d f(x),dx$.

### Expectation / Erwartungswert

Often abbreviated $\mu$. It is the **weighted mean** / _gewichteter Mittelwert_ of the possible values of $X$ and a measure of the **central tendency** / _zentrale Tendenz_.

$$ E(X) = \sum_i x_i, p(x_i) \quad\text{(discrete)}, \qquad E(X) = \int_{-\infty}^{\infty} x, f(x),dx \quad\text{(continuous)} $$

It is assumed that the sum / integral converges **absolutely** / _absolut konvergent_.

**Moment of order $k$ / Moment der Ordnung $k$:** $E(X^k)$.

**Rules:** $E(aX + b) = a,E(X) + b$, and $E(X + Y) = E(X) + E(Y)$ (always, even without independence).

**Via the CDF:** for $X \geq 0$ the expectation is the area above the CDF,

$$ E(X) = \int_0^\infty \bigl(1 - F_X(x)\bigr),dx = \int_0^\infty P(X > x),dx $$

### Variance & Standard Deviation / Varianz & Standardabweichung

$$ \sigma^2 = \operatorname{Var}(X) = E\bigl[(X - E(X))^2\bigr] = E(X^2) - \bigl(E(X)\bigr)^2, \qquad \sigma = \sqrt{\operatorname{Var}(X)} $$

**Rules:** $\operatorname{Var}(aX + b) = a^2 \operatorname{Var}(X)$. For _independent_ $X, Y$: $\operatorname{Var}(X + Y) = \operatorname{Var}(X) + \operatorname{Var}(Y)$.

**Examples:**

|Random variable|$E(X)$|$\operatorname{Var}(X)$|
|---|---|---|
|One fair die|$3.5$|$\frac{35}{12}$|
|Sum of two dice (independent)|$7$|$\frac{35}{6}$|
|Bus waiting time $X \sim \mathcal{U}(0,10)$|$5$|$\frac{100}{12} = \frac{25}{3}$|

### Quartiles / Quartile

Special quantiles of the quantile function:

- $x_{0.25}$ is the **lower quartile** / _unteres Quartil_
- $x_{0.5}$ is the **median** / _Median_
- $x_{0.75}$ is the **upper quartile** / _oberes Quartil_

---

## Common Distributions & R Functions / Wichtige Verteilungen & R-Funktionen

### Discrete distributions / Diskrete Verteilungen

|Distribution / _Verteilung_|Meaning|p.m.f. $p(k)$|$E(X)$|$\operatorname{Var}(X)$|
|---|---|---|---|---|
|**Bernoulli** $X \sim \operatorname{ber}(p)$|only two outcomes: success / failure|$p(1) = p,; p(0) = 1-p$|$p$|$p(1-p)$|
|**Binomial** / _Binomialverteilung_ $X \sim B(n,p)$|number of successes in $n$ independent Bernoulli trials|$\binom{n}{k}p^k(1-p)^{n-k}$|$np$|$np(1-p)$|
|**Geometric** / _Geometrische Verteilung_|number of trials until the first success|$(1-p)^{k-1}p,; k = 1, 2, \ldots$|$\frac{1}{p}$|$\frac{1-p}{p^2}$|
|**Poisson** $X \sim \operatorname{Poi}(\lambda)$|number of rare events in an interval|$e^{-\lambda}\dfrac{\lambda^k}{k!},; k = 0, 1, \ldots$|$\lambda$|$\lambda$|

> [!warning] Geometric distribution: two conventions Counting the _trials_ up to and including the first success gives $k = 1, 2, \ldots$ with $E(X) = \frac1p$ (formula above). **R counts the failures before the first success** ($k = 0, 1, \ldots$, $p(k) = (1-p)^k p$, $E = \frac{1-p}{p}$). Always check which convention is meant.

The binomial coefficient $\binom{n}{k}$ is the one from the combinatorics section at the top: a binomial variable is the sum of $n$ independent Bernoulli variables, and $\binom nk$ counts the ways to place the $k$ successes.

### Continuous distributions / Stetige Verteilungen

|Distribution / _Verteilung_|Density $f(x)$|$E(X)$|$\operatorname{Var}(X)$|
|---|---|---|---|
|**Uniform** / _Gleichverteilung_ $\mathcal{U}(a,b)$|$\dfrac{1}{b-a}$ on $[a,b]$|$\dfrac{a+b}{2}$|$\dfrac{(b-a)^2}{12}$|
|**Exponential** / _Exponentialverteilung_ $\operatorname{Exp}(\lambda)$|$\lambda e^{-\lambda x}$, $x \geq 0$|$\dfrac{1}{\lambda}$|$\dfrac{1}{\lambda^2}$|
|**Normal** (Gauß) $\mathcal{N}(\mu, \sigma^2)$|$\dfrac{1}{\sigma\sqrt{2\pi}}e^{-(x-\mu)^2/(2\sigma^2)}$|$\mu$|$\sigma^2$|

Gamma, chi-squared and $t$ follow in the sections below.

### R functions / R-Funktionen

R names every distribution with a **prefix** + **short name**. The four prefixes correspond directly to the concepts of these notes:

|Prefix|Meaning (English / _Deutsch_)|In the notes|
|:-:|---|---|
|`d`|density / p.m.f. / _Dichte_|$f_X(x)$ or $p(x)$|
|`p`|distribution function / _Verteilung_|CDF $F_X(x)$, for the normal: $\Phi$|
|`q`|quantile function / _Quantile_|$F^{-1}(p)$, for the normal: $\Phi^{-1}$|
|`r`|random deviates / _Zufallszahlen_|sampling, see inversion method|

|Distribution|Density|CDF|Quantile|Random|
|---|---|---|---|---|
|Binomial|`dbinom()`|`pbinom()`|`qbinom()`|`rbinom()`|
|Geometric|`dgeom()`|`pgeom()`|`qgeom()`|`rgeom()`|
|Poisson|`dpois()`|`ppois()`|`qpois()`|`rpois()`|
|Uniform|`dunif()`|`punif()`|`qunif()`|`runif()`|
|Exponential|`dexp()`|`pexp()`|`qexp()`|`rexp()`|
|Normal|`dnorm()`|`pnorm()`|`qnorm()`|`rnorm()`|
|_Gamma (addition)_|`dgamma()`|`pgamma()`|`qgamma()`|`rgamma()`|
|_Chi-squared (addition)_|`dchisq()`|`pchisq()`|`qchisq()`|`rchisq()`|
|_t (addition)_|`dt()`|`pt()`|`qt()`|`rt()`|

Examples: `pnorm(1.96)` $\approx 0.975 = \Phi(1.96)$ and `qnorm(0.975)` $\approx 1.96 = \Phi^{-1}(0.975)$. The probability $P(a < X \leq b)$ is `pnorm(b) - pnorm(a)`, exactly the rule $F(b) - F(a)$.

---

## Normal Distribution / Normalverteilung

A random variable $X \sim \mathcal{N}(\mu, \sigma^2)$ with **mean (expectation)** / _Erwartungswert_ $\mu$ and **standard deviation** / _Standardabweichung_ $\sigma$ has the density

$$ f_X(x) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left( -\frac{(x-\mu)^2}{2\sigma^2} \right) $$

### Standard Normal Distribution / Standardnormalverteilung $\mathcal{N}(0,1)$

$$ \varphi(x) = \frac{1}{\sqrt{2\pi}} \exp\left(-\frac{x^2}{2}\right) $$

Its CDF has its own letter, $\Phi$:

$$ \Phi(x) = P(Z \leq x) = \int_{-\infty}^{x} \varphi(t),dt $$

**Standardization / Standardisierung (z-transformation):** every normal distribution can be reduced to the standard one,

$$ Z = \frac{X - \mu}{\sigma} \sim \mathcal{N}(0,1), \qquad F_X(x) = \Phi!\left(\frac{x-\mu}{\sigma}\right) $$

Because the density is symmetric: $\Phi(-x) = 1 - \Phi(x)$.

### Why the density is normalized (Gaussian Integral / Gaußsches Integral)

$$ \int_{-\infty}^{\infty} e^{-x^2/2},dx = \sqrt{2\pi} $$

There is no elementary antiderivative of $e^{-x^2/2}$, but there is a classic trick (attributed to Poisson): square the integral and go to **polar coordinates** / _Polarkoordinaten_:

$$ I^2 = \int!!\int_{\mathbb{R}^2} e^{-(x^2+y^2)/2},dx,dy = \int_0^{2\pi}!\int_0^\infty r,e^{-r^2/2},dr,d\theta = 2\pi \cdot 1 = 2\pi $$

so $I = \sqrt{2\pi}$ and therefore $\int_{-\infty}^\infty \varphi(x),dx = 1$.

### Values worth remembering

|$x$|0|1|1.645|1.96|2|3|
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
|$\Phi(x)$|0.5|0.8413|0.95|0.975|0.9772|0.99865|

The **68–95–99.7 rule**: $P(|Z| \leq 1) \approx 0.6827$, $P(|Z| \leq 2) \approx 0.9545$, $P(|Z| \leq 3) \approx 0.9973$. Printed tables of $\Phi$ are called the **standard normal table / z-table** / _Tabelle der Standardnormalverteilung_.

---

## Error Integral & Error Function / Fehlerintegral & Fehlerfunktion

### Gaussian Error Integral / Gaußsches Fehlerintegral

In the German literature, the **Gaußsches Fehlerintegral** is simply the CDF of the standard normal distribution, i.e. $\Phi(x)$ from above:

$$ \Phi(x) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{x} e^{-t^2/2},dt $$

It gives the probability that a standard normal variable is $\leq x$. The probability of a value $\geq x$ follows with $1 - \Phi(x)$. Since the total area under the bell curve (**Gauß-Glocke**) is 1, $\Phi(\infty) = 1$.

> [!example] Noise on a transmission channel (Störrauschen) A channel works without errors as long as Gaussian noise $N \sim \mathcal{N}(0, \sigma^2)$ stays within $-5,\text{V} \ldots +5,\text{V}$. The probability of a transmission error is $$ P(\text{error}) = P(N \leq -5) + P(N \geq 5) = 2\left(1 - \Phi!\left(\tfrac{5}{\sigma}\right)\right) $$ For (an assumed) $\sigma = 2,\text{V}$: $2,(1 - \Phi(2.5)) \approx 2 \cdot 0.0062 = 0.0124$, so about 1.2 %.

### Error Function / Fehlerfunktion $\operatorname{erf}$

The **error function** (_Gaußsche Fehlerfunktion_, from "error function") is defined by

$$ \operatorname{erf}(x) = \frac{2}{\sqrt{\pi}} \int_0^x e^{-t^2},dt $$

and the **complementary error function** / _komplementäre Fehlerfunktion_:

$$ \operatorname{erfc}(x) = 1 - \operatorname{erf}(x) = \frac{2}{\sqrt{\pi}} \int_x^\infty e^{-t^2},dt $$

Properties:

- $\operatorname{erf}$ is an **odd function** / _ungerade Funktion_: $\operatorname{erf}(-x) = -\operatorname{erf}(x)$. It is the only odd antiderivative of $\frac{2}{\sqrt\pi}e^{-x^2}$.
- Limits: $\operatorname{erf}(0) = 0$, $\operatorname{erf}(\infty) = 1$, $\operatorname{erf}(-\infty) = -1$. The value $1$ is exactly the Gaussian integral $\int_0^\infty e^{-t^2}dt = \frac{\sqrt\pi}{2}$.
- It is a **sigmoid function** / _Sigmoidfunktion_ (S-shaped).
- Not expressible by a closed formula of elementary functions, it must be computed **numerically** / _numerisch_, e.g. by the **power series** / _Reihenentwicklung_ for small $x$:

$$ \operatorname{erf}(x) = \frac{2}{\sqrt{\pi}} \sum_{n=0}^{\infty} \frac{(-1)^n,x^{2n+1}}{n!,(2n+1)} $$

(for large $x$ a **continued fraction** / _Kettenbruch_ is used instead).

|$x$|0.5|1.0|1.5|2.0|2.5|3.0|
|:--|:-:|:-:|:-:|:-:|:-:|:-:|
|$\operatorname{erf}(x)$|0.5205|0.8427|0.9661|0.9953|0.9996|0.99998|
|$\operatorname{erfc}(x)$|0.4795|0.1573|0.0339|0.0047|0.0004|0.00002|

### Connection: $\Phi$ and $\operatorname{erf}$

Substituting $t \to t/\sqrt{2}$ turns one into the other:

$$ \Phi(x) = \frac{1}{2}\left(1 + \operatorname{erf}!\left(\frac{x}{\sqrt{2}}\right)\right) = \frac{1}{2}\operatorname{erfc}!\left(-\frac{x}{\sqrt{2}}\right) \qquad\Longleftrightarrow\qquad \operatorname{erf}(x) = 2,\Phi(\sqrt{2},x) - 1 $$

**Important difference:** a CDF must take values in $[0,1]$. $\operatorname{erf}$ takes values in $(-1, 1)$, so _it is not itself a CDF_, only a rescaled version of $\Phi$.

For a general normal distribution with mean $\mu$ and standard deviation $\sigma$:

$$ F_X(x) = \frac{1}{2}\left(1 + \operatorname{erf}!\left(\frac{x-\mu}{\sigma\sqrt{2}}\right)\right) $$

**Measurement error / Messfehler:** if the deviations of a measurement series from the mean are $\mathcal{N}(0,\sigma^2)$, the probability that a single error lies in $[-a, a]$ (for $a > 0$) is

$$ P(-a \leq X \leq a) = \operatorname{erf}!\left(\frac{a}{\sigma\sqrt{2}}\right) $$

(check: $a = \sigma$ gives $\operatorname{erf}(1/\sqrt{2}) \approx 0.6827$, the "one sigma" probability).

**Uses:** statistics (normal distribution), solutions of the **heat equation** / _Wärmeleitungsgleichung_ with step-function boundary conditions, and generating normally distributed random numbers via the inverse transform method with $\Phi^{-1}(p) = \sqrt{2},\operatorname{erf}^{-1}(2p - 1)$.

---

## Gamma Function / Gammafunktion

The **Euler gamma function** / _Eulersche Gammafunktion_ (also _Eulersches Integral zweiter Gattung_) is defined for $p > 0$ (more generally $\operatorname{Re}(p) > 0$) by

$$ \Gamma(p) = \int_0^\infty t^{p-1} e^{-t},dt $$

It **extends the factorial** / _Fakultät_ to non-integer arguments, but shifted by 1:

$$ \Gamma(n) = (n-1)! \qquad \text{for } n \in \mathbb{N} $$

For example $\Gamma(5) = 4! = 24$.

**Functional equation / Funktionalgleichung:**

$$ \Gamma(p+1) = p,\Gamma(p), \qquad \Gamma(1) = 1 $$

Integration by parts proves it, and it is the exact analogue of $(n+1)! = (n+1)\cdot n!$.

**Domain / Definitionsbereich:** the gamma function can be continued to all complex numbers except $0, -1, -2, \ldots$ where it has **poles** / _Polstellen_. It has no zeros.

**A key value** (this is the one from the notes above):

$$ \Gamma!\left(\tfrac{1}{2}\right) = \sqrt{\pi}, \qquad \Gamma!\left(\tfrac{3}{2}\right) = \tfrac{1}{2}\Gamma!\left(\tfrac12\right) = \frac{\sqrt{\pi}}{2} $$

_Proof via the Gaussian integral:_ substitute $t = u^2$, $dt = 2u,du$:

$$ \Gamma!\left(\tfrac12\right) = \int_0^\infty t^{-1/2}e^{-t},dt = 2\int_0^\infty e^{-u^2},du = 2\cdot\frac{\sqrt{\pi}}{2} = \sqrt{\pi} $$

So the error integral, the Gaussian integral, and the gamma function are all closely linked.

**More facts:**

- **Reflection formula / Ergänzungssatz** (Euler): $\Gamma(z),\Gamma(1-z) = \dfrac{\pi}{\sin(\pi z)}$
- **Stirling's formula / Stirlingsche Formel** for large $x$: $\Gamma(x+1) \approx \sqrt{2\pi x},\left(\dfrac{x}{e}\right)^{x}$
- **Bohr–Mollerup theorem / Satz von Bohr-Mollerup:** on $(0,\infty)$ the gamma function is the _only_ function with $f(1) = 1$, $f(x+1) = x f(x)$ that is **logarithmically convex** / _logarithmisch konvex_. (The first two properties alone do not determine it uniquely.)
- **History:** Euler introduced it in 1729 (letters to Goldbach), Legendre introduced the symbol $\Gamma$ in 1809, Gauß used a shifted version $\Pi(n) = n!$.

### Incomplete Gamma Function / Unvollständige Gammafunktion

Cutting the integral off at a limit $x$ gives

$$ \gamma(s,x) = \int_0^x t^{s-1}e^{-t},dt \quad\text{(lower / untere)}, \qquad \Gamma(s,x) = \int_x^\infty t^{s-1}e^{-t},dt \quad\text{(upper / obere)} $$

with $\gamma(s,x) + \Gamma(s,x) = \Gamma(s)$. Dividing by $\Gamma(s)$ gives the **regularized** / _regularisierte_ versions

$$ P(s,x) = \frac{\gamma(s,x)}{\Gamma(s)}, \qquad Q(s,x) = \frac{\Gamma(s,x)}{\Gamma(s)} = 1 - P(s,x) $$

> [!warning] Notation The notation for the incomplete / regularized gamma function is not uniform in the literature, always check which limit (upper or lower) and which normalization is meant.

The regularized lower function $P(s,x)$ is exactly the CDF of the gamma distribution (see below). The connection to the error function: $\operatorname{erf}(x) = P!\left(\tfrac12, x^2\right)$.

---

## Gamma Distribution / Gammaverteilung $\Gamma(\alpha, \beta)$

A continuous distribution on the positive real numbers, a **generalization of the exponential distribution** / _Exponentialverteilung_ and of the **Erlang distribution** / _Erlang-Verteilung_ to non-integer parameters.

With **shape parameter** / _Formparameter_ $\alpha > 0$ and **rate parameter** / _Ratenparameter_ $\beta > 0$ (parametrization common in German literature):

$$ f_X(x) = \frac{\beta^\alpha}{\Gamma(\alpha)},x^{\alpha-1},e^{-\beta x}, \qquad x > 0 $$

The prefactor $\frac{\beta^\alpha}{\Gamma(\alpha)}$ is the **normalization** / _Normierung_. This is where the gamma function enters. The CDF is the regularized lower incomplete gamma function:

$$ F_X(x) = P(\alpha, \beta x) = \frac{\gamma(\alpha, \beta x)}{\Gamma(\alpha)} $$

|Quantity / _Kenngröße_|Value|
|---|---|
|Expectation / _Erwartungswert_|$\dfrac{\alpha}{\beta}$|
|Variance / _Varianz_|$\dfrac{\alpha}{\beta^2}$|
|Skewness / _Schiefe_|$\dfrac{2}{\sqrt{\alpha}}$|
|Mode / _Modus_ (for $\alpha \geq 1$)|$\dfrac{\alpha - 1}{\beta}$|
|Moment generating function / _momenterzeugende Funktion_|$\left(1 - \dfrac{t}{\beta}\right)^{-\alpha}$ for $t < \beta$|

> [!warning] Two parametrizations The English literature often uses **shape $k$ and scale $\theta$** with $\theta = 1/\beta$. Then $E[X] = k\theta$ and $\operatorname{Var}(X) = k\theta^2$. To avoid confusion, state mean and variance explicitly.

**Use / Anwendung:** waiting times, service and repair times in **queueing theory** / _Warteschlangentheorie_, small to medium claim sizes in **actuarial mathematics** / _Versicherungsmathematik_.

### Relations to other distributions

- $\alpha = 1$: **Exponential distribution** $\operatorname{Exp}(\beta)$, since $\Gamma(1) = 1$ and the density becomes $\beta e^{-\beta x}$.
- **Sum of exponentials:** the sum of $n$ independent $\operatorname{Exp}(\beta)$ variables is $\Gamma(n, \beta)$. This is the **Erlang distribution** (waiting time until the $n$-th event of a Poisson process).
- **Reproductive property / Reproduktivität:** for independent $X \sim \Gamma(\alpha_1, \beta)$, $Y \sim \Gamma(\alpha_2, \beta)$ (same $\beta$):

$$ X + Y \sim \Gamma(\alpha_1 + \alpha_2,, \beta) $$

So the gamma distribution forms a **convolution semigroup** / _Faltungshalbgruppe_ in $\alpha$.

- **Beta distribution / Betaverteilung:** $\dfrac{X}{X+Y} \sim \operatorname{Beta}(\alpha_1, \alpha_2)$.
- **Chi-squared distribution / Chi-Quadrat-Verteilung:** see next section.

---

## Chi-Squared Distribution / Chi-Quadrat-Verteilung $\chi^2(k)$

A continuous distribution on the **non-negative real numbers**. Usually the _central_ chi-squared distribution is meant (older name: _Helmert–Pearson-Verteilung_). It has exactly one parameter, the number of **degrees of freedom** / _Freiheitsgrade_ $k$. It was introduced by Helmert (1876), the name comes from Karl Pearson (1900).

### Definition

If $Z_1, \ldots, Z_k$ are **independent and standard normal** / _stochastisch unabhängig und standardnormalverteilt_, then

$$ \chi^2_k = Z_1^2 + Z_2^2 + \dots + Z_k^2 \sim \chi^2(k) $$

A sum of squares can't be negative, so the density is $0$ for $x \leq 0$. For $x > 0$:

$$ f_X(x) = \frac{x^{k/2 - 1},e^{-x/2}}{2^{k/2},\Gamma!\left(\frac{k}{2}\right)} $$

The gamma function $\Gamma$ appears in the normalization. Values $\Gamma(\frac{k}{2})$ follow recursively from $\Gamma(p+1) = p,\Gamma(p)$ with $\Gamma(1) = 1$ and $\Gamma(\frac12) = \sqrt\pi$.

**CDF / Verteilungsfunktion:** via the regularized lower incomplete gamma function $P(s,x)$ from above:

$$ F_X(x) = P!\left(\frac{k}{2}, \frac{x}{2}\right) = \frac{\gamma!\left(\frac{k}{2}, \frac{x}{2}\right)}{\Gamma!\left(\frac{k}{2}\right)} $$

Special cases (for $x \geq 0$):

$$ k = 1:\quad F_X(x) = \operatorname{erf}!\left(\sqrt{\tfrac{x}{2}}\right), \qquad\qquad k = 2:\quad F_X(x) = 1 - e^{-x/2} $$

For $k=1$ the **error function** / _Fehlerfunktion_ shows up again, which matches the folded normal distribution ($\chi^2_1 = X^2$, so $F(x) = P(|X| \leq \sqrt{x}) = \operatorname{erf}(\sqrt{x/2})$).

### Properties / Eigenschaften

|Quantity / _Kenngröße_|Value|
|---|---|
|Expectation / _Erwartungswert_|$k$|
|Variance / _Varianz_|$2k$|
|Mode / _Modus_|$\max(k-2,,0)$ (for $k = 1, 2$ the density is decreasing, mode $0$)|
|Skewness / _Schiefe_|$\sqrt{8/k}$ (positive, _rechtsschief_; less skewed for larger $k$)|
|Excess kurtosis / _Exzess_|$12/k$ (kurtosis / _Wölbung_ $= 3 + 12/k$)|
|Moment generating function / _momenterzeugende Funktion_|$(1 - 2t)^{-k/2}$ for $t < \tfrac12$|
|Characteristic function / _charakteristische Funktion_|$(1 - 2it)^{-k/2}$|

**Reproductive property / Reproduktivität:** for independent $X \sim \chi^2(m)$, $Y \sim \chi^2(n)$:

$$ X + Y \sim \chi^2(m+n) $$

Reason: $X$ is a sum of $m$ squared standard normals, $Y$ of $n$, so $X+Y$ is a sum of $m+n$ squared standard normals.

### Relations to other distributions

- **Gamma distribution:** $\chi^2(k) = \Gamma!\left(\frac{k}{2}, \frac12\right)$ (special case, see above).
- **Exponential distribution:** $\chi^2(2) = \operatorname{Exp}!\left(\frac12\right)$.
- **Erlang distribution:** $\chi^2(2n)$ equals the Erlang distribution with $n$ degrees of freedom and rate $\frac12$.
- **Normal approximation / Normalapproximation:** for large $k$ the standardized variable $\dfrac{\chi^2_k - k}{\sqrt{2k}}$ is approximately $\mathcal{N}(0,1)$. For $k > 30$, $\sqrt{2\chi^2_k}$ is approximately normal with mean $\sqrt{2k-1}$ and standard deviation $1$ (**Fisher**).
- **F-distribution / F-Verteilung:** for independent $X \sim \chi^2(m)$, $Y \sim \chi^2(n)$:

$$ \frac{X/m}{Y/n} \sim F(m, n) $$

- **Poisson distribution:** the probability of $k$ _or more_ events in an interval with expected number $\lambda$ equals the probability that $\chi^2(2k) \leq 2\lambda$. (Check $k=1$: $P(N \geq 1) = 1 - e^{-\lambda} = F_{\chi^2(2)}(2\lambda)$.)
- **Uniform distribution / Gleichverteilung:** for $U \sim \mathcal{U}(0,1)$ we get $-2\ln U \sim \chi^2(2)$, because $P(-2\ln U \leq x) = P(U \geq e^{-x/2}) = 1 - e^{-x/2}$. For i.i.d. $U_1, \ldots, U_n$:

$$ -2\sum_{i=1}^{n} \ln U_i \sim \chi^2(2n) $$

### Quantile function / Quantilfunktion

The $p$-quantile $\chi^2_{k;p}$ solves $F_X(x) = p$ and is therefore given by the inverse of the regularized incomplete gamma function:

$$ \chi^2_{k;p} = 2,P^{-1}!\left(\frac{k}{2},, p\right) $$

In practice these values are read from a **quantile table** / _Quantiltabelle_ or computed by software (e.g. Excel `CHIINV`). Because $\chi^2$ is not symmetric, lower and upper quantiles differ.

### Why it matters in statistics (Anwendungen)

**Sample variance / Stichprobenvarianz.** For a sample $x_1, \ldots, x_n$ from $\mathcal{N}(\mu, \sigma^2)$ with sample mean $\bar{x}$ and **corrected sample variance** / _korrigierte Stichprobenvarianz_

$$ s^2 = \frac{1}{n-1}\sum_{i=1}^{n}(x_i - \bar{x})^2 $$

we have

$$ \frac{(n-1),s^2}{\sigma^2} \sim \chi^2(n-1) $$

Only $n-1$ degrees of freedom: one is "used up" by the sample mean, because the last deviation $x_n - \bar{x}$ is already determined by the other $n-1$ (the deviations sum to 0). That is why we divide by $n-1$ (the number of degrees of freedom). The proof uses Helmert's orthonormal transformation of the $x_i$ into new independent variables.

**Confidence interval for the variance / Konfidenzintervall für die Varianz.** With $q_p$ the $p$-quantile of $\chi^2(n-1)$, the $(1-\alpha)$-confidence interval is

$$ \left[\frac{(n-1),s^2}{q_{1-\alpha/2}},;; \frac{(n-1),s^2}{q_{\alpha/2}}\right] $$

_Example:_ $n = 100$, $\alpha = 0.05$: $q_{0.025} \approx 73.4$ and $q_{0.975} \approx 128.4$ (for $99$ degrees of freedom), so the interval for $\sigma^2$ is about $[,0.77,s^2,; 1.35,s^2,]$.

**Goodness of fit / Anpassungsgüte.** To decide whether a model (a line, a parabola, a logarithm, ...) explains measured data, one compares the $\chi^2$ values of the models: the smallest $\chi^2$ fits best. Details belong to the **chi-squared test** / _Chi-Quadrat-Test_.

### Non-central chi-squared distribution / Nichtzentrale Chi-Quadrat-Verteilung

If the normal variables are _not centered_, i.e. $X_i \sim \mathcal{N}(\mu_i, 1)$ independent, then

$$ \sum_{i=1}^{k} X_i^2 \sim \chi^2(k, \lambda), \qquad \lambda = \sum_{i=1}^{k}\mu_i^2 $$

with the **non-centrality parameter** / _Nichtzentralitätsparameter_ $\lambda$ as second parameter. Equivalent view as a **mixture distribution** / _Mischverteilung_: $\chi^2(k + 2J)$ with $J \sim \text{Poisson}!\left(\frac{\lambda}{2}\right)$. For $\lambda = 0$ we recover the central distribution.

### Derivation of the density (sketch)

The joint density of $Z_1, \ldots, Z_k$ is the $k$-fold product of standard normal densities, $(2\pi)^{-k/2}\exp(-\tfrac12\sum z_i^2)$. It only depends on $r^2 = \sum z_i^2$. So $P(x \leq \chi^2_k \leq x + dx)$ is $(2\pi)^{-k/2}e^{-x/2}$ times the **volume of the shell** / _Kugelschale_ between the balls of radius $\sqrt{x}$ and $\sqrt{x+dx}$. Using the volume of the $k$-dimensional ball ($\propto R^k$) this gives a density proportional to $x^{k/2-1}e^{-x/2}$, which is the formula above.

---

## Sample Mean, z-Test & t-Distribution / Stichprobenmittel, z-Test & t-Verteilung

### Distribution of the sample mean / Verteilung des Mittelwerts

Let $X_1, \ldots, X_n$ be **independent and identically distributed** (i.i.d.) / _unabhängig und identisch verteilt_ with $X_i \sim \mathcal{N}(\mu, \sigma^2)$. Then the **arithmetic mean** / _arithmetisches Mittel_

$$ \bar{X} = \frac{1}{n}\sum_{i=1}^{n} X_i ;\sim; \mathcal{N}!\left(\mu,; \frac{\sigma^2}{n}\right) $$

- again **normally distributed** (sums of independent normal variables are normal),
- the **same expectation** $\mu$ (since $E(\bar X) = \frac1n \cdot n\mu$),
- a **smaller standard deviation** $\frac{\sigma}{\sqrt n}$ (since $\operatorname{Var}(\bar X) = \frac{1}{n^2}\cdot n\sigma^2$).

The quantity $\frac{\sigma}{\sqrt{n}}$ is called the **standard error of the mean** / _Standardfehler des arithmetischen Mittels_.

### z-Test (σ known) / z-Test (σ bekannt)

**Standardizing** / _Standardisieren_ (z-transformation, as before):

$$ Z = \frac{\bar{X} - \mu_0}{\sigma/\sqrt{n}} ;\sim; \mathcal{N}(0,1) $$

Here $\mu_0$ is given by the **null hypothesis** / _Nullhypothese_ $H_0: \mu = \mu_0$, and $\sigma$ is _assumed to be known_. The two-sided **p-value** is a tail probability of $\Phi$ (the complementary CDF from above):

$$ p = 2\bigl(1 - \Phi(\lvert z \rvert)\bigr) $$

$H_0$ is rejected at level $\alpha = 0.05$ if $\lvert z \rvert > 1.96$.

_Example:_ $n = 25$, $\sigma = 10$, $\bar{x} = 104$, $\mu_0 = 100$:

$$ z = \frac{104 - 100}{10/\sqrt{25}} = 2, \qquad p = 2,(1 - \Phi(2)) \approx 2 \cdot 0.02275 = 0.0455 < 0.05 $$

so $H_0$ is rejected.

### Empirical standard deviation / Empirische Standardabweichung

If $\sigma$ is unknown it is estimated from the sample:

$$ S^2 = \frac{1}{n-1}\sum_{i=1}^{n}\bigl(X_i - \bar{X}\bigr)^2 $$

(the **corrected sample variance** / _korrigierte Stichprobenvarianz_, divided by the $n-1$ degrees of freedom). By the chi-squared section,

$$ V = \frac{(n-1),S^2}{\sigma^2} \sim \chi^2(n-1) $$

and for normal samples $V$ is _independent_ of $\bar{X}$.

### t-Distribution / t-Verteilung (σ unknown)

Replacing $\sigma$ by $S$ gives

$$ T = \frac{\bar{X} - \mu_0}{S/\sqrt{n}} ;\sim; t(n-1) $$

This is exactly the ratio of a standard normal variable and the square root of an independent chi-squared variable divided by its degrees of freedom:

$$ T = \frac{Z}{\sqrt{V/(n-1)}}, \qquad Z \sim \mathcal{N}(0,1),; V \sim \chi^2(n-1) $$

In general, a $t(\nu)$ distribution with $\nu$ **degrees of freedom** / _Freiheitsgrade_ has the density

$$ f_T(t) = \frac{\Gamma!\left(\frac{\nu+1}{2}\right)}{\sqrt{\nu\pi};\Gamma!\left(\frac{\nu}{2}\right)}\left(1 + \frac{t^2}{\nu}\right)^{-\frac{\nu+1}{2}} $$

so the gamma function appears here again. Properties:

- symmetric around $0$, $E(T) = 0$ for $\nu > 1$, $\operatorname{Var}(T) = \frac{\nu}{\nu - 2}$ for $\nu > 2$
- **heavier tails** / _schwerere Ränder_ than the normal distribution (extra uncertainty from estimating $\sigma$)
- for **increasing degrees of freedom** it approaches $\mathcal{N}(0,1)$; for $\nu = 1$ it is the **Cauchy distribution**

Quantiles that show this convergence ($t_{0.975}$ is the value used for a two-sided 95 % test):

|$\nu$|4|9|29|$\infty$ (normal)|
|:--|:-:|:-:|:-:|:-:|
|$t_{0.975}$|2.776|2.262|2.045|1.960|

_Same example as above with unknown $\sigma$_ ($s = 10$ estimated, $n = 25$, so $\nu = 24$): $t = 2$, but now $t_{0.975} \approx 2.064 > 2$ and $p \approx 0.057$, so $H_0$ is **not** rejected. The heavier tails make the test more cautious.

In R: `pt(2, df = 24)` for the CDF, `qt(0.975, df = 24)` for the quantile.

---

## Transformations of Random Variables

### Absolute value of a normal variable / Betrag einer Normalverteilten ($Y = |X|$)

Also called the **folded normal distribution** / _gefaltete Normalverteilung_. For $X \sim \mathcal{N}(0,1)$ and $y \geq 0$:

$$ F_Y(y) = P(-y \leq X \leq y) = 2\Phi(y) - 1 = \operatorname{erf}!\left(\frac{y}{\sqrt{2}}\right) $$

**Differentiating** / _Ableiten_ gives the density, which "doubles" on the non-negative half-line due to symmetry:

$$ f_{|X|}(y) = \begin{cases} 2 f_X(y) = \sqrt{\dfrac{2}{\pi}};e^{-y^2/2}, & y \geq 0, \[2mm] 0, & y < 0. \end{cases} $$

The CDF of the folded normal distribution _is_ the error function (this is its most direct meaning).

### General principle (CDF method)

To find the distribution of $Y = g(X)$: compute $F_Y(y) = P(g(X) \leq y)$ in terms of $F_X$, then differentiate to get $f_Y$. Example $Y = X^2$ with $X \sim \mathcal{N}(0,1)$ and $y > 0$:

$$ F_{X^2}(y) = P(-\sqrt{y} \leq X \leq \sqrt{y}) = 2\Phi(\sqrt{y}) - 1, \qquad f_{X^2}(y) = \frac{\varphi(\sqrt{y})}{\sqrt{y}} = \frac{1}{\sqrt{2\pi y}},e^{-y/2} $$

This is the gamma density with $\alpha = \beta = \frac12$, i.e. $X^2 \sim \chi^2(1)$. The folded normal $|X|$ above works the same way.

---

## Extreme Values / Extremwerte

### Maximum

For $Y = \max(X_1, \ldots, X_n)$ with **independent and identically distributed (i.i.d.)** / _unabhängig und identisch verteilt (u.i.v.)_ variables, "the maximum is $\leq y$" means _all_ are $\leq y$:

$$ F_Y(y) = P(X_1 \leq y ,\wedge, \dots \wedge, X_n \leq y) = \prod_{i=1}^n P(X_i \leq y) = \bigl(F_X(y)\bigr)^n $$

For $n = 2$ this is the formula $F_Y(y) = (F_X(y))^2$. The density follows by differentiation:

$$ f_Y(y) = n,\bigl(F_X(y)\bigr)^{n-1} f_X(y) $$

### Minimum

"The minimum is $> y$" means _all_ are $> y$, so use the survival function:

$$ F_{\min}(y) = 1 - \bigl(1 - F_X(y)\bigr)^n $$

### Example: maximum of two uniform variables

For $X_1, X_2 \sim \mathcal{U}(0,1)$ i.i.d. we have $F_X(y) = y$ on $[0,1]$, so

$$ F_Y(y) = y^2, \qquad f_Y(y) = 2y, \qquad E[Y] = \int_0^1 y \cdot 2y,dy = \frac{2}{3} $$

The maximum of two uniform numbers is on average larger than a single one (expectation $\frac12$), which makes sense.

---

## Summary: Relations at a glance

|Connection|Formula|
|---|---|
|Density ↔ CDF|$f_X = F_X'$, $;F_X(x) = \int_{-\infty}^x f_X(t),dt$|
|Interval probability|$P(a < X \leq b) = F_X(b) - F_X(a)$|
|Normal ↔ Standard normal|$F_X(x) = \Phi!\left(\frac{x-\mu}{\sigma}\right)$|
|Error integral ↔ error function|$\Phi(x) = \frac12\left(1 + \operatorname{erf}\frac{x}{\sqrt2}\right)$|
|Gamma function ↔ factorial|$\Gamma(n) = (n-1)!$|
|Gamma function ↔ Gaussian integral|$\Gamma(\tfrac12) = \sqrt\pi$|
|Gamma distribution ↔ exponential|$\Gamma(1,\beta) = \operatorname{Exp}(\beta)$|
|Gamma distribution ↔ chi-squared|$\chi^2(k) = \Gamma(\tfrac k2, \tfrac12)$|
|Chi-squared ↔ normal|$\chi^2(k) = \sum_{i=1}^k Z_i^2$, $;Z_i \sim \mathcal{N}(0,1)$|
|Folded normal ↔ error function|$F_{\lvert X\rvert}(y) = \operatorname{erf}!\left(\frac{y}{\sqrt2}\right)$|
|Maximum of i.i.d.|$F_{\max} = F_X^n$|
|Uniform → any distribution|$X = F^{-1}(U)$ has CDF $F$ (inversion method)|
|CDF turns data into uniform|$F(X) \sim \mathcal{U}(0,1)$ (probability integral transform)|
|Uniform → chi-squared|$-2\ln U \sim \chi^2(2)$|
|Poisson ↔ chi-squared|$P(N \geq k) = P\bigl(\chi^2(2k) \leq 2\lambda\bigr)$|
|Chi-squared ↔ sample variance|$\frac{(n-1)s^2}{\sigma^2} \sim \chi^2(n-1)$|
|Chi-squared ↔ F-distribution|$\frac{X/m}{Y/n} \sim F(m,n)$|
|Variance|$\operatorname{Var}(X) = E(X^2) - (E(X))^2$|
|Expectation via CDF ($X \geq 0$)|$E(X) = \int_0^\infty (1 - F_X(x)),dx$|
|Sample mean (normal)|$\bar{X} \sim \mathcal{N}(\mu, \sigma^2/n)$, standard error $\sigma/\sqrt{n}$|
|z-test statistic ($\sigma$ known)|$\frac{\bar X - \mu_0}{\sigma/\sqrt n} \sim \mathcal{N}(0,1)$|
|t-test statistic ($\sigma$ unknown)|$\frac{\bar X - \mu_0}{S/\sqrt n} \sim t(n-1)$|
|t ↔ normal & chi-squared|$T = Z/\sqrt{V/\nu}$, $Z \sim \mathcal{N}(0,1)$, $V \sim \chi^2(\nu)$|
|R functions|`d` density, `p` CDF, `q` quantile function, `r` random numbers|

## Glossary EN ↔ DE

|English|Deutsch|
|---|---|
|cumulative distribution function (CDF)|Verteilungsfunktion|
|probability density function (p.d.f.)|Wahrscheinlichkeitsdichte / Dichtefunktion|
|probability mass function (p.m.f.)|Wahrscheinlichkeitsfunktion / Zähldichte|
|complementary CDF, survival function|komplementäre Verteilungsfunktion, Überlebensfunktion|
|quantile function (inverse CDF)|Quantilfunktion (Umkehrfunktion der Verteilungsfunktion)|
|empirical distribution function|empirische Verteilungsfunktion|
|inverse transform sampling|Inversionsmethode|
|standard normal distribution|Standardnormalverteilung|
|(Gaussian) error integral|(Gaußsches) Fehlerintegral|
|error function / complementary error function|Fehlerfunktion / komplementäre Fehlerfunktion|
|gamma function|Gammafunktion|
|incomplete / regularized gamma function|unvollständige / regularisierte Gammafunktion|
|gamma distribution|Gammaverteilung|
|chi-squared distribution|Chi-Quadrat-Verteilung|
|degrees of freedom|Freiheitsgrade|
|folded normal distribution|gefaltete Normalverteilung|
|shape / rate / scale parameter|Form- / Raten- / Skalenparameter|
|expectation (mean), variance, skewness|Erwartungswert, Varianz, Schiefe|
|independent and identically distributed (i.i.d.)|unabhängig und identisch verteilt (u.i.v.)|
|convolution|Faltung|
|sigmoid function|Sigmoidfunktion|
|odd function|ungerade Funktion|
|moment generating function|momenterzeugende Funktion|
|inverse transform sampling (inversion method)|Inversionsmethode|
|simulation lemma|Simulationslemma|
|probability integral transform|Wahrscheinlichkeitsintegraltransformation|
|pseudo-random numbers|Pseudozufallszahlen|
|rejection sampling|Verwerfungsmethode|
|step function|Treppenfunktion|
|random walk|Irrfahrt|
|queueing theory|Warteschlangentheorie|
|sample variance (corrected)|(korrigierte) Stichprobenvarianz|
|confidence interval|Konfidenzintervall|
|goodness of fit|Anpassungsgüte|
|non-central chi-squared distribution|nichtzentrale Chi-Quadrat-Verteilung|
|non-centrality parameter|Nichtzentralitätsparameter|
|kurtosis (excess)|Wölbung (Exzess)|
|mixture distribution|Mischverteilung|
|F-distribution|F-Verteilung|
|reproductive property|Reproduktivität|
|expectation (mean)|Erwartungswert|
|moment of order $k$|Moment der Ordnung $k$|
|standard deviation|Standardabweichung|
|lower / upper quartile|unteres / oberes Quartil|
|median|Median|
|Bernoulli / binomial / geometric / Poisson distribution|Bernoulli- / Binomial- / Geometrische / Poisson-Verteilung|
|uniform distribution|Gleichverteilung|
|standard error of the mean|Standardfehler des arithmetischen Mittels|
|null hypothesis|Nullhypothese|
|p-value|p-Wert|
|z-test|z-Test|
|t-distribution|t-Verteilung|
|arithmetic mean|arithmetisches Mittel|
|absolutely convergent|absolut konvergent|
|random deviates (R)|Zufallszahlen|

---

# Links

- [Probability theory](https://en.wikipedia.org/wiki/Probability_theory?useskin=vector)
- [Conditional Probability](https://en.wikipedia.org/wiki/Conditional_probability?useskin=vector)
- [Law of total probablity](https://en.wikipedia.org/wiki/Law_of_total_probability?useskin=vector)
- [Bedingte Wahrscheinlichkeit](https://de.wikipedia.org/wiki/Bedingte_Wahrscheinlichkeit?useskin=vector)
- [Cumulative distribution function](https://en.wikipedia.org/wiki/Cumulative_distribution_function?useskin=vector)
- [Fehlerintegral](https://de.wikipedia.org/wiki/Fehlerintegral?useskin=vector)
- [Fehlerfunktion](https://de.wikipedia.org/wiki/Fehlerfunktion?useskin=vector)
- [Gammafunktion](https://de.wikipedia.org/wiki/Gammafunktion?useskin=vector)
- [Gammaverteilung](https://de.wikipedia.org/wiki/Gammaverteilung?useskin=vector)
- [Chi-Quadrat-Verteilung](https://de.wikipedia.org/wiki/Chi-Quadrat-Verteilung?useskin=vector)
- [Inverse transform sampling](https://en.wikipedia.org/wiki/Inverse_transform_sampling?useskin=vector)
- [Inversionsmethode](https://de.wikipedia.org/wiki/Inversionsmethode?useskin=vector)
- [VoWi: Hilfe:Statistik und Wahrscheinlichkeitstheorie](https://vowi.fsinf.at/wiki/Hilfe:Statistik_und_Wahrscheinlichkeitstheorie)
- https://www.youtube.com/watch?v=_lq7zfecSpw
- https://www.itl.nist.gov/div898/handbook/eda/section3/eda366.htm



