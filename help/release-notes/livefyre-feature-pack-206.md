---
title: Livefyre機能パック2.0.6リリースノート
seo-title: Livefyre機能パック2.0.6リリースノート
description: Livefyre機能パック2.0.6リリースノート
seo-description: Livefyre機能パック2.0.6リリースノート
uuid: 81ee0527-72c3-4530-80f1-c802ddbe62d0
products: SG_EXPERIENCEMANAGER/6.4
contentOwner: alba
discoiquuid: d445bcfb-7712-472f-bfb4-a8811c2bc4f1
exl-id: e09d2d59-41f0-4cf2-bcf3-ec3dbc3b8474
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 4%

---

# Livefyre機能パック2.0.6リリースノート{#livefyre-feature-pack-release-notes}

## リリース情報 {#release-information}

| 製品 | Livefyre機能パック2.0.6 |
|--- |--- |
| バージョン | 2.0.6 |
| タイプ | 機能リリース |
| 日付 | 2018 年 8 月 31 日 |
| ダウンロード URL | 管理者に問い合わせる |
| 互換性 (*) | AEM 6.4 SP1、6.4、6.3 GA、6.2 SP1 |
| 説明 | このパッケージを使用すると、Livefyreの業界最先端のキュレーション機能をAEMインスタンスと統合し、ソーシャルネットワークから貴重なユーザー生成コンテンツ(UGC)を数分でサイトに公開できます。 |

## Livefyre機能パック2.0.6に含まれる内容{#what-is-included-in-livefyre-feature-pack}

このパッケージは、Livefyreの業界最先端のキュレーション機能をAEMインスタンスと統合し、ソーシャルネットワークから貴重なユーザー生成コンテンツ(UGC)を数分でサイトに公開できます。 このパッケージには、次の3つの異なるコンポーネントがあります。

**UGCコンテンツのAEM Assetsへの読み込み**

* UGCインポーターを使用して、TwitterとInstagramのユーザー生成コンテンツ(UGC)をLivefyre StudioからAEM Assetsに読み込みます。
* Livefyreライブラリにアクセスします。
* Livefyre Social検索を使用して、TwitterとInstagramでリアルタイムに検索します。
* UGCの権限を管理します。

**LivefyreコンポーネントのAEM SitesまたはCommunitiesへの追加**

* マップ、ギャラリー、メディアウォールなどのソーシャルコンポーネントのスイートを使用して、動的で魅力的なエクスペリエンスを即座に作成し、カスタマイズできます。
* UGCをAEM SitesまたはCommunitiesに公開します。

**AEM Commerce を使用した製品カタログの Livefyre への読み込み**

* 既存の製品カタログをLivefyreにシームレスに統合して、サイトでのユーザーエンゲージメントとコンバージョンを促進し、ショッパブルなUGCエクスペリエンスを提供します。
* AEM Commerce製品カタログの項目を編集または削除し、Livefyreの変更を自動的に更新します。

インストールに関するヘルプについては、[Livefyreとの統合](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html)を参照してください。

### 追加のリリース情報{#additional-release-information}

instagram非ビジネスユーザーアカウントからのコンテンツの集計に影響する更新により、お客様に代わってコメントを投稿したり、作成者からの返信を自動的に確認したりできなくなりました。 [詳しくはここをクリック](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/)してください。

>[!NOTE]
>
>Livefyre機能パック2.0.6はAEM Classic UIをサポートしていません。

#### 新機能または改善{#new-feature-or-improvement}

* Livefyreで権限リクエストソーシャルアカウントを設定する前にUGCを検索する機能を追加しました。 ソーシャルアカウントを設定して権限をリクエストするか、コンテンツを所有している場合は権限リクエストを上書きする必要があります。
* InstagramとTwitterの[UGC権限リクエストワークフロー](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html)が更新され、最新のAPIに準拠するようになりました。
* 権限ステータスと適切なアクションが、権限リクエスト画面に表示されます。

#### バグの修正 {#bug-fixes}

* AEMでUGCライブラリを読み込む際に、権限リクエストに使用するLivefyre Studioでソーシャルアカウントを削除するとエラーが発生する問題を修正しました。
* Livefyre Studioのアセット数がAEM UGCライブラリのアセット数と一致しない問題を修正しました。
* UGCライブラリで、フィルターオプションがリセットされた後に、フィルターされた結果が表示される問題を修正しました。
* AEM Commerceで、コールトゥアクションボタンが誤ったURLにリダイレクトされる問題を修正しました。
* AEM Sitesで、複数のコンポーネントをparsysプレースホルダーにドラッグ&amp;ドロップすると表示されなくなる問題を修正しました。
* 権限リクエストを送信する際に、無効になっているソーシャルアカウントを選択できる問題を修正しました。
* UGCをAssetsからSitesにドラッグ&amp;ドロップするとエラーが発生する問題を修正しました。
* チャットコンポーネントとLiveblogコンポーネントをSitesにドラッグ&amp;ドロップしてもアプリが作成されない問題を修正しました。
* ユーザーがコメントを試みるとコメントアプリでエラーが発生する問題を修正しました。
* Livefyre Media Wallアプリをサイトに追加すると、Javaコンテンツリポジトリに追加のノードが作成される問題を修正しました。
* instagram UGC検索で改ページとコンソールエラーが発生する問題を修正しました。
* instagramのユーザーアイコンがAssetsでAPIエラーを生成していた問題を修正しました。
* 事前に定義された形式でレビューアプリがサイトに追加されていた問題を修正しました。
* タッチ操作対応UI機能とインライン編集の問題を修正しました。
* 特定のInstagram画像アセットを読み込む際にエラーが発生する問題を修正しました。
* AEMのLivefyre HTTP Clientがプロキシ設定をサポートしていなかった問題を修正しました。
