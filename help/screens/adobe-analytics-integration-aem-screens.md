---
title: 'Adobe Analytics と AEM Screens の統合 '
seo-title: Adobe Analytics と AEM Screens の統合
description: ここでは、標準で利用できる、AEM Screens と Adobe Analytics の統合について説明し、提供される再生検証機能についても紹介します。
seo-description: ここでは、標準で利用できる、AEM Screens と Adobe Analytics の統合について説明し、提供される再生検証機能についても紹介します。
uuid: f4f71c85-ab6b-4e4d-94d3-5ba55ec0a246
contentOwner: jsyal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
topic-tags: administering
discoiquuid: 2784b590-3402-492f-94a6-36fe16633e89
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340

---


# Adobe Analytics と AEM Screens の統合{#adobe-analytics-integration-with-aem-screens}

>[!CAUTION]
>
>この AEM Screens 機能は、AEM 6.4.2 機能パック 2 と AEM 6.3.3 機能パック 4 がインストールされている場合にのみ使用できます。

>このいずれかの機能パックにアクセスするには、アドビサポートに連絡してアクセス権をリクエストする必要があります。アクセス権が付与されると、パッケージ共有から機能パックをダウンロードできるようになります。
>
ここでは、以下のトピックについて説明します。

* **概要**
* **アーキテクチャの詳細**
* **プロパティの設定**

## 概要 {#overview}

***AEM Screens*** で Adobe Analytics を活用することにより、特定の場所に表示されるコンテンツと他のデータソースとの関連性を探るのに役立つユニークなクロスチャネル分析を実現できます。

AEM Screens は、標準で Adobe Analytics と統合されており、再生検証機能を提供します。

ここでは、AEM Screens プロジェクトと Adobe Analytics の連携に関係する以下の機能について説明します。

* デバイス別の再生検証レポートが可能
* アセット別の再生検証レポートが可能
* すべてのプレーヤーイベントをキャプチャしタイムスタンプを設定できる
* 再生がネットワークに接続されていない場合、すべてのプレーヤーイベントをローカルに保存できる

Adobe Analytics と AEM Screens の統合により、*次の*&#x200B;目標を達成できます。

* デジタルサイネージの実装による ROI の実現
* 使用状況情報の収集と分析を将来可能にする基盤として Analytics を統合

## アーキテクチャの詳細 {#architectural-details}

次のアーキテクチャ図では、Adobe Analytics と AEM Screens の統合について説明しています。

![screen_shot_2018-09-12at85611am](assets/screen_shot_2018-09-12at85611am.png)

## AEM Screens での Adobe Analytics の有効化 {#enabling-adobe-analytics-in-aem-screens}

Adobe Analytics の設定は、OSGi コンソールから指定できます。

**Adobe Experience Manager Web コンソール設定**&#x200B;に移動して、次の図のように Adobe Analytics を AEM Screens 用に設定します。

![screen_shot_2018-09-04at25550pm](assets/screen_shot_2018-09-04at25550pm.png)

### プロパティの設定 {#configuring-the-properties}

>[!CAUTION]
プロパティを設定する前に、アドビのリレーションシップマネージャーに連絡して、AEM Screens で使用する **Analytics API キー**&#x200B;と **Analytics プロジェクト**&#x200B;を取得するためのチケットを作成してください。

Adobe Analytics を AEM Screens 用に設定するためのプロパティとその説明を次の表に示します。

<table> 
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td> 
   <td><strong>説明</strong></td> 
  </tr>
  <tr>
   <td><strong>Analytics URL</strong></td> 
   <td>プレーヤーから得られる分析データを投稿するための URL<br /> </td> 
  </tr>
  <tr>
   <td><strong>Analytics API キー</strong></td> 
   <td>Adobe Analytics サーバーに対して認証をおこなうための API キー（アカウントマネージャーから提供される）</td> 
  </tr>
  <tr>
   <td><strong>Analytics プロジェクト</strong></td> 
   <td>データを受け取るように Analytics 上で設定された AEM Screens プロジェクト（アカウントマネージャーから提供される）</td> 
  </tr>
  <tr>
   <td><strong>環境</strong></td> 
   <td><p>ステージング環境または実稼動環境。</p> <p><em>開発／ステージング環境の場合</em> - https://cc-api-data-stage.adobe.io/ingest/<br /><em>プロダクション環境の場合</em> - https://cc-api-data.adobe.io/ingest/</p> </td> 
  </tr>
  <tr>
   <td><strong>分析送信頻度</strong></td> 
   <td>プレーヤーから分析データを送信する間隔（分）。デフォルトでは 15 分に設定されています。</td> 
  </tr>
 </tbody>
</table>

>[!NOTE]
デフォルトでは、分析送信頻度は 15 分です。

#### AEM Screens での Adobe Analytics サービスの使用 {#using-adobe-analytics-service-in-aem-screens}

このシナリオでは、ファームウェアや機器の Screens コアコンポーネントに実装されている Analytics サービスから REST 呼び出しを通じて Analytics API を呼び出して、特定の使用例に固有のイベントを明示的に作成および送信しつつ、カスタム開発したチャネルから任意のカスタムメッセージを Analytics に送信できる拡張性も備えています。

Analytics イベントは、IndexedDB にオフラインで保存され、後でまとめてクラウドに送信されます。

>[!NOTE]
To learn more about the ***Sequencing*** and ***Standard Data Model for Events***, please refer to [Configuring Adobe Analytics for AEM Screens](configuring-adobe-analytics-aem-screens.md) in Developer&#39;s section of AEM Screens.

