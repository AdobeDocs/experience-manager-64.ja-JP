---
title: AEM Forms データのバックアップ
seo-title: Backing up the AEM forms data
description: このドキュメントでは、AEM forms データベース、GDS およびコンテンツ保存場所のルートディレクトリのホットバックアップ（オンラインバックアップ）を完了するために必要な手順について説明します。
seo-description: This document describes the steps that are required to complete a hot, or online, backup of the AEM forms database, the GDS, and Content Storage Root directories.
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
exl-id: d86cf58f-6595-4f37-977f-09437a7f89f9
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1540'
ht-degree: 20%

---

# AEM Forms データのバックアップ {#backing-up-the-aem-forms-data}

ここでは、AEM forms データベース、GDS およびコンテンツ保存場所のルートディレクトリのホットバックアップ（オンラインバックアップ）を完了するために必要な手順について説明します。

AEM forms をインストールして実稼動環境にデプロイした後は、データベース管理者がデータベースの最初の完全バックアップ（コールドバックアップ）を実行する必要があります。 このバックアップを実行するには、データベースをシャットダウンする必要があります。 次に、データベースの差分バックアップまたは増分（またはホット）バックアップを定期的に実行する必要があります。

バックアップとリカバリを正常に実行するには、システムイメージのバックアップを常に使用可能にする必要があります。 その後、損失が発生した場合は、環境全体を一貫性のある状態に回復できます。

GDS、AEMリポジトリ、およびコンテンツ保存場所のルートディレクトリのバックアップと同時にデータベースをバックアップすることで、回復が必要な場合に、これらのシステムを同期し続けることができます。

この節で説明するバックアップ手順では、AEM forms データベース、AEMリポジトリ、GDS およびコンテンツ保存場所のルートディレクトリをバックアップする前に、セーフバックアップモードに入る必要があります。 バックアップが完了したら、セーフバックアップモードを終了する必要があります。 セーフバックアップモードは、GDS 内に存在する長期間有効な永続的なドキュメントをマークするために使用されます。 このモードでは、セーフバックアップモードが解放されるまで、自動ファイルクリーンアップメカニズム（ファイルコレクター）が期限切れのファイルを削除しないようにします。 GDS バックアップとデータベースバックアップの同期を維持する必要があります。

GDS の場所をバックアップする頻度は、AEM forms の使用方法と使用可能なバックアップウィンドウによって異なります。 バックアップウィンドウは、数日間実行される可能性があるので、長期間有効なプロセスの影響を受ける場合があります。 このディレクトリ内のファイルを継続的に変更、追加、削除する場合は、GDS の場所をより頻繁にバックアップする必要があります。

前の節で説明したように、データベースがログ・モードで実行されている場合は、データベース・ログも頻繁にバックアップして、メディアの障害が発生した場合にデータベースのリストアに使用できるようにする必要があります。

>[!NOTE]
>
>参照されていないファイルは、回復プロセスの後で GDS ディレクトリに保持される場合があります。 これは、現時点での既知の制限です。

## データベース、GDS、AEMリポジトリおよびコンテンツ保存場所のルートディレクトリのバックアップ {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

AEM forms は、セーフバックアップ（スナップショット）モードまたはローリングバックアップ（継続的な有効範囲）モードのいずれかにする必要があります。 AEM forms を設定していずれかのバックアップモードに入る前に、次の点を確認してください。

* システムのバージョンを確認し、最後の完全なシステムイメージバックアップの実行後に適用されたパッチまたは更新を記録します。
* ローリングモードまたはスナップショットモードのバックアップを使用する場合は、データベースのホットバックアップを実行できるように、データベースに正しいログ設定が設定されていることを確認します。 ( [AEM forms データベース](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

これらに加えて、バックアップ/復元プロセスに関する次のガイドラインを確認します。

* 使用可能なオペレーティングシステムまたはサードパーティのバックアップユーティリティを使用して、GDS ディレクトリをバックアップします。 ( [GDS の場所](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* （オプション）使用可能なオペレーティングシステムまたはサードパーティのバックアップとユーティリティを使用して、コンテンツ保存場所のルートディレクトリをバックアップします。 ( [コンテンツ保存場所のルートの場所（スタンドアロン環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) または [コンテンツ保存場所のルートの場所（クラスター環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* オーサーインスタンスとパブリッシュインスタンス（ crx -repository バックアップ）をバックアップします。

   Correspondence Management Solution 環境をバックアップするには、オーサーインスタンスとパブリッシュインスタンスで手順を実行します。詳しくは、 [バックアップと復元](/help/sites-administering/backup-and-restore.md).

   オーサーインスタンスとパブリッシュインスタンスをバックアップする際は、次の点を考慮してください。

   * オーサーインスタンスとパブリッシュインスタンスのバックアップが同時に開始するようにしてください。バックアップの実行中は、オーサーインスタンスとパブリッシュインスタンスを引き続き使用できますが、バックアップ中にアセットを公開しないでください。 オーサーインスタンスとパブリッシュインスタンスの両方のバックアップが終了するのを待ってから、新しいアセットを公開します。
   * オーサーノードの完全なバックアップには、Forms Manager とAEM Forms Workspace データのバックアップが含まれます。
   * Workbench 開発者は、引き続きローカルでプロセスを操作できます。 バックアップフェーズ中に新しいプロセスをデプロイしないでください。
   * 各バックアップセッションの長さに関する決定は、AEMフォーム (DB、GDS、AEMリポジトリ、およびその他の追加のカスタムデータ ) のすべてのデータのバックアップに要した合計時間に基づいておこなう必要があります。

トランザクションログを含むAEM forms データベースをバックアップする必要があります。 ( [AEM forms データベース](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) 詳細については、使用するデータベースに適したナレッジベースを参照してください。

* [AEM Forms の Oracle バックアップと回復](https://www.adobe.com/go/kb403624)
* [AEM Forms の MySQL バックアップと回復](https://www.adobe.com/go/kb403625)
* [AEM Forms の Microsoft SQL Server バックアップと回復](https://www.adobe.com/go/kb403623)
* [AEM forms の DB2 バックアップと回復](https://www.adobe.com/go/kb403626)

これらの記事は、データのバックアップと回復に関する基本的なデータベース機能のガイダンスを提供します。 特定のベンダーのデータベースバックアップ/リカバリ機能に関する包括的な技術ガイドとしての意図はありません。 AEM forms アプリケーションデータの信頼性の高いデータベースバックアップ方法を作成するために必要なコマンドの概要を説明します。

>[!NOTE]
>
>GDS のバックアップを開始する前に、データベースのバックアップが完了している必要があります。 データベースのバックアップが完了しない場合、データは同期されません。

### バックアップモードの開始 {#entering-the-backup-modes}

管理コンソール、LCBackupMode コマンド、またはAEM forms のインストールで使用可能な API を使用して、バックアップモードを開始および終了できます。 ローリングバックアップ（継続的なバックアップ）の場合、管理コンソールオプションは使用できません。コマンドラインオプションまたは API を使用する必要があります。 <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>forms サーバーで SSL を設定した場合、LCBackupMode.CMD スクリプトを使用して forms サーバーをバックアップモードにすることはできません。

**管理コンソールを使用したセーフバックアップモードの開始**

1. 管理コンソールにログインします。
1. 設定/コアシステム設定/バックアップユーティリティをクリックします。
1. 「セーフバックアップモードで動作」を選択し、「OK」をクリックします。

   この方法では、AEMフォームが無期限（タイムアウトなし）にバックアップモードになり、ローリングバックアップモードではなくスナップショットモードになります。

**コマンドラインオプションを使用したセーフバックアップモードの開始**

コマンドラインインターフェイスの `LCBackupMode` スクリプトを使用して、AEM Forms をセーフバックアップモードにすることができます。

1. ADOBE_LIVECYCLE を設定し、アプリケーションサーバーを起動します。
1. `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` フォルダーに移動します。
1. オペレーティングシステムに応じて、`LCBackupMode.cmd` または `LCBackupMode.sh` スクリプトを編集して、システムに適合するデフォルト値を指定します。
1. コマンドプロンプトで、次のコマンドを 1 行で実行します。

   * （Windows）`LCBackupMode.cmd enter [-Host=`*ホスト名* `] [-port=`*ポート番号* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `] [-label=`*ラベル名* `] [-timeout=`*秒数* `]`
   * （Linux、UNIX）`LCBackupMode.sh enter [-host=`*ホスト名* `] [-port=`*ポート番号* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `] [-label=`*ラベル名* `]`

   上記のコマンドでは、プレースホルダーは次のように定義されています。

   `Host` は、AEM Forms が実行されているホストの名前です。

   `port` は、AEM Forms が実行されているアプリケーションサーバーの WebService ポートです。

   `user` は、AEM Forms 管理者のユーザー名です。

   `password` は、AEM Forms 管理者のパスワードです。

   `label` は、このバックアップのテキストラベルです（任意の文字列を指定可能）。

   `timeout` は、バックアップモードが自動的に終了するまでの秒数です。0 ～ 10,080 の値を指定できます。 0 （デフォルト）の場合、バックアップモードはタイムアウトしません。

   バックアップモードへのコマンドラインインターフェイスの詳細については、BackupRestoreCommandline ディレクトリの Readme ファイルを参照してください。

### バックアップモードの終了 {#leaving-backup-modes}

バックアップモードを終了するには、管理コンソールまたはコマンドラインオプションを使用できます。

**セーフバックアップモード（スナップショットモード）を終了**

管理コンソールを使用してAEM forms のセーフバックアップモード（スナップショットモード）を解除するには、次のタスクを実行します。

1. 管理コンソールにログインします。
1. 設定/コアシステム設定/バックアップユーティリティをクリックします。
1. 「セーフバックアップモードで動作」の選択を解除し、「OK」をクリックします。

**すべてのバックアップモードを終了**

コマンドラインインターフェイスを使用して、AEM forms をセーフバックアップモード（スナップショットモード）から切り離したり、現在のバックアップモードセッション（ローリングモード）を終了したりできます。 管理コンソールを使用してローリングバックアップモードを終了することはできません。 ローリングバックアップモードの場合、管理コンソールの [ バックアップユーティリティ ] コントロールは無効になります。 API 呼び出しを使用するか、LCBackupMode コマンドを使用する必要があります。

1. `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` フォルダーに移動します。
1. オペレーティングシステムに応じて、`LCBackupMode.cmd` または `LCBackupMode.sh` スクリプトを編集して、システムに適合するデフォルト値を指定します。

   >[!NOTE]
   >
   >JAVA_HOME ディレクトリは、アプリケーション・サーバーの適切な章 ( [AEM forms のインストールの準備](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63_jp)*.*

1. 次のコマンドを 1 行で実行します。

   * （Windows）`LCBackupMode.cmd leaveContinuousCoverage [-Host=`*ホスト名* `] [-port=`*ポート番号* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `]`
   * （Linux、UNIX）`LCBackupMode.sh leaveContinuousCoverage [-Host=`*ホスト名* `] [-port=`*ポート番号* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `]`

      上記のコマンドでは、プレースホルダーは次のように定義されています。

      `Host` は、AEM Forms が実行されているホストの名前です。

      `port` は、AEM Forms が実行されているアプリケーションサーバー上のポートです。

      `user` は、AEM Forms 管理者のユーザー名です。

      `password` は、AEM Forms 管理者のパスワードです。

      `leaveContinuousCoverage` は、ローリングバックアップモードを完全に無効にする場合に使用します。
   >[!NOTE]
   >
   >バックアップモードがオフの場合は、継続的なカバレッジを再確立できません。 その間の変更は保護されません。

   >[!NOTE]
   >
   >データベースでドキュメントの保存を有効にした場合、スナップショットバックアップモードとローリングバックアップモードは使用できません。

   バックアップモードへのコマンドラインインターフェイスの詳細については、BackupRestoreCommandline ディレクトリの readme ファイルを参照してください。
