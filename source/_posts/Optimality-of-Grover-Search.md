---
title: Optimality of Grover Search
date: 2019-07-09 19:48:11
tags:
- complexity
- quantum
- query complexity
---

Grover search is a generic pre-image finding algorithm. It is interesting not only as a symmetric crypto adversary, but also as a line that any quantum algorithms cannot go beyond. Particularly, Grover search gives a quadratic and no more than quadratic speed up, which is one of the reasons why quantum algorithm **might not** be able to solve brute-force problems, for instance, NP-complete problems.

### Pre-image Finding Problem
A preimage finding problem generally gives an oracle $f:\{0,1\}^n\rightarrow\{0,1\}$ and ask to find any $x$ that $f(x)=1$, promsing that such $x$ exists (and sometimes more than one). For classical version, algorithms can query one boolean $x$ at a time; the quantum algorithms, on another hand, could be queried a superposition input.
$$
O_f:|x\rangle|b\rangle\mapsto |x\rangle|b\oplus f(x)\rangle, \forall x\in\{0,1\}^n
$$


To solve this classically, one must do the exponential brute-force to find a pre-image. But since a quantum algorithm could query a superposition at a time, there is the Grover search. The search process is composed of multiple iterations. For each iteration, first we could prepare the following ket from $|\psi\rangle$,
$$
|\psi\rangle=\sum_{x\in\{0,1\}^n} v_x|x\rangle\mapsto\sum_{x\in\{0,1\}^n} (-1)^{f(x)}v_x|x\rangle.
$$
We called this step *phase inversion*. Secondly, we flip the magnitude about its mean, namely we apply the following operator,
$$
2|+^n\rangle\langle+^n|-I.
$$
This operator is clearly unitary because it's eigenvalues are
$$
1,-1,\dots,-1,
$$
multiplicity counted.

### Convergence of Search
We are going to show how fast Grover search converges. In particular, it would be requiring $\Theta(\sqrt{2^n})$ queries to converge. Let's assume among all possible inputs, with fraction $\delta$ of them output 1. Consider at the i'th iteration, each search target has magnitude $v_i$, then all other non-targets are with amplitude,
$$u_i = \sqrt{\frac{1-2^n\delta v_i^2}{2^n-2^n\delta}}.$$
The mean after phase inversion would be,
$$M_i=(1-\delta)u_i+\delta v_i.$$
Then each iteration will amplify the target amplitude,
$$v_{i+1} = 2M_i+v_i = 2(1-\delta)u_i+(1+2\delta)v_i$$
Substitude with $2^n\delta v_i^2=\sin^2\theta_i$. Then since
$$
u_i=\frac{\cos\theta_i}{\sqrt{2^n(1-\delta)}},\\
v_i=\frac{\sin\theta_i}{\sqrt{2^n\delta}},
$$
we have,
$$
\frac{\sin\theta_{i+1}}{\sqrt{2^n\delta}}=\frac{2(1-\delta)\cos\theta_i}{\sqrt{2^n(1-\delta)}}+\frac{(1+2\delta)\sin\theta_i}{\sqrt{2^n\delta}},\\
\sin\theta_{i+1}=2\sqrt{(1-\delta)\delta}\cos\theta_i+(1+2\delta)\sin\theta_i.
$$
Checking the coeficient square sum do gives us 1. Substitute $\sin\phi=2\sqrt{(1-\delta)\delta}$ and $\cos\phi=1+2\delta$. We obtain,
$$\sin\theta_{i+1}=sin(\theta_i+\phi)=sin(\theta_0+q\phi).$$
Because $q\phi=\Theta(q\sqrt{\delta})$, when $q=\Theta(\frac{1}{\sqrt{\delta}})$ there is high probability that we will obtain a pre-image of 1. Particularly if such $x$ is unique, the iteration number is $\Theta(\sqrt{2^n})$. Before completely converge, the probability of getting a correct answer is $\sin^2(\theta_q)=\Theta(q^2\delta)$.


### Lower Bound of Search
In fact, the Grover search algorithm is already the optimal algorithm, in the sense that we have query lower bound for the pre-image finding problem that matches the upper bound of Grover search.

Before started, we could look at the following lemma. For convenience, we denote $N=2^n$.
#### Lemma.
For $\alpha, \beta\in\mathbb{C}^N$, if $\Vert\alpha\Vert=\Vert\beta\Vert=1$ and $\Vert\alpha-\beta\Vert\leq\epsilon$, then the probability distribution $D(\alpha), D(\beta)$ is as near as,
$$
|D(\alpha)-D(\beta)|\leq\epsilon^2+2\epsilon\leq 4\epsilon.
$$

*proof*.
Let $\alpha=\sum_i\alpha_i|i\rangle$, $\beta=\sum_i\beta_i|i\rangle$ and $\gamma=\alpha-\beta=\sum_i\gamma_i|i\rangle$. Then
$$
(D(\alpha)-D(\beta))_i=\bar{\alpha_i}\alpha_i-\beta_i\bar{\beta_i}\\
=(\beta_i+\gamma_i)(\bar{\beta_i}+\bar{\gamma_i})-\beta_i\bar{\beta_i}\\
=\gamma_i\bar{\gamma_i}+\beta_i\bar{\gamma_i}+\gamma_i\bar{\beta_i}
$$
Thus we have,
$$
|D(\alpha)-D(\beta)|\leq \epsilon^2+\langle\gamma|\beta\rangle+\langle\beta|\gamma\rangle\\
\leq\epsilon^2+2\Vert\gamma\Vert\Vert\beta\Vert\leq\epsilon^2+2\epsilon. _{\Box}
$$

In another word, as long as the 2-norm of two states is too small, their probability are indistinguishable. It suffice to consider the *phase inversion* oracle.

Then any $q$-query algorithm is composed of 
$$
U_{q+1}O_fU_q\dots O_fU_2O_fU_1.
$$
We pick adversary oracle as
$$
O_\tilde{x}:|x\rangle\mapsto(-1)^{x=\tilde{x}}|x\rangle.
$$
Comparing this oracle with identity map $Id$, let's denote
$$
|\psi_\tilde{x}^k\rangle=O_\tilde{x}U_k\dots O_\tilde{x}U_2O_\tilde{x}U_1|\psi_0\rangle,\\
|\psi_\tilde{x}^k\rangle=U_k\dots U_2U_1|\psi_0\rangle.
$$
We try to bound,
$$
\Vert|\psi_\tilde{x}^k\rangle-|\psi_{id}^k\rangle\Vert\leq\Vert|U_{k-1}\psi_\tilde{x}^{k-1}\rangle-|\psi_{id}^k\rangle\Vert\\
=\Vert O_\tilde{x}U_{k-1}|\psi_\tilde{x}^{k-1}\rangle-U_{k-1}|\psi_\tilde{x}^{k-1}\rangle\Vert+\Vert\psi_\tilde{x}^{k-1}\rangle-|\psi_{id}^{k-1}\rangle\Vert
$$
Suppose $U_{k-1}|\psi_\tilde{x}^{k-1}\rangle=\sum_{i}u_i|i\rangle$, then
$$
\Vert O_\tilde{x}U_{k-1}|\psi_\tilde{x}^{k-1}\rangle-U_{k-1}|\psi_\tilde{x}^{k-1}\rangle\Vert\leq\sqrt{4|u_\tilde{x}|^2}=2|u_\tilde{x}|.
$$
By Cauchy-Schwarz inequality,
$$
\sum_{\tilde{x}}|u_\tilde{x}|\leq\sqrt{\sum_{\tilde{x}}|u_\tilde{x}|^2\cdot N}.
$$
So one could picke one $\tilde{x}$ below or equal to the average,
$$
|u_\tilde{x}|\leq \frac{\sum_{\tilde{x}}|u_\tilde{x}|}{N}\leq\frac{1}{\sqrt{N}}.
$$
Then we have
$$
\Vert|\psi_\tilde{x}^k\rangle-|\psi_{id}^k\rangle\Vert\leq \frac{2}{\sqrt{N}}+\Vert|\psi_\tilde{x}^{k-1}\rangle-|\psi_{id}^{k-1}\rangle\Vert\leq\frac{2k}{\sqrt{N}}.
$$
Thus, we have probability differ by,
$$
|D(|\psi_\tilde{x}^q\rangle)-D(|\psi_{id}^q\rangle)|\leq 4\Vert|\psi_\tilde{x}^k\rangle-|\psi_{id}^k\rangle\Vert\leq\frac{8q}{\sqrt{N}}.
$$
If $O_{\tilde{x}}$ is distinguishible from id (by some constant difference), we must have,
$$
\Omega(1)\leq |D(|\psi_\tilde{x}^q\rangle)-D(|\psi_{id}^q\rangle)|\leq \frac{8q}{\sqrt{N}}.
$$
Thus $q\geq\Omega(\sqrt{N})._\Box$

### Quantum Query Complexity
The pre-image finding problem is a search problem, for decisional version, it is $OR_N$ problem. Where we just verify the answer by evaluating whether $H(x)=y$ on given $y$. So with the same logic applied, we have the Quantum query complexity
$$
Q(OR_N)=\Theta(\sqrt{N})
$$

