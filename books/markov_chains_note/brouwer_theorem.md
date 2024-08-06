---
title: "4.1.3.3 Brouwer’s Theorem"
---

## ブラウワーの不動点定理

[$\text{Theorem 4.1.1}$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/existence_and_uniqueness#%E5%AE%9A%E5%B8%B8%E7%8A%B6%E6%85%8B%E3%81%AE%E5%AD%98%E5%9C%A8%E3%81%A8%E4%B8%80%E6%84%8F%E6%80%A7)の定常分布の存在は，かの有名な L.E.J. Brouwer (1881-1966) の不動点定理を使って証明することができる．

:::message
$\textbf{Theorem 4.1.2}$ $\text{(Brouwer).}$
$C$が$\mathbb{R}^n$上のコンパクト凸部分集合であり，$G$が$C$への連続な自己写像であるならば，$G$は$C$上に少なくとも一つの[不動点](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/stationary_distributions#%E4%B8%8D%E5%8B%95%E7%82%B9%E3%81%A8%E3%81%97%E3%81%A6%E3%81%AE%E5%AE%9A%E5%B8%B8%E5%88%86%E5%B8%83)を持つ．
:::

## EXERCISE 4.1.6.

$\text{EXERCISE 4.1.6.}$ 中間値の定理を用いて，$C=[0,1]$である場合のブラウワーの不動点定理を証明せよ．

:::details 解答例
$G:[0,1] \to [0,1]$を連続な自己写像とし，$F(x) \equiv x - G(x)$を定義する．$G$の不動点の存在を示すには，$F(x)=0$となる$x$の存在を示せば良い．$F(0)=-G(0) \leq 0$，$F(1)= 1-G(1) \geq 0$であり，$F$は連続なので，中間値の定理から$F(x)=0$を満たす$x$が存在する．このとき$F(x)=x-G(x)=0$なので，$x=G(x)$が成り立ち，$x$は$G$の不動点である．
:::

![](/images/markov_chains_note/fixed_points.png =350x)
*図 6.4：自己写像$G: x \mapsto 2.125/(1+x^{-4})$の不動点
出所）Stachurski et al. (2024)*

ブラウワーの不動点定理の長所は，その条件がかなり弱いことにある．他方で，不動点の存在を保証するだけで，一意性や安定性には言及できないという短所もある．図6.4は，ブラウワーの不動点定理の条件の下で，不動点が複数存在しうる例を示している．

## EXERCISE 4.1.7.

$\text{EXERCISE 4.1.7.}$ ブラウワーの不動点定理を用いて，[$\text{Theorem 4.1.1}$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/existence_and_uniqueness#%E5%AE%9A%E5%B8%B8%E7%8A%B6%E6%85%8B%E3%81%AE%E5%AD%98%E5%9C%A8%E3%81%A8%E4%B8%80%E6%84%8F%E6%80%A7)の定常分布の存在に関する主張が正しいことを示せ．

:::details 解答例
$\mathscr{D}(S)$は有限の集合$S$に対して

$$
\mathscr{D}(S) \coloneqq \left\{ \varphi \in \mathbb{R}_+^{S} ~:~ \sum_{x \in S} \varphi (x) = 1  \right\}
$$

と定義されるので，$\mathbb{R}^{|S|}$上のコンパクトな部分集合である．$\psi_1, \psi_2 \in \mathscr{D}(S)$と$\lambda \in (0,1)$を任意に選び，凸結合$\lambda\psi_1 + (1-\lambda)\psi_2$を作る．いま$\sum_x\psi_1(x) = \sum_x\psi_2(x) =1$より

$$
\begin{align}
\sum_{x\in S}\left[\lambda\psi_1 + (1-\lambda)\psi_2\right](x) &= \sum_{x\in S}\left[\lambda\psi_1(x) + (1-\lambda)\psi_2(x)\right] \\
&= \lambda\sum_{x\in S}\psi_1(x) + (1-\lambda)\sum_{x\in S}\psi_2(x) \\
&= \lambda + (1-\lambda) \\
&= 1
\end{align}
$$

が成り立つため，$\mathscr{D}(S)$は凸集合である．さらに，行列$P$は有限次元線形写像$P:\mathscr{D}(S) \to \mathscr{D}(S)$の表現行列なので，写像$P$は連続である．ブラウワーの不動点定理より$P$は$\psi^* = P(\psi^*)$なる不動点を持ち，$\psi^*$は定常分布に他ならない．
:::
