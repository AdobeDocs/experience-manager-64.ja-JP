---
title: アップグレード手順
seo-title: Upgrade Procedure
description: AEMをアップグレードするために従う必要がある手順について説明します。
seo-description: Learn about the procedure you need to follow in order to upgrade AEM.
uuid: 56fb6af7-6e5f-4288-822b-f40c4605a28b
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
discoiquuid: ba90b25f-f672-42c5-8b06-07bb32cc51de
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: e6092e80-3a39-4fde-8a94-084eee5fa8a9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 58%

---

# アップグレード手順{#upgrade-procedure}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>ほとんどのAEMのアップグレードはインプレースで実行されるので、アップグレードにはオーサー層のダウンタイムが必要になります。 これらのベストプラクティスに従うことで、パブリッシュ層のダウンタイムを最小限に抑えたり、削除したりできます。

AEM環境をアップグレードする際は、作成者とエンドユーザーの両方のダウンタイムを最小限に抑えるために、オーサー環境またはパブリッシュ環境のアップグレードのアプローチの違いを考慮する必要があります。 このページでは、AEM 6.x のバージョンで現在実行中のAEMトポロジをアップグレードするための高レベルの手順について説明します。このプロセスは、オーサー層とパブリッシュ層、Mongo と TarMK ベースのデプロイメントとで異なるので、各層とマイクロカーネルは別の節に記載されています。 デプロイメントを実行する場合は、まずオーサー環境をアップグレードし、成功を判断してから、パブリッシュ環境に進むことをお勧めします。

## TarMK オーサー層 {#tarmk-author-tier}

### トポロジの開始 {#starting-topology}

この節で想定されるトポロジは、TarMK 上で実行され、コールドスタンバイを使用するオーサーサーバーで構成されます。 オーサーサーバーから TarMK パブリッシュファームへのレプリケーションが発生します。 ここでは説明しませんが、この方法は、オフロードを使用するデプロイメントにも利用できます。 オーサーインスタンスでレプリケーションエージェントを無効にした後、再度有効にする前に、新しいバージョンでオフロードインスタンスをアップグレードまたは再構築してください。

![tarmk_starting_topology](assets/tarmk_starting_topology.jpg)

### アップグレードの準備 {#upgrade-preparation}

![upgrade-preparation-author](assets/upgrade-preparation-author.png)

1. コンテンツのオーサリングを停止します。
1. スタンバイインスタンスを停止します。
1. オーサーのレプリケーションエージェントを無効にします。
1. を実行します。 [アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md).

### アップグレードの実行 {#upgrade-execution-1}

![execute_upgrade](assets/execute_upgrade.jpg)

1. [インプレースアップグレード](/help/sites-deploying/in-place-upgrade.md)を実行します。
1. *必要に応じて*、Dispatcher モジュールを更新します。
1. QA がアップグレードを検証します。
1. オーサーインスタンスをシャットダウンします。

### 成功した場合 {#if-successful}

![if_successful](assets/if_successful.jpg)

1. 新しいコールドスタンバイを作成するために、アップグレードされたインスタンスをコピーします。
1. オーサーインスタンスを起動します。
1. スタンバイインスタンスを起動します。

### 失敗した場合（ロールバック） {#if-unsuccessful-rollback}

![rollback](assets/rollback.jpg)

1. コールドスタンバイインスタンスを新しいプライマリとして起動します。
1. コールドスタンバイからオーサー環境を再構築します。

## MongoMK オーサークラスター {#mongomk-author-cluster}

### トポロジの開始 {#starting}

この節で想定されるトポロジは、少なくとも 2 つの MongoMK データベースをベースとする、2 つ以上の AEM オーサーインスタンスを持つ MongoMK オーサークラスターで構成されます。 すべてのオーサーインスタンスは 1 つのデータストアを共有します。 以下の手順は、S3 とファイルの両方のデータストアに適用する必要があります。 オーサーサーバーから TarMK パブリッシュファームへのレプリケーションが発生します。

![mongo-topology](assets/mongo-topology.jpg)

### アップグレードの準備 {#preparation}

![mongo-upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. コンテンツのオーサリングを停止します。
1. バックアップ用のデータストアのクローンを作成します。
1. 1 つの AEM オーサーインスタンス（プライマリオーサー）以外をすべて停止します。
1. レプリカセットから 1 つの MongoDB ノード（プライマリ Mongo インスタンス）以外をすべて削除します。
1. 単一メンバーのセカンダリセットが反映されるように、プライマリ作成者上の `DocumentNodeStoreService.cfg` ファイルをアップデートします。
1. プライマリオーサーを再起動して、正常に再起動することを確認します。
1. プライマリオーサーのレプリケーションエージェントを無効にします。
1. プライマリオーサーインスタンスで[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を実行します。
1. 必要に応じて、プライマリ Mongo インスタンスの MongoDB を WiredTiger が搭載されたバージョン 3.2 にアップグレードします。

### アップグレードの実行 {#execution}

![mongo-execution](assets/mongo-execution.jpg)

1. プライマリオーサーで[インプレースアップグレード](/help/sites-deploying/in-place-upgrade.md)を実行します。
1. *必要に応じて*、Dispatcher モジュールまたは Web モジュールを更新します。
1. QA がアップグレードを検証します。

### 成功した場合 {#successful-1}

![mongo-secondaries](assets/mongo-secondaries.jpg)

1. アップグレードされた Mongo インスタンスに接続する新しい 6.3 オーサーインスタンスを作成します。
1. クラスターから削除された MongoDB ノードを再構築します。
1. レプリカのフルセットが反映されるように、`DocumentNodeStoreService.cfg` ファイルを更新します。
1. オーサーインスタンスを 1 つずつ再起動します。
1. クローン作成されたデータストアを削除します。

### 失敗した場合（ロールバック）  {#if-unsuccessful}

![mongo-rollback](assets/mongo-rollback.jpg)

1. クローン作成されたデータストアに接続するために、セカンダリオーサーインスタンスを再設定します。
1. アップグレードされたオーサープライマリインスタンスをシャットダウンします。
1. アップグレードされた Mongo プライマリインスタンスをシャットダウンします。
1. セカンダリ Mongo インスタンスを起動し、そのうちの 1 つを新しいプライマリとして設定します。
1. アップグレードされていない Mongo インスタンスのレプリカセットを指すように、セカンダリオーサーインスタンスで `DocumentNodeStoreService.cfg` ファイルを設定します。
1. セカンダリオーサーインスタンスを起動します。
1. アップグレードされたオーサーインスタンス、Mongo ノードおよびデータストアをクリーンアップします。

## TarMK パブリッシュファーム {#tarmk-publish-farm}

### TarMK パブリッシュファーム {#publish-farm}

この節で想定されるトポロジは、2 つの TarMK パブリッシュインスタンスで構成され、Dispatcher がフロントし、ロードバランサーがフロントします。 オーサーサーバーから TarMK パブリッシュファームへのレプリケーションが発生します。

![tarmk-pub-farmv5](assets/tarmk-pub-farmv5.png)

### アップグレードの実行 {#execution-upgrade}

![upgrade-publish2](assets/upgrade-publish2.png)

1. ロードバランサーで Publish 2 インスタンスへのトラフィックを停止します。
1. Publish 2 で[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を実行します。
1. Publish 2 で[インプレースアップグレード](/help/sites-deploying/in-place-upgrade.md)を実行します。
1. *必要に応じて*、Dispatcher モジュールまたは Web モジュールを更新します。
1. Dispatcher キャッシュをフラッシュします。
1. QA が、ファイアウォールの後ろにある Dispatcher を介して Publish 2 を検証します。
1. Publish 2 をシャットダウンします。
1. Publish 2 インスタンスをコピーします。
1. Publish 2 を起動します。

### 成功した場合 {#successful-2}

![upgrade-publish1](assets/upgrade-publish1.png)

1. Publish 2 へのトラフィックを有効にします。
1. Publish 1 へのトラフィックを停止します。
1. Publish 1 インスタンスを停止します。
1. Publish 1 インスタンスを Publish 2 のコピーに置き換えます。
1. *必要に応じて*、Dispatcher モジュールまたは Web モジュールを更新します。
1. Publish 1 の Dispatcher キャッシュをフラッシュします。
1. Publish 1 を起動します。
1. QA が、ファイアウォールの後ろにある Dispatcher を介して Publish 1 を検証します。

### 失敗した場合（ロールバック） {#rollback}

![pub_rollback](assets/pub_rollback.jpg)

1. Publish 1 のコピーを作成します。
1. Publish 2 インスタンスを Publish 1 のコピーに置き換えます。
1. Publish 2 の Dispatcher キャッシュをフラッシュします。
1. Publish 2 を起動します。
1. QA が、ファイアウォールの後ろにある Dispatcher を介して Publish 2 を検証します。
1. Publish 2 へのトラフィックを有効にします。

## アップグレードの最終手順 {#final-upgrade-steps}

1. Publish 1 へのトラフィックを有効にします。
1. QA がパブリック URL から最終検証を実行します。
1. オーサー環境からレプリケーションエージェントを有効にします。
1. コンテンツのオーサリングを再開します。
1. [アップグレード後のチェック](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)を実行します。

![final](assets/final.jpg)
