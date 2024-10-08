---
title: "4.1.1 Markov Models"
---

# 定義
**有限マルコフモデル** (finite Markov model) とは，重み付き有向グラフ$\mathscr{M}=(S,E,p)$である．ここで，$S$は（有限の）頂点集合，$E$はエッジの集合，$p$は以下の制約を満たす重み関数 (weight function) である．

$$
\sum_{y\in\mathscr{O}(x)}p(x,y)=1 \quad \text{for all } x \in S. \tag{4.1}
$$

ただし，$\mathscr{O}(x)$は頂点$x$の[出近傍](https://zenn.dev/nagayu71/articles/61e5f6c2cd55a0#%E3%83%8E%E3%83%BC%E3%83%89%E3%81%AE%E7%89%B9%E5%BE%B4%E3%82%92%E8%A1%A8%E3%81%99%E7%94%A8%E8%AA%9E)である．
頂点集合$S$はモデルの**状態空間** (state space) とも呼ばれ，頂点のことを**状態** (states) と言う．

![weighted_digraph.png](/images/markov_chains_note/weighted_digraph.png =350x)
*図 1.15：有限マルコフモデルの例
出所）Stachurski et al. (2022)*

# 有限マルコフモデルの解釈
1. $S$は確率的な要素が取りうる実現可能な状態の集合であり，重み$p(x,y)$は１ステップで状態$x$から$y$へ遷移する確率を表す

2. $S$は大規模な集団に対する測定値の取りうる値の集合であり，$p(x,y)$は単位時間あたりに状態$x$から$y$へ遷移するエージェントの割合を表す
   - ある状態$x$にある資源（e.g., 水，労働者数）の量を$q(x)$と表す．全体の資源量が$\sum_{x\in S}q(x)=1$と規格化されているとすれば，状態$x$にある資源$q(x)$の$100\times p(x,y)\%$が$y$に移動すると理解できる