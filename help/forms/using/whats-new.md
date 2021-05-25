---
title: 新機能の概要 | AEM 6.4 Forms
seo-title: 新機能の概要 | AEM 6.4 Forms
description: AEM 6.4 Forms の新機能と機能強化の概要
seo-description: AEM 6.4 Forms の新機能と機能強化の概要
uuid: 152068ec-47a8-43f4-b9c8-3a17d1f085fe
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: introduction
discoiquuid: 436aa424-d05e-4f3d-90ac-5ff3b05ddba8
exl-id: 21b8ed83-9c0c-41ee-9fbb-56ccebaee132
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2016'
ht-degree: 81%

---

# 新機能の概要 | AEM 6.4 Forms {#new-features-summary-aem-forms}

AEM 6.4 Forms の新機能と機能強化の概要

AEM Forms に、いくつかの新機能と機能強化が導入されました。これにより、アダプティブフォームとインタラクティブ通信の作成と管理がさらに簡素化され、ユーザーエクスペリエンスが向上します。

ここでは、これらの新機能と機能強化について簡単に説明します。詳しくは、各リソースのドキュメントを参照してください。また、AEM 6.4 Forms の[リリースノート](/help/release-notes/forms.md)も参照してください。AEM 6.4 Formsに関する完全なドキュメントについては、『[AEM 6.4 Formsガイド](/help/forms/home.md)』を参照してください。

## インタラクティブコミュニケーション {#interactive-communications}

![correspondence-management](assets/correspondence-management.png)

Interactive Communicationsは、ビジネス通信、レター、ドキュメント、声明書、特典通知、資産管理の目論見書、マーケティングメール、請求、ウェルカムキットなど、安全でパーソナライズされたインタラクティブな通信の作成、アセンブリ、配信を一元化および管理します。

インタラクティブ通信では、アダプティブフォームと同じ基本的な技術、プロセス、コンポーネントを使用して、レスポンシブなマルチチャネル通信が作成されます。これは、レスポンシブなアダプティブフォームと非常によく似ています。

インタラクティブ通信には、次のような大きな利点があります。

* そのままの状態でフォームデータモデルに統合できるため、バックエンドデータベースと、MS Dynamics などの CRM システムに簡単にアクセスすることができます。
* 印刷チャネルと Web チャネル用の統合オーサリングインターフェイスが用意されています。
* 印刷チャネルと Web チャネルの両方で、ドラッグアンドドロップ操作をベースとするオーサリングインターフェイスを使用することができます。これは、アダプティブフォームのオーサリングインターフェイスに似ています。

インタラクティブ通信は、顧客通信を作成するためのデフォルトの方法です。顧客通信を作成する場合は、インタラクティブ通信を使用することをお勧めします。AEM 6.3 Forms と AEM 6.2 Forms のレターを引き続き使用する場合は、互換性のあるパッケージをインストールする必要があります。

### マルチチャネルのインタラクティブ通信の作成  {#multi-channel-interactive-communication-authoring}

インタラクティブ通信では、1 つのドキュメントエディターだけを使用して、印刷ドキュメントと Web ドキュメントの両方について、作成と編集を行うことができます。同じドキュメントフラグメントを使用して両方のチャネルのレンディションを作成することにより、同じ作業を繰り返し行う必要がなくなります。![printweb_2](assets/printweb_2.png)

詳しくは、「[インタラクティブ通信の概要](/help/forms/using/interactive-communications-overview.md)」を参照してください。

### WYSIWYG ドキュメントエディター {#wysiwyg-document-editor}

ドラッグアンドドロップ操作をベースとする WYSIWYG ドキュメントエディターは、作業しやすいエディターです。直感的なインターフェイス、ドラッグアンドドロップ機能、標準コンポーネント、データモデル、アセットの統合リポジトリにより、インタラクティブ通信を素早く簡単に作成することができます。

インタラクティブ通信を作成したり、既存の通信を編集したりするには、次の構成要素を使用できます。チャネル、コンテンツ、プロパティ、アセット、コンポーネント、データソースについて説明します。

![drag-n-drop-lf](assets/drag-n-drop-lf.png)

詳しくは、「[インタラクティブ通信のオーサリングの概要](/help/forms/using/introduction-interactive-communication-authoring.md)」を参照してください。

### インタラクティブ通信で、印刷コンテンツの Web 版を自動的に生成する {#auto-generate-web-version-from-print-content-in-interactive-communication}

作成者は、印刷ドキュメントからWebドキュメントのコンテンツを自動生成し、同じエディターで印刷ドキュメントとWebドキュメントの両方を作成、プレビュー、および編集できます。 インタラクティブ通信の作成者は、1回作成してすべてのチャネルにパブリッシュできます。 インタラクティブ通信の作成者は、印刷チャネルとWebチャネルで同じドキュメントフラグメントを使用して、作業の重複を防ぐことができます。

詳しくは、[印刷チャネルとWebチャネル](/help/forms/using/web-channel-print-channel.md)を参照してください。

### テーマを使用して、インタラクティブ通信の Web チャネルのスタイルを設定する {#use-themes-to-style-web-channel-of-interactive-communication}

インタラクティブ通信では、テーマがサポートされています。テーマを作成してインタラクティブ通信に適用することができます。テーマには、コンポーネントやパネルのスタイル設定の詳細が含まれています。異なるインタラクティブ通信で同じテーマを再利用することにより、インタラクティブ通信の外観とブランド表示を統一することができます。

AEM Formsには、インタラクティブ通信用の標準テーマが含まれています。 テーマを使用して、デバイス上で表示されるインタラクティブ通信の外観をカスタマイズすることもできます。

詳しくは、「[AEM Forms のテーマ](/help/forms/using/themes.md)」を参照してください。

### エージェントインターフェイスの機能強化 {#enhanced-agent-interface}

エージェントユーザーインターフェイスで、インタラクティブ通信の印刷チャネルと Web チャネルをプレビュー表示できるようになりました。同じエージェントユーザーインターフェイスから、マルチチャネルインタラクティブ通信の印刷チャネルとWebチャネルのプレビューを選択できます。 印刷チャネルのフィールド、変数、FDM 要素、ドキュメントフラグメントを、エージェントユーザーインターフェイスによって変更するように設定することができます。フォームデータモデルでは、事前に設定されたサンプルデータを使用して、プレビューを生成することができます。

詳しくは、[エージェントUI](/help/forms/using/prepare-send-interactive-communication.md)を使用したインタラクティブ通信の準備と送信を参照してください。

### グラフを使用して情報を表示する {#present-information-in-charts}

インタラクティブ通信の Web チャネルと印刷チャネルでグラフを使用すると、分かりやすい通信を作成することができます。円グラフ、ドーナツグラフ、棒グラフ、列グラフなどを使用して大量の情報を視覚的に表現することにより、内容を簡単に把握して情報を分析できるようになります。

![chart-2](assets/chart-2.png) ![チャート](assets/chart.png)

詳しくは、[Using charts in Interactive Communications](/help/forms/using/chart-component-interactive-communications.md)を参照してください。

### 付属のデータコネクタを使用してドキュメントにデータを取り込む {#out-of-the-box-data-connectors-to-prefill-documents}

インタラクティブ通信には、各種のビジネスツールにデータを統合するための機能が用意されています。これにより、CRM システムなど、複数の業務システムに接続し、データをカスタマイズしてドキュメント内に挿入することができます。

![fdm_ad](assets/fdm_ad.png)

詳しくは、「[フォームデータモデルの使用](/help/forms/using/using-form-data-model.md)」を参照してください。

### ドキュメントフラグメントエディターの機能強化 {#enhanced-document-fragment-editor}

インタラクティブ通信のドキュメントフラグメント内で、FDM の各種要素とルールを使用できるようになりました。

* フォームデータモデル要素のサポート
* ルールを使用して、アセットフラグメントやテキストフラグメントの表示と非表示を切り替えることができます。
* 要素や変数の値を検証することができます。
* 関数を実行して数式の値を計算する

詳しくは、次を参照してください。

* [インタラクティブ通信内のテキスト](/help/forms/using/texts-interactive-communications.md)
* [インタラクティブ通信内の条件](/help/forms/using/conditions-interactive-communications.md)

### 既存アセットの互換性パッケージ {#compatibility-package-for-existing-assets}

デフォルトでは、旧バージョンの AEM Forms のレターアセットは、このリリースではサポートされていません。AEM 6.3 Forms と AEM 6.2 Forms のレターを引き続き使用する場合は、互換性パッケージをインストールする必要があります。

## データ統合 {#data-integration}

![](do-not-localize/data-integeration-1.png)

[AEM Forms のデータ統合機能](/help/forms/using/data-integration.md)により、データベース、RESTful ベースの Web サービス、SOAP ベースの Web サービス、OData サービスなど、各種のデータソースを使用して、フォームデータモデルを作成することができます。アダプティブフォームとドキュメントでフォームデータモデルを使用して、データの連結、データの取り込み、サービスの呼び出しを行うことができます。

このリリースでは、データ統合機能に関して、いくつかの新しい機能と機能強化が導入されています。

### データソースを使用せずにフォームデータモデルを作成する {#create-form-data-model-without-data-source}

ビジネスユーザーとフォーム作成者は、データソースを設定することなく、フォームデータモデルと、フォームデータモデルのエンティティとプロパティを作成することができます。また、フォームデータモデルを使用して、アダプティブフォームとドキュメントを作成することができます。後で、フォームデータモデルをデータソースに連結することができます。フォームデータモデルを使用してフォームやドキュメントを作成する際に、データソースに依存する必要がなくなります。

同様に、既存のフォームデータモデル内でエンティティと子プロパティを作成し、そのエンティティとプロパティを、データソース内の対応するエンティティとプロパティに後から連結することができます。

詳しくは、「[フォームデータモデルの作成](/help/forms/using/create-form-data-models.md)」を参照してください。

### 計算済みプロパティの作成 {#create-computed-properties}

フォームの作成者と開発者は、フォームデータモデル内で計算済みプロパティを作成することができます。計算済みプロパティを使用して、設定済みデータソース内の有効なデータ上でルールやロジックを作成することにより、プロパティの値を計算することができます。ルールとは、フォームデータモデルにデータが読み込まれたとき、または式のプロパティの値が変更されたときに評価される式です。 例えば、Installments という計算済みプロパティの場合、データソース内で指定された利率と、フォーム内でユーザーが指定したローンの金額と期間に基づいて、毎月のローン支払額が計算されます。

計算済みプロパティはフォームデータモデル内に格納され、データソース内には存在しません。計算済みプロパティは、アダプティブフォームとインタラクティブ通信で使用することができます。

詳しくは、「[フォームデータモデルの操作](/help/forms/using/work-with-form-data-model.md)」を参照してください。

### サンプルデータを使用してフォームとドキュメントのプレビューを表示する {#preview-forms-and-documents-with-sample-data}

フォームデータモデル内のすべてのエンティティについて、サンプルデータを生成することができます。生成されたデータは、プロパティに対して設定されたデータタイプに対応します。フォームデータモデルに関連付けられたアダプティブフォームまたはドキュメントのプレビューを表示すると、事前に設定されたサンプルデータを使用してそのアダプティブフォームまたはドキュメントがレンダリングされます。

サンプルデータは、一連のランダムな値から構成されています。サンプルデータを生成するたびに、これらの値が変化します。ただし、サンプルデータを編集して保存してからサンプルデータを再生成しても、元のサンプルデータは保存されたままになります。例えば、「姓」プロパティと「名」プロパティのサンプルデータを編集して保存し、後で別のプロパティをフォームデータモデル内で追加してからサンプルデータを再生成すると、後から追加したプロパティには新しい値が表示されますが、その前に保存した「姓」プロパティと「名」プロパティには、保存したときの値が表示されます。

詳しくは、「[フォームデータモデル](/help/forms/using/using-form-data-model.md)の使用」を参照してください。

### データソース定義の更新 {#refresh-data-source-definitions}

データソースのエンティティやプロパティを更新しても、関連するフォームデータモデル内でその更新内容が自動的に反映されることはありません。フォームデータモデルエディターに、サーバーキャッシュを無効化し、更新されたスキーマをデータソースから取得してフォームデータモデルに即座に反映する![refresh_forms_di](assets/refresh_forms_di.png) （データソース定義の更新）が追加されました。

### タッチユーザーインターフェイスを使用したデータソースの設定 {#configure-data-sources-using-touch-user-interface}

このリリースでは、タッチユーザーインターフェイスを使用して、データソース用にクラウドサービスを設定できるようになりました。また、クラウドサービスを設定する場所が&#x200B;**[!UICONTROL ツール/Cloud Services/データソース]**&#x200B;に変更されました。 [データソースの設定](/help/forms/using/configure-data-sources.md)を参照してください。

## アダプティブフォーム {#adaptive-forms}

![simplification-of-authoring-forms-and-documents_hero-image_2](assets/simplification-of-authoring-forms-and-documents_hero-image_2.png)

### 遅延読み込み機能を強化してアダプティブフォームのパフォーマンスを改善 {#improve-performance-of-adaptive-forms-with-enhanced-lazy-loading}

アダプティブフォームの遅延読み込み機能を実行すると、フォームフラグメントの初期化が必要になるまで、その初期化が遅延されます。フォームのレンダリングにかかる時間を最小限に抑えることにより、サイズの大きなフォームのパフォーマンスが向上するため、結果としてユーザーエクスペリエンスが改善されます。

このリリースでは、遅延読み込み機能が以下のように改善されています。

* 遅延読み込み機能が有効になっているフォームフラグメントで、添付ファイルコンポーネントと利用規約コンポーネントを使用できるようになりました。
* 繰り返し可能パネルで、遅延読み込み機能が有効になっているアダプティブフォームフラグメントを使用できるようになりました。
* AEM Forms アプリケーションで、遅延読み込み機能が有効になっているアダプティブフォームを使用できるようになりました。

## フォームベースの AEM ワークフロー  {#forms-centric-aem-workflows}

![aem-forms-workflow-on-osgi-](assets/aem-forms-workflow-on-osgi-.png)

フォームベース AEM ワークフロー機能により、様々なタスクのワークフローを短時間で作成して OSGi スタック上にデプロイすることができます。Process Management 機能を JEE スタックにインストールする必要はないため、デプロイメントが簡素化され、アプリケーションサーバーとインフラストラクチャに関するコストも削減されます。詳しくは、「[OSGi でのフォームベースワークフロー](/help/forms/using/aem-forms-workflow.md)」を参照してください。

Forms中心型AEMワークフローの機能強化は次のとおりです。

* タッチユーザーインターフェイスでワークフローモデルエディターを使用できるようになりました。これにより、フォームベースの AEM ワークフローを短時間で作成できるようになります。
* 電子メールを送信するワークフローステップが改善されました。例えば、電子メールステップを使用して、ワークフローの完了時にレコードのドキュメントを送信することができます。
* ワークフローモデル内でフォームデータモデルを使用するワークフローステップが改善されました。これにより、カスタムコードを記述することなく、データ統合サービスを呼び出すことができます。例えば、カスタムコードを記述することなく GET サービスを呼び出して、データベースアーカイブから社員データを取得することができます。

## AEM Forms アプリケーション {#aem-forms-app}

![aem-forms-app](assets/aem-forms-app.png)

AEM Forms アプリを使用すると、フィールドワーカーはモバイルデバイスを AEM Forms サーバーと同期し、タスクを実行できます。オンフライン状態のデバイスにデータを保存し、デバイスをオンライン状態に戻してサーバー上のデータと同期する場合でも、このアプリケーションはシームレスに機能します。詳しくは、[AEM Formsアプリ](/help/forms/using/aem-forms-app.md)を参照してください。

AEM Forms アプリケーションの改善点を以下に示します。

* AEM Forms アプリケーションで、遅延読み込み機能が有効になっているアダプティブフォームを使用できるようになりました。
* AEM Forms アプリケーションで、フォームデータモデルが含まれているアダプティブフォームを使用できるようになりました。

## Document Security {#document-security}

![aem-forms-document-security-](assets/aem-forms-document-security-.png)

Document Security を使用すると、サポートされる形式で保存した情報を安全に配布できます。Document Security を使用して、許可されたユーザーだけがドキュメントを使用するように指定できます。Document Securityの主な変更点は次のとおりです。

* Document Security に、ドキュメントをローカルで保護するための[ポータブル保護ライブラリ（PPL）](/help/forms/using/document-security-offerings.md)が導入されました。ドキュメントが AEM Forms サーバーに送信されることはありません。ネットワーク経由で AEM Forms サーバーに送信されるのは、セキュリティ証明書とポリシーの詳細データだけです。AEM 6.4 Forms には、OSGi バンドル形式でポータブル保護ライブラリ（PPL）が導入されています。これにより、PPL を AEM Forms サーバーに直接インストールし、AEM の機能と PPL の機能を相互に組み合わせて使用することができます。
* Document Security の C++ SDK と C++ PPL ライブラリは、Microsoft Visual Studio 2013 を使用してコンパイルすることができます。以前はMicrosoft Visual Studio 2010がサポートされていました。

## サポートされているプラットフォーム {#supported-platforms}

サポート対象のオペレーティングシステム、アプリケーションサーバー、データベース、データベースドライバー、JDK サーバー、LDAP サーバー、電子メールサーバーを自由に組み合わせて、AEM Forms をセットアップすることができます。次に、サポートされるプラットフォームの主な変更点を示します。

<table> 
 <tbody> 
  <tr> 
   <td>コンポーネント</td> 
   <td>サポート対象として追加</td> 
   <td>サポート対象から除外</td> 
  </tr> 
  <tr> 
   <td>オペレーティングシステム</td> 
   <td> 
    <ul> 
     <li>Microsoft Windows Server 2016</li> 
     <li>Oracle Linux 7 Update 3</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>IBM AIX 7.2 <sup>[1]</sup><br /> </li> 
     <li>Solaris 11 <sup>[1]</sup></li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>アプリケーションサーバー<br /> </td> 
   <td> 
    <ul> 
     <li>Red Hat JBoss EAP 7</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>IBM Weblogic 12.1.3</li> 
     <li>IBM WebSphere 8.5.5</li> 
     <li>Red Hat JBoss EAP 6</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>データベース</td> 
   <td> 
    <ul> 
     <li>Microsoft SQL Server 2016</li> 
     <li>MySQL 5.7.19 以降</li> 
     <li>IBM DB2 11.1</li> 
     <li>Oracle Multitenant アーキテクチャ</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>Microsoft SQL Server 2012<br /> </li> 
     <li>Microsoft SQL Server 2014</li> 
     <li>MySQL 5.5</li> 
     <li>IBM DB2 10.5<br /> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>LDAP サーバー</td> 
   <td> 
    <ul> 
     <li>Microsoft Active Directory 2016</li> 
     <li>IBM Tivoli Directory Server 6.4</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>Microsoft Active Directory 2008</li> 
     <li>IBM Tivoli Directory Server 6.3</li> 
     <li>Oracle Directory Server Enterprise Edition 7.0</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>電子メールサーバー</td> 
   <td> 
    <ul> 
     <li>Microsoft Office 365</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>Novell Groupwise 7</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>コネクタ</td> 
   <td> 
    <ul> 
     <li>Connector for Microsoft Sharepoint 2016</li> 
     <li>Connector for EMC Documentum 7.3</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>Connector for Microsoft Sharepoint 2007</li> 
     <li>Connector for Microsoft Sharepoint 2010</li> 
     <li>Connector for IBM Filenet 5.0</li> 
     <li>Connector for EMC Documentum 6.7</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>ブラウザー</td> 
   <td> 
    <ul> 
     <li>Apple Safari 11.x（macOS）</li> 
     <li>Apple Safari 11.x（iOS 用）</li> 
    </ul> </td> 
   <td> 
    <ul> 
     <li>Blackberry ブラウザー（Blackberry Z30 デバイスおよび Q10 デバイス用）</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>AEM Forms アプリケーション<br /> </td> 
   <td> 
    <ul> 
     <li>Android 4.4 以降</li> 
     <li>Apple iOS 10 以降</li> 
    </ul> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

1. アップグレード実行した場合のみ、AIX オペレーティングシステムと Solaris オペレーティングシステムを使用することができます。
