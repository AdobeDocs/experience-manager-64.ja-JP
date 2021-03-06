---
title: アーカイブの読み込みと管理
seo-title: Import and manage archives
description: アーカイブの読み込みと管理の方法について説明します。
seo-description: Learn how to import and manage archives.
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
exl-id: 12183806-5e00-46e8-bf25-5379a07a56a4
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 100%

---

# アーカイブの読み込みと管理 {#import-and-manage-archives}

Workbench で作成した LCA の読み込みと管理を行うには、「アーカイブ」タブを使用します。

## アーカイブの読み込み {#import-an-archive}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／アプリケーションの管理をクリックし、「アーカイブ」タブをクリックします。
1. 「読み込み」をクリックします。
1. 「参照」をクリックして読み込むアーカイブを選択し、「プレビュー」をクリックします。
1. アーカイブでインストールされるリソースとオブジェクトのリストを確認します。取り消し機能はないので、既存のリソース、オブジェクトおよびサービス設定との競合がないことを確認してください。

   サービス設定の読み込みを選択すると、AEM Forms では、LCA のプロセスで使用されるすべてのプロセス設定ファイル（エンドポイント、セキュリティプロファイルおよびサービス設定パラメーター）が読み込まれます。

1. 「読み込み」をクリックします。
1. 読み込み結果を確認し、「設定をスキップ」をクリックして読み込みプロセスを終了するか、「設定」をクリックしてアーカイブを設定します。

   >[!NOTE]
   >
   >「設定をスキップ」をクリックした場合でも、後でアーカイブを設定できます。

1. 「設定」をクリックすると、エンドポイントを設定ページが表示され、次のような必要な変更を行うことができます。

   * エンドポイントの名前を変更するか、または説明を編集するには、該当するエンドポイントをクリックします。
   * タスクマネージャーエンドポイントを追加するには、「TaskManager を追加」をクリックします。タスクマネージャーの設定について詳しくは、[タスクマネージャーエンドポイントの設定](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)を参照してください。
   * 監視フォルダーエンドポイントを追加するには、「WatchedFolder を追加」をクリックします。監視フォルダーの設定について詳しくは、[監視フォルダーエンドポイントの設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)を参照してください。
   * 電子メールエンドポイントを追加するには、「電子メールを追加」をクリックします。電子メールの設定について詳しくは、[電子メールエンドポイントの設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)を参照してください。
   * EJB エンドポイントを追加するには、「EJB を追加」をクリックし、エンドポイントの名前と説明を指定します。
   * SOAP エンドポイントを追加するには、「SOAP を追加」をクリックし、エンドポイントの名前と説明を指定します。
   * リモートエンドポイントを追加するには、「リモートを追加」をクリックします。Remoting の設定について詳しくは、[リモートエンドポイントの設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)を参照してください。
   * REST エンドポイントを追加するには、「REST を追加」をクリックし、エンドポイントの名前と説明を指定します。REST 呼び出し URL が REST エンドポイントを追加ページに表示されます。
   * エンドポイントを削除するには、エンドポイントの横にあるチェックボックスを選択し、「削除」をクリックします。

1. 「次へ」をクリックします。
1. LCA 内のプロセスまたはサービスに設定パラメーターがある場合は、パラメーターを設定ページが表示されます。ここでサービスパラメーターを設定し、「次へ」をクリックします。
1. セキュリティプロファイルを設定ページで、必要な変更を行います。

   * **呼び出し元の認証が必要：**&#x200B;この設定は、サービスを呼び出すときに認証情報が必要かどうかを示します。

      「*現在、呼び出し元は認証が必要です*」と表示される場合は、サービスの呼び出し元に認証が必要であり、その呼び出し元のユーザープリンシパルにはサービスを呼び出す権限が必要です。そうでないと、呼び出しは拒否されます。認証を不要にするには、「未認証呼び出し元を許可する」をクリックします。

      「*呼び出し元は認証が不要です*」と表示される場合は、サービスの呼び出し元は認証されていなくても構いません。認証チェックがないので、サービスの呼び出しは常に成功します。認証を必要にするには、「呼び出し元の認証が必要」をクリックします。

   * **実行ユーザー：**&#x200B;呼び出し後のサービスで使用する実行時 ID を指定します。このオプションを変更するには、「変更」をクリックします。次のいずれかのオプションを選択します。

      **未指定：**&#x200B;デフォルトの動作を使用します。

      **呼び出し元：**&#x200B;サービスを呼び出したユーザーと同じ ID を使用します。

      **システム：**&#x200B;フルコントロールでサービスを実行します。これは、長期間有効なプロセスのデフォルト設定です。

      **指定したユーザー：**&#x200B;ある特定のユーザーとしてサービスを実行できます。これは、短時間のみ有効なプロセスのデフォルト設定です。このオプションを選択する場合、「ユーザーを選択」をクリックすると、プリンシパルを選択ページが表示され、ユーザーを検索して選択することができます。

   * セキュリティプロファイルにプリンシパルを追加するには、「プリンシパルを追加」をクリックしてから、プリンシパルとして追加するユーザーまたはグループを選択します。「次へ」をクリックして、このプリンシパルに割り当てる権限を選択します。

      **INVOKE_PERM：**&#x200B;サービスのすべての操作を呼び出します。

      **MODIFY_CONFIG_PERM：**&#x200B;サービスの設定を変更します。

      **SUPERVISOR_PERM：**&#x200B;サービスに対してプロセスから作成されたプロセスインスタンスデータを表示します。

      **START_STOP_PERM：**&#x200B;サービスを開始および停止します。

      **ADD_REMOVE_ENDPOINTS_PERM：**&#x200B;サービスのエンドポイントを追加、削除、変更します。

      **CREATE_VERSION_PERM：**&#x200B;サービスの新しいバージョンを作成します。

      **DELETE_VERSION_PERM：**&#x200B;サービスのバージョンを削除します。

      **MODIFY_VERSION_PERM：**&#x200B;サービスのバージョンを変更します。

      **READ_PERM：**&#x200B;サービスを表示します。

      「完了」をクリックして、セキュリティプロファイルにプリンシパルを追加します。

1. 「完了」をクリックして、設定を完了します。

## アーカイブファイルの一部である AEM Forms の設定 {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／アプリケーションの管理をクリックし、「アーカイブ」タブをクリックします。
1. アーカイブの管理ページで、設定するアーカイブファイルを選択します。
1. アーカイブの表示ページで、ハイライト表示されているアーカイブリソースを選択します。
1. 読み込まれたプロセスのアーカイブファイルを設定します。

## 設定ウィザードを使用した、アーカイブファイルの一部である AEM Forms の設定 {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／アプリケーションの管理をクリックし、「アーカイブ」タブをクリックします。
1. 設定するアーカイブファイルの横にある「設定」をクリックします。
1. エンドポイントを設定ページが表示され、必要な変更を行うことができます。

   * エンドポイントの名前を変更するか、または説明を編集するには、該当するエンドポイントをクリックします。
   * タスクマネージャーエンドポイントを追加するには、「TaskManager を追加」をクリックします。タスクマネージャーの設定について詳しくは、[タスクマネージャーエンドポイントの設定](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)を参照してください。
   * 監視フォルダーエンドポイントを追加するには、「WatchedFolder を追加」をクリックします。監視フォルダーの設定について詳しくは、[監視フォルダーエンドポイントの設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)を参照してください。
   * 電子メールエンドポイントを追加するには、「電子メールを追加」をクリックします。電子メールの設定について詳しくは、[電子メールエンドポイントの設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)を参照してください。
   * EJB エンドポイントを追加するには、「EJB を追加」をクリックし、エンドポイントの名前と説明を指定します。
   * SOAP エンドポイントを追加するには、「SOAP を追加」をクリックし、エンドポイントの名前と説明を指定します。
   * リモートエンドポイントを追加するには、「リモートを追加」をクリックします。Remoting の設定について詳しくは、[リモートエンドポイントの設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)を参照してください。
   * REST エンドポイントを追加するには、「REST を追加」をクリックし、エンドポイントの名前と説明を指定します。REST 呼び出し URL が REST エンドポイントを追加ページに表示されます。
   * エンドポイントを削除するには、エンドポイントの横にあるチェックボックスを選択し、「削除」をクリックします。

1. 「次へ」をクリックします。
1. LCA 内のプロセスまたはサービスに設定パラメーターがある場合は、パラメーターを設定ページが表示されます。ここでサービスパラメーターを設定し、「次へ」をクリックします。
1. セキュリティプロファイルを設定ページで、必要な変更を行うことができます。

   * **呼び出し元の認証が必要：**&#x200B;この設定は、サービスを呼び出すときに認証情報が必要かどうかを示します。

      「*現在、呼び出し元は認証が必要です*」と表示される場合は、サービスの呼び出し元に認証が必要であり、その呼び出し元のユーザープリンシパルにはサービスを呼び出す権限が必要です。そうでないと、呼び出しは拒否されます。認証を不要にするには、「未認証呼び出し元を許可する」をクリックします。

      「*呼び出し元は認証が不要です*」と表示される場合は、サービスの呼び出し元は認証されていてもいなくても構いません。認証チェックがないので、サービスの呼び出しは常に成功します。認証を必要にするには、「呼び出し元の認証が必要」をクリックします。

   * **実行ユーザー：**&#x200B;呼び出し後のサービスで使用する実行時 ID を指定します。このオプションを変更するには、「変更」をクリックします。次のいずれかのオプションを選択します。

      **未指定：**&#x200B;デフォルトの動作を使用します。

      **呼び出し元：**&#x200B;サービスを呼び出したユーザーと同じ ID を使用します。

      **システム：**&#x200B;フルコントロールでサービスを実行します。これは、長期間有効なプロセスのデフォルト設定です。

      **指定したユーザー：**&#x200B;ある特定のユーザーとしてサービスを実行できます。これは、短時間のみ有効なプロセスのデフォルト設定です。このオプションを選択する場合、「ユーザーを選択」をクリックすると、プリンシパルを選択ページが表示され、ユーザーを検索して選択することができます。

   * セキュリティプロファイルにプリンシパルを追加するには、「プリンシパルを追加」をクリックしてから、プリンシパルとして追加するユーザーまたはグループを選択します。「次へ」をクリックして、このプリンシパルに割り当てる権限を選択します。

      **INVOKE_PERM：**&#x200B;サービスのすべての操作を呼び出します。

      **MODIFY_CONFIG_PERM：**&#x200B;サービスの設定を変更します。

      **SUPERVISOR_PERM：**&#x200B;サービスに対してプロセスから作成されたプロセスインスタンスデータを表示します。

      **START_STOP_PERM：**&#x200B;サービスを開始および停止します。

      **ADD_REMOVE_ENDPOINTS_PERM：**&#x200B;サービスのエンドポイントを追加、削除、変更します。

      **CREATE_VERSION_PERM：**&#x200B;サービスの新しいバージョンを作成します。

      **DELETE_VERSION_PERM：**&#x200B;サービスのバージョンを削除します。

      **MODIFY_VERSION_PERM：**&#x200B;サービスのバージョンを変更します。

      **READ_PERM：**&#x200B;サービスを表示します。

      「完了」をクリックして、セキュリティプロファイルにプリンシパルを追加します。

## アーカイブの削除 {#remove-an-archive}

>[!NOTE]
>
>サードパーティのリポジトリ（EMC Documentum Content Server、IBM FileNet Content Manager または IBM Content Manager）に格納されているアセットを含むアーカイブを削除するには、Workbench を使用して、リポジトリからもアセットファイルを削除する必要があります。

1. 管理コンソールで、サービス／アプリケーションおよびサービス／アーカイブの管理をクリックします。
1. アーカイブの管理ページで、削除するアーカイブのチェックボックスを選択して、「削除」をクリックします。
