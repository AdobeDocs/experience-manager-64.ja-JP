---
title: レプリケーションのトラブルシューティング
seo-title: Troubleshooting Replication
description: この記事では、レプリケーションの問題のトラブルシューティング方法に関する情報を提供します。
seo-description: This article provides information on how to troubleshoot replication issues.
uuid: 7c3fdaad-0916-4159-a26c-17ff8c6617fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: configuring
discoiquuid: e862c8a9-b5b6-4857-a154-03d3ffac3e67
feature: Configuring
exl-id: e83317bb-e69c-4e2c-92f8-4f613786e7ae
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 36%

---

# レプリケーションのトラブルシューティング{#troubleshooting-replication}

このページでは、レプリケーションの問題のトラブルシューティング方法に関する情報を提供します。

## 問題 {#problem}

何らかの理由で、レプリケーション（非リバースレプリケーション）が失敗している。

## 解決方法 {#resolution}

レプリケーションが失敗する理由は様々です。 この記事では、これらの問題を分析する際に取る可能性のあるアプローチについて説明します。

**「アクティブ化」ボタンをクリックしたときに、レプリケーションがトリガーされますか。 そうでない場合は、次の操作を行います。**

1. /crx/explorer (CQ5.5) に移動し、管理者としてログインします。
1. 「Content Explorer」を開く
1. ノード/bin/replicate または/bin/replicate.jsonが存在するかどうかを確認します。 ノードが存在する場合は、そのノードを削除して保存します。

**レプリケーションはレプリケーションエージェントキューでキューに入っていますか。**

確認するには、/etc/replication/agents.author.html に移動し、レプリケーションエージェントをクリックします。

**1 つまたは複数のエージェントキューが停止している場合：**

1. キューのステータスには「**ブロック**」と示されていますか。その場合、パブリッシュインスタンスが実行していないか、完全に応答しない状態になっていますか。パブリッシュインスタンスを確認し、何が問題かを調査します。例えば、ログをチェックして、OutOfMemory エラーなどの問題が発生していないかを確認します。単に一般的な遅延が発生している場合は、スレッドダンプを取得して分析します。
1. キューのステータスは「**Queue is active - # pending**」と示されていますか。基本的に、レプリケーションジョブはソケット読み取りにおいて、パブリッシュインスタンスまたは Dispatcher の応答待ちで停止する可能性があります。この場合、パブリッシュインスタンスまたは Dispatcher が高負荷の状態か、ロックによって停止状態になる可能性があります。そのような場合は、オーサーまたはパブリッシュでスレッドダンプを取得してください。

   * スレッドダンプアナライザーでオーサーのスレッドダンプを開き、レプリケーションエージェントの sling イベントジョブが socketRead で停止していないかを確認します。
   * スレッドダンプアナライザーでパブリッシュのスレッドダンプを開き、パブリッシュインスタンスが応答しない原因を分析します。オーサーからレプリケーションを受信するスレッドである POST /bin/receive という名前のスレッドを確認します。

**すべてのエージェントキューが停止している場合**

1. リポジトリの破損などの問題があり、コンテンツの特定の部分を /var/replication/data にシリアライズできない可能性があります。logs/error.log で、関連するエラーがないか確認してください。不正なレプリケーション項目を除去するには、次の操作を行います。

   1. https://に移動します。&lt;host>:&lt;port>/crx にログインし、管理者ユーザーとしてログインします。 CQ5.5 で、https://に移動します。&lt;host>:&lt;port>/crx/explorer を使用します。
   1. 「Content Explorer」をクリックします。
   1. 「Content Explorer」ウィンドウで、ウィンドウの右上にある虫眼鏡のボタンをクリックすると、検索ダイアログがポップアップ表示されます。
   1. 「XPath」ラジオボタンを選択します。
   1. 「Query」ボックスに、次のクエリを入力します。 /jcr:root/var/eventing/jobs//element(&amp;ast;,slingevent:Job) order by @slingevent:created
   1. 「検索」をクリックします。
   1. 結果では、上位の項目は最新の Sling イベンティングジョブです。 それぞれをクリックし、キューの上部に表示される内容に一致する、停止したレプリケーションを見つけます。

1. Sling イベンティングフレームワークのジョブキューに問題がある可能性があります。 /system/console で org.apache.sling.event バンドルを再起動してみてください。
1. ジョブ処理が完全にオフになっている可能性があります。 Sling Eventing Tab の Felix コンソールで確認できます。 「Apache Sling Eventing （JOB PROCESSING が無効になっています。）」と表示されるかどうかを確認します。

   * 有効な場合は、Felix コンソールの「Configuration」タブで「Apache Sling Job Event Handler」をオンにします。 [ ジョブ処理が有効 ] チェックボックスがオフになっている可能性があります。 このオプションをオンにしても「ジョブ処理が無効です」と表示される場合は、ジョブ処理を無効にするオーバーレイが/apps/system/config の下に存在するかどうかを確認します。 boolean 値を true に設定して jobmanager.enabled の osgi:config ノードを作成し、アクティベーションが開始したかどうか、およびキューにジョブがなくなったかどうかを再確認します。

1. また、DefaultJobManager 構成に一貫性のない状態が発生する場合もあります。 この問題は、ユーザーが OSGiconsole で「Apache Sling Job Event Handler」設定を手動で変更した場合に発生する可能性があります（例えば、「Job Processing Enabled」プロパティを無効にして再度有効にし、設定を保存します）。

   * この時点で、crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.configに保存されている DefaultJobManager 設定が不整合な状態になります。 また、「Apache Sling Job Event Handler」プロパティで「Job Processing Enabled」がチェック状態になっている場合でも、「Sling Eventing」タブに移動すると、「JOB PROCESSING IS DISABLED」というメッセージが表示され、レプリケーションは機能しません。
   * この問題を解決するには、OSGi コンソールの「Configuration」ページに移動して、「Apache Sling Job Event Handler」設定を削除する必要があります。次に、クラスターのマスターノードを再起動して、設定を整合性のある状態に戻します。この操作によって問題が修正され、レプリケーションが再び動作を開始します。

**replication.log の作成**

すべてのレプリケーションログを別のログファイルの DEBUG レベルで追加するように設定すると非常に役立つ場合があります。 次の手順を実行します。

1. に移動します。 `https://host:port/system/console/configMgr` 管理者としてログインします。
1. Apache Sling Logging Logger ファクトリを探して、ファクトリ設定の右側の「**+**」ボタンをクリックしてインスタンスを作成します。新しいログロガーが作成されます。
1. 次のように設定します。

   * ログレベル：DEBUG
   * ログファイルのパス： *（CQ5.4 および 5.3）* ../logs/replication.log *(CQ5.5)* logs/replication.log
   * カテゴリ：com.day.cq.replication

1. 問題が何らかの形で sling eventing/jobs に関連していると思われる場合は、次のカテゴリにこの java パッケージを追加することもできます。org.apache.sling.event

### レプリケーションエージェントキューを一時停止中  {#pausing-replication-agent-queue}

オーサーシステムの負荷を減らすために、無効にせずにレプリケーションキューを一時停止するのが適している場合があります。 現在、これは、無効なポートを一時的に設定するハッキングによってのみ可能です。 5.4 以降では、レプリケーションエージェントキューに一時停止ボタンが表示されるようになりましたが、いくつかの制限があります

1. 状態は保持されません。つまり、サーバーまたはレプリケーションバンドルを再起動すると、実行状態に戻ります。
1. 一時停止は、より短い期間（他のスレッドによるレプリケーションを使用するアクティビティがなかった後、OOB 1 時間）アイドル状態で、長時間はアイドル状態になりません。 スレッドがアイドル状態になるのを避ける機能が sling に存在するからです。 基本的に、ジョブキュースレッドが長時間使用されていないかどうかを確認します。使用している場合は、クリーンアップサイクルを開始します。 クリーンアップサイクルにより、スレッドが停止し、一時停止した設定が失われます。 ジョブは永続化されるので、一時停止された設定の詳細を持たないキューを処理するための新しいスレッドを開始します。 このキューは、実行状態に変わります。

### ユーザーアクティベーションでページ権限がレプリケートされません {#page-permissions-are-not-replicated-on-user-activation}

ページ権限は、ユーザーに付与されるのではなく、アクセス権が付与されるノードに保存されるので、レプリケートされません。

一般的に、ページ権限は、オーサーからパブリッシュにレプリケートしないでください。デフォルトではレプリケートされません。 これは、これら 2 つの環境でアクセス権が異なる必要があるためです。 したがって、オーサーとは別に、パブリッシュに ACL を設定することをお勧めします。

### オーサーからパブリッシュに名前空間情報をレプリケートする際にレプリケーションキューがブロックされました {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

オーサーインスタンスからパブリッシュインスタンスに名前空間情報をレプリケートしようとすると、レプリケーションキューがブロックされる場合があります。 これは、レプリケーションユーザーが `jcr:namespaceManagement` 権限を持っていないために起こります。この問題を回避するには、次のことを確認してください。

* レプリケーションユーザー（「[トランスポート](/help/sites-deploying/replication.md#replication-agents-configuration-parameters)」タブ／ユーザーで設定）はパブリッシュインスタンス上にも存在します。
* ユーザーは、コンテンツがインストールされているパスで読み取りと書き込みの権限を持っています。
* ユーザーはリポジトリレベルで `jcr:namespaceManagement` 権限を持っています。次のようにして権限を付与できます。

1. CRX/DE（`http://localhost:4502/crx/de/index.jsp`）に管理者としてログインします。
1. をクリックします。 **アクセス制御** タブをクリックします。
1. 選択 **リポジトリ**.
1. クリック **エントリを追加** （プラスアイコン）。
1. ユーザーの名前を入力します。
1. 権限リストから `jcr:namespaceManagement` を選択します。
1. 「OK」をクリックします。
