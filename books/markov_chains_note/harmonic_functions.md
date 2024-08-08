---
title: "4.2.1.1 Harmonic Functions"
---

## 4.2.1 Ergodicity

マルコフ連鎖における重要でかつ興味深いトピックに，**エルゴード性** (ergodicity) という性質がある．エルゴード性は，IIDな確率変数列に成り立つ大数の法則を，IIDが限られた意味でのみ成り立つより一般的なセッティングに拡張したものとして理解できる．

## 4.2.1.1 Harmonic Functions

$\mathscr{M}$ を状態空間 $S$ と遷移行列 $P$ をもつ有限マルコフモデルとする．[実数値関数](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#%E9%81%B7%E7%A7%BB%E8%A1%8C%E5%88%97%E3%81%A8%E5%88%86%E5%B8%83%E3%81%AE%E9%9B%86%E5%90%88-(%C2%A71.3.1.1)) $h \in \mathbb{R}^S$ に対して関数 $Ph(x)$ を次式で定める．

$$
Ph(x) \coloneqq \sum_{y \in S} P(x,y)h(y) \qquad (x \in S) \tag{4.16}
$$

関数 $h$ を $\mathbb{R}^{|S|}$ 上の列ベクトルとして理解すると，$Ph(x)$ とはベクトル $Ph$ の要素 $x$ に他ならない．写像 $P: \mathbb{R}^S \ni h \mapsto Ph \in \mathbb{R}^S$ はしばしば**条件付き期待値演算子** (conditional expectation operator) と呼ばれる．というのも，$P(x,y) = \mathbb{P}\{X_{t+1}=y \mid X_t=x\}$ であったことから，

$$
\sum_{y \in S} P(x,y)h(y) = \sum_{y \in S} \mathbb{P}\{X_{t+1}=y \mid X_t=x\} h(y) = \mathbb{E}\left[h(X_{t+1}) \mid X_t=x\right]
$$

と $Ph(x)$ が $x$ を所与としたときの $h(\cdot)$ の条件付き期待値を表すからである．

関数 $h \in \mathbb{R}^S$ が $Ph(x) = h(x)\ \forall x \in S$ を満たすとき，$h$ は $P$-$\textbf{harmonic}$ であるという．したがって，$P$-harmonic 関数は条件付き期待値演算子 $h \mapsto Ph$ の[不動点](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/stationary_distributions#%E4%B8%8D%E5%8B%95%E7%82%B9%E3%81%A8%E3%81%97%E3%81%A6%E3%81%AE%E5%AE%9A%E5%B8%B8%E5%88%86%E5%B8%83)である．

関数 $h$ が $P$-harmonic で $(X_t)$ が [$P$-Markov](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/markov_chains#%E3%83%9E%E3%83%AB%E3%82%B3%E3%83%95%E9%80%A3%E9%8E%96%E3%81%AE%E5%AE%9A%E7%BE%A9)であるとき，

$$
\mathbb{E}\left[h(X_{t+1}) \mid X_t\right] = (Ph)(X_t) = h(X_t) \tag{4.17}
$$

が成り立つ．$(4.17)$ が表す，現在の状態を所与としたときの来期の期待値が現在の値に一致するという性質をもった確率過程 $(h(X_t))$ のことを**マルチンゲール** (martingale) という．

### Example 4.2.1.

$\mathscr{M}$ を状態空間 $S$ と遷移行列 $P$ からなる有限マルコフモデルとする．$A \subset S$ と $A^c \coloneqq S \setminus A$ がともに $\mathscr{M}$ の吸収状態であるとき，$\bm{1}_A$ と $\bm{1}_{A^c}$ はどちらも $P$-harmonic な関数である．実際，[$\text{Exercise 4.1.1}$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#exercise-4.1.1.)の結果から次式が成り立つ．

$$
(P\bm{1}_A)(x) = \sum_{y \in S}P(x,y)\bm{1}_A(y) = \sum_{y \in A}P(x,y) =
\begin{cases}
1 \quad \text{if } x \in A, \\
0 \quad \text{if } x \in A^c
\end{cases}
= \bm{1}_A(x),
$$

$$
(P\bm{1}_{A^c})(x) = \sum_{y \in S}P(x,y)\bm{1}_{A^c}(y) = \sum_{y \in A^c}P(x,y) =
\begin{cases}
1 \quad \text{if } x \in A^c, \\
0 \quad \text{if } x \in A
\end{cases}
= \bm{1}_{A^c}(x).
$$

## EXERCISE 4.2.1.

$\text{EXERCISE 4.2.1.}$ $\mathscr{M}$ を状態空間 $S$ と遷移行列 $P$ をもつ有限マルコフモデルとする．$\mathbb{R}^S$ 上の定数関数はすべて $P$-harmonic であることを示せ．

:::details 解答例
$Ph(x) = h(x)\ \forall x \in S$ が成り立つことを示す．$h \in \mathbb{R}^S$を定数関数とする．このとき，定数 $c \in \mathbb{R}$ を用いると

$$
h(x) = c \quad \forall x \in S
$$

である．任意の $x \in S$ に対して，

$$
Ph(x) = \sum_{y \in S} P(x,y)h(y) = c\sum_{y \in S} P(x,y) = c = h(x)
$$

が成り立つので，$\mathbb{R}^S$ 上の定数関数 $h(x) = c$ は $P$-harmonic である．
:::