---
title: "4.1.2.1 Updating Marginal Distributions"
---

# 周辺分布の更新

このセクションの鍵となるアイデアは，連続する二つの周辺分布に成立する単純な規則である．すなわち，全確率の法則 (the law of total probability) より

$$
\mathbb{P}\{X_{t+1} = y\} =
\sum_x \underbrace{\mathbb{P}\{X_{t+1} = y | X_t = x\}\mathbb{P}\{X_t = x\}}_\text{joint probability}.
$$

関数$\psi_\cdot \in$ [$\mathscr{D}(S)$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#%E9%81%B7%E7%A7%BB%E8%A1%8C%E5%88%97%E3%81%A8%E5%88%86%E5%B8%83%E3%81%AE%E9%9B%86%E5%90%88-(%C2%A71.3.1.1))を用いれば，上の式は次のように書ける．

$$
\psi_{t+1}(y) = \sum_x P(x,y) \psi_t(x) \quad (y \in S). \tag{4.12}
$$

$(4.12)$は，遷移行列$P$を用いた周辺分布の更新規則を述べたものである．

# Forward Equation and Forward Operator

関数$\psi_t \in \mathscr{D}(S)$を行ベクトルと解釈すれば，$(4.12)$は次式のように行列形式で書ける：

$$
\psi_{t+1} = \psi_t P. \tag{4.13}
$$

連続時間におけるコルモゴロフの前進方程式とのアナロジーから，$(4.13)$を$P$に関する **forward equation**，写像$\psi \to \psi P$を **forward operator** と呼ぶこともある．

これ以降，行列代数 (matrix algebra) を用いた表記では，特に断りのない限り分布$\psi$は行ベクトルを表す．

$(4.13)$を分布空間$\mathscr{D}(S)$における差分方程式と考えると，

$$
\psi_t = \psi_{t-1}P = (\psi_{t-2}P)P = \psi_{t-2}P^2 = \cdots = \psi_0P^t.
$$

任意の初期条件$\psi_0\in\mathscr{D}(S)$と$t\in\mathbb{N}$を取れば，

$$
\psi_0P^t = \text{ the distribution of } X_t \text{ given } X_0 \overset{d}{=} \psi_0.
$$

つまり，$t$期の確率変数$X_t$が従う分布$\psi_t$については，**決定論的な予言**が可能である．

# Example 4.1.2.

具体例として再び [Quah (1993) の国際成長ダイナミクスの研究](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#quah-(1993)%EF%BC%9A%E5%9B%BD%E9%9A%9B%E7%9A%84%E6%88%90%E9%95%B7%E3%83%80%E3%82%A4%E3%83%8A%E3%83%9F%E3%82%AF%E3%82%B9%E3%81%AE%E7%A0%94%E7%A9%B6)を取り上げる．1960年から1984年までのデータを用いて推定された遷移行列[$P_Q$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#%E7%B5%90%E6%9E%9C)を使って，2019年のGDP分布を予測することを考えよう．予測するには1985年の分布を$P_Q$で $t=2019-1985=34$回更新 $(\psi_{2019}=\psi_{1985}P_Q^{34})$ すれば良い．

![](/images/markov_chains_note/income_distribution2019.png =400x)
*図 4.5：2019年のGDP分布の予測値と観測値
出所）Stachurski et al. (2024)*

図4.5は，予測された分布と World Bank GDP data を使って計算された2019年の実際のGDP分布を比べたものである．完全に一致とまではいかないが，それなりの予測を与えていることがわかる．
