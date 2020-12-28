---
title: Smart Content Serviceリリースノート
seo-title: Smart Content Serviceリリースノート
description: Smart Content Serviceの概要と、サービスに関する既知の問題です。
seo-description: Smart Content Serviceの概要と、サービスに関する既知の問題です。
uuid: 5f474b36-3451-48ea-8669-b2d793638b06
content-type: reference
products: SG_EXPERIENCEMANAGER
discoiquuid: 9f88c773-ddeb-4c66-ac07-7d3aa196c51b
translation-type: tm+mt
source-git-commit: f8ba597c62379ba413309303c2ad066ab7afce1e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 17%

---


# Smart Content Serviceリリースノート{#smart-content-service-release-notes}

Smart Content Serviceの概要と、サービスに関する既知の問題です。

組織は、従業員、パートナー、および顧客がデジタルアセットを参照および検索する際に使用する分類に基づいて、デジタルアセットにタグ付けする必要があります。 一般的なタグと比較して、ビジネスタクソノミに基づいてタグ付けされたアセットは、タグベースの検索によって、より簡単に識別および取得できます。

Smart Content Serviceは、ビジネス分類であるAEM Assetsを使用してデジタルアセットに自動的にタグ付けを行い、最も関連性の高いアセットを検索に表示します。

ビジネス分類を認識するために、AEMアセットとタグの厳選されたセットに対してSmart Content Serviceをトレーニングする必要があります。 トレーニングが終わると、サービスはこれらのタグを類似のアセットに適用できます。

Smart Content Serviceは、Adobe Sensei・プラットフォームを基盤としており、このプラットフォームを使用して、ビジネス分類に基づいて画像認識アルゴリズムをトレーニングできます。 このコンテンツインテリジェンスを利用して、類似のアセットに関連性の高いタグが付加されます。

## キーの改善{#key-improvements}

Smart Content Serviceには、次の主な機能強化が含まれています。

* アルゴリズムの最適化により、モデルの精度、再現率の値をさらに改善
* テナントレベルのすべてのタグに対するモデルトレーニングのリセットのサポート
* 競合を回避するための拡張スマートタグ名前空間のサポート
* 再トレーニングによる劣化を回避する新しいモデル交換ポリシー
* テナントごとの監視によるサービスの使用
* クラスタリングと接続に関する問題が修正され、サービスの堅牢性が向上しました。

## 修正された問題 {#fixed-issues}

このリリースでは、次の問題が修正されました。

* タグ付けおよびトレーニングワークフローのワーカープロセスは、MySQLサーバーに接続できない場合に終了します。 CQ-4242886

* 精度のバイアススコアが正しく計算されません。 CQ-4241797

* モデルのPR計算が正しくありません。 CQ-4241381

* トレーニングワークフローで、キューCQ-4240901からサンプルアセットを処理する際にサンプルアセットが見つからない

* 精密再現の改善。 CQ-4239895

* モデル置き換えポリシー。 CQ-4239886

* 男性用シャツの画像には、女性用ジャケットタグでタグが付けられます。 CQ-4239650

* トレーニングの例は、ステージでの導入では見逃しています。 CQ-4239483

* トレーニングジョブの検証は、トレーニング用に送信された一連のアセットに対して実行されます。 CQ-4238834

* タグに最小の肯定/否定が存在する場合でも、負のフォールアップではモデルの作成に失敗します。 CQ-4240741

* トレーナーログでの除外フォールアップに対して誤ったエントリが発生する。 CQ-4240738

* トレーニング用に送信されたタグがお互いにランダムな否定である場合、初回のトレーニングに問題があります。 CQ-4240118

* ログを即時に作成し、テナントごとのサービスの使用状況を監視します。 CQ-4239781

## 言語 {#languages}

Smart Content Serviceは、次のロケールで使用できます。

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
* [スマートタグドキュメントの強化](/help/assets/enhanced-smart-tags.md)

## 製品のアクセスとサポート（制限付きサイト）{#product-access-and-support-restricted-sites}

以下のサイトは既存ユーザーのみが参照できます。アクセス権を必要とするお客様は、アドビのアカウントマネージャーにご連絡ください。

* [製品へのアクセス](https://login.marketing.adobe.com)
* [licensing.adobe.com での製品のダウンロード](https://licensing.adobe.com/).
* [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)の追加機能に対する製品アップデート、パッチ、パッケージ。
* [Admin Consoleを介したカスタマーサポート](https://adminconsole.adobe.com/)。詳しくは、[新しいAdobeカスタマーサポート体験](https://docs.adobe.com/content/help/en/customer-one/using/home.html)を参照してください。
