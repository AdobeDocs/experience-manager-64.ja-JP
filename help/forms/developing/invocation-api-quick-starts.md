---
title: 呼び出し API のクイックスタート
seo-title: Invocation API Quick Starts
description: クイックスタートを使用して、AEM Formsサービスをプログラムで呼び出します。
seo-description: Use the Quick Starts to programmatically invoke AEM Forms services.
uuid: acf67177-98a4-4c99-95a5-3086907d7c2c
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: dcf83c9f-b818-44a2-9079-80a4fc357c4f
role: Developer
exl-id: dcfc1c9f-fedd-4e00-9b09-19268620fc6d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 6%

---

# 呼び出し API のクイックスタート {#invocation-api-quick-starts}

次のクイックスタートは、AEM Formsサービスをプログラムで呼び出すために使用できます。

<table> 
 <thead> 
  <tr> 
   <th><p>説明</p></th> 
   <th><p>リモート API</p></th> 
   <th><p>Java API</p></th> 
   <th><p>Web サービス API</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#invoking_human_centric_long_lived_processes">人間中心の長期間有効なプロセスの呼び出し</a></p></td> 
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#invoking-a-long-lived-process-using-remoting">(AEM forms では廃止 )AEM Forms Remoting を使用した長期間有効なプロセスの呼び出し</a></p></td> 
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#quick_start_invoking_a_long_lived_process_using_the_invocation_api">クイックスタート：呼び出し API を使用した長期間有効なプロセスの呼び出し</a></p></td> 
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#quick_start_invoking_a_long_lived_process_using_the_web_service_api">クイックスタート：Web サービス API を使用した長期間有効なプロセスの呼び出し</a></p></td> 
  </tr> 
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking_a_short_lived_process_using_the_invocation_api">呼び出し API を使用した短時間のみ有効なプロセスの呼び出し</a></p></td> 
   <td><p>該当なし</p></td> 
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_short_lived_process_using_the_invocation_api">クイックスタート：呼び出し API を使用した短時間のみ有効なプロセスの呼び出し</a></p></td> 
   <td><p>該当なし</p></td> 
  </tr> 
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding">Base64 エンコーディングを使用したAEM Formsの呼び出し</a> （Java Web サービスプロキシ）</p></td> 
   <td><p>該当なし</p></td> 
   <td><p>該当なし</p></td> 
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_java_proxy_files_and_base64_encoding">クイックスタート：Java プロキシファイルと Base64 エンコーディングを使用したサービスの呼び出し</a></p></td> 
  </tr> 
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding">Base64 エンコーディングを使用したAEM Formsの呼び出し</a> （.NET Web サービスプロキシ）</p></td> 
   <td><p>該当なし</p></td> 
   <td><p>該当なし</p></td> 
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_base64_in_a_microsoft_net_project">クイックスタート：Microsoft .NET プロジェクトで base64 を使用したサービスの呼び出し</a></p></td> 
  </tr> 
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom">MTOM を使用したAEM Formsの呼び出し</a> （.NET Web サービスの例）</p></td> 
   <td><p>該当なし</p></td> 
   <td><p>該当なし</p></td> 
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_mtom_in_a_net_project">クイックスタート：.NET プロジェクトでの MTOM を使用したサービスの呼び出し</a></p></td> 
  </tr> 
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref">SwaRef を使用したAEM Formsの呼び出し</a> （Java Web サービスの例）</p></td> 
   <td><p>該当なし</p></td> 
   <td><p>該当なし</p></td> 
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_swaref_in_a_java_project">クイックスタート：Java プロジェクトでの SwaRef を使用したサービスの呼び出し</a></p></td> 
  </tr> 
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http">HTTP 経由での BLOB データを使用したAEM Formsの呼び出し</a> （Java Web サービスの例）</p></td> 
   <td><p>該当なし</p></td> 
   <td><p>該当なし</p></td> 
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_blob_data_over_http_in_a_net_project">クイックスタート：.NET プロジェクトで HTTP 経由での BLOB データを使用したサービスの呼び出し</a></p></td> 
  </tr> 
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http">HTTP 経由での BLOB データを使用したAEM Formsの呼び出し</a> （.NET Web サービスの例）</p></td> 
   <td><p>該当なし</p></td> 
   <td><p>該当なし</p></td> 
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_blob_data_over_http_in_a_java_project">クイックスタート：Java プロジェクトで HTTP 経由での BLOB データを使用したサービスの呼び出し</a></p></td> 
  </tr> 
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime">DIME を使用したAEM Formsの呼び出し</a> （Java Web サービスの例）</p></td> 
   <td><p>該当なし</p></td> 
   <td><p>該当なし</p></td> 
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_dime_in_a_java_project">クイックスタート：Java プロジェクトでの DIME を使用したサービスの呼び出し</a></p></td> 
  </tr> 
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し</a></p></td> 
   <td><p><a href="invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting">クイックスタート：AEM Forms Remoting (AEM forms では非推奨 ) を使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し</a></p></td> 
   <td><p>該当なし</p></td> 
   <td><p>該当なし</p></td> 
  </tr> 
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#passing_secure_documents_to_invoke_processes_using_remoting">リモート処理を使用してプロセスを呼び出すための安全なドキュメントの受け渡し</a></p></td> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting">クイックスタート：(AEM forms では非推奨 )AEM Forms Remoting を使用してセキュリティで保護されたドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し</a></p></td> 
   <td><p>該当なし</p></td> 
   <td><p>該当なし</p></td> 
  </tr> 
  <tr> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking_custom_component_services_using_remoting">リモート処理を使用したカスタムコンポーネントサービスの呼び出し</a></p></td> 
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#quick-start-invoking-the-customer-custom-service-using-remoting">クイックスタート：(AEM forms では廃止 )AEM Forms Remoting を使用した顧客カスタムサービスの呼び出し</a></p></td> 
   <td><p>該当なし</p></td> 
   <td><p>該当なし</p></td> 
  </tr> 
 </tbody> 
</table>

AEM Formsの操作は、AEM Formsの厳密に型指定された API を使用して実行できます。接続モードは、SOAP に設定する必要があります。

>[!NOTE]
>
>「AEM forms によるプログラミング」のクイックスタートは、JBoss Application Server とMicrosoft Windows オペレーティングシステムにデプロイされるFormsサーバーに基づいています。 ただし、UNIX などの別のオペレーティングシステムを使用している場合は、Windows 固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。 同様に、別の J2EE アプリケーションサーバーを使用する場合は、有効な接続プロパティを必ず指定してください。 詳しくは、 [接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## クイックスタート：呼び出し API を使用した短時間のみ有効なプロセスの呼び出し {#quick-start-invoking-a-short-lived-process-using-the-invocation-api}

次の Java コードの例では、という名前の短時間のみ有効なプロセスを呼び出しています。 `MyApplication/EncryptDocument`. このプロセスは同期的に呼び出されます。 このプロセスの入力パラメーターは、 `inDoc`. このプロセスの出力パラメーターは、 `outDoc`. パスワードで暗号化されたPDF・ドキュメントは、という名前のPDF・ファイルとして保存されます。 `EncryptLoan.pdf`. ( [呼び出し API を使用した短時間のみ有効なプロセスの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api).)

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-convertpdf-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. jacorb.jar (use a different JAR file if the forms server is not deployed on JBoss) 
     * 7. jnp-client.jar (use a different JAR file if the forms server is not deployed on JBoss) 
     * 
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
     * your local development environment and then include the 3 JBoss JAR files in your class path 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * The adobe-utilities.jar file is located in the following path: 
     * <install directory>/sdk/client-libs/jboss 
     * 
     * The jboss-client.jar file is located in the following path: 
     * <install directory>/jboss/bin/client 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include additional JAR files located in the following  
     * path 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * For information about the SOAP  
     * mode and the additional JAR files that need to be included,  
     * see "Setting connection properties" in Programming  
     * with AEM Forms 
     * 
     * For complete details about the location of the AEM Forms JAR files,  
     * see "Including AEM Forms Java library files" in Programming  
     * with AEM Forms 
     */ 
 import java.io.File; 
 import java.io.FileInputStream; 
 import java.io.InputStream; 
 import java.util.HashMap; 
 import java.util.Map; 
 import java.util.Properties; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.InvocationRequest; 
 import com.adobe.idp.dsc.InvocationResponse; 
 import com.adobe.idp.dsc.clientsdk.ServiceClient; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
      
  
     public class InvokeDocumentEncryptLooselyTypedAPI { 
  
         public static void main(String[] args) 
         { 
         try 
         { 
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
  
             // Create a ServiceClientFactory instance 
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); 
              
             //Create a ServiceClient object 
             ServiceClient myServiceClient = factory.getServiceClient(); 
  
             //Create a Map object to store the parameter value 
             Map params = new HashMap(); 
               
             InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf"); 
             Document inDoc = new Document(inFile); 
              
             //Populate the Map object with a parameter value  
             //required to invoke the MyApplication/EncryptDocument short-lived process 
             //inDoc refers to the name of the input parameter for the process 
             params.put("inDoc", inDoc);  
  
             //Create an InvocationRequest object 
             InvocationRequest request =  factory.createInvocationRequest( 
                     "MyApplication/EncryptDocument",        //Specify the short-lived process name 
                     "invoke",           //Specify the operation name     
                     params,               //Specify input values 
                     true);               //Create a synchronous request  
  
             //Send the invocation request to the short-lived process and  
             //get back an invocation response -- outDoc refers to the output parameter for the  
             //MyApplication/EncryptDocument process 
             InvocationResponse response = myServiceClient.invoke(request); 
             Document encryptDoc = (Document) response.getOutputParameter("outDoc"); 
              
             //Save the encrypted PDF document returned by the process 
             //Save the password-encrypted PDF document 
             File outFile = new File("C:\\Adobe\EncryptLoan.pdf"); 
             encryptDoc.copyToFile (outFile); 
             }catch (Exception e) { 
                 e.printStackTrace(); 
             } 
         } 
 }
```

## クイックスタート：Microsoft .NET プロジェクトで base64 を使用したサービスの呼び出し {#quick-start-invoking-a-service-using-base64-in-a-microsoft-net-project}

次の C#コードの例は、という名前のプロセスを呼び出します。 `MyApplication/EncryptDocument` Base64 エンコーディングを使用したMicrosoft .NET プロジェクトから。 ( [Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

という名前のPDFファイルに基づく保護されていないPDFドキュメント *Loan.pdf* がAEM Formsプロセスに渡されます。 このプロセスは、パスワードで暗号化されたPDF・ドキュメントを返します。このドキュメントは、という名前のPDF・ファイルとして保存されます。 *EncryptedPDF.pdf*.

```as3
 /* 
     * Ensure that you create a .NET client assembly that uses  
     * base64 encoding. This is required to populate a BLOB  
     * object with data or retrieve data from a BLOB object. 
     * 
     * For information, see "Invoking AEM Forms using Base64 Encoding" in  
     * Programming with AEM forms 
     */ 
 using System; 
 using System.Collections; 
 using System.ComponentModel; 
 using System.Data; 
 using System.IO; 
  
 namespace InvokeEncryptDocumentBase64 
 { 
  
        class InvokeEncryptDocumentUsingBase64 
        { 
  
            const int BUFFER_SIZE = 4096; 
            [STAThread] 
            static void Main(string[] args) 
            { 
  
                try 
                { 
                    String pdfFile = "C:\\Adobe\Loan.pdf"; 
                    String encryptedPDF = "C:\\Adobe\EncryptedPDF.pdf"; 
  
  
                    //Create an MyApplication_EncryptDocumentService object and set authentication values 
                    MyApplication2_EncryptDocumentService encryptClient = new MyApplication2_EncryptDocumentService(); 
                    encryptClient.Credentials = new System.Net.NetworkCredential("administrator", "password"); 
  
                    //Reference the PDF file to send to the EncryptDocument process 
                    FileStream fs = new FileStream(pdfFile, FileMode.Open); 
      
                    //Create a BLOB object 
                    BLOB inDoc = new BLOB(); 
  
                    //Get the length of the file stream  
                    int len = (int)fs.Length; 
                    byte[] ByteArray = new byte[len]; 
  
                    //Populate the byte array with the contents of the FileStream object 
                    fs.Read(ByteArray, 0, len); 
                    inDoc.binaryData = ByteArray;  
      
                    //Invoke the EncryptDocument process 
                    BLOB outDoc = encryptClient.invoke(inDoc); 
  
                    //Populate a byte array with BLOB data 
                    byte[] outByteArray = outDoc.binaryData; 
  
                    //Create a new file named UsageRightsLoan.pdf 
                    FileStream fs2 = new FileStream(encryptedPDF, FileMode.OpenOrCreate); 
  
                    //Create a BinaryWriter object 
                    BinaryWriter w = new BinaryWriter(fs2); 
                    w.Write(outByteArray); 
                    w.Close(); 
                    fs2.Close(); 
                 } 
                catch (Exception ee) 
                { 
                    Console.WriteLine(ee.Message); 
                } 
            } 
        } 
 } 
 
```

## クイックスタート：Java プロキシファイルと Base64 エンコーディングを使用したサービスの呼び出し {#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding}

次の Java コードの例は、という名前のプロセスを呼び出します。 `MyApplication/EncryptDocument` JAX-WS および Base64 エンコーディングを使用して作成された Java プロキシファイルを使用します。 ( [Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

という名前のPDFファイルに基づく保護されていないPDFドキュメント *Loan.pdf* がAEM Formsプロセスに渡されます。 このプロセスは、パスワードで暗号化されたPDF・ドキュメントを返します。このドキュメントは、という名前のPDF・ファイルとして保存されます。 *EncryptedDocument.pdf*.

```as3
 /** 
     * Ensure that you create Java proxy files that consume 
     * the AEM Forms service WSDL. You can use JAX-WS to create 
     * the Java proxy files.   
     * 
     * This Java quick start uses Base64 to invoke a short-lived process named 
     * EncryptDocument. For information, see  
     * "Invoking AEM Forms using Base64" in Programming with AEM forms.   
     */ 
  
 import java.io.*; 
  
 import javax.xml.ws.BindingProvider; 
 import com.adobe.idp.services.*; 
  
 public class InvokeEncryptDocumentBase64 { 
     public static void main(String[] args){ 
          
         try{ 
             //Create a MyApplicationEncryptDocument object 
             MyApplicationEncryptDocumentService encClient = new MyApplicationEncryptDocumentService(); 
             MyApplicationEncryptDocument encryptDocClient = encClient.getEncryptDocument(); 
              
             //Set connection values required to invoke AEM Forms 
             String url = "[server]:[port]/soap/services/MyApplication/EncryptDocument?blob=base64"; 
             String username = "administrator"; 
             String password = "password"; 
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url); 
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username); 
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password); 
              
                // Get the input PDF document to send to the EncryptDocument process 
                BLOB inDoc = new BLOB(); 
              
             // Get the input DDX document and input PDF sources 
             File fileName = new File("C:\\Adobe\Loan.pdf"); 
             FileInputStream inFs = new FileInputStream(fileName);  
                          
             // Get the length of the file stream and create a byte array 
             int inLen = (int)fileName.length(); 
             byte[] inByteArray = new byte[inLen]; 
              
                // Populate the byte array with the content of the file stream 
             inFs.read(inByteArray, 0, inLen); 
                   
                // Populate the BLOB objects 
             inDoc.setBinaryData(inByteArray); 
              
                //invoke the short-lived process named MyApplication/EncryptDocument 
             BLOB outDoc = encryptDocClient.invoke(inDoc); 
              
             //Save the encrypted file as a PDF file 
             byte[] encryptedDocument = outDoc.getBinaryData(); 
              
             //Create a File object 
             File outFile = new File("C:\\Adobe\EncryptedDocument.pdf"); 
              
             //Create a FileOutputStream object. 
             FileOutputStream myFileW = new FileOutputStream(outFile); 
              
             //Call the FileOutputStream object's write method and pass the pdf data 
             myFileW.write(encryptedDocument); 
              
             //Close the FileOutputStream object 
             myFileW.close(); 
                System.out.println("The short-lived process named MyApplication/EncryptDocument was successfully invoked.");             
         } 
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
      
     } 
  
 } 
  
 
```

## クイックスタート：AEM Forms Remoting (AEM forms では非推奨 ) を使用して安全でないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し {#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting}

次のFlexコードの例では、という名前の短時間のみ有効なプロセスを呼び出しています。 `MyApplication/EncryptDocument`. ( [(AEM forms では廃止 )AEM Forms Remoting を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

>[!NOTE]
>
>このクイックスタートでは、AEM Formsプロセスを呼び出し、安全でないドキュメントをアップロードします。 このクイックスタートを実行するには、安全でないドキュメントをアップロードするようにAEM Formsを設定する必要があります。 安全でないドキュメントを受け入れるようにAEM Formsを設定する方法について詳しくは、 [安全なドキュメントと安全でないドキュメントを受け入れるためのAEM Formsの設定](/help/forms/developing/invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).

```as3
 <?xml version="1.0" encoding="utf-8"?> 
 <mx:Application  xmlns="*"  
      creationComplete="initializeChannelSet();"> 
      <mx:Script> 
        <![CDATA[ 
      
      import mx.rpc.AEM Forms.DocumentReference; 
      import flash.net.FileReference; 
      import flash.net.URLRequest; 
      import flash.events.Event; 
      import flash.events.DataEvent; 
      import mx.messaging.ChannelSet; 
      import mx.messaging.channels.AMFChannel;   
      import mx.rpc.events.ResultEvent; 
      import mx.collections.ArrayCollection; 
      import mx.rpc.AsyncToken; 
      
       // Classes used in file retrieval   
      private var fileRef:FileReference = new FileReference(); 
      private var docRef:DocumentReference = new DocumentReference(); 
      private var parentResourcePath:String = "/"; 
      private var serverPort:String = "[server]:[port]"; 
      private var now1:Date;     
      private  var cs:ChannelSet 
      
      // Holds information returned from AEM Forms 
      [Bindable] 
      public var progressList:ArrayCollection = new ArrayCollection(); 
      
      // Set up channel set to invoke AEM Forms. 
      // This must be done before calling any service or process, but only  
      // once for the entire application. 
       private function initializeChannelSet():void { 
        cs = new ChannelSet();  
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));  
        EncryptDocument.setCredentials("administrator", "password"); 
        EncryptDocument.channelSet = cs; 
      } 
      
      // Call this method to upload the file. 
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process. 
      private function uploadFile():void { 
        fileRef.addEventListener(Event.SELECT, selectHandler); 
        fileRef.browse(); 
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
             var request:URLRequest = DocumentReference.constructRequestForUpload("https://[server]:[port]", token); 
              
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
        now1 = new Date(); 
      
        // Set the docRefs url and referenceType parameters 
        docRef.url = event.data as String;       
        docRef.referenceType=DocumentReference.REF_TYPE_URL; 
        executeInvokeProcess();  
      }       
      
      //This method invokes the EncryptDocument process 
      public function executeInvokeProcess():void { 
      
         //Create an Object to store the input value for the EncryptDocument process 
         var params:Object = new Object(); 
         params["inDoc"]=docRef; 
      
         // Invoke the EncryptDocument process 
         var token:AsyncToken;             
         token = EncryptDocument.invoke(params); 
         token.name = name; 
      } 
      
      // This method handles a successful conversion invocation 
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
          progObject.link = "<a href=" + dr.url + "> open </a>"; 
          progressList.addItem(progObject); 
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
        <mx:Button label="Select File" click="uploadFile()" /> 
      </mx:Panel> 
 </mx:Application> 
 
```

## クイックスタート：.NET プロジェクトでの DIME を使用したサービスの呼び出し {#quick-start-invoking-a-service-using-dime-in-a-net-project}

次の C#コードの例は、という名前のプロセスを呼び出します。 `MyApplication/EncryptDocument` Dime を使用してMicrosoft .NET プロジェクトから ( [Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).)

という名前のPDFファイルに基づく保護されていないPDFドキュメント *map.pdf* は、DIME を使用してAEM Formsプロセスに渡されます。 このプロセスは、パスワードで暗号化されたPDF・ドキュメントを返します。このドキュメントは、という名前のPDF・ファイルとして保存されます。 *mapEncrypt.pdf*.

```as3
 /** 
     * 
     * Ensure that you create a .NET project that uses  
     * Web Services Enhancements 2.0. This is required to send a  
     * AEM Forms process an attachment using DIME. 
     * 
     * For information, see "Invoking AEM Forms using DIME" in Programming with AEM forms.   
     */ 
  
 using System; 
 using System.Collections; 
 using System.ComponentModel; 
 using System.Data; 
 using System.IO; 
 using Microsoft.Web.Services2.Dime; 
 using Microsoft.Web.Services2.Attachments; 
 using Microsoft.Web.Services2.Configuration; 
 using Microsoft.Web.Services2; 
  
 //The following statement represents a web reference to 
 //the forms server that contains the process that 
 //is invoked 
 using ConsoleApplication1.LC_Host; 
  
 namespace ConsoleApplication1 
 { 
  
      class InvokeEncryptDocumentUsingDime 
        { 
  
            const int BUFFER_SIZE = 4096; 
            [STAThread] 
            static void Main(string[] args) 
            { 
  
            try 
               { 
                   String pdfFile = "C:\\Adobe\map.pdf"; 
                   String encryptedPDF = "C:\\Adobe\mapEncrypt.pdf"; 
      
                   //Create an EncryptDocumentServiceWse object and set authentication values 
                   EncryptDocumentServiceWse encryptClient = new EncryptDocumentServiceWse(); 
                   encryptClient.Credentials = new System.Net.NetworkCredential("administrator", "password"); 
  
                   // Create the DIME attachment representing a PDF document 
                   DimeAttachment inputDocAttachment = new DimeAttachment( 
                       System.Guid.NewGuid().ToString(), 
                       "application/pdf", 
                       TypeFormat.MediaType, 
                       pdfFile); 
      
                    //Create a BLOB object 
                    BLOB inDoc = new BLOB(); 
      
                    //Set the DIME attachment ID 
                    inDoc.attachmentID = inputDocAttachment.Id; 
                    encryptClient.RequestSoapContext.Attachments.Add(inputDocAttachment); 
      
                    //Invoke the EncryptDocument process 
                    BLOB outDoc = encryptClient.invoke(inDoc); 
      
                    //Get the returned attachment identifier value     
                    String encryptedDocId = outDoc.attachmentID; 
                    FileStream myStream = new FileStream(encryptedPDF, FileMode.Create, FileAccess.Write); 
      
                    //Iterate through the attachments 
                    foreach (Attachment attachment in encryptClient.ResponseSoapContext.Attachments) 
                      { 
                        if (attachment.Id.Equals(encryptedDocId)) 
                          { 
                            //Create a byte array that contains the encrypted PDF document 
                            System.IO.Stream mySteam2 = attachment.Stream; 
                            byte[] myBytes = new byte[mySteam2.Length]; 
                            int size = (int)mySteam2.Length; 
                            mySteam2.Read(myBytes, 0, size); 
      
                            //Save the encrypted PDF document as a PDF file 
                            FileStream fs2 = new FileStream(encryptedPDF, FileMode.OpenOrCreate); 
      
                            //Create a BinaryWriter object 
                            BinaryWriter w = new BinaryWriter(fs2); 
                            w.Write(myBytes); 
                            w.Close(); 
                            fs2.Close(); 
                            Console.Out.WriteLine("Saved converted document at:" + encryptedPDF); 
                        } 
                   } 
                } 
                catch (Exception ee) 
               { 
                   Console.WriteLine(ee.Message); 
                } 
            } 
        } 
 } 
 
```

## クイックスタート：Java プロジェクトでの DIME を使用したサービスの呼び出し {#quick-start-invoking-a-service-using-dime-in-a-java-project}

次の Java コードの例は、という名前のプロセスを呼び出します。 `MyApplication/EncryptDocument` DIME を使用して。 ( [DIME を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime).)

という名前のPDFファイルに基づく保護されていないPDFドキュメント *Loan.pdf* は、DIME を使用してAEM Formsプロセスに渡されます。 このプロセスは、パスワードで暗号化されたPDF・ドキュメントを返します。このドキュメントは、という名前のPDF・ファイルとして保存されます。 *EncryptLoan.pdf*.

```as3
 /** 
     * Ensure that you create Java Axis files that  
     * are required to send a AEM Forms process  
     * an attachment using DIME. 
     * 
     * For information, see "Invoking AEM Forms using DIME" in Programming with AEM forms.   
     */ 
 import com.adobe.idp.services.*; 
 import java.io.File; 
 import java.io.FileOutputStream; 
 import java.io.InputStream; 
 import java.net.URL; 
 import javax.activation.DataHandler; 
 import javax.activation.FileDataSource; 
  
 import org.apache.axis.attachments.AttachmentPart; 
  
 public class InvokeDocumentEncryptDime { 
     public static void main(String[] args) { 
      
     try{ 
          
         //Create a MyApplicationEncryptDocumentServiceLocator object 
         MyApplicationEncryptDocumentServiceLocator locate = new MyApplicationEncryptDocumentServiceLocator (); 
  
         //specify the service target URL and object type 
         URL serviceURL = new URL("https://[server]:[port]/soap/services/MyApplication/EncryptDocument?blob=dime"); 
          
         //Use the binding stub with the locator 
         EncryptDocumentSoapBindingStub encryptionClientStub = new EncryptDocumentSoapBindingStub(serviceURL,locate); 
         encryptionClientStub.setUsername("administrator"); 
         encryptionClientStub.setPassword("password");     
              
          //Get the DIME Attachments - which is the PDF document to encrypt 
          java.io.File file = new java.io.File("C:\\Adobe\Loan.pdf"); 
                        
          //Create a DataHandler object 
          DataHandler buildFile = new DataHandler(new FileDataSource(file)); 
           
          //Use the DataHandler object to create an AttachmentPart object  
          AttachmentPart part = new AttachmentPart(buildFile); 
         //get the attachment ID 
         String attachmentID = part.getContentId();     
          
         //Add the attachment to the encryption service stub 
         encryptionClientStub.addAttachment(part);  
                                  
         //Inform ES where the attachment is stored by providing the attachment id 
         BLOB inDoc = new BLOB(); 
         inDoc.setAttachmentID(attachmentID); 
                          
         BLOB outDoc = encryptionClientStub.invoke(inDoc); 
  
         //Go through the returned attachments and get the encrypted PDF document 
         byte[] resultByte = null;         
         attachmentID = outDoc.getAttachmentID(); 
          
         //Find the proper attachment 
         Object[] parts = encryptionClientStub.getAttachments(); 
         for (int i=0;i<parts.length;i++){ 
             AttachmentPart attPart = (AttachmentPart)  parts[i]; 
             if (attPart.getContentId().equals(attachmentID)) { 
                 //DataHandler 
                 buildFile = attPart.getDataHandler(); 
                 InputStream stream = buildFile.getInputStream();  
                  
                 byte[] pdfStream = new byte[stream.available()]; 
                 stream.read(pdfStream); 
                  
                 //Create a File object 
                 File outFile = new File("C:\\Adobe\EncryptLoan.pdf"); 
                  
                 //Create a FileOutputStream object. 
                 FileOutputStream myFileW = new FileOutputStream(outFile); 
                  
                 //Call the FileOutputStream object?s write method and pass the pdf data 
                 myFileW.write(pdfStream); 
                  
                 //Close the FileOutputStream object 
                 myFileW.close(); 
                  
             } 
         } 
     } 
     catch(Exception e) 
     { 
         e.printStackTrace(); 
     } 
     } 
  
 } 
 
```

## クイックスタート：Java プロジェクトで HTTP 経由での BLOB データを使用したサービスの呼び出し {#quick-start-invoking-a-service-using-blob-data-over-http-in-a-java-project}

次の Java コードの例は、という名前のプロセスを呼び出します。 `MyApplication/EncryptDocument` HTTP 経由でのデータの使用。 ( [HTTP 経由での BLOB データを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http).)

という名前のPDFファイルに基づく保護されていないPDFドキュメント *Loan.pdf* は、SOAP over HTTP を使用してAEM Formsプロセスに渡されます。 PDFファイルは次の URL にあります。 `https://[server]:[port]/FormsQS`. このプロセスは、パスワードで暗号化されたPDF・ドキュメントを返します。このドキュメントは、という名前のPDF・ファイルとして保存されます。 *EncryptedDocument.pdf*.

```as3
 /** 
     * Ensure that you create Java proxy files that consume 
     * the AEM Forms service WSDL. You can use JAX-WS to create 
     * the Java proxy files.   
     * 
     * This Java quick start uses BLOB over HTTP to invoke a short-lived process named 
     * EncryptDocument. For information, see  
     * "Invoking AEM Forms using BLOB over HTTP" in Programming with AEM forms.   
     */ 
 import java.io.*; 
 import java.net.URL; 
  
 import javax.xml.ws.BindingProvider; 
 import com.adobe.idp.services.*; 
  
 public class InvokeEncryptDocumentHTTP { 
     public static void main(String[] args){ 
          
         try{ 
             //Create a MyApplicationEncryptDocument object 
             MyApplicationEncryptDocumentService encClient = new MyApplicationEncryptDocumentService(); 
             MyApplicationEncryptDocument encryptDocClient = encClient.getEncryptDocument(); 
              
             //Set connection values required to invoke AEM Forms using BLOB over HTTP 
             String url = "https://[server]:[port]/soap/services/MyApplication/EncryptDocument?blob=http"; 
             String username = "administrator"; 
             String password = "password"; 
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url); 
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username); 
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password); 
              
             //Create a BLOB object and populate it by invoking the setRemoteURL method 
             BLOB inDoc = new BLOB(); 
             inDoc.setRemoteURL("https://[server]:[port]/FormsQS/Loan.pdf"); 
              
                //invoke the short-lived process named MyApplication/EncryptDocument 
             BLOB outDoc = encryptDocClient.invoke(inDoc); 
              
             //Retrieve an InputStream from the returned BLOB instance 
             URL myURL = new URL(outDoc.getRemoteURL()); 
             InputStream inputStream = myURL.openStream(); 
              
             //Create a new file containing the returned PDF document 
             File f = new File("C:\\Adobe\EncryptedDocument.pdf"); 
             OutputStream out = new FileOutputStream(f); 
              
             //Iterate through the buffer 
             byte buf[] = new byte[1024]; 
             int len; 
             while ((len = inputStream.read(buf)) > 0) 
                 out.write(buf, 0, len); 
             out.close(); 
             inputStream.close(); 
              
              System.out.println("The short-lived process named EncryptDocument was successfully invoked.");             
         } 
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
      
     } 
  
 } 
  
 
```

## クイックスタート：.NET プロジェクトで HTTP 経由での BLOB データを使用したサービスの呼び出し {#quick-start-invoking-a-service-using-blob-data-over-http-in-a-net-project}

次の C#コードの例は、という名前のプロセスを呼び出します。 `MyApplication/EncryptDocument` HTTP 経由のデータを使用してMicrosoft .NET プロジェクトから ( [HTTP 経由での BLOB データを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http).)

という名前のPDFファイルに基づく保護されていないPDFドキュメント *Loan.pdf* は、BLOB over HTTP を使用してAEM Formsプロセスに渡されます。 このプロセスは、パスワードで暗号化されたPDF・ドキュメントを返します。このドキュメントは、という名前のPDF・ファイルとして保存されます。 *EncryptedPDF.pdf*.

```as3
 /* 
     * Ensure that you create a .NET client assembly that uses  
     * SOAP over HTTP. This is required to populate a BLOB  
     * object’s remote URL data memeber. 
     * 
     * For information, see "Invoking AEM Forms using BLOB data over HTTP" in  
     * Programming with AEM forms 
     */ 
 using System; 
 using System.Collections; 
 using System.ComponentModel; 
 using System.Data; 
 using System.IO; 
 using System.Security.Policy; 
  
 namespace InvokeEncryptDocumentHTTP 
 { 
  
        class InvokeEncryptDocumentUsingHTTP 
        { 
  
            const int BUFFER_SIZE = 4096; 
            [STAThread] 
            static void Main(string[] args) 
            { 
  
                try 
                { 
                    String urlData = "https://[server]:[port]/FormsQS/Loan.pdf"; 
  
                    //Create a MyApplication_EncryptDocumentService object and set authentication values 
                    MyApplication_EncryptDocumentService encryptClient = new MyApplication_EncryptDocumentService(); 
                    encryptClient.Credentials = new System.Net.NetworkCredential("administrator", "password"); 
  
                    //Create a BLOB object 
                    BLOB inDoc = new BLOB(); 
  
                    //Populate the BLOB object’s remoteURL data member 
                    inDoc.remoteURL = urlData; 
  
                    //Invoke the EncryptDocument process 
                    BLOB outDoc = encryptClient.invoke(inDoc); 
  
                    //Create a UriBuilder object using the  
                    //BLOB object’s remoteURL data member field 
                    UriBuilder uri = new UriBuilder(outDoc.remoteURL); 
  
                   //Convert the UriBuilder to a Stream object 
                    System.Net.WebRequest wr = System.Net.WebRequest.Create(uri.Uri); 
                    System.Net.WebResponse response = wr.GetResponse(); 
                    System.IO.StreamReader sr = new System.IO.StreamReader(response.GetResponseStream()); 
                    Stream mySteam = sr.BaseStream; 
  
                    //Create a byte array 
                    byte[] myData = new byte[BUFFER_SIZE]; 
  
                   //Populate the byte array 
                   PopulateArray(mySteam, myData); 
  
                   //Create a new file named UsageRightsLoan.pdf 
                   FileStream fs2 = new FileStream("C:\\Adobe\EncryptedPDF.pdf", FileMode.OpenOrCreate); 
  
                   //Create a BinaryWriter object 
                   BinaryWriter w = new BinaryWriter(fs2); 
                   w.Write(myData); 
                   w.Close(); 
                   fs2.Close(); 
                } 
                catch (Exception ee) 
                { 
                    Console.WriteLine(ee.Message); 
                } 
            } 
  
            public static void PopulateArray(Stream stream, byte[] data) 
            { 
                int offset = 0; 
                int remaining = data.Length; 
                while (remaining > 0) 
                { 
                    int read = stream.Read(data, offset, remaining); 
                    if (read <= 0) 
                        throw new EndOfStreamException(); 
                    remaining -= read; 
                    offset += read; 
                } 
            } 
      
        } 
 } 
 
```

## クイックスタート：.NET プロジェクトでの MTOM を使用したサービスの呼び出し {#quick-start-invoking-a-service-using-mtom-in-a-net-project}

次の C#コードの例は、という名前のプロセスを呼び出します。 `MyApplication/EncryptDocument` MTOM を使用したMicrosoft .NET プロジェクトから。 ( [MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).)

という名前のPDFファイルに基づく保護されていないPDFドキュメント *loan.pdf* は、MTOM を使用してAEM Formsプロセスに渡されます。 このプロセスは、パスワードで暗号化されたPDF・ドキュメントを返します。このドキュメントは、という名前のPDF・ファイルとして保存されます。 *EncryptedDocument.pdf*.

```as3
 ???/** 
     * Ensure that you create a .NET project that uses  
     * MS Visual Studio 2008 and version 3.5 of the .NET 
     * framework. This is required to invoke a  
     * AEM Forms service using MTOM. 
     * 
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms  
     */ 
 using System; 
 using System.Collections.Generic; 
 using System.Linq; 
 using System.Text; 
 using System.ServiceModel; 
 using EncryptDocumentMTOM.ServiceReference1; 
 using System.IO; 
  
 //Invoke the EncryptDocument process using MTOM 
 namespace EncryptDocumentUsingMTOM 
 { 
        class Program 
        { 
            static void Main(string[] args) 
            { 
                try 
                { 
                    //Specify the name of the PDF file to encrypt 
                    String pdfFile = "C:\\Adobe\loan.pdf"; 
  
                    //Create an EncryptDocumentClient object 
                    MyApplication_EncryptDocumentClient encryptProcess = new MyApplication_EncryptDocumentClient(); 
                    encryptProcess.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://[server]:[port]/soap/services/MyApplication/EncryptDocument?blob=mtom"); 
                    BasicHttpBinding b = (BasicHttpBinding)encryptProcess.Endpoint.Binding; 
                    b.MessageEncoding = WSMessageEncoding.Mtom; 
  
                    //Enable BASIC HTTP authentication 
                    encryptProcess.ClientCredentials.UserName.UserName = "administrator"; 
                    encryptProcess.ClientCredentials.UserName.Password = "password"; 
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic; 
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly; 
                    b.MaxReceivedMessageSize = 4000000; 
                    b.MaxBufferSize = 4000000; 
                    b.ReaderQuotas.MaxArrayLength = 4000000; 
      
                    //Reference the PDF file to send to the EncryptDocument process 
                    FileStream fs = new FileStream(pdfFile, FileMode.Open); 
  
                    //Create a BLOB object 
                    BLOB inDoc = new BLOB(); 
  
                    //Get the length of the file stream  
                    int len = (int)fs.Length; 
                    byte[] ByteArray = new byte[len]; 
  
                    //Populate the byte array with the contents of the FileStream object 
                    fs.Read(ByteArray, 0, len); 
                    inDoc.MTOM = ByteArray; 
      
                    //Invoke the EncryptDocument short-lived process 
                    BLOB outDoc = encryptProcess.invoke(inDoc); 
                    byte[] encryptDoc = outDoc.MTOM; 
  
                    //Create a new file containing the encrypted PDF document 
                    string FILE_NAME = "C:\\Adobe\EncryptedDocument.pdf"; 
                    FileStream fs2 = new FileStream(FILE_NAME, FileMode.OpenOrCreate); 
                    BinaryWriter w = new BinaryWriter(fs2); 
                    w.Write(encryptDoc); 
                    w.Close(); 
                    fs2.Close(); 
                } 
                catch (Exception ee) 
                { 
                    Console.WriteLine(ee.Message); 
                } 
            } 
        } 
 } 
 
```

>[!NOTE]
>
>AEM Formsサービスの操作の実行方法を示すクイックスタートの多くには、MTOM コードの例が含まれています。

## クイックスタート：Java プロジェクトでの SwaRef を使用したサービスの呼び出し {#quick-start-invoking-a-service-using-swaref-in-a-java-project}

次の Java コードの例は、という名前のプロセスを呼び出します。 `MyApplication/EncryptDocument` を Java プロジェクトから取得します。 この Java プロジェクトでは、JAX-WS と SwaRef をエンコーディングタイプとして使用して作成されたプロキシクラスを使用します。 ( [SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref).)

という名前のPDFファイルに基づく保護されていないPDFドキュメント *Loan.pdf* は、SwaRef を使用してAEM Formsプロセスに渡されます。 暗号化されたPDFドキュメントは、という名前のPDFファイルとして保存されます *EncryptedDocument.pdf*.

```as3
 /** 
     * Ensure that you create Java proxy files that consume 
     * the AEM Forms service WSDL. You can use JAX-WS to create 
     * the Java proxy files.   
     * 
     * This Java quick start uses SwaRef to invoke a short-lived process named 
     * EncryptDocument. For information, see  
     * "Invoking AEM Forms using SwaRef" in Programming with AEM forms.   
     */ 
  
 import javax.xml.ws.BindingProvider; 
 import javax.activation.DataHandler; 
 import javax.activation.DataSource; 
 import javax.activation.FileDataSource;  
 import java.io.*; 
  
 import com.adobe.idp.services.*; 
  
 public class InvokeEncryptDocumentSwaRef { 
  
 public static void main(String[] args) { 
          
         try{ 
              
         //Specify connection values required to invoke the MyApplication/EncryptDocument process  
         //using SwaRef     
         String url = "https://[server]:[port]/soap/services/MyApplication/EncryptDocument?blob=swaref"; 
         String username = "administrator"; 
         String password = "password"; 
         String pdfFile = "C:\\Adobe\Loan.pdf"; 
          
         //Create a MyApplicationEncryptDocument object 
         MyApplicationEncryptDocumentService encClient = new MyApplicationEncryptDocumentService(); 
         MyApplicationEncryptDocument encryptDocClient = encClient.getEncryptDocument(); 
          
         ((BindingProvider)encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url); 
         ((BindingProvider)encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username); 
         ((BindingProvider)encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password); 
           
          //Create a file object 
          File pdf = new File(pdfFile);  
           
          //Create a DataSource object 
          DataSource myDS = new FileDataSource(pdf); 
           
          //Create a DataHandler object 
          DataHandler dataHandler = new DataHandler(myDS);  
                                         
         //Create a BLOB object and populate it with the DataHandler 
         BLOB inDoc = new BLOB(); 
         inDoc.setSwaRef(dataHandler); 
          
         //Invoke the EncryptDocument process 
         BLOB outDoc = encryptDocClient.invoke(inDoc);   
          
         //Save the encrypted file as a PDF file 
         DataHandler handler = outDoc.getSwaRef(); 
          
         //Create a new file containing the returned PDF document 
         File f = new File("C:\\Adobe\EncryptedDocument.pdf"); 
         InputStream inputStream = handler.getInputStream(); 
         OutputStream out = new FileOutputStream(f); 
          
         //Iterate through the buffer 
         byte buf[] = new byte[1024]; 
         int len; 
         while ((len = inputStream.read(buf)) > 0) 
             out.write(buf, 0, len); 
         out.close(); 
         inputStream.close(); 
  
          System.out.println("The short-lived process named MyApplication/EncryptDocument was successfully invoked.");             
              
         }catch (Exception e) { 
              e.printStackTrace(); 
             }     
         } 
 } 
  
 
```

>[!NOTE]
>
>サービス操作の実行方法を示すクイックスタートの多くには、SwaRef コード例が含まれます。
