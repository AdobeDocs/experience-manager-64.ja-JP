---
title: APIを使用したAEM Formsの呼び出し
seo-title: APIを使用したAEM Formsの呼び出し
description: 'Adobe Experience Manager Formsは、共有インフラストラクチャ内で動作するサービスで構成される、J2EEベースのエンタープライズソフトウェアです。 クライアントアプリケーションを使用して、Java API、Webサービス、Remoting、およびREST APIを使用してAEM Formsをプログラムで呼び出す方法について説明します。 '
seo-description: Adobe Experience Manager Formsは、共有インフラストラクチャ内で動作するサービスで構成される、J2EEベースのエンタープライズソフトウェアです。 クライアントアプリケーションを使用して、Java API、Webサービス、Remoting、およびREST APIを使用してAEM Formsをプログラムで呼び出す方法について説明します。
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
source-wordcount: '349'
ht-degree: 0%

---

# API {#invoking-aem-forms-using-apis}を使用したAEM Formsの呼び出し

Adobe Experience Manager Formsは、共有インフラストラクチャ内で動作するサービスで構成される、J2EEベースのエンタープライズソフトウェアです。 サービス操作は、通常、ドキュメントを使用または生成します。 AEM Formsを使用すると、フォームワークフローと電子フォーム、ドキュメントセキュリティ、ドキュメント生成を、統合されたまとまったサービスのセットで組み合わせることができます。 これらのサービスは、ファイアウォールの内外からアクセスできます。

クライアントアプリケーションは、Java API、Webサービス、Remoting、およびRESTを使用して、AEM Formsサービスをプログラムで呼び出すことができます。 管理コンソールを使用して、プログラムによってAEM Formsサービスを呼び出すことでサービスを公開するエンドポイントを設定できます。 デフォルトでは、ほとんどのサービスは、リモート、Java、Webサービスの各エンドポイントを公開するように事前に設定されています。

ビジネス要件によって、使用する呼び出し方法が決まります。 例えば、Java APIを使用して、JavaエンティティやメッセージBeanなどのJavaエンタープライズアプリケーションにAEM Forms機能を統合できます。 同様に、Webサービスを使用して、AEM Forms機能を.NETプロジェクト（または、Webサービス標準をサポートする開発環境で開発された他のプロジェクト）に統合できます。

サービスを実行するには、Enterprise JavaBeans™ (EJB)でJ2EEコンテナが必要となるのと同様に、サービスコンテナが必要です。 AEM Formsには、サービスコンテナの1つの実装のみが含まれています。 サービスコンテナは、サービスのデプロイや、すべてのリクエストが正しいサービスに送信されることなど、サービスの有効期間を管理する役割を担います。 また、サービスが使用または生成するドキュメントも管理します。

>[!NOTE]
>
>AEM formsによるプログラミングには、監視フォルダーや電子メールを使用したAEM Formsの呼び出し方法に関する情報は含まれていません。
