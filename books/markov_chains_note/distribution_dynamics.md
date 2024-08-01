---
title: "4.1.2 Distribution Dynamics"
---

# 周辺分布

$\mathscr{M}$を状態空間$S$と遷移行列$P$を持つ有限マルコフモデルとする．確率変数列$(X_t)$を[$P$-Markov](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/markov_chains#%E3%83%9E%E3%83%AB%E3%82%B3%E3%83%95%E9%80%A3%E9%8E%96%E3%81%AE%E5%AE%9A%E7%BE%A9)とし，任意の$t\geq0$に対して$\psi_t \in$ [$\mathscr{D}(S)$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#%E9%81%B7%E7%A7%BB%E8%A1%8C%E5%88%97%E3%81%A8%E5%88%86%E5%B8%83%E3%81%AE%E9%9B%86%E5%90%88-(%C2%A71.3.1.1))を次式で定義する：

$$
\psi_t \coloneqq \mathbb{P}\{X_t = \cdot\} = ~\text{the distribution of }X_t.
$$

ベクトル$\psi_t$を$X_t$の**周辺分布** (marginal distribution) と言う．

状態の列$(X_t)$がランダムである一方で，その分布列$(\psi_t)$は**決定論的なダイナミクス**に従う．
