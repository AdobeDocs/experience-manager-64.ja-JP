---
title: ディレクトリの同期
seo-title: Synchronizing directories
description: 手動またはスケジュールされた同期を使用して、User Management データベースをソースディレクトリサーバーに対する変更と同期する方法を説明します。
seo-description: Learn how to synchronize the User Management database with changes to the source directory servers using manual or scheduled synchronization.
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
exl-id: d6b2f389-bff4-481d-93bf-87f56114a91b
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 12%

---

# ディレクトリの同期 {#synchronizing-directories}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ドメインを同期するには、手動で同期するか、スケジュールに沿って同期するかを選択します。 A *手動同期* 選択したドメインを同期します。 A *予定同期* はすべてのドメインを同期します。

ディレクトリの同期を使用して、ディレクトリ設定で指定したディレクトリサーバーから詳細を User Management データベースに取り込みます。 後で、ディレクトリサーバーで変更や更新が発生した場合は、手動で同期を実行することもできます。 例えば、ユーザーとグループが追加された場合や、ユーザーのアカウントに変更が加えられた場合に、手動で同期を実行できます。

また、User Management データベースをソース・ディレクトリ・サーバーに対する変更や更新と自動的に同期する、毎日の同期スケジュールを設定することもできます。 ただし、このプロセスではネットワークおよびサーバーのリソースが使用されることに注意してください。 使用率の低い期間を選択し、システムおよびネットワークリソースを結び付ける不要な同期をスケジュールしないようにします。 不要な同期を最小限に抑えるには、代わりに即時同期オプションを使用します。

>[!NOTE]
>
>LDAP ディレクトリの同期が進行中の間に、複数のローカルユーザーおよびグループを作成しないでください。 この処理を試みると、エラーが発生します。

>[!NOTE]
>
>ドメインの同期プロセスが中断された場合（プロセス中にアプリケーションサーバーがシャットダウンされた場合など）は、ドメインの同期を試みる前に待ちます。 同期の状態を評価するには、状態を確認します。 User Management がシャットダウン前にロックを取得した場合は、サーバーの再起動後にロックが解除されるまで 10 分待ちます。 同期ステータスが「処理中」で、同期が中断または停止されている場合、User Management は 3 分後に同期を再試行します。 3 回失敗した後、User Management は同期の失敗を宣言し、ロックを解除します。

>[!NOTE]
>
>Adobe®LiveCycle® Content Services ES（非推奨）は、LiveCycleと共にインストールされるコンテンツ管理システムです。 これにより、ユーザーは人間中心のプロセスを設計、管理、監視、最適化できます。 Content Services（非推奨）のサポートは12/31/2014で終了します。 [アドビ製品のライフサイクルに関するドキュメント](https://www.adobe.com/jp/support/products/enterprise/eol/eol_matrix.html)を参照してください。

## 差分ディレクトリ同期の有効化 {#enable-delta-directory-synchronization}

差分ディレクトリの同期により、ディレクトリの同期の効率が向上します。 差分ディレクトリ同期が有効な場合、User Management は前回の同期以降に追加または更新されたユーザーとグループのみを同期します。

差分ディレクトリ同期が有効な場合、User Management は次の手順を実行します。

* ディレクトリサーバーからすべてのユーザーを取得しますが、タイムスタンプが変更されたユーザーのみを使用して User Management データベースを更新します。
* すべてのグループを取得しますが、タイムスタンプが変更されたグループのみを使用して User Management データベースを更新します。
* タイムスタンプが変更されたグループのグループメンバーのみを取得し、その情報を使用して User Management データベースを更新します。

>[!NOTE]
>
>ディレクトリから削除されたユーザーとグループは、完全なディレクトリ同期を実行するまで、User Management データベースから削除されません。

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 「差分同期」で、チェックボックスを選択し、「保存」をクリックします。
1. 差分ディレクトリ同期機能を使用する各エンタープライズドメインのディレクトリ設定を編集します。 ユーザー設定ページとグループ設定ページで、「タイムスタンプを変更」設定を見つけ、値として `modify TimeStamp` を入力します。エンタープライズドメインの編集について詳しくは、 [既存のドメインの編集と変換](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## 同期中に詳細ログを有効または無効にします {#enable-or-disable-detailed-logging-during-synchronization}

デフォルトでは、User Management は、同期プロセス中に詳細な統計情報をログに記録します。

1. 管理コンソールで、設定／User Management／設定／システム属性の詳細設定をクリックしてください。
1. 「同期統計ログ」で、詳細なログを無効にする場合はこのチェックボックスの選択を解除し、ログを有効にする場合はこのチェックボックスを選択して、「保存」をクリックします。

## ディレクトリ同期再試行オプションの設定 {#configure-the-directory-synchronization-retry-option}

User Management を設定して、失敗したディレクトリ同期の試行を定期的に確認できます。 その後、User Management は、失敗した同期の完了を試みます。

1. 管理コンソールで、設定／User Management／設定／システム属性の詳細設定をクリックしてください。
1. 「同期完了の Cron 形式」で、User Management が失敗した同期を再試行する間隔を表す Cron 形式を入力します。 Cron 式の使用方法は、Quartz オープンソースジョブスケジューリングシステムのバージョン 1.4.0 に基づいています。

   デフォルトは 0 0/13 &amp;ast; ? &amp;ast;、この設定ではチェックが 13 分ごとに実行されます。

## 手動でのディレクトリの同期 {#manually-synchronize-directories}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. （オプション）ユーザーおよびグループの情報を Content Services（非推奨）にプッシュするには、「このオプションを選択して、ユーザーおよびグループを登録済みの外部プリンシパルストレージプロバイダーにプッシュします」オプションを選択します。 このオプションは、ユーザーとグループページで新しいユーザーとグループを追加する場合にも適用されます。
1. 同期する各エンタープライズドメインのチェックボックスを選択し、「今すぐ同期」をクリックします。

   複数のドメインを選択した場合、すべてのドメインのドメイン同期を同時に実行できます。 ただし、ドメインを個別に選択した場合、一度に実行できるドメイン同期は 1 つだけです。

## ディレクトリの同期をスケジュール {#schedule-directory-synchronization}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 同期をスケジュール：

   * 毎日の自動同期を有効にするには、[ スケジューラ ] で [ 発生 ] を選択します。 リストから「毎日」を選択し、時刻を 24 時間形式で対応するボックスに入力します。 設定を保存すると、この値は Cron 式に変換され、「Cron 式」ボックスに表示されます。
   * 特定の曜日や月の特定の日に同期をスケジュールする場合、または特定の月に同期をスケジュールする場合は、「 Cron 式」を選択し、ボックスに適切な式を入力します。 例えば、月の最後の金曜日の午前 1 時 30 分に同期します。

Cron 式の使用方法は、Quartz オープンソースジョブスケジューリングシステムのバージョン 1.4.0 に基づいています。

* 自動同期を無効にするには、「発生」を選択し、リストから「なし」を選択します。
* （オプション）ユーザーおよびグループの情報を Content Services（非推奨）にプッシュするには、「このオプションを選択して、ユーザーおよびグループを登録済みの外部プリンシパルストレージプロバイダーにプッシュします」オプションを選択します。 このオプションは、ユーザーとグループページで新しいユーザーとグループを追加する場合にも適用されます。
* 「保存」をクリックします。

## 現在進行中のディレクトリ同期をすべて停止 {#stop-all-directory-synchronizations-currently-in-progress}

1. 管理コンソールで、設定／User Management／ドメインの管理をクリックします。
1. 「中止」をクリックします。 このボタンは、ディレクトリの同期が進行中の場合にのみ表示されます。
