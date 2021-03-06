---
title: Forms Service API クイックスタート
seo-title: Forms Service API Quick Starts
description: Forms Service API のクイックスタートを使用する。
seo-description: Use the Quick Starts for the Forms Service API.
uuid: dfce259a-e392-4929-ad7e-6d902faceaeb
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: 9fe48243-24c6-4e08-9886-148cd99dec87
role: Developer
exl-id: abc2af58-3bf7-493e-917d-081022afb9a3
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 0%

---

# Forms Service API クイックスタート {#forms-service-api-quick-starts}

Formsサービスでは、次のクイックスタートを使用できます。

[クイックスタート（SOAP モード）:Java API を使用したインタラクティブPDFフォームのレンダリング](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-interactive-pdf-form-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用してクライアントでフォームをレンダリングする](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用したフラグメントに基づくフォームのレンダリング](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用した権限が有効なフォームのレンダリング](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用したHTMLフォームのレンダリング](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用した、カスタムHTMLでのツールバーでのツールバーフォームのレンダリング](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用して、XML として送信されたPDF formsの処理](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用して、PDFとして送信されたPDF formsの処理](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用して、XML として送信されたHTMLフォームの処理](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用した、送信済み XML データを使用したPDFドキュメントの作成](forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用した、Formsへの編集可能なレイアウトの自動埋め込み](forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用した計算スクリプトを含むフォームの処理](forms-service-api-quick-starts.md#quick-start-soap-mode-handling-a-form-containing-a-calculation-script-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用したパフォーマンスの最適化](forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用した値によるレンダリング](forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用してForms Service にドキュメントを渡す](forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

Forms Service API を使用するアプリケーションロジックは Java サーブレットとして実装されています。 AEM Formsの操作は、AEM Formsの厳密に型指定された API を使用して実行できます。接続モードは、SOAP に設定する必要があります。

>[!NOTE]
>
>「 v によるプログラミング」のクイックスタートは、Unix などの別のオペレーティングシステムを使用している forms サーバーに基づいています。windows 固有のパスは、該当するオペレーティングシステムでサポートされているパスに置き換えます。 同様に、別の J2EE アプリケーションサーバーを使用している場合は、有効な接続プロパティを指定する必要があります。 詳しくは、 [接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).


## クイックスタート（SOAP モード）:Java API を使用したインタラクティブPDFフォームのレンダリング {#quick-start-soap-mode-rendering-an-interactive-pdf-form-using-the-java-api}

次のコードの例では、という名前のインタラクティブなPDFフォームをレンダリングします。 *Loan.xdp* クライアントの Web ブラウザーにコピーします。 ファイルがフォームに添付されます。 フォームデザインはアプリケーションの一部で、コンテンツルート URI 値を使用して参照されています `repository:///`. ( [インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
     * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms. 
     */ 
 import java.io.FileInputStream; 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
  
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
 import java.util.*; 
 import java.io.InputStream; 
  
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RenderPDFForm extends HttpServlet implements Servlet { 
  
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
             doPost(req,resp); 
     } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
         try{ 
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
             //Create a FormsServiceClient object 
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
             //Set the parameter values for the renderPDFForm method 
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";   
                      
             byte[]    cData = "".getBytes(); 
             Document oInputData = new Document(cData); 
                                      
             //Set run-time options using a PDFFormRenderSpec instance 
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec(); 
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true)); 
             pdfFormRenderSpec.setAcrobatVersion(AcrobatVersion.Acrobat_9); 
                      
             //Specify URI values that are required to render a form 
             URLSpec uriValues = new URLSpec();  
             uriValues.setApplicationWebRoot("https://[server]:[port]/FormsQS"); 
             uriValues.setContentRootURI("repository:///"); 
             uriValues.setTargetURL("https://[server]:[port]/FormsQS/HandleData"); 
                      
             //Specify file attachments to attach to the form 
             FileInputStream fileAttachment = new FileInputStream("C:\\rideau1.jpg");  
             Document attachment1 = new Document(fileAttachment); 
             String fileName = "rideau1.jpg"; 
             Map fileAttachments = new HashMap(); 
             fileAttachments.put(fileName, attachment1);  
                          
             //Invoke the renderPDFForm method and write the  
             //results to a client web browser 
             FormsResult formOut = formsClient.renderPDFForm( 
                         formName,               //formQuery 
                         oInputData,             //inDataDoc 
                         pdfFormRenderSpec,      //PDFFormRenderSpec 
                         uriValues,                //urlSpec 
                         fileAttachments            //attachments 
                         ); 
          
             //Create a Document object that stores form data 
             Document myData = formOut.getOutputContent(); 
          
             //Get the content type of the response and 
             //set the HttpServletResponse objects content type 
             String contentType = myData.getContentType();  
             resp.setContentType(contentType); 
          
             //Create a ServletOutputStream object 
             ServletOutputStream oOutput = resp.getOutputStream(); 
          
             //Create an InputStream object 
             InputStream inputStream = myData.getInputStream(); 
          
             //Write the data stream to the web browser 
             byte[] data = new byte[4096]; 
             int bytesRead = 0; 
             while ((bytesRead = inputStream.read(data)) > 0) 
             { 
                 oOutput.write(data, 0, bytesRead); 
             } 
          
             }catch (Exception e) { 
                  e.printStackTrace(); 
               } 
         } 
 }
```

## クイックスタート（SOAP モード）:Java API を使用してクライアントでフォームをレンダリングする {#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api}

次のコードの例では、Formsサービス Java API を使用して、クライアントで Loan.xdp という名前のフォームをレンダリングします。 フォームデザインはアプリケーションの一部で、コンテンツルート URI 値を使用して参照されています `repository:///`. ( [クライアントでのFormsのレンダリング](/help/forms/developing/rendering-forms.md#rendering-forms-at-the-client).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
    * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms. 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
 import java.util.*; 
 import java.io.InputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RenderPDFFormClient extends HttpServlet implements Servlet { 
      
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
              
             doPost(req,resp); 
     } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
              
     try{ 
         //Set connection properties required to invoke AEM Forms                                 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
         //Create a ServiceClientFactory object 
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
         //Create a FormsServiceClient object 
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
         //Set parameter values required by the renderPDFForm method 
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";  
         byte[]    cData = "".getBytes(); 
         Document oInputData = new Document(cData); 
                  
         //Set a run-time option required to render a form on the client 
         PDFFormRenderSpec pdfRenderSpec = new PDFFormRenderSpec();  
         pdfRenderSpec.setRenderAtClient(RenderAtClient.Yes); 
                  
         //Specify URI values required to render a form 
         URLSpec uriValues = new URLSpec();  
         uriValues.setApplicationWebRoot("https://[server]:[port]/FormsServiceClientApp"); 
         uriValues.setContentRootURI("repository:///"); 
         uriValues.setTargetURL("https://[server]:[port]/FormsServiceClientApp/HandleData"); 
          
         //Invoke the renderPDFForm method to render  
         //an interactive PDF form on the client 
         FormsResult formOut = formsClient.renderPDFForm( 
                 formName,            
                 oInputData,          
                 pdfRenderSpec,       
                 uriValues,             
                 null                 
             ); 
          
         //Create a Document object that stores form data 
         Document myData = formOut.getOutputContent(); 
          
         //Get the content type of the response and 
         //set the HttpServletResponse objects content type 
         String contentType = myData.getContentType();  
         resp.setContentType(contentType); 
          
         //Create a ServletOutputStream object 
         ServletOutputStream oOutput = resp.getOutputStream(); 
          
         //Create an InputStream object 
         InputStream inputStream = myData.getInputStream(); 
          
         //Write the data stream to the web browser 
         byte[] data = new byte[4096]; 
         int bytesRead = 0; 
         while ((bytesRead = inputStream.read(data)) > 0) 
         { 
             oOutput.write(data, 0, bytesRead); 
         } 
          
         }catch (Exception e) { 
              System.out.println("The following exception occurred: "+e.getMessage()); 
          } 
     } 
 } 
 
```

## クイックスタート（SOAP モード）:Java API を使用したガイドのレンダリング（非推奨） {#quick-start-soap-mode-rendering-a-guide-deprecated-using-the-java-api}

次のコード例では、という名前のガイド（非推奨）をレンダリングしています。 *TLALifeClaim.xdp* クライアントの Web ブラウザーにコピーします。

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
    * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.IOException; 
 import java.io.InputStream; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
 import java.util.*; 
  
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RenderFormGuide extends HttpServlet implements Servlet { 
  
      
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
             doPost(req,resp);  
     } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
     try{ 
              
         //Set connection properties required to invoke AEM Forms                                 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
         //Create a ServiceClientFactory object 
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
         //Specify the parameters for the renderActivityGuide method 
         String formName = "Applications/FormsApplication/1.0/FormsFolder/TLALifeClaim.xdp";  
         byte[] cData = "".getBytes(); 
         Document oInputData = new Document(cData); 
                  
         //Cache the PDF form 
         PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec(); 
         pdfFormRenderSpec.setCacheEnabled(new Boolean(true)); 
  
         //Set Form Guide run-time options 
         ActivityGuideRenderSpec renderSpec = new ActivityGuideRenderSpec();  
         renderSpec.setGuidePDF(false); 
          
         //Specify URI values that are required to render a form 
         //design located in the AEM Forms repository 
         URLSpec uriValues = new URLSpec();  
         uriValues.setApplicationWebRoot("https://[server]:[port]/FormsQS"); 
         uriValues.setContentRootURI("repository:///"); 
         uriValues.setTargetURL("https://[server]:[port]/FormsQS/HandleData"); 
          
  
         //Invoke the renderFormGuide method 
         FormsResult formOut = formsClient.renderFormGuide( 
                 formName,            //formQuery 
                 oInputData,          //inDataDoc  
                 pdfFormRenderSpec,    //pdfFormRenderSpec 
                 renderSpec,           //activityGuideRenderSpec 
                 uriValues              //urlSpec 
                 );   
          
         //Create a Document object that stores form data 
         Document myData = formOut.getOutputContent(); 
          
         //Get the content type of the response 
         String contentType = myData.getContentType();  
         resp.setContentType(contentType); 
          
         //Create a ServletOutputStream object 
         ServletOutputStream oOutput = resp.getOutputStream(); 
          
         //Create an InputStream object 
         InputStream inputStream = myData.getInputStream(); 
          
         //Write the data stream to the web browser 
         byte[] data = new byte[4096]; 
         int bytesRead = 0; 
         while ((bytesRead = inputStream.read(data)) > 0) 
         { 
             oOutput.write(data, 0, bytesRead); 
         } 
  
     }catch (Exception e) { 
              System.out.println("The following exception occured: "+e.getMessage()); 
               } 
      } 
 } 
 
```

## クイックスタート（SOAP モード）:Java API を使用したフラグメントに基づくフォームのレンダリング {#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api}

次のコード例では、フラグメントに基づくフォームをレンダリングします。 フォームデザインの名前は次のようになります。 *PurchaseOrderDynamic.xdp* このファイルはAEM Formsリポジトリに格納されます（XDP ファイルはリポジトリ内の FormsFolder という名前のフォルダーに格納されます）。 また、POFragment フォームが参照するフラグメントもリポジトリ内に配置する必要があります。 ( [フラグメントに基づくFormsのレンダリング](/help/forms/developing/rendering-forms.md#rendering-forms-based-on-fragments).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
     * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.FileInputStream; 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
 import java.util.*; 
 import java.io.InputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RenderFormFragments extends HttpServlet implements Servlet { 
      
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
             doPost(req,resp);  
  
     } 
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
     throws ServletException, IOException { 
              
         try{ 
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
             //Create a FormsServiceClient object 
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
             //Set the parameter values for the renderPDFForm method 
             String formName = "Applications/FormsApplication/1.0/FormsFolder/PurchaseOrderDynamic.xdp";   
              
             FileInputStream myFormData = new FileInputStream("C:\\Adobe\Purchase Order US.xml"); 
             Document oInputData = new Document(myFormData); 
                                      
             //Cache the PDF form 
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec(); 
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true)); 
          
             //Specify URI values that are required to render a form 
             //design based on fragments 
             URLSpec uriValues = new URLSpec();  
             uriValues.setApplicationWebRoot("https://[server]:[port]/FormsServiceClientApp"); 
             uriValues.setContentRootURI("repository:///"); 
             uriValues.setTargetURL("https://[server]:[port]/FormsServiceClientApp/HandleData"); 
                      
             //Invoke the renderPDFForm method and write the  
             //results to a client web browser 
             FormsResult formOut = formsClient.renderPDFForm( 
                         formName,               //formQuery 
                         oInputData,             //inDataDoc 
                         pdfFormRenderSpec,      //PDFFormRenderSpec 
                         uriValues,                //urlSpec 
                         null                    //attachments 
                         ); 
          
             //Create a Document object that stores form data 
             Document myData = formOut.getOutputContent(); 
          
             //Get the content type of the response and 
             //set the HttpServletResponse object’s content type 
             String contentType = myData.getContentType();  
             resp.setContentType(contentType); 
          
             //Create a ServletOutputStream object 
             ServletOutputStream oOutput = resp.getOutputStream(); 
          
             //Create an InputStream object 
             InputStream inputStream = myData.getInputStream(); 
          
             //Write the data stream to the web browser 
             byte[] data = new byte[4096]; 
             int bytesRead = 0; 
             while ((bytesRead = inputStream.read(data)) > 0) 
             { 
                 oOutput.write(data, 0, bytesRead); 
             } 
         }catch (Exception e) { 
              System.out.println("The following exception occurred: "+e.getMessage()); 
       } 
     } 
 }
```

## クイックスタート（SOAP モード）:Java API を使用した権限が有効なフォームのレンダリング {#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api}

次のコードの例では、権限が有効なフォームをクライアントの Web ブラウザーにレンダリングします。 このコードの例で設定された使用権限により、ユーザーはフォームにコメントを追加し、フォームデータを保存できます。 ( [レンダリング権限が有効なForms](/help/forms/developing/rendering-forms.md#rendering-rights-enabled-forms).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
    * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
 import java.util.*; 
 import java.io.InputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
  
 public class RenderUsageRightsForms extends HttpServlet implements Servlet { 
  
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
             doPost(req,resp); 
     } 
  
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
              
     try{ 
         //Set connection properties required to invoke AEM Forms                                 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
         //Create a FormsServiceClient object 
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
         //Set parameter values for the renderPDFFormWithUsageRights method 
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";  
         byte[]    cData = "".getBytes(); 
         Document oInputData = new Document(cData); 
          
         //Set run-time options 
         PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec(); 
         pdfFormRenderSpec.setCacheEnabled(new Boolean(true)); 
          
         //Set usage-rights run-time options 
         ReaderExtensionSpec reOptions = new ReaderExtensionSpec(); 
         reOptions.setReCredentialAlias("RE2"); 
         reOptions.setReCommenting(true); 
         reOptions.setReFillIn(true); 
          
         //Specify URI values required to render the form 
         URLSpec uriValues = new URLSpec();  
         uriValues.setApplicationWebRoot("https://[server]:[port]/FormsQS"); 
         uriValues.setContentRootURI("repository:///"); 
         uriValues.setTargetURL("https://[server]:[port]/FormsQS/HandleData"); 
          
         //Render a rights-enabled PDF form 
         FormsResult formOut = formsClient.renderPDFFormWithUsageRights( 
             formName,            //formQuery 
             oInputData,          //inDataDoc  
             pdfFormRenderSpec,   //renderFormOptionsSpec 
             reOptions,              //applicationWebRoot 
             uriValues            //targetURL 
             ); 
          
         //Create a Document object that stores form data 
         Document myData = formOut.getOutputContent(); 
          
         //Get the content type of the response and 
         //set the HttpServletResponse objects content type 
         String contentType = myData.getContentType();  
         resp.setContentType(contentType); 
          
         //Create a ServletOutputStream object 
         ServletOutputStream oOutput = resp.getOutputStream(); 
          
         //Create an InputStream object 
         InputStream inputStream = myData.getInputStream(); 
          
         //Write the data stream to the web browser 
         byte[] data = new byte[4096]; 
         int bytesRead = 0; 
         while ((bytesRead = inputStream.read(data)) > 0) 
         { 
             oOutput.write(data, 0, bytesRead); 
         } 
          
     }catch (Exception e) { 
          System.out.println("The following exception occurred: "+e.getMessage()); 
       } 
     } 
 } 
  
 
```

## クイックスタート（SOAP モード）:Java API を使用したHTMLフォームのレンダリング {#quick-start-soap-mode-rendering-an-html-form-using-the-java-api}

次のコードの例では、Formsサービス Java API を使用してHTMLフォームをレンダリングします。 ツールバーがHTMLフォームに追加され、2 つの添付ファイルが追加されます。 さらに、ユーザーエージェントの値は `HttpServletRequest` オブジェクト。 ( [FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms.md#rendering-forms-as-html).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
    * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
  
 import java.util.*; 
 import java.io.InputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import java.io.FileInputStream; 
  
  
 public class RenderHTMLForms extends HttpServlet implements Servlet { 
      
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
             doPost(req,resp);  
     } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
              
             try{ 
              
                 //Set connection properties required to invoke AEM Forms     
                 Properties connectionProps = new Properties(); 
                 connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://[server]:[port]"); 
                 connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");           
                 connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss"); 
                 connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator"); 
                 connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password"); 
              
                 //Create a FormsServiceClient object 
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
                 //Set parameter values for the (Deprecated) renderHTMLForm method 
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";   
                 byte[]    cData = "".getBytes(); 
                 Document oInputData = new Document(cData); 
                  
                 //Obtain the user agent value from the HttpServletRequest object 
                 String userAgent = req.getHeader("user-agent"); 
                                      
                 //Create an HTMLRenderSpec object to store HTML run-time options 
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec(); 
                 htmlRS.setHTMLToolbar(HTMLToolbar.Vertical); 
                                                          
                 //Specify the locale value 
                 htmlRS.setLocale("en_US"); 
                          
                 //Render the HTML form within full HTML tags 
                 htmlRS.setOutputType(OutputType.FullHTMLTags); 
                  
                 //Set style information that controls the presentation of the HTML form 
                 htmlRS.setStyleGenerationLevel(StyleGenerationLevel.InlineAndInternalStyles); 
                                                                  
                 //Specify URI values that are required to render a form 
                 URLSpec uriValues = new URLSpec();  
                 uriValues.setApplicationWebRoot("https://[server]:[port]/FormsQS"); 
                 uriValues.setContentRootURI("repository:///"); 
                 uriValues.setTargetURL("https://[server]:[port]/FormsQS/HandleSubmittedHTMLForm"); 
                                  
                 //Specify file attachments 
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");  
                 Document attachment1 = new Document(myForm); 
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");  
                 Document attachment2 = new Document(myForm2); 
                 String fileName = "Attach1.txt"; 
                 String fileName2 = "Attach2.txt"; 
                      
                 Map fileAttachments = new HashMap(); 
                 fileAttachments.put(fileName, attachment1);  
                 fileAttachments.put(fileName2, attachment2);  
                          
                 //Invoke the (Deprecated) renderHTMLForm method 
                 FormsResult formOut = formsClient.renderHTMLForm( 
                     formName,               //formQuery 
                     TransformTo.MSDHTML,    //transformTo 
                     oInputData,             //inDataDoc 
                     htmlRS,                    //renderHTMLSpec 
                     userAgent,                //User Agent 
                     uriValues,                //urlSpec 
                     fileAttachments            //attachments 
                     ); 
          
                 //Create a Document object that stores form data 
                 Document myData = formOut.getOutputContent(); 
          
                 //Get the content type of the response and 
                 //set the HttpServletResponse object’s content type 
                 String contentType = myData.getContentType();  
                 resp.setContentType(contentType); 
          
                 //Create a ServletOutputStream object 
                 ServletOutputStream oOutput = resp.getOutputStream(); 
          
                 //Create an InputStream object 
                 InputStream inputStream = myData.getInputStream(); 
          
                 //Write the data stream to the web browser 
                 byte[] data = new byte[4096]; 
                 int bytesRead = 0; 
                 while ((bytesRead = inputStream.read(data)) > 0) 
                 { 
                     oOutput.write(data, 0, bytesRead); 
                 } 
          
                 }catch (Exception e) { 
                      System.out.println("The following exception occurred: "+e.getMessage()); 
                      } 
             } 
 } 
  
  
  
 
```

## クイックスタート（SOAP モード）:Java API を使用した CSS ファイルを使用するHTMLフォームのレンダリング {#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api}

次のコードの例では、Formsサービスクライアント API を使用してHTMLフォームをレンダリングします。 参照されるカスタム CSS ファイルの名前は次のとおりです。 *custom.css*. ( [カスタム CSS ファイルを使用したHTMLFormsのレンダリング](/help/forms/developing/rendering-forms.md#rendering-html-forms-using-custom-css-files).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
     * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
  
 import java.util.*; 
 import java.io.InputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 import java.io.FileInputStream; 
  
  
 public class RenderHTMLCSS extends HttpServlet implements Servlet { 
      
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
             doPost(req,resp);  
     } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
              
             try{ 
                 //Set connection properties required to invoke AEM Forms                                 
                 Properties connectionProps = new Properties(); 
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
                 //Create a FormsServiceClient object 
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
                 //Set parameter values for the (Deprecated) renderHTMLForm method 
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";  
                 byte[]    cData = "".getBytes(); 
                 Document oInputData = new Document(cData); 
                 String userAgent = "" ; 
                                      
                 //Create an HTMLRenderSpec object to store HTML run-time options 
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec(); 
                                                                          
                 //Specify the locale value 
                 htmlRS.setLocale("en_US"); 
                  
                 //Specify a custom CSS file to use 
                 htmlRS.setCustomCSSURI("C:\\Adobe\custom.css"); 
                  
                 //Render the HTML form within full HTML tags 
                 htmlRS.setOutputType(OutputType.FullHTMLTags); 
                                                                  
                 //Specify URI values that are required to render a form 
                 URLSpec uriValues = new URLSpec();  
                 uriValues.setApplicationWebRoot("https://[server]:[port]/FormsQS"); 
                 uriValues.setContentRootURI("repository:///"); 
                 uriValues.setTargetURL("https://[server]:[port]/FormsQS/HandleData"); 
                                  
                 //Specify file attachments 
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");  
                 Document attachment1 = new Document(myForm); 
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");  
                 Document attachment2 = new Document(myForm2); 
                 String fileName = "Attach1.txt"; 
                 String fileName2 = "Attach2.txt"; 
                      
                 Map fileAttachments = new HashMap(); 
                 fileAttachments.put(fileName, attachment1);  
                 fileAttachments.put(fileName2, attachment2);  
                          
                 //Invoke the (Deprecated) renderHTMLForm method 
                 FormsResult formOut = formsClient.renderHTMLForm( 
                     formName,               //formQuery 
                     TransformTo.MSDHTML,    //transformTo 
                     oInputData,             //inDataDoc 
                     htmlRS,                    //renderHTMLSpec 
                     userAgent,                //User Agent 
                     uriValues,                //urlSpec 
                     fileAttachments            //attachments 
                     ); 
          
                 //Create a Document object that stores form data 
                 Document myData = formOut.getOutputContent(); 
          
                 //Get the content type of the response and 
                 //set the HttpServletResponse object’s content type 
                 String contentType = myData.getContentType();  
                 resp.setContentType(contentType); 
          
                 //Create a ServletOutputStream object 
                 ServletOutputStream oOutput = resp.getOutputStream(); 
          
                 //Create an InputStream object 
                 InputStream inputStream = myData.getInputStream(); 
          
                 //Write the data stream to the web browser 
                 byte[] data = new byte[4096]; 
                 int bytesRead = 0; 
                 while ((bytesRead = inputStream.read(data)) > 0) 
                 { 
                     oOutput.write(data, 0, bytesRead); 
                 } 
          
             }catch (Exception e) { 
                      System.out.println("The following exception occurred: "+e.getMessage()); 
              } 
     } 
 }
```

## クイックスタート（SOAP モード）:Java API を使用した、カスタムHTMLでのツールバーでのツールバーフォームのレンダリング {#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api}

次のコードの例では、フランス語で表示されるHTMLを含むツールバーフォームをレンダリングします。 fscmenu.xml の場所はC:\Adobe です ( このフォルダーはAEM Formsをホストするサーバー上に存在する必要があります )。 ロケールの値が `fr_FR`. カスタムツールバーを使用してHTMLフォームをレンダリングする方法を説明する節では、このクイックスタートで使用する fscmenu.xml ファイルの構文を示します。 ( [HTMLFormsとカスタムツールバーのレンダリング](/help/forms/developing/rendering-forms.md#rendering-html-forms-with-custom-toolbars).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
    * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
  
 import java.util.*; 
 import java.io.InputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import java.io.FileInputStream; 
  
  
 public class RenderCustomToolbar extends HttpServlet implements Servlet { 
      
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
             doPost(req,resp);  
     } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
              
             try{ 
                 //Set connection properties required to invoke AEM Forms     
                 Properties connectionProps = new Properties(); 
                 connectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://[server]:[port]"); 
                 connectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");           
                 connectionProps.setProperty("DSC_SERVER_TYPE", "JBoss"); 
                 connectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator"); 
                 connectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password"); 
              
                 //Create a FormsServiceClient object 
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                 FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
                 //Set parameter values for the renderHTMLForm method 
                 String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";   
                 byte[]    cData = "".getBytes(); 
                 Document oInputData = new Document(cData); 
                 String userAgent = "" ; 
                                      
                 //Create an HTMLRenderSpec object to store HTML run-time options 
                 HTMLRenderSpec htmlRS = new HTMLRenderSpec(); 
                 htmlRS.setHTMLToolbar(HTMLToolbar.Vertical); 
                                                          
                 //Specify the URI location of the  
                 // fscmenu.xml file that contains French 
                 htmlRS.setToolbarURI("C:\\Adobe"); 
                  
                 //Specify the locale value 
                 htmlRS.setLocale("fr_FR"); 
                                  
                 //Render the HTML form within full HTML tags 
                 htmlRS.setOutputType(OutputType.FullHTMLTags); 
                                                                  
                 //Specify URI values that are required to render a form 
                 URLSpec uriValues = new URLSpec();  
                 uriValues.setApplicationWebRoot("https://[server]:[port]/FormsQS"); 
                 uriValues.setContentRootURI("repository:///"); 
                 uriValues.setTargetURL("https://[server]:[port]/FormsQS/HandleData"); 
                                  
                 //Specify file attachments 
                 FileInputStream myForm = new FileInputStream("C:\\Attach1.txt");  
                 Document attachment1 = new Document(myForm); 
                 FileInputStream myForm2 = new FileInputStream("C:\\Attach2.txt");  
                 Document attachment2 = new Document(myForm2); 
                 String fileName = "Attach1.txt"; 
                 String fileName2 = "Attach2.txt"; 
                      
                 Map fileAttachments = new HashMap(); 
                 fileAttachments.put(fileName, attachment1);  
                 fileAttachments.put(fileName2, attachment2);  
                          
                 //Invoke the renderHTMLForm method 
                 FormsResult formOut = formsClient.renderHTMLForm( 
                     formName,               //formQuery 
                     TransformTo.MSDHTML,    //transformTo 
                     oInputData,             //inDataDoc 
                     htmlRS,                    //renderHTMLSpec 
                     userAgent,                //User Agent 
                     uriValues,                //urlSpec 
                     fileAttachments            //attachments 
                     ); 
          
                 //Create a Document object that stores form data 
                 Document myData = formOut.getOutputContent(); 
          
                 //Get the content type of the response and 
                 //set the HttpServletResponse object’s content type 
                 String contentType = myData.getContentType();  
                 resp.setContentType(contentType); 
          
                 //Create a ServletOutputStream object 
                 ServletOutputStream oOutput = resp.getOutputStream(); 
          
                 //Create an InputStream object 
                 InputStream inputStream = myData.getInputStream(); 
          
                 //Write the data stream to the web browser 
                 byte[] data = new byte[4096]; 
                 int bytesRead = 0; 
                 while ((bytesRead = inputStream.read(data)) > 0) 
                 { 
                     oOutput.write(data, 0, bytesRead); 
                 } 
          
                 }catch (Exception e) { 
                      System.out.println("The following exception occurred: "+e.getMessage()); 
                      } 
             } 
 } 
 
```

## クイックスタート（SOAP モード）:Java API を使用して、XML として送信されたPDF formsの処理 {#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api}

次のコードの例では、XML として送信されるフォームを処理します。 に渡されるコンテンツタイプ値 `processFormSubmission` メソッド `CONTENT_TYPE=text/xml`. 次の名前のフィールドに対応する値： `mortgageAmount`, `lastName`、および `firstName` が表示されます。 という名前のユーザー定義メソッド `getNodeText` このクイックスタートではが使用されます。 これは、 `org.w3c.dom.Document` インスタンスと、ノード名を指定する string 値。 このメソッドは、ノードの値を表す string 値を返します。 ( [送信済みFormsの処理](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 9. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
    * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
 import java.util.*; 
 import java.io.DataInputStream; 
 import java.io.File; 
 import java.io.InputStream; 
 import java.io.PrintWriter; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 //Import DOM libraries 
 import org.w3c.dom.NodeList; 
 import org.w3c.dom.Node; 
 import javax.xml.parsers.*; 
  
 public class HandleData extends HttpServlet implements Servlet { 
  
      
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
                 doPost(req,resp); 
         } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
              
         try{ 
             PrintWriter pp = resp.getWriter();      
              
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
             //Create a FormsServiceClient object 
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
             //Get Form data to pass to the processFormSubmission method 
             Document formData = new Document(req.getInputStream());  
                          
             //Set run-time options 
              RenderOptionsSpec processSpec = new RenderOptionsSpec();  
              processSpec.setLocale("en_US"); 
              
             //Invoke the processFormSubmission method 
             FormsResult formOut = formsClient.processFormSubmission(formData, 
             "CONTENT_TYPE=text/xml", 
             "", 
             processSpec); 
              
             //Get the processing state 
             short processState = formOut.getAction(); 
                          
             //Determine if the form data is ready to be processed 
             //This code example checks only for submitted data (value is 0) 
             if (processState == 0)  
             { 
               //Determine the content type of the data 
               String myContentType = formOut.getContentType(); 
               System.out.println("THE CONTENT TYPS IS" +myContentType); 
              
                if (myContentType.equals("application/vnd.adobe.xdp+xml"))    { 
              
                 //Get the form data 
                 Document formOutput = formOut.getOutputContent();  
                 InputStream formInputStream = new DataInputStream(formOutput.getInputStream());  
                  
                 //Create DocumentBuilderFactory and DocumentBuilder objects 
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance(); 
                 DocumentBuilder builder = factory.newDocumentBuilder(); 
                 org.w3c.dom.Document myDOM = builder.parse(formInputStream); 
                                          
                 //Call for each field in the form 
                 String Amount = getNodeText("mortgageAmount", myDOM); 
                 String myLastName =  getNodeText("lastName", myDOM);  
                 String myFirstName = getNodeText("firstName", myDOM); 
                  
                 //Write the form data to the web browser 
                 pp.println("<p> The form data is :<br><br>" + 
                         "<li> The mortgage amount is "+ Amount+"" + 
                         "<li> Last name is "+ myLastName+"" + 
                         "<li> First name is "+ myFirstName+"")    ; 
                  
                          
                 } 
              } 
             } 
         catch (Exception e) { 
              e.printStackTrace(); 
           } 
     } 
          
     //This method returns the value of the specified node 
     private String getNodeText(String nodeName, org.w3c.dom.Document myDOM) 
     { 
       //Get the XML node by name 
       NodeList oList = myDOM.getElementsByTagName(nodeName); 
       Node myNode = oList.item(0);  
       NodeList oChildNodes = myNode.getChildNodes(); 
                                   
      String sText = ""; 
      for (int i = 0; i < oChildNodes.getLength(); i++) 
      { 
          Node oItem = oChildNodes.item(i); 
         if (oItem.getNodeType() == Node.TEXT_NODE) 
          { 
            sText = sText.concat(oItem.getNodeValue()); 
          } 
      } 
     return sText; 
     } 
 } 
 
```

>[!NOTE]
>
>を使用する場合 `com.adobe.idp.Document` オブジェクトと `org.w3c.dom.Document` 同じアプリケーションで、 `org.w3c.dom.Document`.

## クイックスタート（SOAP モード）:Java API を使用して、PDFとして送信されたPDF formsの処理 {#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api}

次のコードの例では、送信データとして送信されたフォームをPDFします。 に渡されるコンテンツタイプ値 `processFormSubmission` メソッド `CONTENT_TYPE=application/pdf`. 送信されたフォームは、次の名前のPDFファイルとして保存されます： *tempPDF.pdf*. また、フォームはPDFとして送信されるので、添付ファイルを取得できます。 添付ファイルはすべてJPEGファイルとして保存されます。 ( [送信済みFormsの処理](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
    * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
 import java.util.*; 
 import java.io.DataInputStream; 
 import java.io.File; 
 import java.io.InputStream; 
 import java.io.PrintWriter; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 //Import DOM libraries 
 import org.w3c.dom.NodeList; 
 import org.w3c.dom.Node; 
 import javax.xml.parsers.*; 
  
 public class HandleSubmittedPDFData extends HttpServlet implements Servlet { 
  
      
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
                 doPost(req,resp); 
         } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
              
         try{ 
             PrintWriter pp = resp.getWriter();      
              
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
             //Create a FormsServiceClient object 
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
             //Get Form data to pass to the processFormSubmission method 
             Document formData = new Document(req.getInputStream());  
                          
             //Set run-time options 
              RenderOptionsSpec processSpec = new RenderOptionsSpec();  
              processSpec.setLocale("en_US"); 
              
             //Invoke the processFormSubmission method 
             FormsResult formOut = formsClient.processFormSubmission(formData, 
             "CONTENT_TYPE=application/pdf", 
             "", 
             processSpec); 
              
             //Determine if the form contains file attachments 
             //It is assumed that file attachments are JPG files 
             List fileAttachments = formOut.getAttachments();  
                                  
             //Create an Iterator object and iterate through  
             //the List object 
             Iterator iter = fileAttachments.iterator();  
             int i = 0 ;  
             while (iter.hasNext()) {  
                 Document file = (Document)iter.next();  
                 file.copyToFile(new File("C:\\Adobe\tempFile"+i+".jpg")); 
                 i++;  
             } 
              
             //Get the processing state 
             short processState = formOut.getAction(); 
                          
             //Determine if the form data is ready to be processed 
             //This code example checks only for submitted data (value is 0) 
             if (processState == 0)  
             { 
               //Determine the content type of the data 
               String myContentType = formOut.getContentType(); 
              
               if (myContentType.equals("application/pdf")){ 
                      
                     //Get the form data 
                     Document myPDFfile = formOut.getOutputContent();  
                                      
                     //Create a PDF object 
                     File myPDFFile = new File("C:\\Adobe\tempPDF.pdf"); 
                      
                     //Populate the PDF file 
                     myPDFfile.copyToFile(myPDFFile);                     
                     pp.println("<p> The PDF file is saved as C:\\Adobe\tempPDF.pdf") ;  
                      
                 } 
               } 
         } 
         catch (Exception e) { 
              e.printStackTrace(); 
           } 
     } 
  
 } 
  
  
 
```

## クイックスタート（SOAP モード）:Java API を使用して、XML として送信されたHTMLフォームの処理 {#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api}

次のコードの例では、XML データとして送信されるHTMLフォームを処理します。 に渡されるコンテンツタイプ値 `processFormSubmission` メソッド `CONTENT_TYPE=application/x-www-form-urlencoded`. `mortgageAmount`, `lastName`、および `firstName` が表示されます。 という名前のユーザー定義メソッド `getNodeText` このクイックスタートではが使用されます。 これは、 `org.w3c.dom.Document` インスタンスと、ノード名を指定する string 値。 このメソッドは、ノードの値を表す string 値を返します。 ( [送信済みFormsの処理](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
    * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
 import java.util.*; 
 import java.io.DataInputStream; 
 import java.io.File; 
 import java.io.InputStream; 
 import java.io.PrintWriter; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 //Import DOM libraries 
 import org.w3c.dom.NodeList; 
 import org.w3c.dom.Node; 
 import javax.xml.parsers.*; 
  
 /* 
     * This quick start handles data submitted as XML from a rendered HTML form  
     */ 
 public class HandleSubmittedHTMLForm extends HttpServlet implements Servlet { 
  
      
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
                 doPost(req,resp); 
         } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
              
         try{ 
             PrintWriter pp = resp.getWriter();      
              
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
             //Create a FormsServiceClient object 
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
             //Get Form data to pass to the processFormSubmission method 
             Document formData = new Document(req.getInputStream());  
                          
             //Set run-time options 
              RenderOptionsSpec processSpec = new RenderOptionsSpec();  
              processSpec.setLocale("en_US"); 
              
             //Invoke the processFormSubmission method 
             FormsResult formOut = formsClient.processFormSubmission(formData, 
             "CONTENT_TYPE=application/x-www-form-urlencoded", 
             "", 
             processSpec); 
              
             //Get the processing state 
             short processState = formOut.getAction(); 
                          
             //Determine if the form data is ready to be processed 
             //This code example checks only for submitted data (value is 0) 
             if (processState == 0)  
             { 
              
                     //Get the form data 
                     Document formOutput = formOut.getOutputContent();  
                     InputStream formInputStream = new DataInputStream(formOutput.getInputStream());  
                                                      
                     //Create DocumentBuilderFactory and DocumentBuilder objects 
                     DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance(); 
                     DocumentBuilder builder = factory.newDocumentBuilder(); 
                     org.w3c.dom.Document myDOM = builder.parse(formInputStream); 
                                              
                     //Call for each field in the form 
                     String Amount = getNodeText("mortgageAmount", myDOM); 
                     String myLastName =  getNodeText("lastName", myDOM);  
                     String myFirstName = getNodeText("firstName", myDOM); 
                      
                     //Write the form data to the web browser 
                     pp.println("<p> The form data is :<br><br>" + 
                             "<li> The mortgage amount is "+ Amount+"" + 
                             "<li> Last name is "+ myLastName+"" + 
                             "<li> First name is "+ myFirstName+"")    ; 
                      } 
                 } 
             catch (Exception e) { 
                  e.printStackTrace(); 
               } 
         } 
              
         //This method returns the value of the specified node 
         private String getNodeText(String nodeName, org.w3c.dom.Document myDOM) 
         { 
           //Get the XML node by name 
           NodeList oList = myDOM.getElementsByTagName(nodeName); 
           Node myNode = oList.item(0);  
           NodeList oChildNodes = myNode.getChildNodes(); 
                                       
          String sText = ""; 
          for (int i = 0; i < oChildNodes.getLength(); i++) 
          { 
              Node oItem = oChildNodes.item(i); 
             if (oItem.getNodeType() == Node.TEXT_NODE) 
              { 
                sText = sText.concat(oItem.getNodeValue()); 
              } 
          } 
         return sText; 
         } 
     } 
 
```

## クイックスタート（SOAP モード）:Java API を使用した、送信済み XML データを使用したPDFドキュメントの作成 {#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api}

次の Java コードの例では、XML として送信されたフォームデータを処理します。 フォームデータは、Forms API を使用してフォーム送信から取得され、Output サービスに送信されます。 フォームデータとフォームデザインは、非インタラクティブフォームドキュメントの作成にPDFされます。 非インタラクティブPDFドキュメントは、 `/Company Home/Test Directory`. フォームの名前が動的に作成されます。 つまり、ユーザーの姓と名が、ユーザーファイルの名前に使用されます。 新しいコンテンツのリソース識別子が、クライアント Web ブラウザーに書き出されます。 ( [送信済み XMLPDFでのデータ・ドキュメントの作成](/help/forms/developing/rendering-forms.md#creating-pdf-documents-with-submitted-xml-data).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
     * 20. adobe-output-client.jar 
     * 21. adobe-contentservices-client.jar 
     * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
  
 import com.adobe.livecycle.contentservices.client.CRCResult; 
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl; 
 import com.adobe.livecycle.contentservices.client.impl.UpdateVersionType; 
 import com.adobe.livecycle.formsservice.client.*; 
 import com.adobe.livecycle.output.client.OutputClient; 
 import com.adobe.livecycle.output.client.OutputResult; 
 import com.adobe.livecycle.output.client.PDFOutputOptionsSpec; 
 import com.adobe.livecycle.output.client.TransformationFormat; 
  
 import java.util.*; 
 import java.io.DataInputStream; 
 import java.io.File; 
 import java.io.InputStream; 
 import java.io.PrintWriter; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.InvocationRequest; 
 import com.adobe.idp.dsc.InvocationResponse; 
 import com.adobe.idp.dsc.clientsdk.ServiceClient; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 //Import DOM libraries 
 import org.w3c.dom.NodeList; 
 import org.w3c.dom.Node; 
 import javax.xml.parsers.*; 
  
 public class HandleDataSendToOutput extends HttpServlet implements Servlet { 
  
      
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
                 doPost(req,resp); 
         } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
              
         try{ 
             PrintWriter pp = resp.getWriter();      
              
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
             //Create a FormsServiceClient object 
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
             //Get Form data to pass to the processFormSubmission method 
             Document formData = new Document(req.getInputStream());  
                          
             //Set run-time options 
              RenderOptionsSpec processSpec = new RenderOptionsSpec();  
              processSpec.setLocale("en_US"); 
              
             //Invoke the processFormSubmission method 
             FormsResult formOut = formsClient.processFormSubmission(formData, 
             "CONTENT_TYPE=text/xml", 
             "", 
             processSpec); 
              
             //Get the processing state 
             short processState = formOut.getAction(); 
                          
             //Determine if the form data is ready to be processed 
             //This code example checks only for submitted data (value is 0) 
             if (processState == 0)  
             { 
               //Determine the content type of the data 
               String myContentType = formOut.getContentType(); 
              
               if (myContentType.equals("application/vnd.adobe.xdp+xml"))    { 
              
                 //Get the form data 
                 Document formOutput = formOut.getOutputContent();  
                 InputStream formInputStream = new DataInputStream(formOutput.getInputStream());  
                  
                 //Create DocumentBuilderFactory and DocumentBuilder objects 
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance(); 
                 DocumentBuilder builder = factory.newDocumentBuilder(); 
                 org.w3c.dom.Document myDOM = builder.parse(formInputStream); 
                                          
                 //Call for each field in the form 
                 String Amount = getNodeText("mortgageAmount", myDOM); 
                 String myLastName =  getNodeText("lastName", myDOM);  
                 String myFirstName = getNodeText("firstName", myDOM); 
                  
                 //Write the form data to the web browser 
                 pp.println("<p> The form data is :<br><br>" + 
                         "<li> The mortgage amount is "+ Amount+"" + 
                         "<li> Last name is "+ myLastName+"" + 
                         "<li> First name is "+ myFirstName+"")    ; 
                  
                  
                 //Create a non-interactive PDF document by invoking the Output service 
                 Document myPDFform = GeneratePDFDocument(myFactory, formOutput); 
                  
                 //Create the name of the PDF file to store 
                 String pdfName = "Loan_"+myLastName+"_"+myFirstName+".pdf" ; 
                 String userName = myFirstName+" "+myLastName ;  
                  
                 //Store the PDF form into Content Services (deprecated) 
                 String resourceID = StorePDFDocument(myFactory, myPDFform, pdfName,userName); 
                 pp.println("<p> The pdf document was store in :<br><br>" + 
                         "<li> /Company home "+ 
                         "<li> The identifier value of the new resource is "+ resourceID+""); 
                   } 
             } 
         } 
         catch (Exception e) { 
              e.printStackTrace(); 
           } 
     } 
          
      
     //Store the PDF document in /Company Home/Test Directory using the  
     //AEM Forms Content Service API 
     private String StorePDFDocument(ServiceClientFactory myFactory, com.adobe.idp.Document pdfDoc, String formName, String userName) 
     { 
         try 
         { 
             //Create a DocumentManagementServiceClientImpl object 
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory); 
              
             //Specify the store and node name 
             String storeName ="SpacesStore";  
             String nodeName = "/Company Home/Test Directory"; 
              
             //Create a MAP instance to store attributes 
             Map<String,Object> inputs = new HashMap<String,Object>(); 
              
             //Specify attributes that belong to the new content 
             String creator = "{https://www.alfresco.org/model/content/1.0}creator"; 
             String description = "{https://www.alfresco.org/model/content/1.0}description";  
              
             inputs.put(creator,userName); 
             inputs.put(description,"A mortgage application form"); 
                                  
             //Store MortgageForm.pdf in /Company Home/Test Directory 
             CRCResult result = docManager.storeContent(storeName,  
                      nodeName, 
                      formName, 
                     "{https://www.alfresco.org/model/content/1.0}content",  
                     pdfDoc, 
                     "UTF-8", 
                     UpdateVersionType.INCREMENT_MAJOR_VERSION, 
                     null, 
                     inputs);  
             //Get the identifier value of the new resource 
             String id = result.getNodeUuid(); 
             return id;  
     } 
         catch (Exception ee) 
         { 
             ee.printStackTrace(); 
         } 
         return null ;  
     } 
      
      
     //This method returns the value of the specified node 
     private com.adobe.idp.Document GeneratePDFDocument(ServiceClientFactory myFactory, com.adobe.idp.Document formData) 
     { 
         try 
         { 
         //Create an OutputClient object 
         OutputClient outClient = new OutputClient(myFactory);  
              
         //Set PDF run-time options     
         com.adobe.livecycle.output.client.PDFOutputOptionsSpec outputOptions = new PDFOutputOptionsSpec(); 
         outputOptions.setLocale("en_US"); 
              
         //Set rendering run-time options 
         com.adobe.livecycle.output.client.RenderOptionsSpec pdfOptions = new com.adobe.livecycle.output.client.RenderOptionsSpec();  
         pdfOptions.setLinearizedPDF(true); 
                                  
         //Create a PDF document             
         OutputResult outputDocument = outClient.generatePDFOutput( 
             TransformationFormat.PDF, 
             "Loan.xdp", 
             "C:\\Adobe", 
             outputOptions, 
             pdfOptions, 
             formData 
         ); 
      
         //Get the Generated PDF file  
         Document ouputDoc = outputDocument.getGeneratedDoc(); 
         return ouputDoc ;  
         } 
         catch (Exception ee) 
         { 
             ee.printStackTrace(); 
         } 
         return null;  
     } 
      
     //This method returns the value of the specified node 
     private String getNodeText(String nodeName, org.w3c.dom.Document myDOM) 
     { 
       //Get the XML node by name 
       NodeList oList = myDOM.getElementsByTagName(nodeName); 
       Node myNode = oList.item(0);  
       NodeList oChildNodes = myNode.getChildNodes(); 
                                   
      String sText = ""; 
      for (int i = 0; i < oChildNodes.getLength(); i++) 
      { 
          Node oItem = oChildNodes.item(i); 
         if (oItem.getNodeType() == Node.TEXT_NODE) 
          { 
            sText = sText.concat(oItem.getNodeValue()); 
          } 
      } 
     return sText; 
     } 
 }
```

## クイックスタート（SOAP モード）:Java API を使用した、Formsへの編集可能なレイアウトの自動埋め込み {#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api}

次のコードの例では、フォームに動的データソースを事前入力します。 つまり、データソースは実行時に作成され、XML ファイル内に含まれず、デザイン時にも作成されません。 このコードの例には、3 つのユーザー定義メソッドが含まれています。

* `createDataSource`:を `org.w3c.dom.Document` フォームの自動埋め込みに使用されるデータソースを表すオブジェクト。 このユーザー定義メソッドは、 `org.w3c.dom.Document` オブジェクト。
* `convertDataSource`:変換後の `org.w3c.dom.Document` オブジェクトを `com.adobe.idp.Document` オブジェクト。 このメソッドは、 `org.w3c.dom.Document` オブジェクトを入力パラメーターとして渡し、 `com.adobe.idp.Document` オブジェクト。
* `renderPOForm`:Formsサービス Java API を使用して、動的な発注書フォームをレンダリングします。 この `com.adobe.idp.Document` が返したオブジェクト `convertDataSource` メソッドは、フォームの事前入力に使用されます。

   これらのメソッドはすべて、Java サーブレットの `doPost` メソッド。 ( [編集可能なレイアウトを使用したFormsの事前入力](/help/forms/developing/rendering-forms.md#prepopulating-forms-with-flowable-layouts).)

```java
/*
* This Java Quick Start uses the following JAR files
* 1. adobe-forms-client.jar
* 2. adobe-livecycle-client.jar
* 3. adobe-usermanager-client.jar
* 4. activation.jar (required for SOAP mode)
* 5. axis.jar (required for SOAP mode)
* 6. commons-codec-1.3.jar (required for SOAP mode)
* 7. commons-collections-3.2.jar (required for SOAP mode)
* 8. commons-discovery.jar (required for SOAP mode)
* 9. commons-logging.jar (required for SOAP mode)
* 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
* 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
* 12. jaxrpc.jar (required for SOAP mode)
* 13. log4j.jar (required for SOAP mode)
* 14. mail.jar (required for SOAP mode)
* 15. saaj.jar (required for SOAP mode)
* 16. wsdl4j.jar (required for SOAP mode)
* 17. xalan.jar (required for SOAP mode)
* 18. xbean.jar (required for SOAP mode)
* 19. xercesImpl.jar (required for SOAP mode)
*
* (Because Forms quick starts are implemented as Java servlets, it is
* not necessary to include J2EE specific JAR files - the Java project
* that contains this quick start is exported as a WAR file which
* is deployed to the J2EE application server)
*
* These JAR files are located in the following path:
* <install directory>/sdk/client-libs/common
*
* For complete details about the location of these JAR files,
* see "Including AEM Forms library files" in Programming with AEM forms
*/
import java.io.IOException;
import javax.servlet.Servlet;
import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import com.adobe.livecycle.formsservice.client. * ;
import java.util. * ;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import org.w3c.dom.Element;
import javax.xml.parsers. * ;
import javax.xml.transform. * ;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;
public class RenderDynamicForm extends HttpServlet implements Servlet {
 public void doGet(HttpServletRequest req, HttpServletResponse resp)
 throws ServletException,
 IOException {
  doPost(req, resp);
 }
 public void doPost(HttpServletRequest req, HttpServletResponse resp)
 throws ServletException,
 IOException {
  //Render a dynamic purchase order form
  //Create an org.w3c.dom.Document object
  org.w3c.dom.Document myDom = createDataSource();
  //Convert the org.w3c.dom.Document object
  //to a com.adobe.idp.Document object
  com.adobe.idp.Document formData = convertDataSource(myDom);
  //Render the dynamic form using data located within the
  //com.adobe.idp.Document object
  renderPOForm(resp, formData);
 }
 //Creates an org.w3c.dom.Document object
 private org.w3c.dom.Document createDataSource() {
  org.w3c.dom.Document document = null;
  try {
   //Create DocumentBuilderFactory and DocumentBuilder objects
   DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
   DocumentBuilder builder = factory.newDocumentBuilder();
   //Create a new Document object
   document = builder.newDocument();
   //Create the root element and append it to the XML DOM
   Element root = (Element) document.createElement("transaction");
   document.appendChild(root);
   //Create the header element
   Element header = (Element) document.createElement("header");
   root.appendChild(header);
   //Create the txtPONum element and append it to the
   //header element
   Element txtPONum = (Element) document.createElement("txtPONum");
   txtPONum.appendChild(document.createTextNode("8745236985"));
   header.appendChild(txtPONum);
   //Create the dtmDate element and append it to the
   //header element
   Element dtmDate = (Element) document.createElement("dtmDate");
   dtmDate.appendChild(document.createTextNode("2007-02-08"));
   header.appendChild(dtmDate);
   //Create the orderedByAddress element and append
   //it to the header element
   Element orderedByAddress = (Element) document.createElement("orderedByAddress");
   orderedByAddress.appendChild(document.createTextNode("222, Any Blvd"));
   header.appendChild(orderedByAddress);
   //Create the txtOrderedByPhone element and append
   //it to the header element
   Element txtOrderedByPhone = (Element) document.createElement("txtOrderedByPhone");
   txtOrderedByPhone.appendChild(document.createTextNode("(555) 555-2334"));
   header.appendChild(txtOrderedByPhone);
   //Create the txtOrderedByFax element and append
   //it to the header element
   Element txtOrderedByFax = (Element) document.createElement("txtOrderedByFax");
   txtOrderedByFax.appendChild(document.createTextNode("(555) 555-9334"));
   header.appendChild(txtOrderedByFax);
   //Create the txtOrderedByContactName element and append
   //it to the header element
   Element txtOrderedByContactName = (Element) document.createElement("txtOrderedByContactName");
   txtOrderedByContactName.appendChild(document.createTextNode("Frank Jones"));
   header.appendChild(txtOrderedByContactName);
   //Create the deliverToAddress element and append
   //it to the header element
   Element deliverToAddress = (Element) document.createElement("deliverToAddress");
   deliverToAddress.appendChild(document.createTextNode("555, Any Blvd"));
   header.appendChild(deliverToAddress);
   //Create the txtDeliverToPhone element and append
   //it to the header element
   Element txtDeliverToPhone = (Element) document.createElement("txtDeliverToPhone");
   txtDeliverToPhone.appendChild(document.createTextNode("(555) 555-9098"));
   header.appendChild(txtDeliverToPhone);
   //Create the txtDeliverToFax element and append
   //it to the header element
   Element txtDeliverToFax = (Element) document.createElement("txtDeliverToFax");
   txtDeliverToFax.appendChild(document.createTextNode("(555) 555-9000"));
   header.appendChild(txtDeliverToFax);
   //Create the txtDeliverToContactName element and
   //append it to the header element
   Element txtDeliverToContactName = (Element) document.createElement("txtDeliverToContactName");
   txtDeliverToContactName.appendChild(document.createTextNode("Jerry Johnson"));
   header.appendChild(txtDeliverToContactName);
   //Create the detail element and append it to the root
   Element detail = (Element) document.createElement("detail");
   root.appendChild(detail);

   //Create the txtPartNum element and append it to the
   //detail element
   Element txtPartNum = (Element) document.createElement("txtPartNum");
   txtPartNum.appendChild(document.createTextNode("00010-100"));
   detail.appendChild(txtPartNum);
   //Create the txtDescription element and append it
   //to the detail element
   Element txtDescription = (Element) document.createElement("txtDescription");
   txtDescription.appendChild(document.createTextNode("Monitor"));
   detail.appendChild(txtDescription);
   //Create the numQty element and append it to
   //the detail element
   Element numQty = (Element) document.createElement("numQty");
   numQty.appendChild(document.createTextNode("1"));
   detail.appendChild(numQty);
   //Create the numUnitPrice element and append it
   //to the detail element
   Element numUnitPrice = (Element) document.createElement("numUnitPrice");
   numUnitPrice.appendChild(document.createTextNode("350.00"));
   detail.appendChild(numUnitPrice);
   //Create another detail element named detail2 and
   //append it to root
   Element detail2 = (Element) document.createElement("detail");
   root.appendChild(detail2);
   //Create the txtPartNum element and append it to the
   //detail2 element
   Element txtPartNum2 = (Element) document.createElement("txtPartNum");
   txtPartNum2.appendChild(document.createTextNode("00010-200"));
   detail2.appendChild(txtPartNum2);
   //Create the txtDescription element and append it
   //to the detail2 element
   Element txtDescription2 = (Element) document.createElement("txtDescription");
   txtDescription2.appendChild(document.createTextNode("Desk lamps"));
   detail2.appendChild(txtDescription2);
   //Create the numQty element and append it to the
   //detail2 element
   Element numQty2 = (Element) document.createElement("numQty");
   numQty2.appendChild(document.createTextNode("3"));
   detail2.appendChild(numQty2);
   //Create the NUMUNITPRICE element
   Element numUnitPrice2 = (Element) document.createElement("numUnitPrice");
   numUnitPrice2.appendChild(document.createTextNode("55.00"));
   detail2.appendChild(numUnitPrice2);
  }
  catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
  return document;

 }
 //Converts an org.w3c.dom.Document object to a
 //com.adobe.idp.Document object
 private Document convertDataSource(org.w3c.dom.Document myDOM) {
  byte[] mybytes = null;
  try {
   //Create a Java Transformer object
   TransformerFactory transFact = TransformerFactory.newInstance();
   Transformer transForm = transFact.newTransformer();
   //Create a Java ByteArrayOutputStream object
   ByteArrayOutputStream myOutStream = new ByteArrayOutputStream();
   //Create a Java Source object
   javax.xml.transform.dom.DOMSource myInput = new DOMSource(myDOM);
   //Create a Java Result object
   javax.xml.transform.stream.StreamResult myOutput = new StreamResult(myOutStream);
   //Populate the Java ByteArrayOutputStream object
   transForm.transform(myInput, myOutput);
   // Get the size of the ByteArrayOutputStream buffer
   int myByteSize = myOutStream.size();
   //Allocate myByteSize to the byte array
   mybytes = new byte[myByteSize];
   //Copy the content to the byte array
   mybytes = myOutStream.toByteArray();
  }
  catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
  //Create a com.adobe.idp.Document object and copy the
  //contents of the byte array
  Document myDocument = new Document(mybytes);
  return myDocument;
 }
 //Render the purchase order form using the specified
 //com.adobe.idp.Document object
 private void renderPOForm(HttpServletResponse resp, Document formData) {
  try {
   //Set connection properties required to invoke AEM Forms
   Properties connectionProps = new Properties();
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceC
   lientFactoryProperties.DSC_SOAP_PROTOCOL);
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
   //Create a ServiceClientFactory object
   ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
   //Create a FormsServiceClient object
   FormsServiceClient formsClient = new FormsServiceClient(myFactory);
   //Set the parameter values for the renderPDFForm method
   String formName = "Applications/FormsApplication/1.0/FormsFolder/PO.xdp";
   //Cache the form
   PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
   pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
   //Specify URI values that are required to render a form
   URLSpec uriValues = new URLSpec();
   uriValues.setApplicationWebRoot("https://[server]:[port]/FormsQS");
   uriValues.setContentRootURI("repository:///");
   uriValues.setTargetURL("https://[server]:[port]/FormsQS/HandleData");
   //Invoke the renderForm method
   FormsResult formOut = formsClient.renderPDFForm(
   formName, //formQuery
   formData, //inDataDoc
   pdfFormRenderSpec, //PDFFormRenderSpec
   uriValues, //urlSpec
   null //attachments
   );
   //Create a ServletOutputStream object
   ServletOutputStream oOutput = resp.getOutputStream();
   //Create a Document object that stores form data
   Document myData = formOut.getOutputContent();
   //Create an InputStream object
   InputStream inputStream = myData.getInputStream();
   //Write the data stream to the web browser
   byte[] data = new byte[4096];
   int bytesRead = 0;
   while ((bytesRead = inputStream.read(data)) > 0) {
    oOutput.write(data, 0, bytesRead);
   }
  } catch(Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
 }
}
```

## クイックスタート（SOAP モード）:Java API を使用した計算スクリプトを含むフォームの処理 {#quick-start-soap-mode-handling-a-form-containing-a-calculation-script-using-the-java-api}

次のコード例では、計算スクリプトを含むフォームを処理し、結果をクライアント Web ブラウザーに書き戻します。 ( [フォームデータの計算](/help/forms/developing/rendering-forms.md#calculating-form-data).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
    * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
 import java.util.*; 
 import java.io.InputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class CalculateData extends HttpServlet implements Servlet { 
  
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
             doPost(req,resp); 
     } 
  
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
              
         try{ 
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
             //Create a FormsServiceClient object 
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
             //Get form data to pass to the processFormSubmission method 
             Document formData = new Document(req.getInputStream());  
  
             //Set run-time options 
             RenderOptionsSpec processSpec = new RenderOptionsSpec();  
             processSpec.setLocale("en_US"); 
                                    
             //Invoke the processFormSubmission method 
             FormsResult formOut = formsClient.processFormSubmission(formData,"CONTENT_TYPE=application/pdf&CONTENT_TYPE=application/vnd.adobe.xdp+xml","",processSpec); 
              
             //Get the processing state 
             short processState = formOut.getAction(); 
              
             //Determine if the form data is calculated 
             if (processState == 1)  
             { 
                  
                 //Write the data back to to the client web browser 
                 ServletOutputStream oOutput = resp.getOutputStream(); 
                 Document calData = formOut.getOutputContent(); 
                  
                 //Create an InputStream object 
                 InputStream inputStream = calData.getInputStream(); 
          
                 //Write the data stream to the web browser 
                 byte[] data = new byte[4096]; 
                 int bytesRead = 0; 
                 while ((bytesRead = inputStream.read(data)) > 0) 
                 { 
                     oOutput.write(data, 0, bytesRead); 
                 } 
              } 
             } 
         catch (Exception e) { 
              System.out.println("The following exception occurred: "+e.getMessage()); 
         } 
     } 
 }
```

## クイックスタート（SOAP モード）:Java API を使用したパフォーマンスの最適化 {#quick-start-soap-mode-optimizing-performance-using-the-java-api}

次のコードの例では、caching、standalone、linearized の各オプションを設定することで、パフォーマンスを最適化しています。 線形化されたファイルは、Web 上での配信に最適化されます。 ( [Forms Service のパフォーマンスの最適化](/help/forms/developing/rendering-forms.md#optimizing-the-performance-of-the-forms-service).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
    * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
 import java.util.*; 
 import java.io.InputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RenderFormsPerformance extends HttpServlet implements Servlet { 
      
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
             doPost(req,resp);  
     } 
  
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
     try{ 
              
         //Set connection properties required to invoke AEM Forms                                 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
         //Create a ServiceClientFactory object 
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
         //Create a FormsServiceClient object 
         FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
         //Set the parameter values for the renderForm method 
         String formName = "Applications/FormsApplication/1.0/FormsFolder/Loan.xdp";  
         byte[]    cData = "".getBytes(); 
         Document oInputData = new Document(cData); 
                      
         //Set performance run-time options 
         PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();  
         renderSpec.setCacheEnabled(new Boolean(true)); 
         renderSpec.setLinearizedPDF(true); 
                  
         //Specify URI values that are required to render a form 
         //design located in the AEM Forms Repository 
         URLSpec uriValues = new URLSpec();  
         uriValues.setApplicationWebRoot("https://[server]:[port]/FormsServiceClientApp"); 
         uriValues.setContentRootURI("repository:///"); 
         uriValues.setTargetURL("https://[server]:[port]/FormsServiceClientApp/HandleData"); 
                  
         //Invoke the renderPDFForm method and write the  
         //results to a client web browser 
         FormsResult formOut = formsClient.renderPDFForm( 
                     formName,       //formQuery 
                     oInputData,     //inDataDoc 
                     renderSpec,     //PDFFormRenderSpec 
                     uriValues,        //urlSpec 
                     null            //attachments 
                     ); 
          
         //Create a ServletOutputStream object 
         ServletOutputStream oOutput = resp.getOutputStream(); 
          
         //Create a Document object that stores form data 
         Document myData = formOut.getOutputContent(); 
          
         //Create an InputStream object 
         InputStream inputStream = myData.getInputStream(); 
          
         //Write the data stream to the web browser 
         byte[] data = new byte[4096]; 
         int bytesRead = 0; 
         while ((bytesRead = inputStream.read(data)) > 0) 
         { 
             oOutput.write(data, 0, bytesRead); 
         } 
          
         }catch (Exception e) { 
              System.out.println("The following exception occurred: "+e.getMessage()); 
       } 
     } 
 }
```

## クイックスタート（SOAP モード）:Java API を使用した値によるレンダリング {#quick-start-soap-mode-rendering-by-value-using-the-java-api}

次の Java クイックスタートでは、という名前のフォームデザインに基づいたインタラクティブなPDFフォームがレンダリングされます。 *Loan.xdp* 値別。 フォームデザインは `com.adobe.idp.Document` * inputXDP*という名前のオブジェクト。 ( [値別にFormsをレンダリング](/help/forms/developing/rendering-forms.md#rendering-forms-by-value).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
    * 4. activation.jar (required for SOAP mode) 
    * 5. axis.jar (required for SOAP mode) 
    * 6. commons-codec-1.3.jar (required for SOAP mode) 
    * 7. commons-collections-3.2.jar  (required for SOAP mode) 
    * 8. commons-discovery.jar (required for SOAP mode) 
    * 9. commons-logging.jar (required for SOAP mode) 
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
    * 12. jaxrpc.jar (required for SOAP mode) 
    * 13. log4j.jar (required for SOAP mode) 
    * 14. mail.jar (required for SOAP mode) 
    * 15. saaj.jar (required for SOAP mode) 
    * 16. wsdl4j.jar (required for SOAP mode) 
    * 17. xalan.jar (required for SOAP mode) 
    * 18. xbean.jar (required for SOAP mode) 
    * 19. xercesImpl.jar (required for SOAP mode) 
    * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms. 
     */ 
 import java.io.FileInputStream; 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
  
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
 import com.adobe.livecycle.formsservice.client.*; 
 import java.util.*; 
 import java.io.InputStream; 
  
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RenderByValue extends HttpServlet implements Servlet { 
  
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
             doPost(req,resp); 
     } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
         try{ 
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
             //Create a FormsServiceClient object 
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
          
             //Retrieve the form design 
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xdp");  
             Document inputXDP = new Document(fileInputStream); 
          
             //Specify URI values that are required to render a form 
             URLSpec uriValues = new URLSpec();  
             uriValues.setApplicationWebRoot("https://[server]:[port]/FormsQS"); 
             uriValues.setTargetURL("https://[server]:[port]/FormsQS/HandleData"); 
                      
             //Invoke the renderPDFForm method and pass the  
             //form design by value 
             FormsResult formOut = formsClient.renderPDFForm( 
                         "",                     //formQuery 
                         inputXDP,                 //inDataDoc 
                         new PDFFormRenderSpec(), //PDFFormRenderSpec 
                         uriValues,                //urlSpec 
                         null                    //attachments 
                         ); 
          
             //Create a Document object that stores form data 
             Document myData = formOut.getOutputContent(); 
          
             //Get the content type of the response and 
             //set the HttpServletResponse object?s content type 
             String contentType = myData.getContentType();  
             resp.setContentType(contentType); 
          
             //Create a ServletOutputStream object 
             ServletOutputStream oOutput = resp.getOutputStream(); 
          
             //Create an InputStream object 
             InputStream inputStream = myData.getInputStream(); 
          
             //Write the data stream to the web browser 
             byte[] data = new byte[4096]; 
             int bytesRead = 0; 
             while ((bytesRead = inputStream.read(data)) > 0) 
             { 
                 oOutput.write(data, 0, bytesRead); 
             } 
          
             }catch (Exception e) { 
                  e.printStackTrace(); 
               } 
         } 
 }
```

## クイックスタート（SOAP モード）:Java API を使用してForms Service にドキュメントを渡す {#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api}

次の Java クイックスタートでは、Content Services（非推奨）から Loan.xdp ファイルを取得します。 この XDP ファイルはスペース内にあります `/Company Home/Form Designs`. XDP ファイルは `com.adobe.idp.Document` インスタンス。 この `com.adobe.idp.Document` インスタンスがFormsサービスに渡されます。 インタラクティブフォームは、クライアント Web ブラウザーに書き込まれます。 ( [Forms Service にドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md).)

```as3
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-forms-client.jar 
     * 2. adobe-contentservices-client.jar 
     * 3. adobe-livecycle-client.jar 
     * 4. adobe-usermanager-client.jar 
     * 
     * (Because Forms quick starts are implemented as Java servlets, it is  
     * not necessary to include J2EE specific JAR files - the Java project 
     * that contains this quick start is exported as a WAR file which 
     * is deployed to the J2EE application server) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * For complete details about the location of these JAR files,  
     * see "Including AEM Forms library files" in Programming with AEM forms. 
     */ 
 import java.io.IOException; 
 import javax.servlet.Servlet; 
 import javax.servlet.ServletException; 
 import javax.servlet.ServletOutputStream; 
 import javax.servlet.http.HttpServlet; 
 import javax.servlet.http.HttpServletRequest; 
 import javax.servlet.http.HttpServletResponse; 
  
 import com.adobe.livecycle.contentservices.client.CRCResult; 
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl; 
 import com.adobe.livecycle.formsservice.client.*; 
  
 import java.util.*; 
 import java.io.InputStream; 
  
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RenderFormsFromContentServices extends HttpServlet implements Servlet { 
  
     public void doGet(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
             doPost(req,resp); 
     } 
      
     public void doPost(HttpServletRequest req, HttpServletResponse resp) 
         throws ServletException, IOException { 
         try{ 
             //Set connection properties required to invoke AEM Forms 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
             //Create a FormsServiceClient object 
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);  
                          
             //Create an empty Document that represents form data 
             byte[]    cData = "".getBytes(); 
             Document oInputData = new Document(cData); 
              
             //Get the form design from Content Services (deprecated) 
             Document formDesign =  GetFormDesign(myFactory); 
                                      
             //Cache the PDF form 
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec(); 
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true)); 
                      
             //Invoke the renderPDFForm2 and pass to the  
             //Document that contains the form design 
             FormsResult formOut = formsClient.renderPDFForm2( 
                     formDesign,               
                     oInputData,              
                     pdfFormRenderSpec,       
                     null,                 
                     null             
                     ); 
          
             //Create a Document object that stores form data 
             Document myData = formOut.getOutputContent(); 
          
             //Get the content type of the response and 
             //set the HttpServletResponse object?s content type 
             String contentType = myData.getContentType();  
             resp.setContentType(contentType); 
          
             //Create a ServletOutputStream object 
             ServletOutputStream oOutput = resp.getOutputStream(); 
          
             //Create an InputStream object 
             InputStream inputStream = myData.getInputStream(); 
          
             //Write the data stream to the web browser 
             byte[] data = new byte[4096]; 
             int bytesRead = 0; 
             while ((bytesRead = inputStream.read(data)) > 0) 
             { 
                 oOutput.write(data, 0, bytesRead); 
             } 
          
             }catch (Exception e) { 
                  e.printStackTrace(); 
               } 
         } 
          
     //Retrieve the form design from Content Services (deprecated) 
     private Document GetFormDesign(ServiceClientFactory myFactory) 
     { 
         try{ 
              
         //Create a DocumentManagementServiceClientImpl object 
         DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);  
              
         //Specify the name of the store and the content to retrieve 
            String storeName = "SpacesStore"; 
            String nodeName  = "/Company Home/Form Designs/Loan.xdp"; 
  
            //Retrieve /Company Home/Form Designs/Loan.xdp 
            CRCResult content = docManager.retrieveContent( 
                      storeName, 
                      nodeName, 
                      ""); 
      
            //Return the Document instance 
             Document doc =content.getDocument();  
             return  doc; 
          } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
         return null;  
     } 
      
 } 
 
```
