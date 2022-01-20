---
title: サービスコンテナ
seo-title: Service container
description: サービスコンテナの機能の詳細を説明します。 また、この記事では、AEM Formsサービスをプログラムで呼び出す様々な方法についても説明します。
seo-description: Learn more about the functionalities of service container. In addition, the article also describes the different ways in which you can programmatically invoke AEM Forms services.
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: development-tools, coding
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
role: Developer
exl-id: 92351e2d-1928-4bc4-aaff-d557ee09d1ee
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 2%

---

# サービスコンテナ {#service-container}

サービスコンテナに配置されたAEM Formsサービス（Encryption サービス、長期間有効なプロセス、短時間有効なプロセスなどの標準サービスを含む）は、EJB プロバイダーなどの様々なプロバイダーを使用して呼び出すことができます。 EJB プロバイダーを使用すると、RMI/IIOP 経由でAEM Formsサービスを呼び出すことができます。 Web サービスプロバイダーは、SOAP/HTTP や SOAP/JMS などの標準を使用して、Web サービス (WSDL Generation) としてサービスを公開します。

次の表に、AEM Forms Services をプログラムで呼び出す様々な方法を示します。

<table>
 <thead>
  <tr>
   <th><p>呼び出しメソッド</p></th> 
   <th><p>説明</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr>
   <td><p>リモート統合</p></td> 
   <td><p>リモート統合により、Flexクライアントがサービス操作を呼び出す機能が提供されます。 ( <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し</a>.)</p></td> 
  </tr> 
  <tr>
   <td><p>Java API</p></td> 
   <td><p>Java API は、AEM Formsサービスを呼び出すことができます。 Java API は、クライアントライブラリと Java 呼び出し API に整理されています。 ( <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Java API を使用したAEM Formsの呼び出し</a>.)</p></td> 
  </tr> 
  <tr>
   <td><p>Web サービス</p></td> 
   <td><p>AEM Formsは、SOAP/HTTP などの Web サービス標準をサポートしています。 W3C で定義された Web サービス標準に準拠した WSDL を使用して、サービスを Web サービスとして公開できます。</p><p>サービスは、.NET Framework や Sun™ Web Services SDK など、任意の Web サービススタックから呼び出すことができます。 ( <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Web サービスを使用したAEM Formsの呼び出し</a>.)</p></td> 
  </tr> 
  <tr>
   <td><p>REST リクエスト</p></td> 
   <td><p>AEM Formsは、REST リクエストをサポートします。 サービスは、サービスページから直接HTMLできます。 ( <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">REST リクエストを使用したAEM Formsの呼び出し</a>.)</p></td> 
  </tr> 
 </tbody> 
</table>

次の図は、AEM Forms Services をプログラムで呼び出す様々な方法を視覚的に示しています。

>[!NOTE]
>
>AEM Forms SDK を使用してAEM Formsサービスを呼び出すクライアントアプリケーションを作成するほか、サービスコンテナにデプロイできるコンポーネントを作成することもできます。 例えば、プロセスで使用できるカスタムデータ型を含む Bank コンポーネントを作成できます。 つまり、次のようなデータタイプを作成できます。 `com.adobe.idp.BankAccount`. 次に、 `com.adobe.idp.BankAccount` インスタンスを使用します。

サービスコンテナには次の機能が用意されています。

* 異なるメソッドを使用してAEM Formsサービスを呼び出すことを許可します。 サービスを設定するには、エンドポイントを設定して、すべてのメソッドで呼び出せるようにします。リモート処理、Java API、Web サービスおよび REST。 ( [エンドポイントのプログラム管理](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints).)
* メッセージを呼び出し要求と呼ばれる正規化された形式に変換します。 呼び出し要求は、クライアントアプリケーション（または他のサービス）から、サービスコンテナ内のサービスに送信されます。 呼び出し要求には、呼び出すサービスの名前や、操作の実行に必要なデータ値などの情報が含まれます。 多くのサービスでは、操作を実行するためにドキュメントが必要です。 したがって、呼び出し要求には通常、PDFデータ、XDP データ、XML データなどのドキュメントが含まれます。
* 呼び出し要求を適切なサービスにルーティングします（呼び出すサービスの名前は呼び出し要求の一部です）。
* 呼び出し元が、指定されたサービス操作を呼び出す権限を持っているかどうかを判断するなどのタスクを実行します。 呼び出し要求には、有効なAEM forms のユーザー名とパスワードが含まれている必要があります。

   呼び出し要求をサービスに送信する方法は異なります。 また、必要な入力値をサービスに送信する方法は異なります。 例えば、Java API を使用して、サービスドキュメントを必要とするサービスを呼び出すとします。PDFドキュメント。 対応する Java メソッドには、パラメータードキュメントを受け入れるPDFーが含まれます。 この場合、パラメーターのデータ型は `com.adobe.idp.Document`. ( [Java API を使用してAEM Formsサービスにデータを渡す](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

   監視フォルダーを使用してサービスを呼び出すと、設定済みの監視フォルダーにファイルを配置すると、呼び出し要求が送信されます。 電子メールを使用してサービスを呼び出す場合、電子メールメッセージが設定済みのインボックスに届くと、呼び出し要求がサービスに送信されます。

   サービスコンテナは、操作の実行後に呼び出し応答を返します。 呼び出し応答には、操作の結果などの情報が含まれます。 例えば、操作によってPDFドキュメントが変更された場合、呼び出し応答には変更されたPDFドキュメントが含まれます。 操作に失敗した場合、呼び出し応答にはエラーメッセージが含まれます。

   呼び出し応答は、呼び出し要求が送信されるのと同じ方法で取得できます。 つまり、呼び出し要求が Java API を使用して送信された場合、呼び出し応答は Java API を使用して取得できます。 例えば、操作によってPDF文書が変更されたとします。 サービスを呼び出した JavaPDFの戻り値を取得することで、変更されたメソッドドキュメントを取得できます。

   長期間有効なプロセスが呼び出されると、呼び出し応答には呼び出し要求に関連付けられた識別子値が含まれます。 この識別子の値を使用して、後でプロセスのステータスを確認できます。 例えば、MortgageLoan の長期間有効なサービスを考えてみましょう。 識別子の値を使用して、プロセスが正常に完了したかどうかを確認できます。 （[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)を参照。）

   次の図は、サービスを呼び出す（Java API を使用する）クライアントアプリケーションを示しています。

   クライアントアプリケーションがサービスを呼び出すと、次の 3 つのイベントが発生します。

   1. クライアントアプリケーションが呼び出し要求をサービスに送信します。
   1. サービスは、呼び出し要求で指定された操作を実行します。
   1. サービスコンテナは、クライアントアプリケーションに呼び出し応答を返します。

**関連トピック**

[AEM Formsプロセスについて](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Java API を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Web サービスを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[REST リクエストを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
