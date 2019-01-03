---
title: Quick Note on the Continued Fraction
date: 2018-11-24 03:07:49
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

本文將簡述連分數，有些內容之後視情況將斟酌補充。

![](https://i.imgur.com/Tht0evZ.png)

連分數在數學上是一個有趣的主題，小時候大家玩過摺紙遊戲，把長方形的紙片等角對折，剪去以折線為對角的正方形，然後不斷重複做一樣的事情之後，把同樣大小的正方形蒐集起來，這時候正方形由大到小的個數就構成了一個連分數。


### Definition

考慮一串整數的序列，
$$
a_0,a_1,a_2,...
$$
其中 $a_i\geq 0,\forall i>0$。
我們定義有限項連分數，
$$
s_n=[a_0;a_1,a_2,...,a_n]:=a_0+\frac{1}{a_1+\frac{1}{a_2+\frac{...}{a_n}}}。
$$
如果 $s_n$ 收斂，那麼定義，
$$
[a_0;a_1,a_2,...]:=\lim_{i\rightarrow\infty}s_n。
$$

### 如何計算

**從連分數算出質因子表達式**

定義
$$
\frac{p_i}{q_i}=[a_0;a_1,...a_i]，
$$
其中 $p_i, q_i$ 互質，那麼我們有遞推關係
$$
p_n=a_n\cdot p_{n-1}+p_{n-2}\\\
q_n=a_n\cdot q_{n-1}+q_{n-2}
$$


**從實數構造出連分數表達式**

任何實數 $r\in\mathbb{R}$ 都可以被連分數序列表達，
$$
r = [a_0;a_1,...]。
$$
並且考慮
$$
r_0 = r\\\
r_n=\frac{1}{r_{n-1}-a_{n-1}}，
$$
那麼我們有
$$
a_n=\lfloor r_n\rfloor。
$$


**表達的唯一性**

考慮
$$
s = [a_0;a_1,...,a_n+1] = [a_0;a_1,...,a_n,1]，
$$
除去這種情況外，連分數的表達是唯一的。

### 有理逼近

考慮我們想要逼近區間 $[l,r),r=l+1\in\mathbb{Z}$ 之間的某個數字 $x$，模仿二分逼近法，我們可以先定義一個"中值函數"
$$
mid(\frac{a}{b},\frac{c}{d})=\frac{a+c}{b+d}。
$$
如果
$$
\frac{a}{b}<\frac{c}{d}，
$$
那麼顯然有
$$
\frac{a}{b}<mid(\frac{a}{b},\frac{c}{d})<\frac{c}{d}。
$$
可以透過下面迭代使解收斂至 $x$
$$
m_i = mid(l_i,r_i)\\\
\pmatrix{l_0\\\r_0} = \pmatrix{l\\\r}\\\
\pmatrix{l_{i+1}\\\r_{i+1}} = \pmatrix{m_i\\\r_i},m_i<x\\\
\pmatrix{l_{i+1}\\\r_{i+1}} = \pmatrix{l_i\\\m_i},x<m_i
$$

仔細觀察 $mid$ 函數，其實正對應到連分數的迭代式，
如果
$$
l_i = [a_0;a_1,a_2,...,a_{i-2}]\\\
r_i = [a_0;a_1,a_2,...,a_{i-1}]
$$
那麼有
$$
mid(l_i, r_i) = [a_0;a_1,a_2,...,a_{i-1},1] = [a_0;a_1,a_2,...,a_{i-1}+1]
$$
可以發現對於數列這樣一個迭代的數列中類似於連分數，結論上兩種序列最終都會收斂至 $x$ (需要證明)，但連分數的收斂速度更快。

### Optimal Diophantine Approximation

事實證明，連分數序列不只會收斂至指定的實數，這個序列是某種意義下的最佳逼近。

對於 $x\in\mathbb{R}$ 考慮 $N\in\mathbb{N}$ ，那麼對於所有質因子表達，
$$
\frac{p}{q}, q<N
$$
總存在
$$
\frac{p_n}{q_n}=[a_0;a_1,a_2,...,a_n],\\\
|\frac{p_n}{q_n}-x|\leq|\frac{p}{q}-x|。
$$

此外，由於連分數的分子分母項都是指數成長(從遞推式可以看出)，計算上它是十分有效率的，可以說這是一個相當好的逼近方法。

### 後記
然後我就把手邊的 double A4拿去做實驗XD，發現它的長寬比大概是24:17
![](https://i.imgur.com/LOJPbkz.png)