---
title: AEM Forms Repository の操作
seo-title: Working with AEM Forms Repository
description: AEM Forms API と Web Service API を使用して、フォルダーの作成、書き込み、リスト作成、リソースの読み取り、更新、およびリソースの検索をおこなうための Java リポジトリを管理します。 さらに、リソースの関係の作成、リソースのロックと削除の方法についても説明します。
seo-description: Manage AEM Forms repository to create folders, write, list, read, update resources, and search resources using the Java API and Web Service API. In addition, learn how to create resource relationships, lock and delete resources.
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
role: Developer
exl-id: e006c32b-edff-40f2-8c0a-228008dcf03a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '9110'
ht-degree: 2%

---

# AEM Forms Repository の操作 {#working-with-aem-forms-repository}

**Repository サービスについて**

Repository サービスは、リソースストレージと管理サービスをAEM Formsに提供します。 開発者が *AEM Forms* アプリケーションでは、ファイルシステムの代わりにリポジトリにアセットをデプロイできます。 アセットには、XML 形式、PDF 形式（Acrobat 形式を含む）、フォームのフラグメント、画像、プロファイル、ポリシー、SWF ファイル、DDX ファイル、XML スキーマ、WSDL ファイルおよびテストデータなど、任意のタイプのコラテラルが含まれます。

例えば、次のFormsアプリケーションの名前を考えてみましょう。 *Applications/FormsApplication*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

FormsFolder に Loan.xdp という名前のファイルがあることに注意してください。 このフォームデザインにアクセスするには、次のパス（バージョンを含む）を指定します。 `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Workbench を使用したFormsアプリケーションの作成について詳しくは、 [Workbench ヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63).

AEM Formsリポジトリ内のリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

次に、URI 値の例を示します。

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>Web ブラウザーを使用してAEM Formsリポジトリを参照できます。 リポジトリを参照するには、次の URL を Web ブラウザーに入力しますhttps://[サーバー名]:[サーバーポート]/repository. Web ブラウザーを使用して、「 AEM Formsリポジトリの操作」セクションに関連付けられたクイックスタートの結果を確認できます。 例えば、AEM Formsリポジトリにコンテンツを追加すると、そのコンテンツは Web ブラウザーに表示されます。 ( [クイックスタート（SOAP モード）:Java API を使用したリソースの書き込み](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

リポジトリ API は、リポジトリから情報を保存および取得するために使用できる多数の操作を提供します。 例えば、リソースのリストを取得したり、アプリケーションの処理の一環としてリソースが必要な場合にリポジトリに保存されている特定のリソースを取得したりできます。

>[!NOTE]
>
>リポジトリ API は、Content Services（非推奨）とのやり取りには使用できません。 Content Services（非推奨）を操作するには、Document Management API を使用します。

Repository サービス API を使用すると、次のタスクを実行できます。

* フォルダーの作成. 詳しくは、 [フォルダーの作成](aem-forms-repository.md#creating-folders).
* リソースとそのプロパティを書き込みます。 詳しくは、 [リソースの書き込み](aem-forms-repository.md#writing-resources).
* 特定のコレクション内または他のリソースに関連するリソースのリスト。 詳しくは、 [リソースの一覧](aem-forms-repository.md#listing-resources).
* リソースとそのプロパティを読み取ります。 詳しくは、 [リソースの読み取り](aem-forms-repository.md#reading-resources).
* リソースとそのプロパティを更新します。 詳しくは、 [リソースの更新](aem-forms-repository.md#updating-resources).
* リソースの履歴、関連リソース、プロパティなどを検索します。 詳しくは、 [リソースの検索](aem-forms-repository.md#searching-for-resources).
* リソース間の関係を指定します。 詳しくは、 [リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships).
* リソースのロックとロック解除、アクセス制御リスト (ACL) の読み取りと書き込みなど、リソースアクセス制御の管理。 詳しくは、 [リソースのロック](aem-forms-repository.md#locking-resources).
* リソースとそのプロパティを削除します。 詳しくは、 [リソースの削除](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>リポジトリ API を使用すると、ECM リポジトリを使用して、リソースのアクセス制御の管理、リソースの検索、リソースの関係の指定を行うことはできません。

>[!NOTE]
>
>暗号化されたPDFがリポジトリに書き込まれると、自動関係抽出機能は使用できません。 そうしないと、暗号化されたPDFをリポジトリに保存し、後で取得することができます。 リポジトリから取得したPDFを復号化できます。

>[!NOTE]
>
>Repository サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## フォルダーの作成 {#creating-folders}

フォルダ（リソースコレクション）は、整理されたグループにオブジェクト（ファイルまたはリソース）を格納するために使用します。 フォルダーには、リソースと他のフォルダー（サブフォルダーとも呼ばれます）を含めることができます。 リソースは一度に 1 つのフォルダーにのみ保存できます。

ファイルはフォルダーからアクセス制御リスト (ACL) を継承し、サブフォルダーは親フォルダーから ACL を継承します。 したがって、子フォルダーを作成するには、親フォルダーが存在する必要があります。 IDE では、ファイル単位ではなく、フォルダー単位でのみ操作できます。 フォルダーのバージョンを設定することはできず、必要ありません。1 つのフォルダーには、データ自体は含まれていません。 データを含むリソースのコンテナにすぎません。 デフォルトの ACL はシステムレベルの権限です。つまり、ユーザーが特定のフォルダに対する権限を付与するまで、ユーザーはシステムレベルの権限（読み取り、書き込み、トラバース、ACL の管理）を持つ必要があります。 ACL は IDE でのみ機能します。

>[!NOTE]
>
>Repository サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

フォルダーを作成するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. サービスクライアントを作成します。
1. フォルダーを作成します。
1. フォルダーをリポジトリに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソース収集を作成する前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実行されます。

**フォルダーの作成**

Repository サービスメソッドを呼び出して、リソースコレクションを作成し、UUID、フォルダー名、説明などの識別情報をリソースコレクションに設定します。

**フォルダーをリポジトリに書き込みます**

Repository サービスメソッドを呼び出して、ターゲットフォルダーの URI を指定してリソースコレクションを書き込みます。

**関連トピック**

[Java API を使用したフォルダーの作成](aem-forms-repository.md#create-folders-using-the-java-api)

[Web サービス API を使用したフォルダーの作成](aem-forms-repository.md#create-folders-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したフォルダーの作成 {#create-folders-using-the-java-api}

Repository service API(Java) を使用してフォルダーを作成します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスにプロジェクトファイルを含めます。

1. サービスクライアントの作成

   の作成 `ResourceRepositoryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. フォルダーの作成

   リソースコレクションを作成するには、まず `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` オブジェクト。

   を呼び出す `repositoryInfomodelFactoryBean` オブジェクトの `newResourceCollection` メソッドを使用して、次のパラメーターを渡します。

   * A `com.adobe.repository.infomodel.Id` リソースに割り当てる UUID 識別子。
   * A `com.adobe.repository.infomodel.Lid` リソースに割り当てる UUID 識別子。
   * A `java.lang.String` リソースコレクションの名前を含む。 （例：`FormsFolder`）。

   このメソッドは、 `com.adobe.repository.infomodel.bean.ResourceCollection` 新しいフォルダーを表すオブジェクト。

   フォルダーの説明を設定するには、 `setDescription` メソッドを使用して、次のパラメーターを渡します。

   * A `String` リソースの収集を表します。 この例では、 `"test Folder"` が使用されています `.`


1. フォルダーをリポジトリに書き込みます

   を呼び出す `ResourceRepositoryClient` オブジェクトの `writeResource` メソッドを使用して、フォルダーの URI と `ResourceCollection` オブジェクト。 例えば、フォルダーの URI は次の値になります `/Applications/FormsApplication/1.0/`.

   メソッドは、新しく作成されたのインスタンスを返します `com.adobe.repository.infomodel.bean.Resource` オブジェクト。 例えば、新しいリソースの識別子の値を取得するには、 `com.adobe.repository.infomodel.bean.Resource` オブジェクトの `getId` メソッド。

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[クイックスタート（SOAP モード）:Java API を使用したフォルダーの作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したフォルダーの作成 {#create-folders-using-the-web-service-api}

Repository service API（Web サービス）を使用してフォルダーを作成します。

1. プロジェクトファイルを含める

   * base64 を使用して、Repository WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、 `RepositoryServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。 設定 `Credentials` プロパティを `System.Net.NetworkCredential` ユーザー名とパスワードを含むオブジェクト。

1. フォルダーの作成

   フォルダーを作成するには、 `ResourceCollection` クラスを渡し、次のパラメーターを渡します。

   * An `Id` オブジェクト。 `Id` クラスに割り当てられ、 `Resource` オブジェクトの `id` フィールドに入力します。
   * An `Lid` オブジェクト。 `Lid` クラスに割り当てられ、 `Resource` オブジェクトの `lid` フィールドに入力します。
   * リソースコレクションの名前を含む文字列で、 `Resource` オブジェクトの `name` フィールドに入力します。 この例で使用される名前は、 `"testfolder"`.
   * リソースコレクションの説明を含む文字列で、 `Resource` オブジェクトの `description` フィールドに入力します。 この例で使用される説明は次のとおりです。 `"test folder"`.

1. フォルダーをリポジトリに書き込みます

   を呼び出す `RepositoryServiceService` オブジェクトの `writeResource` メソッドを使用して、次のパラメーターを渡します。

   * フォルダーを作成するパス。
   * この `ResourceCollection` フォルダーを表すオブジェクト。
   * パス `null` 他の 2 つのパラメータに対して

**関連トピック**

[フォルダーの作成](aem-forms-repository.md#creating-folders)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの書き込み {#writing-resources}

リポジトリ内の特定の場所にリソースを作成できます。 自然なファイルサイズは、データベースの制限やセッションタイムアウトの影響を受けます。 デフォルトの設定では、ファイルのサイズは 25 MB に制限されます。 最大ファイルサイズを増減するには、データベース設定を変更する必要があります。

リソースの書き込みは、リポジトリにデータを保存することと同じです。 リソースをリポジトリに書き込むと、リポジトリエコシステム内のすべてのクライアントがそのリソースにアクセスできるようになります。 XML スキーマ、XDP ファイル、XSD ファイルなどのリソースをリポジトリに書き込むと、その内容は MIME タイプに基づいて解析されます。 MIME タイプがサポートされている場合、パーサーは他のコンテンツとの暗黙の関係があるかどうかを判断します。 例えば、カスケーディングスタイルシート (CSS) に共通の CSS を参照する相対 URL がある場合、共通の CSS もリポジトリに送信する必要があります。 2 つのリソース間の関係は、調整可能でない期間 30 日間の保留関係として保存されます。 30 日以内にリポジトリに共通の CSS を送信すると、関係が形成されます。

リソースを作成すると、アクセス制御リスト (ACL) は親フォルダーから継承されます。 ルートフォルダーには、初期のリソースまたはフォルダーが作成されるまで、システムレベルの権限が割り当てられます。その時点で、リソースまたはフォルダーにデフォルトの ACL 権限が付与されます。

Repository service Java API または Web サービス API を使用して、プログラムによってリソースを書き込むことができます。

>[!NOTE]
>
>Repository サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

リソースを書き込むには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repository サービスクライアントを作成します。
1. 読み取るリソースの URI を指定します。
1. リソースを読み取ります。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実行されます。

**リソースのターゲットフォルダーの URI を指定**

読み取るリソースの URI を含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*パス*/*フォルダー*&quot;.

**リソースの作成**

Repository サービスメソッドを呼び出してリソースを作成し、UUID、リソース名、説明などの識別情報をリソースに設定します。

**リソースコンテンツの指定**

Repository サービスメソッドを呼び出して、リソースコンテンツを作成し、そのコンテンツをリソースに格納します。

**ターゲットフォルダにリソースを書き込む**

Repository サービスメソッドを呼び出して、ターゲットフォルダーの URI を指定してリソースを書き込みます。

**関連トピック**

[Java API を使用したリソースの書き込み](aem-forms-repository.md#write-resources-using-the-java-api)

[Web サービス API を使用したリソースの書き込み](aem-forms-repository.md#write-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したリソースの書き込み {#write-resources-using-the-java-api}

Repository service API(Java) を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   の作成 `ResourceRepositoryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. リソースのターゲットフォルダーの URI を指定

   リソースのターゲットフォルダーの URI を指定します。 この場合、 `testResource` は、 `testFolder`の場合、フォルダーの URI は、 `"/testFolder"`. URI は `java.lang.String` オブジェクト。

1. リソースの作成

   リソースを作成するには、まず `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` オブジェクト。

   を呼び出す `RepositoryInfomodelFactoryBean` オブジェクトの `newResource` メソッド（作成する） `com.adobe.repository.infomodel.bean.Resource` オブジェクト。 この例では、次のパラメーターが提供されます。

   * A `com.adobe.repository.infomodel.Id` オブジェクト。 `Id` クラス。
   * A `com.adobe.repository.infomodel.Lid` オブジェクト。 `Lid` クラス。
   * A `java.lang.String` リソースのファイル名を含みます。

   リソースの説明を指定するには、 `Resource` オブジェクトの `setDescription` メソッドを使用して、説明を含む文字列を渡します。 この例では、説明は次のようになります。 `"test resource"`.

1. リソースコンテンツの指定

   リソースのコンテンツを作成するには、 `RepositoryInfomodelFactoryBean` オブジェクトの `newResourceContent` メソッド。 `com.adobe.repository.infomodel.bean.ResourceContent` オブジェクト。 次にコンテンツを追加： `ResourceContent` オブジェクト。 この例では、次のタスクを実行して実行します。

   * の呼び出し `ResourceContent` オブジェクトの `setDataDocument` メソッドを使用し、 `com.adobe.idp.Document` object
   * の呼び出し `ResourceContent` オブジェクトの `setSize` メソッドを使用し、のサイズをバイト単位で渡す `Document` object

   を呼び出して、コンテンツをリソースに追加します。 `Resource` オブジェクトの `setContent` メソッドを使用して `ResourceContent` オブジェクト。 詳しくは、 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. ターゲットフォルダにリソースを書き込む

   を呼び出す `ResourceRepositoryClient` オブジェクトの `writeResource` メソッドを使用して、フォルダーの URI と `Resource` オブジェクト。

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[クイックスタート（SOAP モード）:Java API を使用したリソースの書き込み](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースの書き込み {#write-resources-using-the-web-service-api}

Repository service API（Web サービス）を使用してリソースを書き込みます。

1. プロジェクトファイルを含める

   * base64 を使用して、Repository WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、 `RepositoryServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。 設定 `Credentials` プロパティを `System.Net.NetworkCredential` ユーザー名とパスワードを含むオブジェクト。

1. リソースのターゲットフォルダーの URI を指定

   リソースのターゲットフォルダーの URI を指定します。 この場合、 `testResource` は、 `testFolder`の場合、フォルダーの URI は、 `"/testFolder"`. Microsoft .NET Framework に準拠している言語（例：C#）を使用する場合、URI を `System.String` オブジェクト。

1. リソースの作成

   リソースを作成するには、 `Resource` クラス。 この例では、次の情報が `Resource` オブジェクト：

   * A `com.adobe.repository.infomodel.Id` オブジェクト。 `Id` クラスに割り当てられ、 `Resource` オブジェクトの `id` フィールドに入力します。
   * A `com.adobe.repository.infomodel.Lid` オブジェクト。 `Lid` クラスに割り当てられ、 `Resource` オブジェクトの `lid` フィールドに入力します。
   * リソースのファイル名を含む文字列で、 `Resource` オブジェクトの `name` フィールドに入力します。 この例で使用される名前は、 `"testResource"`.
   * リソースの説明を含む文字列で、 `Resource` オブジェクトの `description` フィールドに入力します。 この例で使用される説明は次のとおりです。 `"test resource"`.

1. リソースコンテンツの指定

   リソースのコンテンツを作成するには、 `ResourceContent` クラス。 次に、 `ResourceContent` オブジェクト。 この例では、次のタスクを実行して実行します。

   * の割り当て `BLOB` ドキュメントを含むオブジェクトを `ResourceContent` オブジェクトの `dataDocument` フィールドに入力します。
   * のサイズ（バイト単位）の割り当て `BLOB` オブジェクトを `ResourceContent` オブジェクトの `size` フィールドに入力します。

   コンテンツをリソースに追加するには、 `ResourceContent` オブジェクトを `Resource` オブジェクトの `content` フィールドに入力します。

1. ターゲットフォルダにリソースを書き込む

   を呼び出す `RepositoryServiceService` オブジェクトの `writeResource` メソッドを使用して、フォルダーの URI と `Resource` オブジェクト。 パス `null` 他の 2 つのパラメータに対して

**関連トピック**

[リソースの書き込み](aem-forms-repository.md#writing-resources)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの一覧 {#listing-resources}

リソースを一覧表示することで、リソースを見つけることができます。 リポジトリに対してクエリが実行され、特定のリソースコレクションに関連するすべてのリソースが検索されます。

リソースを整理したら、オペレーティングシステムでおこなうように、構造の特定のブランチを表示して、作成した構造を検査できます。

リソースのリストは、次の関係によって機能します。リソースは、フォルダーのメンバーです。 メンバーシップは、「member of」タイプの関係で表されます。 特定のフォルダ内のリソースをリストする場合、「メンバー」の関係によって特定のフォルダに関連するリソースを照会します。 関係は方向性を持ちます。関係のメンバーには、ターゲットのメンバーであるソースがあります。 ソースはリソースです。ターゲットは親フォルダーです。

>[!NOTE]
>
>Repository サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

リソースを一覧表示するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. サービスクライアントを作成します。
1. フォルダーパスを指定します。
1. リソースのリストを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソース収集を作成する前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実行されます。

**フォルダーパスを指定**

リソースを含むフォルダーのパスを含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*パス*/*フォルダー*&quot;.

**リソースのリストの取得**

Repository サービスメソッドを呼び出して、ターゲットフォルダーのパスを指定して、リソースのリストを取得します。

**関連トピック**

[Java API を使用したリソースのリスト](aem-forms-repository.md#list-resources-using-the-java-api)

[Web サービス API を使用したリソースのリスト](aem-forms-repository.md#list-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したリソースのリスト {#list-resources-using-the-java-api}

Repository サービス API(Java) を使用してリソースをリストします。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   の作成 `ResourceRepositoryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. フォルダーパスを指定

   問い合わせるリソースコレクションの URI を指定します。 この場合、URI は `"/testFolder"`. URI は `java.lang.String` オブジェクト。

1. リソースのリストの取得

   を呼び出す `ResourceRepositoryClient` オブジェクトの `listMembers` メソッドを使用して、フォルダーの URI を渡します。

   このメソッドは、 `java.util.List` / `com.adobe.repository.infomodel.bean.Resource` ソースのオブジェクト `com.adobe.repository.infomodel.bean.Relation` タイプ `Relation.TYPE_MEMBER_OF` リソースコレクション URI をターゲットに設定します。 繰り返し実行できます `List` を使用して各リソースを取得します。 この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースの一覧](aem-forms-repository.md#listing-resources).

[クイックスタート（SOAP モード）:Java API を使用したリソースの一覧](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースのリスト {#list-resources-using-the-web-service-api}

Repository サービス API（Web サービス）を使用してリソースをリストします。

1. プロジェクトファイルを含める

   * リポジトリ WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、 `RepositoryServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。 設定 `Credentials` プロパティを `System.Net.NetworkCredential` ユーザー名とパスワードを含むオブジェクト。

1. フォルダーパスを指定

   照会するフォルダーの URI を含む文字列を指定します。 この場合、URI は `"/testFolder"`. Microsoft .NET Framework に準拠している言語（C#など）を使用する場合、URI を `System.String` オブジェクト。

1. リソースのリストの取得

   を呼び出す `RepositoryServiceService` オブジェクトの `listMembers` メソッドを使用し、フォルダーの URI を最初のパラメーターとして渡します。 パス `null` 他の 2 つのパラメータに対して

   メソッドは、キャスト可能なオブジェクトの配列を返します。 `Resource` オブジェクト。 オブジェクト配列を繰り返し処理して、関連する各リソースを取得できます。 この例では、各リソースの名前と説明が表示されます。

**関連トピック**

[リソースの一覧](aem-forms-repository.md#listing-resources).

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの読み取り {#reading-resources}

リポジトリ内の特定の場所からリソースを取得して、そのコンテンツとメタデータを読み取ることができます。 ワークフローは、初期化フォームによってフロントエンドに表示されます。 プロセスには、フォームを読み取るために必要なすべての権限があります。 システムがデータフォームを取得し、リポジトリからコンテンツを読み取ります。 リポジトリーは、コンテンツとメタデータへのアクセス権を付与します（リソースが存在することを知る機能も付与します）。

リポジトリには次の 4 つの権限タイプがあります。

* **traverse**:では、リソースのリストを表示できます。つまり、リソースのメタデータを読み取りますが、リソースの内容は読み取りません。
* **読み取り**:リソースコンテンツを読み取ることができます
* **書き込み**:リソースコンテンツの書き込みを許可
* **アクセス制御リスト (ACL) の管理**:では、リソース上の ACL を操作できます

ユーザーは、プロセスを実行する権限を持っている場合にのみ、プロセスを実行できます。 IDE ユーザーは、リポジトリと同期するには、traverse 権限と read 権限が必要です。 実行時はシステムコンテキスト内で発生するので、ACL は設計時にのみ適用されます。

Repository service Java API または Web サービス API を使用して、プログラムでリソースを読み取ることができます。

>[!NOTE]
>
>Repository サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

リソースを読み取るには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repository サービスクライアントを作成します。
1. 読み取るリソースの URI を指定します。
1. リソースを読み取ります。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実行されます。

**読み取るリソースの URI を指定**

読み取るリソースの URI を含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*パス*/*リソース*&quot;.

**リソースを読み取る**

Repository サービスメソッドを呼び出して、URI を指定してリソースを読み取ります。

**関連トピック**

[Java API を使用したリソースの読み取り](aem-forms-repository.md#read-resources-using-the-java-api)

[Web サービス API を使用したリソースの読み取り](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したリソースの読み取り {#read-resources-using-the-java-api}

Repository service API(Java) を使用してリソースを読み取ります。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   の作成 `ResourceRepositoryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 読み取るリソースの URI を指定

   取得するリソースの URI を表す string 値を指定します。 例えば、リソースの名前がの場合、 *testResource* は、 *testFolder*&#x200B;を指定します。 `/testFolder/testResource`.

1. リソースを読み取る

   を呼び出す `ResourceRepositoryClient` オブジェクトの `readResource` メソッドを使用し、リソースの URI をパラメーターとして渡します。 このメソッドは、 `Resource` リソースを表すインスタンス。

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[クイックスタート（SOAP モード）:Java API を使用したリソースの読み取り](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースの読み取り {#reading-resources-using-the-web-service-api}

Repository service API（Web サービス）を使用してリソースを読み取ります。

1. プロジェクトファイルを含める

   * リポジトリ WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。 ( [Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * Microsoft .NET クライアントアセンブリを参照します。 ( [Base64 エンコーディングを使用する.NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、 `RepositoryServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。 設定 `Credentials` プロパティを `System.Net.NetworkCredential` ユーザー名とパスワードを含むオブジェクト。

1. 読み取るリソースの URI を指定

   取得するリソースの URI を含む文字列を指定します。 この場合、 `testResource` は、次の名前のフォルダーにあります： `testFolder`の場合、その URI は `"/testFolder/testResource"`. Microsoft .NET Framework に準拠している言語（例：C#）を使用する場合、URI を `System.String` オブジェクト。

1. リソースを読み取る

   を呼び出す `RepositoryServiceService` オブジェクトの `readResource` メソッドを使用し、リソースの URI を最初のパラメーターとして渡します。 パス `null` 他の 2 つのパラメータに対して

**関連トピック**

[リソースの読み取り](aem-forms-repository.md#reading-resources)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの更新 {#updating-resources}

リポジトリ内のリソースのコンテンツを取得して更新できます。 リソースを更新しても、それらのリソースへのアクセス制御は、バージョン間で変更されません。 更新を実行する際に、メジャーバージョンを増分するオプションがあります。 メジャーバージョンを増分しない場合、マイナーバージョンは自動的に更新されます。

リソースを更新すると、指定したリソース属性に基づいて新しいバージョンが作成されます。 リソースを更新する際には、次の 2 つの重要なパラメータを指定します。ターゲット URI と、更新されたすべてのメタデータを含むリソースインスタンス。 特定の属性（名前など）を変更しない場合、その属性は渡すインスタンスで必要です。 コンテンツの解析時に作成される関係は、特定のバージョンに追加され、特に指定のない限りは反映されません。

例えば、XDP ファイルを更新し、そのファイルに他のリソースへの参照が含まれている場合、その他の参照も記録されます。 form.xdp バージョン 1.0 に次の 2 つの外部参照があるとします。ロゴとスタイルシートを作成し、その後 form.xdp を更新して、3 つの参照が含まれるようにします。ロゴ、スタイルシートおよびスキーマファイル。 更新中、リポジトリは 3 つ目の関係（スキーマファイル）を保留中の関係テーブルに追加します。 スキーマファイルがリポジトリに存在すると、関係は自動的に形成されます。 ただし、form.xdp バージョン 2.0 でロゴが使用されなくなった場合、form.xdp バージョン 2.0 はロゴとの関係を持ちません。

すべての更新操作はアトミックおよびトランザクションです。 例えば、2 人のユーザーが同じリソースを読み、両方のユーザーがバージョン 1.0 をバージョン 2.0 に更新した場合、いずれかが成功し、いずれかが失敗した場合、リポジトリの整合性は維持され、両方のユーザーに成功または失敗を確認するメッセージが表示されます。 トランザクションがコミットされない場合、データベース障害が発生した場合にロールバックされ、アプリケーションサーバーに応じてタイムアウトまたはロールバックされます。

Repository service Java API または Web サービス API を使用して、プログラムでリソースを更新できます。

>[!NOTE]
>
>Repository サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

リソースを更新するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repository サービスクライアントを作成します。
1. 更新するリソースを取得します。
1. リソースを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実行されます。

**更新するリソースを取得します**

リソースを読み取ります。 詳しくは、 [リソースの読み取り](aem-forms-repository.md#reading-resources).

**リソースを更新**

リソースに新しい情報を設定し、Repository サービスメソッドを呼び出して、リソースを更新し、URI、更新されたリソース、およびバージョン情報の更新方法を指定します。

**関連トピック**

[Java API を使用したリソースの更新](aem-forms-repository.md#update-resources-using-the-java-api)

[Web サービス API を使用したリソースの更新](aem-forms-repository.md#update-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したリソースの更新 {#update-resources-using-the-java-api}

Repository service API(Java) を使用してリソースを更新します。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   の作成 `ResourceRepositoryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 更新するリソースを取得します

   リソースを取得および読み取るリソースの URI を指定します。 この例では、リソースの URI は `"/testFolder/testResource"`.

1. リソースを更新

   を更新します。 `Resource` オブジェクトの情報。 この例では、説明を更新するには、 `Resource` オブジェクトの `setDescription` メソッドを使用して新しい説明文字列をパラメーターとして渡します。

   次に、 `ServiceClientFactory` オブジェクトの `updateResource` メソッドを使用して、次のパラメーターを渡します。

   * A `java.lang.String` リソースの URI を含むオブジェクト。
   * この `Resource` 更新されたリソース情報を含むオブジェクト。
   * A `boolean` メジャーバージョンとマイナーバージョンのどちらを更新するかを示す値。 この例では、値は `true` を渡して、メジャーバージョンの増分を示します。

**関連トピック**

[リソースの更新](aem-forms-repository.md#updating-resources)

[クイックスタート（SOAP モード）:Java API を使用したリソースの更新](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースの更新 {#update-resources-using-the-web-service-api}

Repository API（Web サービス）を使用してリソースを更新します。

1. プロジェクトファイルを含める

   * リポジトリ WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、 `RepositoryServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。 設定 `Credentials` プロパティを `System.Net.NetworkCredential` ユーザー名とパスワードを含むオブジェクト。

1. 更新するリソースを取得します

   取得するリソースの URI を指定し、リソースを読み取ります。 この例では、リソースの URI は `"/testFolder/testResource"`. 詳しくは、 [リソースの読み取り](aem-forms-repository.md#reading-resources).

1. リソースを更新

   を更新します。 `Resource` オブジェクトの情報。 この例では、説明を更新するために、 `Resource` オブジェクトの `description` フィールドに入力します。

1. を呼び出す `RepositoryServiceService` オブジェクトの `updateResource` メソッドを使用して、次のパラメーターを渡します。

   * A `System.String` リソースの URI を含むオブジェクト。
   * この `Resource` 更新されたリソース情報を含むオブジェクト。
   * A `boolean` メジャーバージョンとマイナーバージョンのどちらを更新するかを示す値。 この例では、値は `true` を渡して、メジャーバージョンの増分を示します。
   * パス `null` 残りの 2 つのパラメータに対して

**関連トピック**

[リソースの更新](aem-forms-repository.md#updating-resources)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの検索 {#searching-for-resources}

リポジトリ内のリソース（履歴、関連リソース、プロパティなど）を検索するために使用するクエリを作成できます。

関連リソースを取得して、フォームとそのフラグメント間の依存関係を判断できます。 例えば、フォームがある場合、使用するフラグメントや外部リソースを決定できます。 画像がある場合は、その画像がどのフォームで使用されているかも確認できます。 また、プロパティに基づくフィルタリングを使用して、関連リソースを検索することもできます。 例えば、指定した名前の画像を使用するすべてのフォームを検索したり、指定した名前の画像をフォームで使用しているすべてのフォームを検索したりできます。 また、リソースプロパティを使用して検索することもできます。 例えば、クエリを実行して、名前が指定の文字列で始まるすべてのフォームやリソースを検索し、ワイルドカード「%」と「_」を含めることができます。 プロパティに基づく検索は、関係に基づくものではないことに注意してください。このような検索は、特定のリソースに関する特定の知識を持っていることを前提としています。

**クエリ文**

A *クエリ* には、条件で論理的に結合される 1 つ以上のステートメントが含まれます。 A *文* は、左オペランド、演算子、右オペランドで構成されます。 また、検索結果に使用する並べ替え順を指定できます。 この *並べ替え順* には、SQL と同等の情報が含まれます `ORDER BY` 句およびは、検索の基となった属性と、昇順または降順を使用するかどうかを示す値を含む要素で構成されます。

Repository service Java API を使用して、プログラムによるリソース検索が可能です。 現時点では、Web サービス API を使用してリソースを検索することはできません。

**並べ替え動作**

を呼び出す際に、並べ替え順序は考慮されません `ResourceRepositoryClient` オブジェクトの `searchProperties` メソッドを使用し、並べ替え順を指定します。 たとえば、属性名が `name`, `secondName`、および `asecondName`. 次に、属性名に並べ替え順の要素を作成し、 `ascending` 値 `true`.

次に、 `ResourceRepositoryClient` オブジェクトの `searchProperties` メソッドを使用して、並べ替え順を渡します。 検索を実行すると、適切なリソースと 3 つのプロパティが返されます。 ただし、プロパティは属性名で並べ替えられません。 追加された順序で返されます。 `name`, `secondName`、および `asecondName`.

>[!NOTE]
>
>Repository サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

リソースを検索するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repository サービスクライアントを作成します。
1. 検索のターゲットフォルダーを指定します。
1. 検索で使用する属性を指定します。
1. 検索で使用するクエリを作成します。
1. 検索結果の並べ替え順を作成します。
1. リソースを検索します。
1. 検索結果からリソースを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実行されます。

**検索のターゲットフォルダーを指定**

検索の実行元となるベースパスを含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*パス*/*フォルダー*&quot;.

**検索に使用する属性を指定**

リソース内に含まれる属性に基づいて検索を実行できます。 検索を実行する属性の値を指定します。

**検索で使用するクエリを作成**

文と条件を使用してクエリを作成します。 各文は、検索のベースとなる属性、使用する条件、検索で使用する属性値を指定します。

**検索結果の並べ替え順を作成**

並べ替え順は、要素で構成され、各要素には、検索で使用される属性の 1 つと、昇順または降順を使用するかどうかを示す値が含まれます。

**リソースの検索**

フォルダー、クエリ、並べ替え順を使用してリソースを検索します。 また、検索の深さと、返される結果の数の上限を指定します。

**検索結果からリソースを取得**

返されたリソースのリストを繰り返し処理し、さらに処理するために情報を抽出します。

**関連トピック**

[Java API を使用したリソースの検索](aem-forms-repository.md#search-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したリソースの検索 {#search-for-resources-using-the-java-api}

Repository service API(Java) を使用してリソースを検索します。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   の作成 `ResourceRepositoryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 検索のターゲットフォルダーを指定

   検索を実行するベースパスの URI を指定します。 この例では、リソースの URI は `/testFolder`.

1. 検索に使用する属性を指定

   検索を実行する属性の値を指定します。 属性は、 `com.adobe.repository.infomodel.bean.Resource` オブジェクト。 この例では、検索は name 属性に対して実行されます。したがって `java.lang.String` を含む `Resource` オブジェクトの名前が使用されます。 `testResource` この場合、

1. 検索で使用するクエリを作成

   クエリを作成するには、 `com.adobe.repository.query.Query` オブジェクトを作成するには、 `Query` クラスを使用し、ステートメントをクエリに追加します。

   文を作成するには、 `com.adobe.repository.query.Query.Statement` クラスを渡し、次のパラメーターを渡します。

   * リソース属性定数を含む左オペランド。 この例では、リソースの名前が検索の基礎として使用されるので、静的な値 `Resource.ATTRIBUTE_NAME` が使用されます。
   * 属性の検索で使用される条件を含む演算子。 演算子は、 `Query.Statement` クラス。 この例では、静的な値 `Query.Statement.OPERATOR_BEGINS_WITH` が使用されます。
   * 検索を実行する属性値が含まれる右オペランド。 この例では、name 属性 `String` 値を含む `"testResource"`、が使用されます。

   を呼び出して、左のオペランドの名前空間を指定します。 `Query.Statement` オブジェクトの `setNamespace` メソッドを使用し、 `com.adobe.repository.infomodel.bean.ResourceProperty` クラス。 この例では、 `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` が使用されます。

   を呼び出して、各文をクエリに追加します。 `Query` オブジェクトの `addStatement` メソッドを使用して `Query.Statement` オブジェクト。

1. 検索結果の並べ替え順を作成

   検索結果で使用する並べ替え順を指定するには、 `com.adobe.repository.query.sort.SortOrder` オブジェクトを作成するには、 `SortOrder` クラスを作成し、要素を並べ替え順に追加します。

   並べ替え順の要素を作成するには、 `com.adobe.repository.query.sort.SortOrder.Element` クラス。 この例では、リソースの名前が検索の基礎として使用されるので、静的な値 `Resource.ATTRIBUTE_NAME` は最初のパラメーターとして使用され、昇順 ( `boolean` 値 `true`) が 2 番目のパラメーターとして指定されます。

   を呼び出して、各要素を並べ替え順に追加します。 `SortOrder` オブジェクトの `addSortElement` メソッドを使用して `SortOrder.Element` オブジェクト。

1. リソースの検索

   を検索するには `resources` 属性プロパティに基づいて、を呼び出します。 `ResourceRepositoryClient` オブジェクトの `searchProperties` メソッドを使用して、次のパラメーターを渡します。

   * A `String` 検索を実行するベースパスを含む。 この場合、 `"/testFolder"` が使用されます。
   * 検索で使用されるクエリ。
   * 検索の深さ。 この場合、 `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` は、ベースパスとそのすべてのフォルダーを使用することを示すために使用されます。
   * An `int` 値は、非ページ化結果セットを選択する最初の行を示します。 この例では、 `0` が指定されている。
   * An `int` 返される結果の最大数を示す値。 この例では、 `10` が指定されている。
   * 検索で使用される並べ替え順です。

   このメソッドは、 `java.util.List` / `Resource` 指定した並べ替え順のオブジェクト。

1. 検索結果からリソースを取得

   検索結果に含まれるリソースを取得するには、 `List` そして各オブジェクトを `Resource` 情報を抽出するために。 この例では、各リソースの名前が表示されます。

**関連トピック**

[リソースの検索](aem-forms-repository.md#searching-for-resources)

[クイックスタート（SOAP モード）:Java API を使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## リソースの関係の作成 {#creating-resource-relationships}

リポジトリ内のリソース間の関係を指定できます。 関係には次の 3 種類があります。

* **依存性**:リソースが他のリソースに依存する関係。つまり、リポジトリ内で関連するすべてのリソースが必要になります。
* **メンバーシップ（ファイルシステム）**:特定のフォルダー内にリソースが配置される関係。
* **カスタム**:リソース間で指定する関係。 例えば、あるリソースが非推奨になり、別のリソースがリポジトリに導入された場合、独自の置換関係を指定できます。

独自のカスタムの関係を作成できます。 例えば、HTMLファイルをリポジトリに格納し、画像を使用する場合、カスタムの関係を指定してHTMLファイルと画像を関連付けることができます（通常、リポジトリ定義の依存関係を使用して画像に関連付けられるのは XML ファイルのみです）。 別のカスタム関係の例として、ツリー構造ではなく循環グラフ構造を使用して、リポジトリの別のビューを構築する場合があります。 ビューアと共に円グラフを定義して、これらの関係を横断することができます。 最後に、2 つのリソースが完全に異なる場合でも、1 つのリソースが別のリソースを置き換えることを示すことができます。 この場合、予約範囲外の関係タイプを定義して、これら 2 つのリソース間の関係を作成できます。 アプリケーションは、関係を検出して処理できる唯一のクライアントであり、その関係に関する検索を実行するために使用できます。

Repository service Java API または Web サービス API を使用して、プログラムによってリソース間の関係を指定できます。

>[!NOTE]
>
>Repository サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-6}

2 つのリソース間の関係を指定するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repository サービスクライアントを作成します。
1. 関連付けるリソースの URI を指定します。
1. 関係を作成します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実行されます。

**関連付けるリソースの URI を指定**

関連付けるリソースの URI を含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*パス*/*リソース*&quot;.

**関係の作成**

Repository サービスメソッドを呼び出して、関係のタイプを作成および指定します。

**関連トピック**

[Java API を使用した関係リソースの作成](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[Web サービス API を使用した関係リソースの作成](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用した関係リソースの作成 {#create-relationship-resources-using-the-java-api}

Repository サービス Java API を使用して関係リソースを作成し、次のタスクを実行します。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   の作成 `ResourceRepositoryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 関連付けるリソースの URI を指定

   関連付けるリソースの URI を指定します。 この場合、リソースの名前が `testResource1` および `testResource2` とは、 `testFolder`の場合、URI は `"/testFolder/testResource1"` および `"/testFolder/testResource2"`. URI は `java.lang.String` オブジェクト。 この例では、リソースは最初にリポジトリに書き込まれ、URI が取得されます。 リソースの書き込みについて詳しくは、 [リソースの書き込み](aem-forms-repository.md#writing-resources).

1. 関係の作成

   を呼び出す `ResourceRepositoryClient` オブジェクトの `createRelationship` メソッドを使用して、次のパラメーターを渡します。

   * ソースリソースの URI。
   * ターゲットリソースの URI。
   * 関係のタイプ。これは、 `com.adobe.repository.infomodel.bean.Relation` クラス。 この例では、依存関係は、 `Relation.TYPE_DEPENDANT_OF`.
   * A `boolean` ターゲットリソースが `com.adobe.repository.infomodel.Id`新しい head リソースの —based 識別子。 この例では、依存関係により、値 `true` が指定されている。

   また、特定のリソースに関連するリソースのリストを取得するには、 `ResourceRepositoryClient` オブジェクトの `getRelated` メソッドを使用して、次のパラメーターを渡す。

   * 関連リソースを取得するリソースの URI。 この例では、ソースリソース ( `"/testFolder/testResource1"`) が指定されている場合にのみ有効です。
   * A `boolean` 指定したリソースが関係のソースリソースであるかどうかを示す値。 この例では、値 `true` が指定されているのは、この場合です。
   * 関係タイプ。これは、 `Relation` クラス。 この例では、以前と同じ値を使用して依存関係を指定します。 `Relation.TYPE_DEPENDANT_OF`.

   この `getRelated` メソッドは、 `java.util.List` / `Resource` オブジェクトを繰り返し使用して各関連リソースを取得し、 `List` から `Resource` 君がそうする時 この例では、 `testResource2` は、返されたリソースのリストに含まれると想定されます。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[クイックスタート（SOAP モード）:Java API を使用したリソース間の関係の作成](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した関係リソースの作成 {#create-relationship-resources-using-the-web-service-api}

Repository API（Web サービス）を使用して関係リソースを作成します。

1. プロジェクトファイルを含める

   * リポジトリ WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、 `RepositoryServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。 設定 `Credentials` プロパティを `System.Net.NetworkCredential` ユーザー名とパスワードを含むオブジェクト。

1. 関連付けるリソースの URI を指定

   関連付けるリソースの URI を指定します。 この場合、リソースの名前が `testResource1` および `testResource2` とは、 `testFolder`の場合、URI は `"/testFolder/testResource1"` および `"/testFolder/testResource2"`. Microsoft .NET Framework に準拠している言語（C#など）を使用する場合、URI は `System.String` オブジェクト。 この例では、リソースは最初にリポジトリに書き込まれ、URI が取得されます。 リソースの書き込みについて詳しくは、 [リソースの書き込み](aem-forms-repository.md#writing-resources).

1. 関係の作成

   を呼び出す `RepositoryServiceService` オブジェクトの `createRelationship` メソッドを使用して、次のパラメーターを渡します。

   * ソースリソースの URI。
   * ターゲットリソースの URI。
   * 関係のタイプ。 この例では、依存関係は、 `3`.
   * A `boolean` 関係タイプが指定されたかどうかを示す値。 この例では、値 `true` が指定されている。
   * A `boolean` ターゲットリソースが `Id`新しい head リソースの —based 識別子。 この例では、依存関係により、値 `true` が指定されている。
   * A `boolean` ターゲットヘッドが指定されたかどうかを示す値。 この例では、値 `true` が指定されている。
   * パス `null` を最後のパラメーターに設定します。

   また、特定のリソースに関連するリソースのリストを取得するには、 `RepositoryServiceService` オブジェクトの `getRelated` メソッドを使用して、次のパラメーターを渡す。

   * 関連リソースを取得するリソースの URI。 この例では、ソースリソース ( `"/testFolder/testResource1"`) が指定されている場合にのみ有効です。
   * A `boolean` 指定したリソースが関係のソースリソースであるかどうかを示す値。 この例では、値 `true` が指定されているのは、この場合です。
   * A `boolean` ソースリソースが指定されたかどうかを示す値。 この例では、値 `true` が指定されている。
   * 関係の型を含む整数の配列。 この例では、以前に使用したのと同じ値を配列で使用することで、依存関係を指定します。 `3`.
   * パス `null` 残りの 2 つのパラメータに対して

   この `getRelated` メソッドは、にキャストできるオブジェクトの配列を返します。 `Resource` オブジェクトを使用して、各関連リソースを繰り返し取得できます。 この例では、 `testResource2` は、返されたリソースのリストに含まれると想定されます。

**関連トピック**

[リソースの関係の作成](aem-forms-repository.md#creating-resource-relationships)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースのロック {#locking-resources}

特定のユーザーが排他的に使用するリソースまたはリソースのセットをロックしたり、複数のユーザー間で共有を使用したりできます。 共有ロックは、リソースで何かが起こることを示しますが、他のユーザーがそのリソースに対して何らかの操作を実行するのを防ぐことはありません。 共有ロックは、シグナリングメカニズムと見なす必要があります。 排他ロックとは、リソースをロックしたユーザーがリソースを変更することを意味し、ロックにより、ユーザーがリソースにアクセスする必要がなくなり、ロックが解除されるまでは、他のユーザーは変更できないようにします。 リポジトリ管理者がリソースのロックを解除すると、そのリソースに対するすべての排他的なロックと共有ロックが自動的に削除されます。 このタイプのアクションは、ユーザーが使用できなくなり、リソースのロックが解除されていない場合に使用します。

リソースがロックされていると、次の図に示すように、Workbench の「Resources」タブを表示すると、ロックアイコンが表示されます。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

Repository service Java API または Web サービス API を使用して、リソースへのアクセスをプログラムで制御できます。

>[!NOTE]
>
>Repository サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-7}

リソースをロックおよびロック解除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repository サービスクライアントを作成します。
1. ロックするリソースの URI を指定します。
1. リソースをロックします。
1. リソースのロックを取得します。
1. リソースのロックを解除

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実行されます。

**ロックするリソースの URI を指定**

ロックするリソースの URI を含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*パス*/*リソース*&quot;.

**リソースをロック**

Repository サービスメソッドを呼び出して、リソースをロックし、URI、ロックのタイプ、ロックの深さを指定します。

**リソースのロックの取得**

Repository サービスメソッドを呼び出して、URI を指定して、リソースのロックを取得します。

**リソースのロックを解除**

URI を指定してリソースのロックを解除するには、Repository サービスメソッドを呼び出します。

**関連トピック**

[Java API を使用したリソースのロック](aem-forms-repository.md#lock-resources-using-the-java-api)

[Web サービス API を使用したリソースのロック](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API を使用したリソースのロック {#lock-resources-using-the-java-api}

Repository サービス API(Java) を使用してリソースをロックします。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   の作成 `ResourceRepositoryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. ロックするリソースの URI を指定

   ロックするリソースの URI を指定します。 この場合、 `testResource` は、次の名前のフォルダーにあります： `testFolder`の場合、その URI は `"/testFolder/testResource"`. URI は `java.lang.String` オブジェクト。

1. リソースをロック

   を呼び出す `ResourceRepositoryClient` オブジェクトの `lockResource` メソッドを使用して、次のパラメーターを渡します。

   * リソースの URI。
   * ロック範囲。 この例では、リソースは排他的に使用するためにロックされるので、ロック範囲は `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * ロックの深さ。 この例では、ロックは特定のリソースにのみ適用され、メンバーや子には適用されないので、ロックの深さは `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >オーバーロードされた `lockResource` 4 つのパラメーターを必要とするメソッドでは、例外がスローされます。 必ず `lockResource` メソッドで、この説明に示す 3 つのパラメーターが必要です。

1. リソースのロックの取得

   を呼び出す `ResourceRepositoryClient` オブジェクトの `getLocks` メソッドを使用し、リソースの URI をパラメーターとして渡します。 メソッドは、反復可能な Lock オブジェクトの List を返します。 この例では、各 Lock オブジェクトの `getOwnerUserId`, `getDepth`、および `getType` メソッドに含まれます。

1. リソースのロックを解除

   を呼び出す `ResourceRepositoryClient` オブジェクトの `unlockResource` メソッドを使用し、リソースの URI をパラメーターとして渡します。 詳しくは、 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[クイックスタート（SOAP モード）:Java API を使用したリソースのロック](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースのロック {#lock-resources-using-the-web-service-api}

Repository サービス API（Web サービス）を使用してリソースをロックします。

1. プロジェクトファイルを含める

   * Base64 を使用して、Repository WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、 `RepositoryServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。 設定 `Credentials` プロパティを `System.Net.NetworkCredential` ユーザー名とパスワードを含むオブジェクト。

1. ロックするリソースの URI を指定

   ロックするリソースの URI を含む文字列を指定します。 この場合、 `testResource` がフォルダー内にある `testFolder`の場合、その URI は `"/testFolder/testResource"`. Microsoft .NET Framework に準拠している言語（例：C#）を使用する場合、URI を `System.String` オブジェクト。

1. リソースをロック

   を呼び出す `RepositoryServiceService` オブジェクトの `lockResource` メソッドを使用して、次のパラメーターを渡します。

   * リソースの URI。
   * ロック範囲。 この例では、リソースは排他的に使用するためにロックされるので、ロック範囲は `11`.
   * ロックの深さ。 この例では、ロックは特定のリソースにのみ適用され、メンバーや子には適用されないので、ロックの深さは `2`.
   * An `int` ロックの有効期限が切れるまでの秒数を示す値。 この例では、 `1000` が使用されます。
   * パス `null` を最後のパラメーターに設定します。

1. リソースのロックの取得

   を呼び出す `RepositoryServiceService` オブジェクトの `getLocks` メソッドを使用し、リソースの URI を最初のパラメーターとして渡し、 `null` を返します。 メソッドは、 `object` 含む配列 `Lock` 繰り返し可能なオブジェクト。 この例では、各オブジェクトに対して、ロックの所有者、深さ、範囲が各オブジェクトに対して `Lock` オブジェクトの `ownerUserId`, `depth`、および `type` フィールドに設定されます。

1. リソースのロックを解除

   を呼び出す `RepositoryServiceService` オブジェクトの `unlockResource` メソッドを使用し、リソースの URI を最初のパラメーターとして渡し、 `null` を返します。

**関連トピック**

[リソースのロック](aem-forms-repository.md#locking-resources)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## リソースの削除 {#deleting-resources}

Repository サービス Java API(SOAP) を使用して、リポジトリ内の特定の場所からリソースをプログラムで削除できます。

リソースを削除する場合、削除は通常は永続的ですが、ECM リポジトリの履歴メカニズムに従ってリソースのバージョンを保存する場合もあります。 したがって、リソースを削除する場合は、そのリソースが再び必要にならないようにすることが重要です。 リソースを削除する一般的な理由には、データベースの使用可能な領域を増やす必要がある場合があります。 リソースのバージョンは削除できますが、削除する場合は、論理識別子 (LID) やパスではなく、リソース識別子を指定する必要があります。 フォルダーを削除すると、サブフォルダーやリソースを含め、そのフォルダー内のすべてが自動的に削除されます。

関連リソースは削除されません。 例えば、logo.gif ファイルを使用するフォームがあり、logo.gif を削除した場合、関係は保留中の関係テーブルに保存されます。 別の方法として、バージョンの廃止については、最新バージョンのオブジェクトステータスを「非推奨」に設定します。

削除操作は、ECM システムではトランザクションセーフではありません。 例えば、100 個のリソースを削除しようとした場合、50 番目のリソースで操作が失敗した場合、最初の 49 個のインスタンスは削除されますが、残りは削除されません。 それ以外の場合、デフォルトの動作はロールバック（非コミットメント）です。

>[!NOTE]
>
>を使用する場合、 `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` メソッドと ECM リポジトリ (EMC Documentum Content Server およびIBM FileNet P8 Content Manager) を使用した場合、指定したリソースの削除に失敗した場合、トランザクションはロールバックされません。つまり、削除したファイルは削除を取り消すことができません。

>[!NOTE]
>
>Repository サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-8}

リソースを削除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Repository サービスクライアントを作成します。
1. 削除するリソースの URI を指定します。
1. リソースを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを含めます。

**サービスクライアントの作成**

プログラムによってリソースを読み取る前に、接続を確立し、資格情報を指定する必要があります。 これは、サービスクライアントを作成することで実行されます。

**削除するリソースの URI を指定**

削除するリソースの URI を含む文字列を作成します。 構文には、次のようにスラッシュが含まれます。&quot;/*パス*/*リソース*&quot;. 削除するリソースがフォルダーの場合、削除は繰り返し実行されます。

**リソースを削除**

URI を指定してリソースを削除するには、Repository サービスメソッドを呼び出します。

**関連トピック**

[Java API を使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[Web サービス API を使用したリソースの削除](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Repository Service API クイックスタート](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API(SOAP) を使用したリソースの削除 {#delete-resources-using-the-java-api-soap}

Repository API(Java) を使用してリソースを削除します。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. サービスクライアントの作成

   の作成 `ResourceRepositoryClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 削除するリソースの URI を指定

   取得するリソースの URI を指定します。 この場合、testResourceToBeDeleted という名前のリソースは testFolder という名前のフォルダーにあるので、URI は次のようになります。 `/testFolder/testResourceToBeDeleted`. URI は `java.lang.String` オブジェクト。 この例では、リソースが最初にリポジトリに書き込まれ、その URI が取得されます。 リソースの書き込みについて詳しくは、 [リソースの書き込み](aem-forms-repository.md#writing-resources).

1. リソースを削除

   を呼び出す `ResourceRepositoryClient` オブジェクトの `deleteResource` メソッドを使用し、リソースの URI をパラメーターとして渡します。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[クイックスタート（SOAP モード）:Java API を使用したリソースの検索](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したリソースの削除 {#delete-resources-using-the-web-service-api}

Repository API（Web サービス）を使用してリソースを削除します。

1. プロジェクトファイルを含める

   * Base64 を使用して、Repository WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. サービスクライアントの作成

   Microsoft .NET クライアントアセンブリを使用して、 `RepositoryServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。 設定 `Credentials` プロパティを `System.Net.NetworkCredential` ユーザー名とパスワードを含むオブジェクト。

1. 削除するリソースの URI を指定

   取得するリソースの URI を指定します。 この場合、 `testResourceToBeDeleted` は、次の名前のフォルダーにあります： `testFolder`の場合、その URI は `"/testFolder/testResourceToBeDeleted"`. この例では、リソースが最初にリポジトリに書き込まれ、その URI が取得されます。 リソースの書き込みについて詳しくは、 [リソースの書き込み](aem-forms-repository.md#writing-resources).

1. リソースを削除

   を呼び出す `RepositoryServiceService` オブジェクトの `deleteResources` メソッドと `System.String` リソースの URI を最初のパラメーターとして含む配列。 パス `null` を返します。

**関連トピック**

[リソースの削除](aem-forms-repository.md#deleting-resources)

[Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
