---
title: ロールの作成および設定
seo-title: Creating and configuring roles
description: 既に User Management データベースに含まれている役割にユーザーとグループを関連付ける方法を説明します。 役割の作成、編集、削除もできます。
seo-description: Learn how to associate users and groups with roles that are already part of the User Management database. You can also create, edit, and delete roles.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
exl-id: 794769f8-57c7-43c1-87dd-952121ced3e4
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '2562'
ht-degree: 53%

---

# ロールの作成および設定{#creating-and-configuring-roles}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

User Management Web ページを使用して、既に User Management データベースに含まれている役割にユーザーとグループを関連付けることができます。 役割の作成、編集、削除もできます。

User Management には、次の 2 種類の役割があります。

**可変ロール：**&#x200B;このタイプのロールは編集したり削除したりすることができ、ロール権限の追加や削除を行うことができます。作成したロールはすべて可変ロールと見なされます。 可変ロールに割り当てられたユーザーやグループを追加または削除できます。

**不変ロール：** User Management に含まれているデフォルトのロールは不変ロールです。これらのロールは編集も削除もできません。 ただし、不変ロールに割り当てられたユーザーやグループを追加または削除できます。

可変ロールと不変ロールは、AEM forms API を使用して作成することもできます。

## デフォルトの役割 {#default-roles}

次のデフォルトの役割が User Management データベースに含まれています。

**管理コンソールユーザー：**&#x200B;管理コンソールにアクセスできます。

**アプリケーション管理者：** Workbench のすべての機能を使用できます。管理コンソールのアプリケーションおよびサービスページを使用すると、サービス実行時のプロパティ、エンドポイントおよびセキュリティを設定できます。

**AEM Forms 管理者：**&#x200B;インストールされているすべてのサービスに対して、すべてのタスクを実行できます。

**セキュリティ管理者：** User Management 設定を制御し、任意の User Manager ドメインに関連付けられているユーザーおよびグループを管理します。

**サービスユーザー：**&#x200B;任意のサービスを表示して呼び出すことができます。

**上級管理者：**&#x200B;サービスを含むシステム上のすべての管理機能にアクセスできます。

**トラスト管理者：**&#x200B;管理コンソールの Trust Store の管理ページで管理される PKI 信頼設定および PKI 秘密鍵証明書を管理できます。

### 追加のデフォルトの役割 {#additional-default-roles}

インストールしたAEM forms コンポーネントに応じて、次の追加のデフォルトのロールが含まれる場合があります

**ドキュメントアップロードアプリケーションユーザー：** Flex リモートを使用してドキュメントをアップロードできます。

**Forms 管理者：**&#x200B;管理コンソールの Forms ページの設定を表示して変更できます。

**AEM Forms Contentspace 管理者：**&#x200B;管理コンソールの Content サービス（非推奨）ページの設定を表示して変更できます。

**AEM Forms Contentspace ユーザー：** Contentspace（非推奨）web ページにログインできます。

**Documentum Connector 管理者：**&#x200B;管理コンソールの Connector for EMC Documentum ページの設定を表示して変更できます。

**AEM forms FileNet Connector 管理者：**&#x200B;管理コンソールの IBM FileNet 用 Connector ページの設定を表示して変更できます。

**AEM Forms IBM CM Connector 管理者：** 管理コンソールの IBM Content Manager 用コネクタページの設定を表示して変更できます。

**Rights Management 管理者：**&#x200B;すべてのサーバー設定に関して必要なすべてのタスクを関連する Rights Management ページで実行します。

**Rights Management エ ンドユーザー：** Rights Management のエンドユーザー web ページにアクセスできます。

**Rights Management ユーザー招待：**&#x200B;ユーザーを招待できます。

**Rights Management 招待ユーザーとローカルユーザーの管理：**&#x200B;すべての招待ユーザーおよびローカルユーザーの管理に必要なタスクを、関連する Rights Management ページで実行できます。

**Rights Management ポリシーセット管理者：**&#x200B;すべてのポリシーセットに関して必要なすべてのタスクを、関連する Rights Management ページで実行します。

**Rights Management 上級管理者：**&#x200B;必要なすべてのタスクを Rights Management ページから実行します。

**AEM Forms ワークスペース管理者：**&#x200B;管理コンソールのワークスペースページで設定を表示および変更できます。

***メモ&#x200B;**：AEM Forms のリリースでは Flex Workspace は廃止されています。*

**ワークスペースユーザー：** Workspace エンドユーザーアプリケーションにログインできます。

**Output 管理者：**&#x200B;管理コンソールの Output ページの設定を表示して変更できます。

**PDFG 管理者：**&#x200B;管理コンソールの PDF Generator ページの設定を表示して変更できます。

**PDFG ユーザー：** PDF Generator の管理以外のすべての機能にアクセスできます。

**Acrobat Reader DC Extensions web アプリケーション：** Acrobat Reader DC Extensions web アプリケーションを使用できます。

>[!NOTE]
>
>特定の種類の管理者権限を持つユーザーは、セキュリティ上の理由から、Workspace のエンドユーザー Web ページにアクセスできません。 これらのページはファイアウォールの外に存在する可能性があるので、管理レベルのタスクを許可するとセキュリティ上のリスクが生じる可能性があります。 AEM forms Workspace 管理者またはAEM forms Workspace ユーザーの権限を持つユーザーのみが Workspace エンドユーザー Web ページにアクセスできます。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

## ロールの作成 {#create-a-role}

1. 管理コンソールで、設定/User Management/役割の管理をクリックし、「新しい役割」をクリックします。
1. [ 役割名 ] ボックスに役割の名前を入力し、必要に応じて役割の説明を入力して、[ 次へ ] をクリックします。

   >[!NOTE]
   >
   >MySQL を使用する場合、拡張文字の使用で異なる名前を持つ 2 つのロールを作成することはできません。 例えば、名前が âbcdè の場合に、ロール名が abcde という名前で作成しようとすると、エラーが発生します。

1. 「権限を検索」をクリックし、ロールに追加する権限を選択します。
1. 「 OK 」をクリックし、「次へ」をクリックします。
1. このロールをユーザーおよびグループに割り当てる：

   * 「ユーザー/グループを検索」をクリックします。
   * 「検索」ボックスに検索条件を入力します。
   * 「名前」、「電子メール」または「ユーザー ID」を選択し、「ユーザー」、「グループ」、「ユーザーとグループ」を選択します。
   * ドメインを選択し、表示する結果の数を選択して、「検索」をクリックします。
   * この役割を割り当てるユーザーおよびグループのチェックボックスを選択し、「OK」をクリックします。

1. ユーザーとグループの詳細を表示するには、エンティティを選択します。
1. 「 OK 」をクリックし、「完了」をクリックします。

## ロールの編集 {#edit-a-role}

1. 管理コンソールで、設定/User Management/役割の管理をクリックし、「役割名」をクリックします。

   デフォルトでは、ロールの管理ページには、User Management データベース内のすべてのロールが表示されます。 役割のリストが大きい場合は、ページ上部の「検索」領域を使用して、特定の役割名を検索します。

1. 編集するロールをクリックし、一般設定を編集して、「保存」をクリックします。
1. ロールの権限を編集するには、「権限」タブをクリックし、次のタスクを実行します。

   * 新しい権限を追加するには、[ 権限の検索 ] をクリックし、追加する権限のチェックボックスをオンにして、[OK] をクリックし、[ 保存 ] をクリックします。
   * ロールから権限を削除するには、その権限のチェックボックスをオンにし、[ 削除 ] をクリックして、[ 保存 ] をクリックします。

1. 役割の割り当て先を管理するには、「役割ユーザー」タブをクリックし、次のタスクを実行します。

   * 新しいユーザーおよびグループにロールを割り当てるには、「ユーザーまたはグループを検索」をクリックして、検索情報を入力します。 この役割を割り当てる各ユーザーおよびグループのチェックボックスをオンにし、[OK] をクリックして、[ 保存 ] をクリックします。
   * 役割を削除するには、ユーザーまたはグループのチェックボックスをオンにし、[ 割り当て解除 ] をクリックして、[ 保存 ] をクリックします。

## ロールの削除 {#delete-a-role}

作成した任意のロールを削除できますが、製品に含まれるデフォルトのAEM forms のロールは削除できません。

1. 管理コンソールで、設定/User Management/役割の管理をクリックし、「役割名」をクリックします。

   デフォルトでは、ロールの管理ページには、User Management データベース内のすべてのロールが表示されます。 役割のリストが大きい場合は、ページ上部の「検索」領域を使用して、特定の役割名を検索します。

1. 削除するロールのチェックボックスをオンにし、「削除」をクリックして、「OK」をクリックします。

## ユーザーおよびグループにロールを割り当てる {#assign-a-role-to-users-and-groups}

1. 管理コンソールで、設定／User Management／ユーザーとグループをクリックします。
1. 検索を絞り込むための情報を指定し、「検索」をクリックします。 検索結果がページの下部に表示されます。 任意の列見出しをクリックして、リストを並べ替えることができます。
1. ロールに関連付けるユーザーおよびグループの横のチェックボックスを選択し、「ロールを割り当て」をクリックします。
1. ユーザーまたはグループに割り当てる役割を選択し、「OK」をクリックします。

ロールの管理ページを使用してロールを割り当てることもできます。

## ロールに割り当てられているユーザーの決定 {#determine-who-is-assigned-to-a-role}

1. 管理コンソールで、設定/User Management/役割の管理をクリックし、「役割名」をクリックします。

   デフォルトでは、ロールの管理ページには、User Management データベース内のすべてのロールが表示されます。 役割のリストが大きい場合は、ページ上部の「検索」領域を使用して、特定の役割名を検索します。

1. ロールの詳細ページで、「ロールユーザー」タブをクリックします。 ロールに直接関連付けられているユーザーとグループのリストが表示されます。

## ロールの権限の変更 {#change-role-permissions}

自分で作成した任意のロールの権限を変更できます。 製品に含まれるデフォルトのAEM forms のロールの権限は変更できません。

1. 管理コンソールで、設定/User Management/役割の管理をクリックし、「役割名」をクリックします。

   デフォルトでは、ロールの管理ページには、User Management データベース内のすべてのロールが表示されます。 役割のリストが大きい場合は、ページ上部の「検索」領域を使用して、特定の役割名を検索します。

1. 権限を表示するロールを選択し、「権限」タブをクリックします。
1. これらの権限を変更するには、[ 権限の検索 ] をクリックし、ロールに追加する権限のチェックボックスをオンにして、[OK] をクリックし、[ 保存 ] をクリックします。
1. 権限を削除するには、権限を選択し、「削除」をクリックして、「保存」をクリックします。

### AEM forms の権限 {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM：**&#x200B;サービスのエンドポイントを追加、削除、変更します。

**Admin Console ログイン：**&#x200B;管理コンソールを表示します

**証明書変更：** Trust Store の証明書の信頼設定を変更します

**証明書読み取り：** Trust Store の証明書を読み取ります

**証明書書き込み：** Trust Store に証明書を追加します

**コンポーネント追加：**&#x200B;システムに新しいコンポーネントをインストールします

**コンポーネント削除：** システム内のコンポーネントを削除します

**コンポーネント読み取り：**&#x200B;システム内のコンポーネントを読み取ります

**Contentspace 管理者：** Contentspace（非推奨）管理者の権限

**Contentspace コンソールログイン：** Contentspace（非推奨）コンソールへのログイン権限

**コア設定管理：**&#x200B;管理コンソールのコアシステム設定ページで設定を管理します

**CREATE_VERSION_PERM：**&#x200B;新しいバージョンのサービスを作成します

**資格情報変更：** Trust Store の署名証明書を変更します

**資格情報読み取り：** Trust Store の署名証明書を読み取ります

**資格情報書き込み：** Trust Store に署名証明書を追加します

**CRL 変更：** Trust Store の CRL（証明書失効リスト）を変更します

**CRL 読み取り：** Trust Store の CRL を読み取ります

**CRL 書き込み：** Trust Store に CRL を追加します

**委任：**&#x200B;リソースに ACL を設定します

**DELETE_VERSION_PERM：**&#x200B;サービスのバージョンを削除します

**ドキュメントアップロード：** AEM forms にドキュメントをアップロードします

**ドメイン管理：** User Management ドメインの設定（認証プロバイダーやディレクトリプロバイダーなど）を作成、削除、変更します。

**イベントタイプ編集：**&#x200B;イベントタイプを編集します

**ID 擬装管理：** User Manager で ID を別のユーザーとして実行します

**INVOKE_PERM：**&#x200B;サービスのすべての操作を呼び出します

**LCDS データモデル管理：** Data Services でデータモデルを読み取り、デプロイします

**ライセンスマネージャ更新：** ライセンス情報を更新します

**MODIFY_CONFIG_PERM：**&#x200B;サービスの設定を変更します

**TERM：**&#x200B;サービスのバージョンを変更します

**PDFGAdminPermission：** PDFG 管理者

**PDFGUserPermission：** PDFG ユーザー

**PERM_DCTM_ADMIN：** Documentum Connector 管理者

**PERM_FILENET_ADMIN：** FileNet Connector 管理者

**PERM_FORMS_ADMIN：** Forms 管理者

**PERM_IBMCM_ADMIN：** IBM CM Connector 管理者

**PERM_OUTPUT_ADMIN：** Output 管理者

**PERM_READER_EXTENSIONS_WEB_APPLICATION：** Acrobat Reader DC Extensions web アプリケーションを使用します

**PERM_SP_ADMIN：** SharePoint Connector 設定を管理します

**PERM_WORKSPACE_ADMIN：** Workspace 設定を管理します

**PERM_WORKSPACE_USER：** Workspace エンドユーザーアプリケーションにログインします

**プリンシパル管理：**&#x200B;ドメインのユーザーとグループを管理し、ドメインのユーザーとグループへのロールの割り当てを管理します

**読み取り/削除の記録プロセス：**&#x200B;ワークフローの監査インスタンスをリストアップして取得します

**PROCESS_OWNER_PERM：**&#x200B;プロセスから作成されたサービスに対して、傾向データを表示して管理アクションを実行します

**読み取り：**&#x200B;リソースのコンテンツを読み取ります

**READ_PERM：**&#x200B;サービスの読み取りや表示を行います

**アサーション更新：** User Management でアサーションを更新します

**リポジトリ委任：**&#x200B;リソースに ACL を設定します

**リポジトリ読み取り：**&#x200B;リソースのコンテンツを読み取ります

**リポジトリトラバース：**&#x200B;リソースのリストアップ要求にリソースを含めたり、リソースのメタデータを読み取ったりします

**リポジトリ書き込み：**&#x200B;リポジトリのメタデータとコンテンツを書き込みます

**Rights Management ポリシー所有者変更：** ポリシー所有者を変更します

**Rights Management エンドユーザーコンソールログイン：** Rights Management のエンドユーザー UI にログインします

**Rights Management 設定管理：**&#x200B;サーバー設定を管理します

**Rights Management 招待ユーザー・ローカルユーザー管理：**&#x200B;招待ユーザーとローカルユーザーを管理します

**Rights Management ポリシーセット管理：**&#x200B;ポリシーセット内のすべてのポリシーとドキュメントを管理します

**Rights Management ポリシーセットコーディネーター追加：**&#x200B;ポリシーセットのコーディネーター権限を追加、削除、変更します

**Rights Management ポリシーセットポリシー作成：**&#x200B;ポリシーセットの新しいポリシーを作成します

**Rights Management ポリシーセットポリシー削除：**&#x200B;ポリシーセットからポリシーを削除します

**Rights Management ポリシーセットポリシー編集：**&#x200B;ポリシーセットのポリシーを編集します

**Rights Management ポリシーセットドキュメント発行者管理：**&#x200B;ポリシーセットを作成するには、ユーザーにドキュメント発行者のロールを割り当てます。ドキュメント発行者は、ポリシーでドキュメントを保護するユーザーです。

**Rights Management ポリシーセットコーディネーター削除：**&#x200B;ポリシーセットからポリシーセットコーディネーターを削除します

**Rights Management ポリシーセットドキュメント失効：**&#x200B;ポリシーセット内のドキュメントへのアクセス権を失効させます

**Rights Management ポリシーセットポリシー切り替え：**&#x200B;ドキュメントのポリシーを切り替えます

**Rights Management ポリシーセットドキュメント失効取り消し：**&#x200B;ドキュメントの失効を取り消します

**Rights Management ポリシーセットイベント表示：**&#x200B;ポリシーセット内の任意のポリシーやドキュメントのイベントを表示します

**Rights Management サーバーイベント表示：**&#x200B;すべての監査イベントを検索して表示します

**ロール制御：** User Management でロールを作成、削除、変更します

**サービス有効化** サービスを開始し、呼び出して利用できるようにします

**サービス追加：**&#x200B;新しいサービスをサービスレジストリにデプロイします。新しいプロセスやプロセスのバリアントの追加も含まれます

**サービス無効化：**&#x200B;システム内のサービスを停止します

**サービス削除：**&#x200B;システム内のサービスを削除します。プロセスやプロセスのバリアントも含まれます

**サービス呼び出し** 実行時に利用できる、サービスレジストリ内のサービスを呼び出します

**サービス変更：**&#x200B;システム内のサービスの設定プロパティを変更します。IDE のサービスのロックとロック解除、サービスエンドポイントの追加や削除が含まれます

**サービス読み取り：**&#x200B;システム内のサービスを読み取ります。すべてのプロセスとプロセスのバリアントが含まれます

**SERVICE_AGENT_PERM：**&#x200B;プロセスから作成されたサービスに対して、データを表示してプロセスのインスタンスを操作します

**SERVICE_MANAGER_PERM：**&#x200B;プロセスから作成されたサービスに対して、ロードバランシングなどの管理アクションを実行します

**START_STOP_PERM：**&#x200B;サービスを開始または停止します

**SUPERVISOR_PERM：**&#x200B;プロセスから作成されたサービスに対して、プロセスのインスタンスデータを表示します

**トラバース：**&#x200B;リソースのリストアップ要求にリソースを含めたり、リソースのメタデータを読み取ったりします

**書き込み：**&#x200B;リポジトリのメタデータとコンテンツを書き込みます

**Workbench でファイルを開く**

Workbench で Resources ビューの内容を表示し、表示するファイルを開くには、次の権限が必要です。

* リポジトリ読み取り
* Repository Traverse
* サービス呼び出し
* サービス読み取り

## ロールからユーザーまたはグループを削除する {#remove-a-user-or-group-from-a-role}

ロールの管理ページを使用して、特定のロールからユーザーとグループを削除します。 ユーザーまたはグループがロールアサインを継承した場合、ユーザーまたはグループレベルでロールを削除することはできません。 継承ツリーからユーザーまたはグループを削除するか、親から役割を削除します。

1. 管理コンソールで、設定/User Management/役割の管理をクリックし、「役割名」をクリックします。

   デフォルトでは、ロールの管理ページには、User Management データベース内のすべてのロールが表示されます。 役割のリストが大きい場合は、ページ上部の「検索」領域を使用して、特定の役割名を検索します。

1. 役割のリストで、更新する役割の名前をクリックし、「役割のユーザー」タブをクリックします。 ロールに関連付けられているユーザーとグループのリストが表示されます。
1. ロールから削除するユーザーおよびグループのチェックボックスを選択し、「割り当てを解除」をクリックします。
1. 「保存」をクリックし、「OK」をクリックします。
