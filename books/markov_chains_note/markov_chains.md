---
title: "4.1.1.2 Markov Chains"
---

# マルコフ連鎖のお気持ち

- 状態空間$S$と遷移行列$P$を持つ有限マルコフモデル$\mathscr{M}$を考える
- $P(x,y)$は１ステップで状態$x$から$y$へ遷移する確率
- 今期状態$x$にあるとき，条件付き確率分布$P(x,\cdot)$に従って，新しい状態 $\cdot\in S$に更新する
- 最終的に得られる確率過程のことを**マルコフ連鎖**と呼ぶ

# マルコフ連鎖の定義

$(X_t)_{t\in\Z_+}$を$S$上の確率変数の列とする．次の条件が成り立つとき，$(X_t)$を$S$上の**マルコフ連鎖** (Markov chain) と言う．$S$上に確率行列$P$が存在して，

$$
\mathbb{P}\{X_{t+1}=y \mid X_0, X_1, \ldots,X_t\} = P(X_t, y) \quad \forall\ t \geq 0,\ y \in S. \tag{4.7}
$$

$(4.7)$式を満たす列$(X_t)$を$P$-$\textbf{Markov}$と言うこともある．文脈に応じて，$X_0$あるいはその分布$\psi_0$を$(X_t)$の**初期条件** (initial condition) と呼ぶ．

## マルコフ連鎖の心

1. $X_t$から$X_{t+1}$に更新するとき，過去の情報（$X_0,\ldots,X_{t-1}$）は必要ない
2. $X_t$を所与とすると，行列$P$は更新に必要な全ての情報を持つ

### 【補足】マルコフ性の範囲内で過去の情報を扱う

> $X_t$から$X_{t+1}$に更新するとき，過去の情報（$X_0,\ldots,X_{t-1}$）は必要ない

この点について補足すると，有限マルコフモデルの状態$x \in S$の解釈を広げることで，マルコフ性が成り立つ範囲内で過去の情報をモデルに入れることができる．

$S$上の状態の組み合わせ$(X_t, X_{t-1}) \in S \times S$を一つの状態とみなす．確率変数$Y_t \coloneqq (X_t, X_{t-1})$の列$(Y_t)_{t\in\N}$に対して，$S \times S$上に遷移行列$P$が存在して次式が成り立つとき，$(Y_t)$はマルコフ連鎖である．

$$
\mathbb{P}\{Y_{t+1}=y \mid Y_1, \ldots,Y_t\} = P(Y_t, y) \quad \forall\ t \in \N,\ y \in S \times S.
$$

以下は，過去の情報を取り入れた分析例である．
- 金融政策における政策金利の時系列のモデル化
    - 政策金利$r_{t+1}$は前期の金利$r_t$と経路$\Delta r_t\equiv r_{t}-r_{t-1}$に依存
    - $X_t = (r_t, \Delta r_t)$をマルコフ連鎖と考える
- 旅客機利用者の移動パターンの分析
    - トランジットがある場合，人々の次の行き先は現在地だけでなく，どこから来たかに依存
    - NYにいる人でシカゴから来た人は，東京に向かいやすい，など

# マルコフ連鎖をアルゴリズムとして理解する

- 確率行列$P$と初期条件$\psi_0 \in$ [$\mathscr{D}(S)$](https://zenn.dev/nagayu71/books/084559634e326d/viewer/17ea45#%E9%81%B7%E7%A7%BB%E8%A1%8C%E5%88%97%E3%81%A8%E5%88%86%E5%B8%83%E3%81%AE%E9%9B%86%E5%90%88-(%C2%A71.3.1.1))を用意
- $\textbf{Algorithm 3}$に従って列$(X_t)$を生成
- 得られた列が，$\psi_0$を初期条件とする$P$-Markovである

![](/images/markov_chains_note/algorithm3.png =550x)
*出所）Stachurski et al. (2024)*

## 【Python】実装

```python
import numpy as np
import matplotlib.pyplot as plt
```

1. ベクトルの和を1に規格化する関数を定義する

```python
def normalize(v):
    n = len(v)
    v = [abs(v[i]) for i in range(n)]
    vsum = sum(v)
    return [v[i] / vsum for i in range(n)]
```

2. 状態空間`states`と確率行列`P`を定義する．ここでは行列`P`は確率的に生成．

```python
states = [-2, -1, 0, 1, 2] # state space
P, size = [], 5            # transition matrix
for _ in range(size):
    row = [np.random.randint(1,10) for _ in range(size)]
    P.append(normalize(row))
```

3. 初期条件$\psi_0$を用意

```python
# initial distribution
initial_dist = [0.3, 0.2, 0.2, 0.1, 0.2]
```

4. $\textbf{Algorithm 3}$に従って列$(X_t)$を生成

```python
# first draw
s0 = np.random.choice(a=states, size=1, p=initial_dist)
index0 = states.index(s0)
#### simulation ####
t = 100                     # # of iteration
time, result = [t for t in range(t+1)], [s0[0]]
for _ in range(t):
    index_ = index0
    s = np.random.choice(a=states, size=1, p=P[index_])
    result.append(s[0])
    index = states.index(s)
fig, ax = plt.subplots(figsize=(10,3))
ax.plot(time, result)
ax.set_xlabel("time", fontsize=12)
ax.set_ylabel("state", fontsize=12)
ax.set_yticks(states)
plt.tight_layout();
```

![](/images/markov_chains_note/chains_generated_by_algorithm3.png)
*$\textbf{Algorithm 3}$で生成された列 $(X_t)$*

