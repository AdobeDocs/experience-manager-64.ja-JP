---
title: Livefyre 機能パック 2.0.6 リリースノート
seo-title: Livefyre Feature Pack 2.0.6 Release Notes
description: Livefyre 機能パック 2.0.6 リリースノート
seo-description: Livefyre Feature Pack 2.0.6 Release Notes
uuid: 81ee0527-72c3-4530-80f1-c802ddbe62d0
products: SG_EXPERIENCEMANAGER/6.4
contentOwner: alba
discoiquuid: d445bcfb-7712-472f-bfb4-a8811c2bc4f1
exl-id: e09d2d59-41f0-4cf2-bcf3-ec3dbc3b8474
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 6%

---

# Livefyre 機能パック 2.0.6 リリースノート {#livefyre-feature-pack-release-notes}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## リリース情報 {#release-information}

| 製品 | Livefyre 機能パック 2.0.6 |
|--- |--- |
| バージョン | 2.0.6 |
| タイプ | 機能リリース |
| 日付 | 2018年8月31日（PT） |
| ダウンロード URL | 管理者に問い合わせてください |
| 互換性 (*) | AEM 6.4 SP1、6.4、6.3 GA、および 6.2 SP1 |
| 説明 | このパッケージを使用すると、Livefyre の業界最先端のキュレーション機能をAEMインスタンスと統合して、有用なユーザー生成コンテンツ (UGC) をソーシャルネットワークからサイトに数分で公開できます。 |

## Livefyre 機能パック 2.0.6 に含まれる内容 {#what-is-included-in-livefyre-feature-pack}

このパッケージは、Livefyre の業界最先端のキュレーション機能をAEMインスタンスと統合し、有用なユーザー生成コンテンツ (UGC) をソーシャルネットワークからサイトに数分で公開できます。 このパッケージには、次の 3 つの異なるコンポーネントがあります。

**UGC コンテンツをAEM Assetsに読み込む**

* UGC インポーターを使用して、TwitterおよびInstagramのユーザー生成コンテンツ (UGC) を Livefyre Studio からAEM Assetsに読み込みます。
* Livefyre ライブラリにアクセスします。
* Livefyre Social Search を使用して、TwitterとInstagramでリアルタイムに検索できます。
* UGC に対する権限の管理

**Livefyre コンポーネントのAEM Sitesまたは Communities への追加**

* マップ、ギャラリー、メディアウォールなどの一連のソーシャルコンポーネントを使用して、動的で魅力的なエクスペリエンスを即座に構築し、カスタマイズします。
* UGC をAEM Sitesまたは Communities で公開します。

**AEM Commerce を使用した Livefyre への製品カタログの読み込み**

* 既存の製品カタログを Livefyre にシームレスに統合して、サイトでのユーザーエンゲージメントやコンバージョンを促進し、ショッパブルな UGC エクスペリエンスを提供します。
* AEM Commerce 製品カタログの項目を編集または削除し、Livefyre で変更を自動的に更新します。

インストールに関するヘルプについては、 [Livefyre との統合](https://experienceleague.adobe.com/docs/?lang=jaexperience-manager-64/administering/integration/livefyre.html).

### その他のリリース情報 {#additional-release-information}

instagramの非ビジネスユーザーアカウントからのコンテンツの集計に影響する更新により、お客様に代わってコメントを投稿したり、作成者からの返信を自動的に確認したりできなくなりました。 詳しくは、[こちら](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/)を参照してください。

>[!NOTE]
>
>Livefyre 機能パック 2.0.6 は、AEM Classic UI をサポートしていません。

#### 新機能または改善点 {#new-feature-or-improvement}

* Livefyre で権限リクエストソーシャルアカウントを設定する前に、UGC を検索する機能を追加しました。 ソーシャルアカウントを設定して権限をリクエストするか、コンテンツを所有している場合は権限リクエストを上書きする必要があります。
* InstagramとTwitter [UGC 権限リクエストワークフロー](https://experienceleague.adobe.com/docs/experience-manager-64/administering/integration/livefyre.html?lang=ja-JP) は、最新の API に準拠するように更新されました。
* 権限ステータスと適切なアクションが、権限リクエスト画面に表示されます。

#### バグ修正 {#bug-fixes}

* AEMで UGC ライブラリを読み込む際に、権限リクエストに使用する Livefyre Studio でソーシャルアカウントを削除するとエラーが発生する問題を修正しました。
* Livefyre Studio のアセット数がAEM UGC ライブラリのアセット数と一致しない問題を修正しました。
* UGC ライブラリで、フィルターオプションがリセットされた後にフィルターされた結果が表示される問題を修正しました。
* AEM Commerce で、コールトゥアクションボタンをクリックすると誤った URL にリダイレクトされる問題を修正しました。
* AEM Sitesで、複数のコンポーネントを parsys プレースホルダーにドラッグ&amp;ドロップすると、コンポーネントが表示されなくなる問題を修正しました。
* 権限リクエストを送信する際に、無効になったソーシャルアカウントを選択できる問題を修正しました。
* UGC を Assets から Sites にドラッグ&amp;ドロップするとエラーが発生する問題を修正しました。
* Chat および Liveblog コンポーネントを Sites にドラッグ&amp;ドロップしてもアプリが作成されない問題を修正しました。
* ユーザーがコメントを試みるとコメントアプリがエラーを生成していた問題を修正しました。
* Livefyre Media Wall アプリをサイトに追加すると Java コンテンツリポジトリに余分なノードが作成される問題を修正しました。
* instagram UGC 検索で改ページやコンソールエラーが発生する問題を修正しました。
* instagramのユーザーアイコンが Assets で API エラーを生成していた問題を修正しました。
* 事前に定義された形式で、レビューアプリがサイトに追加されていた問題を修正しました。
* タッチ操作対応 UI 機能とインライン編集の問題を修正しました。
* 特定のInstagram画像アセットの読み込み時にエラーが発生する問題を修正しました。
* AEMの Livefyre HTTP Client がプロキシ設定をサポートしていなかった問題を修正しました。
