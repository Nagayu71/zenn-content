---
title: "4.1.1.4 Higher Order Transition Matrices"
---

# 遷移行列のべき乗

状態空間$S$と遷移行列$P$を持つ有限マルコフモデル$\mathscr{M}$を考え，$(P^k)_{k \in \N}$を$P_{k+1} = PP^k ~ \forall ~ k$によって定義する．ただし，$P^0 = I$とする．行列$P^k$は$P$の$k$乗であり，行列の積$P^{k+1} = PP^k$を成分で表記すると，次式を得る．

$$
P^{k+1}(x,y) \coloneqq \sum_z P(x,z)P^k(z,y) \qquad (x,y \in S,~ k \in \N). \tag{4.9}
$$

## 【復習】行列積の演算規則

正方行列$A$に対して，$\left(A^k\right)_{ij}$ を $A^k$ の $(i,j)$ 成分とし，$\left(A^k\right)_{ij} = a_{ij}^k$ と書く．積の演算規則から次式が成り立つ．

$$
\left(A^{s+t}\right)_{ij} = \left(A^sA^t\right)_{ij} 
= \sum_\ell \left(A^s\right)_{i\ell} \left(A^t\right)_{\ell j} 
= \sum_\ell a_{i\ell}^s a_{\ell j}^t. \tag{1.27}
$$

# EXERCISE 4.1.3.

$\text{EXERCISE 4.1.3.}$ （$P$が$S$上の確率行列であるとき）任意の$k \in \N$に対して$P^k$も確率行列であることを示せ．

:::details 解答例
任意の$k \in \N$を取る．$P$は確率行列なので$P\bm{1} = \bm{1}$が成立する．このとき，

$$
P^k\bm{1} = P^{k-1}(P\bm{1}) = P^{k-1}\bm{1} = \cdots = P\bm{1} = \bm{1}.
$$
よって，$P^k$は確率行列である．
:::

# $k$ステップ遷移行列

確率行列$P^k$は，**$k$ステップ遷移行列** ($k$-step transition matrix) と呼ばれる．$P^k$に対して，確率変数列$(X_t)$が$P$-Markovであれば，任意の$t, k \in \N$と$x, y \in S$について次式が成り立つ．

$$
P^k(x,y) = \mathbb{P}\{X_{t+k} = y | X_t = x\}. \tag{4.10}
$$

つまり，$k$ステップ遷移行列$P^k$は$P$-Markovな列$(X_t)$に対して，$k$ステップの遷移確率を与えるものである．

:::details (4.10)の証明
帰納法で示す．$t \in \N$と$x, y \in S$を任意に取って固定する．$k = 1$のときは定義より成立．$k = n$のとき$(4.10)$が成立すると仮定して$k = n+1$を考える．全確率の法則 (the law of total probability) より

$$
\begin{align*}
\mathbb{P}\{X_{t+n+1} = y | X_t = x\} 
&= \sum_z \mathbb{P}\{X_{t+n+1} = y | X_{t+n} = z\}\mathbb{P}\{X_{t+n} = z | X_{t} = x\} \\
&= \sum_z P(z,y)P^n(x,z) \qquad (\text{When } k=n \text{, (4.10) holds.})\\ 
&= P^{n+1}(x,y).\qquad (\text{matrix multiplication})
\end{align*}
$$

$k =n+1$でも成り立つので，$(4.10)$が成り立つ．
:::

## チャップマン＝コルモゴロフ方程式

高次のマルコフ行列に対して，次の便利な等式が成り立つ．任意の$j, k \in \N$について，

$$
P^{j+k}(x,y) = \sum_z P^k(x,z)P^j(z,y). \qquad ((x,y) \in S \times S) \tag{4.11}
$$

この等式を**チャップマン＝コルモゴロフ方程式** (Chapman-Kolmogorov equation) と言う．
これまで登場した等式とチャップマン＝コルモゴロフ方程式の関係性は次の通りである．

- $(4.9)$は$(4.11)$の特殊ケース（$k=1$と固定し，$j$を$k$に置き換える）
- $(4.11)$は行列積の演算規則$(1.27)$の特殊ケース

実際に行っていることは行列積の演算だが，チャップマン＝コルモゴロフ方程式が確率に関する便利な式であることを確認する．$X_0=x$と$y\in S$を所与とすると，全確率の法則から条件付き確率は

$$
\begin{align*}
\mathbb{P}\{X_{j+k}=y | X_0=x\} 
&= \sum_z \mathbb{P}\{X_{j+k} = y | X_0=x, X_k = z\}\mathbb{P}\{X_k = z | X_0 = x\} \\
&= \sum_z \mathbb{P}\{X_{j+k} = y | X_k = z\}\mathbb{P}\{X_k = z | X_0 = x\} \\
&= \sum_z P^j(z,y)P^k(x,z) \\
&= P^{j+k}(x,y). \\
&\left(=\mathbb{P}\{X_{t+j+k}=y | X_t=x\}\right)
\end{align*}
$$

以上より与えられた初期条件のもとで，任意のステップにおける条件付き確率が，チャップマン＝コルモゴロフ方程式に帰着することが示された．