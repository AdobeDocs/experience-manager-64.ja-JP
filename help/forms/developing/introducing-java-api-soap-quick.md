---
title: Java API QuickStart の概要
seo-title: Introducing Java API QuickStart
description: Java API クイックスタートプログラムを使用すると、AEM Forms Services とやり取りするプログラムの開発を迅速におこなうことができます。 プロジェクト内で Java API クイックスタートプログラムを出発点として使用し、カスタマイズすることができます。
seo-description: Java API Quick Start programs help you expedite the development of programs that interact with AEM Forms services. You can use the Java API Quick Start programs in your project as a starting point and customize it.
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: development-tools, develop
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
role: Developer
exl-id: 8a3f2eb9-d686-49d4-baa4-c0921622d01a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Java API クイックスタートの概要 {#introducing-java-api-quickstart}

AdobeAEM Forms API クイックスタートは、AEM Formsサービスとやり取りするプログラムの開発に向けた取り組みを加速するのに役立ちます。 *クイックスタート*&#x200B;は、独自のプロジェクトにコピーして貼り付け、出発点として使用できる完全なプログラムです。 クイックスタートを実行して、動作を確認し、独自のニーズに合わせて変更できます。

AEM Formsの操作は、AEM Formsの厳密に型指定された API を使用して実行できます。接続モードは、SOAP に設定する必要があります。

Java の強く型付けされた API クイックスタートには、Java アプリケーションの実行に必要な JAR ファイルのリストが表示されます。 ほとんどの Java クイックスタートは、内で実行されるコンソールアプリケーションです `main`. ただし、Forms Java の強く型指定された API クイックスタートは、Web アプリケーション内で実行する Java サーブレットとして実装されます。

JAR ファイルのリストは、クイックスタートの先頭にあるコメントセクションにあります。 例えば、次のコメントは Output クイックスタートにあり、各 Java クイックスタートにある一般的な JAR ファイルリストです。

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-output-client.jar 
     * 2. adobe--client.jar 
     * 3. adobe-usermanager-client.jar 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common 
     * 
     * The adobe-utilities.jar file is located in the following path: 
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss 
     * 
     * The jboss-client.jar file is located in the following path: 
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client 
     * 
     * If you want to invoke a remote AEM Forms instance and there is a 
     * firewall between the client application and AEM Forms, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include additional JAR files located in the following  
     * path 
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty 
     * 
     * For information about the SOAP  
     * mode and the additional JAR files that need to be included,  
     * see "Setting connection properties" in Programming  
     * with AEM Forms 
     * 
     * For complete details about the location of the AEM Forms JAR files,  
     * see "Including AEM Forms library files" in Programming  
     * with AEM Forms 
     */
```

## 複数のサービスのクイックスタート {#multiple-services-quick-start}

ほとんどのクイックスタートは、 *AEM Formsを使用したプログラミング* 操作を実行するには、特定のサービスを呼び出します。 ただし、一部のクイックスタートでは、特定のワークフローを実行するために複数のAEM Formsサービスが呼び出されます。 次のリストは、複数のAEM Formsサービスを呼び出す Java クイックスタートを示しています。

[クイックスタート（SOAP モード）:Java API を使用してAEM Formsリポジトリ内のドキュメントを Output サービスに渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) （Repository および Output サービスを呼び出します）

[クイックスタート（SOAP モード）:Java API を使用して、フラグメントに基づくPDFドキュメントを作成する](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) （Assembler および Output サービスを呼び出します）

[クイックスタート（SOAP モード）:Java API を使用した、送信済み XML データを使用したPDFドキュメントの作成](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (Forms、Output および Document Management サービスを呼び出します )

[クイックスタート（SOAP モード）:Java API を使用してForms Service にドキュメントを渡す](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (Formsおよび Document Management サービスを呼び出します )

[クイックスタート（SOAP モード）:Java API を使用した XFA ベースフォームのデジタル署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (Formsおよび Signature サービスを呼び出します )

[クイックスタート（SOAP モード）:Java API を使用した役割と権限の管理](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) （ DirectoryManager および AuthorizationManager サービスを呼び出します）。

[クイックスタート（SOAP モード）:Java API を使用して Output Service にドキュメントを渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) （Output および Document Management サービスを呼び出す）

>[!NOTE]
>
>「AEM Formsのプログラミング」にあるクイックスタートは、JBoss® Application Server とMicrosoft® Windows®オペレーティングシステムにデプロイされるAEM Formsに基づいています。 ただし、UNIX®などの別のオペレーティング・システムを使用している場合は、Windows 固有のパスを、該当するオペレーティング・システムでサポートされているパスに置き換えます。 同様に、別の J2EE アプリケーションサーバーを使用する場合は、有効な接続プロパティを必ず指定してください。 （[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）

>[!NOTE]
>
>ほとんどの Web サービスクイックスタートは C#で記述され、.NET フレームワークを使用します。 ただし、SOAP 標準をサポートする任意の開発環境でAEM Formsサービスを呼び出すことができるクライアントアプリケーションロジックを作成することができます。 ( [Web サービスを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
