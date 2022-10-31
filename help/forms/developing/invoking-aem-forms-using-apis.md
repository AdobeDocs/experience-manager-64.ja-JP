---
title: API を使用した AEM Forms の呼び出し
seo-title: Invoking AEM Forms using APIs
description: Adobe Experience Manager Forms は、共有インフラストラクチャで操作されるサービスからなる、J2EE ベースのエンタープライズソフトウェアです。Java API、Web サービス、Remoting および REST API を使用して、クライアントアプリケーションを使用して、AEM Formsをプログラムで呼び出す方法を説明します。
seo-description: Adobe Experience Manager Forms is J2EE-based enterprise software that consists of services that operate within a shared infrastructure. Learn how to use client applications to invoke AEM Forms programmatically using a Java API, web services, Remoting, and REST API.
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: development-tools, coding
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
role: Developer
exl-id: 6b60209f-aced-4698-97f1-b1a7782eef46
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 93%

---

# API を使用した AEM Forms の呼び出し {#invoking-aem-forms-using-apis}

Adobe Experience Manager Forms は、共有インフラストラクチャで操作されるサービスからなる、J2EE ベースのエンタープライズソフトウェアです。サービス操作では、通常、 ドキュメントを使用または生成します。AEM Forms を使用すると、統合され凝縮された一連のサービスにより、Forms Workflow と電子フォーム、ドキュメントセキュリティ、ドキュメント生成を組み合わせることができます。これらのサービスへは、ファイアウォールの内側からでも外側からでもアクセスできます。

クライアントアプリケーションは、Java API、web サービス、Remoting、REST を使用することにより、AEM Forms サービスをプログラムで呼び出すことができます。管理コンソールを使用してサービスを設定すると、AEM Forms サービスをプログラムで呼び出せるエンドポイントを公開できます。デフォルトでは、ほとんどのサービスは、Remoting、Java、web サービスの各エンドポイントを公開するように事前に設定されています。

ビジネス要件に応じて、使用する呼び出し方法を決定します。例えば、Java API を使用すると、Java エンティティやメッセージ Bean などの Java エンタープライズアプリケーションに AEM Forms 機能を統合できます。同様に、web サービスを使用して、AEM Forms 機能を .NET プロジェクト（または、web サービス標準をサポートする開発環境で開発された他のプロジェクト）に統合できます。

サービスを実行するには、Enterprise JavaBeans™（EJB）が J2EE コンテナを必要とするのと同様に、サービスコンテナが必要です。AEM Forms に含まれているサービスコンテナの実装は 1 つのみです。サービスコンテナは、サービスのデプロイや、すべてのリクエストが正しいサービスに送信されるようにするなど、サービスの全期間を管理する役割を担います。サービスが使用または生成するドキュメントも管理します。

>[!NOTE]
>
>AEM Forms によるプログラミングには、監視フォルダーやメールを使用した AEM Forms の呼び出し方法に関する情報は含まれていません。
