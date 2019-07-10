---
title: Heirarchy Theorem
date: 2019-02-16 23:32:12
tags: complexity
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

With more resource comes more power, at least computationally speaking.

### Constructibility
Given a function, $f:\mathbb{N}\rightarrow\mathbb{N}$, it is said to be (weakly) time/space construtible if and only if the map $1^n\mapsto 1^{f(n)}$ could be computed in $O(f(n))$ time/space resources.

It basically says that $f$ is computationally easier to determine.

### Diagonalization for Undecidability
One way to show that there's a problem undecidable is by diagonalization.
Consider the following language,
$$
L=\{w=\langle M, x\rangle: w\not\in L(M)\},
$$
where M is a Turing machine. If machine $D$ decides $L,$ then
$$
w=\langle D,x\rangle \in L\iff w\not\in L(D)=L,
$$
which is a contradiction. Thus there exists a undecidable problem.


### Space Heirachy Theorem
Given $s(n)$ weakly space constructible, then there exists a language $A$ that
- $A\in SPACE(s(n))$
- $A\not\in SPACE(o(s(n)))$

We are showing this by also diagonalization. Consider a Turing machine $D$ doing the following,
- On input $w=\langle M,10^k\rangle$ where $M$ is a Turing machine, we try to simulate $M$ on input $w$ under following modification.
- By space constructibility, calculate $1^{s(n)}$ as memory boundary, if during simulation $M$ attempt to use more then $s(n)$ memory, reject.
- Maintain a time counter, if simulatation time ever exceeds $2^{s(n)}$, reject.
- If $M$ accepts $w$, reject; otherwise, accept.

It is clear from declaration that $L(D)\in SPACE(s(n)).$ If $L(D)\in SPACE(o(s(n))),$ then for those machines $M$ running in space $g\in o(f)$ and large enough $N_0$, $g(n)<s(n)$ whenever $n>N_0.$ Therefore consider $k=N_0,$ $M$ runs to the last step. But then $w\in L(D)\iff w\not\in L(D),$ which is a contradiction.

#### Remark.
$SPACE(s(n))\subseteq TIME(2^{O(s(n))})$, so the third step make sure the total process using no more then $O(s(n))$ memory.

### Time Heirachy Theorem
Given $t(n)$ weakly time constructible, then there exists a language $A$ that
- $A\in TIME(t(n))$
- $A\not\in TIME(o(t/\log t))$

The proof is essentially similar, but note that to avoid zigzag that typically wasting time, we need to drag the time counter and state information along with the pointer location. That would cause $O(log(t))$ time for each transition.


