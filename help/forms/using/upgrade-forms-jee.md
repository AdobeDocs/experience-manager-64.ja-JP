---
title: AEM 6.4 Forms へのアップグレード
seo-title: Upgrade to AEM 6.4 Forms
description: AEM 6.1 Forms、AEM 6.2 Forms、LiveCycle ES4 SP1 を、AEM 6.3 Forms に直接アップグレードすることができます。
seo-description: You can perform a direct upgrade from AEM 6.1 Forms, AEM 6.2 Forms, and LiveCycle ES4 SP1 to AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: e41eb0fa-ae88-44d5-9181-0d925b8b62c6
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 17%

---

# JEE 上の AEM 6.4 Forms へのアップグレード {#upgrade-to-aem-forms-jee}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

お使いの環境に応じて、次のアップグレードパスのいずれかを使用します。

## JEE 上のAEM 6.2 Formsまたは JEE 上のAEM 6.3 Formsから JEE 上のAEM 6.4 Formsへ {#aem-forms-jee-62-63-to-64}

JEE 上の AEM 6.2 Forms または JEE 上の AEM 6.3 Forms を JEE 上の AEM 6.4 Forms にアップグレードするには、以下の手順を実行します。

1. JEE 上の AEM 6.4 Forms のインストーラーを、[アドビライセンス Web サイト（LWS）](https://licensing.adobe.com/)からダウンロードします。インストーラーをダウンロードするには、有効なメンテナンス＆サポートの契約が必要です。
1. [アップグレードのチェックリストと計画](https://www.adobe.com/go/learn_aemfroms_upgrade_checklist_63)で、アップグレードを正しく実行するためのチェック項目を確認します。
1. [AEM Forms へのアップグレードの準備](https://www.adobe.com/go/learn_aemforms_prepareupgrade_63_jp)で、サーバーのダウンタイムを最小限に抑えながらアップグレードを正しく行うためのタスクを確認し、これらのタスクを実行します。
1. 現在の環境とアプリケーションサーバーに応じて、以下に示すいずれかのドキュメントに記載されている手順を実行します。

   * [AEM 6.2 Forms または AEM 6.3 Forms から AEM 6.4 Forms へのアップグレード（JBoss 版）](assets/upgrade-jboss.pdf)
   * [AEM 6.2 またはAEM 6.3 FormsからAEM 6.4 Forms（WebLogic 版）へのアップグレード](assets/upgrade-weblogic.pdf)
   * [AEM 6.2 Forms または AEM 6.3 Forms から AEM 6.4 Forms へのアップグレード（WebSphere 版）](assets/upgrade-websphere.pdf)
   * [AEM 6.2 Forms または AEM 6.3 Forms から AEM 6.4 Forms へのアップグレード（JBoss Turnkey 版）](assets/upgrade-turnkey.pdf)

## JEE 上のAEM 6.0 Formsから JEE 上のAEM 6.3 Formsへ {#aem-forms-jee-60-to-63}

LiveCycle ES2、LiveCycle ES3、AEM 6.0 6.1 Forms、AEM Forms を AEM 6.4 Forms に直接アップグレードすることはできません。LiveCycle または AEM Forms のバージョンを 1 つ以上中間アップグレードした後に、AEM 6.4 Forms からアップグレードすることができます。中間バージョンのリストと対応するアップグレード手順について詳しくは、「[アップグレードパスを選択する](upgrade.md)」を参照してください。

## LiveCycleES4 SP1 から JEE 上のAEM 6.4 Formsまで {#livecycle-es4sp1-forms-jee}

LiveCycleES4 SP1 を JEE 上のAEM 6.4 Formsにアップグレードすると、以前のバージョンから、サポートされているアプリケーションサーバー、オペレーティングシステム、データベースの新しいインスタンス（新しいバージョン）にアセットとデータを移行する必要があります。

既存のLiveCycleES4 SP1 サーバーをAEM 6.4 Formsにアップグレードする手順の概要を次に示します。 詳細な手順については、手順の最後に示すドキュメントを参照してください。

1. アップグレードする前に：

   1. JEE 上の AEM 6.4 Forms のインストーラーを、[アドビライセンス Web サイト（LWS）](https://licensing.adobe.com/)からダウンロードします。インストーラーをダウンロードするには、有効なメンテナンス＆サポートの契約が必要です。
   1. 使用するコンテンツリポジトリ（CRX リポジトリ）の種類を決定します。 コンテンツとアセットを保存するために Content Repository の永続性を使用するのは、JEE 上のAEM Formsの機能のごく一部のみです。 JEE 上のAEM Forms機能を使用する予定の場合にのみ、コンテンツリポジトリをインストールして設定します。

      * LiveCycleES4 SP1 では、Correspondence Management、Forms Portal、HTMLワークスペース、プロセスレポート機能でコンテンツリポジトリを使用します。 LiveCycleES4 でこれらの機能を使用せず、AEM Formsでこれらの機能を使用しない予定の場合、コンテンツリポジトリは不要です。
      * AEM Forms、Adaptive Forms、Correspondence Management、HTML5 Forms(LiveCycleES4 SP1 では Mobile Formsと呼ばれます )、Forms Portal、HTMLWorkspace、Process Reporting、OSGi 上でForms中心のワークフローでは、機能はコンテンツリポジトリを使用します。 これらの機能でAEM Formsを使用する予定がある場合は、コンテンツリポジトリが必要です。
      * AEM Forms Document Security の場合は、コンテンツリポジトリは不要です。

      また、リポジトリのタイプがLiveCycleとAEM Formsで異なります。 使用可能なリポジトリタイプと関連情報については、 [AEM Formsインストールの永続性タイプの選択](/help/forms/using/choosing-persistence-type-for-aem-forms.md).

   1. LiveCycleES4 SP1 のコンテンツとデータのバックアップを作成します。

      LiveCycleES4 SP1 データベース、グローバルデータストレージ (GDS)、および crx-repository（Document Security には不要）のバックアップを作成します。 MongoMK または RDBMK 永続性にアップグレードする場合は、LiveCycleES4 SP1 Correspondence Management アセットを.cmp ファイルに書き出し、アセットをAEMパッケージとしてフォーム化します。

   1. 既存のプラットフォーム ( アプリケーションサーバー、データベース、オペレーティングシステム、Adobe Acrobat、サードパーティのアプリケーション、ハードウェア ) が JEE 上のAEM 6.4 Formsでサポートされていることを確認します。 サポートされるハードウェアとソフトウェアの詳細については、 [サポートされているプラットフォームの組み合わせ](/help/forms/using/aem-forms-jee-supported-platforms.md) 文書。

      データベースの新しいインスタンスを作成する場合は、手順 3 でバックアップしたデータをデータベースにインポートします。 データベースにデータをインポートする方法の詳細については、対応するデータベースベンダーのドキュメントを参照してください。

      >[!NOTE]
      >
      >RDBMK 永続化形式を使用する場合は、JEE 上のAEM Formsで実行されるリポジトリ永続化とドキュメントサービスの両方に 1 つのデータベースを使用します。


1. アップグレードを実行します。

   1. インストールプログラムを実行して、新しいサーバーにAEM 6.4 Forms on JEE をインストールします。 インストーラーは、必要なすべてのファイルをコンピューター上の 1 つのインストールディレクトリ構造内に配置します。
   1. インストールが完了したら、 **Configuration Manager** 様々なAEM Formsモジュールを設定し、適切な設定をおこなう。 設定のほかに、グローバルデータストレージ (GDS) と crx-repository のパスを指定できます。

      >[!NOTE]
      >
      >アップグレードタスクの選択画面で、 **[!UICONTROL Adobe Experience Manager Forms 6.2.0 からのアップグレード]** オプション。 この **[!UICONTROL Adobe Experience Manager Forms 6.2.0 からのアップグレード]** オプションを使用すると、configuration manager でLiveCycleES4 SP1 からAEM 6.4 Formsにアップグレードできます。

   1. (AEM Forms Document Security モジュールでは不要 ) コンテンツをAEM 6.4 Formsサーバーにコンテンツリポジトリ (CRX-Repository) に読み込みます。

      >[!NOTE]
      >
      >* crx-repository がアップグレードされ、コンテンツが移行されたら、admin アカウントのパスワードを変更します。 詳しい手順については、 [既存ユーザーのパスワードの変更](/help/sites-administering/granite-user-group-admin.md).


1. デプロイ後のタスクを実行して、ログイン資格情報の検証、Document Services の設定、Correspondence Management、Document Security などを使用事例に応じて行います。
1. サーバーが正常にアップグレードされたことを確認します。

   アップグレードされたAEM Formsサーバーでいくつかの日常的な操作を実行し、サーバーが正常にアップグレードされていることを確認します。 アップグレードを正常に行うには、いくつかの移行済みフォームに入力して送信するか、ドキュメントを保護します。

   >[!NOTE]
   >
   >AEM 6.4 Forms では crx-repository の構造が変更されています。AEM 6.4 forms にアップグレードした後、新しく作成するカスタマイズ用に、変更したパスを使用します。 変更されたパスの完全なリストについては、 [AEM 6.4 におけるFormsリポジトリの再構築](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md).

**既存の環境とアプリケーションサーバーに応じて、次のいずれかのドキュメントを選択し、詳細な手順に従います。**

* [LiveCycleES4 SP1 からAEM 6.4 Formsへのアップグレード（JBoss 版）](assets/upgrade-jboss-livecycle.pdf)
* [LiveCycleES4 SP1 からAEM 6.4 Formsへのアップグレード（WebLogic 版）](assets/upgrade-weblogic-livecycle.pdf)
* [LiveCycleES4 SP1 からAEM 6.4 Formsへのアップグレード（WebSphere 版）](assets/upgrade-websphere-livecycle.pdf)
* [JBoss Turnkey を使用したLiveCycleES4 SP1 からAEM 6.4 Formsへのアップグレード](assets/upgrade-turnkey-livecycle.pdf)

<!--Theses sections used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

## LiveCycleES3/JEE 上のAEM 6.4 Forms {#livecycle-es3-forms-jee}

LiveCycleES3 を JEE 上のAEM 6.4 Formsにアップグレードすると、アセットとデータを以前のバージョンから、サポートされているアプリケーションサーバー、オペレーティングシステム、データベースの新しいインスタンス（新しいバージョン）に移行する必要があるので、アウトオブプレースアップグレードです。

既存のLiveCycleES3 サーバーをAEM 6.4 Formsにアップグレードする手順の概要を次に示します。 詳細な手順については、手順の最後に示すドキュメントを参照してください。

1. アップグレードする前に：

   1. JEE 上の AEM 6.4 Forms のインストーラーを、[アドビライセンス Web サイト（LWS）](https://licensing.adobe.com/)からダウンロードします。インストーラーをダウンロードするには、有効なメンテナンス＆サポートの契約が必要です。
   1. 使用するコンテンツリポジトリ（CRX リポジトリ）の種類を決定します。 コンテンツとアセットを保存するために Content Repository の永続性を使用するのは、JEE 上のAEM Formsの機能のごく一部のみです。 JEE 上のAEM Forms機能を使用する予定の場合にのみ、コンテンツリポジトリをインストールして設定します。

      * AEM Forms、Adaptive Forms、Correspondence Management、HTML5 Forms、Forms Portal、HTMLワークスペース、プロセスレポート、OSGi 上のForms中心のワークフローでは、コンテンツリポジトリを使用します。 これらの機能でAEM Formsを使用する予定がある場合は、コンテンツリポジトリが必要です。
      * AEM Forms Document Security の場合は、コンテンツリポジトリは不要です。

      また、リポジトリのタイプがLiveCycleとAEM Formsで異なります。 使用可能なリポジトリタイプと関連情報については、 [AEM Formsインストールの永続性タイプの選択](/help/forms/using/choosing-persistence-type-for-aem-forms.md).

   1. LiveCycleES3 データベース、グローバルデータストレージ (GDS)、およびコンテンツリポジトリ（Document Security には不要）のバックアップを作成します。 MongoMK または RDBMK 永続性にアップグレードする場合は、LiveCycleES3 Correspondence Management アセットをアーカイブとして書き出します。
   1. 既存のプラットフォーム ( アプリケーションサーバー、データベース、オペレーティングシステム、Adobe Acrobat、サードパーティのアプリケーション、ハードウェア ) が JEE 上のAEM 6.4 Formsでサポートされていることを確認します。 サポートされるハードウェアとソフトウェアの詳細については、 [サポートされているプラットフォームの組み合わせ](/help/forms/using/aem-forms-jee-supported-platforms.md) 文書。

      データベースの新しいインスタンスを作成する場合は、手順 3 でバックアップしたデータをデータベースにインポートします。 データベースにデータをインポートする方法の詳細については、対応するデータベースベンダーのドキュメントを参照してください。

      >[!NOTE]
      >
      >RDBMK 永続化形式を使用する場合は、JEE 上のAEM Formsで実行されているリポジトリ永続化とドキュメントサービスの両方に単一のデータベースを使用します。


1. アップグレードを実行します。

   1. インストールプログラムを実行して、新しいサーバーにAEM 6.4 Forms on JEE をインストールします。 インストーラーは、必要なすべてのファイルをコンピューター上の 1 つのインストールディレクトリ構造内に配置します。
   1. インストールが完了したら、 **Configuration Manager** 様々なAEM Formsモジュールを設定し、適切な設定をおこなう。 設定のほかに、グローバルデータストレージ (GDS) と crx-repository のパスを指定できます。

      >[!NOTE]
      >
      >アップグレードタスクの選択画面で、 **[!UICONTROL Adobe Experience Manager Forms 6.2.0 からのアップグレード]** オプション。 この **[!UICONTROL Adobe Experience Manager Forms 6.2.0 からのアップグレード]** オプションを使用すると、configuration manager でLiveCycleES3 からAEM 6.4 Formsにアップグレードできます。

   1. (AEM Forms Document Security モジュールでは不要 )CRX リポジトリをアップグレードし、AEM 6.4 Formsサーバーに読み込みます。

      >[!NOTE]
      >
      >crx-repository がアップグレードされ、コンテンツが移行されたら、admin アカウントのパスワードを変更します。 詳しい手順については、 [既存ユーザーのパスワードの変更](/help/sites-administering/granite-user-group-admin.md).
1. デプロイ後のタスクを実行して、ログイン資格情報の検証、Document Services の設定、Correspondence Management、Document Security などを使用事例に応じて行います。
1. サーバーが正常にアップグレードされたことを確認します。

   アップグレードされたAEM Formsサーバーでいくつかの日常的な操作を実行し、サーバーが正常にアップグレードされていることを確認します。 アップグレードを正常に行うには、いくつかの移行済みフォームに入力して送信するか、ドキュメントを保護します。

   >[!NOTE]
   >
   >AEM 6.4 Forms では crx-repository の構造が変更されています。AEM 6.4 forms にアップグレードした後、新しく作成するカスタマイズ用に、変更したパスを使用します。 変更されたパスの完全なリストについては、 [AEM 6.4 におけるFormsリポジトリの再構築](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md).

**既存の環境とアプリケーションサーバーに応じて、次のいずれかのドキュメントを選択し、詳細な手順に従います。**

* [LiveCycleES3 からAEM 6.4 Formsへのアップグレード（JBoss 版）](assets/upgrade-jboss-livecycle-es3.pdf)
* [LiveCycleES3 からAEM 6.4 Formsへのアップグレード（WebLogic 版）](assets/upgrade-weblogic-livecycle-es3.pdf)
* [LiveCycleES3 からAEM 6.4 Formsへのアップグレード（WebSphere 版）](assets/upgrade-websphere-livecycle-es3.pdf)
* [JBoss Turnkey を使用したLiveCycleES3 からAEM 6.4 Formsへのアップグレード](assets/upgrade-turnkey-livecycle-es3.pdf)
