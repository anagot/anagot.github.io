---
layout: post
title:  "バーチャルマーケット出展者向け容量制限対策メモ"
date:   2020-09-30 22:52:00 +0900
categories: vrchat
---



# バーチャルマーケット出展者向け容量制限対策メモ

<!--ts-->
   * [バーチャルマーケット出展者向け容量制限対策メモ](#バーチャルマーケット出展者向け容量制限対策メモ)
      * [バーチャルマーケットの入稿容量制限について](#バーチャルマーケットの入稿容量制限について)
         * [入稿フォルダの容量制限](#入稿フォルダの容量制限)
            * [対策](#対策)
               * [① テクスチャを実際の使用解像度と合わせる](#-テクスチャを実際の使用解像度と合わせる)
               * [② テクスチャの画像形式を変更する](#-テクスチャの画像形式を変更する)
               * [③ 画像圧縮ツールの活用](#-画像圧縮ツールの活用)
         * [AssetBundleのビルドサイズの容量制限](#assetbundleのビルドサイズの容量制限)
            * [対策](#対策-1)
               * [①テクスチャのCrunch圧縮](#テクスチャのcrunch圧縮)
               * [②3Dモデルのメッシュを圧縮](#3dモデルのメッシュを圧縮)
               * [③テクスチャのMip Mapを生成させない](#テクスチャのmip-mapを生成させない)

<!-- Added by: root, at: Wed Sep 30 23:01:21 JST 2020 -->

<!--te-->

## バーチャルマーケットの入稿容量制限について

バーチャルマーケットには入稿フォルダの容量制限とAssetBundleのビルドサイズの容量制限が存在する。

これら2つの容量制限はそれぞれ制限超過の対策方法が異なる。



### 入稿フォルダの容量制限

エクスプローラーで見た時の入稿フォルダ内のファイルの総容量。ほとんどの場合3Dモデルやテクスチャで占められることになる。

この制限を超えてしまう場合、多くの場合では高解像度のテクスチャに原因がある。



#### 対策

##### ① テクスチャを実際の使用解像度と合わせる

Unityデフォルトの設定では2k解像度(2048×2048)以上の解像度の画像は2kに変換されて利用されている。そのため4kテクスチャ等を本来のサイズで使いたい場合はテクスチャのInspectorの**Max Size**を2048から引き上げる必要があるが、もし今までこれを知らずに4kテクスチャを利用し、特にビジュアルにも不満がなかったのであれば、いっそ元のテクスチャを2kにリサイズしてしまうことで容量を削減できる。

「Unity側で2kに変換しているのであればその作業は不要なのでは？」と思われるかもしれないが、
あくまでUnity側での解像度の変換はPNGやJPGをGPUで扱う型式(BC6H, DXT5等)変換する際のものに過ぎないため、入稿フォルダ内の元画像のサイズには影響はない。(AssetBundleのビルドサイズを減らす効果はある。)



##### ② テクスチャの画像形式を変更する

入稿フォルダ内にPSDファイルを入れているのであればPNG等の適切な形式に変換。

PNGファイルでもまだ大きいのであればJPEG化も手だが画質の劣化具合次第。



##### ③ 画像圧縮ツールの活用

画質を可能な限り落とさずに容量を圧縮する系のツールがいろいろとあるのでそれらを利用する。
その手のWEBサービスの中には画像のアップロードが必要となるものともあるため利用規約との兼ね合いに気を付ける事。

手軽にできるものであればGoogleの開発した[squoosh](https://squoosh.app/)(ブラウザで利用するが画像の圧縮はローカルで動作する)

手間がかかってもいいからPNGの圧縮率を重視したいのであれば[opt_image](https://github.com/mixsoda/opt_image)

参考としてopt_imageでSubstancePainterで作成した3.07MBのPNGファイルが907KBになった。
パッと見では画質に変化は感じない。



### AssetBundleのビルドサイズの容量制限

AssetBundleは各種アセットをプラットフォームが使う形式に変換してまとめて圧縮したもの（よくわかってない）

3DモデルやテクスチャはGPUが扱う形式に変換・圧縮されるので、エクスプローラーで見た入稿フォルダ内のファイルサイズとは差異がでる。

Crunch圧縮をする前の変換後のテクスチャのファイルサイズは解像度ごとに固定となっているようなので、変換元の画像のファイル形式やサイズは関係ない。そのためAssetBundleのビルドサイズを削減する目的でPNGをJPGに変換するような行為は無意味であることに注意。

また、逆に各種圧縮等の後述の対策は入稿フォルダ内の元ファイルには何の影響も与えないため入稿フォルダの容量制限の回避には効果が無いことにも注意。



#### 対策

##### ①テクスチャのCrunch圧縮

テクスチャのInspectorから**Use Crunch Compression**にチェックを入れることでテクスチャのCrunch圧縮を有効にできる。

これによりAssetBundleの容量を大幅に削減できるが不可逆圧縮のため画質の低下が発生する。

**Compression**は特に問題なければデフォルト値の**Normal Quality**で良い。(Highにするとファイルサイズがかなり大きくなり、Lowにすると画質の低下が無視できない。)

**Compressor Quality**は高くすると画質が上がってファイルサイズが増える、低くすると画質が下がってファイルサイズが減るが、**Compression**を変更した時ほど画質に大きな影響は出ないので画質への影響を見て微調整しながら低めに設定すると良い。



##### ②3Dモデルのメッシュを圧縮

FBX等の3DモデルのInspectorから**Mesh Compression**を有効にすることでメッシュを圧縮し、ファイルサイズを削減するが、
見栄えに影響が出やすいため、どうしても圧縮する際はLowに留めておいた方が良い。



##### ③テクスチャのMip Mapを生成させない

これはあまり褒められた方法ではないが、テクスチャのInspectorから**Generate Mip Maps**のチェックを外すことでファイルサイズを2～3割削減できる。

(Mip Mapの存在意義を考えるとvketのようなイベントでは有効の方がユーザーの負荷は少なく済むはずだが、現状の入稿ツールのチェックではMip Mapの有無による負荷の差は見ていないため、抜け穴的な対処法となる。)