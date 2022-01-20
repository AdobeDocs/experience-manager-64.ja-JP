---
title: Remoting を使用したAEM Formsの呼び出し
seo-title: Invoking AEM Forms using Remoting
description: Remoting を使用してAEM Formsプロセスを呼び出し、Workbench で作成されたプロセスを呼び出します。 Flexで作成されたクライアントアプリケーションからAEM Formsプロセスを呼び出すことができます。
seo-description: Use Remoting to invoke an AEM Forms process to invoke processes created in Workbench. You can invoke a AEM Forms process from a client application built with Flex.
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
role: Developer
exl-id: de8ba694-0b68-4442-bd50-5ba6d845749c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '4621'
ht-degree: 1%

---

# Remoting を使用したAEM Formsの呼び出し {#invoking-aem-forms-using-remoting}

Workbench で作成されたプロセスは、Remoting を使用して呼び出すことができます。 つまり、Flexで作成されたクライアントアプリケーションからAEM Formsプロセスを呼び出すことができます。 この機能は、データサービスに基づいています。

>[!NOTE]
>
>リモート処理を使用する場合は、AEM Formsサービスとは異なり、Workbench で作成されたプロセスを呼び出すことをお勧めします。 ただし、AEM Formsサービスを直接呼び出すことはできます。 (AEM Formsデベロッパーセンターにある「リモート処理を使用したPDFドキュメントの暗号化」を参照 )。

>[!NOTE]
>
>AEM Formsサービスが匿名アクセスを許可するように設定されていない場合、Flexクライアントからのリクエストによって Web ブラウザーの課題が発生します。 ユーザーは、ユーザー名とパスワードの資格情報を入力する必要があります。

次のAEM Formsの短時間のみ有効なプロセス。 `MyApplication/EncryptDocument`を呼び出すには、 Remoting を使用します。 ( このプロセスの入力値や出力値などについて詳しくは、 [短時間のみ有効なプロセスの例](/help/forms/developing/aem-forms-processes.md).)

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>Flexアプリケーションを使用してAEM Formsプロセスを呼び出すには、リモートエンドポイントが有効になっていることを確認します。 プロセスをデプロイすると、デフォルトでリモートエンドポイントが有効になります。

このプロセスを呼び出すと、次のアクションが実行されます。

1. 入力値として渡されたPDFドキュメントを取得します。 このアクションは `SetValue` 操作に基づいています。入力パラメーターの名前は `inDoc` で、そのデータタイプは `document`. ( `document` データタイプは、Workbench 内で使用できるデータタイプです )。
1. PDF ドキュメントをパスワードで暗号化します。このアクションは `PasswordEncryptPDF` 操作に基づいています。このプロセスの出力値の名前は、 `outDoc` は、パスワードで暗号化されたPDF・ドキュメントを表します。 outDoc のデータタイプは次のとおりです。 `document`.
1. パスワードで暗号化されたPDF・ドキュメントをPDF・ファイルとしてローカル・ファイル・システムに保存します。 このアクションは `WriteDocument` 操作に基づいています。

>[!NOTE]
>
>この `MyApplication/EncryptDocument` プロセスは、既存のAEM Formsプロセスに基づいていません。 コード例に従って、という名前のプロセスを作成します。 `MyApplication/EncryptDocument` Workbench の使用を参照してください。

>[!NOTE]
>
>Remoting を使用して長期間有効なプロセスを呼び出す方法について詳しくは、 [人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

**関連トピック**

[AEM Forms Flexライブラリファイルの取り込み](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[(AEM forms では非推奨 )AEM Forms Remoting を使用したドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Remoting (AEM forms では非推奨 ) を使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで作成されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[リモート処理を使用したカスタムコンポーネントサービスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[人間中心の長期間有効なプロセスを呼び出す、Flexで構築されたクライアントアプリケーションの作成](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[HTTP トークンを使用した SSO 認証を実行するFlash Builderアプリケーションの作成](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

Flexグラフコントロールにプロセスデータを表示する方法について詳しくは、 [FlexグラフでのAEM Formsプロセスデータの表示](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html).

>[!NOTE]
>
>*crossdomain.xml ファイルを適切な場所に配置するようにしてください。 例えば、JBoss にAEM Formsをデプロイした場合は、次の場所にこのファイルを配置します。 &lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## AEM Forms Flexライブラリファイルの取り込み {#including-the-aem-forms-flex-library-file}

Remoting を使用してAEM Formsプロセスをプログラムで呼び出すには、adobe-remoting-provider.swc ファイルをFlexプロジェクトのクラスパスに追加します。 この SWC ファイルは次の場所にあります。

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   ここで、*install_directory*> は、AEM Formsがインストールされているディレクトリです。

**関連トピック**

[(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[(AEM forms では非推奨 )AEM Forms Remoting を使用したドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Remoting (AEM forms では非推奨 ) を使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで作成されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## リモート処理を使用したドキュメントの処理 {#handling-documents-with-remoting}

AEM Formsで使用される非プリミティブ Java タイプの中で最も重要なものの 1 つは、 `com.adobe.idp.Document` クラス。 ドキュメントは、通常、AEM Forms操作を呼び出すために必要です。 主にPDFドキュメントですが、SWF、HTML、XML、DOC ファイルなど、他のドキュメントタイプを含めることができます。 ( [Java API を使用してAEM Formsサービスにデータを渡す](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Flexで作成されたクライアントアプリケーションは、ドキュメントを直接リクエストできません。 例えば、Adobe Readerを起動して、PDFファイルを生成する URL をリクエストすることはできません。 PDFやMicrosoft Word ドキュメントなどのドキュメントタイプのリクエストは、URL の結果を返します。 URL のコンテンツを表示するのはクライアントの責任です。 Document Management サービスは、URL およびコンテンツタイプ情報の生成に役立ちます。 XML ドキュメントのリクエストは、結果の完全な XML ドキュメントを返します。

### ドキュメントを入力パラメーターとして渡す {#passing-a-document-as-an-input-parameter}

Flexで作成されたクライアントアプリケーションは、ドキュメントをAEM Formsプロセスに直接渡すことができません。 代わりに、クライアントアプリケーションは `mx.rpc.livecycle.DocumentReference` ActionScriptクラスを使用して、 `com.adobe.idp.Document` インスタンス。 Flexクライアントアプリケーションには、 `DocumentReference` オブジェクト：

* ドキュメントがサーバー上にあり、そのファイルの場所がわかっている場合は、DocumentReference オブジェクトの referenceType プロパティを REF_TYPE_FILE に設定します。 次の例に示すように、 fileRef プロパティをファイルの場所に設定します。

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* 文書がサーバー上にあり、その URL がわかっている場合は、DocumentReference オブジェクトの referenceType プロパティを REF_TYPE_URL に設定します。 次の例に示すように、url プロパティを URL に設定します。

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* クライアントアプリケーションのテキスト文字列から DocumentReference オブジェクトを作成するには、DocumentReference オブジェクトの referenceType プロパティを REF_TYPE_INLINE に設定します。 次の例に示すように、 text プロパティを、オブジェクトに含めるテキストに設定します。

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server’s default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* ドキュメントがサーバー上にない場合は、リモートアップロードサーブレットを使用して、ドキュメントをAEM Formsにアップロードします。 AEM Formsの新機能は、セキュリティで保護されたドキュメントをアップロードする機能です。 安全なドキュメントをアップロードする場合は、「Document Upload Application User」のロールを持つユーザーを使用する必要があります。 このロールがないと、ユーザーは保護されたドキュメントをアップロードできません。 セキュアなドキュメントをアップロードする場合は、シングルサインオンを使用することをお勧めします。 ( [リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).)

   >[!NOTE]
   安全でないドキュメントのアップロードを許可するようにAEM Formsが設定されている場合は、ドキュメントのアップロードアプリケーションユーザーロールを持たないユーザーを使用してドキュメントをアップロードできます。 ユーザーは、ドキュメントのアップロード権限を持つこともできます。 ただし、AEM Formsが保護されたドキュメントのみを許可するように設定されている場合は、ユーザーに「ドキュメントのアップロードアプリケーションユーザー」ロールまたは「ドキュメントのアップロード」権限があることを確認します。 詳しくは、 [安全なドキュメントと安全でないドキュメントを受け入れるためのAEM Formsの設定](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)*.

   指定したアップロード URL には、標準のFlashアップロード機能を使用します。 `https://SERVER:PORT/remoting/lcfileupload`. その後、 `DocumentReference` 型の入力パラメーターがある場合は常にオブジェクト `Document` が期待されます
   ` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`リモート処理クイックスタートは、リモート処理アップロードサーブレットを使用して、PDFファイルをに渡します。 `MyApplication/EncryptDocument`プロセス。 ( [AEM Forms Remoting (AEM forms では非推奨 ) を使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

```java
 
private
function startUpload(): void  { 
 fileRef.addEventListener(Event.SELECT, selectHandler); 
 fileRef.addEventListener("uploadCompleteData", completeHandler); 
 try  { 
  var success: Boolean = fileRef.browse(); 
 }  
 catch (error: Error)  { 
  trace("Unable to browse for files."); 
 } 
}   
private
function selectHandler(event: Event): void { 
 var request: URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try  { 
  fileRef.upload(request); 
 }  
 catch (error: Error)  { 
  trace("Unable to upload file."); 
 } 
}  
private
function completeHandler(event: DataEvent): void  { 
 var params: Object = new Object(); 
 var docRef: DocumentReference = new DocumentReference(); 
 docRef.url = event.data as String; 
 docRef.referenceType = DocumentReference.REF_TYPE_URL; 
}
```

リモート処理クイックスタートは、リモート処理アップロードサーブレットを使用して、PDFファイルをに渡します。 `MyApplication/EncryptDocument`プロセス。 ( [AEM Forms Remoting (AEM forms では非推奨 ) を使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

### クライアントアプリケーションにドキュメントを渡す {#passing-a-document-back-to-a-client-application}

クライアントアプリケーションがタイプのオブジェクトを受け取る `mx.rpc.livecycle.DocumentReference` ( `com.adobe.idp.Document` インスタンスを出力パラメーターとして使用します。 クライアントアプリケーションは Java ではなくActionScriptオブジェクトを扱うので、Java ベースの Document オブジェクトをFlexクライアントに渡すことはできません。 代わりに、サーバーはドキュメントの URL を生成し、その URL をクライアントに渡します。 この `DocumentReference` オブジェクトの `referenceType` プロパティは、コンテンツが `DocumentReference` オブジェクトを使用するか、 `DocumentReference.url` プロパティ。 この `DocumentReference.contentType` プロパティは、ドキュメントの種類を指定します。

**関連トピック**

[(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[AEM Forms Flexライブラリファイルの取り込み](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[AEM Forms Remoting (AEM forms では非推奨 ) を使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで作成されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## リモート処理を使用して保護されていないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

Flexで構築されたアプリケーションからAEM Formsプロセスを呼び出すには、次のタスクを実行します。

1. の作成 `mx:RemoteObject` インスタンス。
1. の作成 `ChannelSet` インスタンス。
1. 必要な入力値を渡します。
1. 戻り値を処理します。

>[!NOTE]
この節では、安全でないドキュメントをアップロードするようにAEM Formsが設定されている場合に、AEM Formsプロセスを呼び出してドキュメントをアップロードする方法について説明します。 AEM Formsプロセスを呼び出し、安全なドキュメントをアップロードする方法、および安全なドキュメントと安全でないドキュメントを受け入れるようにAEM Formsを設定する方法について詳しくは、 [リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).

**mx:RemoteObject インスタンスの作成**

次の項目を作成します。 `mx:RemoteObject` インスタンスを使用して、Workbench で作成されたAEM Formsプロセスを呼び出します。 を作成するには、以下を実行します。 `mx:RemoteObject` インスタンスに、次の値を指定します。

* **id:** の名前 `mx:RemoteObject` 呼び出すプロセスを表すインスタンス。
* **宛先：** 呼び出すAEM Formsプロセスの名前。 例えば、 `MyApplication/EncryptDocument` プロセス、指定 `MyApplication/EncryptDocument`.
* **結果：** 結果を処理するFlexメソッドの名前。

内 `mx:RemoteObject` タグ、指定 `<mx:method>` プロセスの呼び出しメソッドの名前を指定するタグ。 通常、Forms呼び出しメソッドの名前は次のとおりです。 `invoke`.

次のコードの例では、 `mx:RemoteObject` を呼び出すインスタンス `MyApplication/EncryptDocument` プロセス。

```as3
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);"> 
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/> 
      </mx:RemoteObject>
```

**AEM Formsへのチャネルの作成**

クライアントアプリケーションは、次のActionScriptの例に示すように、MXMLまたはActionScriptでチャネルを指定することで、AEM Formsを呼び出すことができます。 チャネルは、 `AMFChannel`, `SecureAMFChannel`, `HTTPChannel`または `SecureHTTPChannel`.

```as3
     ... 
     private function refresh():void{ 
         var cs:ChannelSet= new ChannelSet(); 
         cs.addChannel(new AMFChannel("my-amf",  
             "https://yourlcserver:8080/remoting/messagebroker/amf")); 
         EncryptDocument.setCredentials("administrator", "password"); 
         EncryptDocument.channelSet = cs; 
     } 
     ...
```

を `ChannelSet` インスタンスから `mx:RemoteObject` インスタンスの `channelSet` フィールドに入力します（前のコードの例で示したように）。 一般に、channel クラスは、 `ChannelSet.addChannel` メソッド。

**入力値を渡す**

Workbench で作成されたプロセスは、0 個以上の入力パラメーターを受け取り、出力値を返すことができます。 クライアントアプリケーションは、 `ActionScript` AEM Formsプロセスに属するパラメーターに対応するフィールドを持つオブジェクト。 短時間有効なプロセス。 `MyApplication/EncryptDocument`には次の 1 つの入力パラメーターが必要です： `inDoc`. プロセスによって公開される操作の名前は次のとおりです。 `invoke` （短時間のみ有効なプロセスのデフォルト名） ( [(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

次のコードの例では、PDFドキュメントを `MyApplication/EncryptDocument` プロセス：

```as3
     ... 
     var params:Object = new Object(); 
      
     //Document is an instance of DocumentReference 
     //that store an unsecured PDF document 
     params["inDoc"] = pdfDocument; 
      
     // Invoke an operation synchronously: 
     EncryptDocument.invoke(params); 
     ...
```

このコードの例では、 `pdfDocument` は `DocumentReference` 保護されていないPDFドキュメントを含むインスタンス。 詳しくは、 `DocumentReference`を参照してください。 [(AEM forms では非推奨 )AEM Forms Remoting を使用したドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting).

**特定のバージョンのサービスの呼び出し**

を使用して、特定のバージョンのFormsサービスを呼び出すことができます `_version` パラメーターを指定してください。 例えば、 `MyApplication/EncryptDocument` サービス：

```as3
 var params:Object = new Object(); 
 params["inDoc"] = pdfDocument; 
 params["_version"] = "1.2" 
 var token:AsyncToken = echoService.echoString(params);
```

この `version` パラメーターは、1 つのピリオドを含む文字列である必要があります。 期間の左側、メジャーバージョン、右側、マイナーバージョンの値は整数にする必要があります。 このパラメーターを指定しない場合、head のアクティブバージョンが呼び出されます。

**戻り値の処理**

AEM Formsプロセスの出力パラメーターは、次の例に示すように、ActionScriptオブジェクトに逆シリアル化され、クライアントアプリケーションは特定のパラメーターを名前で抽出します。 ( `MyApplication/EncryptDocument` プロセス名 `outDoc`.)

```as3
     ... 
     var res:Object = event.result; 
     var docRef:DocumentReference = res["outDoc"] as DocumentReference; 
     ...
```

**MyApplication/EncryptDocument プロセスの呼び出し**

を呼び出すことができます。 `MyApplication/EncryptDocument` 次の手順を実行してプロセスを実行します。

1. の作成 `mx:RemoteObject` インスタンスをActionScriptまたはMXML経由で使用できます。 mx:RemoteObject インスタンスの作成を参照してください。
1. の設定 `ChannelSet` AEM Formsと通信し、それを `mx:RemoteObject` インスタンス。 詳しくは、 AEM Formsへのチャネルの作成を参照してください。
1. チャネルセットの `login` メソッドまたはサービスの `setCredentials` メソッドを使用して、ユーザー識別子の値とパスワードを指定します。 ( [シングルサインオンの使用](invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. 次の項目に `mx.rpc.livecycle.DocumentReference` を `MyApplication/EncryptDocument` プロセス。 ( [ドキュメントを入力パラメーターとして渡す](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter).)
1. を呼び出してPDFドキュメントを暗号化する `mx:RemoteObject` インスタンスの `invoke` メソッド。 パス `Object` 入力パラメーター ( セキュリティで保護されていないPDFドキュメント ) を格納する 入力値を渡すを参照してください。
1. プロセスから返される、パスワードで暗号化されたPDFドキュメントを取得します。 戻り値の処理を参照してください。

[クイックスタート：AEM Forms Remoting (AEM forms では非推奨 ) を使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## Flexで作成されたクライアントアプリケーションの認証 {#authenticating-client-applications-built-with-flex}

AEM forms User Manager でFlexアプリケーションから Remoting 要求を認証する方法はいくつかあります。これには、中央のログインサービスを使用したAEM Formsのシングルサインオン、基本認証、カスタム認証などがあります。 シングルサインオンも匿名アクセスも有効になっていない場合、リモート処理リクエストを実行すると、基本認証（デフォルト）とカスタム認証のどちらかが実行されます。

基本認証は、Web アプリケーションコンテナからの標準の J2EE 基本認証に基づいています。 基本認証の場合、HTTP 401 エラーによってブラウザーの課題が発生します。 つまり、RemoteObject を使用してFormsアプリケーションに接続しようとし、Flexアプリケーションからまだログインしていない場合、ブラウザーはユーザー名とパスワードの入力を求めるプロンプトを表示します。

カスタム認証の場合、サーバーは認証が必要であることを示す障害をクライアントに送信します。

>[!NOTE]
HTTP トークンを使用した認証の実行について詳しくは、 [HTTP トークンを使用した SSO 認証を実行するFlash Builderアプリケーションの作成](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens).

### カスタム認証の使用 {#using-custom-authentication}

管理コンソールでカスタム認証を有効にするには、リモートエンドポイントで認証方法を「基本」から「カスタム」に変更します。 カスタム認証を使用する場合、クライアントアプリケーションは `ChannelSet.login` ログイン方法と `ChannelSet.logout` メソッドを使用してログアウトします。

>[!NOTE]
以前のリリースのAEM Formsでは、 `RemoteObject.setCredentials` メソッド。 この `setCredentials` メソッドは、コンポーネントがサーバーへの接続を最初に試みるまで、資格情報を実際にサーバーに渡しませんでした。 したがって、コンポーネントが障害イベントを発行した場合、その障害が認証エラーによって発生したか、別の理由で発生したかを確認することはできません。 この `ChannelSet.login` メソッドは、呼び出し時にサーバーに接続し、認証の問題をすぐに処理できるようにします。 ただし、 `setCredentials` メソッドの場合は、 `ChannelSet.login` メソッド。

複数の宛先で同じチャネルを使用でき、対応する ChannelSet オブジェクトを使用できるので、1 つの宛先にログインすると、同じチャネルまたはチャネルを使用する他の宛先にユーザーがログインします。 2 つのコンポーネントが同じ ChannelSet オブジェクトに異なる資格情報を適用する場合は、最後に適用された資格情報が使用されます。 複数のコンポーネントが同じ認証済み ChannelSet オブジェクトを使用している場合、 `logout` メソッドは、すべてのコンポーネントを宛先からログアウトします。

次の例では、 `ChannelSet.login` および `ChannelSet.logout` メソッドと RemoteObject コントロールの両方を使用します。 このアプリケーションは、次のアクションを実行します。

* を作成します。 `ChannelSet` オブジェクトを `creationComplete` 次に示すように、 `RemoteObject` コンポーネント
* 認証情報を `ROLogin` Button click イベントに応答する関数
* RemoteObject コンポーネントを使用して、Button click イベントに応答して String をサーバーに送信します。 サーバーが同じ String を RemoteObject コンポーネントに返します
* RemoteObject コンポーネントの result イベントを使用して、 TextArea コントロールに String を表示します
* を呼び出してサーバーからログアウトします。 `ROLogout` Button click イベントに応答する関数

```as3
 <?xml version=”1.0”?> 
 <!-- security/SecurityConstraintCustom.mxml --> 
 <mx:Application xmlns:mx=”https://www.adobe.com/2006/mxml” width=”100%” 
     height=”100%” creationComplete=”creationCompleteHandler();”> 
  
     <mx:Script> 
         <![CDATA[ 
             import mx.controls.Alert; 
             import mx.messaging.config.ServerConfig; 
             import mx.rpc.AsyncToken; 
             import mx.rpc.AsyncResponder; 
             import mx.rpc.events.FaultEvent; 
             import mx.rpc.events.ResultEvent; 
             import mx.messaging.ChannelSet; 
  
             // Define a ChannelSet object. 
             public var cs:ChannelSet; 
  
             // Define an AsyncToken object. 
             public var token:AsyncToken; 
  
             // Initialize ChannelSet object based on the  
             // destination of the RemoteObject component. 
             private function creationCompleteHandler():void { 
                 if (cs == null) 
                 cs = ServerConfig.getChannelSet(remoteObject.destination);                     
             } 
  
             // Login and handle authentication success or failure.  
             private function ROLogin():void { 
                 // Make sure that the user is not already logged in. 
                 if (cs.authenticated == false) { 
                     token = cs.login(“sampleuser”, “samplepassword”); 
                     // Add result and fault handlers. 
                     token.addResponder(new AsyncResponder(LoginResultEvent, 
                     LoginFaultEvent)); 
                 } 
             } 
  
             // Handle successful login. 
             private function LoginResultEvent(event:ResultEvent, 
                 token:Object=null):void  { 
                     switch(event.result) { 
                         case “success”: 
                             authenticatedCB.selected = true; 
                             break; 
                             default: 
                     } 
                 } 
      
                 // Handle login failure. 
                 private function LoginFaultEvent(event:FaultEvent, 
                     token:Object=null):void { 
                         switch(event.fault.faultCode) { 
                             case “Client.Authentication”: 
                                 default: 
                                 authenticatedCB.selected = false; 
                                 Alert.show(“Login failure: “ + event.fault.faultString); 
                     } 
                 } 
  
                 // Logout and handle success or failure. 
                 private function ROLogout():void { 
                     // Add result and fault handlers. 
                     token = cs.logout(); 
                     token.addResponder(new 
                         AsyncResponder(LogoutResultEvent,LogoutFaultEvent)); 
                 } 
  
                 // Handle successful logout. 
                 private function LogoutResultEvent(event:ResultEvent, 
                     token:Object=null):void { 
                         switch (event.result) { 
                             case “success”: 
                                 authenticatedCB.selected = false; 
                                 break; 
                                 default: 
                     } 
                 } 
  
                 // Handle logout failure. 
                 private function LogoutFaultEvent(event:FaultEvent, 
                     token:Object=null):void { 
                         Alert.show(“Logout failure: “ + event.fault.faultString); 
                 } 
                 // Handle message recevied by RemoteObject component. 
                 private function resultHandler(event:ResultEvent):void { 
                     ta.text += “Server responded: “+ event.result + “\n”; 
                 } 
  
                 // Handle fault from RemoteObject component. 
                 private function faultHandler(event:FaultEvent):void { 
                     ta.text += “Received fault: “ + event.fault + “\n”; 
                 } 
             ]]> 
     </mx:Script> 
     <mx:HBox> 
         <mx:Label text=”Enter a text for the server to echo”/> 
         <mx:TextInput id=”ti” text=”Hello World!”/> 
         <mx:Button label=”Login”  
             click=”ROLogin();”/> 
         <mx:Button label=”Echo”   
             enabled=”{authenticatedCB.selected}” 
             click=”remoteObject.echo(ti.text);”/> 
         <mx:Button label=”Logout”  
             click=”ROLogout();”/> 
         <mx:CheckBox id=”authenticatedCB”  
             label=”Authenticated?”  
             enabled=”false”/> 
     </mx:HBox> 
     <mx:TextArea id=”ta” width=”100%” height=”100%”/> 
  
     <mx:RemoteObject id=”remoteObject” 
         destination=”myDest” 
         result=”resultHandler(event);” 
         fault=”faultHandler(event);”/> 
 </mx:Application>
```

この `login` および `logout` メソッドは AsyncToken オブジェクトを返します。 成功した呼び出しを処理する結果イベントには AsyncToken オブジェクトに、失敗を処理する障害イベントにはイベントハンドラを割り当てます。

### シングルサインオンの使用 {#using-single-sign-on}

AEM forms ユーザーは、複数のAEM Forms Web アプリケーションに接続して、タスクを実行できます。 ユーザーが Web アプリケーション間を移動する際に、Web アプリケーションごとに個別にログインする必要が生じることは効率的ではありません。 AEM Formsのシングルサインオンメカニズムを使用すると、ユーザーは 1 回ログインし、任意のAEM Forms Web アプリケーションにアクセスできます。 AEM Formsの開発者はAEM Formsで使用するクライアントアプリケーションを作成できるので、シングルサインオンメカニズムも利用できる必要があります。

各AEM Forms Web アプリケーションは、独自の Web アーカイブ (WAR) ファイルにパッケージ化され、エンタープライズアーカイブ (EAR) ファイルの一部としてパッケージ化されます。 アプリケーションサーバーでは異なる Web アプリケーション間でのセッションデータの共有が許可されないので、AEM Formsでは HTTP Cookie を使用して認証情報を保存します。 認証 Cookie を使用すると、ユーザーはFormsアプリケーションにログインしてから、他のAEM Forms Web アプリケーションに接続することができます。 この手法は、シングルサインオンと呼ばれます。

AEM Forms開発者は、フォームガイド（非推奨）の機能を拡張し、Workspace をカスタマイズするためのクライアントアプリケーションを作成します。 例えば、Workspace アプリケーションはプロセスを開始できます。 次に、クライアントアプリケーションはリモートエンドポイントを使用してFormsサービスからデータを取得します。

AEM Forms Remoting(AEM forms では非推奨 ) を使用してAEM Formsサービスが呼び出されると、クライアントアプリケーションは認証 Cookie をリクエストの一部として渡します。 ユーザーは既に認証されているので、クライアントアプリケーションからAEM Formsサービスに接続するために、追加のログインは必要ありません。

>[!NOTE]
Cookie が無効または見つからない場合、ログインページへの暗黙のリダイレクトはありません。 そのため、匿名サービスを呼び出すことができます。

AEM Formsのシングルサインオンメカニズムを回避するには、独自にログインおよびログアウトするクライアントアプリケーションを記述します。 シングルサインオンメカニズムを回避する場合は、アプリケーションで基本認証またはカスタム認証を使用できます。

このメカニズムではAEM Formsのシングルサインオンメカニズムが使用されないので、認証 Cookie はクライアントに書き込まれません。 ログイン資格情報は、 `ChannelSet` オブジェクトを削除します。 したがって、 `RemoteObject` 同じ `ChannelSet` は、これらの資格情報のコンテキストで作成されます。

### AEM Formsでのシングルサインオンの設定 {#setting-up-single-sign-on-in-aem-forms}

AEM Formsでシングルサインオンを使用するには、一元化されたログインサービスを含む forms ワークフローコンポーネントをインストールします。 ユーザーが正常にログインすると、一元化されたログインサービスはユーザーに認証 Cookie を返します。 Forms Web アプリケーションに対する後続のリクエストにはすべて、 Cookie が含まれます。 Cookie が有効な場合、ユーザーは認証済みと見なされ、再度ログインする必要はありません。

### シングルサインオンを使用するクライアントアプリケーションの書き込み {#writing-a-client-application-that-uses-single-sign-on}

シングルサインオンメカニズムを利用する場合、クライアントアプリケーションを起動する前に、一元化されたログインサービスを使用してログインする必要があります。 つまり、クライアントアプリケーションは、ブラウザーを使用してログインしたり、 `ChannelSet.login` メソッド。

AEM Formsのシングルサインオンメカニズムを使用している場合、基本ではなくカスタム認証を使用するようにリモートエンドポイントを設定します。 こうしないと、基本認証を使用する場合、認証エラーによってブラウザーの課題が発生し、ユーザーには表示されなくなります。 代わりに、アプリケーションは認証エラーを検出し、一元化されたログインサービスを使用してログインするようユーザーに指示するメッセージを表示します。

クライアントアプリケーションは、 `RemoteObject` コンポーネントを作成します。

```as3
 <?xml version="1.0"?> 
 <mx:Application   
        backgroundColor="#FFFFFF"> 
  
       <mx:Script> 
          <![CDATA[ 
  
            import mx.controls.Alert; 
            import mx.rpc.events.FaultEvent; 
  
            // Prompt user to login on a fault.          
            private function faultHandler(event:FaultEvent):void 
            { 
             if(event.fault.faultCode=="Client.Authentication") 
             { 
                 Alert.show( 
                     event.fault.faultString + "\n" + 
                     event.fault.faultCode + "\n" + 
                     "Please login to continue."); 
             } 
         } 
          ]]> 
       </mx:Script>          
      
       <mx:RemoteObject id="srv"  
           destination="product"  
           fault="faultHandler(event);"/> 
      
       <mx:DataGrid  
           width="100%" height="100%" 
           dataProvider="{srv.getProducts.lastResult}"/>  
  
       <mx:Button label="Get Data"  
           click="srv.getProducts();"/>  
      
 </mx:Application>
```

**Flexアプリケーションの実行中に新しいユーザーとしてログイン**

Flexで作成されたアプリケーションには、AEM Formsサービスに対するリクエストごとに認証 Cookie が含まれます。 パフォーマンス上の理由から、AEM Formsではリクエストのたびに cookie が検証されません。 ただし、AEM Formsは、認証 Cookie が別の認証 Cookie に置き換えられた場合を検出します。

例えば、クライアントアプリケーションを起動し、アプリケーションがアクティブな状態で、一元化されたログインサービスを使用してログアウトします。 次に、別のユーザーとしてログインできます。 別のユーザーとしてログインすると、既存の認証 Cookie が新しいユーザーの認証 Cookie に置き換えられます。

クライアントアプリケーションからの次のリクエストで、AEM Formsは cookie が変更されたことを検出し、ユーザーをログアウトします。 したがって、Cookie の変更後の最初のリクエストが失敗します。 以降のリクエストはすべて、新しい cookie のコンテキストでおこなわれ、成功します。

**ログアウト**

AEM Formsからログアウトしてセッションを無効にするには、クライアントのコンピューターから認証 Cookie を削除する必要があります。 シングルサインオンの目的はユーザーが 1 回ログインできるようにすることです。そのため、クライアントアプリケーションで cookie を削除する必要はありません。 このアクションは、ユーザーを効果的にログアウトします。

したがって、 `RemoteObject.logout` メソッドを使用すると、クライアント上でセッションがログアウトされていないことを示すエラーメッセージが生成されます。 代わりに、一元化されたログインサービスを使用して、認証 Cookie をログアウトおよび削除できます。

**Flexアプリケーションの実行中にログアウトする**

Flexで構築されたクライアントアプリケーションを起動し、一元化されたログインサービスを使用してログアウトできます。 ログアウトプロセスの一環として、認証 Cookie が削除されます。 Cookie がない、または無効な Cookie を持つリモートリクエストがおこなわれた場合、ユーザーセッションは無効になります。 このアクションはログアウトになります。 次回、クライアントアプリケーションがAEM Formsサービスに接続しようとすると、ユーザーはログインする必要があります。

**関連トピック**

[(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[(AEM forms では非推奨 )AEM Forms Remoting を使用したドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flexライブラリファイルの取り込み](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[AEM Forms Remoting (AEM forms では非推奨 ) を使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し {#passing-secure-documents-to-invoke-processes-using-remoting}

1 つ以上のドキュメントを必要とするプロセスを呼び出す際に、セキュリティで保護されたドキュメントをAEM Formsに渡すことができます。 安全なドキュメントを渡すと、ビジネス情報や機密ドキュメントを保護します。 この場合、ドキュメントはPDFドキュメント、XML ドキュメント、Word ドキュメントなどを参照できます。 セキュリティで保護されたドキュメントを許可するようにAEM Formsを設定した場合、Flexで記述されたクライアントアプリケーションからAEM Formsにセキュアなドキュメントを渡す必要があります。 ( [安全なドキュメントと安全でないドキュメントを受け入れるためのAEM Formsの設定](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).)

安全なドキュメントを渡す場合は、シングルサインオンを使用し、「*Document Upload Application User*」ロールを持つAEM forms ユーザーを指定します。 このロールがないと、ユーザーは保護されたドキュメントをアップロードできません。 プログラムによってユーザーに役割を割り当てることができます。 ( [ロールと権限の管理](/help/forms/developing/users.md#managing-roles-and-permissions).)

>[!NOTE]
新しいロールを作成し、そのロールのメンバーが安全なドキュメントをアップロードする場合は、ドキュメントのアップロード権限を必ず指定してください。

AEM Formsは、 `getFileUploadToken` アップロードサーブレットに渡されたトークンを返します。 この `DocumentReference.constructRequestForUpload` メソッドには、AEM Formsへの URL と、 `LC.FileUploadAuthenticator.getFileUploadToken` メソッド。 このメソッドは、 `URLRequest` オブジェクトを選択します。 次のコードは、このアプリケーションロジックの例を示しています。

```as3
     ... 
         private function startUpload():void 
         {     
             fileRef.addEventListener(Event.SELECT, selectHandler); 
             fileRef.addEventListener("uploadCompleteData", completeHandler); 
             try  
             { 
         var success:Boolean = fileRef.browse(); 
             }  
             catch (error:Error)  
             { 
                 trace("Unable to browse for files."); 
             } 
  
         } 
  
          private function selectHandler(event:Event):void 
             { 
             var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator"); 
             authTokenService.addEventListener("result", authTokenReceived); 
             authTokenService.channelSet = cs; 
             authTokenService.getFileUploadToken(); 
             } 
      
         private function authTokenReceived(event:ResultEvent):void 
             { 
             var token:String = event.result as String; 
             var request:URLRequest = DocumentReference.constructRequestForUpload("http://localhost:8080", token); 
              
             try 
             { 
           fileRef.upload(request); 
             } 
             catch (error:Error) 
             { 
             trace("Unable to upload file."); 
             }                               
             } 
  
         private function completeHandler(event:DataEvent):void  
         { 
              
             var params:Object = new Object(); 
             var docRef:DocumentReference = new DocumentReference(); 
             docRef.url = event.data as String; 
             docRef.referenceType = DocumentReference.REF_TYPE_URL; 
         } 
         ...
```

）

### 安全なドキュメントと安全でないドキュメントを受け入れるためのAEM Formsの設定 {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

管理コンソールを使用して、ドキュメントをFlexクライアントアプリケーションからAEM Formsプロセスに渡す際に、ドキュメントをセキュリティで保護するかどうかを指定できます。 デフォルトでは、AEM Formsはセキュリティで保護されたドキュメントを受け入れるように設定されています。 次の手順を実行することで、保護されたドキュメントを受け入れるようにAEM Formsを設定できます。

1. 管理コンソールにログインします。
1. クリック **設定**.
1. クリック **コアシステム設定**.
1. クリック **設定**.
1. 「 Flex applications からのドキュメントの保護されていないアップロードを許可する」オプションの選択がオフになっていることを確認します。

>[!NOTE]
安全でないドキュメントを受け入れるようにAEM Formsを設定するには、「 Flexアプリケーションからの保護されていないドキュメントのアップロードを許可」オプションを選択します。 次に、アプリケーションまたはサービスを再起動して、設定が有効になることを確認します。

### クイックスタート：リモート処理を使用して保護されたドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

次のコード例では、 `MyApplication/EncryptDocument.`ユーザーは、ログインして「Select File」ボタンをクリックし、ユーザーファイルのアップロードとプロセスのPDFに使用する必要があります。 つまり、ユーザーが認証されると、「 Select File 」ボタンが有効になります。 次の図は、ユーザーが認証された後のFlexクライアントアプリケーションを示しています。 Authenticated CheckBox が有効になっていることに注意してください。

![iu_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

AEM Formsがセキュリティで保護されたドキュメントのアップロードのみを許可するように設定されていて、ユーザーが「*Document Upload Application User*」ロールを持っていない場合は、例外がスローされます。 ユーザーにこの役割が割り当てられている場合は、ファイルがアップロードされ、プロセスが呼び出されます。

```as3
 <?xml version="1.0" encoding="utf-8"?> 
 <mx:Application  xmlns="*"  
      creationComplete="initializeChannelSet();"> 
        <mx:Script> 
        <![CDATA[ 
      import mx.rpc.livecycle.DocumentReference; 
      import flash.net.FileReference; 
      import flash.net.URLRequest; 
      import flash.events.Event; 
      import flash.events.DataEvent; 
      import mx.messaging.ChannelSet; 
      import mx.messaging.channels.AMFChannel;   
      import mx.rpc.events.ResultEvent; 
      import mx.collections.ArrayCollection; 
      import mx.rpc.AsyncToken; 
      import mx.controls.Alert; 
      import mx.rpc.events.FaultEvent; 
      import mx.rpc.AsyncResponder; 
  
      // Classes used in file retrieval   
      private var fileRef:FileReference = new FileReference(); 
      private var docRef:DocumentReference = new DocumentReference(); 
      private var parentResourcePath:String = "/"; 
      private var now1:Date;    
      private var serverPort:String = "hiro-xp:8080"; 
      
      // Define a ChannelSet object. 
      public var cs:ChannelSet;  
      
      // Define an AsyncToken object. 
      public var token:AsyncToken; 
      
       // Holds information returned from AEM Forms  
      [Bindable] 
      public var progressList:ArrayCollection = new ArrayCollection(); 
  
           
      // Handles a successful login 
     private function LoginResultEvent(event:ResultEvent, 
         token:Object=null):void  { 
             switch(event.result) { 
                 case "success": 
                     authenticatedCB.selected = true; 
                     btnFile.enabled = true; 
                     btnLogout.enabled = true; 
                     btnLogin.enabled = false; 
                         break; 
                     default: 
                 } 
             } 
              
              
 // Handle login failure. 
 private function LoginFaultEvent(event:FaultEvent, 
     token:Object=null):void { 
     switch(event.fault.faultCode) { 
                 case "Client.Authentication": 
                         default: 
                         authenticatedCB.selected = false; 
                         Alert.show("Login failure: " + event.fault.faultString); 
                 } 
             } 
                  
      
      // Set up channel set to invoke AEM Forms  
      private function initializeChannelSet():void { 
        cs = new ChannelSet();  
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));  
        EncryptDocument2.channelSet = cs; 
      } 
  
     // Call this method to upload the file. 
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process. 
      private function uploadFile():void { 
        fileRef.addEventListener(Event.SELECT, selectHandler); 
        fileRef.addEventListener(DataEvent.UPLOAD_COMPLETE_DATA,completeHandler); 
        fileRef.browse(); 
      } 
  
      // Gets called for selected file. Does the actual upload via the file upload servlet. 
      private function selectHandler(event:Event):void { 
              var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator"); 
         authTokenService.addEventListener("result", authTokenReceived); 
         authTokenService.channelSet = cs; 
         authTokenService.getFileUploadToken(); 
      } 
  
     private function authTokenReceived(event:ResultEvent):void 
     { 
     var token:String = event.result as String; 
     var request:URLRequest = DocumentReference.constructRequestForUpload("https://hiro-xp:8080", token); 
              
     try 
     { 
           fileRef.upload(request); 
     } 
     catch (error:Error) 
     { 
         trace("Unable to upload file."); 
     }                               
 } 
  
      // Called once the file is completely uploaded. 
      private function completeHandler(event:DataEvent):void {                     
  
        // Set the docRef’s url and referenceType parameters 
        docRef.url = event.data as String;       
        docRef.referenceType=DocumentReference.REF_TYPE_URL; 
        executeInvokeProcess();  
      }       
  
     //This method invokes the EncryptDocument process 
      public function executeInvokeProcess():void { 
         //Create an Object to store the input value for the EncryptDocument process 
           now1 = new Date(); 
      
         var params:Object = new Object(); 
         params["inDoc"]=docRef; 
  
         // Invoke the EncryptDocument process 
         var token:AsyncToken;             
         token = EncryptDocument2.invoke(params); 
         token.name = name; 
      } 
  
      // AEM Forms  login method 
      private function ROLogin():void { 
         // Make sure that the user is not already logged in. 
          
         //Get the User and Password 
         var userName:String = txtUser.text; 
         var pass:String = txtPassword.text; 
          
        if (cs.authenticated == false) { 
             token = cs.login(userName, pass); 
          
         // Add result and fault handlers. 
         token.addResponder(new AsyncResponder(LoginResultEvent,    LoginFaultEvent)); 
                 } 
             } 
      
      // This method handles a successful process invocation 
      public function handleResult(event:ResultEvent):void 
      { 
            //Retrieve information returned from the service invocation 
          var token:AsyncToken = event.token;         
          var res:Object = event.result; 
          var dr:DocumentReference = res["outDoc"] as DocumentReference; 
          var now2:Date = new Date(); 
  
           // These fields map to columns in the DataGrid 
          var progObject:Object = new Object(); 
          progObject.filename = token.name; 
          progObject.timing = (now2.time - now1.time).toString(); 
          progObject.state = "Success"; 
          progObject.link = "<a href='" + dr.url + "'> open </a>"; 
          progressList.addItem(progObject); 
      } 
      
      // Prompt user to login on a fault.          
       private function faultHandler(event:FaultEvent):void 
            { 
             if(event.fault.faultCode=="Client.Authentication") 
             { 
                 Alert.show( 
                     event.fault.faultString + "\n" + 
                     event.fault.faultCode + "\n" + 
                     "Please login to continue."); 
             } 
            } 
      
       // AEM Forms  logout method 
     private function ROLogout():void { 
         // Add result and fault handlers. 
         token = cs.logout(); 
         token.addResponder(new AsyncResponder(LogoutResultEvent,LogoutFaultEvent)); 
     } 
  
     // Handle successful logout. 
     private function LogoutResultEvent(event:ResultEvent, 
         token:Object=null):void { 
         switch (event.result) { 
         case "success": 
                 authenticatedCB.selected = false; 
                 btnFile.enabled = false; 
                 btnLogout.enabled = false; 
                 btnLogin.enabled = true; 
                 break; 
                 default: 
             } 
     } 
  
     // Handle logout failure. 
     private function LogoutFaultEvent(event:FaultEvent, 
             token:Object=null):void { 
             Alert.show("Logout failure: " + event.fault.faultString); 
     } 
  
          private function resultHandler(event:ResultEvent):void { 
          // Do anything else here. 
          } 
        ]]> 
  
      </mx:Script> 
      <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);"> 
          <mx:method name="invoke" result="handleResult(event)"/> 
      </mx:RemoteObject> 
      
       <!--//This consists of what is displayed on the webpage--> 
      <mx:Panel id="lcPanel" title="EncryptDocument  (Deprecated for AEM forms) AEM Forms Remoting Example"  
           height="25%" width="25%" paddingTop="10" paddingLeft="10" paddingRight="10"  
           paddingBottom="10"> 
         <mx:Label width="100%" color="blue" 
                text="Select a PDF file to pass to the EncryptDocument process"/>  
        <mx:DataGrid x="10" y="0" width="500" id="idProgress" editable="false"  
           dataProvider="{progressList}" height="231" selectable="false" > 
          <mx:columns> 
            <mx:DataGridColumn headerText="Filename" width="200" dataField="filename" editable="false"/> 
            <mx:DataGridColumn headerText="State" width="75" dataField="state" editable="false"/> 
            <mx:DataGridColumn headerText="Timing" width="75" dataField="timing" editable="false"/> 
            <mx:DataGridColumn headerText="Click to Open" dataField="link" editable="false" > 
             <mx:itemRenderer> 
                <mx:Component> 
                   <mx:Text x="0" y="0" width="100%" htmlText="{data.link}"/> 
                </mx:Component> 
             </mx:itemRenderer> 
            </mx:DataGridColumn> 
          </mx:columns> 
        </mx:DataGrid> 
        <mx:Button label="Select File" click="uploadFile()"  id="btnFile" enabled="false"/> 
        <mx:Button label="Login" click="ROLogin();" id="btnLogin"/> 
        <mx:Button label="LogOut" click="ROLogout();" enabled="false" id="btnLogout"/> 
        <mx:HBox> 
         <mx:Label text="User:"/> 
         <mx:TextInput id="txtUser" text=""/> 
         <mx:Label text="Password:"/> 
         <mx:TextInput id="txtPassword" text="" displayAsPassword="true"/> 
         <mx:CheckBox id="authenticatedCB"  
             label="Authenticated?"  
             enabled="false"/> 
     </mx:HBox> 
      </mx:Panel> 
 </mx:Application>
```

**関連トピック**

[(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[(AEM forms では非推奨 )AEM Forms Remoting を使用したドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flexライブラリファイルの取り込み](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[AEM Forms Remoting (AEM forms では非推奨 ) を使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで作成されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## リモート処理を使用したカスタムコンポーネントサービスの呼び出し {#invoking-custom-component-services-using-remoting}

Remoting を使用して、カスタムコンポーネント内のサービスを呼び出すことができます。 例えば、顧客サービスを含む銀行コンポーネントについて考えてみましょう。 Flexで記述されたクライアントアプリケーションを使用して、Customer Service に属する操作を呼び出すことができます。 このセクションに関連するクイックスタートを実行する前に、Bank カスタムコンポーネントを作成する必要があります。

顧客サービスは、 `createCustomer`. このディスカッションでは、Customer Service を呼び出して顧客を作成するFlexクライアントアプリケーションの作成方法を説明します。 この操作には、型の複雑なオブジェクトが必要です `com.adobe.livecycle.sample.customer.Customer` 新しい顧客を表す。 次の図に、Customer サービスを呼び出して新しい顧客を作成するクライアントアプリケーションを示します。 この `createCustomer` 操作は顧客識別子の値を返します。 識別子の値が「顧客識別子」テキスト・ボックスに表示されます。

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

次の表に、このクライアントアプリケーションに含まれるコントロールの一覧を示します。

<table> 
 <thead> 
  <tr> 
   <th><p>コントロール名</p></th> 
   <th><p>説明</p></th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td><p>txtFirst</p></td> 
   <td><p>顧客の名を指定します。 </p></td> 
  </tr> 
  <tr> 
   <td><p>txtLast</p></td> 
   <td><p>顧客の姓を指定します。 </p></td> 
  </tr> 
  <tr> 
   <td><p>txtPhone</p></td> 
   <td><p>顧客の電話番号を指定します。</p></td> 
  </tr> 
  <tr> 
   <td><p>txtStreet</p></td> 
   <td><p>顧客の住所名を指定します。</p></td> 
  </tr> 
  <tr> 
   <td><p>txtState</p></td> 
   <td><p>顧客の状態を指定します。 </p></td> 
  </tr> 
  <tr> 
   <td><p>txtZIP</p></td> 
   <td><p>顧客の郵便番号を指定します。 </p></td> 
  </tr> 
  <tr> 
   <td><p>txtCity</p></td> 
   <td><p>顧客の市区町村を指定します。</p></td> 
  </tr> 
  <tr> 
   <td><p>txtCustId</p></td> 
   <td><p>新しいアカウントが属する顧客識別子の値を指定します。 このテキストボックスには、顧客サービスの <code>createCustomer</code> 操作。 </p></td> 
  </tr> 
 </tbody> 
</table>

### AEM Formsの複雑なデータ型のマッピング {#mapping-aem-forms-complex-data-types}

一部のAEM Forms操作では、入力値として複雑なデータ型が必要です。 これらの複雑なデータ型は、操作で使用される実行時の値を定義します。 例えば、顧客サービスの `createCustomer` 操作にはが必要です `Customer` サービスに必要な実行時の値を含むインスタンス。 複合型がない場合、Customer サービスは例外をスローし、操作を実行しません。

AEM Formsサービスを呼び出す際に、必要なAEM Forms複合型にマッピングするActionScriptオブジェクトを作成します。 操作に必要な複雑なデータ型ごとに、個別のActionScriptオブジェクトを作成します。

ActionScriptクラスで、 `RemoteClass` AEM Forms複合型にマッピングするメタデータタグ。 例えば、顧客サービスの `createCustomer` 操作、 `com.adobe.livecycle.sample.customer.Customer` データタイプ。

次の Customer という名前のActionScriptクラスは、AEM Formsデータ型にマッピングする方法を示しています `com.adobe.livecycle.sample.customer.Customer`.

```as3
 package customer 
  
 { 
     [RemoteClass(alias="com.adobe.livecycle.sample.customer.Customer")] 
     public class Customer 
     { 
            public var name:String; 
            public var street:String; 
            public var city:String; 
            public var state:String; 
            public var phone:String; 
            public var zip:int; 
        } 
 }
```

AEM Forms複合型の完全修飾データ型がエイリアスタグに割り当てられます。

ActionScriptクラスのフィールドは、AEM Forms複合型に属するフィールドと一致します。 顧客ActionScriptクラスにある 6 つのフィールドは、 `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
Forms複合型に属するフィールド名を判断する良い方法は、Web ブラウザーでサービスの WSDL を表示することです。 WSDL は、サービスの複合型と対応するデータメンバーを指定します。 Customer Service では、次の WSDL が使用されます。 *https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl を呼び出します。*

顧客ActionScriptクラスは、customer という名前のパッケージに属しています。 複雑なAEM Formsデータ型にマッピングするすべてのActionScriptクラスは、独自のパッケージに配置することをお勧めします。 次の図に示すように、Flexプロジェクトの src フォルダーにActionScriptーを作成し、フォルダー内にフォルダーファイルを配置します。

![iu_iu_customeras](assets/iu_iu_customeras.png)

### クイックスタート：リモート処理を使用した顧客カスタムサービスの呼び出し {#quick-start-invoking-the-customer-custom-service-using-remoting}

次のコード例は、Customer サービスを呼び出して新しい顧客を作成します。 このコード例を実行する場合は、必ずすべてのテキストボックスに入力してください。 また、にマッピングする Customer.as ファイルを必ず作成してください。 `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
このクイックスタートを実行する前に、Bank カスタムコンポーネントを作成してデプロイする必要があります。

```as3
 <?xml version="1.0" encoding="utf-8"?> 
 <mx:Application  layout="absolute" backgroundColor="#B1ABAB"> 
  
 <mx:Script> 
            <![CDATA[ 
      
      import flash.net.FileReference; 
      import flash.net.URLRequest; 
      import flash.events.Event; 
      import flash.events.DataEvent; 
      import mx.messaging.ChannelSet; 
      import mx.messaging.channels.AMFChannel;   
      import mx.rpc.events.ResultEvent; 
      import mx.collections.ArrayCollection; 
      import mx.rpc.AsyncToken; 
      import mx.managers.CursorManager; 
      import mx.rpc.remoting.mxml.RemoteObject; 
  
  
      // Custom class that corresponds to an input to the 
      // AEM Forms encryption method 
      import customer.Customer; 
  
      // Classes used in file retrieval   
      private var fileRef:FileReference = new FileReference(); 
      private var parentResourcePath:String = "/"; 
      private var serverPort:String = "hiro-xp:8080"; 
      private var now1:Date;   
      private var fileName:String;    
  
      // Prepares parameters for encryptPDFUsingPassword method call 
      public function executeCreateCustomer():void  
      { 
      
        var cs:ChannelSet= new ChannelSet();  
     cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));  
      
     customerService.setCredentials("administrator", "password"); 
     customerService.channelSet = cs; 
      
     //Create a Customer object required to invoke the Customer service's 
     //createCustomer operation 
     var myCust:Customer = new Customer();  
      
     //Get values from the user of the Flex application 
     var fullName:String = txtFirst.text +" "+txtLast.text ;  
     var Phone:String = txtPhone.text; 
     var Street:String = txtStreet.text; 
     var State:String = txtState.text; 
     var Zip:int = parseInt(txtZIP.text); 
     var City:String = txtCity.text; 
      
     //Populate Customer fields 
     myCust.name = fullName; 
     myCust.phone = Phone; 
     myCust.street= Street; 
     myCust.state= State; 
     myCust.zip = Zip;  
     myCust.city = City; 
      
     //Invoke the Customer service's createCustomer operation 
     var params:Object = new Object(); 
        params["inCustomer"]=myCust; 
     var token:AsyncToken;             
        token = customerService.createCustomer(params); 
        token.name = name; 
      } 
      
      private function handleResult(event:ResultEvent):void  
      { 
          // Retrieve the information returned from the service invocation 
          var token:AsyncToken = event.token;         
          var res:Object = event.result; 
          var custId:String = res["CustomerId"] as String; 
      
          //Assign to the custId to the text box 
          txtCustId.text = custId;  
      } 
      
      
      private function resultHandler(event:ResultEvent):void  
      { 
      
      }    
            ]]> 
 </mx:Script> 
 <mx:RemoteObject id="customerService" destination="CustomerService" result="resultHandler(event);"> 
 <mx:method name="createCustomer" result="handleResult(event)"/> 
 </mx:RemoteObject> 
  
  
 <mx:Style source="../bank.css"/> 
     <mx:Grid> 
                     <mx:GridRow width="100%" height="100%"> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:Label text="New Customer" fontSize="16" fontWeight="bold"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                         </mx:GridItem> 
                     </mx:GridRow> 
                     <mx:GridRow width="100%" height="100%"> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:Label text="First Name:" fontSize="12" fontWeight="bold"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:TextInput styleName="textField" id="txtFirst"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:Button label="Create Customer" id="btnCreateCustomer" click="executeCreateCustomer()"/> 
                         </mx:GridItem> 
                     </mx:GridRow> 
                     <mx:GridRow width="100%" height="100%"> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:Label text="Last Name" fontSize="12" fontWeight="bold"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:TextInput styleName="textField" id="txtLast"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                         </mx:GridItem> 
                     </mx:GridRow> 
                     <mx:GridRow width="100%" height="100%"> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:Label text="Phone" fontSize="12" fontWeight="bold"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:TextInput styleName="textField" id="txtPhone"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                         </mx:GridItem> 
                     </mx:GridRow> 
                     <mx:GridRow width="100%" height="100%"> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:Label text="Street" fontSize="12" fontWeight="bold"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:TextInput styleName="textField" id="txtStreet"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                         </mx:GridItem> 
                     </mx:GridRow> 
                     <mx:GridRow width="100%" height="100%"> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:Label text="State" fontSize="12" fontWeight="bold"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:TextInput styleName="textField" id="txtState"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                         </mx:GridItem> 
                     </mx:GridRow> 
                     <mx:GridRow width="100%" height="100%"> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:Label text="ZIP" fontSize="12" fontWeight="bold"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:TextInput styleName="textField" id="txtZIP"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                         </mx:GridItem> 
                     </mx:GridRow> 
                     <mx:GridRow width="100%" height="100%"> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:Label text="City" fontSize="12" fontWeight="bold"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:TextInput styleName="textField" id="txtCity"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                         </mx:GridItem> 
                     </mx:GridRow> 
                             <mx:GridRow width="100%" height="100%"> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:Label text="Customer Identifier" fontSize="12" fontWeight="bold"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                             <mx:TextInput styleName="textField" id="txtCustId" editable="false"/> 
                         </mx:GridItem> 
                         <mx:GridItem width="100%" height="100%"> 
                         </mx:GridItem> 
                     </mx:GridRow> 
                 </mx:Grid> 
 </mx:Application> 
 
```

**スタイルシート**

このクイックスタートには、「bank.css」という名前のスタイルシートが含まれています。 次のコードは、使用されるスタイルシートを表しています。

```as3
 /* CSS file */ 
 global 
 { 
          backgroundGradientAlphas: 1.0, 1.0; 
          backgroundGradientColors: #525152,#525152; 
          borderColor: #424444; 
          verticalAlign: middle; 
          color: #FFFFFF; 
          font-size:12; 
          font-weight:normal; 
 } 
  
 ApplicationControlBar 
 { 
          fillAlphas: 1.0, 1.0; 
          fillColors: #393839, #393839; 
 } 
  
 .textField 
 { 
          backgroundColor: #393839; 
          background-disabled-color: #636563; 
 } 
  
  
 .button 
 { 
          fillColors: #636563, #424242; 
 } 
  
 .dropdownMenu 
 { 
          backgroundColor: #DDDDDD; 
          fillColors: #636563, #393839; 
          alternatingItemColors: #888888, #999999; 
 } 
  
 .questionLabel 
 { 
      
 } 
  
 ToolTip  
 { 
        backgroundColor: black; 
        backgroundAlpha: 1.0; 
        cornerRadius: 0; 
        color: white; 
 } 
  
 DateChooser  
 { 
        cornerRadius: 0; /* pixels */ 
        headerColors: black, black; 
        borderColor: black; 
        themeColor: black; 
        todayColor: red; 
        todayStyleName: myTodayStyleName; 
        headerStyleName: myHeaderStyleName; 
        weekDayStyleName: myWeekDayStyleName; 
        dropShadowEnabled: true; 
 } 
  
 .myTodayStyleName  
 { 
        color: white; 
 } 
  
 .myWeekDayStyleName  
 { 
        fontWeight: normal; 
 } 
  
 .myHeaderStyleName  
 { 
        color: red; 
        fontSize: 16; 
        fontWeight: bold; 
 }
```

**関連トピック**

[(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[(AEM forms では非推奨 )AEM Forms Remoting を使用したドキュメントの処理](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[AEM Forms Flexライブラリファイルの取り込み](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[AEM Forms Remoting (AEM forms では非推奨 ) を使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Flexで作成されたクライアントアプリケーションの認証](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
