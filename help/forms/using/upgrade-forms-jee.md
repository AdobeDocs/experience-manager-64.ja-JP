---
title: AEM 6.4 Forms へのアップグレード
seo-title: AEM 6.4 Forms へのアップグレード
description: 'AEM 6.1 Forms、AEM 6.2 Forms、LiveCycle ES4 SP1 を、AEM 6.3 Forms に直接アップグレードすることができます。 '
seo-description: 'AEM 6.1 Forms、AEM 6.2 Forms、LiveCycle ES4 SP1 を、AEM 6.3 Forms に直接アップグレードすることができます。 '
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Administrator
exl-id: e41eb0fa-ae88-44d5-9181-0d925b8b62c6
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 75%

---

# JEE上のAEM 6.4 Forms {#upgrade-to-aem-forms-jee}へのアップグレード

お使いの環境に応じて、次のアップグレードパスのいずれかを使用します。

## JEE 上の AEM 6.2 Forms または JEE 上の AEM 6.3 Forms から JEE 上の AEM 6.4 Forms へのアップグレード {#aem-forms-jee-62-63-to-64}

JEE 上の AEM 6.2 Forms または JEE 上の AEM 6.3 Forms を JEE 上の AEM 6.4 Forms にアップグレードするには、以下の手順を実行します。

1. JEE 上の AEM 6.4 Forms のインストーラーを、[アドビライセンス Web サイト（LWS）](https://licensing.adobe.com/)からダウンロードします。インストーラーをダウンロードするには、有効なメンテナンス＆サポートの契約が必要です。
1. [アップグレードのチェックリストと計画](https://www.adobe.com/go/learn_aemfroms_upgrade_checklist_63)を参照して、アップグレードを正常に実行するために実行するチェックについて確認してください。
1. [AEM Formsへのアップグレードの準備](https://www.adobe.com/go/learn_aemforms_prepareupgrade_63)を参照して、サーバーのダウンタイムを最小限に抑えながらアップグレードを正しく実行するためのタスクを確認し、実行してください。
1. 現在の環境とアプリケーションサーバーに応じて、以下に示すいずれかのドキュメントに記載されている手順を実行します。

   * [AEM 6.2 Forms または AEM 6.3 Forms から AEM 6.4 Forms へのアップグレード（JBoss 版）](assets/upgrade-jboss.pdf)
   * [AEM 6.2 Forms または AEM 6.3 Forms から AEM 6.4 Forms へのアップグレード（WebLogic 版）](assets/upgrade-weblogic.pdf)
   * [AEM 6.2 Forms または AEM 6.3 Forms から AEM 6.4 Forms へのアップグレード（WebSphere 版）](assets/upgrade-websphere.pdf)
   * [AEM 6.2 Forms または AEM 6.3 Forms から AEM 6.4 Forms へのアップグレード（JBoss Turnkey 版）](assets/upgrade-turnkey.pdf)

## JEE 上の AEM 6.0 Forms から JEE 上の AEM 6.3 Forms へのアップグレード {#aem-forms-jee-60-to-63}

LiveCycleES2、LiveCycleES3、AEM 6.0 Forms、AEM 6.1 FormsからAEM 6.4 Formsへの直接アップグレードは使用できません。 LiveCycle または AEM Forms のバージョンを 1 つ以上中間アップグレードした後に、AEM 6.4 Forms からアップグレードすることができます。中間バージョンのリストと対応するアップグレード手順について詳しくは、「[アップグレードパスを選択する](upgrade.md)」を参照してください。

## LiveCycle ES4 SP1 から JEE 上の AEM 6.4 Forms へのアップグレード  {#livecycle-es4sp1-forms-jee}

LiveCycle ES4 SP1 から JEE 上の AEM 6.4 Forms へのアップグレードは、アウトオブプレースアップグレードです。このアップグレードでは、旧バージョンのアセットとデータが、サポートされているアプリケーションサーバー、オペレーティングシステム、データベースの新しいインスタンス（新しいバージョン）に移行されます。

既存の LiveCycle ES4 SP1 サーバーを AEM 6.4 Forms にアップグレードするための概要的な手順を以下に示します。詳しい手順については、このセクションの最後に記載されているドキュメントを参照してください。

1. アップグレードの準備:

   1. JEE 上の AEM 6.4 Forms のインストーラーを、[アドビライセンス Web サイト（LWS）](https://licensing.adobe.com/)からダウンロードします。インストーラーをダウンロードするには、有効なメンテナンス＆サポートの契約が必要です。
   1. 使用するコンテンツリポジトリ（CRX リポジトリ）タイプを選択します。JEE 上の AEM Forms のごく一部の機能でのみ、コンテンツリポジトリの永続化機能を使用してコンテンツとアセットが保管されます。JEE上のAEM Forms機能を使用する予定の場合のみ、Content Repositoryをインストールして設定します。

      * LiveCycle ES4 SP1 では、Correspondence Management、Forms Portal、HTML Workspace、Process Reporting の各機能でコンテンツリポジトリが使用されます。LiveCycleES4でこれらの機能を使用せず、AEM Formsでこれらの機能を使用しない予定の場合、コンテンツリポジトリは不要です。
      * AEM Forms では、Adaptive Forms、Correspondence Management、HTML5 Forms（LiveCycle ES4 SP1 での名称は Mobile Forms）、Forms Portal、HTML Workspace、Process Reporting、OSGi 上の Forms 中心ワークフローの各機能で、コンテンツリポジトリが使用されます。これらの機能でAEM Formsを使用する予定がある場合は、コンテンツリポジトリが必要です。
      * AEM Forms Document Security用のコンテンツリポジトリは不要です。

      また、LiveCycle と AEM Forms では、リポジトリタイプが異なります。使用可能なリポジトリのタイプと関連情報については、[AEM Formsのインストールに永続性タイプを選択する](/help/forms/using/choosing-persistence-type-for-aem-forms.md)を参照してください。

   1. LiveCycle ES4 SP1 のコンテンツとデータのバックアップを作成します。

      LiveCycle ES4 SP1 のデータベース、グローバルデータストレージ（GDS）、CRX リポジトリ（ドキュメントセキュリティの場合は必要ありません）のバックアップを作成します。MongoMK パーシスタンスまたは RDBMK パーシスタンスにアップグレードする場合は、LiveCycle ES4 SP1 の通信管理アセットを .cmp ファイルに書き出し、フォームアセットを AEM パッケージとして書き出します。

   1. アプリケーションサーバー、データベース、オペレーティングシステム、Adobe Acrobat、サードパーティアプリケーション、ハードウェアから構成される既存のプラットフォームが、JEE 上の AEM 6.4 Forms でサポートされているかどうかを確認します。サポート対象のハードウェアおよびソフトウェアについては、「[サポートされているプラットフォームの組み合わせ](/help/forms/using/aem-forms-jee-supported-platforms.md)」ドキュメントを参照してください。

      データベースの新しいインスタンスを作成する場合、手順 3 でバックアップしたデータをデータベースに読み込みます。データをデータベースに読み込む方法については、該当するデータベースベンダーのドキュメントを参照してください。

      >[!NOTE]
      >
      >RDBMK 永続性フォーマットを使用している場合、JEE 上の AEM Forms で実行されているリポジトリ永続化とドキュメントサービスの両方に単一のデータベースを使用します。


1. 以下の手順でアップグレードを実行します。

   1. インストーラーを実行して、JEE 上の AEM 6.4 Forms を新しいサーバーにインストールします。インストーラーを実行すると、必要なすべてのファイルが、使用するコンピューター上の 1 つのインストールディレクトリ構造内に配置されます。
   1. インストールが完了したら、**Configuration Manager** を実行して、各種の AEM Forms モジュールを適切に設定します。設定のほかに、グローバルデータストレージ(GDS)とcrx-repositoryのパスを指定できます。

      >[!NOTE]
      >
      >アップグレードタスクの選択画面で、「Adobe Experience Manager Forms 6.2.0からのアップグレード&#x200B;**** 」オプションを選択します。 「**[!UICONTROL Adobe Experience Manager Forms 6.2.0からアップグレード]**」オプションを使用すると、Configuration ManagerでLiveCycleES4 SP1からAEM 6.4 Formsにアップグレードできます。

   1. コンテンツリポジトリ（CRX リポジトリ）の内容を AEM 6.4 Forms サーバーに読み込みます（AEM Forms ドキュメントセキュリティモジュールの場合は、この操作を実行する必要はありません）。

      >[!NOTE]
      >
      >* CRX リポジトリのアップグレードとリポジトリ内のコンテンツの移行が完了したら、管理者アカウントのパスワードを変更します。詳しい手順については、「[既存ユーザーのパスワードの変更](/help/sites-administering/granite-user-group-admin.md)」を参照してください。


1. デプロイメント後のタスクを実行して、ログイン資格情報の検証、ドキュメントサービスの設定、通信の管理、ドキュメントセキュリティの設定などを行います（使用するユースケースに応じて、必要な作業を行ってください）。
1. サーバーが正常にアップグレードされているかどうかの確認:

   いくつかの一般的な操作をアップグレード後の AEM Forms サーバーで実行し、サーバーが正しくアップグレードされていることを確認します。例えば、移行後のいくつかのフォームで入力を行ったり、ドキュメントの保護を行うことにより、正しくアップグレードされているかどうかを確認することができます。

   >[!NOTE]
   >
   >AEM 6.4 Forms では crx-repository の構造が変更されています。AEM 6.4 Forms にアップグレードしたあと、新規作成するカスタマイズについては、変更後のパスを使用してください。変更後のパスの一覧については、「[AEM 6.4 Forms におけるリポジトリの再構築](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md)」を参照してください。

**現在の環境とアプリケーションサーバーに応じて、以下に示すいずれかのドキュメントに記載されている手順を実行します。**

* [LiveCycle ES4 SP1 から AEM 6.4 Forms へのアップグレード（JBoss 版）](assets/upgrade-jboss-livecycle.pdf)
* [LiveCycleES4 SP1からAEM 6.4 Formsへのアップグレード（WebLogic版）](assets/upgrade-weblogic-livecycle.pdf)
* [LiveCycleES4 SP1からAEM 6.4 Formsへのアップグレード（WebSphere版）](assets/upgrade-websphere-livecycle.pdf)
* [JBoss Turnkeyを使用したLiveCycleES4 SP1からAEM 6.4 Formsへのアップグレード](assets/upgrade-turnkey-livecycle.pdf)

<!--Theses sections used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

## LiveCycle ES3 から JEE 上の AEM 6.4 Forms へのアップグレード {#livecycle-es3-forms-jee}

LiveCycle ES3 から JEE 上の AEM 6.4 Forms へのアップグレードは、アウトオブプレースアップグレードです。このアップグレードでは、旧バージョンのアセットとデータが、サポートされているアプリケーションサーバー、オペレーティングシステム、データベースの新しいインスタンス（新しいバージョン）に移行されます。

既存の LiveCycle ES3 サーバーを AEM 6.4 Forms にアップグレードするための概要的な手順を以下に示します。詳しい手順については、このセクションの最後に記載されているドキュメントを参照してください。

1. アップグレードの準備:

   1. JEE 上の AEM 6.4 Forms のインストーラーを、[アドビライセンス Web サイト（LWS）](https://licensing.adobe.com/)からダウンロードします。インストーラーをダウンロードするには、有効なメンテナンス＆サポートの契約が必要です。
   1. 使用するコンテンツリポジトリ（CRX リポジトリ）タイプを選択します。JEE 上の AEM Forms のごく一部の機能でのみ、コンテンツリポジトリの永続化機能を使用してコンテンツとアセットが保管されます。JEE上のAEM Forms機能を使用する予定の場合のみ、Content Repositoryをインストールして設定します。

      * AEM Forms では、Adaptive Forms、Correspondence Management、HTML5 Forms、Forms Portal、HTML Workspace、Process Reporting、OSGi 上の Forms 中心ワークフローの各機能で、コンテンツリポジトリが使用されます。これらの機能でAEM Formsを使用する予定がある場合は、コンテンツリポジトリが必要です。
      * AEM Forms Document Security用のコンテンツリポジトリは不要です。

      また、LiveCycle と AEM Forms では、リポジトリタイプが異なります。使用可能なリポジトリのタイプと関連情報については、[AEM Formsのインストールに永続性タイプを選択する](/help/forms/using/choosing-persistence-type-for-aem-forms.md)を参照してください。

   1. LiveCycleES3データベース、グローバルデータストレージ(GDS)、およびコンテンツリポジトリ（Document Securityには不要）のバックアップを作成します。 MongoMK パーシスタンスまたは RDBMK パーシスタンスにアップグレードする場合は、LiveCycle ES3 の通信管理アセットをアーカイブとして書き出します。
   1. アプリケーションサーバー、データベース、オペレーティングシステム、Adobe Acrobat、サードパーティアプリケーション、ハードウェアから構成される既存のプラットフォームが、JEE 上の AEM 6.4 Forms でサポートされているかどうかを確認します。サポート対象のハードウェアおよびソフトウェアについては、「[サポートされているプラットフォームの組み合わせ](/help/forms/using/aem-forms-jee-supported-platforms.md)」ドキュメントを参照してください。

      データベースの新しいインスタンスを作成する場合、手順 3 でバックアップしたデータをデータベースに読み込みます。データをデータベースに読み込む方法については、該当するデータベースベンダーのドキュメントを参照してください。

      >[!NOTE]
      >
      >RDBMK 永続性フォーマットを使用している場合、JEE 上の AEM Forms で実行されているリポジトリ永続化とドキュメントサービスの両方に単一のデータベースを使用します。


1. 以下の手順でアップグレードを実行します。

   1. インストーラーを実行して、JEE 上の AEM 6.4 Forms を新しいサーバーにインストールします。インストーラーを実行すると、必要なすべてのファイルが、使用するコンピューター上の 1 つのインストールディレクトリ構造内に配置されます。
   1. インストールが完了したら、**Configuration Manager** を実行して、各種の AEM Forms モジュールを適切に設定します。設定のほかに、グローバルデータストレージ(GDS)とcrx-repositoryのパスを指定できます。

      >[!NOTE]
      >
      >アップグレードタスクの選択画面で、「Adobe Experience Manager Forms 6.2.0からのアップグレード&#x200B;**** 」オプションを選択します。 「**[!UICONTROL Adobe Experience Manager Forms 6.2.0]**&#x200B;からアップグレード」オプションを使用すると、Configuration ManagerでLiveCycleES3からAEM 6.4 Formsにアップグレードできます。

   1. CRX リポジトリをアップグレードして AEM 6.4 Forms サーバーに読み込みます（AEM Forms ドキュメントセキュリティモジュールの場合は、この操作を実行する必要はありません）。

      >[!NOTE]
      >
      >CRX リポジトリのアップグレードとリポジトリ内のコンテンツの移行が完了したら、管理者アカウントのパスワードを変更します。詳しい手順については、「[既存ユーザーのパスワードの変更](/help/sites-administering/granite-user-group-admin.md)」を参照してください。
1. デプロイメント後のタスクを実行して、ログイン資格情報の検証、ドキュメントサービスの設定、通信の管理、ドキュメントセキュリティの設定などを行います（使用するユースケースに応じて、必要な作業を行ってください）。
1. サーバーが正常にアップグレードされているかどうかの確認:

   いくつかの一般的な操作をアップグレード後の AEM Forms サーバーで実行し、サーバーが正しくアップグレードされていることを確認します。例えば、移行後のいくつかのフォームで入力を行ったり、ドキュメントの保護を行うことにより、正しくアップグレードされているかどうかを確認することができます。

   >[!NOTE]
   >
   >AEM 6.4 Forms では crx-repository の構造が変更されています。AEM 6.4 Forms にアップグレードしたあと、新規作成するカスタマイズについては、変更後のパスを使用してください。変更後のパスの一覧については、「[AEM 6.4 Forms におけるリポジトリの再構築](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md)」を参照してください。

**現在の環境とアプリケーションサーバーに応じて、以下に示すいずれかのドキュメントに記載されている手順を実行します。**

* [LiveCycle ES3 から AEM 6.4 Forms へのアップグレード（JBoss 版）](assets/upgrade-jboss-livecycle-es3.pdf)
* [WebLogic版LiveCycleES3からAEM 6.4 Formsへのアップグレード](assets/upgrade-weblogic-livecycle-es3.pdf)
* [LiveCycleES3からAEM 6.4 Formsへのアップグレード（WebSphere版）](assets/upgrade-websphere-livecycle-es3.pdf)
* [JBoss Turnkeyを使用したLiveCycleES3からAEM 6.4 Formsへのアップグレード](assets/upgrade-turnkey-livecycle-es3.pdf)
