---
title: 人間中心の長期間有効なプロセスの呼び出し
seo-title: Invoking Human-Centric Long-Lived Processes
description: 呼び出し API、Web サービスを使用する ASP.NET アプリケーション、および Remoting を使用するFlexで構築されたクライアントアプリケーションを使用して、Workbench で作成された人間中心の長期間有効なプロセスをプログラムで呼び出します。
seo-description: Programmatically invoke human-centric long-lived processes created in Workbench using a Java web-based client application that uses the Invocation API, an ASP.NET application that uses web services, and a client application built with Flex that uses Remoting.
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
role: Developer
exl-id: 4f581af8-9c1a-4e80-b459-a83a1dab3b01
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '3712'
ht-degree: 4%

---

# 人間中心の長期間有効なプロセスの呼び出し {#invoking-human-centric-long-lived-processes}

Workbench で作成された人間中心の長期間有効なプロセスを、次のクライアントアプリケーションを使用してプログラムで呼び出すことができます。

* 呼び出し API を使用する Java Web ベースのクライアントアプリケーション。 ( [Java API を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).
* Web サービスを使用する ASP.NET アプリケーションです。 ( [Web サービスを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
* Remoting を使用するFlexで構築されたクライアントアプリケーション。 ( [(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

呼び出される長期間有効なプロセスの名前はです *FirstAppSolution/PreLoanProcess*. このプロセスは、 [最初のAEM Formsアプリケーションの作成](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).

人間中心のプロセスには、Workspace を使用してユーザーが応答できるタスクが含まれます。 例えば、Workbench を使用して、銀行管理者がローン申し込みを承認または拒否できるプロセスを作成できます。 次の図に、プロセスを示します *FirstAppSolution/PreLoanProcess*.

* FirstAppSolution/PreLoanProcess*プロセスは、データ型が XML である* formData*という名前の入力パラメーターを受け付けます。 この XML データが、という名前のフォームデザインと結合されます。 *PreLoanForm.xdp*. 次の図に、ローン申し込みを承認または拒否するユーザーに割り当てられたタスクを表すフォームを示します。 ユーザーは、Workspace を使用してアプリケーションを承認または拒否します。 Workspace ユーザーは、次の図に示す「承認」ボタンをクリックして、ローン申し込みを承認できます。 同様に、ユーザーは拒否ボタンをクリックして、ローンの申し込みを拒否できます。

長期間有効なプロセスは非同期で呼び出され、次の要因により、同期的に呼び出すことはできません。

* 1 つのプロセスが長い時間を要する場合があります。
* プロセスは、組織の境界にまたがることができます。
* プロセスを完了するには、外部入力が必要です。 例えば、不在の管理者にフォームが送信される場合を考えてみましょう。 この場合、マネージャーがフォームに戻って入力するまで、プロセスは完了しません。

長期間有効なプロセスが呼び出されると、AEM Formsはレコードの作成の一環として呼び出し識別子の値を作成します。 このレコードは、長期間有効なプロセスのステータスを追跡し、AEM Formsデータベースに保存されます。 呼び出し識別子の値を使用して、長期間有効なプロセスのステータスを追跡できます。 また、プロセス呼び出し識別子の値を使用して、実行中のプロセスインスタンスの終了など、Process Manager の操作を実行できます。

>[!NOTE]
>
>短時間のみ有効なプロセスが呼び出された場合、AEM Formsは呼び出し識別子の値やレコードを作成しません。

この `FirstAppSolution/PreLoanProcess` プロセスは、XML データで表されたアプリケーションを申請者が送信すると呼び出されます。 入力プロセス変数の名前は次のとおりです。 `formData` データ型は XML です。 この説明の目的で、次の XML データが `FirstAppSolution/PreLoanProcess` プロセス。

```as3
 <?xml version="1.0" encoding="UTF-8"?> 
 <LoanApp> 
 <Name>Sam White</Name> 
 <LoanAmount>250000</LoanAmount> 
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail> 
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus> 
 </LoanApp>
```

プロセスに渡される XML データは、プロセスで使用されるフォーム内のフィールドと一致する必要があります。 そうしないと、データはフォーム内に表示されません。 を呼び出すすべてのアプリケーション `FirstAppSolution/PreLoanProcess` プロセスは、この XML データソースを渡す必要があります。 で作成されたアプリケーション *人間中心の長期間有効なプロセスの呼び出し* ユーザーが Web クライアントに入力した値から XML データソースを動的に作成します。

クライアントアプリケーションを使用して、 *FirstAppSolution/PreLoanProcess *必要な XML データを処理します。 長期間有効なプロセスは、呼び出し識別子の値を戻り値として返します。 次の図は、* FirstAppSolution/PreLoanProcess *長期間有効なプロセス。 クライアントアプリケーションは XML データを送信し、呼び出し識別子の値を表す string 値を取得します。

**関連トピック**

[人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[人間中心の長期間有効なプロセスを呼び出す ASP.NET Web アプリケーションの作成](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[人間中心の長期間有効なプロセスを呼び出す、Flexで構築されたクライアントアプリケーションの作成](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成 {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

Java サーブレットを使用してを呼び出す Web ベースのアプリケーションを作成できます `FirstAppSolution/PreLoanProcess` プロセス。 Java サーブレットからこのプロセスを呼び出すには、Java サーブレット内で呼び出し API を使用します。 ( [Java API を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)

次の図に、名前、電話（または E メール）および金額の値を投稿する Web ベースのクライアントアプリケーションを示します。 これらの値は、ユーザーが「アプリケーションを送信」ボタンをクリックすると、Java サーブレットに送信されます。

Java サーブレットは、次のタスクを実行します。

* 「HTML」ページから Java サーブレットに投稿された値を取得します。
* FirstAppSolution/PreLoanProcess *process に渡す XML データソースを動的に作成します。 名前、電話（または電子メール）、金額の値は、XML データソースで指定されます。
* を呼び出します。 *FirstAppSolution/PreLoanProcess* プロセスを実行する際に、AEM Forms Invocation API を使用します。
* クライアント Web ブラウザーに呼び出し識別子の値を返します。

### 手順の概要 {#summary-of-steps}

を呼び出す Java Web ベースのアプリケーションを作成するには `FirstAppSolution/PreLoanProcess` 次の手順を実行します。

1. [Web プロジェクトの作成](invoking-human-centric-long-lived.md#create-a-web-project).
1. [サーブレット用の Java アプリケーションロジックの作成](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet).
1. [Web アプリケーション用の Web ページの作成](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [Web アプリケーションを WAR ファイルにパッケージ化する](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file).
1. [AEM Formsをホストする J2EE アプリケーションサーバーに WAR ファイルをデプロイする](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms).
1. [Web アプリケーションのテスト](invoking-human-centric-long-lived.md#test-your-web-application).

>[!NOTE]
>
>これらの手順の一部は、AEM Formsがデプロイされている J2EE アプリケーションによって異なります。 例えば、WAR ファイルのデプロイ方法は、使用している J2EE アプリケーションサーバーによって異なります。 AEM Formsが JBoss®にデプロイされていることを前提としています。

### Web プロジェクトの作成 {#create-a-web-project}

Web アプリケーションを作成する最初の手順は、Web プロジェクトを作成することです。 このドキュメントの基になる Java IDE は Eclipse 3.3 です。Eclipse IDE を使用して、Web プロジェクトを作成し、必要な JAR ファイルをプロジェクトに追加します。 プロジェクトにHTMLページ「index.html」と Java サーブレットを追加します。

次のリストでは、Web プロジェクトに含める JAR ファイルを指定します。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

これらの JAR ファイルの場所については、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

>[!NOTE]
>
>J2EE.jar ファイルは、Java サーブレットで使用されるデータタイプを定義します。 この JAR ファイルは、AEM Formsがデプロイされている J2EE アプリケーションサーバーから取得できます。

**Web プロジェクトの作成**

1. Eclipse を起動し、 **ファイル** >  **新規プロジェクト**.
1. 内 **新規プロジェクト** ダイアログボックスで、次を選択します。 **Web** > **ダイナミック Web プロジェクト**.
1. タイプ `InvokePreLoanProcess` プロジェクト名を入力し、 **完了**.

**必要な JAR ファイルをプロジェクトに追加する**

1. [ プロジェクトエクスプローラ ] ウィンドウで、 `InvokePreLoanProcess` プロジェクトと選択 **プロパティ**.
1. クリック **Java ビルドパス** そして、 **ライブラリ** タブをクリックします。
1. 次をクリック： **外部 JAR を追加** ボタンをクリックし、含める JAR ファイルを参照します。

**プロジェクトに Java サーブレットを追加**

1. [ プロジェクトエクスプローラ ] ウィンドウで、 `InvokePreLoanProcess` プロジェクトと選択 **新規** >  **その他**.
1. を展開します。 **Web** フォルダー、選択 **Servlet**&#x200B;をクリックし、 **次へ**.
1. サーブレットを作成ダイアログボックスで、「 `SubmitXML` サーブレット名の場合は、 **完了**.

**プロジェクトにHTMLページを追加する**

1. [ プロジェクトエクスプローラ ] ウィンドウで、 `InvokePreLoanProcess` プロジェクトと選択 **新規** > **その他**.
1. を展開します。 **Web** フォルダー、選択 **HTML**&#x200B;をクリックし、 **次へ**.
1. [ 新しいHTML] ダイアログボックスで、 `index.html` ファイル名を指定し、 **完了**.

>[!NOTE]
>
>SubmitXML Java サーブレットを呼び出すHTMLコンテンツの作成について詳しくは、 [Web アプリケーション用の Web ページの作成](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application).

### サーブレット用の Java アプリケーションロジックの作成 {#create-java-application-logic-for-the-servlet}

を呼び出す Java アプリケーションロジックの作成 `FirstAppSolution/PreLoanProcess` プロセスを Java サーブレット内から実行します。 次のコードは、 `SubmitXML` Java サーブレット：

```as3
     public class SubmitXML extends HttpServlet implements Servlet { 
         public void doGet(HttpServletRequest req, HttpServletResponse resp 
         throws ServletException, IOException { 
         doPost(req,resp); 
          
         } 
         public void doPost(HttpServletRequest req, HttpServletResponse resp 
         throws ServletException, IOException { 
             //Add code here to invoke the FirstAppSolution/PreLoanProcess process 
             }
```

通常、クライアントコードは Java サーブレットの `doGet` または `doPost` メソッド。 より優れたプログラミング方法は、このコードを別のクラスに配置することです。 次に、 `doPost` メソッド ( または `doGet` メソッド ) を使用し、適切なメソッドを呼び出します。 ただし、コードを簡潔にするために、コード例は最小限に抑えられ、 `doPost` メソッド。

を呼び出すには、以下を実行します。 `FirstAppSolution/PreLoanProcess` 呼び出し API を使用してプロセスを実行するには、次のタスクを実行します。

1. Java プロジェクトのクラスパスに、adobe-livecycle-client.jar などのクライアント JAR ファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。
1. 「HTML」ページから送信された名前、電話、金額の値を取得します。 これらの値を使用して、 `FirstAppSolution/PreLoanProcess` プロセス。 以下を使用できます。 `org.w3c.dom` XML データソースを作成するクラス（このアプリケーションロジックは次のコードの例に示します）。
1. 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
1. コンストラクタを使用して `ServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。`ServiceClient` オブジェクトを使用すると、サービス操作を呼び出すことができます。呼び出し要求の検索、ディスパッチ、ルーティングなどのタスクを処理します。
1. コンストラクタを使用して `java.util.HashMap` オブジェクトを作成します。
1. 各入力パラメーターに対して `java.util.HashMap` オブジェクトの `put` メソッドを呼び出して、長期間有効なプロセスに渡します。プロセスの入力パラメーターの名前を必ず指定してください。 これは、 `FirstAppSolution/PreLoanProcess` プロセスには、型の入力パラメータが 1 つ必要です `XML` ( 名前 `formData`) の場合、を呼び出すだけで済みます `put` メソッドを 1 回だけ使用できます。

   ```as3
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process 
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount); 
                 
    //Create a Map object to store the parameter value 
    Map params = new HashMap(); 
    params.put("formData", inXML);
   ```

1. の作成 `InvocationRequest` を呼び出すことによってオブジェクトを取得 `ServiceClientFactory` オブジェクトの `createInvocationRequest` メソッドを使用して、次の値を渡します。

   * 長期間有効なプロセスを指定する文字列値。を呼び出すには、以下を実行します。 `FirstAppSolution/PreLoanProcess` プロセス、指定 `FirstAppSolution/PreLoanProcess`.
   * プロセス操作名を表す文字列値。長期間有効なプロセス操作の名前は次のとおりです。 `invoke`.
   * サービス操作に必要なパラメーター値を含む `java.util.HashMap` オブジェクト。
   * 指定するブール値 `false`：非同期リクエストを作成します（この値は、長期間有効なプロセスを呼び出す場合に適用されます）。

   >[!NOTE]
   >
   >*短時間のみ有効なプロセスは、 createInvocationRequest メソッドの 4 番目のパラメーターとして値 true を渡すことで呼び出すことができます。 値 true を渡すと、同期リクエストが作成されます。*

1. を呼び出して、AEM Formsに呼び出し要求を送信します。 `ServiceClient` オブジェクトの `invoke` メソッドおよび `InvocationRequest` オブジェクト。 この `invoke` メソッドは、 `InvocationReponse` オブジェクト。
1. 長期間有効なプロセスは、呼び出し識別値を表す string 値を返します。 を呼び出して、この値を取得します。 `InvocationReponse` オブジェクトの `getInvocationId` メソッド。

   ```as3
    //Send the invocation request to the long-lived process and  
    //get back an invocation response object 
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest); 
    String invocationId = lcResponse.getInvocationId();
   ```

1. 呼び出し ID 値をクライアント Web ブラウザーに書き込みます。 以下の `java.io.PrintWriter` インスタンスを使用して、この値をクライアント Web ブラウザーに書き込みます。

### クイックスタート：呼び出し API を使用した長期間有効なプロセスの呼び出し {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

次の Java コードの例は、 `FirstAppSolution/PreLoanProcess` プロセス。

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-livecycle-client.jar 
     * 2. adobe-usermanager-client.jar 
     * 
     * (Because this  quick start is implemented as a Java servlet, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     * */ 
 import java.io.ByteArrayOutputStream; 
 import java.io.File; 
 import java.io.IOException; 
 import java.io.PrintWriter; 
  
 import javax.servlet.ServletException; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import java.util.*; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import javax.xml.parsers.DocumentBuilder; 
 import javax.xml.parsers.DocumentBuilderFactory; 
 import javax.xml.transform.Transformer; 
 import javax.xml.transform.TransformerFactory; 
 import javax.xml.transform.dom.DOMSource; 
 import javax.xml.transform.stream.StreamResult; 
  
 import com.adobe.idp.dsc.InvocationRequest; 
 import com.adobe.idp.dsc.InvocationResponse; 
 import com.adobe.idp.dsc.clientsdk.ServiceClient; 
 import org.w3c.dom.Element; 
  
     public class SubmitXML extends javax.servlet.http.HttpServlet implements javax.servlet.Servlet { 
       static final long serialVersionUID = 1L; 
      
        public SubmitXML() { 
         super(); 
     }        
      
      
     protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
         // TODO Auto-generated method stub 
         doPost(request,response); 
     }       
      
     protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException { 
                  
         try{ 
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
              
             //Create a ServiceClient object 
             ServiceClient myServiceClient = myFactory.getServiceClient(); 
              
             //Get the values that are passed from the Loan HTML page 
             String name = (String)request.getParameter("name"); 
             String phone = (String)request.getParameter("phone"); 
             String amount = (String)request.getParameter("amount"); 
                  
             //Create XML to pass to the FirstAppSolution/PreLoanProcess process 
             org.w3c.dom.Document inXML = GetDataSource(name,phone,amount); 
                                  
             //Create a Map object to store the XML input parameter value 
             Map params = new HashMap(); 
             params.put("formData", inXML);  
              
             //Create an InvocationRequest object 
             InvocationRequest lcRequest =  myFactory.createInvocationRequest( 
                 "FirstAppSolution/PreLoanProcess", //Specify the long-lived process name 
                     "invoke",           //Specify the operation name     
                     params,               //Specify input values 
                     false);               //Create an asynchronous request  
              
             //Send the invocation request to the long-lived process and  
             //get back an invocation response object 
             InvocationResponse lcResponse = myServiceClient.invoke(lcRequest); 
             String invocationId = lcResponse.getInvocationId(); 
  
             //Create a PrintWriter instance 
             PrintWriter pp = response.getWriter();      
              
             //Write the invocation identifier value back to the client web browser 
             pp.println("The job status identifier value is: " +invocationId); 
              
         }catch (Exception e) { 
              System.out.println("The following exception occurred: "+e.getMessage()); 
       } 
     } 
      
      
      //Create XML data to pass to the long-lived process 
      private static org.w3c.dom.Document GetDataSource(String name, String phone, String amount) 
      { 
             org.w3c.dom.Document document = null; 
              
             try 
             { 
                 //Create DocumentBuilderFactory and DocumentBuilder objects 
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance(); 
                 DocumentBuilder builder = factory.newDocumentBuilder(); 
  
                 //Create a new Document object 
                 document = builder.newDocument();  
  
                 //Create MortgageApp - the root element in the XML  
                 Element root = (Element)document.createElement("LoanApp"); 
                 document.appendChild(root); 
                                              
                 //Create an XML element for Name 
                 Element nameElement = (Element)document.createElement("Name"); 
                 nameElement.appendChild(document.createTextNode(name)); 
                 root.appendChild(nameElement); 
                  
                 //Create an XML element for Phone 
                 Element phoneElement = (Element)document.createElement("PhoneOrEmail"); 
                 phoneElement.appendChild(document.createTextNode(phone)); 
                 root.appendChild(phoneElement); 
                  
                 //Create an XML element for amount 
                 Element loanElement = (Element)document.createElement("LoanAmount"); 
                 loanElement.appendChild(document.createTextNode(amount)); 
                 root.appendChild(loanElement); 
  
                 //Create an XML element for ApprovalStatus 
                 Element approveElement = (Element)document.createElement("ApprovalStatus"); 
                 approveElement.appendChild(document.createTextNode("PENDING APPROVAL")); 
                 root.appendChild(approveElement); 
                                  
               } 
          catch (Exception e) { 
                   System.out.println("The following exception occurred: "+e.getMessage()); 
                } 
         return document; 
          } 
         }
```

### Web アプリケーション用の Web ページの作成 {#create-the-web-page-for-the-web-application}

index.html *web ページは、 `FirstAppSolution/PreLoanProcess` プロセス。 この Web ページは、HTMLフォームと送信HTMLを含む基本的なボタンフォームです。 ユーザーが送信ボタンをクリックすると、フォームデータが `SubmitXML` Java サーブレット。

Java サーブレットは、次の Java コードを使用して、HTMLページから投稿されるデータをキャプチャします。

```as3
 //Get the values that are passed from the Loan HTML page 
 String name = request.getParameter("name"); 
 String phone = request.getParameter("phone"); 
 String amount = request.getParameter("amount");
```

次のHTMLコードは、開発環境のセットアップ中に作成された index.html ファイルを表しています。 ( [Web プロジェクトの作成](invoking-human-centric-long-lived.md#create-a-web-project).)

```as3
 <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd"> 
 <html> 
 <head> 
 <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1"> 
 <title>Insert title here</title> 
 </head> 
 <body> 
 <table> 
     <TBODY> 
         <TR> 
             <td><img src="financeCorpLogo.jpg" width="172" height="62"></TD> 
             <td><FONT size="+2"><strong>Java Loan Application Page</strong></FONT></TD> 
             <td> </TD> 
             <td> </TD> 
         </TR> 
          
     </TBODY> 
 </TABLE> 
     <FORM action="https://hiro-xp:8080/PreLoanProcess/SubmitXML" method="post"> 
        <table> 
          <TBODY> 
                <TR> 
                      <td><LABEL for="name">Name: </LABEL></TD> 
                  <td><INPUT type="text" name="name"></TD> 
                  <td><input type="submit" value="Submit Application"></TD> 
                  </TR> 
            <TR> 
                  <td> <LABEL for="phone">Phone/Email: </LABEL></TD> 
              <td><INPUT type="text" name="phone"></TD> 
                  <td></TD> 
              </TR> 
  
            <TR> 
                  <td><LABEL for="amount">Amount: </LABEL></TD> 
              <td><INPUT type="text" name="amount"></TD> 
                 <td></TD> 
             </TR> 
          </TBODY> 
 </TABLE> 
       </FORM> 
 </body> 
 </html>
```

### Web アプリケーションを WAR ファイルにパッケージ化する {#package-the-web-application-to-a-war-file}

を呼び出す Java サーブレットをデプロイするには、以下を実行します。 `FirstAppSolution/PreLoanProcess` プロセスで、Web アプリケーションを WAR ファイルにパッケージ化します。 コンポーネントのビジネスロジックが依存する外部 JAR ファイル（ adobe-livecycle-client.jar や adobe-usermanager-client.jar など）も WAR ファイルに含めるようにします。

次の図は、WAR ファイルにパッケージ化された Eclipse プロジェクトのコンテンツを示しています。

>[!NOTE]
>
>前の図では、JPGファイルは任意のJPG画像ファイルに置き換えることができます。

**Web アプリケーションを WAR ファイルにパッケージ化します。**

1. 次の **プロジェクトエクスプローラ** ウィンドウで、右クリック `InvokePreLoanProcess` プロジェクトと選択 **書き出し** > **WAR ファイル**.
1. 内 **Web モジュール** テキストボックス、タイプ `InvokePreLoanProcess` Java プロジェクトの名前。
1. 内 **宛先** テキストボックス、タイプ `PreLoanProcess.war`**の**&#x200B;ファイル名を指定し、WAR ファイルの場所を指定して、[ 完了 ] をクリックします。

### AEM Formsをホストする J2EE アプリケーションサーバーに WAR ファイルをデプロイする {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

WAR ファイルを、AEM Formsがデプロイされている J2EE アプリケーションサーバーにデプロイします。 WAR ファイルを J2EE アプリケーションサーバーにデプロイするには、WAR ファイルを書き出しパスからにコピーします。 *[AEM Forms Install]*\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy

>[!NOTE]
>
>AEM Formsが JBoss にデプロイされていない場合は、AEM Formsをホストする J2EE アプリケーションサーバーに準拠して WAR ファイルをデプロイする必要があります。

### Web アプリケーションのテスト {#test-your-web-application}

Web アプリケーションをデプロイした後、Web ブラウザーを使用してテストできます。 AEM Formsをホストしているコンピューターを使用している場合は、次の URL を指定できます。

* http://localhost:8080/PreLoanProcess/index.html

   「HTML・フォーム」フィールドに値を入力し、「アプリケーションの送信」ボタンをクリックします。 問題が発生した場合は、J2EE アプリケーションサーバーのログファイルを参照してください。

   >[!NOTE]
   >
   >Java アプリケーションがプロセスを呼び出したことを確認するには、Workspace を起動し、ローンを受け入れます。

## 人間中心の長期間有効なプロセスを呼び出す ASP.NET Web アプリケーションの作成 {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

を呼び出す ASP.NET アプリケーションを作成できます。 `FirstAppSolution/PreLoanProcess` プロセス。 ASP.NET アプリケーションからこのプロセスを呼び出すには、Web サービスを使用します。 ( [Web サービスを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

次の図は、エンドユーザーからデータを取得する ASP.NET クライアントアプリケーションを示しています。 データは XML データソースに配置され、 `FirstAppSolution/PreLoanProcess` ユーザーが「アプリケーションを送信」ボタンをクリックしたときに処理されます。

プロセスの呼び出し後に、呼び出し識別子の値が表示されます。 呼び出し識別子の値は、長期間有効なプロセスのステータスを追跡するレコードの一部として作成されます。

ASP.NET アプリケーションは、次のタスクを実行します。

* ユーザーが Web ページに入力した値を取得します。
* FirstAppSolution/PreLoanProcess *process に渡される XML データソースを動的に作成します。 3 つの値は、XML データソースで指定されます。
* Web サービスを使用して、* FirstAppSolution/PreLoanProcess *process を呼び出します。
* 呼び出し識別子の値と、長時間有効な操作の状態をクライアント Web ブラウザーに返します。

### 手順の概要 {#summary_of_steps-1}

FirstAppSolution/PreLoanProcess プロセスを呼び出す ASP.NET アプリケーションを作成するには、次の手順を実行します。

1. [ASP.NET Web アプリケーションの作成](invoking-human-centric-long-lived.md#create-an-asp-net-web-application).
1. [FirstAppSolution/PreLoanProcess を呼び出す ASP ページを作成します](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess).
1. [ASP.NET アプリケーションを実行します。](invoking-human-centric-long-lived.md#run-the-asp-net-application).

### ASP.NET Web アプリケーションの作成 {#create-an-asp-net-web-application}

Microsoft .NET C# ASP.NET Web アプリケーションを作成します。 次の図は、という名前の ASP.NET プロジェクトの内容を示しています。 *InvokePreLoanProcess*.

「サービス参照」の下に、2 つの項目があります。 最初の項目の名前は JobManager です。 この参照により、ASP.NET アプリケーションは Job Manager サービスを呼び出すことができます。 このサービスは、長期間有効なプロセスのステータスに関する情報を返します。 例えば、プロセスが現在実行中の場合、このサービスは現在実行中のプロセスを示す数値を返します。 2 つ目の参照は、*PreLoanProcess*. このサービスリファレンスは、* FirstAppSolution/PreLoanProcess *process への参照を表します。 サービス参照を作成したら、AEM Formsサービスに関連付けられているデータタイプを.NET プロジェクト内で使用できるようになります。

**ASP.NET プロジェクトを作成します。**

1. Microsoft Visual Studio 2008 を起動します。
1. 次の **ファイル** メニュー、選択 **新規**, **Web サイト**.
1. 内 **テンプレート** リスト、選択 **ASP.NET Web サイト**.
1. 内 **場所** ボックスで、プロジェクトの場所を選択します。 プロジェクトに名前を付ける *InvokePreLoanProcess*.
1. 内 **言語** ボックスで、「ビジュアル C#」を選択します。
1. 「OK」をクリックします。

**サービス参照の追加：**

1. プロジェクトメニューで、 **サービス参照を追加**.
1. 内 **住所** ダイアログボックスで、Job Manager サービスに対する WSDL を指定します。

   ```as3
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 「名前空間」フィールドに「 `JobManager`.
1. クリック **移動**&#x200B;次に、**OK**.
1. 内 **プロジェクト** メニュー、選択 **サービス参照を追加**.
1. 内 **住所** ダイアログボックスで、FirstAppSolution/PreLoanProcess プロセスの WSDL を指定します。

   ```as3
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 「名前空間」フィールドに「 `PreLoanProcess`.
1. クリック **移動**&#x200B;次に、**OK**.

>[!NOTE]
>
>置換 `hiro-xp` AEM Formsをホストする J2EE アプリケーションサーバーの IP アドレスを使用する この `lc_version` オプションを使用すると、MTOM などのAEM Forms機能が使用可能になります。 指定しない `lc_version`」オプションを使用する場合、MTOM を使用してAEM Formsを呼び出すことはできません。 ( [MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).)

### FirstAppSolution/PreLoanProcess を呼び出す ASP ページを作成します {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

ASP.NET プロジェクト内に、ローン申込者にHTMLページを表示する Web フォーム（ASPX ファイル）を追加します。 Web フォームは、から派生したクラスに基づいています `System.Web.UI.Page`. を呼び出す C#アプリケーションロジック `FirstAppSolution/PreLoanProcess` は `Button1_Click` メソッド（このボタンは、「アプリケーションを送信」ボタンを表します）。

次の図は、ASP.NET アプリケーションを示しています

次の表は、この ASP.NET アプリケーションの一部であるコントロールの一覧です。

<table> 
 <thead> 
  <tr> 
   <th><p>コントロール名</p></th> 
   <th><p>説明</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>TextBoxName</p></td> 
   <td><p>顧客の姓と名を指定します。 </p></td> 
  </tr> 
  <tr> 
   <td><p>TextBoxPhone</p></td> 
   <td><p>顧客の電話または電子メールアドレスを指定します。 </p></td> 
  </tr> 
  <tr> 
   <td><p>TextBoxAmount</p></td> 
   <td><p>ローン金額を指定します。</p></td> 
  </tr> 
  <tr> 
   <td><p>Button1</p></td> 
   <td><p>[ アプリケーションの送信 ] ボタンを表します。</p></td> 
  </tr> 
  <tr> 
   <td><p>LabelJobID</p></td> 
   <td><p>呼び出し識別子の値を指定する Label コントロール。</p></td> 
  </tr> 
  <tr> 
   <td><p>LabelStatus</p></td> 
   <td><p>ジョブステータスの値を指定する Label コントロール。 この値は、Job Manager サービスを呼び出して取得されます。 </p></td> 
  </tr> 
 </tbody> 
</table>

ASP.NET アプリケーションの一部であるアプリケーションロジックは、XML データソースを動的に作成し、 `FirstAppSolution/PreLoanProcess` プロセス。 申込者がHTMLページに入力した値は、XML データソース内で指定する必要があります。 これらのデータ値は、フォームが Workspace で表示される際に、フォームに結合されます。 内のクラス `System.Xml` 名前空間は、XML データソースの作成に使用されます。

ASP.NET アプリケーションから XML データを必要とするプロセスを呼び出す場合、XML データ型を使用できます。 つまり、 `System.Xml.XmlDocument` インスタンスをプロセスに追加します。 プロセスに渡す XML インスタンスの完全修飾名はです `InvokePreLoanProcess.PreLoanProcess.XML`. を `System.Xml.XmlDocument` インスタンスから `InvokePreLoanProcess.PreLoanProcess.XML`. このタスクは、次のコードを使用して実行できます。

```as3
 //Create the XML to pass to the FirstAppSolution/PreLoanProcess process 
 XmlDocument myXML = CreateXML(userName, phone, amount); 
      
 //Convert the XML to a InvokePreLoanProcess.PreLoanProcess.XML instance 
 StringWriter sw = new StringWriter(); 
 XmlTextWriter xw = new XmlTextWriter(sw); 
 myXML.WriteTo(xw); 
  
 InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML(); 
 inXML.document = sw.ToString();
```

を呼び出す ASP ページを作成するには `FirstAppSolution/PreLoanProcess` プロセス、 `Button1_Click` メソッド：

1. の作成 `FirstAppSolution_PreLoanProcessClient` オブジェクトのデフォルトのコンストラクタを使用します。
1. の作成 `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す string 値とエンコードの種類を指定します。

   ```as3
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます。 ただし、次の項目を指定する必要があります。 `?blob=mtom`.

   >[!NOTE]
   >
   >置換 `hiro-xp`* AEM Formsをホストする J2EE アプリケーションサーバーの IP アドレス*

1. の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` データメンバー。 戻り値を `BasicHttpBinding` にキャストします。
1. を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` データメンバー `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
1. 次のタスクを実行して、基本的な HTTP 認証を有効にします。

   * AEM forms ユーザー名をデータメンバーに割り当てる `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`.
   * 対応するパスワード値をデータメンバーに割り当てます。 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`.
   * 定数値を割り当て `HttpClientCredentialType.Basic` データメンバーに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` データメンバーに `BasicHttpBindingSecurity.Security.Mode`.

   次のコードの例に、これらのタスクを示します。

   ```as3
    //Enable BASIC HTTP authentication 
    BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding; 
    b.MessageEncoding = WSMessageEncoding.Mtom; 
    mortgageClient.ClientCredentials.UserName.UserName = "administrator"; 
    mortgageClient.ClientCredentials.UserName.Password = "password"; 
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic; 
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly; 
    b.MaxReceivedMessageSize = 2000000; 
    b.MaxBufferSize = 2000000; 
    b.ReaderQuotas.MaxArrayLength = 2000000;
   ```

1. ユーザーが Web ページに入力した名前、電話、金額の値を取得します。 これらの値を使用して、 `FirstAppSolution/PreLoanProcess` プロセス。 の作成 `System.Xml.XmlDocument` プロセスに渡す XML データソースを表す XML データソース（このアプリケーションロジックは次のコード例に示します）。
1. を `System.Xml.XmlDocument` インスタンスから `InvokePreLoanProcess.PreLoanProcess.XML` （このアプリケーションロジックは、次のコードの例に示します）。
1. を呼び出す `FirstAppSolution/PreLoanProcess` を呼び出して処理 `FirstAppSolution_PreLoanProcessClient` オブジェクトの `invoke_Async` メソッド。 このメソッドは、長期間有効なプロセスの呼び出し識別子の値を表す string 値を返します。
1. の作成 `JobManagerClient` を使用する場合は、コンストラクタです。 （Job Manager サービスへのサービス参照が設定されていることを確認してください）。
1. 手順 1 ～ 5 を繰り返します。 手順 2 で次の URL を指定します。 `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. コンストラクタを使用して `JobId` オブジェクトを作成します。
1. を `JobId` オブジェクトの `id` 返り値が `FirstAppSolution_PreLoanProcessClient` オブジェクトの `invoke_Async` メソッド。
1. を `value` 真 `JobId` オブジェクトの `persistent` データメンバー。
1. の作成 `JobStatus` を呼び出すことによってオブジェクトを取得 `JobManagerService` オブジェクト `getStatus` メソッドおよび `JobId` オブジェクト。
1. ステータス値を取得するには、 `JobStatus` オブジェクトの `statusCode` データメンバー。
1. 呼び出し識別子の値を `LabelJobID.Text` フィールドに入力します。
1. ステータス値を `LabelStatus.Text` フィールドに入力します。

### クイックスタート：Web サービス API を使用した長期間有効なプロセスの呼び出し {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

次の C#コードの例では、 `FirstAppSolution/PreLoanProcess`プロセス。

```as3
 ???/** 
     * Ensure that you create a .NET project that uses  
     * MS Visual Studio 2008 and version 3.5 of the .NET 
     * framework. This is required to invoke a  
     * AEM Forms service using MTOM. 
      
  
 using System; 
 using System.Collections; 
 using System.Configuration; 
 using System.Data; 
 using System.Linq; 
 using System.Web; 
 using System.ServiceModel; 
 using System.Web.Security; 
 using System.Web.UI; 
 using System.Web.UI.HtmlControls; 
 using System.Web.UI.WebControls; 
 using System.Web.UI.WebControls.WebParts; 
 using System.Xml.Linq; 
 using System.Xml; 
 using System.IO; 
  
 //A reference to FirstAppSolution/PreLoanProcess 
 using InvokePreLoanProcess.PreLoanProcess; 
  
 //A reference to JobManager service 
 using InvokePreLoanProcess.JobManager; 
  
  
 namespace InvokePreLoanProcess 
 { 
        public partial class _Default : System.Web.UI.Page 
        { 
            //This method is called when the Submit Application button is  
            //Clicked 
            protected void Button1_Click(object sender, EventArgs e) 
            { 
                //Create a FirstAppSolution_PreLoanProcessClient object 
                FirstAppSolution_PreLoanProcessClient mortgageClient = new FirstAppSolution_PreLoanProcessClient(); 
                mortgageClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom"); 
  
                //Enable BASIC HTTP authentication 
                BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding; 
                b.MessageEncoding = WSMessageEncoding.Mtom; 
                mortgageClient.ClientCredentials.UserName.UserName = "administrator"; 
                mortgageClient.ClientCredentials.UserName.Password = "password"; 
                b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic; 
                b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly; 
                b.MaxReceivedMessageSize = 2000000; 
                b.MaxBufferSize = 2000000; 
                b.ReaderQuotas.MaxArrayLength = 2000000; 
      
                //Retrieve values that user entered into the web page 
                String userName = TextBoxName.Text; 
                String phone = TextBoxPhone.Text; 
                String amount = TextBoxAmount.Text; 
  
                //Create the XML to pass to the FirstAppSolution/PreLoanProcess process 
                XmlDocument myXML = CreateXML(userName, phone, amount); 
      
                StringWriter sw = new StringWriter(); 
                XmlTextWriter xw = new XmlTextWriter(sw); 
                myXML.WriteTo(xw); 
  
                InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML(); 
                inXML.document = sw.ToString();  
  
                //INvoke the FirstAppSolution/PreLoanProcess process 
                String invocationID =  mortgageClient.invoke_Async(inXML); 
  
                //Create a JobManagerClient object to obtain the status of the long-lived operation 
                JobManagerClient jobManager = new JobManagerClient(); 
                jobManager.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/JobManager?blob=mtom"); 
  
                //Enable BASIC HTTP authentication 
                BasicHttpBinding b1 = (BasicHttpBinding)jobManager.Endpoint.Binding; 
                b1.MessageEncoding = WSMessageEncoding.Mtom; 
                jobManager.ClientCredentials.UserName.UserName = "administrator"; 
                jobManager.ClientCredentials.UserName.Password = "password"; 
                b1.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic; 
                b1.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly; 
                b1.MaxReceivedMessageSize = 2000000; 
                b1.MaxBufferSize = 2000000; 
                b1.ReaderQuotas.MaxArrayLength = 2000000; 
  
  
                //Create a JobID object that represents the status of the  
                //long-lived operation 
                JobId jobId = new JobId(); 
                jobId.id = invocationID; 
                jobId.persistent = true; 
                JobStatus jobStatus = jobManager.getStatus(jobId); 
                System.Int16 val2 = jobStatus.statusCode; 
                LabelJobID.Text = "The job status identifier value is " + invocationID;   
                LabelStatus.Text = "The status of the long-lived operation is " + getJobDescription(val2);  
      
            } 
  
            private static XmlDocument CreateXML(String name, String phone, String amount) 
            { 
                //This method dynamically creates a DDX document  
                //to pass to the FirstAppSolution/PreLoanProcess process 
                XmlDocument xmlDoc = new XmlDocument(); 
  
                //Create the root element and append it to the XML DOM         
                System.Xml.XmlElement root = xmlDoc.CreateElement("LoanApp"); 
                xmlDoc.AppendChild(root); 
  
                //Create the Name element 
                XmlElement nameElement = xmlDoc.CreateElement("Name"); 
                nameElement.AppendChild(xmlDoc.CreateTextNode(name)); 
                root.AppendChild(nameElement); 
  
                //Create the LoanAmount element 
                XmlElement LoanAmount = xmlDoc.CreateElement("LoanAmount"); 
                LoanAmount.AppendChild(xmlDoc.CreateTextNode(amount)); 
                root.AppendChild(LoanAmount); 
  
                //Create the PhoneOrEmail element 
                XmlElement PhoneOrEmail = xmlDoc.CreateElement("PhoneOrEmail"); 
                PhoneOrEmail.AppendChild(xmlDoc.CreateTextNode(phone)); 
                root.AppendChild(PhoneOrEmail); 
  
                //Create the ApprovalStatus element 
                XmlElement ApprovalStatus = xmlDoc.CreateElement("ApprovalStatus"); 
                ApprovalStatus.AppendChild(xmlDoc.CreateTextNode("PENDING APPROVAL")); 
                root.AppendChild(ApprovalStatus); 
  
                //Return the XmlElement instance 
                return xmlDoc; 
            } 
  
  
            //Returns the String value of the Job Manager status code 
            private String getJobDescription(int val) 
            { 
                switch(val) 
                { 
                    case 0: 
                        return "JOB_STATUS_UNKNOWN"; 
      
                    case 1:  
                        return "JOB_STATUS_QUEUED"; 
  
                    case 2:  
                        return "JOB_STATUS_RUNNING"; 
  
                    case 3:  
                        return "JOB_STATUS_COMPLETED";   
      
                    case 4:  
                        return "JOB_STATUS_FAILED";  
  
                     case 5:  
                        return "JOB_STATUS_COMPLETED";  
      
                    case 6:  
                        return "JOB_STATUS_SUSPENDED"; 
      
                    case 7:  
                        return "JOB_STATUS_COMPLETE_REQUESTED"; 
      
                    case 8:  
                        return "JOB_STATUS_TERMINATE_REQUESTED"; 
  
                     case 9:  
                        return "JOB_STATUS_SUSPEND_REQUESTED"; 
  
                       case 10:  
                        return "JOB_STATUS_RESUME_REQUESTED"; 
                } 
  
                return ""; 
            } 
       } 
 } 
 
```

>[!NOTE]
>
>getJobDescription ユーザー定義メソッド内の値は、Job Manager サービスが返す値に対応しています。

### ASP.NET アプリケーションを実行します。 {#run-the-asp-net-application}

ASP.NET アプリケーションをコンパイルして展開した後、Web ブラウザを使用して実行できます。 ASP.NET プロジェクトの名前が次のようになっているとします。 *InvokePreLoanProcess* Web ブラウザー内で次の URL を指定します。

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

localhost は ASP.NET プロジェクトをホストする Web サーバーの名前で、1629 はポート番号です。 ASP.NET アプリケーションをコンパイルしてビルドすると、Microsoft Visual Studio によって自動的にデプロイされます。

>[!NOTE]
>
>ASP.NET アプリケーションがこのプロセスを呼び出したことを確認するには、Workspace を起動し、ローンを受け入れます。

## 人間中心の長期間有効なプロセスを呼び出す、Flexで構築されたクライアントアプリケーションの作成 {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

Flexで構築したクライアントアプリケーションを作成し、 *FirstAppSolution/PreLoanProcess* プロセス。 このアプリケーションは、リモート処理を使用して *FirstAppSolution/PreLoanProcess* プロセス。 ( [(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

次の図に、Flexでエンドユーザーからデータを収集して構築したクライアントアプリケーションを示します。 データは XML データソースに配置され、プロセスに送信されます。

プロセスの呼び出し後に、呼び出し識別子の値が表示されます。 呼び出し識別子の値は、長期間有効なプロセスのステータスを追跡するレコードの一部として作成されます。

Flexで構築されたクライアントアプリケーションは、次のタスクを実行します。

* ユーザーが Web ページに入力した値を取得します。
* に渡される XML データソースを動的に作成します。 *FirstAppSolution/PreLoanProcess* プロセス。 3 つの値は、XML データソースで指定されます。
* を呼び出します。 *FirstAppSolution/PreLoanProcess* プロセスを実行します。
* 長期間有効なプロセスの呼び出し識別子の値を返します。

### 手順の概要 {#summary_of_steps-2}

FirstAppSolution/PreLoanProcess プロセスを呼び出すことができるFlexを使用して構築されたクライアントアプリケーションを作成するには、次の手順を実行します。

1. 新しいFlexプロジェクトを開始します。
1. プロジェクトのクラスパスに adobe-remoting-provider.swc ファイルを含めます。 ( [AEM Forms Flexライブラリファイルの取り込み](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file).)
1. の作成 `mx:RemoteObject` インスタンスをActionScriptまたはMXML経由で使用できます。 ( [mx:RemoteObject インスタンスの作成](/help/forms/developing/invoking-aem-forms-using-remoting.md))
1. の設定 `ChannelSet` AEM Formsと通信し、それを `mx:RemoteObject` インスタンス。 ( [AEM Formsへのチャネルの作成](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. チャネルセットの `login` メソッドまたはサービスの `setCredentials` メソッドを使用して、ユーザー識別子の値とパスワードを指定します。 ( [シングルサインオンの使用](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. に渡す XML データソースを作成します。 `FirstAppSolution/PreLoanProcess` プロセスを実行します。 （このアプリケーションロジックは次のコード例に示します）。
1. コンストラクタを使用して、Object 型のオブジェクトを作成します。 次のコードに示すように、プロセスの入力パラメーターの名前を指定して、XML をオブジェクトに割り当てます。

   ```as3
    //Get the XML data to pass to the AEM Forms process 
    var xml:XML = createXML(); 
    var params:Object = new Object(); 
    params["formData"]=xml;
   ```

1. を呼び出す `FirstAppSolution/PreLoanProcess` を呼び出すことによるプロセス `mx:RemoteObject` インスタンスの `invoke_Async` メソッド。 パス `Object` 入力パラメーターを格納する ( [入力値を渡す](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. 次のコードに示すように、長期間有効なプロセスから返される呼び出し識別値を取得します。

   ```as3
    // Handles async call that invokes the long-lived process 
    private function resultHandler(event:ResultEvent):void 
    { 
    ji = event.result as JobId; 
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;  
    }
   ```

### Remoting を使用した長期間有効なプロセスの呼び出し {#invoking-a-long-lived-process-using-remoting}

次のFlexコードの例では、 `FirstAppSolution/PreLoanProcess` プロセス。

```as3
 <?xml version="1.0" encoding="utf-8"?> 
  
 <mx:Application  xmlns="*" backgroundColor="#FFFFFF"  
      creationComplete="initializeChannelSet();"> 
  
 <mx:Script> 
          <![CDATA[ 
  
             import mx.controls.Alert; 
             import mx.rpc.events.FaultEvent; 
             import mx.rpc.events.ResultEvent; 
             import flash.net.navigateToURL; 
             import mx.messaging.ChannelSet; 
             import mx.messaging.channels.AMFChannel; 
             import mx.collections.ArrayCollection; 
             import mx.rpc.livecycle.JobId; 
             import mx.rpc.livecycle.JobStatus; 
             import mx.rpc.livecycle.DocumentReference; 
             import mx.formatters.NumberFormatter; 
      
             // Holds the job ID returned by LC.JobManager 
             private var ji:JobId;   
      
             private function initializeChannelSet():void  
              { 
              var cs:ChannelSet= new ChannelSet();  
         cs.addChannel(new AMFChannel("remoting-amf", "https://hiro-xp:8080/remoting/messagebroker/amf"));  
         LC_MortgageApp.setCredentials("tblue", "password"); 
         LC_MortgageApp.channelSet = cs; 
              } 
  
            private function submitApplication():void 
             { 
             //Get the XML data to pass to the AEM Forms process 
             var xml:XML = createXML(); 
             var params:Object = new Object(); 
             params["formData"]=xml; 
             LC_MortgageApp.invoke_Async(params); 
             } 
  
             // Handles async call that invokes the long-lived process 
             private function resultHandler(event:ResultEvent):void 
             { 
                ji = event.result as JobId; 
                jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;  
             } 
  
             private function createXML():XML 
             { 
                //Calculate the Mortgage value to place in the XML data 
                var propertyPrice:String = txtAmount.text ;  
                var name:String = txtName.text ; 
                var phone:String = txtPhone.text ;;  
      
                var model:XML =  
  
                  <LoanApp> 
                           <Name>{name}</Name> 
                           <LoanAmount>{propertyPrice}</LoanAmount> 
                           <PhoneOrEmail>{phone}</PhoneOrEmail>  
                           <ApprovalStatus>PENDING APPROVAL</ApprovalStatus> 
                  </LoanApp> 
      
              return model; 
             } 
      
      
          ]]> 
       </mx:Script> 
      
       <!-- Declare the RemoteObject and set its destination to the mortgage-app remoting endpoint defined in AEM Forms. --> 
       <mx:RemoteObject id="LC_MortgageApp" destination="FirstAppSolution/PreLoanProcess" result="resultHandler(event);"> 
          <mx:method name="invoke_Async" result="resultHandler(event)"/> 
      </mx:RemoteObject> 
  
  
     <mx:Grid x="229" y="186"> 
         <mx:GridRow width="100%" height="100%"> 
             <mx:GridItem width="100%" height="100%"> 
                 <mx:Image> 
                     <mx:source>file:///D|/LiveCycle_9/FirstApp/financeCorpLogo.jpg</mx:source> 
                 </mx:Image> 
             </mx:GridItem> 
             <mx:GridItem width="100%" height="100%"> 
                 <mx:Label text="Flex Loan Application Page" fontSize="20"/> 
             </mx:GridItem> 
             <mx:GridItem width="100%" height="100%"> 
             </mx:GridItem> 
         </mx:GridRow> 
         <mx:GridRow width="100%" height="100%"> 
             <mx:GridItem width="100%" height="100%"> 
                 <mx:Label text="Name:" fontSize="12" fontWeight="bold"/> 
             </mx:GridItem> 
             <mx:GridItem width="100%" height="100%"> 
                 <mx:TextInput id="txtName"/> 
             </mx:GridItem> 
             <mx:GridItem width="100%" height="100%"> 
                 <mx:Button label="Submit Application" click="submitApplication()"/> 
             </mx:GridItem> 
         </mx:GridRow> 
         <mx:GridRow width="100%" height="100%"> 
             <mx:GridItem width="100%" height="100%"> 
                 <mx:Label text="Phone/Email:" fontSize="12" fontWeight="bold"/> 
             </mx:GridItem> 
             <mx:GridItem width="100%" height="100%"> 
                 <mx:TextInput id="txtPhone"/> 
             </mx:GridItem> 
             <mx:GridItem width="100%" height="100%"> 
             </mx:GridItem> 
         </mx:GridRow> 
         <mx:GridRow width="100%" height="100%"> 
             <mx:GridItem width="100%" height="100%"> 
                 <mx:Label text="Amount:" fontSize="12" fontWeight="bold"/> 
             </mx:GridItem> 
             <mx:GridItem width="100%" height="100%"> 
                 <mx:TextInput id="txtAmount"/> 
             </mx:GridItem> 
             <mx:GridItem width="100%" height="100%"> 
             </mx:GridItem> 
         </mx:GridRow> 
         <mx:GridRow width="100%" height="100%"> 
             <mx:GridItem width="100%" height="100%"> 
             </mx:GridItem> 
             <mx:GridItem width="100%" height="100%"> 
                 <mx:Label text="Label" id="jobStatusDisplay" enabled="true" fontSize="12" fontWeight="bold"/> 
             </mx:GridItem> 
             <mx:GridItem width="100%" height="100%"> 
             </mx:GridItem> 
         </mx:GridRow> 
     </mx:Grid> 
      
 </mx:Application> 
 
```
