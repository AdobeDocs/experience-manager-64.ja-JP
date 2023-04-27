---
title: 送信アクションの設定
seo-title: Configuring the Submit action
description: AEM Formsでは、送信アクションを設定して、送信後のアダプティブフォームの処理方法を定義することができます。 組み込みの送信アクションを使用することも、独自のアクションを一から書き込むこともできます。
seo-description: AEM Forms allows you to configure a submit action to define how an adaptive form is processed after submission. You can use built-in submit actions or write your own from scratch.
uuid: aa261e65-a1ec-402b-80de-0ba8a294e315
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: fea76f90-22d5-4836-9901-a35229401eb0
feature: Adaptive Forms
exl-id: 2a842bdc-6dcf-42cc-9a45-57ac15b79eb7
source-git-commit: f8b19b6723d333e76fed111b9fde376b3bb13a1d
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 57%

---

# 送信アクションの設定 {#configuring-the-submit-action}

## 送信アクションの概要 {#introduction-to-submit-actions}

送信アクションは、ユーザーがアダプティブフォームの「送信」ボタンをクリックするとトリガーされます。 アダプティブフォームで送信アクションを設定することができます。 アダプティブフォームには、すぐに使用できる送信アクションがいくつか用意されています。 デフォルトの送信アクションをコピーして拡張し、独自の送信アクションを作成することができます。 ただし、要件に応じて、送信したフォームのデータを処理する独自の送信アクションを書いて登録できます。

フォームが事前入力または送信されると、送信されたデータはAEM経由でルーティングされ、中間形式へのデータマッサージが行われます。 アダプティブフォームがAcrobat Sign、検証、フォームポータルのドラフト、送信、またはAEMワークフローを使用する場合を除き、データはAEMインスタンスに保存されません

サイドバーにある「アダプティブフォームコンテナ」プロパティの「**[!UICONTROL 送信]**」セクションで、送信アクションを設定できます。

![送信アクションの設定](assets/thank-you-setting.png)
**図：** *送信アクションの設定*

アダプティブフォームで使用できるデフォルトの送信アクションは次のとおりです。

* REST エンドポイントへの送信
* メールを送信
* メールでPDFを送信
* Forms ワークフローを起動
* フォームデータモデルを使用して送信
* フォームポータル送信アクション
* AEM ワークフローを起動

>[!NOTE]
>
>メールで PDF を送信アクションは、XFA テンプレートをフォームモデルとして使用しているアダプティブフォームにのみ使用できます。

>[!NOTE]
>
>[AEM_Installation_Directory]\crx-quickstart\temp\datamanager\ASM フォルダーが存在することを確認します。ディレクトリは、添付ファイルを一時的に保存するために必要になります。ディレクトリが存在しない場合は作成します。

>[!CAUTION]
>
>フォームテンプレート、フォームデータモデル、スキーマベースのアダプティブフォームのいずれかを、スキーマ（XML スキーマ、JSON スキーマ、フォームテンプレート、フォームデータモデルのいずれか）に準拠した XML データや JSON データを使用して[事前入力](/help/forms/using/prepopulate-adaptive-form-fields.md)する、つまりデータが &lt;afData>、&lt;afBoundData>、&lt;/afUnboundData> のタグを含まない場合、アダプティブフォームの連結されていないフィールド（連結されていないフィールドとは、[bindref](/help/forms/using/prepopulate-adaptive-form-fields.md) プロパティのないアダプティブフォームフィールドのこと）のデータは失われます。

使用事例を満たすために、アダプティブフォームのカスタム送信アクションを作成することができます。 詳しくは、「[アダプティブフォーム向けのカスタム送信アクションの作成](/help/forms/using/custom-submit-action-form.md)」を参照してください。

## REST エンドポイントへの送信 {#submit-to-rest-endpoint}

この **[!UICONTROL REST エンドポイントに送信]** 送信オプションでは、フォームに入力されたデータを HTTP データリクエストの一環として設定済みの確認ページにGETを渡します。 リクエストにフィールド名を追加できます。リクエストのフォーマットを以下に示します。

`{fieldName}={request parameter name}`

以下の画像に示されているように、`param1` および `param2` が、**[!UICONTROL textbox]** フィールドおよび **[!UICONTROL numericbox]** フィールドからコピーされた値を持つパラメーターとして、次のアクションに向けて渡されます。

**[!UICONTROL POST リクエストを有効にする]**&#x200B;ことで、リクエストを POST する URL を指定することもできます。フォームをホストする AEM サーバーにデータを送信するには、AEM サーバーのルートパスに対応する相対パスを使用します。例：/content/forms/af/SampleForm.html 他のサーバーにデータを送信するには、絶対パスを使用します。

![REST エンドポイント送信アクションの設定](assets/action-config.png)

REST エンドポイント送信アクションの設定

>[!NOTE]
フィールドを REST URL 内のパラメーターとして渡すには、すべてのフィールドが異なる要素名を持っている必要があります。これは、異なるパネルに置かれているフィールドにも適用されます。

### 送信されたデータをリソースまたは外部の REST エンドポイントに投稿  {#post-submitted-data-to-a-resource-or-external-rest-end-point-nbsp}

**[!UICONTROL REST エンドポイントへの送信]**&#x200B;アクションを使用して、送信されたデータを REST URL に POST できます。URL は、内部（フォームがレンダリングされるサーバー）または外部サーバーのどちらのものでも使用できます。

内部サーバーにデータを POST 送信するには、リソースのパスを指定します。データは、リソースのパスに POST されます。例えば、/content/restEndPoint です。このような POST リクエストには、送信リクエストの認証情報が使用されます。

外部サーバーにデータを POST 送信するには、URL を指定します。URL の形式は、https://host:port/path_to_rest_end_point です。POST リクエストを匿名で処理するためのパスを設定してください。

![「ありがとうございます」ページのパラメーターとして渡されたフィールド値のマッピング](assets/post-enabled-actionconfig.png)

上の例で、ユーザーが `textbox` に入力した情報は、パラメーター `param1` を使用して取得されます。`param1` を使用して取得されるデータを POST するための構文を以下に示します。

`String data=request.getParameter("param1");`

同様に、XML データと添付ファイルの投稿に使用するパラメータは次のとおりです `dataXml` および `attachments`.

例えば、この 2 つのパラメーターをスクリプト中で使用して、REST エンドポイントに送信されたデータを解析できます。データを格納および解析するための構文を以下に示します。

`String data=request.getParameter("dataXml");`\
`String att=request.getParameter("attachments");`

この例では、`data` が XML データを格納し、`att` が添付ファイルデータを格納します。

## メールを送信 {#send-email}

「**[!UICONTROL メールを送信]**」送信アクションでは、フォームの送信が完了すると同時に、1 人または複数の受信者にメールが送信されます。生成されるメールには、事前に定義された形式のフォームデータを含めることができます。

>[!NOTE]
フォームデータを電子メールに含めるには、異なるパネルに配置されている場合でも、すべてのフォームフィールドに異なる要素名を付ける必要があります。

## メールでPDFを送信 {#send-pdf-via-email}

「**[!UICONTROL メールで PDF を送信]**」送信アクションでは、フォームの送信が完了すると同時に、1 人または複数の受信者にフォームデータを含む PDF が添付されたメールが送信されます。

**注意：** *この送信アクションは、レコードのドキュメントテンプレートを持つ XFA ベースのアダプティブフォームおよび XSD ベースのアダプティブフォームで使用できます。*

## フォームワークフローを呼び出す {#invoke-a-forms-workflow}

この **[!UICONTROL Formsワークフローに送信]** 「送信」オプションを選択すると、データ xml および添付ファイル（存在する場合）が既存のAdobeLiveCycleまたは JEE 上のAEM Formsプロセスに送信されます。

送信アクション「フォームワークフローへの送信」の設定方法について詳しくは、 [フォームワークフローを使用したフォームデータの送信と処理](/help/forms/using/submit-form-data-livecycle-process.md).

## フォームデータモデルを使用して送信 {#submit-using-form-data-model}

「**[!UICONTROL フォームデータモデルを使用して送信]**」送信アクションでは、フォームデータモデルの特定のデータモデルオブジェクトで送信したアダプティブフォームデータをデータソースに書き込みます。送信アクションを設定する際に、データソースに書き戻す送信済みデータを持つデータモデルオブジェクトを選択できます。

さらに、フォームデータモデルとレコードのドキュメント (DoR) を使用して、フォームの添付ファイルをデータソースに送信できます。

フォームデータモデルについて詳しくは、「[AEM Forms のデータ統合機能](/help/forms/using/data-integration.md)」を参照してください。

## フォームポータル送信アクション {#forms-portal-submit-action}

この **[!UICONTROL Forms Portal 送信アクション]** オプションを使用すると、フォームデータがAEM Formsポータル経由で使用できるようになります。

Forms Portal と送信アクションについて詳しくは、 [ドラフトと送信コンポーネント](/help/forms/using/draft-submission-component.md).

## AEM ワークフローを起動 {#invoke-an-aem-workflow}

この **[!UICONTROL AEM Workflow を起動]** 送信アクションは、アダプティブフォームをAEM Workflow に関連付けます。 フォームが送信されると、関連付けられたワークフローが処理ノードで自動的に開始します。 さらに、データファイル、添付ファイル、レコードのドキュメント（該当する場合）は、ワークフローのペイロードの場所に配置されます。

を使用する前に **[!UICONTROL AEM Workflow を起動]** 送信アクション [AEM DS 設定の構成](/help/forms/using/configuring-the-processing-server-url-.md). AEM ワークフローの作成について詳しくは、「[OSGi 上の Forms 中心のワークフロー](/help/forms/using/aem-forms-workflow.md)」を参照してください。

## アダプティブフォームにおけるサーバー側の再検証 {#server-side-revalidation-in-adaptive-form}

通常、どのオンラインデータ取得システムでも、開発者は、いくつかのビジネスルールを実施するために、クライアント側に JavaScript 検証を配置します。 しかし、最新のブラウザーでは、エンドユーザーが Web Browser DevTools Console などの様々な手法を使用してこれらの検証を回避し、手動で送信を行える方法が存在します。このような方法は、アダプティブフォームでも有効です。 フォーム開発者は、多様な検証ロジックを作成できますが、エンドユーザーは、これらの検証ロジックを回避し、無効なデータをサーバーに送信できます。無効なデータは、フォーム作成者が適用したビジネスルールを破ることになります。

サーバー側の再検証機能を使用すると、アダプティブフォームの作成者がサーバー上でアダプティブフォームをデザインする際に指定した検証を実行することもできます。 これは、フォームの検証で表されるデータ送信の漏洩やビジネスルール違反の可能性を阻止します。

### サーバー側で検証されるもの  {#what-to-validate-on-server-br}

アダプティブフォームの標準 (OOTB) フィールド検証で、サーバーで再実行されるものはすべて次のとおりです。

* 必須
* 検証パターン形式文字列
* 検証式

### サーバー側検証の有効化 {#enabling-server-side-validation-br}

サイドバーにある「アダプティブフォームコンテナ」の「**サーバー側で再検証**」を使用して、現在のフォームのサーバーサイド検証を有効または無効にします。

![サーバーサイド検証の有効化](assets/revalidate-on-server.png)
**図：** *サーバー側検証の有効化*

エンドユーザーがこれらの検証を回避してフォームを送信した場合、サーバーが再度検証を行います。サーバーサイドでの検証が失敗した場合、送信処理が中止されます。エンドユーザーには、元のフォームが再び表示されます。 取得されたデータおよび送信されたデータは、エラーとしてユーザーに表示されます。

### 検証式でのカスタム関数のサポート {#supporting-custom-functions-in-validation-expressions-br}

場合によっては、 **複雑な検証ルール**&#x200B;に設定すると、正確な検証スクリプトはカスタム関数に配置され、作成者はこれらのカスタム関数をフィールド検証式から呼び出します。 このカスタム関数ライブラリをサーバーサイド検証中に認識させ、利用可能にするために、フォーム作成者は、「アダプティブフォームコンテナ」プロパティの「**[!UICONTROL 基本]**」タブで、AEM クライアントライブラリの名前を設定できます（下記画像を参照）。

![検証式でのカスタム関数のサポート](assets/clientlib-cat.png)
**図：** *検証式でのカスタム関数のサポート*

作成者は、アダプティブフォームごとにカスタム JavaScript ライブラリを設定できます。 ライブラリには、jquery および underscore.js サードパーティライブラリに依存する再利用可能な関数のみを保持します。

## 送信アクションに対するエラー処理 {#error-handling-on-submit-action}

AEMのセキュリティと堅牢化のガイドラインの一環として、404.jsp や 500.jsp などのカスタムエラーページを設定します。 これらのハンドラーは、フォームの送信時に 404 エラーまたは 500 エラーが表示されるときに呼び出されます。 また、これらのハンドラーは、パブリッシュノードでこれらのエラーコードがトリガーされるときにも呼び出されます。

詳しくは、「[エラーハンドラーによって表示されるページのカスタマイズ](/help/sites-developing/customizing-errorhandler-pages.md)」を参照してください。
