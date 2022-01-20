---
title: API を使用したAEM Formsの呼び出し
seo-title: Invoking AEM Forms using APIs
description: 'Adobe Experience Manager Formsは、共有インフラストラクチャ内で動作するサービスで構成される、J2EE ベースのエンタープライズソフトウェアです。 Java API、Web サービス、Remoting および REST API を使用して、クライアントアプリケーションを使用して、AEM Formsをプログラムで呼び出す方法を説明します。 '
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
ht-degree: 0%

---

# API を使用したAEM Formsの呼び出し {#invoking-aem-forms-using-apis}

Adobe Experience Manager Formsは、共有インフラストラクチャ内で動作するサービスで構成される、J2EE ベースのエンタープライズソフトウェアです。 サービス操作は、通常、ドキュメントを消費または生成します。 AEM Formsを使用すると、フォームワークフローと電子フォーム、ドキュメントセキュリティ、ドキュメント生成を、統合されたまとまったサービスのセットで組み合わせることができます。 これらのサービスは、ファイアウォールの内外からアクセスできます。

クライアントアプリケーションは、Java API、Web サービス、Remoting、および REST を使用して、AEM Formsサービスをプログラムで呼び出すことができます。 管理コンソールを使用して、プログラムによって呼び出されることによってAEM Formsサービスを可能にするエンドポイントを公開するようにサービスを設定できます。 デフォルトでは、ほとんどのサービスは、リモート、Java、Web サービスの各エンドポイントを公開するように事前に設定されています。

ビジネス要件によって、使用する呼び出し方法が決まります。 例えば、Java API を使用して、Java エンティティや Message Bean などの Java エンタープライズアプリケーションにAEM Forms機能を統合できます。 同様に、Web サービスを使用して、AEM Forms機能を.NET プロジェクト（または、Web サービス標準をサポートする開発環境で開発された他のプロジェクト）に統合できます。

サービスを実行するには、Enterprise JavaBeans™ (EJB) が J2EE コンテナを必要とするのと同様に、サービスコンテナが必要です。 AEM Formsには、サービスコンテナの 1 つの実装のみが含まれています。 サービスコンテナは、サービスのデプロイや、すべてのリクエストが正しいサービスに送信されるようにするなど、サービスの有効期間を管理する役割を担います。 また、サービスが消費または生成するドキュメントも管理します。

>[!NOTE]
>
>AEM forms によるプログラミングには、監視フォルダーや電子メールを使用したAEM Formsの呼び出し方法に関する情報は含まれていません。
