---
title: AEM 6 での監査ログのメンテナンス
seo-title: Audit Log Maintenance in AEM 6
description: AEM での監査ログのメンテナンスについて説明します。
feature: Operations
seo-description: Lear about Audit Log Maintenance in AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: bcbdab55-4871-4c7f-b82a-b7d8280e82e3
source-git-commit: 40a4e01eea3e20fda6d0b2c8af985f905039e320
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 100%

---

# AEM 6 での監査ログのメンテナンス{#audit-log-maintenance-in-aem}

監査ログの対象となる AEM イベントが発生すると、多くのアーカイブデータが生成されます。このデータは、レプリケーション、アセットのアップロード、およびその他のシステムアクティビティによって、短期間で増大する可能性があります。

「監査ログのメンテナンス」に用意されているいくつかの機能要素を使用すると、特定のポリシー条件に基づいて監査ログのメンテナンスを自動化できます。

設定可能な週別メンテナンスタスクとして実装し、操作ダッシュボード監視コンソールからアクセスできます。

詳しくは、[操作ダッシュボードのドキュメント](/help/sites-administering/operations-dashboard.md)を参照してください。

監査ログのパージオプションには 3 つのタイプがあります。

1. [ページ監査ログのパージの設定](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM 監査ログのパージの設定](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [レプリケーション監査ログのパージの設定](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

それぞれ AEM の web コンソールでルールを作成して設定できます。設定後、**ツール／操作／メンテナンス／週別メンテナンスウィンドウ**&#x200B;に移動して、**監査ログのメンテナンスタスク**&#x200B;でそれらを実行することができます。

## ページ監査ログのパージの設定 {#configure-page-audit-log-purging}

監査ログのパージを設定するには、次の手順に従います。

1. ブラウザーに `http://localhost:4502/system/console/configMgr/` と入力して、web コンソール管理に移動します。

1. 「**ページ監査ログパージルール**」という項目を検索してクリックします。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 次に、要件に従ってパージスケジューラーを設定します。使用できるオプションは以下のとおりです。

   * **Rule name：**&#x200B;監査ポリシールールの名前。
   * **Content path：**&#x200B;ルールが適用されるコンテンツのパス。
   * **Minimum age：**&#x200B;監査ログを保持しておく必要がある日数。
   * **Audit log type：**&#x200B;パージする必要がある監査ログのタイプ。

   >[!NOTE]
   >
   >コンテンツパスは、リポジトリの `/var/audit/com.day.cq.wcm.core.page` ノードの子にのみ適用されます。

1. ルールを保存します。
1. 作成したルールを実行するためには、操作ダッシュボードに公開する必要があります。そのためには、AEM のようこそ画面から&#x200B;**ツール／操作／メンテナンス**&#x200B;に移動します。

1. **週別メンテナンスウィンドウ**&#x200B;カードをクリックします。

1. メンテナンスタスクは、**AuditLog メンテナンスタスク**&#x200B;カードの下に既に存在しています。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 次回実行の日付を調べて設定するか、再生ボタンをクリックして手動で実行できます。

AEM 6.3 では、監査ログのパージタスクが完了する前に、スケジュールされたメンテナンスウィンドウを閉じると、タスクは自動的に停止します。次回のメンテナンスウィンドウを開くと、タスクは再開されます。

**AEM 6.4** で実行中の監査ログのパージタスクを手動で停止するには、「**停止**」アイコンをクリックします。次回の実行時に、タスクは安全に再開されます。

>[!NOTE]
>
>メンテナンスタスクを停止すると、タスクの実行は休止されますが、既に進行しているジョブの監視が途切れることはありません。

## DAM 監査ログのパージの設定 {#configure-dam-audit-log-purging}

1. *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr* にあるシステムコンソールに移動します。
1. **DAM 監査ログのパージ** ルールを探して結果をクリックします。
1. それに従って、次のウィンドウでルールを設定します。オプションは以下のとおりです。

   * **Rule name：**&#x200B;監査ポリシールールの名前。
   * **Content path：**&#x200B;ルールが適用されるコンテンツのパス。
   * **Minimum age：**&#x200B;監査ログを保持しておく必要がある日数。
   * **Audit Log Dam event types：** パージする必要がある DAM 監査イベントの種類。

1. 「**保存**」をクリックして設定を保存します。

## レプリケーション監査ログのパージの設定  {#configure-replication-audit-log-purging}

1. *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr* にあるシステムコンソールに移動します。
1. **レプリケーション監査ログのパージスケジューラー** を探して結果をクリックします。
1. それに従って、次のウィンドウでルールを設定します。オプションは以下のとおりです。

   * **Rule name：**&#x200B;監査ポリシールールの名前。
   * **Content path：**&#x200B;ルールが適用されるコンテンツのパス。
   * **Minimum age：**&#x200B;監査ログを保持しておく必要がある日数。
   * **Audit log Replication event types：**&#x200B;パージする必要があるレプリケーション監査イベントのタイプ。

1. 「**保存**」をクリックして設定を保存します。
