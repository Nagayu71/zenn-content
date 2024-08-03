---
title: "4.1.2.2 Trajectories in the Long Run"
---

# 分布の軌跡

周辺分布列$(\psi_t)$の漸近解析 (asymptotics) は，マルコフ連鎖の主要な関連分野であり，ネットワーク理論にとっても重要なトピックである．漸近解析は $\S\ 4.2.2$ で深く掘り下げ，ここではシミュレーションを通してその直感を掴む．

![](/images/markov_chains_note/trajectory4-6.png =400x)
*図 4.6：$\psi_0=(0,0,1)$を初期値とする分布の軌跡
出所）Stachurski et al. (2024)*

図4.6の赤紫色の点列は，状態空間$S=\{1,2,3\}$と遷移行列[$P_a$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#%E9%81%B7%E7%A7%BB%E8%A1%8C%E5%88%97)を持つ有限マルコフモデルにおける，$\psi_0=(0,0,1)$を初期条件としたときの周辺分布$(\psi_0 P_a^t)$の軌跡$(t=0,\ldots,20)$を表している．青い三角形は$\mathbb{R}_{+}^3$上の単位単体$\{\psi \in \mathbb{R}^3 \mid \psi \geq \bm{0}, \psi\bm{1}=1\}$であり，$\mathscr{D}(S)$を描画したものである．

![](/images/markov_chains_note/trajectory4-7.png =400x)
*図 4.7：$\psi_0=(0,1/2,1/2)$を初期値とする分布の軌跡
出所）Stachurski et al. (2024)*

初期値を変えると軌跡はどのように変化するだろうか．図4.7は$\psi_0=(0,1/2,1/2)$を初期条件としたときの$(\psi_0 P_a^t)$の軌跡$(t=0,\ldots,20)$を表している．

図を見る限り，どちらの初期値でも分布列は収束しているように思える．そしてその直感は正しい．図中の黒点は分布列の極限であり，$P_a$の一意の定常分布（$\psi P_a = \psi$を満たす$\psi^*$）である．つまり，初期条件$\psi\in\mathscr{D}(S)$によらず，$(\psi P_a^t)$は必ず$\psi^*$に収束する．この性質は$P_a$の**連結性** (connectivity) と**非周期性** (aperiodicity) から保証される．

# 収束の速度

遷移行列[$P_B$](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/transition_matrices#benhabib-et-al.-(2019)%EF%BC%9A%E7%A4%BE%E4%BC%9A%E9%9A%8E%E7%B4%9A%E3%83%80%E3%82%A4%E3%83%8A%E3%83%9F%E3%82%AF%E3%82%B9%E3%81%AE%E7%A0%94%E7%A9%B6)から生成される分布列を使って，分布列について別の視点から考える．

![](/images/markov_chains_note/distribution_projections.png =400x)
*図 4.8：$P_B$による一様分布の更新
出所）Stachurski et al. (2024)*

図4.8のパネルはそれぞれ，一様分布$\psi_0$を$\psi_t = \psi_0 P_B^t$によって $t=1,2,100$ 回更新した分布を表している．この数値例では，富の分布は長期における極限と思われる分布に急速に収束している．つまり，$t=2$ の時点ですでに $t=100$ の分布にほぼ一致している．

次のセクションでは初期分布が実際に極限分布に収束しており，極限分布が初期条件によらないことを確認する．また，極限分布への収束の速さは，状態遷移ダイナミクスの[高い混合度 (the high level of mixing)](https://zenn.dev/nagayu71/books/markov_chains_note/viewer/simulation#%E7%A2%BA%E7%8E%87%E5%B7%AE%E5%88%86%E6%96%B9%E7%A8%8B%E5%BC%8F%E3%81%AB%E3%82%88%E3%82%8B%E3%82%B7%E3%83%9F%E3%83%A5%E3%83%AC%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3) に起因しており，$\S\ 4.2.2.3$ と $\S\ 4.2.3$ で議論する．