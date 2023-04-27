---
title: OSGi の設定
seo-title: Configuring OSGi
description: OSGi は、Adobe Experience Manager（AEM）の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。この記事では、このようなバンドルの設定を管理する方法について詳しく説明します。
seo-description: OSGi is a fundamental element in the technology stack of Adobe Experience Manager (AEM). It is used to control the composite bundles of AEM and their configuration. This article details how you can manage the configuration settings for such bundles.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
exl-id: 977d07d2-36cf-4799-bcfe-991cf89a612a
source-git-commit: 51358642a2fa8f59f3f5e3996b0c37269632c4cb
workflow-type: tm+mt
source-wordcount: '1970'
ht-degree: 67%

---

# OSGi の設定{#configuring-osgi}

[OSGi](https://www.osgi.org/) は、Adobe Experience Manager（AEM）の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。

OSGi は標準化されたプリミティブを提供し、小さく再利用が可能で連携機能に優れたコンポーネントを組み合わせてアプリケーションを構築することを可能にします。これらのコンポーネントからアプリケーションを作成し、デプロイすることができます&#x200B;*。*

これにより、 バンドルの管理が容易になり、バンドルを個別に停止、インストール、開始できます。相互依存関係は自動的に処理されます。各 OSGi コンポーネント ( [OSGi の仕様](https://docs.osgi.org/specification/)を参照) は、様々なバンドルの 1 つに含まれています。

これらのバンドルの設定は、次のいずれかの方法で管理できます。

* の使用 [Adobe CQ Web コンソール](#osgi-configuration-with-the-web-console)
* using [設定ファイル](#osgi-configuration-with-configuration-files)
* [リポジトリ内のコンテンツノード（`sling:OsgiConfig`）](#osgi-configuration-in-the-repository)を設定

いずれの方法も使用できますが、主に[実行モード](/help/sites-deploying/configure-runmodes.md)に関連する、次のようなわずかな違いがあります。

* [Adobe CQ Web コンソール](#osgi-configuration-with-the-web-console)

   * Web コンソールは OSGi 設定の標準インターフェイスです。様々なプロパティを編集するための UI が提供されており、事前に定義されているリストから設定可能な値を選択できます。

      そのため、最も簡単に使用できます。

   * Web コンソールで行われた設定は、現在のインスタンスにすぐに適用されます。現在の実行モードや、今後の実行モードの変更には関係ありません。

* [設定ファイル](#osgi-configuration-with-configuration-files)

   * Web コンソールで定義された設定が含まれます。
   * 他のインスタンスで使用するために、コンテンツパッケージに含めることができます。

* [リポジトリ内のコンテンツノード（sling:osgiConfig）](#osgi-configuration-in-the-repository)

   * CRXDE Lite を使用した手動による設定が必要です。
   * `sling:OsgiConfig` ノードの命名規則により、設定を特定の[実行モード](/help/sites-deploying/configure-runmodes.md)に関連付けることができます。同じリポジトリに複数の実行モードの設定を保存することもできます。
   * 適切な設定がすぐに適用されます（実行モードに依存）。

使用するメソッドに関わらず、次のことが可能です。

* リポジトリのコンテンツをコピーまたはレプリケートすると、同じ設定が再作成されることを確認します。
* 設定を FileVault または Subversion にチェックアウトできます。セキュリティまたは更新のために。
* 他のインスタンスの設定時に使用するために、パッケージに保存できます。
* スクリプトを使用して設定の詳細を提案する設定ロールアウトを実行できます。

>[!NOTE]
>
>特定の重要な設定について詳しくは、[OSGi 設定の指定](/help/sites-deploying/osgi-configuration-settings.md)を参照してください。

## Web コンソールでの OSGi 設定 {#osgi-configuration-with-the-web-console}

この [Web コンソール](/help/sites-deploying/web-console.md) のAEMでは、バンドルを設定するための標準化されたインターフェイスが提供されます。 この **設定** タブは OSGi バンドルの設定に使用されるので、AEMシステムパラメーターを設定するための基礎となるメカニズムです。

おこなった変更は、関連する OSGi 設定に直ちに適用され、再起動は必要ありません。

>[!NOTE]
>
>Web コンソールで加えた変更は、[設定ファイル](#osgi-configuration-with-configuration-files)としてリポジトリ内に保存されます。これらは、その後のインストールで再利用するために、コンテンツパッケージに含めることができます。

>[!NOTE]
>
>Web コンソールでは、デフォルト設定に関する説明は Sling のデフォルトに関連します。
>
>Adobe Experience Manager には独自のデフォルト値があり、設定されるデフォルト値は、コンソールに表示される値と異なる場合があります。

Web コンソールで設定を更新するには：

1. 次にアクセス： **設定** 次のいずれかの方法で Web コンソールの「 」タブを開きます。

   * Web コンソールを **ツール/操作** メニュー コンソールにログインしたら、次のドロップダウンメニューを使用できます。

      **OSGi >**

   * ダイレクト URL 例：

      `http://localhost:4502/system/console/configMgr`
   リストが表示されます。

1. 次のいずれかの方法で、設定するバンドルを選択します。

   * 該当するバンドルの「**編集**」アイコンをクリック
   * 該当するバンドルの「**名前**」をクリック

1. ダイアログが開きます。必要に応じて編集します。例えば「**ログレベル**」を `INFO` に設定します。

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新内容は、[設定ファイル](#osgi-configuration-with-configuration-files)としてリポジトリ内に保存されます。後で必要になったときに探し出せるようにするために（コンテンツパッケージに含めて別のインスタンスで使用できるようにする場合など）、永続 ID（`PID`）をメモしておく必要があります。

1. 「**保存**」をクリックします。

   変更内容は、実行しているシステムの関連する OSGi 設定にすぐに適用されます。再起動は不要です。

   >[!NOTE]
   >
   >これで関連する[設定ファイル](#osgi-configuration-with-configuration-files)を見つけられるようになります。例えば、コンテンツパッケージに含めて別のインスタンスで使用できるようにする場合などがあります。

## 設定ファイルでの OSGi 設定 {#osgi-configuration-with-configuration-files}

Web コンソールで行った設定変更は、設定ファイル（`.config`）としてリポジトリ内の次の場所に保存されます。

`/apps`

これらの設定ファイルをコンテンツパッケージに含めて、他のインスタンスで再利用することができます。

>[!NOTE]
>
>設定ファイルは特殊な形式になっています（詳しくは [Sling Apache のドキュメント](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)を参照してください）。
>
>このため、Web コンソールで実際に変更を加えて、設定ファイルを作成し、維持することをお勧めします。

Web コンソールには、リポジトリ内で変更が保存された場所を示すものは表示されませんが、簡単に見つけることができます。

1. 次の方法で設定ファイルを作成します。 [web コンソールでの初期変更](#osgi-configuration-with-the-web-console).
1. CRXDE Lite を開きます。
1. 内 **ツール** メニュー選択 **クエリ…** .
1. **タイプ**&#x200B;が `SQL` のクエリーを送信して、更新した設定の PID を検索します。

   例えば、**Apache Felix OSGi マネージメントコンソール**&#x200B;の永続 ID（PID）は次のとおりです。

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   したがって、SQL クエリは次のようになります。

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 設定ファイルノードが表示されます。

   上記の例の場合：

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >このファイルを開いて変更内容を表示できますが、入力エラーを避けるには、コンソールで実際に変更を加えることをお勧めします。

1. これで、このノードを含むコンテンツパッケージを構築し、必要に応じて他のインスタンスで使用できます。

## リポジトリ内の OSGi 設定 {#osgi-configuration-in-the-repository}

Web コンソールを使用する以外に、リポジトリで設定の詳細を定義することもできます。 これにより、異なる実行モードを簡単に設定できます。

これらの設定は、システムが参照するリポジトリ内の `sling:OsgiConfig` ノードを作成することによって行います。これらのノードは OSGi 設定を反映し、OSGi 設定に対するユーザーインターフェイスを形成します。設定データを更新するには、ノードのプロパティを更新します。

リポジトリ内の設定データを変更すると、Web コンソールで変更した場合と同様に、適切な検証と整合性チェックが行われ、関連する OSGi 設定に変更が直ちに適用されます。これは、設定を `/libs/` から `/apps/` へコピーするアクションの場合も当てはまります。

同じ設定パラメーターを複数の場所に配置できるので、システムでは次の処理が行われます。

* タイプが `sling:OsgiConfig` のすべてのノードを検索
* サービス名に従ってフィルター処理
* 実行モードに従ってフィルター処理

>[!NOTE]
>
>参照 [特定のインスタンスに対してのみリポジトリベースの設定を定義する方法](https://helpx.adobe.com/jp/experience-manager/kb/RunModeDependentConfigAndInstall.html).

### リポジトリへの新しい設定の追加 {#adding-a-new-configuration-to-the-repository}

#### 知っておくべきこと {#what-you-need-to-know}

新しい設定をリポジトリに追加するには、次の情報が必要です。

1. サービスの **永続 ID**（PID）。

   Web コンソールの「**設定** 」フィールドを参照します。この名前は、バンドル名の後に括弧でくくって（またはページの下部に向かって&#x200B;**設定情報**&#x200B;に）表示されます。

   例えば、`com.day.cq.wcm.core.impl.VersionManagerImpl.` ノードを作成して、**AEM WCM バージョンマネージャー**&#x200B;を設定します。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 特定の[実行モード](/help/sites-deploying/configure-runmodes.md)が必要かどうか。次のようにフォルダーを作成します。

   * `config` - すべての実行モード用
   * `config.author` - オーサー環境用
   * `config.publish` - パブリッシュ環境用
   * `config.<run-mode>` - 適宜

1. **設定**&#x200B;または&#x200B;**ファクトリ設定**&#x200B;が必要かどうか。
1. 設定する個々のパラメーター。再作成が必要な既存のパラメーター定義を含めます。

   Web コンソールの個々のパラメーターフィールドを参照します。名前は、各パラメーターに対して角括弧で囲まれて表示されます。

   例えば、プロパティを作成します。
   `versionmanager.createVersionOnActivation` で **アクティベーション時にバージョンを作成**&#x200B;を設定します。

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. `/libs` に既に設定が存在しますか？インスタンス内のすべての設定をリストするには、CRXDELite の&#x200B;**クエリ**&#x200B;ツールを使用して、次の SQL クエリを送信します。

   `select * from sling:OsgiConfig`

   その場合は、この設定を ` /apps/<yourProject>/` にコピーすると、新しい場所にカスタマイズされます。

#### リポジトリでの設定の作成 {#creating-the-configuration-in-the-repository}

新しい設定をリポジトリに実際に追加するには、次の手順を実行します。

1. CRXDE Liteを使用して次の場所に移動します。

   ` /apps/<yourProject>`

1. 存在しない場合は、`config` フォルダーを作成します（`sling:Folder`）。

   * `config` - すべての実行モードに該当
   * `config.<run-mode>` - 特定の実行モードに固有

1. このフォルダーの下に、次の設定でノードを作成します。

   * タイプ：`sling:OsgiConfig`
   * 名前：永続 ID（PID）

      例えば、AEM WCM Version Manager の場合は `com.day.cq.wcm.core.impl.VersionManagerImpl` を使用します
   >[!NOTE]
   >
   >ファクトリ設定を作成する場合は、`-<identifier>` を名前に付加します。
   >
   >例： `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >`<identifier>` の部分は、インスタンスを識別するフリーテキストに置き換えます（この情報は省略できません）。次に例を示します。
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 設定するパラメーターごとに、このノードでプロパティを作成します。

   * 名前：Web コンソールに表示される名前。名前は、フィールドの説明の最後に角括弧で囲んで表示されます。例： `Create Version on Activation` では `versionmanager.createVersionOnActivation` を使用
   * タイプ：適宜。
   * 値：必要に応じて。

   設定するパラメーターのプロパティを作成するだけで済みます。その他のパラメーターは、AEMで設定されたデフォルト値を引き続き使用します。

1. すべての変更を保存します。

   変更は、（Web コンソールでおこなった変更と同様に）サービスを再起動することで、ノードが更新されるとすぐに適用されます。

>[!CAUTION]
>
>`/libs` パス内は一切変更しないでください。

>[!CAUTION]
>
>起動時に設定を読み込むには、設定のフルパスが正しい必要があります。

## 設定の詳細 {#configuration-details}

### 起動時の解決順序 {#resolution-order-at-startup}

次の優先順位が使用されます。

1. `/apps/*/config...` の下のリポジトリノード。タイプ `sling:OsgiConfig` またはプロパティファイル。

1. `/libs/*/config...` の下にある、タイプ `sling:OsgiConfig` のリポジトリノード。（標準定義）

1. `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...` からの任意の `.config` ファイル。ローカルファイルシステム上。

これは、`/libs` 内の汎用設定は、`/apps` 内のプロジェクト固有の設定によってマスクできるということを意味します。

### 実行時の解決順序 {#resolution-order-at-runtime}

システムの実行中に行われた構成の変更は、変更した構成でトリガーを再読み込みします。

次の優先順位が適用されます。

1. Web コンソールでの設定の変更は、実行時に優先されるので、即座に有効になります。
1. `/apps` での設定変更がすぐに有効になります。
1. `/apps` で設定によってマスクされない限り、`/libs` での設定変更がすぐに有効になります。

### 複数の実行モードの解決 {#resolution-of-multiple-run-modes}

実行モード固有の設定の場合、複数の実行モードを組み合わせることができます。 例えば、次のスタイルで設定フォルダーを作成できます。

`/apps/*/config.<runmode1>.<runmode2>/`

このようなフォルダー内の設定は、起動時に定義されている実行モードにすべての実行モードが一致した場合に適用されます。

例えば、インスタンスが実行モード `author,dev,emea` で起動された場合は、`/apps/*/config.emea`、`/apps/*/config.author.dev/`、`/apps/*/config.author.emea.dev/` の設定ノードが適用され、`/apps/*/config.author.asean/` および `/config/author.dev.emea.noldap/` の設定ノードは適用されません。

同じ PID に複数の設定が該当する場合は、一致する実行モードの数が最も大きい設定が適用されます。

例えば、インスタンスが実行モードで開始した場合、 `author,dev,emea`と `/apps/*/config.author/` および `/apps/*/config.emea.author/` 設定を定義する\
`com.day.cq.wcm.core.impl.VersionManagerImpl`、 `/apps/*/config.emea.author/` が適用されます。

このルールの精度は PID レベルです。
\
つまり、`/apps/*/config.author/` で同じ PID の一部のプロパティと、`/apps/*/config.emea.author/` で同じ PID のより具体的なプロパティを定義することはできません。
\
一致する実行モードの数が最も多い設定は、PID 全体に対して効果的です。

### 標準設定 {#standard-configurations}

次のリストは、リポジトリで（標準インストールで）使用可能な設定の一部を示しています。

* 作成者 - AEM WCM フィルター：

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 公開 - AEM WCM フィルター：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 公開 - AEM WCM ページ統計：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>これらの設定は `/libs` 内にあるので、直接編集はせず、アプリケーション領域（`/apps`）にコピーしてからカスタマイズしてください。

インスタンスに含まれるすべての設定ノードをリストするには、CRXDE Lite の&#x200B;**クエリ**&#x200B;機能を使用して、次の SQL クエリを送信します。

`select * from sling:OsgiConfig`

### 設定の永続性 {#configuration-persistence}

* Web コンソールを使用して設定を変更した場合、（通常は）リポジトリの次の場所に書き込まれます。

   `/apps/{somewhere}`

   * デフォルトでは、`{somewhere}` は `system/config` なので、設定は次の場所に書き込まれます。

      `/apps/system/config`

   * ただし、最初にリポジトリ内の別の場所から取得した設定を編集する場合は、次のようにします。例：

      /libs/foo/config/someconfig

      その後、更新された設定が元の場所に書き込まれます。例：

      `/apps/foo/config/someconfig`

* `admin` によって変更された設定は、次の場所の下の `*.config` ファイルに保存されます。

   ```
      /crx-quickstart/launchpad/config
   ```

   * これは OSGi 設定管理者の非公開データ領域であり、システムへの入力方法にかかわらず、`admin` によって指定された設定の詳細がすべて保持されます。
   * これは実装の詳細です。このディレクトリを直接編集しないでください。
   * ただし、バックアップや複数のインストール用にコピーを取得できるように、これらの設定ファイルの場所を把握すると便利です。

      * Apache Felix OSGi Management Console

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling クライアントレポジトリ

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>次の場所にあるフォルダーやファイルは、***決して***&#x200B;編集しないでください。
>
>`/crx-quickstart/launchpad/config`
