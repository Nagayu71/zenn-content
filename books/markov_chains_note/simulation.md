---
title: "4.1.1.3 Simulation"
---

# 【復習】マルコフ連鎖を生成するアルゴリズム

- 確率行列$P$と初期条件$\psi_0 \in$ [$\mathscr{D}(S)$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#%E9%81%B7%E7%A7%BB%E8%A1%8C%E5%88%97%E3%81%A8%E5%88%86%E5%B8%83%E3%81%AE%E9%9B%86%E5%90%88-(%C2%A71.3.1.1))を用意
- $\textbf{Algorithm 3}$に従って列$(X_t)$を生成
- 得られた列が，$\psi_0$を初期条件とする$P$-Markovである

![](/images/markov_chains_note/algorithm3.png =550x)
*出所）Stachurski et al. (2024)*

# アルゴリズムから確率差分方程式へ

数値計算と理論の双方にとって，$\textbf{Algorithm3}$を確率変数列$(X_t)_{t \geq 0}$の時間発展を記述する確率差分方程式に翻訳できると便利である．ここでは，**逆変換法** (inverse transform sampling) を用いた方法を見ていく．

### Step 1. 累積分布関数の定義

状態空間を$S=\Set{1,\ldots,n}$とし，遷移行列を$P$とする．各$i,j \in S$について，$q(i,j)$を次式で再帰的に定義する．

$$
q(i,j) \coloneqq q(i,j-1) + P(i,j) \quad \text{with } q(i,0)=0.
$$

$q(i,j)$は以下のように変形できるので，

$$
\begin{align*}
q(i,j) &= q(i,0) + P(i,1) + P(i,2) + \cdots + P(i,j) \\
&= \sum_{k=1}^j P(i,k) \\
&= \Pr(J \leqslant j |i)\\
\end{align*}
$$

状態$i$を所与とした$j$に関する累積分布関数として理解できる．

### Step 2. 来期の状態を記録する関数を定義

一様確率変数の実現値$u \in (0,1)$が，$q(i,\cdot)$のどの区間にヒットしたかを記録する関数を設定する．

$$
F(i,u) \coloneqq \sum_{j=1}^n j \bm{1}\{q(i,j-1) < u \leqslant q(i,j)\} \qquad (i \in S,\ u \in (0,1)).
$$
この$F(i,u)$が今期の状態が$i$であるときの来期の状態を（一様乱数から）決定する関数である．

### Step 3. 差分方程式の構築

$U(0,1)$を$(0,1)$上の一様分布とすると，確率変数列を与える差分方程式を得る．

$$
X_{t+1} = F(X_t, U_{t+1}) \quad \text{where}~(U_t) \overset{\text{IID}}{\sim} U(0,1). \tag{4.8}
$$

$X_0$が$S$上の分布$\psi_0$から独立に抽出された確率変数であるならば，差分方程式$(4.8)$が生み出す$(X_t)$は，$\psi_0$を初期条件とした$S$上の$P$-Markovである．

# EXERCISE 4.1.2.

$\text{EXERCISE 4.1.2.}$ $X_t = i$の条件の下で，$j \in S$について以下の$\textrm{(i)}$と$\textrm{(ii)}$が成り立つことを示せ．

$$
\begin{align*}
&\textrm{(i)} ~~ X_{t+1} = j \textrm{ if and only if } U_{t+1} \in (q(i,j-1), q(i,j)] \\
&\textrm{(ii)} ~~ \mathbb{P}\{X_{t+1}=j \mid X_t=i\} = P(i,j)
\end{align*}
$$

:::details 解答例
$(4.8)$より

$$
\begin{align*}
X_{t+1} &= F(i, U_{t+1}) \\
&= \sum_{j=1}^n j \bm{1}\{q(i,j-1) < U_{t+1} \leqslant q(i,j)\}. \tag{1}
\end{align*}
$$

$\textrm{(i)}$
$(\implies)$ $X_{t+1} = j$のとき，$(4.8)$から$\bm{1}\{q(i,j-1) < U_{t+1} \leqslant q(i,j)\} = 1$．よって，$q(i,j-1) < U_{t+1} \leqslant q(i,j)$．
$(\impliedby)$ $U_{t+1} \in (q(i,j-1), q(i,j)]$のとき，$(1)$から$X_{t+1} = j$．

<br>

$\textrm{(ii)}$
$\textrm{(i)}$より

$$
\begin{align*}
   \mathbb{P}\{X_{t+1}=j \mid X_t=i\} &= \mathbb{P}\left\{q(i,j-1) < U_{t+1} \leqslant q(i,j)\right\} \\
   &= q(i,j) - q(i,j-1) \\ &= P(i,j).
\end{align*}
$$
:::

$\textrm{(i)},\ \textrm{(ii)}$によって，差分方程式$(4.8)$の$X_{t+1}$が，確率分布$P(i,\cdot)$から抽出されることが確かめられた．

# 確率差分方程式によるシミュレーション

確率差分方程式$(4.8)$を用いて生成された2つのマルコフ連鎖の実例を示す．

![](/images/markov_chains_note/wealth_percentile_over_time.png =550x)
*図 4.4：マルコフ連鎖のシミュレーション
出所）Stachurski et al. (2024)*

- 上段は遷移行列[$P_B$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#benhabib-et-al.-(2019)%EF%BC%9A%E7%A4%BE%E4%BC%9A%E9%9A%8E%E7%B4%9A%E3%83%80%E3%82%A4%E3%83%8A%E3%83%9F%E3%82%AF%E3%82%B9%E3%81%AE%E7%A0%94%E7%A9%B6)から，下段は主対角成分の大きい[$P_Q$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#%E7%B5%90%E6%9E%9C)からサンプリング
- 各列は独立に抽出された一様確率変数列$(U_t)$で生成
- どちらも初期条件に極端な状態（最高／最低）を指定
- $P_B$から生成した時系列では，初期条件の影響が"burn in"の後まで持続していない