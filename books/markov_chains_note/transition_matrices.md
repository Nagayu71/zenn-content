---
title: "4.1.1.1 Transition Matrices"
---

# 復習

**有限マルコフモデル** (finite Markov model) とは，重み付き有向グラフ$\mathscr{M}=(S,E,p)$である．ここで，$S$は（有限の）頂点集合，$E$はエッジの集合，$p$は以下の制約を満たす重み関数 (weight function) である．

$$
\sum_{y\in\mathscr{O}(x)}p(x,y)=1 \quad \text{for all } x \in S. \tag{4.1}
$$

ただし，$\mathscr{O}(x)$は頂点$x$の[出近傍](https://zenn.dev/nagayu71/articles/61e5f6c2cd55a0#%E3%83%8E%E3%83%BC%E3%83%89%E3%81%AE%E7%89%B9%E5%BE%B4%E3%82%92%E8%A1%A8%E3%81%99%E7%94%A8%E8%AA%9E)である．頂点集合$S$はモデルの**状態空間** (state space) とも呼ばれ，頂点のことを**状態** (states) と言う．

![](/images/markov_chains_note/weighted_digraph.png =350x)
*図 1.15：有限マルコフモデルの例
出所）Stachurski et al. (2024)*

# 遷移行列

$\mathscr{M}$が有限マルコフモデルであれば，制約$(4.1)$式は有向グラフ$\mathscr{M}$の隣接行列が確率行列であることを意味する．

:::details 確率行列 (§1.3.1.3)
行列$P=(p_{ij})\in\Bbb{M}^{n\times n}$が次の条件を満たすとき，$P$を**確率行列** (stochastic matrix) と言う．

$$
P \geqslant O \quad \text{and} \quad P\bm{1} = \bm{1}
$$
ただし，$P \geqslant O$は$P$が非負行列であることを表し，$\bm{1} \in \R^n$は全ての要素が$1$の列ベクトルである．
:::

例えば図1.15の重み付き有向グラフの隣接行列は

$$
P_a = \begin{pmatrix}
0.9 & 0.1 & 0.0 \\
0.4 & 0.4 & 0.2 \\
0.1 & 0.1 & 0.8 \\
\end{pmatrix}\tag{4.2}
$$

で与えられる．$P_a \geqslant \bm{0}$かつ$P_a\bm{1}=\bm{1}$を満たすため，$P_a$は確率行列である．有限マルコフモデルでは，$\mathscr{M}$の隣接行列は**遷移行列** (transition matrix) とも呼ばれる．

## 行列要素の表記

$S$が要素$x,y$を持つ時，遷移行列$P$の要素を$P_{ij}$ではなく$P(x,y)$と書くと都合が良い．この表記によって，重み関数$p:E\to\R_{++}$の定義域$E$を$S \times S$上のペア$(x,y)$全ての集合に拡張した関数として$P$を理解できる．$P(x,y)$が$(x,y)\notin E$ならば常に$0$をとるようにすれば，任意のペア$(x,y)\in S \times S$について，$P(x,y)$の値は$x$から$y$に1ステップで遷移する確率を表す．

この表記法を用いると，$P$が確率行列として満たす制約は，$P \geqslant \bm{0}$かつ

$$
\sum_{y\in S}P(x,y) = 1 \quad \text{for all}~ x \in S. \tag{4.3} 
$$

である．$(4.3)$式は状態空間が **complete**^[状態$x\in S$に到達した後，必ず何らかの状態$y\in S$に遷移する]であることを述べているに過ぎない．

## 遷移行列と分布の集合 (§1.3.1.1)

$S$を有限集合としたとき，

$$
\mathscr{D}(S) \coloneqq \left\{ \varphi \in \R_+^{S} ~:~ \sum_{x \in S} \varphi (x) = 1  \right\}
$$

を$S$上における分布 (**distributions**) の集合と呼ぶ．

::: details cf) 実数値関数 (§6.1.1.5)
$S$を任意の集合として，$f:S\to\R$であるとき，$f$を**実数値関数** (real-valued function) と言う．$S$上の実数値関数全体の集合を$\R^S$と表記する．$S$が$n$個の要素を持つときは，表記は異なるが$\R^S$と$\R^n$は同じ集合である．

$\textbf{Lemma 6.1.2.}\enspace|S|=n$であれば，

$$
\mathbb{R}^S \ni h = (h(x_1), \ldots, h(x_n)) \ \ \longleftrightarrow\ \ 
\begin{pmatrix} h_1 \\ \vdots \\ h_n \end{pmatrix} \in \mathbb{R}^n \tag{6.3}
$$
は$\mathbb{R}^n$と関数空間$\mathbb{R}^S$の間の全単射（1対1対応; one-to-one correspondence）である．
:::

$$
\mathbb{P} \{X = x\} = \varphi(x) \quad \text{for all } x \in S
$$

が成り立つ時，$S$上の値をとる確率変数$X$は分布$\varphi \in \mathscr{D}(S)$に従うと言い，これを$X \overset{d}{=} \varphi$と書く．

遷移行列$P$が確率行列であるとは，$P$の各行（ベクトル）が$\mathscr{D}(S)$に含まれることを意味する．

# Examples

経済学におけるマルコフモデルを用いた分析の例として，[Quah (1993)](https://doi.org/10.1016/0014-2921(93)90031-5) と [Benhabib et al. (2019)](https://doi.org/10.1257/aer.20151684) を取り上げる．

## Quah (1993)：国際的成長ダイナミクスの研究

### 研究内容

- マルコフモデル（の遷移行列）を推定
- 状態は，ある国の世界平均に対する一人当たり実質GDP
- 状態がとりうる値を5つの区間に離散化：

| 状態1 | 状態2 | 状態3 | 状態4 | 状態5 |
| ---- | ---- | ---- | ---- | ---- |
| $0-1/4$ | $1/4-1/2$ | $1/2-1$ | $1-2$ | $2-\infty$ |
- 遷移期間は１年間

### 研究方法

- 最尤推定法
- 1960-1984年の遷移データを使用
- 状態間遷移の相対的な頻度を記録

### 結果

![](/images/markov_chains_note/cross-country_gdp_dynamics.png =400x)
*図 4.1：GDPダイナミクスを表現する有向グラフ
出所）Stachurski et al. (2024)*

図4.1の有向グラフは，推定された１ステップの遷移確率を表している．状態空間は$S=\Set{1,\ldots,5}$であり，エッジはノードを結ぶ矢印で表されている．エッジに付された数値が重みであり，二つの状態間の遷移確率を表す．
図4.1のマルコフモデルの遷移行列は，

$$
P_Q = \begin{pmatrix}
\color{red}0.97 & 0.03 & 0.00 & 0.00 & 0.00 \\
0.05 & \color{red}0.92 & 0.03 & 0.00 & 0.00 \\
0.00 & 0.04 & \color{red}0.92 & 0.04 & 0.00 \\
0.00 & 0.00 & 0.04 & \color{red}0.94 & 0.02 \\
0.00 & 0.00 & 0.00 & 0.01 & \color{red}0.99 \\
\end{pmatrix}\tag{4.4}
$$

であり，主対角成分が大きな値を取っていることに注意されたい．これは毎期毎期，高確率で同じ状態にとどまり続けるという強い持続性を表している．

## Benhabib et al. (2019)：社会階級ダイナミクスの研究

2007-2009年の米国消費者金融調査（Survey of Consumer Finances）のデータを使用して，$S_1\sim S_8$で表される世代間の社会階級（富の分布のパーセンタイル）の移動を捉える遷移行列を推定した．

$$
P_B := \begin{pmatrix}
\color{blue}0.222 & 0.222 & 0.215 & 0.187 & 0.081 & 0.038 & 0.029 & 0.006 \\
0.221 & \color{blue}0.22 & 0.215 & 0.188 & 0.082 & 0.039 & 0.029 & 0.006 \\
0.207 & 0.209 & \color{blue}0.21 & 0.194 & 0.09 & 0.046 & 0.036 & 0.008 \\
0.198 & 0.201 & 0.207 & \color{blue}0.198 & 0.095 & 0.052 & 0.04 & 0.009 \\
0.175 & 0.178 & 0.197 & 0.207 & \color{blue}0.11 & 0.067 & 0.054 & 0.012 \\
0.182 & 0.184 & 0.2 & 0.205 & 0.106 & \color{blue}0.062 & 0.05 & 0.011 \\
0.123 & 0.125 & 0.166 & 0.216 & 0.141 & 0.114 & \color{blue}0.094 & 0.021 \\
0.084 & 0.084 & 0.142 & 0.228 & 0.17 & 0.143 & 0.121 & \color{blue}0.028 \\
\end{pmatrix}\tag{4.5}
$$

$S_1$:0-20%, $S_2$:20-40%, $S_3$:40-60%, $S_4$:60-80%, $S_5$:80-90%, $S_6$:90-95%, $S_7$:95-99%, $S_8$:99-100%

状態の持続性の強い$P_Q$に対して，$P_B$の主対角成分は小さい値をとっているので，初期条件の影響がすぐに消失することがわかる．遷移行列$P_B$を反時計回りに90°回転させると，図4.3のカントールプロットを得る．状態$x$からの垂直の線は，来期の状態の条件付き確率$P(x,\cdot)$を表す．

![](/images/markov_chains_note/contour_plot.png =350x)
*図 4.3：遷移行列$P_B$のカントールプロット
出所）Stachurski et al. (2024)*

階級のトップ($S_8$)が中流階級($S_4$)に遷移する傾向がある一方で，下流階級($S_1,S_2,S_3$)での持続性が強いことがわかる．

# EXERCISE 4.1.1.

$\text{EXERCISE 4.1.1.}$ $\mathscr{M}$を状態空間$S$と遷移行列$P$を持つ有限マルコフモデルとする．有向グラフ$\mathscr{M}$において，部分集合$U\subset S$は次式が成り立つ時，そしてその時に限り吸収 (absorbing) であることを示せ．

$$
\sum_{y \in U}P(x,y)=1 \quad \text{for all} \quad x \in U. \tag{4.6}
$$

:::details 吸収 (§1.4.1.3) 
有向グラフ$\mathscr{G}=(V,E)$において，頂点$u\in V$から$v$に向かう有向パスが存在するとき，あるいは$u=v$であるとき，頂点$v$は$u$から**accessible**であると言う．部分集合$U \subset V$から$V\setminus U$のどの要素にも有向パスが存在しないとき，$U$を**absorbing**と言う．
:::

:::details 解答例
$U$が吸収 $\implies$ (4.6)：
部分集合$U$が吸収であるとき，任意の$x \in U$に対して$P(x,y') > 0$となるような$y' \in V \setminus U$は存在しない．つまり，任意の$x \in U,\ y' \in V \setminus U$について$P(x,y') = 0$である．行列$P$が確率的であることの制約(4.3)より，

$$
  \forall x \in U, \quad 1 = \sum_{y\in S}P(x,y) 
  = \sum_{y'\in V\setminus U}P(x,y') + \sum_{y\in U}P(x,y)
  = \sum_{y\in U}P(x,y).
$$

$(\impliedby)$：
確率行列$P$の制約(4.3)より

$$
  \forall x \in S,\quad \sum_{y\in S}P(x,y) = \sum_{y'\in V\setminus U}P(x,y') + \sum_{y\in U}P(x,y) = 1.
$$
よって，

$$
  \sum_{y'\in V\setminus U}P(x,y') = 1 - \sum_{y\in U}P(x,y) \quad \forall x \in S
$$
を得る．(4.6)より

$$
  \sum_{y'\in V\setminus U}P(x,y') = 1 - 1 = 0 \quad \forall x \in S.
$$
$P(x,\cdot)$は非負なので，

$$
  P(x,y') = 0 \quad (x \in U,\ y' \in V \setminus U).
$$
これは集合$U$が吸収であることに他ならない．
:::

# 参考文献

- Quah, D. (1993). Empirical cross-section dynamics in economic growth. *European Economic Review*, 37(2-3.):426–434.
- Benhabib, J., Bisin, A., and Luo, M. (2019). Wealth distribution and social mobility in the us: A quantitative approach. *American Economic Review*, 109(5):1623–47.