---
title: "4.1.3.2 Existence and Uniqueness"
---

## 定常状態の存在と一意性

[ペロン＝フロベニウスの定理](https://zenn.dev/nagayu71/articles/dc49767d388f98#%E3%83%9A%E3%83%AD%E3%83%B3%EF%BC%9D%E3%83%95%E3%83%AD%E3%83%99%E3%83%8B%E3%82%A6%E3%82%B9%E3%81%AE%E5%AE%9A%E7%90%86)から，直ちに次の結果を得る．

:::message
$\textbf{Theorem 4.1.1}$ $\text{(Existence and Uniqueness of Stationary Distributions).}$
どんな有限マルコフモデル$\mathscr{M}=(S,E,p)$も，少なくとも一つの定常分布$\psi^* \in \mathscr{D}(S)$を持つ．さらに，有向グラフ$(S,E)$が[強連結](https://zenn.dev/nagayu71/articles/61e5f6c2cd55a0#%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%81%AE%E6%A7%8B%E9%80%A0%E3%82%92%E8%A1%A8%E3%81%99%E7%94%A8%E8%AA%9E)であるとき，$\psi^*$は$S$上の一意かつ$\psi^* \gg \bm{0}$ (everywhere positive)な定常分布である．
:::

$\text{Proof.}$　$\mathscr{M}$を有限マルコフモデルとする．その隣接行列$P$は確率行列なので，$\S1.3.1.3$ の$\text{Exercise 1.3.7}$より定常分布の存在が示される．また，$\text{Theorem 1.4.3}$より$\mathscr{M}$の強連結性と$P$が既約であることは同値である．$P$が既約であるとき，ペロン＝フロベニウスの定理から定常分布の一意性と，どの状態確率も正であることが保証される．$\square$

:::details 補足（Exercise 1.3.7；Theorem 1.4.3）

$\text{EXERCISE 1.3.7.}$
$P, Q$を$n \times n$の確率行列であるとする．以下の事実〈該当箇所のみ記載〉を示せ．
> $\text{(iii)}$ $\psi\bm{1} = 1$かつ$\psi P = \psi$であるような行ベクトル$\psi \in \mathbb{R}^n_+$が存在する．

$\text{Proof.}$ $\psi P = \psi$を満たす$\psi \in \mathbb{R}^n_+$を考える．この成分に注目すると，

$$
\psi P = \psi \iff \left(\sum_i\psi_iP_{i1}, \ldots, \sum_i\psi_iP_{in} \right) = (\psi_1, \ldots, \psi_n).
$$

すなわち，すべての$j=1,\ldots,n$について$\sum_i\psi_iP_{ij} = \psi_j$が成り立つ．両辺で$j$についての和をとると，

$$
\sum_j\sum_i\psi_iP_{ij} = \sum_j\psi_j \implies \sum_i\psi_i\left(\sum_jP_{ij}\right) = \sum_j\psi_j \implies \sum_i\psi_i = \sum_j\psi_j.
$$

ここで，$\sum_i\psi_i = 1$と規格化すれば，$\psi\bm{1} = 1$となるので，$\psi\bm{1} = 1$かつ$\psi P = \psi$であるような行ベクトル$\psi$が存在する．$\square$

<br>

$\textbf{Theorem 1.4.3}$
$\mathscr{G}$を重み付き有向グラフとする．以下の二つの主張は同値である．

- $\mathscr{G}$は強連結(strongly connected)である．
- $\mathscr{G}$の隣接行列は既約(irreducible)である．

https://zenn.dev/nagayu71/articles/61e5f6c2cd55a0#%E9%9A%A3%E6%8E%A5%E8%A1%8C%E5%88%97%E3%81%A8%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%81%AE%E6%A7%8B%E9%80%A0
:::

$\text{Theorem 4.1.1}$の一意性に関する主張の背後にあるアイデアは次の通りである．強連結であるが相異なる定常分布$\psi^*, \psi^{**} \in \mathscr{D}(s)$を持つモデル$\mathscr{M}$を仮定する．このとき，$\psi^*$を初期条件とする$P$-Markovは常に周辺分布$\psi^*$を持つことになる（$\psi^{**}$についても同様）．

すると，異なる初期条件が，長期において異なる結果をもたらしていることになるが，この事実は次の意味で強連結性に反する．すなわち，$P$-Markovな列 $(X_t)\sim\psi^*$と$(Y_t)\sim\psi^{**}$のどちらも，状態空間$S$全体を移動でき，一度ある状態に到達すると過去の軌跡を忘れるため（マルコフ性），最終的に初期条件は無関係になるはずである^[厳密には，初期条件が無関係になるという主張はミスリーディングである．強連結性が成り立っていても，初期条件は次の意味で長期におけるふるまいを決定づけることがある．すなわち，周期的 (periodic) なマルコフモデルは状態空間全体を移動できるが，その周期性により初期条件に依存する特定の時間にしか訪れることができない状態がある．周期性を除外すると，$\text{Theorem 4.1.1}$よりも強い結論を得ることができるが，このトピックは $\S\ 4.2.2$ で詳しく扱う．]．よって，仮定が誤りで，強連結性は定常分布の一意性を導く．
