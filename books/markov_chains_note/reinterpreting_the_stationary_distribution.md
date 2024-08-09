---
title: "4.2.1.4 Reinterpreting the Stationary Distribution"
---

## 平均滞在時間分布としての定常分布

> 後のセクションでエルゴード性について学ぶと，定常分布にもう一つの重要な解釈を与えることができる．

[$\S 4.1.3.1$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/stationary_distributions#4.1.3-stationarity) で予告した，エルゴード性が定常分布に新たな解釈を与えることを見ていこう．

$\mathscr{M}$ を状態空間 $S$ と遷移行列 $P$ からなるエルゴード的な有限マルコフモデルとする．$(X_t)$ を [$P$-Markov](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/markov_chains#%E3%83%9E%E3%83%AB%E3%82%B3%E3%83%95%E9%80%A3%E9%8E%96%E3%81%AE%E5%AE%9A%E7%BE%A9) とし，

$$
\hat{\psi}_k(y) \coloneqq \frac{1}{k}\sum_{t=0}^{k-1} \bm{1}\{X_t = y\} \qquad (y \in S)
$$

のように $\S 4.2.1.3$ で任意にとっていた関数 $h \in \mathbb{R}^S$ を指示関数 $h(x) = \bm{1}\{x=y\}$ で定める．すると，$\hat{\psi}_k(y)$ はマルコフ連鎖 $(X_t)$ が $t = 0,1,\ldots, k-1$ の間に状態 $y$ に滞在した時間の割合を表す．

エルゴード性の下で $\text{Theorem 4.2.2}$ の $(4.18)$ を用いると次式を得る．

$$
\hat{\psi}_k(y) \to \sum_{x \in S} \bm{1}\{x=y\}\psi^*(x) = \psi^*(y). \tag{4.19}
$$

つまり，エルゴード性の下では，

$$
\psi^*(y) \approx \text{マルコフ連鎖が平均的に状態 } y \text{ に滞在する時間の割合} \tag{4.20}
$$

であり，定常分布 $\psi^*$ はマルコフ連鎖の平均滞在時間分布と一致する．

![](/images/markov_chains_note/convergence_of_the_empirical_distribution.png =500x)
*図 4.10：経験分布 $\hat{\psi}_k$ の定常分布 $\psi^*$ への収束
出所）Stachurski et al. (2024)*

図4.10は遷移行列 [$P_B$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#benhabib-et-al.-(2019)%EF%BC%9A%E7%A4%BE%E4%BC%9A%E9%9A%8E%E7%B4%9A%E3%83%80%E3%82%A4%E3%83%8A%E3%83%9F%E3%82%AF%E3%82%B9%E3%81%AE%E7%A0%94%E7%A9%B6) から生成されたマルコフ連鎖 $(X_t)$ の各イテレーション（$k = 10, 100, 1000, 10000$）ごとに算出した滞在時間分布 $\hat{\psi}_k$ と定常分布 $\psi^*$ を比較したものである．

図4.10から $\text{Theorem 4.2.2}$ の $(4.18)$ が示す通り，$k \to \infty$ になるにつれて，経験分布が定常分布に収束する様子がわかる．