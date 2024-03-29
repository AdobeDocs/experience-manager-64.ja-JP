---
title: AEM Forms のアセットとドキュメントの移行
seo-title: Migrate AEM Forms assets and documents
description: 移行ユーティリティを使用すると、AEM FormsのアセットとドキュメントをAEM 6.3 Forms以前のバージョンからAEM 6.4 Formsに移行できます。
seo-description: The Migration utility allows you to Migrate AEM Forms assets and documents from AEM 6.3 Forms or prior versions to AEM 6.4 Forms.
uuid: 593fc421-b70e-4dbe-87bc-ea49ff025368
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
content-strategy: max-2018
discoiquuid: a8b1f7df-e36f-4d02-883a-72120fea7046
role: Admin
exl-id: 72ead30c-648d-43ad-9826-9c8945a8860d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 56%

---

# AEM Forms のアセットとドキュメントの移行  {#migrate-aem-forms-assets-and-documents}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

移行ユーティリティを実行すると、[アダプティブフォームのアセット](/help/forms/using/introduction-forms-authoring.md)、[クラウドの設定](/help/sites-developing/extending-cloud-config.md)、[Correspondence Management のアセット](/help/forms/using/cm-overview.md) が、旧バージョンの AEM Forms で使用されていた形式から、AEM 6.4 Forms で使用される形式に変換されます。移行ユーティリティを実行すると、以下の項目が移行されます。

* アダプティブフォームのカスタムコンポーネント
* アダプティブフォームと Correspondence Management テンプレート
* クラウドの設定情報
* Correspondence Management とアダプティブフォームのアセット

>[!NOTE]
>
>アウトオブプレースアップグレードの場合、Correspondence Management アセットの場合は、アセットを読み込むたびに移行を実行できます。 Correspondence Management の移行の場合は、Forms互換性パッケージをインストールする必要があります。

## 移行のアプローチ {#approach-to-migration}

以下が可能です。 [アップグレード](/help/forms/using/upgrade.md) AEM Forms 6.3 または 6.2 からAEM Forms 6.4 の最新バージョンにアップグレードするか、新規インストールを実行します。 以前のインストールをアップグレードしたか、新規インストールを実行したかに応じて、次のいずれかを実行する必要があります。

**インプレースアップグレードの場合**

インプレースアップグレードを実行した場合、アップグレードされたインスタンスには既にアセットとドキュメントが含まれています。 ただし、アセットとドキュメントを使用する前に、をインストールする必要があります [AEMFD 互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) （Correspondence Management 互換性パッケージを含む）

その後、[移行ユーティリティを実行](#runningmigrationutility)して、アセットとドキュメントを更新する必要があります。

**新規インストールを実行した場合**

新規インストールを実行した場合は、アセットやドキュメントを使用する前に、[AEMFD 互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)（Correspondence Management 互換性パッケージが含まれています）をインストールする必要があります。

その後、アセットパッケージ（zip ファイルまたは cmp ファイル）を新しいセットアップ環境にインポートし、[移行ユーティリティ](#runningmigrationutility) を実行してアセットとドキュメントを更新してください。[後方互換性に関する要件](/help/sites-deploying/backward-compatibility.md)が変更されたことに伴い、CRX リポジトリ内のいくつかのフォルダーの場所が変更されています。以前のセットアップ環境内の依存関係（カスタムライブラリとカスタムアセット）を手動でエクスポートし、新しい環境に手動でインポートしてください。 

## 移行を進める前にお読みください {#prerequisites}

Correspondence Management のアセットを移行する場合は、以下の点に注意してください。

* 旧バージョンのプラットフォームからインポートしたアセットの場合、「**fd:version=1.0**」というプロパティが追加されます。
* AEM 6.1 Forms 以降、コメントは初期状態では使用できません。以前に追加されたコメントはアセット内で使用できますが、インターフェイスには自動で表示されません。コメントを表示させるには、AEM Forms のユーザーインターフェイスで extendedProperties プロパティをカスタマイズする必要があります。
* LiveCycleES4 などの以前のバージョンの一部では、テキストはFlex RichTextEditor を使用して編集されましたが、AEM 6.1 Forms以降はHTMLエディターが使用されます。 このレンダリングと外観により、フォント、フォントサイズ、フォントマージンは、作成者ユーザーインターフェイスの以前のバージョンとは異なる場合があります。 ただし、レンダリング時にはレターは同じように見えます。
* テキストモジュール内のリストが改善され、別の方法でレンダリングされるようになりました。 視覚的な違いが生じる場合があります。 テキストモジュールでリストを使用している場所でレンダリングしてレターを表示することをお勧めします。
* 画像コンテンツモジュールは移行時に DAM アセットおよびレイアウトに変換され、フラグメントはフォームに追加されるので、これらのモジュールの更新者プロパティは管理者に変更されます。
* アセットのバージョン履歴は移行されず、移行後は使用できません。 移行後のバージョン履歴は保持されます。
* AEM 6.1 Forms 以降では、「発行準備完了」の状態は廃止されました。このため、「発行準備完了」の状態にあったすべてのアセットは、変更済みの状態に変更されます。
* AEM Forms 6.3 ではユーザーインターフェイスが更新されたので、カスタマイズを実行する手順も異なります。 6.3 より前のバージョンから移行する場合は、カスタマイズをやり直す必要があります。
* レイアウトフラグメントは、/content/apps/cm/layouts/fragmentlayouts/1001 から /content/apps/cm/modules/fragmentlayouts に移動しました。アセットのデータディクショナリ参照では、名前の代わりにデータディクショナリのパスを表示します。
* テキストモジュールでの配置に使用するタブスペースは、再調整する必要があります。 詳しくは、 [Correspondence Management — タブ間隔を使用したテキストの配置](https://helpx.adobe.com/jp/aem-forms/kb/cm-tab-spacing-limitations.html).
* Asset Composer の設定は、Correspondence Management 設定に変更されました。
* アセットは、「Existing Text」や「Existing List」などの名前のフォルダーに移動されます。

## 移行ユーティリティの使用 {#using-the-migration-utility}

### 移行ユーティリティの実行 {#runningmigrationutility}

アセットに変更を加えたり、アセットを作成したりする前に、移行ユーティリティを実行します。 アセットの変更や作成を行った後は、ユーティリティを実行しないことをお勧めします。 移行プロセスの実行中は、Correspondence Management アセットまたはアダプティブフォームアセットのユーザーインターフェイスが開いていないことを確認してください。

移行ユーティリティをはじめて実行する場合、`\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log` というパスと名前でログが作成されます。このログは、アセットの移動など、Correspondence Management および Adaptive Formsの移行情報で更新され続けます。

>[!NOTE]
>
>移行ユーティリティを実行する前に、crx リポジトリのバックアップを作成していることを確認します。

1. ブラウザーセッションで、AEM オーサーインスタンスに管理者としてログインします。

1. ブラウザーで次の URL を開きます。

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   ブラウザーに、以下に示す 4 つのオプションが表示されます。

   * AEM Forms アセットの移行
   * アダプティブフォームカスタムコンポーネントの移行
   * アダプティブフォームテンプレートの移行
   * AEM Forms クラウド設定の移行

1. 移行を実行するには、以下の手順を実行します。

   * **アセット**&#x200B;を移行する場合は、「AEM Forms アセットの移行」をタップし、次の画面で「**移行を開始**」をタップします。次のものが移行されます。

      * アダプティブフォーム
      * ドキュメントフラグメント
      * テーマ
      * レター
      * データディクショナリ

   >[!NOTE]
   >
   >アセットの移行中に、「競合が見つかりました…」などの警告メッセージが表示される場合があります。 このようなメッセージは、アダプティブフォームのコンポーネントのいくつかのルールを移行できなかったことを示します。例えば、コンポーネントにルールとスクリプトの両方がある場合、スクリプトの後にルールが発生した場合はそのコンポーネントのルールは移行されません。ただし、アダプティブフォームのオーサリングでルールエディターを開くと、このようなルールを移行できます。
   >
   >これらのコンポーネントは、アダプティブフォームのルールエディターで開くことで移行できます。
   >
   >* カスタムコンポーネントのルールとスクリプトを移行する場合は、「アダプティブフォームカスタムコンポーネントの移行」をタップし、次の画面で「移行を開始」をタップします（バージョン 6.3 をアップグレードする場合は、この移行手順を実行する必要はありません）。次のものが移行されます。
   >
   >  * ルールエディターで作成されたルールとスクリプト（6.1 FP1 以降）
   >  * 6.1 以前の UI の「スクリプト」タブで作成されたスクリプト
   >* （6.3 からアップグレードする場合は不要）テンプレートを移行するには、「アダプティブFormsテンプレートの移行」をタップし、次の画面で「移行を開始」をタップします。 次のものが移行されます。
   >
   >  * 古いテンプレート - AEM 6.1 Forms 以前を使用して /apps に作成されたアダプティブフォームテンプレート。これには、テンプレートコンポーネントに定義されたスクリプトも含まれます。
   >  * 新しいテンプレート - テンプレートエディターを使用して /conf に作成されたアダプティブフォームテンプレート。これには、ルールエディターで作成されたルールとスクリプトが含まれます。


   * アダプティブフォームのカスタムコンポーネントを移行する場合は、「**アダプティブフォームカスタムコンポーネントの移行**」をタップし、カスタムコンポーネントの移行ページで「**移行を開始**」をタップします。次のものが移行されます。

      * アダプティブForms用に作成されたカスタムコンポーネント
      * コンポーネントオーバーレイ（存在する場合）。
   * アダプティブフォームのテンプレートを移行する場合は、「**アダプティブフォームテンプレートの移行**」をタップし、カスタムコンポーネントの移行ページで「**移行を開始**」をタップします。次のものが移行されます。

      * AEMテンプレートエディターを使用して/apps または/conf の下に作成されたアダプティブフォームテンプレート。
   * 新しいコンテキスト認識クラウドサービスメカニズムを使用するには、AEM Forms クラウド設定サービスを移行する必要があります。このメカニズムには、タッチ操作が可能な UI が用意されています（/conf フォルダーに保管されています）。AEM Forms クラウド設定サービスを移行すると、/etc 内のクラウドサービスが /conf に移動します。移行前のパス（/etc）に依存するクラウドサービスがカスタマイズされていない場合は、バージョン 6.4 にアップグレード後すぐに移行ユーティリティを実行して、クラウド設定のタッチ UI を使用して作業を行うことをお勧めします。既存のクラウドサービスがカスタマイズされている場合は、移行後のパス（/conf フォルダー）に合わせてカスタマイズ内容を更新するまでは、アップグレード後のセットアップ環境で既存の UI を使用してください。カスタマイズ内容の更新が完了したら、移行ユーティリティを実行してください。

   **AEM Forms クラウドサービス**&#x200B;を移行する場合は、「AEM Forms クラウド設定の移行」（クラウド設定の移行は、AEMFD 互換性パッケージとは独立して実行されます）をタップし、「AEM Forms クラウド設定の移行」をもう一度タップして、設定の移行ページで「**移行を開始**」をタップします。AEM Forms クラウドサービスには、以下の項目が含まれています。

   * フォームデータモデルのクラウドサービス

      * ソースパス：/etc/cloudservices/fdm
      * ターゲットパス：/conf/global/settings/cloudconfigs/fdm
   * reCAPTCHA

      * ソースパス：/etc/cloudservices/recaptcha
      * ターゲットパス：/conf/global/settings/cloudconfigs/recaptcha
   * Acrobat Sign

      * ソースパス：/etc/cloudservices/echosign
      * ターゲットパス：/conf/global/settings/cloudconfigs/echosign
   * Typekit クラウドサービス

      * ソースパス：/etc/cloudservices/typekit
      * ターゲットパス：/conf/global/settings/cloudconfigs/typekit

   移行プロセスの実行時は、ブラウザーウィンドウにそれぞれ以下が表示されます。

   * アセットが更新されたとき：アセットが正常に更新されました。
   * 移行が完了したら、次の手順に従います。アセットの移行が完了しました。

   実行すると、移行ユーティリティは次の処理を実行します。

   * **アセットにタグを追加します**:タグ「Correspondence Management :移行済みのアセット/「アダプティブForms」:移行されたアセット」 これにより、ユーザーは移行済みアセットを識別できます。移行ユーティリティを実行するときは、システム内の既存のアセットはすべて移行済みとしてマークされます。
   * **タグを生成**：以前のシステムに存在するカテゴリおよびサブカテゴリはタグとして作成され、これらのタグは AEM 内で関連する Correspondence Management アセットに関連付けられます。例えば、レターテンプレートのカテゴリ（要求）およびサブカテゴリ（要求）は、タグとして生成されます。
   * **レイアウトおよびレイアウトフラグメントをAEM 6.4 Formsユーザーインターフェイスに移動します**:6.2 から 6.4 にアップグレードする場合、レイアウトテンプレートとレイアウトフラグメントは、 AEM Forms 6.4 のユーザーインターフェイスの節にフォームとして追加されます。

   >[!NOTE]
   >
   >6.2 から 6.4 にアップグレードする場合、Correspondence Management では、UI にアセットを含む新しいフォルダが表示される場合があります。 アセットを見つけるには、これらのフォルダーを確認する必要がある場合があります。

1. 移行ユーティリティが実行を終了した後、[ハウスキーピングタスク](#housekeepingtasks)に進みます。

### 移行ユーティリティ実行後のハウスキーピングタスク {#housekeepingtasks}

移行ユーティリティを実行した後、次のハウスキーピングタスクを実行します。

1. レイアウトおよびフラグメントレイアウトの XFA バージョンが 3.3 以降であることを確認してください。旧バージョンのレイアウトおよびフラグメントレイアウトを使用している場合、レターのレンダリングで問題が発生する可能性があります。旧バージョンの XFA を最新バージョンの XFA に更新するには、以下の手順を行ってください。

   1. Forms ユーザーインターフェイスから [XFA を zip ファイルとしてダウンロード](/help/forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p)します。
   1.  ファイルを解凍します。
   1. 最新の Designer で XFA ファイルを開き、保存します。 XFA のバージョンが最新のバージョンに更新されます。
   1. Formsユーザーインターフェイスで XFA をアップロードします。

1. 移行前に以前のシステムで公開されたすべてのアセットを公開します。 移行ユーティリティは、オーサーインスタンス上でのみアセットを更新し、アセットの公開に必要なパブリッシュインスタンス上のアセットを更新します。
1. AEM Forms 6.4 では、forms users グループの一部の権限が変更されています。 任意のユーザーが XDP やスクリプトを含むアダプティブFormsをアップロードしたり、コードエディターを使用したりできるようにするには、それらのユーザーを forms-power-users グループに追加する必要があります。 同様に、 template-authors は、ルールエディターでコードエディターを使用できなくなりました。 ユーザーがコードエディターを使用できるようにするには、そのユーザーを af-template-script-writers グループに追加します。ユーザーをグループに追加する方法については、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。
