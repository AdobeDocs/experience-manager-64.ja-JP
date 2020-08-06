---
title: コミュニティのユーザーの同期
seo-title: コミュニティのユーザーの同期
description: ユーザーの同期の仕組み
seo-description: ユーザーの同期の仕組み
uuid: 5b9bb7b6-9238-41f6-81da-84b9a303b9e2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 32b56b48-75cb-4cc9-a077-10e335f01a35
translation-type: tm+mt
source-git-commit: 5ddbcb2addff2d6e3a3e9d7e100a6d9ba89fdd60
workflow-type: tm+mt
source-wordcount: '2507'
ht-degree: 22%

---


# コミュニティのユーザーの同期 {#communities-user-synchronization}

## 概要 {#introduction}

In AEM Communities, from the publish environment (depending on permissions configured), *site visitors* may become *members*, create *user groups*, and edit their *member profile*.

*User data* (ユーザーデータ *)は、*&#x200B;ユーザー *、* ユーザープロファイル *、*&#x200B;ユーザーグループを指す用語です。

メンバーという用語は、オーサー環境で登録されたユーザーではなく、パブリッシュ環境で登録されたユーザーを指します。****

ユーザーデータについて詳しくは、[ユーザーとユーザーグループの管理](users.md)を参照してください。

## パブリッシュファーム間のユーザーの同期 {#synchronizing-users-across-a-publish-farm}

仕様上、パブリッシュ環境で作成されたデータは、オーサー環境では表示されません。

オーサー環境で作成されたほとんどのユーザーデータは、オーサー環境に残されたままとなり、パブリッシュインスタンスには同期もレプリケートもされません。

When the [topology](topologies.md) is a [publish farm](../../help/sites-deploying/recommended-deploys.md#tarmk-farm), registration  and  modifications made on one publish instance need to be synchronized with other publish instances. メンバーは、ログインして任意の発行ノードでデータを確認できる必要があります。

ユーザーの同期を有効にすると、ファーム内のパブリッシュインスタンス間でユーザーデータが自動的に同期されます。

### ユーザーの同期のセットアップ手順 {#user-sync-setup-instructions}

詳細なステップバイステップの手順については、以下を参照してください。

* [ユーザーの同期](../../help/sites-administering/sync.md)

## バックグラウンドでのユーザー同期  {#user-sync-in-the-background}

![sling-dist-workflow](assets/sling-dist-workflow.png)

* **VLTパッケージ**: は、発行者に対して行われたすべての変更のzipファイルです。発行者に配布する必要があります。 パブリッシャの変更は、変更イベントリスナーによって選択されたイベントを生成します。 これにより、すべての変更を含むvltパッケージが作成されます。

* **配布パッケージ**: Slingの配布情報が含まれます。 これは、コンテンツの配布が必要な場所、および最後に配布された日時に関する情報です。

## What Happens When ... {#what-happens-when}

### コミュニティのサイトコンソールでのサイトの公開 {#publish-site-from-communities-sites-console}

オーサー環境で、コミュニティサイトを[コミュニティサイトコンソール](sites-console.md)から公開すると、関連するページが[レプリケート](../../help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents)されます。また、Sling によって、動的に作成されたコミュニティユーザーグループ（メンバーシップを含む）が配信されます。

### パブリッシュ環境でのユーザーの作成またはプロファイルの編集 {#user-is-created-or-edits-profile-on-publish}

仕様上、パブリッシュ環境で（自己登録、ソーシャルログイン、LDAP 認証などで）作成されたユーザーやプロファイルはオーサー環境では表示されません。

When the topology is a [publish farm](topologies.md) and user sync has been correctly configured, the *user* and *user profile* is synchronized across the publish farm using Sling distribution.

### パブリッシュ環境での新しいコミュニティグループの作成 {#new-community-group-is-created-on-publish}

発行インスタンスから開始されても、コミュニティグループの作成（新しいサイトページと新しいユーザーグループに結びつく）は、実際には作成者インスタンスで発生します。

このプロセスの一環として、新しいサイトページがすべてのパブリッシュインスタンスにレプリケートされます。動的に作成されるコミュニティユーザーグループとそのメンバーシップは、すべての発行インスタンスに配布されるSlingです。

### セキュリティコンソールでのユーザーまたはユーザーグループの作成 {#users-or-user-groups-are-created-using-security-console}

仕様上、パブリッシュ環境で作成されたユーザーデータは、オーサー環境では表示されません。その反対も同様です。

[ユーザー管理およびセキュリティ](../../help/sites-administering/security.md)コンソールを使用してパブリッシュ環境で新しいユーザーを追加すると、ユーザーの同期機能により、新しいユーザーとそのグループメンバーシップがその他のパブリッシュインスタンスに同期されます（必要な場合）。ユーザー同期は、セキュリティコンソールを使用して作成されたユーザーグループも同期します。

### ユーザーによるパブリッシュ環境でのコンテンツの投稿 {#user-posts-content-on-publish}

ユーザー生成コンテンツ（UGC）に関しては、パブリッシュインスタンスで入力されたデータへのアクセスは、[設定済みの SRP](srp-config.md) を通じておこなわれます。

## ベストプラクティス {#bestpractices}

デフォルトでは、ユーザー同期は&#x200B;**無効**&#x200B;になっています。ユーザー同期を有効にするには、OSGi の既存の&#x200B;**&#x200B;設定を変更する必要があります。ユーザー同期を有効にした結果、新しい設定が追加されることはありません。

ユーザー同期では、オーサー環境で作成されていないユーザーデータでもその配布の管理はオーサー環境に依存します。

**前提条件**

1. If users and user groups have already been created on one publisher, it is recommended to [manually sync](../../help/sites-administering/sync.md#manually-syncing-users-and-user-groups) the user data to all publishers prior to configuring and enabling user sync.

   ユーザー同期を有効にすると、新規に作成されたユーザーおよびグループのみが同期されるようになります。

1. 最新のコードがインストールされていることを確認します。

   * [AEM プラットフォームの更新](https://helpx.adobe.com/jp/experience-manager/kb/aem62-available-hotfixes.html)
   * [AEM Communities の更新](deploy-communities.md#latestfeaturepack)

AEM Communitiesでユーザー同期を有効にするには、次の設定が必要です。 Slingコンテンツの配信が失敗しないように、これらの設定が正しいことを確認します。

### Apache Sling Distribution Agent - Sync Agents Factory {#apache-sling-distribution-agent-sync-agents-factory}

この設定は、発行者間で同期されるコンテンツを取得します。 設定は作成者インスタンスに対して行われます。 作成者は、そこに存在するすべての発行者と、すべての情報をどこで同期するかを追跡する必要があります。

設定のデフォルト値は、単一の発行インスタンスに対するものです。 ユーザー同期は、発行ファームなど複数の発行インスタンスを同期するのに役立つので、追加の発行インスタンスを設定に追加する必要があります。

**コンテンツはどのように同期されますか。**

発行者インスタンスが発行者のエクスポーターエンドポイントにpingを送信します。 特定の発行者(n)に対してユーザーが作成または更新されると(n)、作成者はエクスポーターエンドポイントからコンテンツを取得し、そのコンテンツ [を他の発行者](sync.md#main-pars-image-1413756164) （n-1、つまりコンテンツの取得元とは別の発行者）にプッシュします。

<!--This section used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

### Apache Sling同期エージェントの設定を行うには

AEMオーサーインスタンス：

1. 管理者権限でサインインします。
1. Access the [Web Console](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/configuring-osgi.html).

   For example, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Locate **[!UICONTROL Apache Sling Distribution Agent - Sync Agents Factory]**.

   * 編集用に開く既存の設定を選択します（鉛筆アイコン）。
   * 検証名： **`socialpubsync`.**
   * Select the **[!UICONTROL Enabled]** checkbox.
   * 「 **[!UICONTROL Use Multiple queues]**」を選択します。
   * 「 **[!UICONTROL エクスポーターエンドポイント]** 」と「 **[!UICONTROL インポーターエンドポイント」を指定します]** （エクスポーターエンドポイントとインポーターエンドポイントをさらに追加できます）。

      これらのエンドポイントは、コンテンツの取得元と、コンテンツのプッシュ先を定義します。 作成者は、指定されたエクスポーターエンドポイントからコンテンツを取得し、コンテンツを（コンテンツの取得元の発行者以外の）発行者にプッシュします。
   ![sync-agent-fact](assets/sync-agent-fact.png)

### Adobe Granite Distribution - Encrypted Password Transport Secret Provider {#adobe-granite-distribution-encrypted-password-transport-secret-provider}

これにより、作成者は、許可されたユーザーを、作成者から発行するユーザーデータを同期する権限を持つユーザーとして識別できます。

すべての発行インスタンスで [作成された認証済みユーザーは](../../help/sites-administering/sync.md#createauthuser) 、発行者が作成者と接続し、発行者のSling配布を設定するのに役立ちます。 この権限を持つユーザーには、必要なすべての [ACLがあり](../../help/sites-administering/sync.md#howtoaddacl)ます。

発行者にデータをインストールする場合、または発行者からデータを取得する場合は、この設定で設定された資格情報（ユーザー名とパスワード）を使用して作成者と接続します。

<!--This section used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

### 許可されたユーザーを使用して発行者と発行者を接続するには

AEMオーサーインスタンス：

1. 管理者権限でサインインします。
1. Access the [Web Console](../../help/sites-deploying/configuring-osgi.md).

   For example, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Locate **[!UICONTROL Adobe Granite Distribution - Encrypted Password Transport Secret Provider]**.
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   プロパティ `name:` \ — を検証し **`socialpubsync`ま`publishUser`す。**
1. ユーザー名とパスワードを [許可されたユーザーに設定します](../../help/sites-administering/sync.md#createauthorizeduser)。

   例えば、 **`usersync`\-admin **

   ![花崗岩 — パスワード —trans](assets/granite-paswrd-trans.png)

### Apache Sling Distribution Agent - Queue Agents Factory {#apache-sling-distribution-agent-queue-agents-factory}

この設定は、発行者間で同期するデータを設定する場合に使用します。 「 **[!UICONTROL 許可されたルート」で指定されたパスでデータが作成/更新されると]**、「var/community/distribution/diff」がアクティブ化され、作成されたレプリケーターはパブリッシャーからデータを取得し、他のパブリッシャーにインストールします。

<!--This section used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

### 同期するデータ（ノードパス）を設定するには

AEM発行インスタンス：

1. 管理者権限でサインインします。
1. Access the [Web Console](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/configuring-osgi.html).

   For example, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr).
1. Locate **[!UICONTROL Apache Sling Distribution Agent - Queue Agents Factory]**.
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   検証名： `socialpubsync` \-reverse.
1. 「 **[!UICONTROL 有効]** 」チェックボックスを選択して保存します。
1. 「 **[!UICONTROL 許可されたルート」で複製するノードパスを指定します]**。
1. Repeat  for each `publish` instance.

   ![queue-agents-fact](assets/queue-agents-fact.png)

### Adobe Granite Distribution - Diff Observer Factory {#adobe-granite-distribution-diff-observer-factory}

この設定は、パブリッシャー間でグループメンバーシップを同期します。\
ある発行者のグループのメンバーシップを変更しても、他の発行者のメンバーシップが更新されない場合は、 **ref:members** が **参照されたプロパティ名に追加されていることを確認します**。

<!--This section used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

### メンバーの同期を確実に行うには

各AEM発行インスタンスで、次の操作を行います。

1. 管理者権限でサインインします。
1. Access the [Web Console](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/configuring-osgi.html).

   For example, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr).
1. Locate **[!UICONTROL Adobe Granite Distribution - Diff Observer Factory]**.
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   検証 **[!UICONTROL エージェント名]**: `socialpubsync` \-reverse&amp;ast;&amp;ast;.
1. Select the **[!UICONTROL Enabled]** checkbox.
1. 検索されたプロパティ名 **のpropertyNameに対して`:members`**rep`description`****と指定し、[保存]を選択します。

   ![diff-obs](assets/diff-obs.png)

### Apache Sling Distribution Trigger - Scheduled Triggers Factory {#apache-sling-distribution-trigger-scheduled-triggers-factory}

この設定では、（発行者がpingを送信し、変更を作成者が取得した後の）ポーリング間隔を設定して、発行者間で変更を同期できます。

作成者は、30秒（デフォルト）ごとに投稿者をポーリングします。 任意のパッケージがフォルダー */var/sling/distribution/packages/ socialpubsync - vlt /shared*&#x200B;に存在する場合、それらのパッケージが取得され、他の発行者にインストールされます。

<!--This section used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

### ポーリング間隔を変更するには

AEMオーサーインスタンス：

1. 管理者権限でサインインします。
1. Access the [Web Console](../../help/sites-deploying/configuring-osgi.md), for example, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. Locate **[!UICONTROL Apache Sling Distribution Trigger - Scheduled Triggers Factory]**

   * 編集用に開く既存の設定を選択します（鉛筆アイコン）
   * \ `Name:` -scheduled-trigger **`socialpubsync`の検証&#x200B;**
   * 間隔（秒）を目的の間隔に設定し、保存します。

   ![scheduled-trigger](assets/scheduled-trigger.png)

### AEM Communities User Sync Listener {#aem-communities-user-sync-listener}

Sling配布で、購読に不一致があり、それに続く問題については、 **[!UICONTROL AEM Communitiesユーザー同期リスナー]** の設定で次のプロパティが設定されているかどうかを確認してください。

* NodeTypes
* IgnorableProperties
* IgnorableNodes
* DistributedFolders

<!--This section used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

### 購読、フォロー、通知を同期するには

各AEM発行インスタンスで、次の操作を行います。

1. 管理者権限でサインインします。
1. Access the [Web Console](../../help/sites-deploying/configuring-osgi.md). For example, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr).
1. Locate **[!UICONTROL AEM Communities User Sync Listener]**.
1. 編集用に開く既存の設定を選択します（鉛筆アイコン）。

   検証名： **`socialpubsync`\-scheduled-trigger **
1. 次を設定しま **`NodeTypes`** す。

   rep:User

   `nt` :unstructured

   `nt` :resource

   rep:ACL

   sling:Folder

   sling:OrderedFolder

   このプロパティで指定されたノードタイプが同期され、通知情報（ブログと使用された設定）が異なる発行者間で同期されます。
1. DistributedFolders追加内で同期するすべてのフォルダ ****。 例：

   segments/scoring

   social/relationships

   activities

1. Set the **`ignorablenodes`** to:

   .tokens

   system

   rep `:cache` （スティッキーセッションを使用するので、このノードを別の発行者と同期する必要はありません）

   ![user-sync-listner](assets/user-sync-listner.png)

### 一意の Sling ID{#unique-sling-id} の節を参照してください 

AEM作成者インスタンスは、Sling IDを使用して、データの送信元およびパッケージの返送先（または送り返す必要のない発行者）を識別します。

発行ファーム内のすべての発行者が一意のSling IDを持っていることを確認します。 Sling IDが、発行ファーム内の複数の発行インスタンスに対して同じである場合、ユーザーの同期は失敗します。 作成者はパッケージの取り込み元とインストール先を知りません。

<!--This section used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

### 発行ファームで発行者のSling IDを一意にするには

各パブリッシュインスタンスで以下をおこないます。

1. Browse to [https://_host:port_/system/console/status-slingsettings](http://localhost:4503/system/console/status-slingsettings).
1. Check the value of **[!UICONTROL Sling ID]**.

   ![slingid](assets/slingid.png)

   あるパブリッシュインスタンスの Sling ID が他のパブリッシュインスタンスの Sling ID と一致する場合は、次のようにします。

1. 一致するSling IDを持つ発行インスタンスの1つを停止します。
1. ディレクトリで、_sling.id.fileという名前のファイルを検索して削除します。 `crx-quickstart/launchpad/felix`

   *例えば、Linuxシステムでは：*

   `rm -i $(find . -type f -name sling.id.file)`

   *例えば、Windowsシステムでは、次の操作を行います。*

   `use windows explorer and search for _sling.id.file_`

1. 発行インスタンスを起動します。起動時に、新しいSling IDが割り当てられます。
1. Validate that the **[!UICONTROL Sling ID]** is now unique.

すべてのパブリッシュインスタンスの Sling ID が一意になるまでこの手順を繰り返します。

### Vault Package Builder Factory {#vault-package-builder-factory}

アップデートを正しく同期するには、ユーザ同期用にVaultパッケージビルダを変更する必要があります。\
で `/home/users`は、 `/rep:cache` ノードが作成されます。 これは、ノードのプリンシパル名にクエリした場合に、そのキャッシュを直接使用できることを確認するために使用されるキャッシュです。

ノードが発行者間で同期されている場合、ユーザーの同期は停止する場合があり `rep:cache `ます。

<!--This section used to be an accordion until converted to straight Markdown. When accordions are enabled, revert-->

### アップデートが発行者間で適切に同期されるようにするには

各AEM発行インスタンスで、次の操作を行います。

1. Access the [Web Console](../../help/sites-deploying/configuring-osgi.md), for example, [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr).
1. Locate the **[!UICONTROL Apache Sling Distribution Packaging - Vault Package Builder Factory Builder name]**: socialpubsync-vlt.
1. 編集アイコンを選択します。
1. 2つの追加パッケージフィルター:

   * `/home/users|-.\*/.tokens`
   * `/home/users|**+**.\*/rep:cache`
1. ポリシー処理
   * To overwrite existing rep `:policy` nodes with new ones, add a third Package Filter:

      `/home/users|**+**.\*/rep:policy`
   * ポリシーの配布を防ぐには、

      Acl処理： IGNORE

![vault-package-builder-factory](assets/vault-package-builder-factory.png)

## AEM CommunitiesでのSlingの配布のトラブルシューティング {#troubleshoot-sling-distribution-in-aem-communities}

Slingの配布に失敗した場合は、次のデバッグ手順を試してください。

1. **不[適切に追加された設定を確認します](../../help/sites-administering/sync.md#improperconfig)。** 複数の設定を追加または編集しないでください。既存のデフォルト設定は、編集する必要があります。
1. **設定を確認**。 ベストプラクティスに従って、AEM Authorインスタンスですべての [設定](sync.md#bestpractices) が適切に設定されていることを確認し [ます](sync.md#main-pars-header-863110628)。
1. **認証済みユーザー権限を確認します**。 パッケージが正しくインストールされていない場合は、最初の発行インスタンスで [作成された認証済みユーザー](../../help/sites-administering/sync.md#createauthuser) に、正しいACLが割り当てられていることを確認します。

   これを検証するには、 [作成した認証済みユーザーの代わりに](../../help/sites-administering/sync.md#createauthuser) 、作成者インスタンスの [AdobeGranite配布 — 暗号化パスワードトランスポートシークレットプロバイダー](../../help/sites-administering/sync.md#adobegraniteencpasswrd) の設定を、管理者ユーザーの資格情報を使用するように変更します。 次に、パッケージのインストールを再試行します。 ユーザー同期が管理者の資格情報で正常に機能する場合は、作成した発行ユーザーに適切なACLがないことを意味します。

1. **相違オブザーバーファクトリの構成を確認します**。 特定のノードのみがパブリッシュファーム全体で同期されない場合（例えば、グループメンバーは同期されない）、 [AdobeGranite Distribution - Diff Observer Factory](../../help/sites-administering/sync.md#diffobserver) 構成が有効で、 **rep:members** が **検索されたプロパティ名に設定されていることを確認します**。
1. **AEM Communitiesユーザー同期リスナーの設定を確認します。** 作成したユーザーが同期されているが、購読と次のユーザーが機能していない場合は、AEM Communitiesユーザー同期リスナーの構成に次の値が含まれていることを確認します。

   * ノードタイプ — **rep:User, nt:unstructured**, **nt:resource**, nt:ACL **, sling:Folder Sling,********OrderedFolderに設定**
   * 無視可能なノード： **.tokens**、 **system**、 **rep:cacheに設定**
   * 分散フォルダ：分散するフォルダに設定

1. **発行インスタンスでのユーザー作成時に生成されたログを確認します**。 上記の設定が適切に設定されているにもかかわらずユーザー同期が機能していない場合は、ユーザーの作成時に生成されたログを確認します。

   次のように、ログの順序が同じかどうかを確認します。

   ```shell
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7422] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ2: ADD paths=[/home/users/C, /home/users/C/Cw-5avWqilmqsNn5hCvK], user=communities-user-admin
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy]
   15.05.2016 18:33:01.523 *INFO* [sling-oak-observation-7431] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ3: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK, /home/users/C/Cw-5avWqilmqsNn5hCvK/profile, /home/users/C/Cw-5avWqilmqsNn5hCvK/rep:policy], user=communities-user-admin
   15.05.2016 18:33:01.757 *INFO* [sling-oak-observation-7431] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_ebb27ad9-a861-4405-9342-d64c916654e2:0.0.1
   15.05.2016 18:33:01.820 *INFO* [sling-oak-observation-7422] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337181554_58811273-5861-48fe-95d2-4aff367b99c3:0.0.1
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] com.adobe.cq.social.sync.impl.PublisherSyncServiceImpl Handing these paths to the distribution subsystem: [/home/users/C/Cw-5avWqilmqsNn5hCvK/profile]
   15.05.2016 18:33:02.023 *INFO* [sling-oak-observation-7430] org.apache.sling.distribution.agent.impl.SimpleDistributionAgent [agent][socialpubsync-reverse] REQUEST-START DSTRQ4: ADD paths=[/home/users/C/Cw-5avWqilmqsNn5hCvK/profile], user=communities-user-admin
   15.05.2016 18:33:02.273 *INFO* [sling-oak-observation-7430] org.apache.jackrabbit.vault.packaging.impl.JcrPackageDefinitionImpl unwrapping package sling/distribution:socialpubsync-vlt_1463337182039_f34f4fa6-10b9-42eb-8740-4da9d4d38f99:0.0.1
   ```

   デバッグするには：

   1. ユーザー同期を無効にします。
   1. AEMオーサーインスタンスで、管理者権限でサインインします。

      1. Access the [Web Console](../../help/sites-deploying/configuring-osgi.md). For example, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
      1. Locate the configuration **[!UICONTROL Apache Sling Distribution Agent - Sync Agents Factory]**.

      1. Deselect the **[!UICONTROL Enabled]** checkbox.
      作成者インスタンスでユーザー同期を無効にすると、（エクスポーターとインポーター）エンドポイントが無効になり、作成者インスタンスは静的になります。 **[!UICONTROL vlt]** パッケージは、作成者によってpingまたは取得されません。

      現在は、ユーザーが発行インスタンスで作成された場合、 **[!UICONTROL vlt]** パッケージは */var/sling/distribution/packages/ socialpubsync - vlt /data* nodeに作成されます。 また、これらのパッケージが作成者によって別のサービスにプッシュされた場合も、 このデータをダウンロードして抽出し、すべてのプロパティが他のサービスにプッシュされたものかどうかを確認できます。

   1. 投稿者に移動し、投稿でユーザーを作成します。 その結果、イベントが作成されます。
   1. ユーザーの作成時に作成されたログ [、ログの](sync.md#troubleshoot-sling-distribution-in-aem-communities)順序を確認します。
   1. に **[!UICONTROL vlt]** パッケージが作成されているかどうかを確認 `/var/sling/distribution/packages/socialpubsync-vlt/data`します。
   1. 次に、AEMオーサーインスタンスでユーザー同期を有効にします。
   1. 発行者で、 **[!UICONTROL Apache Sling Distribution Agent - Sync Agents Factoryのエクスポーターまたはインポーターエンドポイントを変更します]**。

      パッケージデータをダウンロードして抽出し、すべてのプロパティが他の発行者にプッシュされ、どのデータが失われるかを確認できます。


