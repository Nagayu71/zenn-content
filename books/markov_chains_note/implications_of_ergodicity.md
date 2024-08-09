---
title: "4.2.1.3 Implications of Ergodicity"
---

## エルゴード性の意味

確率論における最も重要な帰結の一つに，**大数の法則** (law of large numbers; LLN) がある．大数の（強）法則によれば，有限の状態空間 $S$ 上の確率分布 $\varphi \in$  [$\mathscr{D}(S)$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#%E9%81%B7%E7%A7%BB%E8%A1%8C%E5%88%97%E3%81%A8%E5%88%86%E5%B8%83%E3%81%AE%E9%9B%86%E5%90%88-(%C2%A71.3.1.1))に独立かつ同一に従う確率変数列 $(X_t)_{t \geqslant 0}$ と任意の[実数値関数](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#%E9%81%B7%E7%A7%BB%E8%A1%8C%E5%88%97%E3%81%A8%E5%88%86%E5%B8%83%E3%81%AE%E9%9B%86%E5%90%88-(%C2%A71.3.1.1)) $h \in \mathbb{R}^S$ について，以下の性質が成り立つ．

$$
\mathbb{P}\left\{\lim_{k\to\infty}\frac{1}{k}\sum_{t=0}^{k-1}h(X_t) = \sum_{x\in S}h(x)\varphi(x)\right\} = 1.
$$

このクラスの LLN は IID の仮定が課されているという点で古典的である．実は，この IID の仮定を弱めて観測値間の依存性をある程度許すことができるが，そうなるとマルコフ連鎖に対しても LLN が成り立つのかという疑問が生じる．

そして，この疑問に対する答えは yes である．というのも，観測値の間の依存性は，（IID とみなすのに）十分なほど速く消滅するからである．エルゴード性は，そのための条件の一つの候補であり，実際にエルゴード性は大数の法則をマルコフ連鎖に拡張するための必要かつ十分な条件である．

:::message
$\textbf{Theorem 4.2.2}$　$\mathscr{M}$ を状態空間 $S$ と遷移行列 $P$ をもつ有限マルコフモデルとする．このとき次の二つの命題は同値である．

$\text{(i)}$ $\mathscr{M}$ はエルゴード的である．
$\text{(ii)}$ $\mathscr{M}$ は一意の定常分布 $\psi^*$ をもち，任意の [$P$-Markov](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/markov_chains#%E3%83%9E%E3%83%AB%E3%82%B3%E3%83%95%E9%80%A3%E9%8E%96%E3%81%AE%E5%AE%9A%E7%BE%A9) な列 $(X_t)$ と任意の関数 $h \in \mathbb{R}^S$ に対して，

$$
\mathbb{P}\left\{\lim_{k\to\infty}\frac{1}{k}\sum_{t=0}^{k-1}h(X_t) = \sum_{x\in S}h(x)\psi^*(x)\right\} = 1. \tag{4.18}
$$
:::

$\text{Theorem 4.2.2}$ の証明は，[Meyn and Tweedie (2009)](https://doi.org/10.1017/CBO9780511626630)^[Meyn, S. P. and Tweedie, R. L. (2009). *Markov chains and stochastic stability*. Cambridge University Press.] の Chapter 17 を見よ．ここでは証明をスキップし，具体例を通して定理の直感的な意味を考える．

### Example 4.2.5.

[Example 4.2.2](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/definition_and_implications#example-4.2.2.) のマルコフ連鎖だが IID な特殊ケースを思い出そう．

> $\varphi$ を $S$ 上の確率分布とする．任意の $x,y \in S$ について，遷移確率が $P(x,y) = \varphi(y)$ であるとき，来期の状態は今期の状態から独立なので，$P$ は IID なマルコフ連鎖を生成する．このとき，$P$ を遷移行列としてもつ有限マルコフモデル $\mathscr{M}$ はエルゴード的である．実際，$h \in \mathbb{R}^S$ が $P$-harmonic であるなら，任意の $x \in S$ について
> $$h(x) = Ph(x) = \sum_{y \in S} P(x,y)h(y) = \sum_{y \in S} \varphi(y)h(y) = \text{const.}$$
であるので，どの $P$-harmonic 関数も定数関数である．したがって，$\mathscr{M}$ はエルゴード的である．

$\text{Theorem 4.2.2}$ より $(4.18)$ の収束は $\psi^* = \varphi$ で成り立ち，これは IID な確率変数列に対する LLN に他ならない．

### Example 4.2.6.

状態空間 $S = \set{1,2}$ と遷移行列 $P = I$ からなる有限マルコフモデル $\mathscr{M}$ を考える．このとき $P$ から生成されるマルコフ連鎖 $(X_t)_{t\geqslant 0}$ は定数であり，

$$
Ph = Ih = h \quad \forall h \in \mathbb{R}^S
$$

より任意の関数 $h$ は $P$-harmonic である．したがって，定義から $\mathscr{M}$ は非エルゴード的であり，

$$
\mathbb{P}\left\{\lim_{k\to\infty}\frac{1}{k}\sum_{t=0}^{k-1}h(X_t) = \sum_{x\in S}h(x)\psi^*(x)\right\} = 1 \tag{4.18}
$$

も成り立たない．なぜなら，

$$
\frac{1}{k}\sum_{t=0}^{k-1}X_t = \frac{1}{k}\sum_{t=0}^{k-1}X_0 = X_0 \quad \forall k \geqslant 0
$$

が示すように，時間平均の初期値依存性が消えないからである．特に，$X_0$ が非退化分布から抽出される場合は $(X_t)$ の標本平均は一定の値に収束しない．

### Example 4.2.7.

![](/images/markov_chains_note/poverty_trap.png =250x)
*図 4.9：貧困の罠
出所）Stachurski et al. (2024)*

図4.9の貧困の罠モデルを再び考えよう．$h(x)$ を状態 $x$ での所得であるとし，$h(\text{poor}) = 1,\ h(\text{middle}) = 2,\ h(\text{rich}) = 3$ と定める．初期状態が $X_0 = \text{poor}$ で始まった家計は，貧困から抜け出せないので $\frac{1}{k}\sum_{t=0}^{k-1}h(X_t) = 1\ \forall k$ である．他方で，初期状態が $X_0 \in \set{\text{middle, rich}}$ であった家計は，この吸収状態に永遠にとどまり続けるので $\frac{1}{k}\sum_{t=0}^{k-1}h(X_t) \geqslant 2\ \forall k$ である．

このように，所得の合計の極限が初期値に依存するので，$(4.18)$ が示す極限の $X_0$ の分布からの独立性に反する．したがって，このマルコフモデルはエルゴード的でない．

:::message
$\textbf{Theorem 4.2.2}$ **の直感的な意味**

通常のマルコフ連鎖 $(X_t)$ は，来期の状態が今期の状態に依存し，周辺分布も時間発展するので，独立同分布 (IID) ではない．しかし，エルゴード性のもとでは十分時間が経過した後の $(X_t)$ は，周辺分布が定常分布 $\psi^*$ に収束しているため，$\psi^*$ からのランダムサンプリングであるとみなすことができる．
:::

## 時間平均とアンサンブル平均

:::message alert
以下の議論は，理解に自信のない部分ですので，間違った部分があればご指摘いただけますと幸いです．
:::

$\text{Theorem 4.2.2}$ の $(4.18)$ 式を眺めてみよう．

$$
\mathbb{P}\left\{\lim_{k\to\infty}\frac{1}{k}\sum_{t=0}^{k-1}h(X_t) = \sum_{x\in S}h(x)\psi^*(x)\right\} = 1 \tag{4.18}
$$

ここで，

$$
\lim_{k\to\infty}\frac{1}{k}\sum_{t=0}^{k-1}h(X_t)
$$

という統計量は，ある一つのマルコフ連鎖 $(X_t)$ を継続的に観測したときの**時間平均**を表す．ある一つのエージェントの動きを追えば計算できるので，シミュレーション的な操作と言える．

これに対して，

$$
\sum_{x\in S}h(x)\psi^*(x)
$$

という統計量は，定常分布 $\psi^*(x)$ の下での関数 $h(x)$ の期待値であり，**アンサンブル平均**（集合平均）とも言われる^[正直，位相平均，空間平均との違いが理解できていないので，有識者の方がいらっしゃれば，ご教示いただけると嬉しいです．]．すべてのエージェントの動きを追う必要があるので，計算にはそれなりのコストがかかる^[どの状態にどれだけのエージェントが存在するかを知る必要があるので，神様向けの統計量とも言えるかもしれない．]．

$(4.18)$ は時間平均とアンサンブル平均が一致することを意味しており，[（個別）エルゴード定理](https://ja.wikipedia.org/wiki/%E3%82%A8%E3%83%AB%E3%82%B4%E3%83%BC%E3%83%89%E5%AE%9A%E7%90%86)と呼ばれる．この性質のおかげで，解析的に事後分布を計算できない場合に近似的に事後分布からのサンプリングを実現するマルコフ連鎖モンテカルロ法 (MCMC) が成り立っている．