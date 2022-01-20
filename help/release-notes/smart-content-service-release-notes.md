---
title: スマートコンテンツサービスのリリースノート
seo-title: Smart Content Service Release Notes
description: スマートコンテンツサービスの概要と、サービスに関する既知の問題です。
seo-description: Overview of the Smart Content Service and known issues around the service.
uuid: 5f474b36-3451-48ea-8669-b2d793638b06
content-type: reference
products: SG_EXPERIENCEMANAGER
discoiquuid: 9f88c773-ddeb-4c66-ac07-7d3aa196c51b
exl-id: 6e7ac9d2-7181-48bb-82c4-61a90e594ff5
source-git-commit: a842c45f0a0597f4c7f143974a550874258e5382
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 17%

---

# スマートコンテンツサービスのリリースノート {#smart-content-service-release-notes}

スマートコンテンツサービスの概要と、サービスに関する既知の問題です。

組織では、従業員、パートナーおよび顧客がデジタルアセットを参照および検索する際に使用する分類に基づいてデジタルアセットをタグ付けする必要があります。 汎用タグと比べて、ビジネス上の分類に基づいてタグ付けされたアセットは、タグベースの検索でより簡単に識別および取得できます。

スマートコンテンツサービスは、AEM Assetsのビジネス上の分類を使用してデジタルアセットに自動的にタグ付けし、最も関連性の高いアセットを検索時に表示します。

ビジネス上の分類を認識するには、厳選されたAEMアセットとタグのセットでスマートコンテンツサービスのトレーニングをおこなう必要があります。 トレーニングが終わると、サービスは類似のアセットセットにこれらのタグを適用できます。

スマートコンテンツサービスは、Adobe Senseiプラットフォームを活用して、ビジネス上の分類に基づいて画像認識アルゴリズムのトレーニングをおこなうことができます。 このコンテンツインテリジェンスを利用して、類似のアセットに関連性の高いタグが付加されます。

## 主な改善点 {#key-improvements}

スマートコンテンツサービスには、次の主な改善点が含まれています。

* アルゴリズムの最適化により、モデルの精度と再現率の値をさらに向上
* テナントレベルのすべてのタグのモデルトレーニングのリセットをサポート
* 競合を回避するための拡張スマートタグ名前空間のサポート
* 再トレーニングによる劣化を回避する新しいモデル置換ポリシー
* サービス使用のテナントごとの監視
* クラスタリングと接続に関する問題が修正され、サービスの堅牢性が向上しました。

## 修正された問題 {#fixed-issues}

このリリースでは、次の問題が修正されました。

* MySQL サーバーに接続できない場合、タグ付けおよびトレーニングワークフローのワーカープロセスは終了します。 CQ-4242886

* 精度のバイアススコアが正しく計算されません。 CQ-4241797

* モデルの PR 計算が正しくありません。 CQ-4241381

* トレーニングワークフローで、キューのサンプルアセットを処理する際にサンプルアセットが失われる CQ-4240901

* 精度の再現率の向上。 CQ-4239895

* モデルの置き換えポリシー。 CQ-4239886

* 男性用シャツの画像には、女性用ジャケットタグがタグ付けされています。 CQ-4239650

* ステージのデプロイメントでは、トレーニング例に記載されていません。 CQ-4239483

* トレーニングジョブでの検証は、トレーニング用に送信された一連のアセットに対しておこなわれます。 CQ-4238834

* タグに最小の陽性/否定が存在する場合でも、負の計算ではモデルの作成が失敗します。 CQ-4240741

* トレーナーログのネガティブフォーレージに対して誤解を招くエントリ。 CQ-4240738

* トレーニング用に送信されたタグが互いにランダムな否定である場合の、初回のトレーニングに関する問題。 CQ-4240118

* ログを即興化してテナントごとのサービス使用状況を監視します。 CQ-4239781

## 言語 {#languages}

スマートコンテンツサービスは、次のロケールで使用できます。

* 英語
* ドイツ語
* フランス語
* スペイン語
* イタリア語
* ポルトガル語
* 日本語
* 簡体字中国語
* 韓国語

## リンク {#links}

* [Adobe Experience Manager 製品ページ（adobe.com）](https://www.adobe.com/marketing-cloud/experience-manager.html)
* [拡張スマートタグのドキュメント](/help/assets/enhanced-smart-tags.md)

## 製品のアクセスとサポート（制限付きサイト） {#product-access-and-support-restricted-sites}

以下のサイトは既存ユーザーのみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにご連絡ください。

* [製品へのアクセス](https://login.experiencecloud.adobe.com/exc-content/login.html)
* [licensing.adobe.com での製品のダウンロード](https://licensing.adobe.com/).
* の追加機能に関する製品アップデート、パッチ、パッケージ [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* [Admin Console](https://adminconsole.adobe.com/). 詳しくは、 [新しいAdobeカスタマーサポートエクスペリエンス](https://docs.adobe.com/content/help/en/customer-one/using/home.html).
