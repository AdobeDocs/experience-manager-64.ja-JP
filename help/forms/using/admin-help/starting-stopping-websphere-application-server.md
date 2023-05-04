---
title: WebSphere Application Server の起動と停止
seo-title: Starting and stopping WebSphere Application Server
description: 一部の手順では、AEM forms 製品をデプロイする WebSphere のインスタンスを停止または開始する必要があります。 このドキュメントでは、WebSphere Application Server を起動および停止する方法について説明します。
seo-description: Several procedures require you to stop or start the instance of WebSphere where you want to deploy AEM forms products. This document describes how to start and stop the WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
exl-id: 8e3bb77f-b187-42c8-a90e-fe0fee50dc34
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 40%

---

# WebSphere Application Server の起動と停止 {#starting-and-stopping-websphere-application-server}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

一部の手順では、AEM forms 製品をデプロイする WebSphere のインスタンスを停止または開始する必要があります。 アプリケーションサーバーが起動しているかどうかが不明な場合は、まず WebSphere Application Server のステータスを表示できます。

## WebSphere Application Server のステータスの表示 {#view-the-status-of-websphere-application-server}

1. コマンドプロンプトで、 *[appserver root]*/bin ディレクトリ。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * （Windows）`serverStatus.bat`*server_name*
   * （Linux、UNIX）/ `serverStatus.sh`*server_name*

## WebSphere Application Server の起動 {#start-websphere-application-server}

1. コマンドプロンプトで、 *[appserver root]*/bin ディレクトリ。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * （Windows）`startServer.bat`*server_name*
   * （Linux、UNIX）/ `startServer.sh`*server_name*

## WebSphere Application Server の停止 {#stop-websphere-application-server}

1. コマンドプロンプトで、 *[appserver root]*/bin ディレクトリ。
1. 次のコマンドを入力します。*server_name* には、WebSphere Application Server の名前を指定します。

   * （Windows）`stopServer.bat`*server_name*
   * （Linux、UNIX）/ `stopServer.sh`*server_name*
