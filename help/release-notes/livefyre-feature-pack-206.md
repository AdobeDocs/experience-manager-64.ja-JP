---
title: Livefyre機能パック2.0.6リリースノート
seo-title: Livefyre機能パック2.0.6リリースノート
description: Livefyre機能パック2.0.6リリースノート
seo-description: Livefyre機能パック2.0.6リリースノート
uuid: 81ee0527-72c3-4530-80f1-c802ddbe62d0
products: SG_EXPERIENCEMANAGER/6.4
contentOwner: alba
discoiquuid: d445bcfb-7712-472f-bfb4-a8811c2bc4f1
translation-type: tm+mt
source-git-commit: f1bf1545689b977a0f5074954df224db58cbd695
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 6%

---


# Livefyre Feature Pack 2.0.6 Release Notes {#livefyre-feature-pack-release-notes}

## リリース情報 {#release-information}

<table> 
 <tbody>
  <tr>
   <td>製品</td> 
   <td>Livefyre機能パック2.0.6</td> 
  </tr>
  <tr>
   <td>バージョン</td> 
   <td>2.0.6</td> 
  </tr>
  <tr>
   <td>型</td> 
   <td>機能リリース</td> 
  </tr>
  <tr>
   <td>日付</td> 
   <td>2018 年 9 月 1 日</td> 
  </tr>
  <tr>
   <td>ダウンロード URL<br /> </td> 
   <td>管理者に問い合わせてください</td> 
  </tr>
  <tr>
   <td>互換性 (*)</td> 
   <td>AEM 6.4 SP1、6.4、6.3 GA、6.2 SP1</td> 
  </tr>
  <tr>
   <td>説明</td> 
   <td>このパッケージを使用すると、Livefyreの業界トップクラスのキュレーション機能をAEMインスタンスに統合でき、ソーシャルネットワークから貴重なユーザー生成コンテンツ(UGC)を数分でサイトに公開できます。</td> 
  </tr>
 </tbody>
</table>

## What is included in Livefyre Feature Pack 2.0.6 {#what-is-included-in-livefyre-feature-pack}

このパッケージは、Livefyreの業界最先端のキュレーション機能をAEMインスタンスと統合して、貴重なユーザー生成コンテンツ(UGC)をソーシャルネットワークからサイトに数分で公開できます。 このパッケージには3つの異なるコンポーネントがあります。

**AEM AssetsへのUGCコンテンツの読み込み**

* TwitterおよびInstagramのユーザー生成コンテンツ(UGC)をLivefyre StudioからUGCインポーターを使用してAEM Assetsに読み込みます。
* Livefyreライブラリにアクセスします。
* Livefyre Social Searchを使用して、TwitterおよびInstagramでリアルタイムに検索できます。
* UGCの権限の管理を参照してください。

**AEM Sites追加またはコミュニティへのLivefyreコンポーネント**

* マップ、ギャラリー、メディアウォールなどの一連のソーシャルコンポーネントを使用して、動的で魅力的なエクスペリエンスを迅速に構築およびカスタマイズできます。
* AEM SitesまたはコミュニティでUGCを公開します。

**AEM Commerce を使用した製品カタログの Livefyre への読み込み**

* 既存の製品カタログをLivefyreにシームレスに統合して、サイト内でのユーザーの関与やコンバージョンを促進し、買い物かごの多いUGCエクスペリエンスを提供します。
* AEM Commerce製品カタログ内の項目を編集または削除し、Livefyre内の変更を自動的に更新します。

インストールに関するヘルプについては、Livefyreとの [統合を参照してください](https://helpx.adobe.com/jp/experience-manager/6-4/sites/administering/using/livefyre.html)。

### その他のリリース情報 {#additional-release-information}

Instagramの非ビジネスユーザーアカウントからのコンテンツの集計に影響する更新により、お客様の代わりにコメントを投稿したり、作成者からの返信を自動的に確認したりすることはできません。 [詳しくは、ここをクリックしてください](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/)。

>[!NOTE]
>
>Livefyre機能パック2.0.6はAEM Classic UIをサポートしていません。

#### 新機能または改善点 {#new-feature-or-improvement}

* Livefyreで権限リクエストのソーシャルアカウントを設定する前に、UGCを検索する機能を追加しました。 権限を要求するソーシャルアカウントを設定するか、コンテンツを所有している場合は権限要求を上書きする必要があります。
* InstagramとTwitterの [UGC権限要求ワークフロー](https://helpx.adobe.com/jp/experience-manager/6-4/sites/administering/using/livefyre.html) が、最新のAPIに準拠するように更新されました。
* 権限のステータスと適切なアクションが、権限の要求画面に表示されるようになりました。

#### バグの修正 {#bug-fixes}

* Livefyre Studioで権限リクエストに使用するソーシャルアカウントを削除すると、AEMでUGCライブラリを読み込む際にエラーが発生する問題を修正しました。
* Livefyre studioのアセット数がAEM UGCライブラリのアセット数と一致しない問題を修正しました。
* UGCライブラリで、フィルターオプションをリセットするとフィルターされた結果が表示される問題を修正しました。
* AEM Commerceで、「行動喚起」ボタンを使用すると、ユーザーが正しくないURLにリダイレクトされる問題が修正されました。
* 複数のコンポーネントをparsysプレースホルダーにドラッグ&amp;ドロップするとプレースホルダーが消えるAEM Sitesの問題が修正されました。
* 無効になったソーシャルアカウントを、権限リクエストの送信時に選択できる問題を修正しました。
* アセットからサイトにUGCをドラッグ&amp;ドロップするとエラーが発生する問題を修正しました。
* ChatおよびLiveblogのコンポーネントをSitesにドラッグ&amp;ドロップしてもアプリが作成されない問題を修正しました。
* ユーザーがコメントを試みるとコメントアプリでエラーが発生する問題を修正しました。
* Livefyre Media Wallアプリをサイトに追加すると、Java Content Repositoryに追加のノードが作成される問題を修正しました。
* Instagram UGC検索での改ページとコンソールエラーの問題を修正しました。
* InstagramのユーザーアイコンがアセットでAPIエラーを生成していた問題を修正しました。
* レビューアプリが、定義済みの形式を持たないサイトに追加される問題を修正しました。
* タッチ操作対応UI機能とインライン編集の問題を修正しました。
* 特定のInstagram画像アセットを読み込む際にエラーが発生する問題を修正しました。
* AEMのLivefyre HTTPクライアントがプロキシ設定をサポートしていなかった問題を修正しました。

