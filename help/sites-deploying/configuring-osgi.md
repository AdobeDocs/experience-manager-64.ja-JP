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
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 58%

---

# OSGi の設定{#configuring-osgi}

[OSGi は、Adobe Experience Manager（AEM）の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。](https://www.osgi.org/)

OSGi は標準化されたプリミティブを提供し、小さく再利用が可能で連携機能に優れたコンポーネントを組み合わせてアプリケーションを構築することを可能にします。これらのコンポーネントからアプリケーションを作成し、デプロイすることができます。**

これにより、 バンドルの管理が容易になり、バンドルを個別に停止、インストール、開始できます。相互依存関係は自動的に処理されます。各 OSGi コンポーネント ( [OSGi の仕様](https://www.osgi.org/Specifications/HomePage)) は、様々なバンドルの 1 つに含まれています。

これらのバンドルの設定は、次のいずれかの方法で管理できます。

* [Adobe CQ Web コンソール](#osgi-configuration-with-the-web-console)を使用
* [設定ファイル](#osgi-configuration-with-configuration-files)を使用
* 設定 [content-nodes ( `sling:OsgiConfig`) をリポジトリ内に追加します。](#osgi-configuration-in-the-repository)

いずれの方法も使用できますが、主に[実行モード](/help/sites-deploying/configure-runmodes.md)に関連して、次のようなわずかな違いがあります。

* [Adobe CQ Web コンソール](#osgi-configuration-with-the-web-console)

   * Web コンソールは、OSGi 設定用の標準インターフェイスです。様々なプロパティを編集する UI が用意されています。この UI では、定義済みリストから使用可能な値を選択できます。

      そのため、最も簡単に使用できます。

   * Web コンソールでおこなわれた設定は、現在のインスタンスにすぐに適用されます。現在の実行モードや、今後の実行モードの変更には関係ありません。

* [設定ファイル](#osgi-configuration-with-configuration-files)

   * Web コンソールで定義される設定を含みます。
   * 他のインスタンスで使用できるよう、コンテンツパッケージに含めることができます。

* [リポジトリ内のコンテンツノード（sling:osgiConfig）](#osgi-configuration-in-the-repository)

   * CRXDE Lite を使用した手動による設定が必要です。
   * の命名規則により、 `sling:OsgiConfig` ノードを使用すると、設定を特定の [実行モード](/help/sites-deploying/configure-runmodes.md). 同じリポジトリに複数の実行モードの設定を保存することもできます。
   * 適切な設定がすぐに適用されます（実行モードに依存）。

使用するメソッドに関わらず、次のことが可能です。

* リポジトリのコンテンツをコピーまたはレプリケートすることにより、同一の設定を再作成できます。
* セキュリティやさらなる更新のために、FileVault または Subversion に設定をチェックアウトできます。
* パッケージとして保存し、他のインスタンスを設定する際に使用できます。
* スクリプトを使用して設定の詳細を反映させることにより、設定のロールアウトを実行できます。

>[!NOTE]
>
>特定の重要な設定について詳しくは、[、OSGi 設定](/help/sites-deploying/osgi-configuration-settings.md)を参照してください。。

## Web コンソールでの OSGi 設定 {#osgi-configuration-with-the-web-console}

AEM の [Web コンソール](/help/sites-deploying/web-console.md)は、バンドルを設定するための標準化されたインターフェイスを提供します。「**設定**」タブは、OSGi バンドルの設定時に使用します。AEM システムパラメーターを設定するための基盤となるメカニズムです。

おこなった変更は、関連する OSGi 設定にすぐに適用されます。再起動の必要はありません。

>[!NOTE]
>
>Web コンソールで行った変更は、次の名前でリポジトリに保存されます。 [設定ファイル](#osgi-configuration-with-configuration-files). このファイルをコンテンツパッケージに含めておき、将来のインストールで再利用することができます。

>[!NOTE]
>
>Web コンソールでは、デフォルト設定に言及している説明はすべて、Sling のデフォルトに関連しています。
>
>Adobe Experience Manager には独自のデフォルト値があり、設定されるデフォルト値は、コンソールに表示される値と異なる場合があります。

Web コンソールで設定を更新するには：

1. 次のいずれかの方法で、Web コンソールの「**設定**」タブにアクセスします。

   * **ツール／運営**&#x200B;メニューのリンクから Web コンソールを開きます。コンソールにログインした後、次のドロップダウンメニューを使用できます。

      **OSGi >**

   * ダイレクト URL例：

      `http://localhost:4502/system/console/configMgr`
   リストが表示されます。

1. 次のいずれかの方法で、設定するバンドルを選択します。

   * 該当するバンドルの「**編集**」アイコンをクリック
   * 該当するバンドルの&#x200B;**名前**&#x200B;をクリック

1. ダイアログが開きます。ここでは、必要に応じて編集できます。例えば、 **ログレベル** から `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新内容は、[設定ファイル](#osgi-configuration-with-configuration-files)としてリポジトリ内に保存されます。後でこれらを見つけるには（例えば、別のインスタンスで使用するためにコンテンツパッケージに含める場合）、永続的な ID( `PID`) をクリックします。

1. 「**保存**」をクリックします。

   変更内容は、関連する OSGi 設定にすぐに適用され、再起動は不要です。

   >[!NOTE]
   >
   >これで、 [設定ファイル](#osgi-configuration-with-configuration-files);例えば、別のインスタンスで使用するためにコンテンツパッケージに含める場合などです。

## 設定ファイルでの OSGi 設定 {#osgi-configuration-with-configuration-files}

Web コンソールを使用して行った設定の変更は、設定ファイル ( `.config`) の下：

`/apps`

これらの設定ファイルをコンテンツパッケージに含めて、他のインスタンスで再利用することができます。

>[!NOTE]
>
>設定ファイルの形式は非常に具体的です。詳しくは、 [Sling Apache ドキュメント](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) 詳細はこちら。
>
>そのため、実際の変更は Web コンソールを使用しておこない、設定ファイルが作成、維持されるようにすることをお勧めします。

Web コンソールには、リポジトリのどの場所に変更が保存されたかは表示されませんが、次の手順で簡単に見つけることができます。

1. [Web コンソールで最初の変更をおこなう](#osgi-configuration-with-the-web-console)ことで、設定ファイルを作成します。
1. CRXDE Lite を開きます。
1. **ツール**&#x200B;メニューの「**クエリー**」を選択します。
1. **タイプ**&#x200B;が `SQL` のクエリーを送信して、更新した設定の PID を検索します。

   例えば、**Apache Felix OSGi Management Console** の永続識別子（PID）は次のとおりです。

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   よって、SQL クエリーは次のようになります。

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 設定ファイルのノードが表示されます。

   上の例では、次のようになります。

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >このファイルを開くと、変更内容を確認できます。ただし、タイプミスを防ぐために、実際の変更はコンソールでおこなうことをお勧めします。

1. このノードを含むコンテンツパッケージをビルドしておくと、必要に応じて他のインスタンスで使用できます。

## リポジトリでの OSGi 設定 {#osgi-configuration-in-the-repository}

Web コンソールを使用するほかに、リポジトリで設定の詳細を定義することもできます。これにより、様々な実行モードを簡単に設定できます。

これらの設定は、 `sling:OsgiConfig` 参照するシステムのリポジトリ内のノード。 これらのノードは OSGi 設定を反映し、OSGi 設定に対するユーザーインターフェイスを形成します。 設定データを更新するには、ノードのプロパティを更新します。

リポジトリ内の設定データを変更すると、Web コンソールを使用して変更がおこなわれた場合と同様に、適切な検証と整合性チェックをおこなって、変更が関連する OSGi 設定に直ちに適用されます。 これは、 `/libs/` から `/apps/`.

同じ設定パラメーターが複数の場所に配置される場合があるので、システムでは次の処理がおこなわれます。

* タイプのすべてのノードを検索 `sling:OsgiConfig`
* サービス名に従ってフィルター処理
* 実行モードに従ってフィルター処理

>[!NOTE]
>
>[特定のインスタンスのためだけにリポジトリベースの設定を定義する方法](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html)も参照してください。

### リポジトリへの新しい設定の追加 {#adding-a-new-configuration-to-the-repository}

#### 必要な知識 {#what-you-need-to-know}

新しい設定をリポジトリに追加するには、以下を知っておく必要があります。

1. この **永続 ID** (PID) サービス。

   参照先 **設定** Web コンソールの「 」フィールド。 この名前は、バンドル名の後 ( または **設定情報** をページの下部に向かって )、

   例えば、ノードを作成します。 `com.day.cq.wcm.core.impl.VersionManagerImpl.` 設定する **AEM WCM Version Manager**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 特定の [実行モード](/help/sites-deploying/configure-runmodes.md) が必要です。フォルダーを作成します。

   * `config`  — すべての実行モード用
   * `config.author`  — オーサー環境用
   * `config.publish`  — パブリッシュ環境用
   * `config.<run-mode>`  — 適宜

1. Whether a **設定** または **ファクトリ設定** が必要です。
1. 設定する個々のパラメーター。再作成が必要な既存のパラメータ定義を含めます。

   Web コンソールの個々のパラメーターフィールドを参照します。 名前は、各パラメーターに対して角括弧で囲まれて表示されます。

   例えば、プロパティを作成します。
   `versionmanager.createVersionOnActivation` 設定する **アクティベーション時にバージョンを作成**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. に既に設定が存在しますか？ `/libs`?インスタンス内のすべての設定をリストするには、 **クエリ** ツールをCRXDE Liteして次の SQL クエリを送信します。

   `select * from sling:OsgiConfig`

   その場合は、この設定をにコピーできます。 ` /apps/<yourProject>/`新しい場所にカスタマイズされます。

#### リポジトリでの設定の作成 {#creating-the-configuration-in-the-repository}

新しい設定をリポジトリに実際に追加するには：

1. CRXDE Lite を使用して次の場所に移動します。

   ` /apps/<yourProject>`

1. 既存のものがない場合は、 `config` フォルダー ( `sling:Folder`):

   * `config` - すべての実行モードに該当
   * `config.<run-mode>`  — 特定の実行モードに固有

1. このフォルダーの下に、次の設定でノードを作成します。

   * 型：`sling:OsgiConfig`
   * 名前：永続 ID(PID)

      例えば、AEM WCM Version Manager の場合は、 `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >ファクトリ設定を追加する場合 `-<identifier>` を名前に追加します。
   >
   >例： `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >ここで、 `<identifier>` は、インスタンスを識別するフリーテキストに置き換えられます（この情報は省略できません）。例：
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 設定するパラメーターごとに、このノードでプロパティを作成します。

   * 名前：Web コンソールに表示されるパラメーター名名前は、フィールドの説明の最後に角括弧で囲まれて表示されます。 例： `Create Version on Activation` use `versionmanager.createVersionOnActivation`
   * タイプ：適宜。
   * 値：必要に応じて。

   プロパティを作成する必要があるのは、設定対象のパラメーターのみです。その他は、AEM で設定されているデフォルト値を引き続き使用します。

1. すべての変更を保存します。

   変更は、サービスを再起動することによってノードが更新されるとすぐに適用されます（Web コンソールでおこなった変更と同様）。

>[!CAUTION]
>
>`/libs` パス内のものは一切変更しないでください。

>[!CAUTION]
>
>起動時に設定を読み込むには、設定のフルパスを正しく指定する必要があります。

## 設定の詳細 {#configuration-details}

### 起動時の優先順位 {#resolution-order-at-startup}

次の優先順位を使用します。

1. 以下のリポジトリノード `/apps/*/config...`.次のタイプ `sling:OsgiConfig` またはプロパティファイル。

1. タイプのリポジトリノード `sling:OsgiConfig` under `/libs/*/config...`. （標準定義）

1. 任意 `.config` から `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. ローカル・ファイル・システム上で

つまり、 `/libs` は、 `/apps`.

### 実行時の優先順位 {#resolution-order-at-runtime}

システム実行中に設定変更をおこなうと、変更後の設定で再読み込みが開始されます。

その後、次の優先順位が適用されます。

1. Web コンソールでの設定変更が、実行時に優先されるので、すぐに有効になります。
1. での設定の変更 `/apps` すぐに有効になります。
1. での設定の変更 `/libs` は、 `/apps`.

### 複数の実行モードの解決 {#resolution-of-multiple-run-modes}

実行モードに固有の設定に関しては、複数の実行モードを組み合わせることができます。例えば、設定フォルダーを次のスタイルで作成できます。

`/apps/*/config.<runmode1>.<runmode2>/`

このようなフォルダー内の設定は、起動時に定義されている実行モードにすべての実行モードが一致した場合に適用されます。

例えば、インスタンスが実行モードで開始した場合、 `author,dev,emea`、設定ノード `/apps/*/config.emea`, `/apps/*/config.author.dev/` および `/apps/*/config.author.emea.dev/` が適用され、設定ノードが `/apps/*/config.author.asean/` および `/config/author.dev.emea.noldap/` が適用されない。

同じ PID に複数の設定が該当する場合は、一致する実行モードの数が最も大きい設定が適用されます。

例えば、インスタンスが実行モードで開始した場合、 `author,dev,emea`と `/apps/*/config.author/` および `/apps/*/config.emea.author/` 設定を定義する\
`com.day.cq.wcm.core.impl.VersionManagerImpl`、 `/apps/*/config.emea.author/` が適用されます。

このルールの精度は PID レベルです。\
で同じ PID の一部のプロパティを定義することはできません。 `/apps/*/config.author/` の `/apps/*/config.emea.author/` と同じ PID の\
一致する実行モードの数が最も多い設定は、PID 全体に対して有効です。

### 標準設定 {#standard-configurations}

以下のリストは、リポジトリで使用できる（標準インストールの）設定の一部を示しています。

* 作成者 — AEM WCM フィルター：

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 公開 — AEM WCM フィルター：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 公開 — AEM WCM ページ統計：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>これらの設定はに存在するので、 `/libs` これらを直接編集することはできず、アプリケーション領域 ( `/apps`) をクリックします。

インスタンスに含まれるすべての設定ノードをリストするには、CRXDE Lite の&#x200B;**クエリ**&#x200B;機能を使用して、次の SQL クエリを送信します。

`select * from sling:OsgiConfig`

### 設定の永続性 {#configuration-persistence}

* Web コンソールを使用して設定を変更した場合、（通常は）次の場所にリポジトリに書き込まれます。

   `/apps/{somewhere}`

   * デフォルト `{somewhere}` が `system/config` 設定が

      `/apps/system/config`

   * ただし、最初にリポジトリ内の別の場所から取得した設定を編集する場合は、次のようにします。例：

      /libs/foo/config/someconfig

      その後、更新された設定が元の場所に書き込まれます。例：

      `/apps/foo/config/someconfig`

* 変更された設定 `admin` 次に保存： `*.config` 次の場所のファイル：

   ```
      /crx-quickstart/launchpad/config
   ```

   * これは OSGi 設定管理者の非公開データ領域であり、システムへの入力方法にかかわらず、`admin` によって指定された設定の詳細がすべて保持されます。
   * これは実装の詳細であり、このディレクトリをユーザーが直接編集してはいけません。
   * しかし、バックアップや複数インストールのためにコピーを取れるように、これらの設定ファイルの場所を知っておくと便利です。

      * Apache Felix OSGi Management Console

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling Client Repository

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>次の場所にあるフォルダーやファイルは、***決して***&#x200B;編集しないでください。
>
>`/crx-quickstart/launchpad/config`
