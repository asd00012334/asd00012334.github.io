---
title: On the Communication Complexity of EQ
date: 2019-05-18 03:27:34
tags:
- complexity
- communication
---

The notion of communication complexity is to look only at number of information that is being exchanged between multiple parties.
## Deterministic Communication

### Def. Communication Complexity
A (communication) protocol $P$ is a rooted binary tree, with each internal node $v$ labelled with a boolean function,
$$
f_v: \{0,1\}^n\rightarrow\{0,1\}
$$

On input $(x,y)$, the computation start from the root. At each internal node, either Alice or Bob sendss one bit. When Alice is speaking, $f_v(x)$ is sent, otherwise, $f_v(y)$ is sent. If $0$ is yield, the protocol go to the left child, otherwise, it goes to the right child. Each leaf node is labelled with output functions,
$$
f_v: \{0,1\}^n\times\{0,1\}^n\rightarrow\{0,1\},
$$
then output $f(x,y)$. In our setting, we require Alice and Bob to make consensus on their outputs, if not, then whoever knows the output first could send out one output bit, so both would agree on the same output, that would only require one more bit.

We said the depth of $P$ is the depth of underlying tree. And (communication) complexity of a function $f:\{0,1\}^n\times\{0,1\}^n$ be the smallest depth over all possible $P$. For deterministic one, we denote $D^{cc}(f)$.

### Cor. $D^{cc}(f)\leq n+1$

Simply send all bits at once from Alice to Bob, then send output bits from Bob.

### Def. Combinatorial Rectangle

A (combinatorial) rectangle is a set $A\times B$ where
$$
A, B\subseteq \{0,1\}^n.
$$

We care about combinatorial rectangle because it captures the state of communication. Namely, we have the following.

### Lem.

Given protocol $P$, node $v$. define $I_v:=\{(x,y):P$ on $(x,y)$ goes through node $v\}$. Then $I_v$ is a rectangle.

#### proof.

Let's inductively suppose $v$ is a $b$-child of $u$ where $I_u=A\times B$ is a rectangle. Then $I_v=(A\cap f^{-1}[b])\times B$, which is obviously a rectangle. $_\Box$

Furthermore, because each $I_v$'s at leaves are necessarily disjoint, we can partitioned all possible inputs into rectangles.

### Cor.
Suppose $P$ is a $c$-bit protocol for $f$, then $\{0,1\}^n\times \{0,1\}^n$ could be partitioned into $2^c$ $f$-monochromatic rectangles.


### Def.
A $b$-fooling set $S\subseteq\{0,1\}^n\times\{0,1\}^n$ for $f$ is a $b$-monochromatic subset that contains no $b$-monochromatic rectangles of size larger than 1. Equivalently,
$$
\forall (x,y)\in S: f(x,y)=b,\\
\forall (x,y),(x',y')\in S: f(x,y')\neq b\lor f(x',y)\neq b.
$$

### Cor.
Let $S$ be a $b$-fooling set for $f$, then $D^{cc}(f)\geq \lg|S|$.

#### proof.
It is because $S$ could collect no more than one ellement from each $f$-monochromatic rectangle, and we could partitioned all possible input into no more than $2^c$ monochromatic rectangle, where $c$ is the depth of $P$. Therefore, we have $2^c\geq |S|$. $_\Box$

The corollary gives a complexity lower bound with respect to size of a fooling set. Techniques using this to provide communication lower bounds are called the *fooling set methods*. For example, let's consider the equality problem,
$$
EQ_n = \{(x,y)\in\{0,1\}^n\times\{0,1\}^n:x=y\}.
$$
Picking $EQ_n$ itself as the $1$-fooling set,
$$
D^{cc}(EQ_n)\geq n.
$$
By looking closer, the lower bound $n$ only contains the $1$-monochromatic rectangles. If we look closer, there must be at least one $0$-monochromatic rectangle contained in the communication matrix. We therefore have the folloing lower bound.
### Prop.
$$
D^{cc}(EQ_n)\geq n+1.
$$

## Non-deterministic Communication
When walking on the communication tree, we non-deterministically take our step by descending to possibly both childs. We output 1 if one bracnch output 1, otherwise output 0. Equivalently. the notion of non-deterministic communication could also be introduced in the "verifier-certificate" manner. Which is the existence of verifier functions $V_a,V_b:\{0,1\}^n\times \{0,1\}^k\rightarrow \{0,1\}$ for both Alice and Bob where,
$$
x\in L\Rightarrow \exists z\in\{0,1\}^k:V_a(x,z)=1\land V_b(y,z)=1,\\
x\not\in L\Rightarrow\forall z\in\{0,1\}^k:V_a(x,z)=0\lor V_b(y,z)=0.
$$
The smallest possible $k$ is the non-deterministic communication complexity, denoted $N_1(f)$. Similarly, we could define the co-non-deterministic communication and $N_0(f)$.

It follows immediately that, if we choose $0$-certificate as the index of bit pointing to where $x,y$ differ (if there is), then the following upper bound holds.

### Cor.
$$
N_0(EQ_n)\leq\lceil\lg n\rceil.
$$

### Def.
For $f:\{0,1\}^n\times\{0,1\}^n\rightarrow\{0,1\}$, the $b$-cover number $C_b(f)$ is defined as the minium number of $b$-monochromatic rectangles $A_i\times B_i$ that $f(x,y) = \bigvee_{i}[x\in A_i\land y\in B_i]$.


### Lem.
$$
N_b(f)=\lceil\lg C_b(f)\rceil.
$$

#### proof.
For $N_b(f)\leq\lceil\lg C_b(f)\rceil$ part, simply choose $b$-certificate be an index pointing to a $b$-monochromatic rectangle. For $N_b(f)\geq\lceil\lg C_b(f)\rceil$ part, we know that each $b$-certificate $z$ would yield a rectanglel, namely,
$$
\{V_a(x,z)=b\}\times\{V_b(y,z)=b\}.
$$
These rectangles cover the whole $b$-colorred inputs. Therefore we have,
$$
2^{N_b(f)}\geq C_b(f).
$$
$_\Box$

By the similar argument as above, because there is a $1$-fooling set as large as $2^n$ and some $0$-rectangles in $EQ_n$. We have $C_b(EQ_n)\geq 2^n+1$, therefore we have the following lower bound.
### Cor.
$$
N_1(EQ_n)\geq n+1.
$$

## Randomized Communication
The randomized communication is essentially similar as the previous definition. Except each step here could be performed randomly. We are going to show a protocol that solves $EQ_n$ in $O(\lg n)$ number of bits.

### Cor.
There exists a $coRP$ communication protocol that resolve $EQ_n$
#### proof.
Consider the following protocol.

On input $x,y$, first we could compute
$$
p_x(z)=\sum_{1\leq i\leq n}x_iz^i,\\
p_y(z)=\sum_{1\leq i\leq n}y_iz^i.
$$
Randomly pick $r\in\mathbb{F}$, accept if $p_x(r)=p_y(r)$, otherwise reject.
Since a polynomial can only have degree number of roots, by picking $\mathbb{F}$ to be at least $2$ times larger than $n\geq\deg[p_x(z)-p_y(z)]$, we are guaranteed to obtain a $coRP$ protocol, since if $x=y$, the protocol certainly accept, otherwise,
$$
Pr_r[p_x(r)=p_y(r)]\leq \frac{\deg(p_x-p_y)}{|\mathbb{F}|}\leq\frac{1}{2}.
$$
$_\Box$

## Complexity Classes
We sum up with relations between communication complexity classes.
### Def.
- $P^{cc}=\{f:D^{cc}(f)\leq poly(\lg n)\}$
- $NP^{cc}=\{f:N_1^{cc}(f)\leq poly(\lg n)\}$
- $coNP^{cc}=\{f:N_0^{cc}(f)\leq poly(\lg n)\}$
- $RP^{cc}=\{f:\exists$ RP protocol with complexity $\leq poly(\lg n)\}$
- $coRP^{cc}=\{f:\exists$ coRP protocol with complexity $\leq poly(\lg n)\}$

### Theorems
From above arguement, we conclude the following relations.
- $P^{cc}\subsetneq RP^{cc}\subseteq NP^{cc}$
- $P^{cc}\subsetneq coRP^{cc}\subseteq coNP^{cc}$
- $NP^{cc}\neq coNP^{cc}$
- $NP^{cc}\not\supseteq coRP^{cc}$
- $coNP^{cc}\not\supseteq RP^{cc}$


