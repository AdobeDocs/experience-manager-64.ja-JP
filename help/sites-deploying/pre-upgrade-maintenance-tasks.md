---
title: アップグレード前のメンテナンスタスク
seo-title: Pre-Upgrade Maintenance Tasks
description: AEMでのアップグレード前のタスクについて説明します。
seo-description: Learn about the pre-upgrade tasks in AEM.
uuid: 6c0d4b31-6464-470b-9e40-1fc2abb9b2a6
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 899ea120-c96d-4dbf-85da-e5d25959d10a
feature: Upgrading
exl-id: f146cb2f-ee77-4c99-8dff-446cdb3a7797
source-git-commit: dd996d0bb856b9140d420d03dec446a382d10acd
workflow-type: tm+mt
source-wordcount: '2168'
ht-degree: 43%

---

# アップグレード前のメンテナンスタスク{#pre-upgrade-maintenance-tasks}

アップグレードを開始する前に、次のメンテナンスタスクに従って、問題が発生した場合にシステムの準備が整い、ロールバックが可能であることを確認することが重要です。

* [十分なディスク領域の確保](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [AEM の完全なバックアップ](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [/etc に対する変更のバックアップ](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [quickstart.properties ファイルの生成](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [ワークフローおよび監査ログのパージの設定](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [アップグレード前のタスクのインストール、設定および実行](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [カスタムログインモジュールの無効化](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [/install ディレクトリからの更新の削除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [すべてのコールドスタンバイインスタンスの停止](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [カスタムのスケジュール済みジョブの無効化](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [オフラインでのリビジョンクリーンアップの実行](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [データストアのガベージコレクションの実行](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [必要に応じてデータベーススキーマをアップグレード](pre-upgrade-maintenance-tasks.md#upgrade-the-database-schema-if-needed)
* [アップグレードの妨げになる可能性のあるユーザーの削除](pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)
* [ログファイルのローテーション](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## 十分なディスク領域の確保 {#ensure-sufficient-disk-space}

アップグレードを実行する際には、コンテンツおよびコードのアップグレードアクティビティに加えて、リポジトリの移行を実行する必要があります。 移行すると、新しい Segment Tar 形式でリポジトリのコピーが作成されます。 その結果、リポジトリのサイズが大きくなる可能性のある 2 つ目のバージョンを保持するのに十分なディスク容量が必要になります。

## AEM の完全なバックアップ {#fully-back-up-aem}

アップグレードを開始する前に、AEMを完全にバックアップする必要があります。 必要に応じて、リポジトリ、アプリケーションのインストール、データストア、Mongo の各インスタンスを必ずバックアップしてください。 AEMインスタンスのバックアップと復元について詳しくは、 [バックアップと復元](/help/sites-administering/backup-and-restore.md).

## /etc に対する変更のバックアップ {#backup-changes-etc}

アップグレードプロセスは、リポジトリの `/apps` パスおよび `/libs` パスの下にある既存のコンテンツおよび設定のメンテナンスやマージに役立ちます。Context Hub 設定など、`/etc` パスに加えられた変更は、多くの場合、アップグレード後に再適用する必要があります。アップグレードにより、マージできない変更のバックアップコピーが `/var` の下に作成されますが、アップグレードを開始する前にこれらの変更を手動でバックアップすることをお勧めします。

## quickstart.properties ファイルの生成 {#generate-quickstart-properties}

jar ファイルから AEM を起動すると、`quickstart.properties` の下に `crx-quickstart/conf` ファイルが生成されます。AEMが以前に開始スクリプトで開始されただけの場合、このファイルは存在せず、アップグレードは失敗します。 このファイルが存在するかどうかを確認し、存在しない場合は jar ファイルからAEMを再起動します。

## ワークフローおよび監査ログのパージの設定 {#configure-wf-audit-purging}

`WorkflowPurgeTask` タスクおよび `com.day.cq.audit.impl.AuditLogMaintenanceTask` タスクには個別の OSGi 設定が必要であり、この設定がない場合は機能しません。アップグレード前のタスクの実行中に失敗した場合は、設定が見つからない可能性が最も高い理由です。 したがって、これらのタスクの OSGi 設定を追加するか、実行しない場合はアップグレード前の最適化タスクリストから完全に削除してください。 ワークフローのパージタスクの設定に関するドキュメントについては、を参照してください。 [ワークフローインスタンスの管理](/help/sites-administering/workflows-administering.md) 監査ログのメンテナンスタスク設定は、次の場所にあります。 [AEM 6 での監査ログのメンテナンス](/help/sites-administering/operations-audit-log.md).

CQ 5.6 でのワークフローおよび監査ログのパージとAEM 6.0 での監査ログのパージについては、 [ワークフローと監査ノードのパージ](https://helpx.adobe.com/jp/experience-manager/kb/howtopurgewf.html).

## アップグレード前のタスクのインストール、設定および実行 {#install-configure-run-pre-upgrade-tasks}

カスタマイズ可能なAEMのレベルにより、通常、環境は一様なアップグレード実行方法に準拠しません。 これにより、アップグレードのための標準化された手順を作成するのが困難になります。

以前のバージョンでは、停止したAEMのアップグレードや、安全に再開できなかったのアップグレードも困難でした。 その結果、完全なアップグレード手順を再開する必要があった場合や、警告を発生させずに不良なアップグレードが実行された場合がありました。

これらの問題に対処するため、Adobeはアップグレードプロセスにいくつかの機能強化を加え、より柔軟でユーザーにとって使いやすいものにしました。 アップグレード前のメンテナンスタスクを手動で実行する必要があった場合は、最適化と自動化が行われています。 また、アップグレード後のレポートが追加され、問題がより簡単に見つかることを期待してプロセスを完全に詳細に調べることができます。

アップグレード前のメンテナンスタスクは、現在、手動で部分的または完全に実行される様々なインターフェイスに分散しています。 AEM 6.3 で導入されたアップグレード前のメンテナンス最適化により、これらのタスクを統合的にトリガーし、その結果をオンデマンドで調べることができます。

アップグレード前の最適化手順に含まれるすべてのタスクは、AEM 6.0 以降のすべてのバージョンと互換性があります。

### 設定方法 {#how-to-set-it-up}

AEM 6.3 以降では、アップグレード前のメンテナンス最適化タスクが quickstart jar に含まれています。 古いバージョンのAEM 6 からアップグレードする場合は、別のパッケージを通じて使用可能になり、パッケージマネージャーからダウンロードできます。

パッケージは次の場所にあります。

* [AEM 6.0 からアップグレードする場合](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [AEM 6.1 からアップグレードする場合](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [AEM 6.2 からアップグレードする場合](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### 使用方法 {#how-to-use-it}

`PreUpgradeTasksMBean` OSGI コンポーネントは、アップグレード前のメンテナンスタスクのリストで事前設定されており、それらのすべてのタスクを一度に実行できます。以下の手順に従ってタスクを設定できます。

1. Web コンソールに移動するには、 `https://serveraddress:serverport/system/console/configMgr`

1. 「**preupgradetasks**」を検索し、最初に一致したコンポーネントをクリックします。コンポーネントのフルネームは、`com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl` です。

1. 次に示すように、実行が必要なメンテナンスタスクのリストを変更します。

   ![1487758925984](assets/1487758925984.png)

タスクリストは、インスタンスの開始に使用される実行モードに応じて異なります。 以下に、各メンテナンスタスクが設計された実行モードの説明を示します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>タスク</strong></td> 
   <td><strong>実行モード</strong></td> 
   <td><strong>メモ</strong></td> 
  </tr> 
  <tr> 
   <td><code>TarIndexMergeTask</code></td> 
   <td>crx2</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td><code>DataStoreGarbageCollectionTask</code></td> 
   <td>crx2</td> 
   <td>マークとスイープを実行します。 共有データストアの場合は、このステップを削除し、次を実行します。<br /> を手動で、または適切にインスタンスを準備してから実行してください。</td> 
  </tr> 
  <tr> 
   <td><code>ConsistencyCheckTask</code></td> 
   <td>crx2</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td><code>WorkflowPurgeTask</code></td> 
   <td>crx2/crx3</td> 
   <td>実行する前に、Adobe「Granite Workflow Purge Configuration」OSGi を設定する必要があります。</td> 
  </tr> 
  <tr> 
   <td><code>GenerateBundlesListFileTask</code></td> 
   <td>crx2/crx3</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td><code>RevisionCleanupTask</code></td> 
   <td>crx3</td> 
   <td>AEM 6.0 から 6.2 の TarMK インスタンスの場合は、代わりにオフラインでのリビジョンクリーンアップを手動で実行します。</td> 
  </tr> 
  <tr> 
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td> 
   <td>crx3</td> 
   <td>実行する前に、 Audit Log Purge Scheduler OSGi 設定を設定する必要があります。</td> 
  </tr> 
 </tbody> 
</table>

>[!CAUTION]
>
>`DataStoreGarbageCollectionTask` を使用する場合、マークアンドスイープフェーズでデータストアガベージコレクション操作を呼び出します。共有データストアを使用するデプロイメントでは、再設定するか正しく準備するか、別のインスタンスが参照する項目が削除されないようにインスタンスを準備します。 このアップグレード前のタスクをトリガーする前に、すべてのインスタンスに対して手動でマークフェーズを実行する必要が生じる場合があります。

### アップグレード前のヘルスチェックのデフォルト設定 {#default-configuration-of-the-pre-upgrade-health-checks}

`PreUpgradeTasksMBeanImpl` OSGI コンポーネントは、`runAllPreUpgradeHealthChecks` メソッドが呼び出されたときに実行されるアップグレード前のヘルスチェックタグのリストで事前設定されています。

* **システム** - granite のメンテナンスヘルスチェックで使用されるタグ

* **アップグレード前**  — アップグレード前に実行するように設定できるすべてのヘルスチェックに追加できるカスタムタグです。

リストは編集可能です。 プラス記号は **(+)** およびマイナス **(-)** タグの横にあるボタンを使用して、カスタムタグを追加したり、デフォルトのタグを削除したりできます。

**MBean メソッド**

管理 Bean 機能には、 [JMX コンソール](/help/sites-administering/jmx-console.md).

MBean にアクセスするには、次の方法があります。

1. JMX コンソール（*https://serveraddress:serverport/system/console/jmx*）に移動
1. 「**PreUpgradeTasks**」を検索し、結果をクリックします。

1. 「**操作**」セクションからメソッドを選択し、次のウィンドウで「**呼び出し**」を選択します。

`PreUpgradeTasksMBeanImpl` によって公開されている使用可能なすべてのメソッドのリストを以下に示します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>メソッド名</strong></td> 
   <td><strong>タイプ</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td><code>getAvailablePreUpgradeTasksNames()</code></td> 
   <td>INFO</td> 
   <td>使用可能なアップグレード前のメンテナンスタスク名のリストを表示します。</td> 
  </tr> 
  <tr> 
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td> 
   <td>情報</td> 
   <td>アップグレード前のヘルスチェックタグ名のリストを表示します。</td> 
  </tr> 
  <tr> 
   <td><code>runAllPreUpgradeTasks()</code></td> 
   <td>アクション</td> 
   <td>リスト内のアップグレード前のメンテナンスタスクをすべて実行します。</td> 
  </tr> 
  <tr> 
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td> 
   <td>アクション</td> 
   <td>指定された名前をパラメーターとして使用して、アップグレード前のメンテナンスタスクを実行します。</td> 
  </tr> 
  <tr> 
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td> 
   <td>ACTION_INFO</td> 
   <td><code>runAllPreUpgradeTasksmaintenance</code> タスクが現在実行されているかどうかを確認します。</td> 
  </tr> 
  <tr> 
   <td><code>getAnyPreUpgradeTaskRunning()</code></td> 
   <td>ACTION_INFO</td> 
   <td>アップグレード前のメンテナンスタスクが現在実行中かどうかを確認し、<br /> 現在実行中のタスクの名前を含む配列を返します。</td> 
  </tr> 
  <tr> 
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td> 
   <td>アクション</td> 
   <td>パラメーターとして指定された名前で、アップグレード前のメンテナンスタスクの正確な実行時間を表示します。</td> 
  </tr> 
  <tr> 
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td> 
   <td>アクション</td> 
   <td>アップグレード前のメンテナンスタスクの最後の実行状態を、パラメーターとして指定された名前で表示します。</td> 
  </tr> 
  <tr> 
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td> 
   <td>アクション</td> 
   <td><p>すべてのアップグレード前のヘルスチェックを実行して、sling ホームパスにある <code>preUpgradeHCStatus.properties</code> というファイルにそれらのステータスを保存します。<code>shutDownOnSuccess</code> パラメーターが <code>true</code> に設定されていると、AEM インスタンスがシャットダウンされますが、これはすべてのアップグレード前のヘルスチェックのステータスが OK の場合のみです。</p> <p>properties ファイルは、今後のアップグレードの前提条件として使用されます<br /> アップグレード前のヘルスチェックが実行された場合、アップグレードプロセスは停止されます<br /> 実行に失敗しました。 アップグレード前の結果を無視する場合<br /> ヘルスチェックを実行して、アップグレードを開始します。このファイルは削除できます。</p> </td> 
  </tr> 
  <tr> 
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td> 
   <td>アクション</td> 
   <td>次の場合に満たされなくなった、インポートされたすべてのパッケージをリストします<br /> 指定したAEMバージョンにアップグレードしています。 対象のAEMのバージョンが<br /> をパラメーターとして指定する。</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>MBean メソッドは、次の場所から呼び出すことができます。
>
>* JMX コンソール
>* JMX に接続する外部アプリケーション
>* cURL
>


## カスタムログインモジュールの無効化 {#disable-custom-login-modules}

>[!NOTE]
>
>この手順は、AEM 5 バージョンからアップグレードする場合にのみ必要です。 古いAEM 6 バージョンからのアップグレードの場合は、完全にスキップできます。

カスタム `LoginModules` がリポジトリレベルで認証設定される方法は、Apache Oak で根本的に変更されました。

CRX2 を使用していた旧バージョンの AEM では、`repository.xml` ファイルで設定をおこないましたが、AEM 6 以降では、web コンソールを使用して、Apache Felix JAAS Configuration Factory サービスで設定をおこないます。

そのため、既存の設定を無効にして、アップグレード後、Apache Oak 用に再作成する必要があります。

`repository.xml` の JAAS 設定で定義したカスタムモジュールを無効にするには、次の例のようにデフォルトの `LoginModule` を利用するように設定を変更する必要があります。

```xml
<Security >
             ....
          <!--
                 Use LoginModule authenticating against repository itself
                 -->
                 <LoginModule class = "com.day.crx.core.CRXLoginModule" >
                     <param name = "anonymousId" value = "anonymous" />
                     <param name = "adminId" value ="admin" />
                     <param name = "disableNTLMAuth" value = "true" />
                     <param name = "tokenExpiration" value = "43200000" />
                     <!-- param name="trust_credentials_attribute" value="d5b9167e95dad6e7d3b5d6fa8df48af8"/
                -->
                 </LoginModule >
         </ Security>
```

>[!NOTE]
>
>詳しくは、[外部ログインモジュールによる認証](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)を参照してください。
>
>AEM 6 での `LoginModule` 設定例については、[AEM 6 での LDAP の設定](/help/sites-administering/ldap-config.md)を参照してください。

## /install ディレクトリからの更新の削除 {#remove-updates-install-directory}

>[!NOTE]
>
>AEMインスタンスをシャットダウンした後に、crx-quickstart/install ディレクトリからパッケージを削除するだけです。 これは、インプレースアップグレード手順を開始する前の最後の手順の 1 つです。

ローカルファイルシステムの `crx-quickstart/install` ディレクトリを介してデプロイされたサービスパック、機能パックまたはホットフィックスを削除します。これにより、更新が完了した後に、新しいAEMバージョン上に古いホットフィックスとサービスパックが誤ってインストールされるのを防ぐことができます。

## すべてのコールドスタンバイインスタンスの停止 {#stop-tarmk-coldstandby-instance}

TarMK コールドスタンバイを使用する場合は、すべてのコールドスタンバイインスタンスを停止します。 これらは、アップグレードで問題が発生した場合に、効率的にオンラインに戻す方法を保証します。 アップグレードが正常に完了したら、アップグレードされたプライマリインスタンスからコールドスタンバイインスタンスを再構築する必要があります。

## カスタムのスケジュール済みジョブの無効化 {#disable-custom-scheduled-jobs}

アプリケーションコードに含まれる OSGi スケジュール済みジョブを無効にします。

## オフラインでのリビジョンクリーンアップの実行 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>この手順は、TarMK インストールでのみ必要です

TarMK を使用する場合は、アップグレードの前にオフラインでのリビジョンクリーンアップを実行する必要があります。 これにより、リポジトリの移行手順とそれ以降のアップグレードタスクの実行がはるかに高速になり、アップグレードが完了した後にオンラインでのリビジョンクリーンアップを正常に実行できるようになります。 オフラインでのリビジョンクリーンアップの実行については、 [オフラインでのリビジョンクリーンアップの実行](https://helpx.adobe.com/experience-manager/6-2/sites-deploying/storage-elements-in-aem-6.html#performing-offline-revision-cleanup).

## データストアのガベージコレクションの実行 {#execute-datastore-garbage-collection}

>[!NOTE]
>
>この手順は、crx3 を実行するインスタンスでのみ必要です

CRX3 インスタンスでリビジョンクリーンアップを実行した後、データストアのガベージコレクションを実行して、データストア内の参照されていない BLOB をすべて削除する必要があります。 手順については、 [データストアのガベージコレクション](/help/sites-administering/data-store-garbage-collection.md).

## アップグレードの妨げになる可能性のあるユーザーの削除 {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>このアップグレード前のメンテナンスタスクは、次の場合にのみ必要です。
>
>* AEM 6.3 より前の AEM バージョンからアップグレードしている
>* アップグレード中に以下に示すエラーが発生した


サービスユーザーが以前の AEM バージョンで、通常のユーザーとして適切にタグ付けされていない場合があります。

この場合、アップグレードは失敗し、次のようなメッセージが表示されます。

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

この問題を回避するには、必ず次の手順を実行してください。

この問題を回避するには、必ず次の手順を実行してください。

* 実稼動トラフィックからインスタンスを分離する
* 問題の原因となるユーザーのバックアップを作成する。バックアップの作成は、パッケージマネージャーから実行できます。詳しくは、 [パッケージの操作方法](/help/sites-administering/package-manager.md).
* 問題の原因となっているユーザーを削除する以下は、このカテゴリに該当する可能性のあるユーザーのリストです。
   * dynamic-media-replication
   * communities-ugc-writer
   * communities-utility-reader
   * communities-user-admin
   * oauthservice
   * sling-scripting

## 必要に応じてデータベーススキーマをアップグレード {#upgrade-the-database-schema-if-needed}

通常、AEM が永続化に使用する基になる Apache Oak スタックは、 必要に応じてデータベーススキーマのアップグレードに対処します。

ただし、スキーマを自動的にアップグレードできない場合が考えられます。これらは、ほとんどの場合、権限が非常に限られたユーザーでデータベースが実行されている高いセキュリティ環境です。 この場合、AEM は引き続き古いスキーマを使用します。

この問題が発生しないようにするには、次の手順に従ってスキーマをアップグレードする必要があります。

1. アップグレードする必要がある AEM インスタンスをシャットダウンします。
1. データベーススキーマをアップグレードします。これを実現するために必要なツールを確認するには、データベースのタイプに関するドキュメントを参照してください。

   Oak でのスキーマのアップグレードの処理方法について詳しくは、Apache Web サイトで[このページ](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade)を参照してください。

1. AEM のアップグレードを続行します。

## ログファイルのローテーション {#rotate-log-files}

アップグレードを開始する前に、現在のログファイルをアーカイブすることをお勧めします。 これにより、アップグレード中およびアップグレード後にログファイルを監視およびスキャンし、発生する可能性のある問題を特定して解決しやすくなります。
