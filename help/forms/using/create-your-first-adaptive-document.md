---
title: 発行しない最初のアダプティブドキュメントの作成
seo-title: 発行しない最初のアダプティブドキュメントの作成
description: 'null'
seo-description: 'null'
page-status-flag: de-activated
uuid: 2cb2bf82-130f-4d6b-a711-df0b97cb0504
discoiquuid: f3ca177f-7c0d-4b8b-ab4b-bf04668d634c
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340

---


# 発行しない最初のアダプティブドキュメントの作成 {#do-not-publish-create-your-first-adaptive-document}

## ユースケース {#use-case}

We Finance社は、金融サービス業界の主要な組織で、多様な顧客プロファイルの要件に合わせて、包括的でパーソナライズされた金融ソリューションを提供します。

顧客の自動保険の1つが期限切れになり、リマインダーを送信します。リマインダーはインタラクティブで、更新見積もり付きのPDFを含みます。 このコミュニケーションには、忠誠度の報酬や割引のオファーなど、他の情報も含まれます。

ポータルはAdobe AEM上で実行されます。 Webおよび印刷のウェルカムチャネル出力は、アダプティブドキュメントのマルチチャネル機能を使用して作成されます。

チュートリアルの最後に、次のようなアダプティブドキュメントが用意されています。[ ad-1 ![ad-2初のアダプティブドキュメ](assets/ad-1.png)](https://blogs.adobe.com/contentcorner/files/2017/07/PAF_Mobile.pdf)[![](assets/ad-2.png)](https://blogs.adobe.com/contentcorner/files/2017/07/PAF_Desktop.pdf)ントの作成は、手順に分類されます。 各ステップは、それ自体が完全な記事です。

<table> 
 <tbody>
  <tr>
   <th>君は学ぶ</th> 
   <th>
    <ul> 
     <li>アダプティブドキュメントおよびフォームデータモデルの作成</li> 
     <li>アダプティブドキュメント用のテンプレートとテーマの作成</li> 
     <li>ルールエディターを使用したビジネスルールの作成。<br /> </li> 
     <li>Publishing an adaptive document. <br /> </li> 
    </ul> </th> 
  </tr>
  <tr>
   <td>前提条件</td> 
   <td>
    <ul> 
     <li>AEM作成者インスタンスを設定します。 </li> 
     <li>AEM Forms アドオンのインストール. 詳しくは、「AEM Formsのインスト <a href="/help/forms/using/installing-configuring-aem-forms-osgi.md" target="_blank">ールと設定」を参照してください</a>。</li> 
     <li>JDBC データベースドライバー（JAR ファイル）をデータベースプロバイダーから取得します。このチュートリアルの例は、MySQLデータベースに基づいており、OracleのMySQL JDBCデータベースドライバーを使用しています。 </li> 
     <li>顧客データを含むデータベースを設定します。 アダプティブドキュメントを作成するには、データベースが必要です。 このチュートリアルではデータベースを使用して、AEM Forms のフォームデータモデルと永続性機能を表示します。 </li> 
     <li>印刷およびWebチャネル用のテンプ <a href="/help/forms/using/web-channel-print-channel.md">レートを作成/読み込み、有効にしま</a>す。</li> 
     <li>FDMに基づくドキュメ <a href="/help/forms/using/document-fragments.md">ント・フラグメントがあることを確認します</a>。</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

## 手順 1：フォームデータモデルを作成する {#step-create-form-data-model}

フォームデータモデルを使用すると、アダプティブドキュメントを異なるデータソースに接続できます。 例えば、AEM ユーザープロファイル、RESTful Web サービス、SOAP ベースの Web サービス、OData サービス、関連データベースなどに接続することができます。フォームデータモデルは、接続されたデータソースで使用可能なビジネスエンティティとサービスの統一されたデータ表現スキーマです。アダプティブドキュメントでフォームデータモデルを使用して、接続されたデータソースからデータを取得できます。 For more information about form data model, see [AEM Forms Data Integration](/help/forms/using/data-integration.md).

ゴール:

* データベースインスタンス(Microsoft Dynamics)をデータソースとして構成する
* Microsoft Dynamicsをデータソースとして使用してフォームデータモデルを作成する
* データモデルオブジェクトをフォームデータモデルに追加する
* フォームデータモデルの読み取りサービスと書き込みサービスを設定する
* テストデータを使用して、フォームデータモデルと設定済みサービスをテストする

## Step 2: Create an adaptive document {#step-create-an-adaptive-document}

Customer Communicationsは、ビジネスの通信、レター、ドキュメント、明細、給付通知、資産管理の目論見書、マーケティング・メール、請求書、ウェルカムキットなど、パーソナライズされた安全なインタラクティブな通信の作成、アセンブリ、配信を集中管理します。

アダプティブドキュメントを使用すると、本来魅力的で、レスポンシブ、動的、アダプティブな顧客コミュニケーションを作成できます。 AEM formsは、アダプティブドキュメントを作成するためのドラッグ&amp;ドロップWYSIWYGエディターを提供します。

<!--`For more information about adaptive documents, see [Introduction to authoring adaptive documents](/forms/using/introduction-ad-authoring.md).`-->

ゴール:

* フォームデータモデルに基づいてアダプティブドキュメントの印刷およびWeb出力を作成します。
* 顧客に情報を表示するためのアダプティブフォームのレイアウトフィールド
* フォームデータモデルからアダプティブドキュメントに情報を取得し、表示するルールを作成します。

<!--![see-the-guide-sm](assets/see-the-guide-sm.png)-->

## 手順3:アダプティブドキュメントフィールドへのルールの適用（Webチャネルのみ） {#step-apply-rules-to-adaptive-document-fields-web-channel-only}

アダプティブドキュメントには、アダプティブドキュメントオブジェクトにルールを記述するためのエディターが用意されています。 これらのルールは、ドキュメントに対して事前設定された条件とユーザーアクションに基づいて、ドキュメントオブジェクトに対してトリガーするアクションを定義します。 アダプティブドキュメントのWebバージョンの精度を確保し、ユーザーエクスペリエンスを高速化するのに役立ちます。 アダプティブドキュメントのルールとルールエディターの詳細については、「ルールエディター」 [を参照してくださ](/help/forms/using/rule-editor.md)い。

ゴール:

* アダプティブドキュメントのWebチャネルフィールドの作成と適用
* ルールを使用してWebチャネル内のドキュメントデータモデルサービスをトリガーする

## 手順4:アダプティブドキュメントのスタイル設定（Webチャネルのみ） {#step-style-the-adaptive-document-web-channel-only}

アダプティブドキュメントには、アダプティブドキュメントのテーマやインラインスタイルを作成するためのエディターが用意されています。 テーマには、コンポーネントとパネルのスタイル設定の詳細が含まれ、異なるドキュメントのWebチャネルでテーマを再利用できます。 スタイルには、背景色、状態色、透明度、配置、およびサイズなどのプロパティが含まれます。テーマをドキュメントに適用すると、指定したスタイルはドキュメントの対応するコンポーネントに反映されます。 詳しくは、「[テーマ](/help/forms/using/themes.md)」を参照してください。

ゴール:

* アダプティブドキュメントのWebチャネル用のテーマの作成
* アダプティブドキュメントのWebチャネルへのテーマの適用
* モバイルデバイスおよびデスクトップ上でのアダプティブドキュメントのWebチャネルの外観の検証

## 手順5:アダプティブドキュメントの発行 {#step-publish-the-adaptive-document}

アダプティブドキュメントの作成が完了したら、そのアダプティブドキュメントを発行インスタンスで使用できるようにするには、そのアダプティブドキュメントを発行する必要があります。

アダプティブドキュメントを発行するには、ドキュメント作成者が必要な権限を持っている必要があります。
