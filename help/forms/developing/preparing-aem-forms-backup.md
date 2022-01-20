---
title: バックアップ用のAEM Formsの準備
seo-title: Preparing AEM Forms for Backup
description: Java API と Web Service API を使用して、Backup and Restore サービスを使用し、AEM Formsサーバーのバックアップモードを開始し、終了する方法について説明します。
seo-description: Learn how to use the Backup and Restore service to enter and leave the Backup mode for AEM Forms server using the Java API and the Web Service API.
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
role: Developer
exl-id: fa2bff05-a3b8-4230-95d6-1fbdc96bac3b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2506'
ht-degree: 2%

---

# バックアップ用のAEM Formsの準備 {#preparing-aem-forms-for-backup}

## バックアップと復元サービスについて {#about-the-backup-and-restore-service}

バックアップと復元サービスを使用すると、AEM Formsを *バックアップモード*：ホット・バックアップを実行できます。 バックアップと復元サービスは、実際にはAEM Formsのバックアップを実行したり、システムを復元したりしません。 その代わりに、サーバを一貫性と信頼性の高いバックアップのための状態にし、サーバの実行を継続できます。 グローバルドキュメントストレージ (GDS) と forms サーバーに接続されたデータベースをバックアップするアクションは、ユーザーが担当します。 GDS は、長期間有効なプロセス内で使用されるファイルの保存に使用されるディレクトリです。

バックアップモードは、バックアップ手順の実行中に GDS 内のファイルがパージされないように、サーバがに入る状態です。 代わりに、GDS ディレクトリの下にサブディレクトリが作成され、保存バックアップモードの終了後にパージされるファイルの記録が維持されます。 ファイルは、システムの再起動後も存続し、数日間、または数年間にわたる可能性があります。 これらのファイルは、forms サーバーの全体的な状態の重要な部分であり、PDFファイル、ポリシー、フォームテンプレートなどが含まれる場合があります。 これらのファイルが失われたり破損したりした場合は、forms サーバー上のプロセスが不安定になり、データが失われる可能性があります。

スナップショットバックアップを実行する場合は、通常、一定期間バックアップモードに入り、バックアップアクティビティの完了後にバックアップモードを終了します。 バックアップモードを終了すると、ファイルが不必要に大きくならないように GDS からパージできるようになります。 バックアップモードを明示的に終了するか、バックアップモードセッションで期限が切れるまで待つことができます。

また、サーバを永続的なバックアップ・モードのままにすることもできます。これは、ローリング・バックアップや継続的なシステム・カバレッジのバックアップ戦略に典型的な機能です。 ローリングバックアップモードは、システムが常にバックアップモードになり、前回のセッションが解放されるとすぐに新しいバックアップモードセッションが開始されることを示します。 連続バックアップモードの場合、ファイルは 2 つのバックアップモードセッションの後にパージされ、参照されなくなります。

Backup and Restore サービスを使用して、Forms サーバーに接続された GDS またはデータベースのバックアップを実行するために作成する既存のアプリケーションまたは新しいアプリケーションに追加できます。

>[!NOTE]
>
>AEM Formsの実装の他の側面と同様に、バックアップと回復戦略は、実稼動環境で使用する前に、開発環境またはステージング環境で開発およびテストして、データを失うことなく、ソリューション全体が期待どおりに動作することを確認する必要があります。

バックアップと復元サービスを使用して、次のタスクを実行できます。

* バックアップモードに入ります。
* バックアップモードを終了します。

>[!NOTE]
>
>AEM Formsのバックアップを実行する際に考慮すべき事項の詳細については、 [管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>バックアップと復元サービスの詳細については、「 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## forms サーバーでのバックアップモードの開始 {#entering-backup-mode-on-the-forms-server}

バックアップモードを開始すると、Forms サーバーのホットバックアップが可能になります。 バックアップモードを開始する場合、組織のバックアップ手順に基づいて次の情報を指定します。

* バックアッププロセスに役立つバックアップモードセッションを識別する一意のラベル。
* バックアップ手順が完了するまでの時間。
* 連続バックアップモードにするかどうかを示すフラグ。ローリングバックアップを実行する場合にのみ役立ちます。

アプリケーションをバックアップモードに切り替える前に、forms サーバーをバックアップモードにした後に使用するバックアップ手順を理解しておくことをお勧めします。 AEM Formsのバックアップを実行する際に考慮すべき事項の詳細については、 [管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>バックアップと復元サービスの詳細については、「 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

バックアップモードに入るアプリケーションを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. BackupService クライアントオブジェクトを作成します。
1. 一意のラベル、バックアップを実行する時間、継続的なバックアップ・モードにするかどうかを決定します。
1. バックアップモードに入ります。
1. （オプション）サーバー上のバックアップモードセッションに関する情報を取得します。
1. GDS（グローバルデータストア）とデータベースのバックアップを実行します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 これらのファイルは、コードを正しくコンパイルし、Backup and Restore Service API を使用するために、プロジェクトに含めることが重要です。

これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**BackupService Client API オブジェクトの作成**

プログラムによるバックアップモードを終了するには、Backup and Restore Service API を使用する BackupService クライアントオブジェクトを作成します。

**固有のラベルを決定し、バックアップを実行する時間を決定し、継続的なバックアップ・モードにするかどうかを決定**

バックアップモードに入る前に、固有のラベルを決定し、バックアップの実行に割り当てる時間を決定し、forms サーバーをバックアップモードのままにするかどうかを決定する必要があります。 これらの検討事項は、お客様の組織が確立したバックアップ手順と統合する際に重要です。 ( [管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63).)

**バックアップモードを開始**

組織のバックアップ手順と一致するパラメータを使用して、バックアップモードに入ります。

**サーバー上のバックアップモードセッションに関する情報を取得します**

バックアップモードに入った後、セッションに関する情報を取得できます。 この情報は、バックアップ手順との統合に使用できます

**GDS とデータベースのバックアップを実行します**

バックアップモードに正常に入ったら、グローバルドキュメントストレージ (GDS) と forms サーバーが接続されているデータベースのバックアップを実行できます。 この手順は、手動で実行することも、他のツールを実行してバックアップ手順を実行することもできるので、組織に固有の手順です。

### Java API を使用してバックアップモードに入る {#enter-backup-mode-using-the-java-api}

バックアップと復元サービス API を使用してバックアップモードに入ります。

1. プロジェクトファイルを含める

   必要なクライアント JAR ファイル（ adobe-backup-restore-client-sdk.jar など）を Java プロジェクトのクラスパスに含めます。 Java クライアントアプリケーションを作成するには、次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
   * jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

1. BackupService Client API オブジェクトの作成

   次を使用する： `ServiceClientFactory` オブジェクトと BackupService クライアント API オブジェクトを一緒に使用します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * の作成 `BackupService` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクト。

1. 固有のラベルを決定し、バックアップを実行する時間を決定し、継続的なバックアップ・モードにするかどうかを決定

   固有のラベルを決定し、バックアップの実行に割り当てる時間を決定し、forms サーバーを継続的なバックアップモードに保つかどうかを決定します。

1. バックアップモードを開始

   次を呼び出してバックアップモードに入ります： `enterBackupMode` メソッドを次のパラメーターで指定します。

   * A `String` バックアップモードセッションを識別する一意の人間が読み取れるラベルを指定する値。 XML 形式にエンコードできないスペースや文字は使用しないことをお勧めします。
   * An `int` バックアップモードで維持する時間（分）を指定する値。 値は、 `1` から `10080` （1 週間の分数） 連続バックアップモードを使用する場合、この値は無視されます。
   * A `Boolean` 連続バックアップモードにするかどうかを指定する値。 値： `True` 連続バックアップモードにするよう指定します。 連続バックアップモードの場合、バックアップモードで保持する分数に指定した値は無視されます。

      連続バックアップモードとは、現在のバックアップモードが完了した後に新しいバックアップモードセッションが開始されることを意味します。 値： `False` は、継続的なバックアップモードが使用されず、バックアップモードを終了した後に、GDS からのファイルのパージが再開されることを意味します。

1. サーバー上のバックアップモードセッションに関する情報を取得します

   を使用して情報を取得する `BackupModeEntryResult` を呼び出した後に返されるオブジェクト `enterBackupMode` メソッド。 バックアップモードに入った後に取得できる情報は、バックアップ手順との統合に役立つ場合があります。 例えば、バックアップ手順のファイル名の入力として、ラベル、バックアップ ID、開始時刻が役立つ場合があります。

1. GDS とデータベースのバックアップを実行します

   グローバルドキュメントストレージ (GDS) と、Forms サーバーが接続されているデータベースをバックアップします。 バックアップを実行するアクションは、AEM Forms SDK には含まれておらず、組織内のバックアップ手順に固有の手動の手順が含まれている場合もあります。

### Web サービス API を使用してバックアップモードに入ります {#enter-backup-mode-using-the-web-service-api}

バックアップと復元サービス API が提供する Web サービスを使用して、バックアップモードに入ります。

1. プロジェクトファイルを含める

   * Backup and Restore Service API WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. BackupService Client API オブジェクトの作成

   Microsoft .NET クライアントアセンブリを使用して、 `BackupServiceService` オブジェクトを作成するには、デフォルトのコンストラクターを呼び出し、 `Credentials` メソッド。

1. 固有のラベルを決定し、バックアップを実行する時間を決定し、継続的なバックアップ・モードにするかどうかを決定

   固有のラベルを決定し、バックアップの実行に割り当てる時間を決定し、forms サーバーを継続的なバックアップモードに保つかどうかを決定します。

1. バックアップモードを開始

   バックアップモードに入るには、 enterBackupMode メソッドを呼び出して、次の値を渡します。

   * A `String` バックアップモードセッションを識別する一意の人間が読み取れるラベルを指定する値。 XML 形式にエンコードできないスペースや文字は使用しないことをお勧めします。
   * A `Uint32` バックアップモードで維持する時間（分）を指定する値。 値は、 `1` から `10080` （1 週間の分数）。 連続バックアップモードを使用する場合、この値は無視されます。
   * A `Boolean` 連続バックアップモードにするかどうかを指定する値。 値： `True` 連続バックアップモードにするよう指定します。 連続バックアップモードの場合、バックアップモードで保持する分数に指定した値は無視されます。 連続バックアップモードとは、現在のバックアップモードが完了した後に新しいバックアップモードセッションが開始されることを意味します。

      値： `False` は、継続的なバックアップモードが使用されず、バックアップモードを終了した後に、GDS からのファイルのパージが再開されることを意味します。

1. サーバー上のバックアップモードセッションに関する情報を取得します

   enterBackupMode メソッドを BackupModeEntryResult から呼び出し、成功したことを確認するために返された、バックアップモードセッションに関する情報を取得します。 バックアップモードに入った後に取得できる情報は、バックアップ手順との統合に役立つ場合があります。 例えば、バックアップ手順のファイル名の入力として、ラベル、バックアップ ID、開始時刻が役立つ場合があります。

1. GDS とデータベースのバックアップを実行します

   グローバルドキュメントストレージ (GDS) と、Forms サーバーが接続されているデータベースをバックアップします。 バックアップを実行するアクションは、AEM Forms SDK には含まれておらず、組織内のバックアップ手順に固有の手動の手順が含まれている場合もあります。

## forms サーバーへのバックアップモードの終了 {#leaving-backup-mode-on-the-forms-server}

forms サーバーが forms サーバー上の GDS（グローバルドキュメントストレージ）からのファイルのパージを再開できるように、バックアップモードを終了します。

アプリケーションを終了モードに切り替える前に、AEM Formsで使用されるバックアップ手順を理解しておくことをお勧めします。 AEM Formsのバックアップを実行する際に考慮すべき事項の詳細については、 [管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>バックアップと復元サービスの詳細については、「 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

バックアップモードを終了するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. BackupService クライアントオブジェクトを作成します。
1. バックアップモードを終了します。
1. （オプション）forms サーバー上で実行されていたバックアップモードセッションに関する情報を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルをすべて含めます。 これらのファイルは、コードを正しくコンパイルし、Backup and Restore Service API を使用する際に重要です。

これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**BackupService Client API オブジェクトの作成**

プログラムによるバックアップモードを終了するには、Backup and Restore Service API を使用する BackupService クライアントオブジェクトを作成します。

**バックアップモードを終了**

バックアップモードのままにして、グローバルドキュメントストレージ (GDS) からのファイルの通常のパージを再開します。 バックアップモードを終了する前に、バックアップ手順が完了したことを確認する必要があります。

**終了したバックアップモードセッションに関する情報を取得します**

バックアップモードを終了した後、セッションに関する情報を取得できます。 この情報は、バックアップ手順との統合に使用できます。

### Java API を使用してバックアップモードを終了 {#leave-backup-mode-using-the-java-api}

Backup and Restore Service API(Java) を使用してバックアップモードを終了します。

1. プロジェクトファイルを含める

   必要なクライアント JAR ファイル（ adobe-backup-restore-client-sdk.jar など）を Java プロジェクトのクラスパスに含めます。 Java クライアントアプリケーションを作成するには、次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )
   * jbossall-client.jar(AEM Formsが JBoss Application Server にデプロイされている場合に必要 )

1. BackupService Client API オブジェクトの作成

   次を使用する： `ServiceClientFactory` オブジェクトと BackupService クライアント API オブジェクトを一緒に使用します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * の作成 `BackupService` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` オブジェクトをパラメーターとして渡します。

1. バックアップモードを開始

   を呼び出してバックアップモードを終了する `leaveBackupMode` メソッド。

1. サーバー上のバックアップモードセッションに関する情報を取得します

   を使用して操作に関する情報を取得する `BackupModeResult` 返されるオブジェクト。 バックアップモードに入った後に取得できる情報は、バックアップ手順との統合に役立つ場合があります。 例えば、バックアップ手順のファイル名の入力として、ラベル、バックアップ ID、開始時刻が役立つ場合があります。

### Web サービス API を使用してバックアップモードを終了 {#leave-backup-mode-using-the-web-service-api}

Backup and Restore Service API（Web サービス）を使用してバックアップモードを終了します。

1. プロジェクトファイルを含める

   Web サービスを使用するには、必ずプロキシファイルを含める必要があります。 次の手順に従って、Backup and Restore Service API を Web サービスとして使用するようにプロジェクトを設定します。

   * Backup and Restore Service API WSDL を使用するMicrosoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. BackupService Client API オブジェクトの作成

   Microsoft .NET クライアントアセンブリを使用して、 `BackupServiceService` オブジェクトのデフォルトのコンストラクターを呼び出す。

1. バックアップモードを開始

   を呼び出してバックアップモードを終了する `leaveBackupMode` web サービス操作。

1. サーバー上のバックアップモードセッションに関する情報を取得します

   操作後にバックアップモード識別子を取得し、正常に実行されたことを確認します。 バックアップモードを終了した後に取得できる情報は、バックアップ手順との統合に役立つ場合があります。
