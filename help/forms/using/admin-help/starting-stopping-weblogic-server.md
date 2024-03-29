---
title: WebLogic Server の起動と停止
seo-title: Starting and stopping WebLogic Server
description: いくつかの手順では、AEM forms モジュールをデプロイする WebLogic Server のインスタンスを起動または停止する必要があります。 このドキュメントでは、WebLogic Server を起動および停止する方法について説明します。
seo-description: Several procedures require you to start or stop the instance of WebLogic Server where you want to deploy AEM forms modules. This document describes how to start and stop the WebLogic Server.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
exl-id: c7a74e20-4cfb-4674-af41-f3333c9b5397
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 25%

---

# WebLogic Server の起動と停止 {#starting-and-stopping-weblogic-server}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

いくつかの手順では、AEM forms モジュールをデプロイする WebLogic Server のインスタンスを起動または停止する必要があります。 実行するタスクに応じて、WebLogic Server が停止または実行されていることを確認します。

<table> 
 <thead> 
  <tr> 
   <th><p>アクティビティ</p></th> 
   <th><p>必須の WebLogic の状態</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>WebLogic ドメインの作成</p></td> 
   <td><p>中止</p></td> 
  </tr> 
  <tr> 
   <td><p>WebLogic 管理対象サーバーの作成</p></td> 
   <td><p>実行中</p></td> 
  </tr> 
  <tr> 
   <td><p>サーバースレッド数の増加</p></td> 
   <td><p>実行中</p></td> 
  </tr> 
  <tr> 
   <td><p>AEM forms 製品のデプロイ</p></td> 
   <td><p>実行中</p></td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Red Hat® Enterprise Linux Advanced Server 4.0 で WebLogic Server を実行している場合は、`export LD_ASSUME_KERNEL=2.4.19` コマンドを使用して、`LD_ASSUME_KERNEL` 環境変数を 2.4.19 に設定します。次に、この環境変数を設定したシェルと同じシェルから WebLogic Server を実行します。

## WebLogic Server を起動します {#start-weblogic-server}

1. コマンドプロンプトで *[appserver root]*/user_projects/domains/*[appserverdomain]* に移動します。
1. 以下のコマンドを入力します。

   * （Windows）`startWebLogic.cmd`
   * （Linux、UNIX）./ `startWebLogic.sh`

## WebLogic Server の停止 {#stop-weblogic-server}

1. Web ブラウザーの URL 行に `https://[host name]:7001/console` と入力して、WebLogic Server 管理コンソールを起動します。
1. この WebLogic 設定の作成時に使用したユーザー名とパスワードを入力してログインし、「Log In」をクリックします。
1. Change Center で、「Lock &amp; Edit」をクリックします。
1. 「Domain Structure」で、 Environment / Servers をクリックします。
1. [AdminServer] をクリックし、[Settings for AdminServer] ウィンドウで [Control] タブをクリックします。
1. Server Status テーブルで AdminServer が選択されていることを確認し、「Shutdown」をクリックします。
1. サーバーを正常にシャットダウンする場合は「When Work Completes」を選択し、進行中のタスクを完了せずにサーバーを直ちに停止する場合は「Force Shutdown Now」を選択します。
1. Server Life Cycle Assistant ウィンドウで、[ はい ] をクリックしてシャットダウンを完了します。

WebLogic Server 管理コンソールは使用できなくなり、start コマンドを実行したコマンドプロンプトが使用可能になります。

## WebLogic 管理コンソールを起動します {#start-weblogic-administration-console}

1. WebLogic 管理サーバーがまだ実行されていない場合は、コマンドプロンプトで *[appserver root]\user_projects\domains\[domainname]* ディレクトリに移動し、次のコマンドを入力します。

   * （Windows）`startWebLogic.cmd`
   * （Linux、UNIX）./ `startWebLogic.sh`

1. 入力して WebLogic Server 管理コンソールにアクセス `https://*[host name]:`[ポート] `/console` (Web ブラウザーの URL 行で *[ポート]* は、安全でないリスニングポートです。 デフォルトでは、このポート値は 7001 です。
1. ログイン画面で、管理者のユーザー名とパスワードを入力し、「Log In」をクリックします。

## ノードマネージャを起動 {#start-node-manager}

1. WebLogic Server が実行中であることを確認します。
1. 新たに起動したコマンドプロンプトで *[appserver root]*/server/bin に移動します。
1. 以下のコマンドを入力します。

   * （Windows）`startNodeManager.cmd`
   * （Linux、UNIX）`./startNodeManager.sh`

## ノードマネージャを停止 {#stop-node-manager}

WebLogic Server をシャットダウンした後、Node Manager を呼び出したコマンドプロンプトを閉じることができます。

## WebLogic 管理対象サーバーの起動 {#start-a-weblogic-managed-server}

>[!NOTE]
>
>このタスクは、WebLogic ドメインと管理対象サーバーを作成した後にのみ実行できます。

1. WebLogic Server と Node Manager が実行されていることを確認します。
1. Web ブラウザーの URL 行に `https://`*[host name]:[port ]*`/console` と入力して、WebLogic Server 管理コンソールを起動します。
1. 「Domain Structure」で、 Environment / Servers をクリックします。
1. 右側のウィンドウで、[ コントロール ] タブをクリックします。
1. 起動する管理対象サーバーを選択します。
1. 起動する管理対象サーバーの下の「開始」ボタンをクリックします。

## WebLogic 管理対象サーバーの停止 {#stop-a-weblogic-managed-server}

1. Web ブラウザーの URL 行に `https://`*[host name]:[port ]*`/console` と入力して、WebLogic Server 管理コンソールを起動します。
1. 「Domain Structure」で、 Environment / Servers をクリックします。
1. 右側のウィンドウで、[ コントロール ] タブをクリックします。
1. 停止する管理対象サーバーを選択します。
1. 停止する管理対象サーバーの下の [ シャットダウン ] ボタンをクリックします。
1. サーバーを正常にシャットダウンする場合は「When Work Completes」を選択し、進行中のタスクを完了せずにサーバーを直ちに停止する場合は「Force Shutdown Now」を選択します。
1. Server Life Cycle Assistant ウィンドウで、[ はい ] をクリックしてシャットダウンを完了します。
