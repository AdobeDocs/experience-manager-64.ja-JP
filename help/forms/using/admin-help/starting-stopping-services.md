---
title: サービスの開始と停止
seo-title: Starting and stopping services
description: AEM Formsモジュールとアプリケーションサーバーおよびデータベースに関連付けられたサービスを開始および停止する方法について説明します。
seo-description: Learn how to start and stop services associated with AEM Forms modules and the application server and database.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
exl-id: 6e0607d6-171c-4119-95a1-373b30fb63c1
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 21%

---

# サービスの開始と停止 {#starting-and-stopping-services}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM forms には、次の 2 種類のサービスが含まれます。

* AEM forms アプリケーションサーバーとデータベースを制御するサービス。
* AEM forms モジュールを制御するサービス

## AEM forms モジュールに関連付けられたサービスを開始または停止します {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM forms モジュール (Forms、Rights Management、出力など ) は、サービスとして動作します。 これらのAEM forms モジュールのサービスは、場合によっては停止または開始する必要があります。 例えば、サービスの設定を変更した後、AEM forms サービスを停止してから再起動する必要があります。

1. 管理コンソールで、**サービス**／**アプリケーションおよびサービス**／**サービスの管理**&#x200B;をクリックしてください。
1. 「サービスの管理」ページで、停止または開始するサービスの横にあるチェックボックスを選択し、「停止」または「開始」をクリックします。

## アプリケーションサーバーおよびデータベースのサービスを開始または停止します {#start-or-stop-services-for-the-application-server-and-database}

AEM Forms の完全な実装には、アプリケーションサーバーとデータベースサービスが含まれます。

* AEM Forms 用の *`[application server]`*
* AEM Forms 用の *`[database]`*

Windows では、これらのサービスには、**管理ツール**／**サービスパネル**&#x200B;からアクセスできます。例えば、自動オプションを使用して JBoss にAEM forms をインストールした場合、システム上で次のサービスを使用できます。

* JBoss for Adobe Experience Manager forms
* Adobe Experience Manager forms の MySQL

サービスパネルのリストからサービスを選択し、パネルの適切なアクションボタンをクリックして、これらのサービスを開始または停止します。

UNIX® または Linux では、コマンドラインから次のテキストを入力します。*`[service name]`* には、確認するサービスの名前を指定します。

```as3
     ps -A | grep [service name]
```
