---
layout: post
title:  "Mesh Baker(無料版)やSimplest Mesh Bakerで統合したメッシュがVRChatで表示されないときの対策"
date:   2020-10-09 00:00:00 +0900
categories: vrchat
---

VRChatでよく軽量化でお勧めされるMesh bakerですが、無料版やSimplest Mesh Bakerなどの無料アセットで統合した際はVRChatにアバターとしてアップロードした際に透明になってしまい正常に表示できない問題が存在します。

よくある解決策として有料版Mesh bakerを買うように勧められていますが、実はこれは有料版を買わなくても回避可能なのがあまり知られていないようなので以下にメモしておきます。

(genericアバターに対してしかこの方法を使ったことがないので、この方法はシェイプキーとかがどうなるのかは一切考えていません。)

### 手順①　統合されたメッシュのMesh Filterを確認する

統合されたメッシュ(Mesh Bakerであれば*MeshBaker (0)-mesh-mesh*のような名称)のゲームオブジェクトのMesh Filterコンポーネントを確認し、空欄であることを確認する。

Mesh Bakerでシーン内に作成された統合メッシュは、Mesh Filterコンポーネントが空欄であるのにメッシュが表示されているのが特徴です。（なんでなのかは知りません。）

この状態でVRChatにアバターとしてアップロードすると、このメッシュは透明になってしまいます。（なんでなのかは知りません。）

![スクリーンショット 2020-10-08 225631](/images/bake.assets/2020-10-08 225631.png)



### 手順②　FBX Exporterを導入する

昔はアセットストアからインストールできたのですが最近はPackage Managerから導入します。

**「window」＞「Package Manager」**でPackage Managerに入り、**「Advanced」**のドロップダウンメニューを開き**「Show preview packages」**にチェックを入れてFBX Exporterをインストールします。

![image-20201008230939531](/images/bake.assets/image-20201008230939531.png)



### 手順③　FBXに変換する

FBXに変換します。対象の統合されたメッシュを右クリックして**「Export to FBX...」**をクリック

![image-20201008231344888](/images/bake.assets/image-20201008231344888.png)



保存先等を指定してExportをクリック

（仮に後で作成したFBXをblanederでいじりたいのであればExport FormatをBinaryに変更すること）

（シェイプキーを維持したい時はAnimated Skinned Meshにチェックを入れる？※未確認）

![image-20201008231747937](/images/bake.assets/image-20201008231747937.png)



### 手順④　Mesh Filterを入れ替える

手順①で空欄になっていたMesh Filterを、手順③で生成したFBX由来のメッシュと置き換える。

![2020-10-08 232311](/images/bake.assets/2020-10-08 232311.png)



完

