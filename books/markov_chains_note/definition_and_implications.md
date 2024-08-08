---
title: "4.2.1.2 Definition and Implications"
---

## エルゴード性

$\mathscr{M}$ を状態空間 $S$ と遷移行列 $P$ をもつ有限マルコフモデルとする．[$\text{EXERCISE 4.2.1}$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/harmonic_functions#exercise-4.2.1.)で確認した通り，$\mathbb{R}^S$ 上の定数関数はすべて $P$-harmonic なのであった．

ここで，$\mathbb{R}^S$ 上の$P$-harmonic な関数が定数関数だけであるとき，$\mathscr{M}$ を**エルゴード的** (ergodic) であるという^[エルゴード性は時間平均がアンサンブル平均に一致する性質と説明されることが多いですが，それは次の $\S\ 4.2.1.3$ で扱います．]．

### Example 4.2.2.

$\varphi$ を $S$ 上の確率分布とする．任意の $x,y \in S$ について，遷移確率が $P(x,y) = \varphi(y)$ であるとき，来期の状態は今期の状態から独立なので，$P$ は IID なマルコフ連鎖を生成する．このとき，$P$ を遷移行列としてもつ有限マルコフモデル $\mathscr{M}$ はエルゴード的である．実際，$h \in \mathbb{R}^S$ が $P$-harmonic であるなら，任意の $x \in S$ について

$$
h(x) = Ph(x) = \sum_{y \in S} P(x,y)h(y) = \sum_{y \in S} \varphi(y)h(y) = \text{const.}
$$

であるので，どの $P$-harmonic 関数も定数関数である．したがって，$\mathscr{M}$ はエルゴード的である．

### Example 4.2.3.

![](/images/markov_chains_note/worker_transition_dynamics.png =250x)
*図 1.3：Worker transition dynamics
出所）Stachurski et al. (2024)*

図1.3のように，労働者が失業（状態 $1$）と就業（状態 $2$）の二つの状態間を遷移するとする．状態 $1$ にあるときは確率 $\alpha$ で雇用され，状態 $2$ にあるときは確率 $\beta$ で解雇される．この有限マルコフモデル $\mathscr{M}$ の状態空間と遷移行列は，次式で与えられる．

$$
S = \Set{1,2} \quad \text{and} \quad
P_w = 
\begin{pmatrix}1-\alpha & \alpha \\ \beta & 1-\beta \end{pmatrix}.
$$

このとき，$P$-harmonic 関数の条件 $P_wh = h$ は

$$
\begin{pmatrix}1-\alpha & \alpha \\ \beta & 1-\beta \end{pmatrix}
\begin{pmatrix}
h(1) \\ h(2)
\end{pmatrix}
=
\begin{pmatrix}
h(1) \\ h(2)
\end{pmatrix}
$$

と書ける．第１行は $(1-\alpha)h(1) + \alpha h(2) = h(1)$ より $\alpha h(1) = \alpha h(2)$ を得る．同様に，第２行から $\beta h(1) = \beta h(2)$．よって，$\mathscr{M}$ がエルゴード的であるための必要十分条件は，$\alpha>0$ または $\beta>0$ である．

### Example 4.2.4.

$\mathscr{M}$ を状態空間 $S$ と遷移行列 $P$ からなる有限マルコフモデルとする．[Example 4.2.1](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/harmonic_functions#example-4.2.1.) より，$S$ が二つの非空な吸収状態に分割されるときは，定数関数以外の $P$-harmonic 関数が存在するので $\mathscr{M}$ はエルゴード的でないことは明らかである．

![](/images/markov_chains_note/poverty_trap.png =250x)
*図 4.9：貧困の罠
出所）Stachurski et al. (2024)*

図4.9の貧困の罠モデルは，分割された二つの吸収状態を持つのでエルゴード的でない．

同様の理由で，図1.3の worker dynamics において $\alpha=\beta=0$ であるときは，遷移行列が単位行列に一致し，エルゴード性が破れる．

## エルゴード性の十分条件

以上の例から，有限マルコフモデル $\mathscr{M}$ のエルゴード性はどうやら有向グラフの連結性に依存しているようだという予測が立つ．次の命題はその予測を裏付けるものである．

:::message
$\textbf{Proposition 4.2.1.}$
$\mathscr{M}$ が[強連結](https://zenn.dev/nagayu71/articles/61e5f6c2cd55a0#%E9%9A%A3%E6%8E%A5%E8%A1%8C%E5%88%97%E3%81%A8%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%81%AE%E6%A7%8B%E9%80%A0)であれば，$\mathscr{M}$ はエルゴード的である．
:::

$\text{Proof.}$　$\mathscr{M}$ を状態空間 $S$ と遷移行列 $P$ からなる強連結な有限マルコフモデルとする．背理法で，定数関数でない $P$-harmonic な関数 $h \in \mathbb{R}^S$ が存在すると仮定し，$x \in S$ を $h$ の最大元，$m = h(x)$ を $h$ の最大値とする．このとき，$h(y) < m$ となる $y \in S$ が存在する．$\mathscr{M}$ の強連結性から $P^k(x,y) > 0$ となる $k \in \mathbb{N}$ が存在し，$h$ が $P$-harmonic なので $h = P^kh$ が成り立つ．したがって，

$$
\begin{align*}
m = h(x) = (P^kh)(x) 
&= \sum_{z\in S}P^k(x,z)h(z) \\
&= P^k(x,y)h(y) + \sum_{z\neq y}P^k(x,z)h(z) \\
&< P^k(x,y)m + \left[1 - P^k(x,y)\right]m \\
&= m
\end{align*}
$$

となり，$m<m$ という矛盾が生じる．したがって仮定が誤りで，すべての $P$-harmonic 関数 $h \in \mathbb{R}^S$ は定数関数である．よって，強連結な有限マルコフモデル $\mathscr{M}$ はエルゴード的である．$\square$

## EXERCISE 4.2.2.

$\text{EXERCISE 4.2.2.}$ エルゴード的だが強連結でない有限マルコフモデルの例を挙げよ．

:::details 解答例
$$
S = \Set{1,2,3} \quad \text{and} \quad
P = 
\begin{pmatrix}
1/2  & 1/2 & 0   \\
0    & 1/2 & 1/2 \\
0    & 1/2 & 1/2
\end{pmatrix}
$$

からなる有限マルコフモデル $\mathscr{M}$ は，エルゴード的だが強連結ではない．実際，

$$
h = Ph \iff
\begin{pmatrix}
h(1) \\ h(2) \\h(3)
\end{pmatrix}
=
\begin{pmatrix}
1/2  & 1/2 & 0   \\
0    & 1/2 & 1/2 \\
0    & 1/2 & 1/2
\end{pmatrix}
\begin{pmatrix}
h(1) \\ h(2) \\h(3)
\end{pmatrix}
$$

より，

$$
\begin{cases}
h(1) = h(2) \\
h(2) = h(3)
\end{cases}
$$

なので，$h(1) = h(2) = h(3) = c\quad (c\in\mathbb{R})$ を得る．よって，$\mathscr{M}$ はエルゴード的である．

しかし，状態 $2,3$ から状態 $1$ へ遷移することはできないので，$\mathscr{M}$ は強連結ではない．
:::