---
title: "4.1.3.1 Stationary Distributions"
---

## 4.1.3 Stationarity

このセクションでは，定常分布とその性質について議論する．以下の議論で確認するが，定常分布は周辺分布の時間発展における定常状態とみなすことができる．なお，後のセクションでエルゴード性について学ぶと，定常分布にもう一つの重要な解釈を与えることができる．

## 4.1.3.1  Stationary Distributions

### 不動点としての定常分布

$\S\ 1.3.1.3$ で学んだ通り，$P$が確率行列で$\psi \in \mathbb{R}_+^n$が$\psi\bm{1} = 1$かつ$\psi P = \psi$を満たす行ベクトルであるとき，$\psi$は確率行列$P$について**定常的** (stationary) であるという．

状態空間$S$と遷移行列$P$を持つ有限マルコフモデル$\mathscr{M}$を考える．上と同じことをマルコフ連鎖の表記で書くと，確率分布$\psi^* \in \mathscr{D}(S)$は，$\psi^* = \psi^* P$，すなわち

$$
\psi^*(y) = \sum_{x \in S} P(x,y)\psi^*(x) \quad \text{for all}\ y \in S
$$

が成り立つとき，有限マルコフモデル$\mathscr{M}$について定常的 (stationary) である．なお，$\psi^*$は分布を更新する写像$\psi \mapsto \psi P$（cf., 差分方程式[$(4.13)$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/updating_marginal_distributions#forward-equation-and-forward-operator)）の不動点(fixed point)として理解できる．

:::details cf) 不動点 (§6.1.1.6)
任意の集合$S$上の関数$G: S\to S$を**自己写像** (self-map) という．関数が自己写像であるときは，$G$による$x$の像を$G(x)$ではなく$Gx$と表記するのが一般的である．$S$上の自己写像$G$に対して，$Gx = x$となる$x \in S$を**不動点** (fixed point) という．

![](/images/markov_chains_note/fixed_points.png =350x)
*図 6.4：自己写像$G: x \mapsto 2.125/(1+x^{-4})$の不動点
出所）Stachurski et al. (2024)*

:::

したがって，$X_t \overset{d}{=} \psi^*$であるとき，任意の$j \in \mathbb{N}$に対して不動点の性質から$X_{t+j} \overset{d}{=} \psi^* P^j = \psi^* P^{j-1} = \cdots = \psi^* P =\psi^*$が成り立つ．すなわち，

$$
X_t \overset{d}{=} \psi^* \implies X_{t+j} \overset{d}{=} \psi^* \quad \text{for all}\ j \in \mathbb{N}.
$$

### Example 4.1.3.

![](/images/markov_chains_note/worker_transition_dynamics.png =250x)
*図 1.3：Worker transition dynamics
出所）Stachurski et al. (2024)*

図1.3のように失業者のうち$\alpha \in [0,1]$の割合が就業し，就業者のうち$\beta \in [0,1]$の割合が失業するとする．このとき労働者は$(4.14)$の遷移行列に従って，失業と就業の状態間を遷移する．

$$
P_w = 
\begin{pmatrix}1-\alpha & \alpha \\ \beta & 1-\beta \end{pmatrix} \tag{4.14}
$$

$\S\ 1.2.3.3$ で $\alpha+\beta>0 \implies \psi = \left(\beta/(\alpha+\beta),\alpha/(\alpha+\beta)\right)$ を示し，$\psi$が$P_w$の支配的な左固有ベクトルであることを確認した．$\rho(P_w) = 1$^[教科書では行列$A$のスペクトル半径を$r(A)$で表していますが，このノートでは表記を他の記事と統一するために$\rho(A)$を用いています．]より[ペロン＝フロベニウスの定理](https://zenn.dev/nagayu71/articles/dc49767d388f98#%E3%83%9A%E3%83%AD%E3%83%B3%EF%BC%9D%E3%83%95%E3%83%AD%E3%83%99%E3%83%8B%E3%82%A6%E3%82%B9%E3%81%AE%E5%AE%9A%E7%90%86)から，$P_w$の最大固有値が$1$であることが保証され，$\psi$が$P_w$の定常分布であることがわかる．したがって，労働者の状態についての分布が$\psi$で与えられ，かつ分布の更新が$\psi_{t+1} = \psi_t P_w$に従うのであれば，失業率は定数$\beta/(\alpha+\beta)$になる．

### Example 4.1.4.

![](/images/markov_chains_note/trajectory4-6.png =300x)
*図 4.6：$\psi_0=(0,0,1)$を初期値とする分布の軌跡
出所）Stachurski et al. (2024)*

![](/images/markov_chains_note/trajectory4-7.png =300x)
*図 4.7：$\psi_0=(0,1/2,1/2)$を初期値とする分布の軌跡
出所）Stachurski et al. (2024)*

[図4.6と図4.7](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/trajectories_in_the_long_run#%E5%88%86%E5%B8%83%E3%81%AE%E8%BB%8C%E8%B7%A1)で周辺分布列の極限を表す黒い点は，遷移行列[$P_a$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#%E9%81%B7%E7%A7%BB%E8%A1%8C%E5%88%97)の定常分布である．定常分布の求め方については $\S\ 4.1.3.4$ で議論する．

## EXXERCISE 4.1.4.

$\text{EXERCISE 4.1.4.}$ $\mathscr{M}$を状態空間$|S|=n$と遷移行列$P$を持つ有限マルコフモデルとする．$\psi \equiv (1/n, \ldots, 1/n)$を$S$上の一様分布とする．$P$が二重確率行列である時，そしてその時に限り$\psi$は$P$の定常分布であることを示せ．

:::details 二重確率行列
$$
P\bm{1} = \bm{1},\quad P^\top\bm{1} = \bm{1}
$$

と行和，列和がすべて$1$となる行列$P\in\mathbb{M}^{n\times n}$を**二重確率行列** (doubly stochastic matrix) という．
:::

:::details 解答例
($\implies$)

遷移行列$P$が$P\bm{1} = \bm{1}$かつ$P^\top\bm{1} = \bm{1}$を満たすとする．$P^\top\bm{1} = \bm{1}$の両辺を$n$で割れば，$P^\top\psi^\top = \psi^\top$を得る．両辺の転置をとると，$\psi P = \psi$より$\psi$は定常分布である．

($\impliedby$)

$\psi$が$P$の定常分布なので，$\psi = \psi P$が成り立つ．両辺の転置をとって，

$$
P^\top \psi^\top = \psi^\top \iff P^\top \frac{1}{n}\bm{1} = \frac{1}{n}\bm{1} \iff P^\top\bm{1} = \bm{1}
$$

を得る．また，$P$は確率行列なので，$P\bm{1} = \bm{1}$が成り立つ．すなわち，$P$は二重確率行列である．
:::

図4.6と図4.7では，どの分布の軌跡も定常分布に収束している．しかし，すべての定常分布がこのアトラクター (attractor) としての性質を持つわけではない．一般に，定常分布は無数に存在し，次の問題はそのことを確かめるものである．

## EXXERCISE 4.1.5.

$\text{EXERCISE 4.1.5.}$ $\mathscr{M}=(S,E,p)$を有限マルコフモデルとする．ただし，$x=y \iff (x,y) \in E$である．この設定の下で導かれる[重み関数](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/markov_models#%E5%AE%9A%E7%BE%A9)と，それに対応する遷移行列を説明せよ．また，任意の$\psi \in \mathscr{D}(G)$は$\mathscr{M}$の定常分布であることを示せ．

:::details 解答例
重み関数は

$$
P(x,y) = \begin{cases} 1 \qquad (x=y) \\ 0 \qquad (\text{otherwise}) \end{cases}
$$

であり，これに対応する遷移行列は単位行列$I$である．すなわち，$P = I$が成り立つ．また，任意の$\psi \in \mathscr{D}(G)$に対して，単位行列の定義から$\psi P =\psi I = \psi$より，$\psi$は$\mathscr{M}$の定常分布である．
:::