---
title: Assets の監視のベストプラクティス
description: 環境とパフォーマンスの監視のベストプラクティス [!DNL Experience Manager] インスタンスをデプロイした後に追加します。
contentOwner: AG
feature: Asset Management
role: Admin,Architect
exl-id: edbb275a-5ead-4ed2-8708-29e766081d75
source-git-commit: 63a4304a1a10f868261eadce74a81148026390b6
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 74%

---

#  Assets の監視に関するベストプラクティスについて説明しています。 {#assets-monitoring-best-practices}

Adobe Experience Manager Assets の観点から見ると、監視には、次のプロセスおよびテクノロジーの観察とレポートを含める必要があります。

* システム CPU
* システムメモリ使用量
* システムディスク IO および IO 待機時間
* システムネットワーク IO
* 以下のための JMX MBean：

   * ヒープ使用状況
   * ワークフローなどの非同期プロセス

* OSGi コンソールヘルスチェック

通常、 [!DNL Assets] は、ライブ監視と長期監視の 2 つの方法で監視できます。

## ライブ監視 {#live-monitoring}

開発のパフォーマンステストの段階、または高負荷な状態になったときに、環境のパフォーマンス特性を把握するためにライブ監視を実行する必要があります。通常、ライブ監視はいくつかのツールを使用して実行します。以下にお勧めのツールを示します。

* [ビジュアル VM](https://visualvm.github.io/):Visual VM を使用すると、CPU 使用量、Java メモリ使用量など、Java VM の詳細情報を表示できます。 また、インスタンス上で実行されるコードをサンプリングおよび評価できます。
* [Top](https://man7.org/linux/man-pages/man1/top.1.html)：Top は、CPU、メモリ、IO 使用量などの使用量統計を表示するダッシュボードを開く Linux コマンドです。インスタンスの状況の概要を示します。
* [Htop](https://hisham.hm/htop/)：Htop は、インタラクティブなプロセスビューアです。Top が提供する情報に加えて、詳細な CPU およびメモリ使用状況が表示されます。Htop は、 `yum install htop` または `apt-get install htop`.

* [Iotop](https://guichaz.free.fr/iotop/)：Iotop は、ディスク IO 使用量の詳細なダッシュボードです。ディスク IO を使用するプロセス、およびそのプロセスによる使用量を示すバーやメーターが表示されます。Iotop は、 `yum install iotop` または `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/)：Iftop は、イーサネット／ネットワークの使用量についての詳細情報を表示します。Iftop では、イーサネットを使用するエンティティについての通信チャネルごとの統計情報、および使用されている帯域幅の量が表示されます。Iftop は、 `yum install iftop` または `apt-get install iftop`.

* Java Flight Recorder（JFR）：非実稼動環境で自由に使用できる、Oracle の市販ツールです。詳しくは、 [Java Flight Recorder を使用して CQ ランタイムの問題を診断する方法](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] の error.log ファイル：システムでログに記録されたエラーの詳細を の error.log ファイルで調査できます。[!DNL Experience Manager]コマンドを使用する `tail -F quickstart/logs/error.log` 調査する必要があるエラーを特定する。
* [ワークフローコンソール](../sites-administering/workflows.md)：ワークフローコンソールを使用して、遅れているワークフローや、停止しているワークフローを監視できます。

通常は、これらのツールを一緒に使用して、 [!DNL Experience Manager] インスタンス。

>[!NOTE]
>
>これらのツールは標準的なツールです。アドビでは直接サポートしません。追加のライセンスは必要ありません。

![chlimage_1-142](assets/chlimage_1-142.png) ![chlimage_1-143](assets/chlimage_1-143.png)

## 長期的監視 {#long-term-monitoring}

の長期監視 [!DNL Experience Manager] インスタンスは、ライブで監視されるのと同じ部分を、より長い期間監視する必要があります。 また、環境に固有のアラートも定義します。

### ログの集約とレポート {#log-aggregation-and-reporting}

Splunk（TM）や Elastic Search/Logstash/Kabana（ELK）など、いくつかのログ集約ツールがあります。の稼動時間を評価するには [!DNL Experience Manager] 例えば、システムに固有のログイベントを理解し、それに基づいてアラートを作成することが重要です。 開発と運用に関する十分な知識を持っていれば、ログ集計プロセスを調整して重要なアラートを生成する方法をより深く理解できます。

### 環境の監視 {#environment-monitoring}

環境の監視には、以下の監視が含まれます。

* ネットワークのスループット
* ディスク IO
* メモリ
* CPU 使用率
* JMX MBean
* 外部 Web サイト

それぞれの項目を監視するには、NewRelic（TM）や AppDynamics（TM）などの外部ツールが必要です。これらのツールを使用して、システム固有のアラート（システム利用率が高い、ワークフローのバックアップ、ヘルスチェック失敗、Web サイトへの不正なアクセスなど）を定義できます。アドビでは、特定のツールを推奨することはありません。ご自身に合ったツールを見つけ、説明した項目の監視に利用してください。

#### 内部アプリケーション監視 {#internal-application-monitoring}

内部アプリケーションの監視には、 [!DNL Experience Manager] プラットフォーム上に構築されたカスタムアプリケーションコードを介して、JVM、コンテンツリポジトリ、監視を含むスタック。 通常、SolarWinds（TM）、HP OpenView（TM）、Hyperic（TM）、Zabbix（TM）などの一般的な多くの監視ソリューションで直接監視できる JMX MBean を通して監視を実行します。JMX への直接接続をサポートしないシステムでは、JMX データを抽出して、それらのシステムがネイティブで理解できる形式で公開するシェルスクリプトを記述できます。

JMX MBean へのリモートアクセスは、デフォルトで無効になっています。JMX を使用した監視について詳しくは、 [JMX テクノロジーを使用した監視と管理](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

多くの場合、統計情報を効果的に監視するにはベースラインが必要です。ベースラインを作成するには、通常の動作条件の下で一定期間システムを監視し、通常の指標を特定します。

**JVM 監視**

Java ベースのアプリケーションスタックと同様に、 [!DNL Experience Manager] は、基になる Java 仮想マシンを通じて提供されるリソースに依存します。 JVM により公開されているプラットフォーム MXBean によって、それらのリソースの多くの状態を監視できます。MXBean について詳しくは、[プラットフォーム MBean サーバーおよびプラットフォーム MXBean の使用](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html)を参照してください。

JVM で監視できるベースラインパラメーターを次に示します。

メモリ

* `MBean: lava.lang:type=Memory`
* URL：*/system/console/jmx/java.lang:type=Memory*
* インスタンス：すべてのサーバー
* アラームしきい値：ヒープまたは非ヒープメモリ使用率が、対応する最大メモリの 75％を超えた場合。
* アラーム定義：システムメモリが不十分である、またはコードにメモリリークがあります。スレッドダンプを分析して、定義を満たすかどうか判断します。

**注意**：この Bean から提供される情報の単位はバイトです。

スレッド

* MBean: `java.lang:type=Threading`
* URL：*/system/console/jmx/java.lang:type=Threading*
* インスタンス：すべてのサーバー
* アラームしきい値：スレッド数がベースラインの 150％を超えた場合。
* アラーム定義：適切に停止できていないアクティブなプロセスがある、または非効率な操作で大量のリソースを消費しています。スレッドダンプを分析して、定義を満たすかどうか判断します。

**[!DNL Experience Manager]監視**

[!DNL Experience Manager] も、JMX を通して一連の統計情報および操作を公開しています。これにより、システムヘルスの評価をおこない、ユーザーに影響を与える前に問題を特定できます。詳しくは、 JMX MBean の[ドキュメント](/help/sites-administering/jmx-console.md)を参照してください。[!DNL Experience Manager]

次に、監視できるベースラインパラメーターを示します [!DNL Experience Manager]:

レプリケーションエージェント

* MBean: `com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>”`
* URL：*/system/console/jmx/com.adobe.granite.replication:type=agent,id=”&lt;AGENT_NAME>”*
* インスタンス：1 つのオーサーインスタンスおよびすべてのパブリッシュインスタンス（フラッシュエージェント）
* アラームしきい値：`QueueBlocked` の値が true、または `QueueNumEntries` の値がベースラインの 150％を超えた場合。

* アラーム定義：システムにブロックされたキューが存在しており、レプリケーションターゲットがダウンしているか、または到達不能であることを示しています。多くの場合、ネットワークまたはインフラストラクチャの問題により過剰なエントリがキューに登録されています。それによってシステムのパフォーマンスに悪影響が生じる可能性があります。

**注意**:MBean および URL パラメーターの場合、 `<AGENT_NAME>` を、監視するレプリケーションエージェントの名前で指定します。

セッションカウンター

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL：*/system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository Statistics&quot;,type*=&quot;RepositoryStats&quot;
* インスタンス：すべてのサーバー
* アラームしきい値：開いているセッションの数がベースラインよりも 50％以上多い場合。
* アラーム定義：特定のコードによりセッションが開かれ、閉じられない状態になっています。この状態は徐々に進行し、最終的にはシステムでメモリリークの原因となります。システム上のセッション数は多少変動しますが、継続的に上昇してはいけません。

ヘルスチェック

[操作ダッシュボード](/help/sites-administering/operations-dashboard.md#health-reports)のヘルスチェックには、監視用の対応する JMX MBean があります。ただし、カスタムのヘルスチェックを記述して、追加のシステム統計情報を公開できます。

監視に役立つ、あらかじめ用意されたヘルスチェックをいくつか示します。

* システムチェック

   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL：*/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck*
   * インスタンス：1 つのオーサーサーバー、およびすべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：いずれかの指標のステータスが警告または重要となっています。問題の原因について詳しくは、ログ属性を確認してください。

* レプリケーションキュー

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL：*/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck*
   * インスタンス：1 つのオーサーサーバー、およびすべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：いずれかの指標のステータスが警告または重要となっています。問題を発生させたキューについて詳しくは、ログ属性を確認してください。

* 応答パフォーマンス

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL：*/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck*
   * インスタンス：すべてのサーバー
   * アラーム期間：ステータスが OK ではない場合。
   * アラーム定義：いずれかの指標のステータスが警告または重要となっています。問題を発生させたキューについて詳しくは、ログ属性を確認してください。

* クエリパフォーマンス

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL：*/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck*
   * インスタンス：1 つのオーサーサーバー、およびすべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：システムで 1 つ以上のクエリの実行速度が遅くなっています。問題を発生させたクエリについて詳しくは、ログ属性を確認してください。

* アクティブなバンドル

   * MBean：org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck
   * URL：*/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck*
   * インスタンス：すべてのサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：システム上の非アクティブまたは未解決な OSGi バンドルの存在。問題を発生させたバンドルについて詳しくは、ログ属性を確認してください。

* ログエラー

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL：*/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck*
   * インスタンス：すべてのサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：ログファイルにエラーがあります。問題の原因について詳しくは、ログ属性を確認してください。

## よくある問題と解決策  {#common-issues-and-resolutions}

監視の過程で問題が発生した場合は、次に、 [!DNL Experience Manager] インスタンス：

* TarMK を使用している場合は、Tar 圧縮を頻繁に実行します。詳しくは、 [リポジトリの保守](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* チェック `OutOfMemoryError` ログ。 詳しくは、[メモリの問題の分析](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)を参照してください。
* ログを確認し、インデックス化されていないクエリ、ツリートラバーサル、インデックストラバーサルへの参照がないかを確認します。これらは、インデックス化されていないクエリ、または不適切にインデックス化されたクエリを示しています。クエリとインデックス作成のパフォーマンスの最適化に関するベストプラクティスについては、 [クエリとインデックスに関するベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* ワークフローが予期したとおりに動作していることを確認するには、ワークフローコンソールを使用します。可能な場合は、複数のワークフローを単一のワークフローにまとめます。
* ライブ監視を再確認し、他にボトルネックがないか、または特定のリソースを大量に使用している箇所がないかを確認します。
* クライアントネットワークからの出力ポイントと、 [!DNL Experience Manager] インスタンスネットワーク（dispatcher を含む）。 多くの場合、これらがボトルネックが発生する領域となります。詳しくは、[Assets のネットワークにおける考慮事項](assets-network-considerations.md)を参照してください。
* のサイズを大きくします [!DNL Experience Manager] サーバー。 サイズが不十分な可能性があります [!DNL Experience Manager] インスタンス。 Adobeカスタマーサポートは、サーバーのサイズが小さいかどうかを特定するのに役立ちます。
* `access.log` および `error.log` ファイルで、不具合の発生した時刻付近のエントリを調査します。カスタムコードの異常の兆候となるパターンを探します。それらを監視するイベントのリストに追加します。
