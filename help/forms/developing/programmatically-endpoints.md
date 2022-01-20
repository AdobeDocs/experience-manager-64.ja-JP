---
title: エンドポイントのプログラム管理
seo-title: Programmatically Managing Endpoints
description: Endpoint Registry サービスを使用して、EJB エンドポイントの追加、SOAP エンドポイントの追加、監視フォルダーエンドポイントの追加、E メールエンドポイントの追加、リモートエンドポイントの追加、Task Manager エンドポイントの追加、エンドポイントの変更、エンドポイントの削除、エンドポイントコネクタ情報の取得を行います。
seo-description: Use the Endpoint Registry service to add EJB endpoints, add SOAP endpoint, add Watched Folder endpoints, add Email endpoints, add  Remoting endpoints, add Task Manager endpoints, modify endpoints, remove endpoints, and retrieve endpoint connector information.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
role: Developer
exl-id: 1dc43962-dffe-4062-838f-737b3100ad28
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '10791'
ht-degree: 6%

---

# エンドポイントのプログラム管理 {#programmatically-managing-endpoints}

**エンドポイントレジストリサービスについて**

Endpoint Registry サービスは、エンドポイントをプログラムで管理する機能を提供します。 例えば、次の種類のエンドポイントをサービスに追加できます。

* EJB
* SOAP
* 監視フォルダー
* 電子メール
* (AEM forms では非推奨 )Remoting
* タスクマネージャー

   >[!NOTE]
   >
   >SOAP、EJB、および (JEE 上のAEM forms では非推奨 ) リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。 SOAP および EJB エンドポイントは、すべてのサービス操作で SOAP および EJB を有効にします。

   リモートエンドポイントを使用すると、Flexクライアントは、エンドポイントが追加されるAEM Formsサービスで操作を呼び出すことができます。 エンドポイントと同じ名前のFlex宛先が作成され、Flexクライアントは、この宛先を指す RemoteObjects を作成して、関連するサービスの操作を呼び出すことができます。

   電子メール、タスクマネージャー、監視フォルダーの各エンドポイントでは、サービスの特定の操作のみが公開されます。 これらのエンドポイントを追加するには、呼び出すメソッドを選択し、設定パラメーターを設定し、入力および出力パラメーターのマッピングを指定する、2 番目の設定手順が必要です。

   TaskManager エンドポイントは、 *カテゴリ*. その後、これらのカテゴリは TaskManager を通じて Workspace に公開され、エンドユーザーは TaskManager エンドポイントを分類されたとおりに表示します。 Workspace 内では、エンドユーザーはナビゲーションウィンドウにこれらのカテゴリを表示します。 各カテゴリ内のエンドポイントは、Workspace の「Start Processes」ページにプロセスカードとして表示されます。

   Endpoint Registry サービスを使用して、次のタスクを実行できます。

* EJB エンドポイントを追加します。 ( [EJB エンドポイントの追加](programmatically-endpoints.md#adding-ejb-endpoints).)
* SOAP エンドポイントを追加します。 ( [SOAP エンドポイントの追加](programmatically-endpoints.md#adding-soap-endpoints).)
* 監視フォルダーエンドポイントを追加する ( [監視フォルダーエンドポイントの追加](programmatically-endpoints.md#adding-watched-folder-endpoints).)
* 電子メールエンドポイントを追加します。 ( [電子メールエンドポイントの追加](programmatically-endpoints.md#adding-email-endpoints).)
* リモートエンドポイントを追加します。 ( [リモートエンドポイントの追加](programmatically-endpoints.md#adding-remoting-endpoints).)
* TaskManager エンドポイントを追加します ( [TaskManager エンドポイントの追加](programmatically-endpoints.md#adding-taskmanager-endpoints).)
* エンドポイントを変更する ( [エンドポイントの変更](programmatically-endpoints.md#modifying-endpoints).)
* エンドポイントを削除します ( [エンドポイントの削除](programmatically-endpoints.md#removing-endpoints).)
* エンドポイントコネクタ情報の取得 ( [エンドポイントコネクタ情報の取得](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## EJB エンドポイントの追加 {#adding-ejb-endpoints}

EJB エンドポイントは、AEM Forms Java API を使用して、プログラムによってサービスに追加できます。 EJB エンドポイントをサービスに追加すると、クライアントアプリケーションで EJB モードを使用してサービスを呼び出すことができます。 つまり、AEM Formsを呼び出すために必要な接続プロパティを設定する場合、EJB モードを選択できます。 （[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）

>[!NOTE]
>
>Web サービスを使用して EJB エンドポイントを追加することはできません。

>[!NOTE]
>
>通常、EJB エンドポイントはデフォルトでサービスに追加されますが、EJB エンドポイントは、プログラムでデプロイされたプロセスや、EJB エンドポイントが削除され、再度追加される必要があるプロセスに追加できます。

### 手順の概要 {#summary-of-steps}

EJB エンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. の作成 `EndpointRegistry Client` オブジェクト。
1. EJB エンドポイント属性を設定します。
1. EJB エンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry Client オブジェクトの作成**

EJB エンドポイントをプログラムで追加する前に、 `EndpointRegistryClient` オブジェクト。

**EJB エンドポイント属性を設定する**

サービスの EJB エンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**:作成するエンドポイントのタイプを指定します。 EJB エンドポイントを作成するには、次を指定します。 `EJB`.
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子**:エンドポイントが属するサービスを指定します。
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 EJB エンドポイントを作成する際に、ワイルドカード文字 ( `*`) をクリックします。 ただし、すべてのサービス操作を呼び出すのとは異なり、特定の操作を指定する場合は、ワイルドカード文字 ( `*`) をクリックします。

**EJB エンドポイントの作成**

EJB エンドポイント属性を設定した後、サービス用の EJB エンドポイントを作成できます。

**エンドポイントを有効にする**

新しいエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。 エンドポイントを有効にした後は、エンドポイントを使用してサービスを呼び出すことができます。 エンドポイントを有効にすると、管理コンソール内で表示できます。

**関連トピック**

[Java API を使用した EJB エンドポイントの追加](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した EJB エンドポイントの追加 {#adding-an-ejb-endpoint-using-the-java-api}

Java API を使用して EJB エンドポイントを追加します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-livecycle-client.jar などのクライアント JAR ファイルを含めます。 （

1. EndpointRegistry Client オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EndpointRegistryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. EJB エンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * を呼び出して、コネクタ識別子の値を指定します。 `CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドと文字列値を渡す `EJB`.
   * を呼び出して、エンドポイントの説明を指定します。 `CreateEndpointInfo` オブジェクトの `setDescription` メソッドを使用してエンドポイントを表す string 値を渡す方法を示します。
   * を呼び出して、エンドポイントの名前を指定します。 `CreateEndpointInfo` オブジェクトの `setName` メソッドを使用して、名前を指定する string 値を渡す。
   * を呼び出して、エンドポイントが属するサービスを指定します。 `CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを使用して、サービス名を指定する string 値を渡す。
   * を呼び出して呼び出す操作を指定します。 `CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを使用して、操作名を指定する string 値を渡します。 SOAP および EJB エンドポイントの場合、ワイルドカード文字 ( `*`) で始まり、すべての操作を示します。

1. EJB エンドポイントを作成します。

   を呼び出してエンドポイントを作成する `EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドおよび `CreateEndpointInfo` オブジェクト。 このメソッドは、 `Endpoint` 新しい EJB エンドポイントを表すオブジェクト。

1. エンドポイントを有効にします。

   を呼び出してエンドポイントを有効にする `EndpointRegistryClient` オブジェクトの enable メソッドおよび `Endpoint` が返したオブジェクト `createEndpoint` メソッド。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用した EJB エンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## SOAP エンドポイントの追加 {#adding-soap-endpoints}

AEM Forms Java API を使用して、プログラムによって SOAP エンドポイントをサービスに追加できます。 SOAP エンドポイントを追加すると、SOAP モードを使用してクライアントアプリケーションからサービスを呼び出すことができます。 つまり、AEM Formsを呼び出すために必要な接続プロパティを設定する場合、SOAP モードを選択できます。

>[!NOTE]
>
>Web サービスを使用して SOAP エンドポイントを追加することはできません。

>[!NOTE]
>
>通常、SOAP エンドポイントはデフォルトでサービスに追加されます。ただし、SOAP エンドポイントは、プログラムによってデプロイされたプロセスや、SOAP エンドポイントが削除され、再度追加される必要があるプロセスに追加できます。

### 手順の概要 {#summary_of_steps-1}

SOAP エンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. の作成 `EndpointRegistryClient` オブジェクト。
1. SOAP エンドポイント属性を設定します。
1. SOAP エンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

これらの JAR ファイルは、SOAP エンドポイントを作成するために必要です。 ただし、SOAP エンドポイントを使用してサービスを呼び出す場合は、追加の JAR ファイルが必要です。 AEM Forms JAR ファイルについて詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry Client オブジェクトの作成**

プログラムによって SOAP エンドポイントをサービスに追加するには、 `EndpointRegistryClient` オブジェクト。

**SOAP エンドポイント属性の設定**

SOAP エンドポイントをサービスに追加するには、次の値を指定します。

* **コネクタ識別子の値**:作成するエンドポイントのタイプを指定します。 SOAP エンドポイントを作成するには、次を指定します。 `SOAP`.
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイント名を指定します。
* **サービス識別子の値**:エンドポイントが属するサービスを指定します。
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 SOAP エンドポイントを作成する際に、ワイルドカード文字 ( `*`) をクリックします。 ただし、すべてのサービス操作を呼び出すのとは異なり、特定の操作を指定する場合は、ワイルドカード文字 ( `*`) をクリックします。

**SOAP エンドポイントの作成**

SOAP エンドポイント属性を設定した後、SOAP エンドポイントを作成できます。

**エンドポイントを有効にする**

新しいエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。 エンドポイントが有効な場合、エンドポイントを使用してサービスを呼び出すことができます。 エンドポイントを有効にすると、管理コンソール内に表示されます。

**関連トピック**

[Java API を使用した SOAP エンドポイントの追加](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した SOAP エンドポイントの追加 {#add-a-soap-endpoint-using-the-java-api}

Java API を使用して、SOAP エンドポイントをサービスに追加します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-livecycle-client.jar などのクライアント JAR ファイルを含めます。

1. EndpointRegistry Client オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EndpointRegistryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. SOAP エンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * を呼び出して、コネクタ識別子の値を指定します。 `CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドと文字列値を渡す `SOAP`.
   * を呼び出して、エンドポイントの説明を指定します。 `CreateEndpointInfo` オブジェクトの `setDescription` メソッドを使用してエンドポイントを表す string 値を渡す方法を示します。
   * を呼び出して、エンドポイントの名前を指定します。 `CreateEndpointInfo` オブジェクトの `setName` メソッドを使用して、名前を指定する string 値を渡す。
   * を呼び出して、エンドポイントが属するサービスを指定します。 `CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを使用して、サービス名を指定する string 値を渡す。
   * を呼び出して呼び出す操作を指定します。 `CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを使用して、操作名を指定する string 値を渡す。 SOAP および EJB エンドポイントの場合、ワイルドカード文字 ( `*`) で始まり、すべての操作を示します。

1. SOAP エンドポイントを作成します。

   を呼び出してエンドポイントを作成する `EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドおよび `CreateEndpointInfo` オブジェクト。 このメソッドは、 `Endpoint` 新しい SOAP エンドポイントを表すオブジェクト。

1. エンドポイントを有効にします。

   を呼び出してエンドポイントを有効にする `EndpointRegistryClient` オブジェクトの enable メソッドを参照し、 `Endpoint` が返したオブジェクト `createEndpoint` メソッド。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用した SOAP エンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 監視フォルダーエンドポイントの追加 {#adding-watched-folder-endpoints}

AEM Forms Java API を使用して、プログラムによって監視フォルダーエンドポイントをサービスに追加できます。 監視フォルダーエンドポイントを追加すると、ユーザーはフォルダーにファイル (PDFファイルなど ) を配置できます。 ファイルがフォルダーに配置されると、設定済みのサービスが呼び出され、ファイルが操作されます。 サービスが指定の操作を実行した後に、変更されたファイルが指定の出力フォルダーに保存されます。監視フォルダーは、毎週月曜日、水曜日、金曜日の正午など、一定の速度の間隔で、または Cron スケジュールでスキャンするように設定されます。

監視フォルダーエンドポイントをプログラムによってサービスに追加する場合は、次の短時間のみ有効なプロセスを考慮してください。 *EncryptDocument*. ( [AEM Formsプロセスについて](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

このプロセスは、セキュリティで保護されていないPDFドキュメントを入力値として受け取り、セキュリティで保護されていないPDFドキュメントを Encryption サービスの `EncryptPDFUsingPassword` 操作。 PDFドキュメントはパスワードで暗号化され、PDFドキュメントはこのプロセスの出力値です。 入力値 ( 保護されていないPDFドキュメント ) の名前は `InDoc` データタイプは `com.adobe.idp.Document`. 出力値の名前 ( パスワードで暗号化されたPDFドキュメント ) は `SecuredDoc` データタイプは `com.adobe.idp.Document`.

>[!NOTE]
>
>Web サービスを使用して監視フォルダーエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-2}

監視フォルダーエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. の作成 `EndpointRegistryClient` オブジェクト。
1. 監視フォルダーエンドポイント属性を設定します。
1. 設定値を指定します。
1. 入力パラメーター値を定義します。
1. 出力パラメータ値を定義します。
1. 監視フォルダーエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry Client オブジェクトの作成**

プログラムによって監視フォルダーエンドポイントを追加するには、 `EndpointRegistryClient` オブジェクト。

**監視フォルダーエンドポイントの属性を設定する**

サービスの監視フォルダーエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**:作成するエンドポイントのタイプを指定します。 監視フォルダーエンドポイントを作成するには、次を指定します。 `WatchedFolder`.
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子**:エンドポイントが属するサービスを指定します。 例えば、この節で説明するプロセスに監視フォルダーエンドポイントを追加する場合（Workbench を使用してアクティベートすると、プロセスはサービスになります）、 `EncryptDocument`.
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 通常、Workbench で作成されたプロセスから発生するサービスの監視フォルダーエンドポイントを作成する場合、操作の名前はになります `invoke`.

**設定値の指定**

プログラムによって監視フォルダーエンドポイントをサービスに追加する場合は、監視フォルダーエンドポイントの設定値を指定する必要があります。 管理コンソールを使用して監視フォルダーエンドポイントを追加した場合、これらの設定値は管理者が指定します。

次のリストでは、監視フォルダーエンドポイントをプログラムでサービスに追加する際に設定される設定値を指定します。

* **url**:監視フォルダーの場所を指定します。 クラスター環境では、この値は、クラスター内のすべてのコンピューターからアクセス可能な共有ネットワークフォルダーを指している必要があります。
* **非同期**:呼び出しの種類を非同期型または同期型として識別します。 一過性および同期型のプロセスは、同期型でのみ呼び出すことができます。デフォルト値は true です。非同期をお勧めします。
* **cronExpression**:Quartz で、入力ディレクトリのポーリングをスケジュールするために使用されます。
* **purgeDuration**:これは必須の属性です。 結果フォルダー内のファイルとフォルダーは、この値より古い場合にパージされます。 この値の単位は日です。この属性は、結果フォルダーがいっぱいにならないようにするのに役立ちます。 -1 を指定すると、結果フォルダーの削除は行われません。デフォルト値は -1 です。
* **repeatInterval**:監視フォルダーをスキャンして入力を求める間隔（秒）です。 スロットルが有効になっていない限り、この値は平均ジョブの処理時間より長くする必要があります。そうしないと、システムが過負荷になる場合があります。 デフォルト値は 5 です。
* **repeatCount**:監視フォルダーがフォルダーまたはディレクトリをスキャンする回数です。 -1 を指定すると、無限にスキャンされます。デフォルト値は -1 です。
* **throttleOn**:一度に処理できる監視フォルダーのジョブ数を制限します。 ジョブの最大数は batchSize の値によって決まります。
* **userName**:監視フォルダーからターゲットサービスを呼び出す際に使用されるユーザー名です。 この値は必須です。デフォルト値は「SuperAdmin」です。
* **domainName**:ユーザーのドメイン。 この値は必須です。デフォルト値は「DefaultDom」です。
* **batchSize**:1 回のスキャンで取得されるファイルまたはフォルダの数。 システムの過負荷を防ぐには、この値を使用します。一度にスキャンするファイル数が多すぎると、クラッシュが発生する場合があります。 デフォルト値は 2 です。
* **waitTime**:作成後にフォルダーまたはファイルをスキャンするまでに待機する時間（ミリ秒単位）です。 例えば、待機時間が 36,000,000 ミリ秒（1 時間）で、1 分前にファイルが作成された場合、このファイルは 59 分以上経過した後に取得されます。 この属性は、ファイルまたはフォルダーを入力フォルダーに完全にコピーする場合に役立ちます。 例えば、処理するファイルのサイズが大きく、ファイルのダウンロードに 10 分かかる場合は、待機時間を 10&amp;ast;60&amp;ast;1000 ミリ秒に設定します。 この設定は、監視フォルダーが 10 分間待たなかった場合に、ファイルをスキャンしないようにします。 デフォルト値は 0 です。
* **excludeFilePattern**:スキャンおよび取得するファイルとフォルダーを決定する際に監視フォルダーが使用するパターン。 このパターンを持つファイルまたはフォルダーは、スキャンされて処理されません。 この設定は、入力が複数のファイルを含むフォルダーの場合に役立ちます。 フォルダーの内容は、監視フォルダーで取得される名前のフォルダーにコピーできます。 この手順では、フォルダーが入力フォルダーに完全にコピーされる前に、監視フォルダーが処理対象のフォルダーを取得するのを防ぎます。 例えば、excludeFilePattern の値が `data*`、 `data*` 取り出されていません。 これには、 `data1`, `data2`など。 また、ファイルパターンを指定するワイルドカードパターンをパターンに追加することもできます。 監視フォルダーでは、ワイルドカードパターン ( `*.*` および `*.pdf`. これらのワイルドカードパターンは、正規表現ではサポートされていません。
* **includeFilePattern**:スキャンおよび取得の対象となるフォルダーとファイルを決定するために監視フォルダーが使用するパターン。 例えば、この値が `*`、 `input*` 拾い上げられた これには、 `input1`, `input2`など。 デフォルト値は `*` です。この値は、すべてのファイルとフォルダーを示します。 また、ファイルパターンを指定するワイルドカードパターンをパターンに追加することもできます。 監視フォルダーでは、ワイルドカードパターン ( `*.*` および `*.pdf`. これらのワイルドカードパターンは、正規表現ではサポートされていません。 この値は必須です。
* **resultFolderName**:保存した結果が保存されるフォルダー。 この場所は、絶対または相対ディレクトリパスにすることができます。 結果がこのフォルダーに表示されない場合は、失敗フォルダーを確認してください。読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。デフォルト値は `result/%Y/%M/%D/` です。これは、監視フォルダー内の結果フォルダーです。
* **preserveFolderName**:正常にスキャンおよび取得された後にファイルが保存される場所。 絶対パス、相対パス、または null ディレクトリパスを指定できます。 デフォルト値は `preserve/%Y/%M/%D/` です。
* **failureFolderName**:失敗ファイルが保存されるフォルダー。 この場所は、常に監視フォルダーからの相対パスで指定します。読み取り専用ファイルは処理されず、失敗フォルダーに保存されます。デフォルト値は `failure/%Y/%M/%D/` です。
* **preserveOnFailure**:サービスで操作を実行できなかった場合に入力ファイルを保持します。 デフォルト値は true です。
* **overwriteDuplicateFilename**:true に設定すると、結果フォルダーと保存用フォルダー内のファイルが上書きされます。 false に設定すると、名前に数値インデックスサフィックスを持つファイルおよびフォルダが使用されます。 デフォルト値は false です。

**入力パラメーター値の定義**

監視フォルダーエンドポイントを作成する場合は、入力パラメーターの値を定義する必要があります。 つまり、監視フォルダーによって呼び出される操作に渡される入力値を記述する必要があります。 例えば、このトピックで導入されたプロセスを考えてみましょう。 これには、 `InDoc` で、そのデータタイプは `com.adobe.idp.Document`. このプロセスの監視フォルダーエンドポイントを作成する場合（プロセスがアクティブ化されると、そのエンドポイントがサービスになります）、入力パラメーターの値を定義する必要があります。

監視フォルダーエンドポイントに必要な入力パラメーター値を定義するには、次の値を指定します。

**パラメーター名を入力**:入力パラメーターの名前。 入力値の名前は、プロセスに対して Workbench で指定されます。 入力値がサービス操作（Workbench で作成されたプロセスではないサービス）に属する場合、入力名は component.xml ファイルで指定されます。 例えば、この節で紹介するプロセスの入力パラメーターの名前は、 `InDoc`.

**マッピングタイプ**:サービス操作を呼び出すために必要な入力値を設定するために使用します。 マッピングには次の 2 つのタイプがあります。

* `Literal`:監視フォルダーエンドポイントは、フィールドに入力された値を表示どおりに使用します。 すべての基本 Java 型がサポートされます。例えば、String、long、int、Boolean などの入力を使用する API の場合、文字列は適切な型に変換され、サービスが呼び出されます。
* `Variable`:入力された値は、監視フォルダーが入力の選択に使用するファイルパターンです。 例えば、マッピングの種類に「変数」を選択し、入力ドキュメントをPDF・ファイルにする場合、 `*.pdf`をマッピング値として使用します。

**マッピング値**:マッピングタイプの値を指定します。 例えば、 `Variable` マッピングのタイプ、 `*.pdf` をファイルパターンとして使用します。

**データタイプ**:入力値のデータタイプを指定します。 例えば、この節で紹介するプロセスの入力値のデータ型は、 `com.adobe.idp.Document`.

**出力パラメータ値の定義**

監視フォルダーエンドポイントを作成する場合は、出力パラメーターの値を定義する必要があります。 つまり、監視フォルダーエンドポイントによって呼び出されるサービスによって返される出力値を記述する必要があります。 例えば、このトピックで導入されたプロセスを考えてみましょう。 これには、 `SecuredDoc` で、そのデータタイプは `com.adobe.idp.Document`. このプロセスの監視フォルダーエンドポイントを作成する場合（プロセスがアクティブ化されると、そのエンドポイントがサービスになります）、出力パラメーターの値を定義する必要があります。

監視フォルダーエンドポイントに必要な出力パラメーター値を定義するには、次の値を指定します。

**出力パラメーター名**:出力パラメーターの名前。 プロセス出力値の名前は、Workbench で指定します。 出力値がサービス操作（Workbench で作成されたプロセスではないサービス）に属する場合、出力名は component.xml ファイルで指定されます。 例えば、この節で紹介するプロセスの出力パラメーターの名前は、 `SecuredDoc`.

**マッピングタイプ**:サービスと操作の出力を設定するために使用します。 以下のオプションが利用できます。

* サービスが 1 つのオブジェクト（1 つのドキュメント）を返す場合、パターンは「 `%F.pdf` ソースの宛先は sourcefilename.pdf です。 例えば、この節で紹介したプロセスは、1 つのドキュメントを返します。 その結果、マッピングタイプは `%F.pdf` ( `%F` は、指定されたファイル名を使用することを意味します )。 パターン `%E` 入力ドキュメントの拡張を指定します。
* サービスがリストを返す場合、パターンは次のようになります。 `Result\%F\`の場合、ソースの宛先は Result\sourcefilename\source1 （出力 1）および Result\sourcefilename\source2 （出力 2）です。
* サービスがマップを返した場合、パターンは次のようになります。 `Result\%F\`の場合、ソースの宛先は Result\sourcefilename\file1 および Result\sourcefilename\file2 です。 マップに複数のオブジェクトがある場合、パターンは次のようになります。 `Result\%F.pdf` ソースの宛先は Result\sourcefilename1.pdf （出力 1）、Result\sourcefilenam2.pdf （出力 2）などです。

**データタイプ**:戻り値のデータ型を指定します。 例えば、この節で導入されるプロセスの戻り値のデータ型はです `com.adobe.idp.Document`.

**監視フォルダーエンドポイントの作成**

エンドポイントの属性、設定値を設定し、入力パラメーターと出力パラメーターの値を定義した後、監視フォルダーエンドポイントを作成する必要があります。

**エンドポイントを有効にする**

監視フォルダーエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。 エンドポイントが有効な場合、エンドポイントを使用してサービスを呼び出すことができます。 エンドポイントを有効にすると、管理コンソール内で表示できます。

**関連トピック**

[Java API を使用した監視フォルダーエンドポイントの追加](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した監視フォルダーエンドポイントの追加 {#add-a-watched-folder-endpoint-using-the-java-api}

AEM Forms Java API を使用して、監視フォルダーエンドポイントを追加します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-livecycle-client.jar などのクライアント JAR ファイルを含めます。

1. EndpointRegistry Client オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EndpointRegistryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 監視フォルダーエンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * を呼び出して、コネクタ識別子の値を指定します。 `CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドと文字列値を渡す `WatchedFolder`.
   * を呼び出して、エンドポイントの説明を指定します。 `CreateEndpointInfo` オブジェクトの `setDescription` メソッドを使用してエンドポイントを表す string 値を渡す方法を示します。
   * を呼び出して、エンドポイントの名前を指定します。 `CreateEndpointInfo` オブジェクトの `setName` メソッドを使用して、名前を指定する string 値を渡す。
   * を呼び出して、エンドポイントが属するサービスを指定します。 `CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを使用して、サービス名を指定する string 値を渡す。
   * を呼び出して呼び出す操作を指定します。 `CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを使用して、操作名を指定する string 値を渡す。 通常、Workbench で作成されたプロセスから生成されたサービスの監視フォルダーエンドポイントを作成する場合、操作の名前は invoke になります。

1. 設定値を指定します。

   設定値ごとに、監視フォルダーエンドポイントに対してを呼び出す必要があります。 `CreateEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッド。 例えば、 `url` 設定値、 `CreateEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッドを使用して、次の文字列値を渡します。

   * 設定値の名前を指定する string 値です。 設定時に `url` 設定値、指定 `url`.
   * 設定値の値を指定する string 値。 設定時に `url` 設定値で、監視フォルダーの場所を指定します。

   >[!NOTE]
   >
   >EncryptDocument サービスに設定されたすべての設定値を確認するには、次の Java コードの例を参照してください。 [クイックスタート：Java API を使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. 入力パラメーター値を定義します。

   を呼び出して、入力パラメーター値を定義する `CreateEndpointInfo` オブジェクトの `setInputParameterMapping` メソッドを使用して、次の値を渡します。

   * 入力パラメーターの名前を指定する string 値。 例えば、EncryptDocument サービスの入力パラメーターの名前は次のようになります。 `InDoc`.
   * 入力パラメーターのデータ型を指定する string 値です。 例えば、 `InDoc` 入力パラメーター： `com.adobe.idp.Document`.
   * マッピングタイプを指定する string 値。 例えば、次の項目を指定できます。 `variable`.
   * マッピングタイプの値を指定する string 値。 例えば、&amp;ast;.pdf をファイルパターンとして指定できます。

   >[!NOTE]
   >
   >を呼び出す `setInputParameterMapping` メソッドを使用します。 EncryptDocument プロセスには 1 つの入力パラメーターしかないので、このメソッドを 1 回呼び出す必要があります。

1. 出力パラメータ値を定義します。

   を呼び出して、出力パラメーター値を定義する `CreateEndpointInfo` オブジェクトの `setOutputParameterMapping` メソッドを使用して、次の値を渡します。

   * 出力パラメーターの名前を指定する string 値。 例えば、EncryptDocument サービスの出力パラメーターの名前は次のようになります。 `SecuredDoc`.
   * 出力パラメーターのデータ型を指定する string 値です。 例えば、 `SecuredDoc` 出力パラメーターは `com.adobe.idp.Document`.
   * マッピングタイプを指定する string 値。 例えば、次の項目を指定できます。 `%F.pdf`.

1. 監視フォルダーエンドポイントを作成します。

   を呼び出してエンドポイントを作成する `EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドおよび `CreateEndpointInfo` オブジェクト。 このメソッドは、 `Endpoint` オブジェクトを返します。

1. エンドポイントを有効にします。

   を呼び出してエンドポイントを有効にする `EndpointRegistryClient` オブジェクトの `enable` メソッドおよび `Endpoint` が返したオブジェクト `createEndpoint` メソッド。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 監視フォルダー設定値定数ファイル {#watched-folder-configuration-values-constant-file}

この [クイックスタート：Java API を使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) は、クイックスタートをコンパイルするために Java プロジェクトの一部である必要がある定数ファイルを使用します。 この定数ファイルは、監視フォルダーエンドポイントを追加する際に設定する必要がある設定値を表します。 次の Java コードは、定数ファイルを表しています。

```as3
 /** 
     * This class contains constants that can be used when setting Watched Folder  
     * configuration values 
     */ 
  
 public final class WatchedFolderEndpointConfigConstants { 
          
         public static final String PROPERTY_FILEPROVIDER_URL = "url"; 
         public static final String PROPERTY_PROPERTY_ASYNCHRONOUS = "asynchronous"; 
         public static final String PROPERTY_CRON_EXPRESSION = "cronExpression"; 
         public static final String PROPERTY_PURGE_DURATION = "purgeDuration"; 
         public static final String PROPERTY_REPEAT_INTERVAL = "repeatInterval"; 
         public static final String PROPERTY_REPEAT_COUNT = "repeatCount"; 
         public static final String PROPERTY_THROTTLE = "throttleOn"; 
         public static final String PROPERTY_USERNAMER = "userName"; 
         public static final String PROPERTY_DOMAINNAME = "domainName"; 
         public static final String PROPERTY_FILEPROVIDER_BATCH_SIZE = "batchSize"; 
         public static final String PROPERTY_FILEPROVIDER_WAIT_TIME = "waitTime"; 
         public static final String PROPERTY_EXCLUDE_FILE_PATTERN = "excludeFilePattern"; 
         public static final String PROPERTY_INCLUDE_FILE_PATTERN = "excludeFilePattern"; 
         public static final String PROPERTY_FILEPROVIDER_RESULT_FOLDER_NAME =  "resultFolderName"; 
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_FOLDER_NAME = "preserveFolderName"; 
         public static final String PROPERTY_FILEPROVIDER_FAILURE_FOLDER_NAME = "failureFolderName"; 
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_ON_FAILURE = "preserveOnFailure"; 
         public static final String PROPERTY_FILEPROVIDER_OVERWRITE_DUPLICATE_FILENAME = "overwriteDuplicateFilename";      
        }
```

## 電子メールエンドポイントの追加 {#adding-email-endpoints}

AEM Forms Java API を使用して、プログラムによって電子メールエンドポイントをサービスに追加できます。 電子メールエンドポイントを追加すると、1 つ以上の添付ファイルを含む電子メールメッセージを、指定した電子メールアカウントに送信できます。 次に、configure サービス操作が呼び出され、ファイルが操作されます。 指定した操作を実行すると、変更されたファイルが添付ファイルとして送信者に電子メールメッセージが送信されます。

E メールエンドポイントをプログラムでサービスに追加する場合は、次のような短時間のみ有効なプロセスを考慮してください。 *MyApplication\EncryptDocument*. 短時間のみ有効なプロセスについては、 [AEM Formsプロセスについて](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

このプロセスは、セキュリティで保護されていないPDFドキュメントを入力値として受け取り、セキュリティで保護されていないPDFドキュメントを Encryption サービスの `EncryptPDFUsingPassword` 操作。 このプロセスは、PDFドキュメントをパスワードで暗号化し、パスワードで暗号化されたPDFドキュメントを出力値として返します。 入力値 ( 保護されていないPDFドキュメント ) の名前は `InDoc` データタイプは `com.adobe.idp.Document`. 出力値の名前 ( パスワードで暗号化されたPDFドキュメント ) は `SecuredDoc` データタイプは `com.adobe.idp.Document`.

>[!NOTE]
>
>Web サービスを使用して E メールエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-3}

E メールエンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. の作成 `EndpointRegistryClient` オブジェクト。
1. 電子メールエンドポイント属性を設定します。
1. 設定値を指定します。
1. 入力パラメーター値を定義します。
1. 出力パラメータ値を定義します。
1. E メールエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry Client オブジェクトの作成**

プログラムで電子メールエンドポイントを追加する前に、 `EndpointRegistryClient` オブジェクト。

**電子メールエンドポイント属性を設定**

サービスの電子メールエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子の値**:作成するエンドポイントのタイプを指定します。 電子メールエンドポイントを作成するには、次を指定します。 `Email`.
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子の値**:エンドポイントが属するサービスを指定します。 例えば、この節で説明するプロセスに電子メールエンドポイントを追加する場合（Workbench を使用してアクティベートすると、プロセスはサービスになります）、 `EncryptDocument`.
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 通常、Workbench で作成されたプロセスから発生するサービスの電子メールエンドポイントを作成する場合、操作の名前はです `invoke`.

**設定値の指定**

プログラムによって電子メールエンドポイントをサービスに追加する場合は、電子メールエンドポイントの設定値を指定する必要があります。 これらの設定値は、管理コンソールを使用して E メールエンドポイントを追加した場合、管理者が指定します。

>[!NOTE]
>
>監視対象の電子メールアカウントは、電子メールエンドポイントにのみ使用される特別なアカウントです。 このアカウントは通常のユーザーの電子メールアカウントではありません。 通常のユーザーの電子メールアカウントは、電子メールプロバイダーが使用するアカウントとして設定してはいけません。電子メールプロバイダーは、メッセージの使用が完了した後で、インボックスから電子メールメッセージを削除します。

プログラムによって電子メールエンドポイントをサービスに追加する際に、次の設定値が設定されます。

* **cronExpression**:Cron 式を使用して電子メールをスケジュールする必要がある場合は、Cron 式を指定します。
* **repeatCount**:電子メールエンドポイントがフォルダーまたはディレクトリをスキャンする回数。 -1 を指定すると、無限にスキャンされます。デフォルト値は -1 です。
* **repeatInterval**:受信者が受信メールの確認に使用するスキャン速度（秒）です。 デフォルト値は 10 です。
* **startDelay**:スケジューラーが起動した後にスキャンするまで待つ時間です。 デフォルトの時間は 0 です。
* **batchSize**:最適なパフォーマンスを得るために受信者がスキャンごとに処理する電子メールメッセージの数。 -1 を指定すると、すべての電子メールが処理されます。デフォルト値は 2 です。
* **userName**:電子メールからターゲットサービスを呼び出す際に使用されるユーザー名。 デフォルト値は `SuperAdmin` です。
* **domainName**:必須の設定値。 デフォルト値は `DefaultDom` です。
* **domainPattern**:プロバイダーが受け入れる受信電子メールのドメインパターンを指定します。 例えば、 `adobe.com` が使用される場合、adobe.com からの電子メールのみが処理され、他のドメインからの電子メールは無視されます。
* **filePattern**:プロバイダーが受け入れる受信ファイル添付パターンを指定します。 これには、特定のファイル名拡張子 (&amp;ast;.dat, &amp;ast;.xml) を持つファイル、特定の名前を持つファイル (data)、名前と拡張子を持つ複合式を持つファイル (&amp;ast;) が含まれます。[dD][aA][Tt]) をクリックします。 デフォルト値は `*` です。
* **recipientSuccessfulJob**:ジョブの成功を示すメッセージの送信先の電子メールアドレス。 デフォルトでは、ジョブの正常終了メッセージは常に送信者に送信されます。`sender` と入力すると、電子メールの結果は送信者に送信されます。最大 100 人の受信者を指定できます。追加の受信者を電子メールアドレスで指定します。各受信者はコンマで区切ります。 このオプションをオフにするには、この値を空白のままにします。 場合によっては、プロセスをトリガーし、結果の電子メール通知を受け取りたくないことがあります。 デフォルト値は `sender` です。
* **recipientFailedJob**:ジョブの失敗を示すメッセージの送信先の電子メールアドレス。 デフォルトでは、失敗したジョブメッセージは常に送信者に送信されます。 `sender` と入力すると、電子メールの結果は送信者に送信されます。最大 100 人の受信者を指定できます。追加の受信者を電子メールアドレスで指定します。各受信者はコンマで区切ります。 このオプションをオフにするには、この値を空白のままにします。 デフォルト値は `sender` です。
* **inboxHost**:電子メールプロバイダーがスキャンするインボックスのホスト名または IP アドレス。
* **inboxPort**:電子メールサーバーが使用するポート。 POP3 のデフォルト値は「110」で、IMAP のデフォルト値は「143」です。SSL が有効になっている場合は、POP3 のデフォルト値は「995」で、IMAP のデフォルト値は「993」です。
* **inboxProtocol**:電子メールエンドポイントがインボックスのスキャンに使用する電子メールプロトコルです。 オプションは次のとおりです。 `IMAP` または `POP3`. 指定のプロトコルはインボックスホストメールサーバーでサポートされている必要があります。
* **inboxTimeOut**:電子メールプロバイダーがインボックスの応答を待機する時間（秒）。 デフォルト値は 60 です。
* **inboxUser**:電子メールアカウントにログインするために必要なユーザー名です。 電子メールサーバーと設定によっては、電子メールのユーザー名の部分のみを指定する場合と、完全な電子メールアドレスを指定する場合があります。
* **inboxPassword**:インボックスユーザーのパスワードです。
* **inboxSSLEnabled**:結果やエラーの通知メッセージを送信する際に、電子メールプロバイダーが SSL を使用するように強制するには、この値を設定します。 IMAP または POP3 ホストが SSL をサポートしていることを確認します。
* **smtpHost**:電子メールプロバイダーが結果およびエラーメッセージを送信するメールサーバーのホスト名。
* **smtpPort**:SMTP ポートのデフォルト値は 25 です。
* **smtpUser**:結果およびエラーの電子メール通知を送信する際に使用する電子メールプロバイダーのユーザーアカウント。
* **smtpPassword**:SMTP アカウントのパスワードです。 SMTP パスワードが不要なメールサーバーもあります。
* **charSet**:E メールプロバイダーが使用する文字セット。 デフォルト値は `UTF-8` です。
* **smtpSSLEnabled**:結果やエラーの通知メッセージを送信する際に、電子メールプロバイダーが SSL を使用するように強制するには、この値を設定します。 SMTP ホストが SSL をサポートしていることを確認します。
* **failedJobFolder**:SMTP メールサーバーが動作していない場合に結果を保存するディレクトリを指定します。
* **非同期**:synchronous に設定すると、すべての入力ドキュメントが処理され、1 回の応答が返されます。 「非同期」に設定すると、処理される入力ドキュメントごとに応答が送信されます。 例えば、このトピックで紹介されるプロセス用に E メールエンドポイントが作成され、セキュリティで保護されていない複数のPDFドキュメントを含む E メールメッセージがエンドポイントのインボックスに送信されるとします。 すべてのPDFドキュメントがPDFで暗号化され、エンドポイントが同期として設定されている場合、1 回の応答 E メールメッセージが送信され、セキュリティで保護されたすべてのパスワードドキュメントが添付されます。 エンドポイントが非同期として設定されている場合は、セキュリティで保護された応答ドキュメントごとに個別のPDFE メールメッセージが送信されます。 各電子メールメッセージには、添付ファイルとして 1 つのPDFドキュメントが含まれています。 デフォルト値は「asynchronous」です。

**入力パラメーター値の定義**

E メールエンドポイントを作成する場合、入力パラメーターの値を定義する必要があります。 つまり、E メールエンドポイントによって呼び出される操作に渡される入力値を記述する必要があります。 例えば、このトピックで導入されたプロセスを考えてみましょう。 これには、 `InDoc` で、そのデータタイプは `com.adobe.idp.Document`. このプロセスの E メールエンドポイントを作成する場合（プロセスがアクティブ化されると、サービスになります）、入力パラメーター値を定義する必要があります。

電子メールエンドポイントに必要な入力パラメーター値を定義するには、次の値を指定します。

**パラメーター名を入力**:入力パラメーターの名前。 入力値の名前は、プロセスに対して Workbench で指定されます。 入力値がサービス操作 (Workbench で作成されたプロセスではないFormsサービス ) に属する場合、入力名は component.xml ファイルで指定されます。 例えば、この節で紹介するプロセスの入力パラメーターの名前は、 `InDoc`.

**マッピングタイプ**:サービス操作を呼び出すために必要な入力値を設定するために使用します。 マッピングのタイプには次の 2 種類があります。

* `Literal`:E メールエンドポイントは、フィールドに表示されるとおりに入力された値を使用します。 すべての基本 Java 型がサポートされます。例えば、String、long、int および Boolean などの入力が使用される API の場合、文字列は適切な型に変換され、サービスが呼び出されます。
* `Variable`:入力された値は、E メールエンドポイントが入力の選択に使用するファイルパターンです。 例えば、マッピングの種類に「変数」を選択し、入力ドキュメントをPDF・ファイルにする場合、 `*.pdf` をマッピング値として使用します。

**マッピング値**:マッピングタイプの値を指定します。 例えば、変数マッピングタイプを選択した場合、 `*.pdf` をファイルパターンとして使用します。

**データタイプ**:入力値のデータタイプを指定します。 例えば、この節で紹介するプロセスの入力値のデータ型は com.adobe.idp.Document です。

**出力パラメータ値の定義**

電子メールエンドポイントを作成する場合、出力パラメーターの値を定義する必要があります。 つまり、E メールエンドポイントによって呼び出されるサービスによって返される出力値を記述する必要があります。 例えば、このトピックで導入されたプロセスを考えてみましょう。 これには、 `SecuredDoc` で、そのデータタイプは `com.adobe.idp.Document`. このプロセスの E メールエンドポイントを作成する場合（プロセスがアクティブ化されると、サービスになります）、出力パラメーターの値を定義する必要があります。

電子メールエンドポイントに必要な出力パラメーター値を定義するには、次の値を指定します。

**出力パラメーター名**:出力パラメーターの名前。 プロセス出力値の名前は、Workbench で指定します。 出力値がサービス操作（Workbench で作成されたプロセスではないサービス）に属する場合、出力名は component.xml ファイルで指定されます。 例えば、この節で紹介するプロセスの出力パラメーターの名前は、 `SecuredDoc`.

**マッピングタイプ**:サービスと操作の出力を設定するために使用します。 以下のオプションが利用できます。

* サービスが 1 つのオブジェクト（1 つのドキュメント）を返す場合、パターンは「 `%F.pdf` ソースの宛先は sourcefilename.pdf です。 例えば、この節で紹介したプロセスは、1 つのドキュメントを返します。 その結果、マッピングタイプは `%F.pdf` ( `%F` は、指定されたファイル名を使用することを意味します )。 パターン `%E` 入力ドキュメントの拡張を指定します。
* サービスがリストを返す場合、パターンは次のようになります。 `Result\%F\`の場合、ソースの宛先は Result\sourcefilename\source1 （出力 1）および Result\sourcefilename\source2 （出力 2）です。
* サービスがマップを返した場合、パターンは次のようになります。 `Result\%F\`の場合、ソースの宛先は Result\sourcefilename\file1 および Result\sourcefilename\file2 です。 マップに複数のオブジェクトがある場合、パターンは次のようになります。 `Result\%F.pdf` ソースの宛先は Result\sourcefilename1.pdf （出力 1）、Result\sourcefilenam2.pdf （出力 2）などです。

**データタイプ**:戻り値のデータ型を指定します。 例えば、この節で導入されるプロセスの戻り値のデータ型はです `com.adobe.idp.Document`.

**E メールエンドポイントの作成**

電子メールエンドポイントの属性と設定値を設定し、入力および出力パラメーターの値を定義した後、電子メールエンドポイントを作成する必要があります。

**エンドポイントを有効にする**

E メールエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。 エンドポイントが有効な場合、エンドポイントを使用してサービスを呼び出すことができます。 エンドポイントを有効にすると、管理コンソール内で表示できます。

**関連トピック**

[Java API を使用した電子メールエンドポイントの追加](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した電子メールエンドポイントの追加 {#add-an-email-endpoint-using-the-java-api}

Java API を使用して電子メールエンドポイントを追加します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-livecycle-client.jar などのクライアント JAR ファイルを含めます。

1. EndpointRegistry Client オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EndpointRegistryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 電子メールエンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * を呼び出して、コネクタ識別子の値を指定します。 `CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドと文字列値を渡す `Email`.
   * を呼び出して、エンドポイントの説明を指定します。 `CreateEndpointInfo` オブジェクトの `setDescription` メソッドを使用してエンドポイントを表す string 値を渡す方法を示します。
   * を呼び出して、エンドポイントの名前を指定します。 `CreateEndpointInfo` オブジェクトの `setName` メソッドを使用して、名前を指定する string 値を渡す。
   * を呼び出して、エンドポイントが属するサービスを指定します。 `CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを使用して、サービス名を指定する string 値を渡す。
   * を呼び出して呼び出す操作を指定します。 `CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを使用して、操作名を指定する string 値を渡す。 通常、Workbench で作成されたプロセスから生成されたサービスの電子メールエンドポイントを作成する場合、操作の名前は invoke になります。

1. 設定値を指定します。

   電子メールエンドポイントに設定する設定値ごとに、 `CreateEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッド。 例えば、 `smtpHost` 設定値、 `CreateEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッドを使用して、次の値を渡します。

   * 設定値の名前を指定する string 値です。 設定時に `smtpHost` 設定値、指定 `smtpHost`.
   * 設定値の値を指定する string 値。 設定時に `smtpHost` 設定値：SMTP サーバーの名前を指定する string 値を指定します。

   >[!NOTE]
   >
   >この節で紹介する EncryptDocument サービスに設定されたすべての設定値を確認するには、次の Java コードの例を参照してください。 [クイックスタート：Java API を使用した電子メールエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. 入力パラメーター値を定義します。

   を呼び出して、入力パラメーター値を定義する `CreateEndpointInfo` オブジェクトの `setInputParameterMapping` メソッドを使用して、次の値を渡します。

   * 入力パラメーターの名前を指定する string 値。 例えば、EncryptDocument サービスの入力パラメーターの名前は次のようになります。 `InDoc`.
   * 入力パラメーターのデータ型を指定する string 値です。 例えば、 `InDoc` 入力パラメーター： `com.adobe.idp.Document`.
   * マッピングタイプを指定する string 値。 例えば、次の項目を指定できます。 `variable`.
   * マッピングタイプの値を指定する string 値。 例えば、&amp;ast;.pdf をファイルパターンとして指定できます。

   >[!NOTE]
   >
   >を呼び出す `setInputParameterMapping` メソッドを使用します。 EncryptDocument プロセスには 1 つの入力パラメーターしかないので、このメソッドを 1 回呼び出す必要があります。

1. 出力パラメータ値を定義します。

   を呼び出して、出力パラメーター値を定義する `CreateEndpointInfo` オブジェクトの `setOutputParameterMapping` メソッドを使用して、次の値を渡します。

   * 出力パラメーターの名前を指定する string 値。 例えば、EncryptDocument サービスの出力パラメーターの名前は次のようになります。 `SecuredDoc`.
   * 出力パラメーターのデータ型を指定する string 値です。 例えば、 `SecuredDoc` 出力パラメーターは `com.adobe.idp.Document`.
   * マッピングタイプを指定する string 値。 例えば、次の項目を指定できます。 `%F.pdf`.

1. E メールエンドポイントを作成します。

   を呼び出してエンドポイントを作成する `EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドおよび `CreateEndpointInfo` オブジェクト。 このメソッドは、 `Endpoint` E メールエンドポイントを表すオブジェクト。

1. エンドポイントを有効にします。

   を呼び出してエンドポイントを有効にする `EndpointRegistryClient` オブジェクトの `enable` メソッドおよび `Endpoint` が返したオブジェクト `createEndpoint` メソッド。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用した監視フォルダーエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### メール設定値の定数ファイル {#email-configuration-values-constant-file}

この [クイックスタート：Java API を使用した電子メールエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) は、クイックスタートをコンパイルするために Java プロジェクトの一部である必要がある定数ファイルを使用します。 この定数ファイルは、電子メールエンドポイントを追加する際に設定する必要がある設定値を表します。 次の Java コードは、定数ファイルを表しています。

```as3
 /** 
     * This class contains constants that can be used when setting email endpoint  
     * configuration values 
     */ 
 public class EmailEndpointConfigConstants { 
      
     public static final String PROPERTY_EMAILPROVIDER_CRON_EXPRESSION = "cronExpression"; 
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_COUNT = "repeatCount"; 
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_INTERVAL = "repeatInterval"; 
     public static final String PROPERTY_EMAILPROVIDER_START_DELAY = "startDelay"; 
     public static final String PROPERTY_EMAILPROVIDER_BATCH_SIZE = "batchSize"; 
     public static final String PROPERTY_EMAILPROVIDER_USERNAME = "userName"; 
     public static final String PROPERTY_EMAILPROVIDER_DOMAINNAME = "domainName"; 
     public static final String PROPERTY_EMAILPROVIDER_DOMAINPATTERN = "domainPattern"; 
     public static final String PROPERTY_EMAILPROVIDER_FILEPATTERN = "filePattern"; 
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_SUCCESSFUL_JOB = "recipientSuccessfulJob"; 
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_FAILED_JOB = "recipientFailedJob"; 
     public static final String PROPERTY_EMAILPROVIDER_INBOX_HOST = "inboxHost"; 
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PORT = "inboxPort"; 
     public static final String PROPERTY_EMAILPROVIDER_PROTOCOL = "inboxProtocol"; 
     public static final String PROPERTY_EMAILPROVIDER_INBOX_TIMEOUT = "inboxTimeOut"; 
     public static final String PROPERTY_EMAILPROVIDER_INBOX_USER = "inboxUser"; 
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PASSWORD = "inboxPassword"; 
     public static final String PROPERTY_EMAILPROVIDER_INBOX_SSL = "inboxSSLEnabled"; 
     public static final String PROPERTY_EMAILPROVIDER_SMTP_HOST = "smtpHost"; 
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PORT = "smtpPort"; 
     public static final String PROPERTY_EMAILPROVIDER_SMTP_USER = "smtpUser"; 
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PASSWORD = "smtpPassword"; 
     public static final String PROPERTY_EMAILPROVIDER_CHARSET = "charSet"; 
     public static final String PROPERTY_EMAILPROVIDER_SMTP_SSL = "smtpSSLEnabled"; 
     public static final String PROPERTY_EMAILPROVIDER_FAILED_FOLDER = "failedJobFolder"; 
     public static final String PROPERTY_EMAILPROVIDER_ASYNCHRONOUS = "asynchronous"; 
 }
```

## リモートエンドポイントの追加 {#adding-remoting-endpoints}

>[!NOTE]
>
>JEE 上のAEM forms で非推奨となったLiveCycle RemotingAPI。

AEM Forms Java API を使用して、プログラムによってリモートエンドポイントをサービスに追加できます。 リモートエンドポイントを追加すると、リモート処理を使用してFlexアプリケーションからサービスを呼び出すことができます。 ( [(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

リモートエンドポイントをプログラムでサービスに追加する場合は、次の短時間のみ有効なプロセスを考慮してください。 *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

このプロセスは、セキュリティで保護されていないPDFドキュメントを入力値として受け取り、セキュリティで保護されていないPDFドキュメントを Encryption サービスの `EncryptPDFUsingPassword` 操作。 PDFドキュメントはパスワードで暗号化され、PDFドキュメントはこのプロセスの出力値です。 入力値 ( 保護されていないPDFドキュメント ) の名前は `InDoc` データタイプは `com.adobe.idp.Document`. 出力値の名前 ( パスワードで暗号化されたPDFドキュメント ) は `SecuredDoc` データタイプは `com.adobe.idp.Document`.

このセクションでは、EncryptDocument という名前のサービスにリモートエンドポイントを追加する方法を示します。

>[!NOTE]
>
>Web サービスを使用してリモートエンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-4}

エンドポイントをサービスから削除するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. の作成 `EndpointRegistryClient` オブジェクト。
1. リモートエンドポイントの属性を設定します。
1. リモートエンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry Client オブジェクトの作成**

プログラムによってリモートエンドポイントを追加するには、 `EndpointRegistryClient` オブジェクト。

**リモートエンドポイント属性の設定**

サービスのリモートエンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子の値**:作成するエンドポイントのタイプを指定します。 リモートエンドポイントを作成するには、次を指定します。 `Remoting`.
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子の値**:エンドポイントが属するサービスを指定します。 例えば、この節で説明するプロセスにリモートエンドポイントを追加する場合（Workbench 内でアクティベートすると、プロセスがサービスになります）に、 `EncryptDocument`.
* **操作名**:エンドポイントを使用して呼び出される操作の名前を指定します。 リモートエンドポイントを作成する場合は、ワイルドカード文字 (&amp;ast;) を指定します。

**リモートエンドポイントの作成**

リモートエンドポイント属性を設定した後、サービスのリモートエンドポイントを作成できます。

**エンドポイントを有効にする**

新しいエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。 リモートエンドポイントが有効な場合、Flexクライアントがサービスを呼び出すことができます。

**関連トピック**

[Java API を使用したリモートエンドポイントの追加](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したリモートエンドポイントの追加 {#add-a-remoting-endpoint-using-the-java-api}

Java API を使用してリモートエンドポイントを追加します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-livecycle-client.jar などのクライアント JAR ファイルを含めます。

1. EndpointRegistry Client オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EndpointRegistryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. リモートエンドポイントの属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * を呼び出して、コネクタ識別子の値を指定します。 `CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドと文字列値を渡す `Remoting`.
   * を呼び出して、エンドポイントの説明を指定します。 `CreateEndpointInfo` オブジェクトの `setDescription` メソッドを使用してエンドポイントを表す string 値を渡す方法を示します。
   * を呼び出して、エンドポイントの名前を指定します。 `CreateEndpointInfo` オブジェクトの `setName` メソッドを使用して、名前を指定する string 値を渡す。
   * を呼び出して、エンドポイントが属するサービスを指定します。 `CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを使用して、サービス名を指定する string 値を渡す。
   * によって呼び出される操作を指定します。 `CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを使用して、操作名を指定する string 値を渡す。 リモートエンドポイントの場合は、ワイルドカード文字 (&amp;ast;) を指定します。

1. リモートエンドポイントを作成します。

   を呼び出してエンドポイントを作成する `EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドおよび `CreateEndpointInfo` オブジェクト。 このメソッドは、 `Endpoint` 新しい Remoting エンドポイントを表すオブジェクト。

1. エンドポイントを有効にします。

   を呼び出してエンドポイントを有効にする `EndpointRegistryClient` オブジェクトの `enable` メソッドおよび `Endpoint` が返したオブジェクト `createEndpoint` メソッド。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用したリモートエンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## TaskManager エンドポイントの追加 {#adding-taskmanager-endpoints}

AEM Forms Java API を使用して、TaskManager エンドポイントをプログラムでサービスに追加できます。 TaskManager エンドポイントをサービスに追加することで、Workspace ユーザーがサービスを呼び出せるようにします。 つまり、Workspace で作業しているユーザーは、対応する TaskManager エンドポイントを持つプロセスを呼び出すことができます。

>[!NOTE]
>
>Web サービスを使用して TaskManager エンドポイントを追加することはできません。

### 手順の概要 {#summary_of_steps-5}

TaskManager エンドポイントをサービスに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. の作成 `EndpointRegistryClient` オブジェクト。
1. エンドポイントのカテゴリを作成します。
1. TaskManager エンドポイント属性を設定します。
1. TaskManager エンドポイントを作成します。
1. エンドポイントを有効にします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry Client オブジェクトの作成**

TaskManager エンドポイントをプログラムで追加する前に、 `EndpointRegistryClient` オブジェクト。

**エンドポイントのカテゴリの作成**

カテゴリは、Workspace 内のサービスを整理するために使用されます。 つまり、Workspace ユーザーは、Workspace 内のカテゴリを選択することで、TaskManager エンドポイントを持つサービスを呼び出すことができます。 TaskManager エンドポイントを作成する場合、既存のカテゴリを参照するか、新しいカテゴリをプログラムで作成できます。

>[!NOTE]
>
>このセクションでは、TaskManager エンドポイントをサービスに追加する際に、新しいカテゴリを作成します。

**TaskManager エンドポイント属性の設定**

サービスの TaskManager エンドポイントを作成するには、次の値を指定します。

* **コネクタ識別子**:作成するエンドポイントのタイプを指定します。 TaskManager エンドポイントを作成するには、次を指定します。 `TaskManagerConnector`.
* **説明**:エンドポイントの説明を指定します。
* **名前**:エンドポイントの名前を指定します。
* **サービス識別子**:エンドポイントが属するサービスを指定します。
* **カテゴリ**:TaskManager エンドポイントに関連付けられるカテゴリ識別子の値を指定します。
* **操作名**:通常、Workbench で作成されたプロセスから発生するサービスの TaskManager エンドポイントを作成する場合、操作の名前はです `invoke`.

**TaskManager エンドポイントの作成**

TaskManager エンドポイント属性を設定した後、サービスの TaskManager エンドポイントを作成できます。

**エンドポイントを有効にする**

新しいエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。 エンドポイントが有効な場合、Workspace 内からサービスを呼び出すために使用できます。 エンドポイントを有効にすると、管理コンソール内で表示できます。

**関連トピック**

[Java API を使用した TaskManager エンドポイントの追加](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した TaskManager エンドポイントの追加 {#add-a-taskmanager-endpoint-using-the-java-api}

Java API を使用して TaskManager エンドポイントを追加します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-livecycle-client.jar などのクライアント JAR ファイルを含めます。

1. EndpointRegistry Client オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EndpointRegistryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. エンドポイントのカテゴリを作成します。

   * の作成 `CreateEndpointCategoryInfo` オブジェクトを作成するには、コンストラクタを使用し、次の値を渡します。

      * カテゴリの識別子の値を指定する string 値
      * カテゴリの説明を指定する string 値です
   * を呼び出して、カテゴリを作成します。 `EndpointRegistryClient` オブジェクトの `createEndpointCategory` メソッドおよび `CreateEndpointCategoryInfo` オブジェクト。 このメソッドは、 `EndpointCategory` 新しいカテゴリを表すオブジェクト。


1. TaskManager エンドポイント属性を設定します。

   * コンストラクタを使用して `CreateEndpointInfo` オブジェクトを作成します。
   * を呼び出して、コネクタ識別子の値を指定します。 `CreateEndpointInfo` オブジェクトの `setConnectorId` メソッドと文字列値を渡す `TaskManagerConnector`.
   * を呼び出して、エンドポイントの説明を指定します。 `CreateEndpointInfo` オブジェクトの `setDescription` メソッドを使用してエンドポイントを表す string 値を渡す方法を示します。
   * を呼び出して、エンドポイントの名前を指定します。 `CreateEndpointInfo` オブジェクトの `setName` メソッドを使用して、名前を指定する string 値を渡す。
   * を呼び出して、エンドポイントが属するサービスを指定します。 `CreateEndpointInfo` オブジェクトの `setServiceId` メソッドを使用して、サービス名を指定する string 値を渡す。
   * を呼び出して、エンドポイントが属するカテゴリを指定します。 `CreateEndpointInfo` オブジェクトの `setCategoryId` メソッドを使用して、カテゴリ識別子の値を指定する string 値を渡す。 を呼び出すことができます。 `EndpointCategory` オブジェクトの `getId` メソッドを使用して、このカテゴリの識別子の値を取得します。
   * を呼び出して呼び出す操作を指定します。 `CreateEndpointInfo` オブジェクトの `setOperationName` メソッドを使用して、操作名を指定する string 値を渡す。 通常、 `TaskManager` Workbench で作成されたプロセスから派生するサービスのエンドポイントで、操作の名前は `invoke`.

1. TaskManager エンドポイントを作成します。

   を呼び出してエンドポイントを作成する `EndpointRegistryClient` オブジェクトの `createEndpoint` メソッドおよび `CreateEndpointInfo` オブジェクト。 このメソッドは、 `Endpoint` 新しい TaskManager エンドポイントを表すオブジェクト。

1. エンドポイントを有効にします。

   を呼び出してエンドポイントを有効にする `EndpointRegistryClient` オブジェクトの `enable` メソッドおよび `Endpoint` が返したオブジェクト `createEndpoint` メソッド。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用した TaskManager エンドポイントの追加](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントの変更 {#modifying-endpoints}

AEM Forms Java API を使用して、既存のエンドポイントをプログラムで変更できます。 エンドポイントを変更すると、エンドポイントの動作を変更できます。 例えば、監視フォルダーとして使用するフォルダーを指定する監視フォルダーエンドポイントがあるとします。 監視フォルダーエンドポイントに属する設定値をプログラムで変更することで、別のフォルダーが監視フォルダーとして機能するようになります。 監視フォルダーエンドポイントに属する設定値について詳しくは、 [監視フォルダーエンドポイントの追加](programmatically-endpoints.md#adding-watched-folder-endpoints).

この節では、エンドポイントを変更する方法を示すために、監視フォルダーとして動作するフォルダーを変更して、監視フォルダーエンドポイントを変更します。

>[!NOTE]
>
>Web サービスを使用してエンドポイントを変更することはできません。

### 手順の概要 {#summary_of_steps-6}

エンドポイントを変更するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. の作成 `EndpointRegistryClient` オブジェクト。
1. エンドポイントを取得します。
1. 新しい設定値を指定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry Client オブジェクトの作成**

エンドポイントをプログラムで変更するには、 `EndpointRegistryClient` オブジェクト。

**変更するエンドポイントを取得します**

エンドポイントを変更する前に、エンドポイントを取得する必要があります。 エンドポイントを取得するには、エンドポイントにアクセスできるユーザーとして接続する必要があります。 管理者として接続することをお勧めします。 ( [接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)) をクリックします。

エンドポイントのリストを取得して、エンドポイントを取得できます。 その後、リストを繰り返し処理し、削除する特定のエンドポイントを検索できます。 例えば、エンドポイントに対応するサービスとエンドポイントのタイプを指定して、エンドポイントを特定できます。 エンドポイントを見つけたら、変更できます。

**新しい設定値を指定する**

エンドポイントを変更する場合は、新しい設定値を指定します。 例えば、監視フォルダーエンドポイントを変更するには、変更するエンドポイントだけでなく、すべての監視フォルダーエンドポイント設定値をリセットします。 監視フォルダーエンドポイントに属する設定値について詳しくは、 [監視フォルダーエンドポイントの追加](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>E メールエンドポイントに属する設定値について詳しくは、 [電子メールエンドポイントの追加](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>エンドポイントによって呼び出されたサービスは変更できません。 サービスを変更しようとすると、例外が発生します。 特定のエンドポイントに関連付けられているサービスを変更するには、エンドポイントを削除し、新しく作成します。 ( [エンドポイントの削除](programmatically-endpoints.md#removing-endpoints).)

**関連トピック**

[Java API を使用したエンドポイントの変更](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したエンドポイントの変更 {#modifying-an-endpoint-using-the-java-api}

Java API を使用してエンドポイントを変更します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-livecycle-client.jar などのクライアント JAR ファイルを含めます。

1. EndpointRegistry Client オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EndpointRegistryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 変更するエンドポイントを取得します。

   * を呼び出して、現在のユーザー（接続プロパティで指定）がアクセスできるすべてのエンドポイントのリストを取得します。 `EndpointRegistryClient` オブジェクトの `getEndpoints` メソッドと `PagingFilter` オブジェクトを指定します。 次の条件を満たす場合に、 `(PagingFilter)null` 値を指定して、すべてのエンドポイントを返します。 このメソッドは、 `java.util.List` 各要素が `Endpoint` オブジェクト。 詳しくは、 `PagingFilter` オブジェクト： [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 反復処理 `java.util.List` オブジェクトを使用して、エンドポイントがあるかどうかを判断します。 エンドポイントが存在する場合、各要素は `EndPoint` インスタンス。
   * を呼び出して、エンドポイントに対応するサービスを判断する `EndPoint` オブジェクトの `getServiceId` メソッド。 このメソッドは、サービス名を指定する string 値を返します。
   * を呼び出して、エンドポイントのタイプを決定します。 `EndPoint` オブジェクトの `getConnectorId` メソッド。 このメソッドは、エンドポイントのタイプを指定する string 値を返します。 例えば、エンドポイントが監視フォルダーエンドポイントの場合、このメソッドは `WatchedFolder`.

1. 新しい設定値を指定します。

   * の作成 `ModifyEndpointInfo` オブジェクトを指定します。
   * 設定する設定値ごとに、 `ModifyEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッド。 例えば、URL 設定値を設定するには、 `ModifyEndpointInfo` オブジェクトの `setConfigParameterAsText` メソッドを使用して、次の値を渡します。

      * 設定値の名前を指定する string 値です。 例えば、 `url` 設定値、指定 `url`.
      * 設定値の値を指定する string 値。 の値を定義するには、以下を実行します。 `url` 設定値で、監視フォルダーの場所を指定します。
   * を呼び出す `EndpointRegistryClient` オブジェクトの `modifyEndpoint` メソッドを使用して、 `ModifyEndpointInfo` オブジェクト。


**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用したエンドポイントの変更](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントの削除 {#removing-endpoints}

AEM Forms Java API を使用して、プログラムによってエンドポイントをサービスから削除できます。 エンドポイントを削除すると、エンドポイントが有効になっている呼び出しメソッドを使用してサービスを呼び出すことはできなくなります。 例えば、サービスから SOAP エンドポイントを削除した場合、SOAP モードを使用してサービスを呼び出すことはできません。

この節では、サービスからエンドポイントを削除する方法を示すために、EJB エンドポイントを、という名前のサービスから削除します *EncryptDocument*.

>[!NOTE]
>
>Web サービスを使用してエンドポイントを削除することはできません。

### 手順の概要 {#summary_of_steps-7}

エンドポイントをサービスから削除するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. の作成 `EndpointRegistryClient` オブジェクト。
1. エンドポイントを取得します。
1. エンドポイントを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry Client オブジェクトの作成**

プログラムによってエンドポイントを削除するには、 `EndpointRegistryClient` オブジェクト。

**削除するエンドポイントを取得します**

エンドポイントを削除する前に、エンドポイントを取得する必要があります。 エンドポイントを取得するには、エンドポイントにアクセスできるユーザーとして接続する必要があります。 管理者として接続することをお勧めします。 ( [接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)) をクリックします。

エンドポイントのリストを取得して、エンドポイントを取得できます。 その後、リストを繰り返し処理し、削除する特定のエンドポイントを検索できます。 例えば、エンドポイントに対応するサービスとエンドポイントのタイプを指定して、エンドポイントを特定できます。 エンドポイントを見つけたら、そのエンドポイントを削除できます。

**エンドポイントを削除**

新しいエンドポイントを作成したら、そのエンドポイントを有効にする必要があります。 エンドポイントが有効な場合、エンドポイントを使用してサービスを呼び出すことができます。 エンドポイントを有効にすると、管理コンソール内で表示できます。

**関連トピック**

[Java API を使用したエンドポイントの削除](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したエンドポイントの削除 {#removing-an-endpoint-using-the-java-api}

Java API を使用してエンドポイントを削除します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-livecycle-client.jar などのクライアント JAR ファイルを含めます。

1. EndpointRegistry Client オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * の作成 `EndpointRegistryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 削除するエンドポイントを取得します。

   * を呼び出して、現在のユーザー（接続プロパティで指定）がアクセス権を持つすべてのエンドポイントのリストを取得します。 `EndpointRegistryClient` オブジェクトの `getEndpoints` メソッドと `PagingFilter` オブジェクトを指定します。 パス `(PagingFilter)null` を使用して、すべてのエンドポイントを返します。 このメソッドは、 `java.util.List` 各要素が `Endpoint` オブジェクト。
   * 反復処理 `java.util.List` オブジェクトを使用して、エンドポイントがあるかどうかを判断します。 エンドポイントが存在する場合、各要素は `EndPoint` インスタンス。
   * を呼び出して、エンドポイントに対応するサービスを判断する `EndPoint` オブジェクトの `getServiceId` メソッド。 このメソッドは、サービス名を指定する string 値を返します。
   * を呼び出して、エンドポイントのタイプを決定します。 `EndPoint` オブジェクトの `getConnectorId` メソッド。 このメソッドは、エンドポイントのタイプを指定する string 値を返します。 例えば、エンドポイントが EJB エンドポイントの場合、このメソッドはを返します `EJB`.

1. エンドポイントを削除します。

   を呼び出してエンドポイントを削除する `EndpointRegistryClient` オブジェクトの `remove` メソッドおよび `EndPoint` 削除するエンドポイントを表すオブジェクト。

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用したエンドポイントの削除](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## エンドポイントコネクタ情報の取得 {#retrieving-endpoint-connector-information}

AEM Forms API を使用して、エンドポイントコネクタに関する情報をプログラムで取得できます。 コネクタは、様々な呼び出しメソッドを使用してエンドポイントからサービスを呼び出すことを可能にします。 例えば、監視フォルダーコネクタを使用すると、エンドポイントは監視フォルダーを使用してサービスを呼び出すことができます。 プログラムによってエンドポイントコネクタに関する情報を取得することで、必要な設定値や任意の設定値など、コネクタに関連付けられた設定値を取得できます。

この節では、エンドポイントコネクタに関する情報を取得する方法を示すために、監視フォルダーコネクタに関する情報を取得します。 ( [監視フォルダーエンドポイントの追加](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>Web サービスを使用してエンドポイントに関する情報を取得することはできません。

>[!NOTE]
>
>このトピックでは、 `ConnectorRegistryClient` エンドポイントコネクタに関する情報を取得する API。 ( [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### 手順の概要 {#summary_of_steps-8}

エンドポイントコネクタ情報を取得するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. の作成 `ConnectorRegistryClient` オブジェクト。
1. コネクタのタイプを指定します。
1. 設定値を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
* jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

AEM Formsが JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar と jbossall-client.jar を、AEM Formsがデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換えます。 すべてのAEM Forms JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**ConnectorRegistry Client オブジェクトの作成**

プログラムによってエンドポイントコネクタ情報を取得するには、 `ConnectorRegistryClient` オブジェクト。

**コネクタのタイプを指定**

情報を取得するコネクタのタイプを指定します。 次のタイプのコネクタが存在します。

* **EJB**:クライアントアプリケーションが EJB モードを使用してサービスを呼び出せるようにします。
* **SOAP**:クライアントアプリケーションが SOAP モードを使用してサービスを呼び出せるようにします。
* **監視フォルダー**:監視フォルダーがサービスを呼び出せるようにします。
* **電子メール**:電子メールメッセージでサービスを呼び出せるようにします。
* **リモート**:Flexクライアントアプリケーションがサービスを呼び出せるようにします。
* **TaskManagerConnector**:Workspace ユーザーが Workspace 内からサービスを呼び出せるようにします。

**設定値の取得**

コネクタタイプを指定した後、サポートされている設定値など、コネクタに関する情報を取得できます。 例えば、任意のコネクタの場合、必要な設定値とオプションの設定値を決定できます。

**関連トピック**

[Java API を使用したエンドポイントコネクタ情報の取得](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したエンドポイントコネクタ情報の取得 {#retrieve-endpoint-connector-information-using-the-java-api}

Java API を使用して、エンドポイントコネクタ情報を取得します。

1. プロジェクトファイルを含めます。.

   Java プロジェクトのクラスパスに、adobe-livecycle-client.jar などのクライアント JAR ファイルを含めます。

1. ConnectorRegistry Client オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ConnectorRegistryClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. コネクタのタイプを指定します。

   を呼び出して、コネクタのタイプを指定します。 `ConnectorRegistryClient` オブジェクトの `getEndpointDefinition` メソッドを使用して、コネクタの種類を指定する string 値を渡します。 例えば、監視フォルダーのコネクタタイプを指定するには、文字列値を渡します `WatchedFolder`. このメソッドは、 `Endpoint` コネクタの種類に対応するオブジェクト。

1. 設定値を取得します。

   * を呼び出して、このエンドポイント内で関連付けられている設定値を取得します。 `Endpoint` オブジェクトの `getConfigParameters` メソッド。 このメソッドは、 `ConfigParameter` オブジェクト。
   * 配列内の各要素を取得して、各設定値に関する情報を取得します。 各要素は `ConfigParameter` オブジェクト。 例えば、設定値が必須かオプションかを、 `ConfigParameter` オブジェクトの `isRequired` メソッド。 設定値が必要な場合、このメソッドは `true`.

**関連トピック**

[手順の概要](programmatically-endpoints.md#summary-of-steps)

[クイックスタート：Java API を使用したエンドポイントコネクタ情報の取得](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
