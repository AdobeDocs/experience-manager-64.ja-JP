---
title: サービスの開始と停止
seo-title: Starting and stopping services
description: AEM Forms モジュール、アプリケーションサーバー、データベースに関連付けられたサービスを開始および停止する方法について説明します。
seo-description: Learn how to start and stop services associated with AEM Forms modules and the application server and database.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
exl-id: 6e0607d6-171c-4119-95a1-373b30fb63c1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 81%

---

# サービスの開始と停止 {#starting-and-stopping-services}

AEM Forms に含まれるサービスには以下の 2 種類があります。

* AEM Forms アプリケーションサーバーおよびデータベースを制御するサービス
* AEM Forms モジュールを制御するサービス

## AEM Forms モジュール関連サービスの開始と停止 {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM Forms モジュール（例えば、Forms、Rights Management、Output）がサービスとして動作します。これらの AEM Forms モジュールのサービスは、場合によって起動または停止する必要があります。例えば、サービスの設定を変更した後には、AEM Forms サービスを停止してから再起動する必要があります。

1. 管理コンソールで、 **サービス** > **アプリケーションとサービス** > **サービス管理**.
1. サービスの管理ページで、停止または開始するサービスの隣のチェックボックスを選択して、「停止」または「開始」をクリックします。

## アプリケーションサーバーおよびデータベースのサービスの開始と停止 {#start-or-stop-services-for-the-application-server-and-database}

AEM Forms の完全な実装には、以下のアプリケーションサーバーおよびデータベースのサービスが含まれています。

* *`[application server]`* (AEM forms の場合 )
* *`[database]`* (AEM forms の場合 )

Windows では、これらのサービスには **管理ツール** > **サービスパネル**. 例えば、自動オプションを使用して JBoss に AEM Forms をインストールした場合、システムでは以下のサービスを使用できます。

* JBoss for Adobe Experience Manager forms
* MySQL for Adobe Experience Manager forms

これらのサービスを開始または停止するには、リストからサービスを選択し、パネルの適切なアクションボタンをクリックします。

UNIX®または Linux の場合は、コマンド・ラインから次のテキストを入力します。 *`[service name]`* は、検証するサービスの名前です。

```as3
     ps -A | grep [service name]
```
