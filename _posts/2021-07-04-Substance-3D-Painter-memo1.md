---
layout: post
title:  "Substance 3D Painter 操作備忘録|高さでグラデーションしたい時"
date:   2021-07-04 19:00:00 +0900
categories: Substance_3D_Painter
---

こんな感じにするとき

<img src="/images/substance_20210704.assets/optimized_2021-07-04 173751.png" alt="optimized_2021-07-04 173751" style="zoom:50%;" />



テクスチャセットの設定→メッシュマップをベイク→Positionマップをベイク。
Positionマップがきれいに上下にわかれずにめちゃめちゃになってしまう場合はベイク時のモードで「1つの軸」と「Y軸」を選択すると良い感じになる。

![optimized_2021-07-04 174704](/images/substance_20210704.assets/optimized_2021-07-04 174704.png)



グラデーションさせたいレイヤーのマスクに「3D Linrear Gradient」ジェネレーターを追加
3D Position Start と 3D Position End でグラデーションさせる上下の端を設定、スポイトで決めると楽。
Balance と Contrast を調整して仕上げる。反転させたい場合はInvertをTrueに

![optimized_2021-07-04 174921](/images/substance_20210704.assets/optimized_2021-07-04 174921.png)

