---
title: インタラクティブ通信の概要
seo-title: Interactive Communications Overview
description: この記事では、インタラクティブ通信の概要、サンプルのユースケース、作成ワークフロー、インタラクティブ通信とレターの違いについて説明します。
seo-description: Interactive Communication key capabilities, sample use cases, creation workflow, and differences between Interactive Communication and Correspondence Management
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
topic-tags: interactive-communications, introduction
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
exl-id: 386fc8b2-c92d-4731-8445-1bb6af54fd98
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 69%

---

# インタラクティブ通信の概要 {#interactive-communications-overview}

この記事では、インタラクティブ通信の概要、サンプルのユースケース、作成ワークフロー、インタラクティブ通信とレターの違いについて説明します。

![](do-not-localize/correspondence-management.png)

Interactive Communications は、ビジネス通信、ドキュメント、声明書、福利厚生通知、マーケティングメール、請求、ウェルカムキットなど、安全でパーソナライズされたインタラクティブな通信の作成、アセンブリ、配信を一元化および管理します。

## 主な機能 {#key-capabilities}

以下に、インタラクティブ通信の主要な機能を示します。

* すぐに使用できる、フォームデータモデルとの統合機能が付属しています。この機能により、バックエンドのデータベースと、MS® Dynamics などの CRM システムに簡単にアクセスすることができます。
* 印刷チャネルと Web チャネル用の統合オーサリングインターフェイスが用意されています。このインターフェイスにより、印刷チャネルから Web チャネルを自動的に生成することができます。
* 印刷チャネルと Web チャネルでグラフを使用して、視覚的に分かりやすい形式で情報を表現することができます。
* ドキュメントフラグメントで、ルールエディターとフォームデータモデルを使用することができます。
* エージェントのユーザーインターフェイスに、インタラクティブ通信の印刷と Web プレビューが表示されます
* ドラッグアンドドロップ操作でコンポーネントを配置し、印刷チャネルと Web チャネルを短時間で作成することができます。

## サンプルの使用例 {#sample-use-case}

この [クレジットカードのお客様向けのウェルカムキット](/help/forms/using/finance-reference-site-walkthrough.md#credit-card-application-walkthrough) 使用例の例は、インタラクティブ通信の機能を示しています。

## インタラクティブ通信の作成  {#interactive-communication-creation}

![interactive_communication-01](assets/interactive_communication-01.jpg)

### ワークフロー {#workflow}

インタラクティブ通信を作成するには、 [構築ブロック](#buildingblocks) インタラクティブ通信の準備が整ったら、次の手順を実行します。

1. 選択して [インタラクティブ通信の作成](/help/forms/using/create-interactive-communication.md).

1. [フォームデータモデル](/help/forms/using/data-integration.md)、事前入力サービス、[印刷チャネルと Web チャネルのテンプレート](/help/forms/using/web-channel-print-channel.md)を指定します。印刷チャネルから Web チャネルを生成することもできます。

1. の使用 [ドラッグ&amp;ドロップインターフェイス](/help/forms/using/introduction-interactive-communication-authoring.md)必要に応じて、ドキュメントフラグメント、画像、コンポーネントをインタラクティブ通信の印刷チャネルと Web チャネルに追加します。
1. 追加したコンポーネントのプロパティを設定します。例えば、以下のようなコンポーネントがあります。

   1. 画像
   1. [テーブル](/help/forms/using/create-interactive-communication.md#tables) （レイアウトフラグメントを含む）
   1. [グラフ](/help/forms/using/chart-component-interactive-communications.md)
   1. [ドキュメントフラグメント](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. 印刷チャネルと Web チャネルのプレビューを表示し、必要に応じてインタラクティブ通信を編集します。
1. エージェントはエージェント UI を使用して、インタラクティブ通信を受信者または後処理に送信するための[準備](/help/forms/using/prepare-send-interactive-communication.md)を行います。

### 構築ブロック {#buildingblocks}

インタラクティブ通信を作成するために必要な構築ブロックを以下に示します。

* [フォームデータモデル](/help/forms/using/data-integration.md)
* [印刷チャネルと Web チャネルのテンプレート](/help/forms/using/web-channel-print-channel.md)
* [ドキュメントフラグメント](/help/forms/using/document-fragments.md)
* 画像
* [テーマ](/help/forms/using/themes.md) （Web チャネル用）

## インタラクティブ通信と Correspondence Management の比較 {#interactive-communications-vs-correspondence-management}

インタラクティブ通信は、顧客とのコミュニケーションを作成するためのデフォルトの推奨される方法です。 AEM 6.3 Forms または AEM 6.2 Forms で作成したレターを引き続き使用する場合は、[互換性パッケージをインストールする必要があります](/help/forms/using/compatibility-package.md)。次に、インタラクティブ通信の機能とレターの機能の比較を示します。

<table> 
 <tbody>
  <tr>
   <td><strong>機能</strong></td> 
   <td><strong>インタラクティブコミュニケーション</strong></td> 
   <td><strong>レター</strong></td> 
  </tr>
  <tr>
   <td>出力</td> 
   <td>印刷出力と Web 出力</td> 
   <td>印刷出力</td> 
  </tr>
  <tr>
   <td>スキーマ</td> 
   <td>フォームデータモデル </td> 
   <td>データディクショナリ </td> 
  </tr>
  <tr>
   <td>ローカリゼーション</td> 
   <td>フォームデータモデルではサポートされていない</td> 
   <td>データディクショナリでサポートされている</td> 
  </tr>
  <tr>
   <td>ルールエディター</td> 
   <td>
    <ul> 
     <li>テキストと条件でルールエディターを使用して、インライン条件を作成できる</li> 
     <li>インタラクティブ通信エディターで、Web チャネルのコンポーネントにルールを適用できる</li> 
    </ul> </td> 
   <td>条件式を作成するための UI はない</td> 
  </tr>
  <tr>
   <td>オーサリング</td> 
   <td>ドラッグアンドドロップ方式のインターフェイスを使用して、印刷チャネルと Web チャネルを作成できる</td> 
   <td>ドラッグ&amp;ドロップメカニズムなし </td> 
  </tr>
  <tr>
   <td>グラフ</td> 
   <td>印刷チャネルと Web チャネルでグラフがサポートされている</td> 
   <td>サポートされていない</td> 
  </tr>
  <tr>
   <td>テーマ</td> 
   <td>テーマを使用して Web チャネルのスタイルを設定できる</td> 
   <td>テーマはサポートされていない</td> 
  </tr>
  <tr>
   <td>監査とバージョン管理</td> 
   <td>サポートされていない</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>下書きとインスタンスの管理</td> 
   <td>サポートされていない</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>バッチ処理</td> 
   <td>サポート対象 </td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>エージェント署名</td> 
   <td>サポートされていない</td> 
   <td>サポート対象</td> 
  </tr>
  <tr>
   <td>リモート関数</td> 
   <td>サポートされていない</td> 
   <td>サポート対象</td> 
  </tr>
 </tbody>
</table>
