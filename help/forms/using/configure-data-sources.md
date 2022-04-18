---
title: データソースの設定
seo-title: Configure data sources
description: ここでは、各種のデータソースを設定し、それらのデータソースを使用してフォームデータモデルを作成する方法について説明します。
seo-description: Learn how to configure different types of data sources and leverage to create form data models.
uuid: 292217c2-8110-4232-a78b-edea212765d2
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: integration
discoiquuid: 1dafd400-16c0-416d-9e81-7bf53b761f98
feature: Form Data Model
exl-id: a8f200ac-cf9f-47b7-9856-e62aa8b229eb
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1399'
ht-degree: 94%

---

# データソースの設定 {#configure-data-sources}

ここでは、各種のデータソースを設定し、それらのデータソースを使用してフォームデータモデルを作成する方法について説明します。

![](do-not-localize/data-integeration.png)

AEM Forms のデータ統合機能により、複数の異なるデータソースを設定して接続することができます。以下のタイプがサポートされています。これらのタイプは、すぐに使用することができます。ただし、これらの機能を少しカスタマイズするだけで、他のデータソースを統合することもできます。

* リレーショナルデータベース - MySQL、Microsoft SQL Server、IBM DB2、Oracle RDBMS
* AEM ユーザープロファイル
* RESTful Web サービス
* SOAP ベース Web サービス
* OData サービス

データ統合では、すぐに使用できる認証タイプとして、OAuth2.0 認証、基本認証、API キー認証がサポートされています。また、Web サービスにアクセスするためのカスタムの認証タイプを実装することもできます。RESTful サービス、SOAP ベースサービス、OData サービスは AEM クラウドサービスで設定し、リレーショナルデータベース用の JDBC と AEM ユーザープロファイル用のコネクターは、AEM Web コンソールで設定します。

## リレーショナルデータベースの設定 {#configure-relational-database}

AEM Web Console Configuration を使用してリレーショナルデータベースを設定することができます。以下の操作を実行します。

1. AEM web コンソール（`https://[server]:[host]/system/console/configMgr`）にアクセスします。
1. 「**[!UICONTROL Apache Sling Connection Pooled DataSource]**」という設定を探し、その設定をタップして編集モードで開きます。
1. 設定ダイアログで、設定するデータベースの詳細を指定します。例えば、以下のような詳細を指定します。

   * データソースの名前
   * データソース名が保管されるデータソースサービスプロパティ
   * JDBC ドライバーの Java クラス名
   * JDBC 接続 URI
   * JDBC ドライバーとの接続を確立するためのユーザー名とパスワード

   >[!NOTE]
   >
   >データソースを設定する前に、パスワードなどの機密情報を必ず暗号化してください。暗号化するには、以下の手順を実行します。
   >
   >1. `https://[server]:[port]/system/console/crypto` にアクセスします。
   >1. 「**[!UICONTROL プレーンテキスト]**」フィールドに暗号化する文字列（パスワードなど）を入力して「**[!UICONTROL 保護]**」をクリックします。

   >
   >暗号化されたテキストが「保護されたテキスト」フィールドに表示されます。このテキストを設定内で指定できます。

1. プールからオブジェクトを取得するときにそのオブジェクトを検証する場合は「**[!UICONTROL Test on Borrow]**」を有効にし、プールにオブジェクトを返すときにそのオブジェクトを検証する場合は「**[!UICONTROL Test on Return]**」を有効にします。
1. 「**[!UICONTROL 検証クエリ]**」フィールドで SQL SELECT クエリを指定して、プールからの接続を検証します。このクエリでは、1 行以上の行が返される必要があります。使用しているデータベースに応じて、以下のいずれかを指定します。

   * SELECT 1（MySQL または MS SQL の場合）
   * SELECT 1 from dual（Oracle の場合）

1. 「**[!UICONTROL 保存]**」をタップして、設定内容を保存します。

## AEM ユーザープロファイルの設定 {#configure-aem-user-profile}

AEM Web コンソールでユーザープロファイルコネクター設定を使用して、AEM のユーザープロファイルを設定することができます。以下の操作を実行します。

1. AEM web コンソール（`https://[server]:[host]/system/console/configMgr`）にアクセスします。
1. 「**[!UICONTROL AEM Forms データ統合 - ユーザープロファイルコネクター設定]**」という設定をタップして、この設定を編集モードで開きます。
1. ユーザープロファイルコネクター設定ダイアログで、ユーザープロファイルプロパティの追加、削除、更新を行うことができます。ここで指定したプロパティは、フォームデータモデルで使用することができます。ユーザープロファイルのプロパティを指定する場合は、以下の形式で指定します。

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >この **&amp;ast;** 上記の例では、 `profile/empLocation/` CRXDE 構造のAEMユーザープロファイルのノード。 この場合、`profile/empLocation/` ノード配下のいずれかのノード内に存在する `string` タイプの `city` プロパティに、フォームデータモデルからアクセスすることができます。ただし、指定されたプロパティが存在するノードの構造が統一されている必要があります。

1. 「**[!UICONTROL 保存]**」をタップして、設定内容を保存します。

## クラウドサービス設定用フォルダーの構成 {#cloud-folder}

>[!NOTE]
>
>RESTful サービス、SOAP サービス、OData サービスのクラウドサービスを設定するには、クラウドサービス用のフォルダーを設定する必要があります。

AEM におけるすべてのクラウドサービス設定は、AEM リポジトリの `/conf` フォルダー内に保存されます。デフォルトの場合、`conf` フォルダーには `global` フォルダーが含まれています。このフォルダーで、クラウドサービスの設定を作成できます。ただし、このフォルダーを手動でクラウド設定用に有効にする必要があります。追加のフォルダーを `conf` フォルダー内に作成して、クラウドサービスの作成と編集を行うこともできます。

クラウドサービス設定用のフォルダーを構成するには、以下の手順を実行します。

1. **[!UICONTROL ツール／一般／設定ブラウザー]**&#x200B;に移動します。
   * 詳しくは、[](/help/sites-administering/configurations.md)設定ブラウザーのドキュメントを参照してください。
1. 以下の手順を実行して、global フォルダーをクラウド設定用に有効にします。クラウドサービス設定用に別のフォルダーを作成する場合は、この手順をスキップしてください。

   1. **[!UICONTROL 設定ブラウザー]**&#x200B;で、「`global`」フォルダーを選択して「**[!UICONTROL プロパティ]**」をタップします。
   1. **[!UICONTROL 設定プロパティ]**&#x200B;ダイアログで、「**[!UICONTROL クラウド設定]**」を有効にします。
   1. 「**[!UICONTROL 保存して閉じる]**」をタップして設定内容を保存し、ダイアログを閉じます。

1. **[!UICONTROL 設定ブラウザー]**&#x200B;で「**[!UICONTROL 作成]**」をタップします。
1. **[!UICONTROL 設定を作成]**&#x200B;ダイアログでフォルダーのタイトルを指定し、「**[!UICONTROL クラウド設定]**」を有効にします。
1. 「**[!UICONTROL 作成]**」をタップします。これで、クラウドサービス設定が有効になったフォルダーが作成されました。

## RESTful Web サービスの設定 {#configure-restful-web-services}

RESTful web サービスは、[Swagger の仕様](https://swagger.io/specification/)に従い、JSON 形式または YAML 形式で Swagger 定義ファイル内に記述することができます。AEM クラウドサービスで RESTful Web サービスを設定するには、ファイルシステム内に Swagger ファイルが存在しているか、Swagger ファイルがホストされる URL を指定する必要があります。

RESTful サービスを設定するには、以下の手順を実行します。

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](/help/forms/using/configure-data-sources.md#cloud-folder)」を参照してください。

1. タップ **[!UICONTROL 作成]** 開く **[!UICONTROL データソース設定を作成ダイアログ]**. 設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL RESTful サービス]**」を選択します。必要な場合は、設定のサムネール画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す RESTful サービスの詳細情報を指定します。

   * 「Swagger ソース」ドロップダウンで「URL」または「ファイル」を選択します。「URL」を選択した場合は、Swagger 定義ファイルに対する Swagger の URL を指定し、「ファイル」を選択した場合は、ローカルのファイルシステムから Swagger ファイルをアップロードします。
   * RESTful サービスにアクセスするための認証タイプ（「なし」、「OAuth2.0 認証」、「基本認証」、「API キー認証」、「カスタム認証」）を選択し、その選択内容に応じて認証の詳細を指定します。

1. 「**[!UICONTROL 作成]**」をタップして、RESTful サービス用のクラウド設定を作成します。

## SOAP Web サービスの設定 {#configure-soap-web-services}

SOAP ベースの web サービスは、[Web Services Description Language（WSDL）の仕様](https://www.w3.org/TR/wsdl)に従って記述します。AEM クラウドサービスで SOAP ベースの Web サービスを設定するには、その Web サービスの WSDL URL を確認して、以下の手順を実行します。

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](/help/forms/using/configure-data-sources.md#cloud-folder)」を参照してください。

1. タップ **[!UICONTROL 作成]** 開く **[!UICONTROL データソース設定を作成ダイアログ]**. 設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL SOAP Web サービス]**」を選択します。必要な場合は、設定のサムネール画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す SOAP Web サービスの詳細情報を指定します。

   * Web サービスの WSDL URL を指定します。
   * サービスエンドポイント。WSDL で指定されているサービスエンドポイントを上書きするには、このフィールドの値を指定します。
   * SOAP サービスにアクセスするための認証の種類（「なし」、「OAuth2.0」、「基本認証」、「カスタム認証」、「X509 トークン」）を選択し、認証の詳細を指定します。

      認証の種類として X509 トークンを選択した場合は、X509 証明書を設定します。詳しくは、[証明書の設定](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service)を参照してください。
X509 証明書のキーストアエイリアスを**[!UICONTROL キーエイリアス]**&#x200B;フィールドに指定します。**[!UICONTROL 有効期間]**&#x200B;フィールドに、認証リクエストが有効なままになるまでの時間（秒）を指定します。オプションで、メッセージの本文、タイムスタンプヘッダーまたはその両方に署名することを選択します。

1. 「**[!UICONTROL 作成]**」をタップして、SOAP web サービス用のクラウド設定を作成します。

## OData サービスの設定 {#config-odata}

OData サービスは、そのサービスのルート URL によって識別されます。AEM クラウドサービスで OData サービスを設定するには、そのサービスのルート URL を確認して、以下の手順を実行します。

>[!NOTE]
>
>オンライン環境またはオンプレミス環境で Microsoft Dynamics 365 を設定する詳しい手順については、「[Microsoft Dynamics OData 設定](/help/forms/using/ms-dynamics-odata-configuration.md)」を参照してください。

1. **[!UICONTROL ツール／Cloud Services／データソース]**&#x200B;に移動します。クラウド設定の作成対象となるフォルダーをタップして選択します。

   クラウドサービス設定用フォルダーの作成方法と構成方法については、「[クラウドサービス設定用フォルダーの構成](/help/forms/using/configure-data-sources.md#cloud-folder)」を参照してください。

1. タップ **[!UICONTROL 作成]** 開く **[!UICONTROL データソース設定を作成ダイアログ]**. 設定の名前と、必要に応じて設定のタイトルを指定し、「**[!UICONTROL サービスタイプ]**」ドロップダウンで「**[!UICONTROL OData サービス]**」を選択します。必要な場合は、設定のサムネール画像を選択して「**[!UICONTROL 次へ]**」をタップします。
1. 以下に示す OData サービスの詳細情報を指定します。

   * 設定する OData サービスのルート URL を指定します。
   * OData サービスにアクセスするための認証タイプ（なし、OAuth2.0 認証、基本認証、カスタム認証）を選択し、その選択内容に応じて認証の詳細を指定します。

   >[!NOTE]
   >
   >OData エンドポイントをサービスルートとして使用して Microsoft Dynamics サービスに接続する場合は、OAuth 2.0 認証を選択する必要があります。

1. 「**作成**」をタップして、OData サービス用のクラウド設定を作成します。

## 次の手順 {#next-steps}

上記の手順により、データソースが設定されました。次に、フォームデータモデルを作成します。データソースが設定されていないフォームデータモデルが既に作成されている場合は、上記の手順で設定したデータソースにそのフォームデータモデルを関連付けます。詳しくは、「[フォームデータモデルの作成](/help/forms/using/create-form-data-models.md)」を参照してください。
