---
layout: post
title:  "PhysBonesのParameter項目の使い方"
date:   2022-04-29 16:50:26 +0900
categories: vrchat PB
---



# PBメモ

PhysBonesのParameter欄の使い方について、自分で調べた内容をメモしておきます。
この記事はAnimator Contorollerの使い方及び、Avater3.0におけるVRC Avater Descripterの設定項目を理解している前提でいろいろ端折ってます。

<!--ts-->

   * [PBメモ](#PBメモ)
      * [パラメーター](#パラメーター)
         * [_IsGrabbed](#_IsGrabbed)
         * [_Angle](#_Angle)
         * [_Stretch](#_Stretch)
      * [使い方](#使い方)

<!--te-->

## パラメーター

Parameter欄に何か文字を入れておくことで使えるようになる機能です。
現状3つのパラメーターが使えます。

### _IsGrabbed

Allow Grabbingにチェックが入っている状況で、該当のPBが掴まれている場合、値が1(true)になります。(bool)

### _Angle

該当のPBの傾きを検出して0～1の値を返します。細かい計算式はよくわかりませんが最大値の1はLimitの限界値に達した時？(float)


### _Stretch

該当のPBの伸びを検出して0～1の値を返します。MaxStretchで設定した限界値まで達した時に1になるようです。(float)

## 使い方

VRC Phys Bone (Script)コンポーネントの下の方にあるOptionsのParameterに何か英数字で文字を入力します。
下記画像例ではmeganeと入力しています。この場合、各パラメータは "megane_IsGrabbed" "megane_Angle" "megane_Stretch"となります。

<img src="/images/PhysBones_memo.assets/pb_parameter.jpg"  />

アバターのExpression parametersに上記パラメーターのうち使いたいものを追加します。型を合わせるよう気を付けてください。

<img src="/images/PhysBones_memo.assets/ex_parameter.jpg"  />

アバターのFXレイヤーのAnimator ControllerのParametersにも同様に追加します。

<img src="/images/PhysBones_memo.assets/animator.jpg"  />

これで使う準備が整ったのであとはレイヤーを追加してアニメーションをいい感じに作ってください。

