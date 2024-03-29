---
title: エンドポイントの種類
seo-title: Types of endpoints
description: 様々な種類のエンドポイントについて説明します。
seo-description: Learn about the different types of endpoints.
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
exl-id: 7c6b9b6c-d4b5-46a8-8a6a-3b8802ac392d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 59%

---

# エンドポイントの種類 {#types-of-endpoints}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

サービスを使用する前に、エンドポイントを設定して有効にする必要があります。 エンドポイントは、サービスの呼び出し方法を指定します。

>[!NOTE]
>
>Workbench では、エンドポイントはスタートポイントと呼ばれます。

次の種類のエンドポイントをサービスに追加できます。 一部のサービスがすべてのエンドポイントをサポートしているわけではありません。

**メール**：1 つ以上の添付ファイルがあるメールメッセージを指定されたメールアカウントに送信することで、ユーザーがサービスを呼び出せるようにします。メールエンドポイントを設定する前に、必要なメールアカウントを設定する必要があります（メールエンドポイントの設定を参照）。

**監視フォルダー**：ファイルを定義済みの間隔でスキャンされるフォルダーに配置することで、ユーザーがサービスを呼び出せるようにします。（監視フォルダーエンドポイントの設定を参照）。

**TaskManager**：Workspace ユーザーがサービスを呼び出せるようにします。

**Remoting** ：Flex で作成されたアプリケーションから AEM forms Remoting（AEM forms では非推奨）を使用してサービスを呼び出せるようにします。リモートエンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。 エンドポイントと同じ名前のFlex宛先が作成され、Flexクライアントは、この宛先を指すリモートオブジェクトを作成して、関連するサービスの操作を呼び出すことができます。

**SOAP** ：AEM Forms プログラミング API を使用して開発されたクライアントアプリケーションから、SOAP モードを使用してサービスを呼び出せるようにします。SOAP エンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。

**注意**：*Adobe Acrobat または Adobe Reader でドキュメントを表示しているときに SOAP エンドポイントが使用されると、Document Security ドキュメントからセキュリティが除去される可能性があります。LCRM ドキュメントで SOAP エンドポイントを無効にする方法について詳しくは、「[Document Security ドキュメントの SOAP エンドポイントの無効化](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*」を参照してください。

**EJB**：AEM forms プログラミング API を使用して開発されたクライアントアプリケーションから、Enterprise JavaBeans（EJB）モードを使用してサービスを呼び出せるようにします。EJB エンドポイントは、アクティブ化された各サービスに対して自動的に作成されます。

**WSDL** ：AEM Forms プログラミング API を使用して開発されたクライアントアプリケーションから、Web サービス記述言語（WSDL）を使用してサービスを呼び出せるようにします。コア設定ページには、AEM Forms に属するすべてのサービスで WSDL の生成を有効にするオプションが含まれています。（一般的な AEM Forms の設定を参照）。

**REST**：Representational State Transfer（REST）要求で呼び出せるように、Workbench で作成したプロセスを設定できます。REST リクエストは、HTMLページから送信されます。 つまり、REST リクエストを使用して、Web ページから直接AEM forms プロセスを呼び出すことができます。

電子メール、タスクマネージャー、監視フォルダーおよびリモートの各エンドポイントでは、サービスの特定の操作のみが公開されます。 これらのエンドポイントを追加するには、サービスを呼び出すメソッドの選択、設定パラメーターの設定、入力および出力パラメーターのマッピングの指定をおこなう 2 番目の設定手順が必要です。
