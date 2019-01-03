---
title: On the Generalised Eigenvalue Problems
date: 2018-11-20 03:00:07
tags: eigenvalue
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

### Standard Eigenvalue Probelm (SEP)
給定矩陣 $A\in\mathbb{C}^{n\times n}$，求解
$$
Ax=\lambda x,x\neq 0
$$

### Generalised Eigenvalue Problem (GEP)
給定矩陣 $A,B\in\mathbb{C}^{n\times n}$，求解
$$
Ax=\lambda Bx,x\neq 0
$$

如果 $B$ 可逆，那麼這類GEP形同 $B^{-1}A$ 的 SEP，但這個想法計算上並不可行。

- Quadratic Eigenvalue Problem (QEP)
$$
(\lambda^2M+\lambda D+K)x=0,x\neq 0
$$
對應到 GEP 設定為:
$$
\pmatrix{-D&-M\\\\I&0}\pmatrix{x\\\\\\lambda x}=\frac{1}{\lambda}\pmatrix{K&0\\\0&I}\pmatrix{x\\\ \lambda x}
$$

- Polynomial Eigenvalue Problem (PEP)
$$
\sum_{0\leq i\leq n}\lambda^iA_ix=0,x\neq 0
$$

對應到 GEP 設定為:
$$
\pmatrix{-A_1&...&...&-A_n\\\I&0&...&0\\\&\ddots&\ddots&\vdots\\\0&&I&0
}\pmatrix{x\\\ \lambda x\\\ \vdots\\\ \lambda^{n-1} x}=\frac{1}{\lambda}\pmatrix{A_0\\\&I\\\&&\ddots\\\&&&I}\pmatrix{x\\\ \lambda x\\\ \vdots\\\ \lambda^{n-1} x}
$$

- Rational Eigenvalue Problem (REP)
$$
A(\lambda)x=x,x\neq 0,
$$
其中 $a_{ij}(\lambda)\in Quot(\mathbb{C}[\lambda])$ 為有理式。

### 和微分方程的關係

以下不考慮特徵值有重根，這種情況亦有解決手段。

- SEP

考慮偏微分算子
$$
D_t:\pmatrix{x_1\\\ \vdots\\\x_n}\mapsto \pmatrix{\frac{dx_1}{dt}\\\ \vdots\\\ \frac{dx_n}{dt}}
$$
對於 $A\in\mathbb{C}^{n\times n}$ ，一階偏微分方程組
$$
D_tx=Ax
$$

若 $\lambda\in\sigma(A), Av=\lambda v$，帶入可發現
$$
x = v\cdot e^{\lambda t}
$$
構成一組可行解。

- QEP

考慮帶有阻尼的震動系統
$$
(M\cdot D_t^2+D\cdot Dt+K)x=0
$$
若 $\lambda,v$ 是一組 Quadratic eigenvalue/eigenvector，那麼帶入
$$
x=e^{\lambda t}v
$$
是一組可行解。

### Schrödinger equation

這是量子力學中一類偏微分方程
$$
\hat{H}|\psi(t)\rangle=i\hbar D_t|\psi(t)\rangle,
$$
其中 $\hat{H}$ 被稱做 Hamiltonian operator，它可以是與時間有關的線性算子，一般意義下可能與時間相關，如果 $\hat{H}$ 與時間獨立，那麼考慮其特徵函數 $v$
$$
\hat{H}v=\lambda v
$$
即可令 $e^{\frac{\lambda t}{i\hbar}}v$ 為一組可行的解。


例如在計算非相對論性單粒子系統(single nonrelativistic particle)時，引入下面的方程組：
$$
i\hbar D_t \psi=(\frac{-\hbar^2}{2\mu}\nabla^2+V)\psi，
$$
其中 $\nabla^2$ 表示關於空間變數的 Laplacian operator (這個語意下沒有對時間變數做偏微分)，因此在這個例子中所對應的 $\hat{H}$ 自然是與時間獨立的。


特別地，計算中我們往往會對這些系統進行離散化，考慮算子 $\hat{H}$ 為 finite rank，透過適當的基底選取(或直接假設函數空間為有限維度)，我們有

$$
\hat{H}|\psi\rangle=A|\psi\rangle,A\in\mathbb{C}^{n\times n}。
$$

例如，上述的非相對論性單粒子系統而言， $\nabla^2$ 可以透過有限差分構造出離散版本的 Laplacian operator，而 $V$ 則可以表示為一個對角陣所構成的算子。

那麼對於任何一個 SEP 的解，
$$
Av=\lambda v，
$$
選擇 $|\psi(t)\rangle=e^{\frac{\lambda t}{\hbar i}}v$ 是一組可行解，對於物理學而言，如果 $\psi$ 獨立於時間變量，那麼得到的特徵值是狀態 $\psi$ 的能量。

### 後記
mathjax plugin裝不起來，只好先欠技術債XDD
```html
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
```
