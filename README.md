# BayesianOptimizer
ベイズ最適化の練習用コード

## 内容について
機械学習のハイパーパラメータチューニングが面倒で、かと言ってグリッドサーチするのも時間がかかるしな、と思ったので
最近（2016/08/02あたり）流行りの（？）ベイズ最適化の練習をしました。その際のコードです。

* 走らせかた
 - run.pyから察してください
 
* アルゴリズム
 - アルゴリズムは参考文献１，２を参考にしています。
 - アルゴリズムに関連したパラメータはBayesianOptimizerParameter.pyに記述してあります
 
* カーネル
 - ガウシアンカーネルと、Maternカーネルが使えます。パラメータは、カーネルオブジェクトを呼び出す際に渡してください（kenerl.py参照）

## 所感
* 単に最適点を見つける、という目的からすると$$ \mathrm{arg}\max_{x}\left(\phi_t \right) $$の計算を真面目にやらないで、適当にinput spaceを間引いてサボってもそこまで困らないような気がする
* カーネルについては、経験的にはMaternカーネルの方が良さそうである
* Confidence Boundを使って、$\beta$をチューニングするのと、相互情報量を使ったアルゴリズムで$\delta$を調整するのとどちらが良いのかはいまいち自身がもてなかった。

## 今後の変更予定
* Bayesian Optimizerのハイパーパラメータの調整をもう少し系統的に行えるようにできないかと考えています。（参考文献4)
* ハイパーパラメータ空間の正則化も適当にやれるといいですね。
 - それは各人が最初に手でやれば良い気もする
* 感度分析機能Ref.5参照。
 - 本当に実装できるかはわからないが、統計的な扱いで推論をしていることのメリットを活かそうと思うとこういうことをやるのが良いのかなと思う。ただ、単に回帰しているだけであることを考えると、私にはそんなに意味があることなのかよくわからない。

## References
1. N. Srinivas, A. Krause, Sham M. Kakade and M. Seeger, "Gaussian Process Optimization in the Bandit Setting: No Regret and Experimental Design" (arXiv:0912.3995v4 [cs.LG] )
 - http://arxiv.org/abs/0912.3995
 - GP-UCBアルゴリズムを用いた更新方法について。
2. E. Contal, V. Perchet and N. Vayatis, "Gaussian Process Optimization with Mutual Information" preprint( arXiv:1311.4825v3[stat.ML])
 - http://arxiv.org/abs/1311.4825
 - 相互情報量を用いた更新方法について
3. "1020：ベイズ的最適化の入門と応用 機械学習による機械学習の実験計画" 
 - https://www.youtube.com/watch?v=pQHWew4YYao
 - 佐藤一誠さんのGTC Japan2015での講演。機械学習の人にとっては、詳細は省いて、イメージを掴みたい場合に有用では
4. J. Snoek, H. Larochelle and Ryan P. Adams, "Practical Bayesian Optimization of Machine Learning Algorithms", preprint(arXiv:1206.2944v2) 
 - https://arxiv.org/abs/1206.2944
 - ハイパーパラメータの調整について書かれている？らしい
5. M. C. Kennedy and A.O'Hagan "Bayesian calibration of computer models", J. R. Statist. Soc. B, 63, 425–464
 - http://onlinelibrary.wiley.com/doi/10.1111/1467-9868.00294/abstract
 - ベイズ最適化を用いることのメリットとして、統計的な扱いがなんかできるようになるということがある。その取り組みの一つとして評価関数の、パラメータに対する感度を調べるというのがあるようだ。そういうのも実装できるとよい。ただ、単に回帰しているだけだというのを忘れそうになるので怖い。