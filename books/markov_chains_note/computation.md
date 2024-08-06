---
title: "4.1.3.4 Computation"
---

## 定常分布の計算

定常分布をどのように求めれば良いのだろうか．[定常性の定義](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/stationary_distributions#4.1.3.1-stationary-distributions)から$\psi^* P = \psi^*$という有限の（$n$本の）連立１次方程式を直接解けば良い気もするが，それだと問題が生じる．$\psi^*=0$という自明な解は$\psi^* \in \mathscr{D}(S)$を満たさないからである．

そこで，$\psi^* \in \mathscr{D}(S)$を満たすように制約をつけた次の問題を考える．

## EXERCISE 4.1.8.

$|S| = n$を仮定し，要素がすべて$1$の行ベクトルと$n\times n$正方行列を次で定める．

$$
\bm{1}_n \coloneqq (1,\ldots,1), \quad \bm{1}_{n\times n} \coloneqq \begin{pmatrix} 1 & \cdots & 1 \\ \vdots & \ddots & \vdots \\ 1 & \cdots & 1\end{pmatrix}
$$

$\psi(I-P) = \bm{0}$の時，そしてその時に限り行ベクトル$\psi \in \mathscr{D}(S)$は定常分布であることに注意しよう．

$\text{EXERCISE 4.1.8.}$ 線形システム（連立１次方程式）

$$
\bm{1}_n = \psi(I - P + \bm{1}_{n\times n}) \tag{4.15}
$$

を考える．次の$\text{(i)}$, $\text{(ii)}$を示せ．

$\text{(i)}$ $(4.15)$のどの解も$\mathscr{D}(S)$に含まれる
$\text{(ii)}$ $\psi$は$P$の定常分布である $\iff$ $\psi$は$(4.15)$を満たす

:::details 解答例
$\text{(i)}$
$(4.15)$の両辺に右から$\bm{1}$をかけると，

$$
\begin{align*}
    \bm{1}_n\bm{1} = \psi(I - P + \bm{1}_{n\times n})\bm{1} &\implies n = \psi(\bm{1} - P\bm{1} + \bm{1}_{n\times n}\bm{1}) \\
    &\implies n = \psi\bm{1}_{n\times n}\bm{1} \\
    &\implies n = \psi(n\bm{1}) \\
    &\implies 1 = \psi\bm{1}.
  \end{align*}
$$

解$\psi$は和が$1$の非負のベクトルなので，$\psi \in \mathscr{D}(S)$を満たす．

<br>

$\text{(ii)}$
$\psi$が$P$の定常分布であるとき，

$$
\begin{align*}
    \psi = \psi P &\iff \psi + \bm{1}_n = \psi P + \bm{1}_n \\
    &\iff \psi - \psi P + \bm{1}_n = \bm{1}_n \\
    &\iff \psi(I - P + \bm{1}_{n\times n}) = \bm{1}_n.
  \end{align*}
$$

:::

## EXERCISE 4.1.9.

$(4.15)$を解けば，定常分布が一意である限り，どのような状況下でも定常分布を得る．これが成り立たない場合は問題が生じる．

$\text{EXERCISE 4.1.9.}$ $P$が確率行列であるならば，行列$(I - P + \bm{1}_{n\times n})$は常に正則であるという主張に対する反例を挙げよ．

:::details 解答例
$P=I$は確率行列だが，$(I - P + \bm{1}_{n\times n}) = \bm{1}_{n\times n}$は$\det(\bm{1}_{n\times n}) = 0$より正則でない．
:::