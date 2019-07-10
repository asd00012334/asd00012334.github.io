---
title: Free Monoid and McMillan's Inequality
date: 2019-01-20 23:21:09
tags:
---
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
<script
    src='https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/latest.js?config=TeX-MML-AM_CHTML' async>
</script>

In theory of computation, or formal language, we usually define an alphabet to be some arbitrary finite (non-empty) set. This of course shows no problem along with construction of strings that is (usually) as below.

Given a finite non-empty set $\Sigma$, a string $s$ is defined as a sequence of its elements,
$$
s=\sigma_1\sigma_2...\sigma_r\in\Sigma^*.
$$

A language is defined as collection of strings,

$$
L\subseteq\Sigma^*.
$$
We took some advantages of the notation, one might just implicitly accept that there's a binary operation that concatenate two different strings so that we don't have to write out the comma's in between.

### Alphabet

It turns out we could as well integrate the above definition based on "concatenation" only, which in this context refers to a *free monoid* operation. A monoid refer to a binary algebraic structure $(M,*)$ that satisfies:
- Associativity: $(ab)c=a(bc)$
- Identity's existence: $\forall a\in M:ea=ae=a$

A monoid is called free if there's a basis $B=\{b_1,...,b_r\}$ that generates the whole set.
$$
\forall m\in M\exists l_i's: b_{l_1}b_{l_2}...b_{l_k}=m,
$$
and the representation is unique, i.e.
$$
b_{l_1}b_{l_2}...b_{l_r}=b_{k_1}b_{k_2}...b_{k_r'}\iff r=r' \land \forall i:l_i=k_i
$$
It is also worth noting that basis of a free monoid must be unique, and the cardinality of $B$ is called its free-monoid rank. Therefore we could just refer to "alphabet" as basis of some free monoid. Following that, we immediately obtain the alphabet of sub-monoid, for instance, if $\Sigma=\{0,1\}$, then $\{0,01\}$ is an alphabet while $\{0,1,01\}$ is not.

### McMillan's Inequality

McMillan's inequality is necessary for a set of strings to be an alphabet. Suppose $S=\{s_1,s_2,...,s_k\}\subseteq\Sigma^*$ is an alphabet. For $l_i:=|s_i|$ and $|\Sigma|=r$ we have,
$$
\sum_{1\leq i\leq k} r^{-l_i} \leq 1.
$$

#### proof.

First we took $n$-power and expand the left-hand term, suppose the index of $r$ ranges from $n$ to $nL=n\max\{l_i\}$.
$$
(\sum_{1\leq i\leq k} r^{-l_i})^n = \sum_{n\leq i\leq nL} a_ir^{-i}.
$$
where $a_i$ is the number of ways to construct a length $i$ string from $n$ elements of $S$. Since $a_i\leq r^i$, we have
$$
(\sum_{1\leq i\leq k} r^{-l_i})^n\leq n(L-1).
$$
If the McMillan's inequality does not hold, as $n\rightarrow\infty$, the above inequality will be violated since the left-hand side grows much faster than the right hand side. ${}_\square$



