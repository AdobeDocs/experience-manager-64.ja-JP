---
title: アプリケーションサーバーのインストール環境のアップグレード手順
seo-title: Upgrade Steps for Application Server Installations
description: アプリケーションサーバーを介してデプロイされるAEMのインスタンスをアップグレードする方法について説明します。
seo-description: Learn how to upgrade instances of AEM that are deployed via Application Servers.
uuid: df3fa715-af4b-4c81-b2c5-130fbc82f395
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: c427c8b6-eb94-45fa-908f-c3d5a337427d
feature: Upgrading
exl-id: 1c72093e-82c8-49ad-bd3c-d61904aaab28
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 39%

---

# アプリケーションサーバーのインストール環境のアップグレード手順{#upgrade-steps-for-application-server-installations}

ここでは、アプリケーションサーバーインストール用の AEM を更新するために必要になる手順を説明します。

この手順の例では、JBoss をアプリケーションサーバーとして使用し、AEMの動作中のバージョンが既にデプロイされていることを示します。 ここでは、**AEM バージョン 5.6 から 6.3** へのアップグレードについて説明します。

1. まず、JBoss を起動します。 ほとんどの場合、これをおこなうには、 `standalone.sh` ターミナルから次のコマンドを実行して、起動スクリプトを実行します。

   ```shell
   jboss-install-folder/bin/standalone.sh
   ```

1. AEM 5.6 が既にデプロイされている場合は、次のコマンドを実行して、バンドルが正しく機能していることを確認します。

   ```shell
   wget https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 次に、AEM 5.6 のデプロイを解除します。

   ```shell
   rm jboss-install-folder/standalone/deployments/cq.war
   ```

1. JBoss を停止します。

1. 次に、crx2oak 移行ツールを使用してリポジトリを移行します。

   ```shell
   java -jar crx2oak.jar crx-quickstart/repository/ crx-quickstart/oak-repository
   ```

   >[!NOTE]
   >
   >この例では、oak-repository は、新しく変換されたリポジトリが配置される一時ディレクトリです。 この手順を実行する前に、最新の crx2oak.jar のバージョンがあることを確認してください。

1. 次の操作をおこなって、sling.properties ファイル内の必要なプロパティを削除します。

   1. `crx-quickstart/launchpad/sling.properties` に置かれたファイルを開きます。
   1. 次のプロパティを削除してファイルを保存します。

      1. `sling.installer.dir`
      1. `felix.cm.dir`
      1. `granite.product.version`
      1. `org.osgi.framework.system.packages`
      1. `osgi-core-packages`
      1. `osgi-compendium-services`
      1. `jre-*`
      1. `sling.run.mode.install.options`

1. 不要になったファイルとフォルダーを削除します。 具体的に削除する必要がある項目は次のとおりです。

   * この **launchpad/startup フォルダー**. ターミナルで次のコマンドを実行して削除できます。`rm -rf crx-quickstart/launchpad/startup`
   * **base.jar ファイル**：`find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`
   * **BootstrapCommandFile_timestamp.txt ファイル**：`rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

1. 新しく移行した segmentstore を適切な場所にコピーします。

   ```shell
   mv crx-quickstart/oak-repository/segmentstore crx-quickstart/repository/segmentstore
   ```

1. データストアもコピーします。

   ```shell
   mv crx-quickstart/repository/repository/datastore crx-quickstart/repository/datastore
   ```

1. 次に、新しくアップグレードされたインスタンスで使用される OSGi 設定を格納するフォルダーを作成する必要があります。 具体的には、 install という名前のフォルダーを以下の場所に作成する必要があります。 **crx-quickstart**.

1. 次に、AEM 6.3 で使用するノードストアとデータストアを作成します。これをおこなうには、次の名前を持つ 2 つのファイルをの下に作成します。 **crx-quickstart\install**:

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`

   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   これら 2 つのファイルは、TarMK ノードストアとファイルデータストアを使用するようにAEMを設定します。

1. 設定ファイルを編集して、使用可能にします。 具体的には、

   * 次の行を **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**:

      `customBlobStore=true`

   * 次の行を **org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**:

      ```
      path=./crx-quickstart/repository/datastore
       minRecordLength=4096
      ```

1. 次のコマンドを実行して、crx2 実行モードを削除します。

   ```shell
   find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf {} \
   ```

1. 今度は、AEM 6.3 war ファイル内の実行モードを変更する必要があります。変更するには、まず AEM 6.3 war を格納する一時フォルダーを作成します。この例では、フォルダーの名前は次のようになります。 **temp**. war ファイルをコピーしたら、temp フォルダー内で次のコマンドを実行して、内容を抽出します。

   ```shell
   jar xvf aem-quickstart-6.3.0.war
   ```

1. 内容を抽出したら、**WEB-INF** フォルダーに移動して ファイルを編集し、実行モードを変更します。`web.xml`XML での実行モードの設定場所を探すには、`sling.run.modes` 文字列を検索します。見つかったら、コードの次の行で実行モードを変更します。デフォルトでは、author に設定されています。

   ```shell
   <param-value >author</param-value>
   ```

1. 上記の author 値を変更し、実行モードを次のように設定します。author,crx3,crx3tar コードの最終ブロックは次のようになります。

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 編集後の内容で jar を再作成します。

   ```shell
   jar cvf aem62.war
   ```

1. 最後に、新しい war ファイルをデプロイします。

   ```shell
   cp temp/aem62.war jboss-install-folder/standalone/deployments/aem61.war
   ```
