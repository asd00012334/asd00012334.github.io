---
title: Randomized Primality Test
date: 2019-03-22 22:07:54
tags:
- prime
- complexity
---

Primality testing is a computational problem that determines whether a given integer $n$ is prime or composite.
$$
PRIMES:=\{p\in\mathbb{N}:\forall n<p, n\nmid p\}
$$

Below we enlist several primality testing algorithm, and will ellaborate one BPP variant of the Miller-Rabin test.

### Theorem [Strassen, Solovay] 
$$
PRIMES\in coRP
$$
On input $n\in\mathbb{N}$, 
- randomly pick $a\in\mathbb{Z}_n$
- compute the legendre symbol $\pmatrix{\frac{a}{n}}$
- if $\pmatrix{\frac{a}{n}}$ = 0 or $a^{(n-1)/2}$, reject; otherwise, accept.

### Theorem [Miller, Rabin]
$$
PRIMES\in coRP
$$
On input $n\in\mathbb{Z}$,
- randomly pick $a\in\mathbb{Z}_n^\times$
- assume $n=r\cdot 2^k$, $r$ is odd
- accept if and only if the following holds
    - $a^r=1$
    - $\exists l<k, a^{r\cdot 2^l}=-1$

We leave the proof to [this article](https://asd00012334.github.io/2019/03/25/Miller-Rabin-Primality-Test/).

### Theorem [Agrawal, Kayal, Saxena]
$$
PRIMES\in P
$$

---

We are going to prove a weaker version of the above theorem, which gives a $BPP$ algorithm. Note that
$$
P\subseteq coRP\subseteq BPP
$$
The algorithm we're going to prove could be slighly modified to elliminate error at one side. In practice, the Miller-Rabin test is most oftenly used. Below we are going to ignore the fact that a uniform random number shall be approximated, instead we uses a exact random variable to make our analysis easier, since it will not affect much.

### Theorem
$$
PRIMES\in BPP
$$

**proof.** 

To prove $PRIMES\in BPP$, consider the following algorithm.

On input $n\in\mathbb{Z}$,
- reject even numbers (assume n is odd)
- randomly pick $a_i\in\mathbb{Z}_n^\times$ for $1\leq i\leq t$
- compute sequence $\{a_i^{(n-1)/2}:1\leq i\leq t\}$
    - if it is not all $\pm 1$, reject
    - if of form 1,1,...,1, reject
    - otherwise, accept

The time complexity for this algorithm is clearly polynomial w.r.t. input length. We only need to show its correctness, i.e. it makes the right decision with high probability.

*Sufficiency*
If $n$ is prime, then by Fermat's little theorem,
$$
a^{(n-1)/2} = \pm 1.
$$
Since $\mathbb{Z}_n^\times=\langle\alpha\rangle$ is cyclic, we have,
$$
a^{(n-1)/2}=-1 \iff a\not\in\langle\alpha^2\rangle.
$$
So $Pr(a^{(n-1)/2}=-1|a\in\mathbb{Z}_n^\times)=\frac{1}{2}$, the acceptance probability is $1-2^{-t}$.

*Necessity*

Now that we assume $n$ is composite, if $gcd(a,n)>1$, we just naturally reject $n$. We want to show that with high probability the sequence will contain non-$\pm 1$.

- Case $n=m_1m_2$, co-prime proper factoring.

Consider the following subsets,
$$
S_+:=\{a\in\mathbb{Z}_n^{\times}: a^{(n-1)/2}=1\},\\
S_{-}:=\{a\in\mathbb{Z}_n^{\times}: a^{(n-1)/2}=-1\}.
$$

If $S_{-}$ is empty, then the algorithm certainly reject. Otherwise, assume $b\in S_{-}$, and of course $1\in S_+$.


By Chinese remainder theorem,
$$
\mathbb{Z}_{n}\cong\mathbb{Z}_{m_1}\times\mathbb{Z}_{m_2}.
$$
Pick $c\mapsto (1,b)$ by the above isomorphism. Then
$$
c^{(n-1)/2}\mapsto (1,-1),
$$
therefore $c^{(n-1)/2}\not\in S:=S_+\cup S_-$, then $S_+\subsetneq S\subsetneq \mathbb{Z}_n$. Since multiplication is closed under $S, S_+$, both are proper subgroups. By Lagrange theorem, $|S|\leq \frac{\phi(n)}{2}$. Therefore
$$
Pr(\exists i,a_i^{(n-1)/2}\neq\pm 1)\geq 1-2^{-t},
$$
is a lower bound for the rejection probability.

- Case $n = p^e$, prime power.

Since $\mathbb{Z}_n^\times=\langle\alpha\rangle$ is cyclic, assume $a=\alpha^k$. We have,
$$
a^{(n-1)/2}=\pm 1\mod n\\
\Rightarrow \alpha^{k(n-1)}= 1\\
\Rightarrow k(n-1)=0\mod\phi(n)
$$
Since $n-1=p^e-1=(p-1)(1+p+p^2+...p^{e-1})$ and $\phi(n)=p^e-p^{e-1}.$
The above implies that
$$
k(1+p+...+p^{e-1})=0\mod p^{e-1}\\
\Rightarrow k=0\mod p^{e-1}
$$
Therefore $Pr(a=\pm 1)\leq Pr(k=0\mod p^{e-1})=\frac{1}{p^{e-1}}\leq\frac{1}{2}$. So a lower bound for the rejection probability is $1-2^{-t}$. $_\Box$

