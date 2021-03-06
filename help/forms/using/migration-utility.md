---
title: AEM Forms のアセットとドキュメントの移行
seo-title: Migrate AEM Forms assets and documents
description: 移行ユーティリティにより、AEM Forms のアセットとドキュメントを AEM 6.3 Forms またはそれ以前のバージョンから AEM 6.4 forms に移行できます。
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
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 96%

---

# AEM Forms のアセットとドキュメントの移行 {#migrate-aem-forms-assets-and-documents}

移行ユーティリティを実行すると、[アダプティブフォームのアセット](/help/forms/using/introduction-forms-authoring.md)、[クラウドの設定](/help/sites-developing/extending-cloud-config.md)、[Correspondence Management のアセット](/help/forms/using/cm-overview.md) が、旧バージョンの AEM Forms で使用されていた形式から、AEM 6.4 Forms で使用される形式に変換されます。移行ユーティリティを実行すると、以下の項目が移行されます。

* アダプティブフォームのカスタムコンポーネント
* アダプティブフォームと Correspondence Management のテンプレート
* クラウドの設定情報
* Correspondence Management とアダプティブフォームのアセット

>[!NOTE]
>
>アウトオブプレースアップグレードを実行する場合（Correspondence Management のアセットを移行する場合）は、アセットをインポートするたびに、移行ユーティリティを実行することができます。Correspondence Management を移行する場合は、Forms 互換性パッケージがインストールされている必要があります。

## 移行の方法 {#approach-to-migration}

以下が可能です。 [アップグレード](/help/forms/using/upgrade.md) AEM Forms 6.3 または 6.2 からAEM Forms 6.4 の最新バージョンにアップグレードするか、新規インストールを実行します。 以前のインストール環境をアップグレードしたのか、新規インストールを実行したのかに応じて、以下に示すいずれかの手順を実行してください。

**インプレースアップグレードを実行した場合**

インプレースアップグレードを実行した場合、アップグレードインスタンスにはすでにアセットやドキュメントが存在します。ただし、これらのアセットやドキュメントを使用する前に、[AEMFD 互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja)（Correspondence Management 互換性パッケージが含まれています）をインストールする必要があります。

その後、[移行ユーティリティを実行](#runningmigrationutility)して、アセットとドキュメントを更新する必要があります。

**新規インストールを実行した場合**

新規インストールを実行した場合は、アセットやドキュメントを使用する前に、[AEMFD 互換性パッケージ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)（Correspondence Management 互換性パッケージが含まれています）をインストールする必要があります。

その後、アセットパッケージ（zip ファイルまたは cmp ファイル）を新しいセットアップ環境にインポートし、[移行ユーティリティ](#runningmigrationutility) を実行してアセットとドキュメントを更新してください。[後方互換性に関する要件](/help/sites-deploying/backward-compatibility.md)が変更されたことに伴い、CRX リポジトリ内のいくつかのフォルダーの場所が変更されています。以前のセットアップ環境内の依存関係（カスタムライブラリとカスタムアセット）を手動でエクスポートし、新しい環境に手動でインポートしてください。 

## 移行を進める前にお読みください {#prerequisites}

Correspondence Management のアセットを移行する場合は、以下の点に注意してください。

* 旧バージョンのプラットフォームからインポートしたアセットの場合、「**fd:version=1.0**」というプロパティが追加されます。
* AEM 6.1 Forms 以降、コメントは初期状態では使用できません。以前に追加されたコメントはアセット内で使用できますが、インターフェイスには自動で表示されません。コメントを表示させるには、AEM Forms のユーザーインターフェイスで extendedProperties プロパティをカスタマイズする必要があります。
* LiveCycle ES4 など、旧バージョンの一部では Flex RichTextEditor を使用してテキストを編集しましたが、AEM 6.1 Forms 以降では HTML エディターを使用します。このレンダリングにより、フォント、フォントサイズ、フォントマージンの外観は以前のバージョンの作成者ユーザーインターフェイスでの外観と異なる可能性があります。ただし、レターは同じように表示されます。
* テキストモジュールのリストが改善され、別々にレンダリングされるようになりました。外観や表示が今までと異なるところがあります。テキストモジュールのリストを使用している場所で、レターのレンダリングや表示を行うことをお勧めします。
* 移行中に画像コンテンツモジュールは DAM アセットおよびレイアウトに変換され、フラグメントはフォームに追加されるため、これらのモジュールの更新者プロパティは管理者に変更されます。
* アセットのバージョン履歴は移行されず、移行後は使用できなくなります。移行後のバージョン履歴は保持されます。
* AEM 6.1 Forms 以降では、「発行準備完了」の状態は廃止されました。このため、「発行準備完了」の状態にあったすべてのアセットは、変更済みの状態に変更されます。
* AEM Forms 6.3 ではユーザーインターフェイスが更新されているため、カスタマイズを行うための手順も異なります。6.3 よりも前のバージョンのアセットを移行する場合は、カスタマイズをやり直す必要があります。
* レイアウトフラグメントは、/content/apps/cm/layouts/fragmentlayouts/1001 から /content/apps/cm/modules/fragmentlayouts に移動しました。アセットのデータディクショナリ参照では、名前の代わりにデータディクショナリのパスを表示します。
* タブスペースを使用してテキストモジュールを調整した場合は、再調整する必要があります。詳しくは、「[Correspondence Management - タブスペースを使用したテキスト調整の詳細](https://helpx.adobe.com/jp/aem-forms/kb/cm-tab-spacing-limitations.html)」を参照してください。
* Asset Composer の設定は、Correspondence Management 設定に変更されました。
* アセットは、「Existing Text」や「Existing List」などの名前のフォルダーに移動されます。

## 移行ユーティリティの使用 {#using-the-migration-utility}

### 移行ユーティリティの実行 {#runningmigrationutility}

移行ユーティリティを実行した後で、アセットに変更を加えたり、アセットを作成したりします。移行ユーティリティは、アセットの変更や作成後に実行しないことをお勧めします。移行プロセスの実行中は、Correspondence Management アセットまたはアダプティブフォームアセットのユーザーインターフェイスが開いていないことを確認してください。

初めて移行ユーティリティを実行すると、次のパスと名前でログが作成されます。 `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. それ以降は、移行ユーティリティを実行するたびに、Correspondence Management とアダプティブフォームの移行に関する情報（アセットの移行に関する情報など）がこのログファイルに記録されます。

>[!NOTE]
>
>移行ユーティリティを実行する前に、必ず CRX リポジトリのバックアップを作成してください。

1. ブラウザーセッションで、AEM オーサーインスタンスに管理者としてログインします。

1. ブラウザーで次の URL を開きます。

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   ブラウザーに、以下に示す 4 つのオプションが表示されます。

   * AEM Forms アセットの移行
   * アダプティブフォームカスタムコンポーネントの移行
   * アダプティブフォームテンプレートの移行
   * AEM Forms クラウド設定の移行

1. 移行するには、次の手順を実行します。

   * **アセット**&#x200B;を移行する場合は、「AEM Forms アセットの移行」をタップし、次の画面で「**移行を開始**」をタップします。次のものが移行されます。

      * アダプティブフォーム
      * ドキュメントフラグメント
      * テーマ
      * レター
      * データディクショナリ

   >[!NOTE]
   >
   >移行中、「競合が見つかりました...」のような警告メッセージが表示される場合があります。このようなメッセージは、アダプティブフォームのコンポーネントのいくつかのルールを移行できなかったことを示します。例えば、コンポーネントにルールとスクリプトの両方がある場合、スクリプトの後にルールが発生した場合はそのコンポーネントのルールは移行されません。ただし、そのようなルールは、アダプティブフォームのオーサリングでルールエディターを開くことで移行することができます。
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

      * アダプティブフォーム用に書き込まれたカスタムコンポーネント
      * コンポーネントのオーバーレイ（存在する場合）
   * アダプティブフォームのテンプレートを移行する場合は、「**アダプティブフォームテンプレートの移行**」をタップし、カスタムコンポーネントの移行ページで「**移行を開始**」をタップします。次のものが移行されます。

      * AEM テンプレートエディターを使用して /apps フォルダーまたは /conf フォルダー内に作成されたアダプティブフォームテンプレート
   * 新しいコンテキスト認識クラウドサービスメカニズムを使用するには、AEM Forms クラウド設定サービスを移行する必要があります。このメカニズムには、タッチ操作が可能な UI が用意されています（/conf フォルダーに保管されています）。AEM Forms クラウド設定サービスを移行すると、/etc 内のクラウドサービスが /conf に移動します。移行前のパス（/etc）に依存するクラウドサービスがカスタマイズされていない場合は、バージョン 6.4 にアップグレード後すぐに移行ユーティリティを実行して、クラウド設定のタッチ UI を使用して作業を行うことをお勧めします。既存のクラウドサービスがカスタマイズされている場合は、移行後のパス（/conf フォルダー）に合わせてカスタマイズ内容を更新するまでは、アップグレード後のセットアップ環境で既存の UI を使用してください。カスタマイズ内容の更新が完了したら、移行ユーティリティを実行してください。

   **AEM Forms クラウドサービス**&#x200B;を移行する場合は、「AEM Forms クラウド設定の移行」（クラウド設定の移行は、AEMFD 互換性パッケージとは独立して実行されます）をタップし、「AEM Forms クラウド設定の移行」をもう一度タップして、設定の移行ページで「**移行を開始**」をタップします。AEM Forms クラウドサービスには、以下の項目が含まれています。

   * フォームデータモデルのクラウドサービス

      * ソースパス：/etc/cloudservices/fdm
      * ターゲットパス：/conf/global/settings/cloudconfigs/fdm
   * reCAPTCHA

      * ソースパス：/etc/cloudservices/recaptcha
      * ターゲットパス：/conf/global/settings/cloudconfigs/recaptcha
   * Adobe Sign

      * ソースパス：/etc/cloudservices/echosign
      * ターゲットパス：/conf/global/settings/cloudconfigs/echosign
   * Typekit クラウドサービス

      * ソースパス：/etc/cloudservices/typekit
      * ターゲットパス：/conf/global/settings/cloudconfigs/typekit

   移行プロセスの実行時は、ブラウザーウィンドウにそれぞれ以下が表示されます。

   * アセットを更新したとき：アセットは正しく更新されました。
   * 移行が完了したとき：アセットの移行が完了しました。

   完了後は、移行ユーティリティで以下を実行します。

   * **タグをアセットに追加**：タグ「Correspondence Management：移行済みアセット」または「アダプティブフォーム：移行済みアセット」を移行済みのアセットに追加します。これにより、ユーザーは移行済みアセットを識別できます。移行ユーティリティを実行するときは、システム内の既存のアセットはすべて移行済みとしてマークされます。
   * **タグを生成**：以前のシステムに存在するカテゴリおよびサブカテゴリはタグとして作成され、これらのタグは AEM 内で関連する Correspondence Management アセットに関連付けられます。例えば、レターテンプレートのカテゴリ（「要求」）とサブカテゴリ（「要求」）は、タグとして生成されます。
   * **レイアウトおよびレイアウトフラグメントを AEM 6.4 Forms ユーザーインターフェイスに移動**：バージョン 6.2 をバージョン 6.4 にアップグレードすると、レイアウトテンプレートとレイアウトフラグメントが、AEM Forms 6.4 のユーザーインターフェイスセクションにフォームとして追加されます。

   >[!NOTE]
   >
   >バージョン 6.2 をバージョン 6.4 にアップグレードすると、アセットが保管された、Correspondence Management 用の新しいフォルダーが UI に表示される場合があります。アセットを見つけるためこれらのフォルダーを確認する必要がある場合があります。

1. 移行ユーティリティが実行を終了した後、[ハウスキーピングタスク](#housekeepingtasks)に進みます。

### 移行ユーティリティ実行後のハウスキーピングタスク {#housekeepingtasks}

移行ユーティリティを実行した後、次のハウスキーピングタスクを行います。

1. レイアウトおよびフラグメントレイアウトの XFA バージョンが 3.3 以降であることを確認してください。旧バージョンのレイアウトおよびフラグメントレイアウトを使用している場合、レターのレンダリングで問題が発生する可能性があります。旧バージョンの XFA を最新バージョンの XFA に更新するには、以下の手順を行ってください。

   1. Forms ユーザーインターフェイスから [XFA を zip ファイルとしてダウンロード](/help/forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p)します。
   1.  ファイルを解凍します。
   1. 最新の Designer で XFA ファイルを開き、保存します。XFA が最新バージョンに更新されます。
   1. XFA を Forms ユーザーインターフェイスでアップロードします。

1. 移行前に以前のシステムで発行されたすべてのアセットを発行します。移行ユーティリティは、オーサーインスタンスでのみアセットを更新して、アセットを発行する必要のあるパブリッシュインスタンスでアセットを更新します。
1. AEM Forms 6.4 では、フォームユーザーグループの権限が一部変更されています。ユーザーが XDP やスクリプトを含むアダプティブフォームをアップロードしたりコードエディターを使用したりできるようにするには、そのユーザーを forms-power-users グループに追加する必要があります。同様に、template-authors グループのユーザーは、ルールエディターのコードエディターを使用できなくなります。ユーザーがコードエディターを使用できるようにするには、そのユーザーを af-template-script-writers グループに追加します。ユーザーをグループに追加する方法については、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。
