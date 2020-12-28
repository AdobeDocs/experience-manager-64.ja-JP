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
source-git-commit: f8ba597c62379ba413309303c2ad066ab7afce1e
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 4%

---


# Livefyre機能パック2.0.6リリースノート{#livefyre-feature-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | Livefyre機能パック2.0.6 |
|--- |--- |
| バージョン | 2.0.6 |
| 型 | 機能リリース |
| 日付 | 2018 年 9 月 1 日 |
| ダウンロード URL | 管理者に問い合わせてください |
| 互換性 (*) | AEM 6.4 SP1、6.4、6.3 GA、6.2 SP1 |
| 説明 | このパッケージを使用すると、Livefyreの業界トップクラスのキュレーション機能をAEMインスタンスと統合でき、ソーシャルネットワークから貴重なユーザー生成コンテンツ(UGC)を数分でサイトに公開できます。 |

## Livefyre機能パック2.0.6 {#what-is-included-in-livefyre-feature-pack}に含まれるもの

このパッケージは、Livefyreの業界最先端のキュレーション機能をAEMインスタンスと統合して、貴重なユーザー生成コンテンツ(UGC)をソーシャルネットワークからサイトに数分で公開できます。 このパッケージには3つの異なるコンポーネントがあります。

**UGCコンテンツをAEM Assetsに読み込む**

* UGCインポーターを使用して、TwitterおよびInstagramのユーザー生成コンテンツ(UGC)をLivefyre StudioからAEM Assetsに読み込みます。
* Livefyreライブラリにアクセスします。
* Livefyre Social Searchを使用して、TwitterおよびInstagramでリアルタイムに検索できます。
* UGCの権限の管理を参照してください。

**追加AEM SitesまたはコミュニティへのLivefyreコンポーネント**

* マップ、ギャラリー、メディアウォールなどの一連のソーシャルコンポーネントを使用して、動的で魅力的なエクスペリエンスを迅速に構築およびカスタマイズできます。
* AEM SitesやコミュニティでUGCを公開します。

**AEM Commerce を使用した製品カタログの Livefyre への読み込み**

* 既存の製品カタログをLivefyreにシームレスに統合して、サイト内でのユーザーの関与やコンバージョンを促進し、買い物かごの多いUGCエクスペリエンスを提供します。
* AEM Commerce Product Catalog内の項目を編集または削除して、Livefyre内の変更を自動的に更新します。

インストールに関するヘルプについては、[Livefyreとの連携](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html)を参照してください。

### 追加のリリース情報{#additional-release-information}

Instagramの非ビジネスユーザーアカウントからのコンテンツの集計に影響する更新により、お客様の代わりにコメントを投稿したり、作成者からの返信を自動的に確認したりすることはできません。 [詳しくは、ここをクリックしてください](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/)。

>[!NOTE]
>
>Livefyre機能パック2.0.6はAEM Classic UIをサポートしていません。

#### 新機能または強化{#new-feature-or-improvement}

* Livefyreで権限リクエストのソーシャルアカウントを設定する前に、UGCを検索する機能を追加しました。 権限を要求するソーシャルアカウントを設定するか、コンテンツを所有している場合は権限要求を上書きする必要があります。
* InstagramとTwitter [UGC権限リクエストワークフロー](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html)が、最新のAPIに準拠するように更新されました。
* 権限のステータスと適切なアクションが、権限の要求画面に表示されるようになりました。

#### バグの修正 {#bug-fixes}

* 権利要求に使用するLivefyre Studioでソーシャルアカウントを削除すると、AEMでUGCライブラリを読み込む際にエラーが発生する問題を修正しました。
* Livefyre studioのアセット数がAEM UGCライブラリのアセット数と一致しない問題を修正しました。
* UGCライブラリで、フィルターオプションをリセットするとフィルターされた結果が表示される問題を修正しました。
* AEMコマースで、アクションの呼び出しボタンが誤ったURLにリダイレクトされる問題を修正しました。
* AEM Sitesで、複数のコンポーネントをparsysプレースホルダーにドラッグ&amp;ドロップすると非表示になる問題を修正しました。
* 無効になったソーシャルアカウントを、権限リクエストの送信時に選択できる問題を修正しました。
* アセットからサイトにUGCをドラッグ&amp;ドロップするとエラーが発生する問題を修正しました。
* ChatおよびLiveblogのコンポーネントをSitesにドラッグ&amp;ドロップしてもアプリが作成されない問題を修正しました。
* ユーザーがコメントを試みるとコメントアプリでエラーが発生する問題を修正しました。
* Livefyre Media Wallアプリをサイトに追加すると、Java Content Repositoryに追加のノードが作成される問題を修正しました。
* Instagram UGC検索での改ページとコンソールエラーの問題を修正しました。
* InstagramのユーザーアイコンがアセットでAPIエラーを生成していた問題を修正しました。
* レビューアプリが、定義済みの形式を持たないサイトに追加される問題を修正しました。
* タッチ操作対応UI機能とインライン編集の問題を修正しました。
* 特定のInstagram画像アセットを読み込むとエラーが発生する問題を修正しました。
* AEMのLivefyre HTTPクライアントがプロキシ設定をサポートしていなかった問題を修正しました。
