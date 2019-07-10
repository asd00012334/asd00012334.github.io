---
title: Miller-Rabin Primality Test
date: 2019-03-25 18:09:07
tags:
- prime
- complexity
---

Although there's AKS test for primality test, it is usually impractical to use. We will introduce a test proposed by Gary Miller based on Reimann hypothesis then modifed by Michael Rabin into a randomized version that does not rely on such conjecture.

### Theorem [Miller, Rabin]
$$
PRIMES\in coRP
$$

On input $n\in\mathbb{Z}$,
- rule out even numbers, and randomly pick $a\in\mathbb{Z}_n^\times$
- assume $n=r\cdot 2^k$, $r$ is odd
- accept if and only if the following holds
    - $a^r=1$
    - $\exists l<k, a^{r\cdot 2^l}=-1$

### Conversibility of Fermat's little theorem
It is a well known fact that for any prime $p$,
$$
\forall a\in\mathbb{Z}_p: a^{p-1} = 1.
$$

It is natural to ask if converse still hold, i.e. given $n\in\mathbb{Z}$ that $\forall a\in\mathbb{Z}_n:a^{n-1}=1$, does it imply that $n$ is prime numbers? If so, it might naturally yield a primality test algorithm. Unfortunately, Carmichael numbers have not only been found but also proven to be infinitely many.

But since $\mathbb{Z}_p$ is a finite field, consider the polynomial,
$$
f(x) = x^2-1,
$$
it contains no more then 2 roots, which is $\pm 1$. The Miller-Rabin test argues that converse "almost" holds.

### Easy Cases
If input is prime, from above we have shown that it is accepted, that is also why we have cut out error at one side. If given odd $n\in\mathbb{N}$, for $n=p^e$ be prime power, the argument in [previous discussion](https://asd00012334.github.io/2019/03/22/Randomized-Primality-Test/) has shown that it is accepted with probability bounded under $\frac{1}{2}$.


### Proof
The algorithm clearly uses polynomial time. Also, it suffices to discuss the case where $n=m_1m_2$ composite. Let $\phi(n) = r\cdot 2^k, 2\nmid r$.

Consider an inclusion tower of subgroups,
$$
S_i:= \{a\in\mathbb{Z}_n^\times : a^{r\cdot 2^i}=1\}, i\leq k\\
S_0\leq S_1\leq ...\leq S_k\leq S_{k+1}:=\mathbb{Z}_n^\times.
$$

If this inclusion tower is strict at one place, i.e. for some $c$, $S_{c-1}\lneq S_c$, then by Lagrange theorem, $|S_{c-1}|\leq |S_c|/2$. Then by picking the $c$ to be largest one, we'd have
$$
Pr(\exists i:a^{r\cdot 2^i}=-1\lor a^r=1)\leq Pr(a\in S_{c-1})\leq \frac{1}{2}.
$$

Suppose otherwise, $S_0=S_1=...=S_k=\mathbb{Z}_n^\times$, then
$$
\forall a\in\mathbb{Z}_n^\times: a^r=1.
$$
Note that this case only possibly happens when $n$ is a Carmichael numbers, the Carmichael numbers have been proven to be square free, and we are going to show that it's not possible to even happens.
And by Chinese remainder theorem,
$$
\mathbb{Z}_n\cong\mathbb{Z}_{m_1}\times\mathbb{Z}_{m_2},
$$
choose $m_1$ to be $p^e$ prime power and co-prime with $m_2$. By the fact that $\mathbb{Z}_{p^e}=\langle \alpha\rangle$ is cyclic, assume
$$
a\mapsto (\alpha,1),
$$
defined by such ring isomorphism. Then
$$
a^r\mapsto(\alpha^r,1)=(1,1).
$$
But then $r=0\mod\phi(p^e)$, which contradict with the fact that $r$ is odd. $_\Box$

