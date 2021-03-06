---
title: ドキュメント管理サービス（非推奨）Java API クイックスタート (SOAP)
seo-title: Document Management Service (Deprecated)Java API Quick Start(SOAP)
description: Document Management Service Java API を使用して、Content Services スペースの作成、Content Services スペースの削除、Content Services へのコンテンツの追加、Content Services からのコンテンツの取得、Content Services コンテンツの検索、Ces 権限の設定を行います。
seo-description: Use the Document Management Service Java API to create Content Services spaces, delete Content Services spaces, Add content to Content Services, retrieve content from Content Services, move Content Services content, list Content Services content, search Content Services content, and set Content Services permissions.
uuid: 967c282a-ccde-4489-a4d5-53c6a1a0cac0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: 9cffdb77-c8a4-4a15-b64f-1d3aadaa60c7
role: Developer
exl-id: 5ffd9600-03ec-4fd5-abb1-a8d9adefe6f3
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---

# ドキュメント管理サービス（非推奨）Java API クイックスタート (SOAP) {#document-management-service-deprecated-java-api-quick-start-soap}

Document Management サービス（非推奨）では、次のクイックスタートを使用できます。

>[!NOTE]
>
>2011 年 8 月 5 日より、Adobeは、Content Services ES のお客様をAdobe Digital Enterprise Platform Experience Services に移行します。 Content Services を使用するお客様向けの製品ロードマップは、Day Software のAdobe買収時に獲得した、最新のモジュラー CRX アーキテクチャに基づいて構築されたネイティブの Content Repository を含む、新しい ADEP Experience Services - Core に移行することです。

[クイックスタート（SOAP モード）:Java API を使用した Content Services スペースの作成](document-management-service-deprecated-java.md#quick-start-soap-mode-create-content-services-spaces-using-the-java-api-deprecated)

[クイックスタート（SOAP モード）:Java API を使用したコンテンツサービスコンテンツの削除](document-management-service-deprecated-java.md#quick-start-soap-mode-delete-content-services-content-using-the-java-api-deprecated)

[クイックスタート（SOAP モード）:Java API を使用してコンテンツサービスにコンテンツを追加する](document-management-service-deprecated-java.md#quick-start-soap-mode-add-content-to-content-services-using-the-java-api-deprecated)

[クイックスタート（SOAP モード）:Java API を使用してコンテンツサービスからコンテンツを取得する](document-management-service-deprecated-java.md#quick-start-soap-mode-retrieve-content-from-content-services-using-the-java-api-deprecated)

[クイックスタート（SOAP モード）:Java API を使用したコンテンツサービスの移動](document-management-service-deprecated-java.md#quick-start-soap-mode-move-content-services-content-using-the-java-api-deprecated)

[クイックスタート（SOAP モード）:Java API を使用したコンテンツサービスコンテンツのリスト](document-management-service-deprecated-java.md#quick-start-soap-mode-list-content-services-content-using-the-java-api-deprecated)

[クイックスタート（SOAP モード）:Java API を使用したコンテンツサービスコンテンツの検索](document-management-service-deprecated-java.md#quick-start-soap-mode-search-content-services-content-using-the-java-api-deprecated)

[クイックスタート（SOAP モード）:Java API を使用したコンテンツサービス権限の設定](document-management-service-deprecated-java.md#quick-start-soap-mode-setting-content-services-permissions-using-the-java-api-deprecated)

AEM Formsの操作は、AEM Formsの厳密に型指定された API を使用して実行できます。接続モードは、SOAP に設定する必要があります。

>[!NOTE]
>
>「 AEM forms によるプログラミング」のクイックスタートは、JBoss および Windows オペレーティングシステムにデプロイされるForms Server に基づいています。 ただし、UNIX などの別のオペレーティング・システムを使用している場合は、windows 固有のパスを、該当するオペレーティング・システムでサポートされるパスに置き換えます。 同様に、別の J2EE アプリケーションサーバーを使用する場合は、有効な接続プロパティを必ず指定してください。 詳しくは、 [接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## クイックスタート（SOAP モード）:Java API（非推奨）を使用した Content Services スペースの作成 {#quick-start-soap-mode-create-content-services-spaces-using-the-java-api-deprecated}

次の Java コードの例では、会社のホームに「Test Directory」という名前の新しいスペースを作成します。 新しいスペースの識別値がコンソールに書き込まれます。

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-contentservices-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. activation.jar (required for SOAP mode) 
     * 7. axis.jar (required for SOAP mode) 
     * 8. commons-codec-1.3.jar (required for SOAP mode) 
     * 9.  commons-collections-3.1.jar  (required for SOAP mode) 
     * 10. commons-discovery.jar (required for SOAP mode) 
     * 11. commons-logging.jar (required for SOAP mode) 
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 14. jaxrpc.jar (required for SOAP mode) 
     * 15. log4j.jar (required for SOAP mode) 
     * 16. mail.jar (required for SOAP mode) 
     * 17. saaj.jar (required for SOAP mode) 
     * 18. wsdl4j.jar (required for SOAP mode) 
     * 19. xalan.jar (required for SOAP mode) 
     * 20. xbean.jar (required for SOAP mode) 
     * 21. xercesImpl.jar (required for SOAP mode) 
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
     * SOAP required JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include these additional JAR files 
     * 
     * For information about the SOAP  
     * mode, see "Setting connection properties" in Programming  
     * with AEM Forms 
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl; 
  
 public class CreateNewSpaceSoap { 
  
     public static void main(String[] args) { 
          
         try{ 
          
             //Set connection properties required to invoke AEM Forms using SOAP mode                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a DocumentManagementServiceClientImpl object 
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);  
              
             //Specify the name of the store and node 
             String storeName ="SpacesStore";  
             String nodeName = "/Company Home/Test Directory" ; 
                                  
             //Create a new space 
             String spaceId = docManager.createSpace(storeName,nodeName); 
             System.out.println("The identifier value of the new space is " +spaceId); 
         } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
 
```

## クイックスタート（SOAP モード）:Java API（非推奨）を使用した Content Services コンテンツの削除 {#quick-start-soap-mode-delete-content-services-content-using-the-java-api-deprecated}

次の Java コードの例では、 /Company Home/Test Directory という名前のスペースを削除します。

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-contentservices-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. activation.jar (required for SOAP mode) 
     * 7. axis.jar (required for SOAP mode) 
     * 8. commons-codec-1.3.jar (required for SOAP mode) 
     * 9.  commons-collections-3.1.jar  (required for SOAP mode) 
     * 10. commons-discovery.jar (required for SOAP mode) 
     * 11. commons-logging.jar (required for SOAP mode) 
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 14. jaxrpc.jar (required for SOAP mode) 
     * 15. log4j.jar (required for SOAP mode) 
     * 16. mail.jar (required for SOAP mode) 
     * 17. saaj.jar (required for SOAP mode) 
     * 18. wsdl4j.jar (required for SOAP mode) 
     * 19. xalan.jar (required for SOAP mode) 
     * 20. xbean.jar (required for SOAP mode) 
     * 21. xercesImpl.jar (required for SOAP mode) 
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
     * SOAP required JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include these additional JAR files 
     * 
     * For information about the SOAP  
     * mode, see "Setting connection properties" in Programming  
     * with AEM Forms 
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl; 
  
 public class DeleteContentSoap { 
  
     public static void main(String[] args) { 
          
         try{ 
          
             //Set connection properties required to invoke AEM Forms using SOAP mode                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a DocumentManagementServiceClientImpl object 
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);  
              
             //Specify the name of the store and node 
             String storeName ="SpacesStore";  
             String nodeName = "/Company Home/Test Directory" ; 
              
             //Delete the content from /Company Home/Test Directory 
             Boolean ans = docManager.deleteContent(storeName, nodeName); 
              
             if (ans == true) 
                 System.out.println("The content was successfully deleted"); 
             else 
                 System.out.println("The content was not deleted"); 
             } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
 
```

## クイックスタート（SOAP モード）:Java API（非推奨）を使用して Content Services にコンテンツを追加する {#quick-start-soap-mode-add-content-to-content-services-using-the-java-api-deprecated}

次の Java コードの例では、という名前のPDFファイルを追加します。 *MortgageForm.pdf* /Company Home/Test Directory という名前のフォルダに移動します。 creator 属性と description 属性が設定されます。 新しいコンテンツの識別値がコンソールに書き込まれます。

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-contentservices-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. activation.jar (required for SOAP mode) 
     * 7. axis.jar (required for SOAP mode) 
     * 8. commons-codec-1.3.jar (required for SOAP mode) 
     * 9.  commons-collections-3.1.jar  (required for SOAP mode) 
     * 10. commons-discovery.jar (required for SOAP mode) 
     * 11. commons-logging.jar (required for SOAP mode) 
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 14. jaxrpc.jar (required for SOAP mode) 
     * 15. log4j.jar (required for SOAP mode) 
     * 16. mail.jar (required for SOAP mode) 
     * 17. saaj.jar (required for SOAP mode) 
     * 18. wsdl4j.jar (required for SOAP mode) 
     * 19. xalan.jar (required for SOAP mode) 
     * 20. xbean.jar (required for SOAP mode) 
     * 21. xercesImpl.jar (required for SOAP mode) 
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
     * SOAP required JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include these additional JAR files 
     * 
     * For information about the SOAP  
     * mode, see "Setting connection properties" in Programming  
     * with AEM Forms 
     */ 
 import java.io.File; 
 import java.util.*; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.livecycle.contentservices.client.CRCResult; 
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl; 
 import com.adobe.livecycle.contentservices.client.impl.UpdateVersionType; 
  
 public class AddContentSoap { 
  
     public static void main(String[] args) { 
          
         try{ 
          
             //Set connection properties required to invoke AEM Forms using SOAP mode                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a DocumentManagementServiceClientImpl object 
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory); 
              
             //Specify the store and node name 
             String storeName ="SpacesStore";  
             String nodeName = "/Company Home/Test Directory" ; 
              
             //Retrieve the document to store in /Company Home/Test Directory 
             Document content =  new Document(new File("C:\\Adobe\MortgageForm.pdf"), false); 
              
             //Create a MAP instance to store attributes 
             Map<String,Object> inputs = new HashMap<String,Object>(); 
              
             //Specify attributes that belong to the new content 
             String creator = "{https://www.alfresco.org/model/content/1.0}creator"; 
             String description = "{https://www.alfresco.org/model/content/1.0}description";  
              
             inputs.put(creator,"Tony Blue"); 
             inputs.put(description,"A mortgage application form"); 
                                  
             //Store MortgageForm.pdf in /Company Home/Test Directory 
             CRCResult result = docManager.storeContent(storeName,  
                      nodeName, 
                     "MortgageForm.pdf", 
                     "{https://www.alfresco.org/model/content/1.0}content",  
                     content, 
                     "UTF-8", 
                     UpdateVersionType.INCREMENT_MAJOR_VERSION, 
                     null, 
                     inputs);  
              
             //Get the identifier value of the new content 
             String id = result.getNodeUuid(); 
             System.out.println("The identifier value of the new content is "+id); 
     } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
 
```

## クイックスタート（SOAP モード）:Java API（非推奨）を使用して Content Services からコンテンツを取得する {#quick-start-soap-mode-retrieve-content-from-content-services-using-the-java-api-deprecated}

次の Java コードの例では、という名前のPDFファイルを取得します。 *MortgageForm.pdf* /Company Home から。 PDF・ファイルはローカル・ファイル・システムに保存され、という名前が付けられます。 *UpdatedMortgageForm.pdf*.

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-contentservices-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. activation.jar (required for SOAP mode) 
     * 7. axis.jar (required for SOAP mode) 
     * 8. commons-codec-1.3.jar (required for SOAP mode) 
     * 9.  commons-collections-3.1.jar  (required for SOAP mode) 
     * 10. commons-discovery.jar (required for SOAP mode) 
     * 11. commons-logging.jar (required for SOAP mode) 
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 14. jaxrpc.jar (required for SOAP mode) 
     * 15. log4j.jar (required for SOAP mode) 
     * 16. mail.jar (required for SOAP mode) 
     * 17. saaj.jar (required for SOAP mode) 
     * 18. wsdl4j.jar (required for SOAP mode) 
     * 19. xalan.jar (required for SOAP mode) 
     * 20. xbean.jar (required for SOAP mode) 
     * 21. xercesImpl.jar (required for SOAP mode) 
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
     * SOAP required JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include these additional JAR files 
     * 
     * For information about the SOAP  
     * mode, see "Setting connection properties" in Programming  
     * with AEM Forms 
     */ 
 import java.io.File; 
 import java.util.*; 
  
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.livecycle.contentservices.client.CRCResult; 
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl; 
  
 public class RetrieveContentSoap { 
  
     public static void main(String[] args) { 
          
         try{ 
             //Set connection properties required to invoke AEM Forms using SOAP mode                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a DocumentManagementServiceClientImpl object 
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);  
              
             //Specify the name of the store and the content to retrieve 
                String storeName = "SpacesStore"; 
                String nodeName  = "/Company Home/MortgageForm.pdf"; 
  
                //Retrieve /Company Home/MortgageForm.pdf 
                CRCResult content = docManager.retrieveContent( 
                      storeName, 
                      nodeName, 
                      ""); 
      
                //Write the PDF file to the local file system 
                File myFile = new File("C:\\Adobe\UpdatedMortgageForm.pdf"); 
                Document doc =content.getDocument();  
                doc.copyToFile(myFile); 
          } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
  
 
```

## クイックスタート（SOAP モード）:Java API（非推奨）を使用した Content Services コンテンツの移動 {#quick-start-soap-mode-move-content-services-content-using-the-java-api-deprecated}

次の Java コードの例では、という名前のPDFファイルを移動します。 *MortgageForm.pdf* /Company Home/Test Directory から/Company Home に移動します。 移動されたコンテンツの識別値がコンソールに書き込まれます。

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-contentservices-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. activation.jar (required for SOAP mode) 
     * 7. axis.jar (required for SOAP mode) 
     * 8. commons-codec-1.3.jar (required for SOAP mode) 
     * 9.  commons-collections-3.1.jar  (required for SOAP mode) 
     * 10. commons-discovery.jar (required for SOAP mode) 
     * 11. commons-logging.jar (required for SOAP mode) 
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 14. jaxrpc.jar (required for SOAP mode) 
     * 15. log4j.jar (required for SOAP mode) 
     * 16. mail.jar (required for SOAP mode) 
     * 17. saaj.jar (required for SOAP mode) 
     * 18. wsdl4j.jar (required for SOAP mode) 
     * 19. xalan.jar (required for SOAP mode) 
     * 20. xbean.jar (required for SOAP mode) 
     * 21. xercesImpl.jar (required for SOAP mode) 
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
     * SOAP required JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include these additional JAR files 
     * 
     * For information about the SOAP  
     * mode, see "Setting connection properties" in Programming  
     * with AEM Forms 
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl; 
  
 public class MoveContentSoap { 
  
     public static void main(String[] args) { 
          
         try{ 
          
             //Set connection properties required to invoke AEM Forms using SOAP mode                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
  
             //Create a DocumentManagementServiceClientImpl object 
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);  
              
             //Specify the name of the store and the content to move 
                String storeName = "SpacesStore"; 
                String nodeName = "/Company Home/Test Directory/MortgageForm.pdf"; 
                String newSpace = "/Company Home"; 
  
                //Move the content from /Company Home/Test Directory 
                //to /Company Home and display the identifier value of the  
                //moved content 
                String contentID = docManager.moveContent(storeName, nodeName, newSpace); 
                System.out.println("The identifier value of the moved content is "+contentID); 
         } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
  
 
```

## クイックスタート（SOAP モード）:Java API（非推奨）を使用した Content Services コンテンツのリスト {#quick-start-soap-mode-list-content-services-content-using-the-java-api-deprecated}

次の Java コードの例は、/Company Home にあるコンテンツをリストします。 各ノードタイプとノード名が表示されます。

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-contentservices-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. activation.jar (required for SOAP mode) 
     * 7. axis.jar (required for SOAP mode) 
     * 8. commons-codec-1.3.jar (required for SOAP mode) 
     * 9.  commons-collections-3.1.jar  (required for SOAP mode) 
     * 10. commons-discovery.jar (required for SOAP mode) 
     * 11. commons-logging.jar (required for SOAP mode) 
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 14. jaxrpc.jar (required for SOAP mode) 
     * 15. log4j.jar (required for SOAP mode) 
     * 16. mail.jar (required for SOAP mode) 
     * 17. saaj.jar (required for SOAP mode) 
     * 18. wsdl4j.jar (required for SOAP mode) 
     * 19. xalan.jar (required for SOAP mode) 
     * 20. xbean.jar (required for SOAP mode) 
     * 21. xercesImpl.jar (required for SOAP mode) 
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
     * SOAP required JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include these additional JAR files 
     * 
     * For information about the SOAP  
     * mode, see "Setting connection properties" in Programming  
     * with AEM Forms 
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.livecycle.contentservices.client.CRCResult; 
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl; 
  
 public class ListingContentSoap { 
  
     public static void main(String[] args) { 
          
         try{ 
          
             //Set connection properties required to invoke AEM Forms using SOAP mode                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a DocumentManagementServiceClientImpl object 
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);  
              
             //Specify the name of the store and the space 
                String storeName = "SpacesStore"; 
                String nodeName  = "/Company Home"; 
  
               //List the contents of /Company Home 
               List<CRCResult> allImages = docManager.getSpaceContents( 
                      storeName, 
                      nodeName, 
                      false); 
               
              //Create an Iterator object and iterate through  
              //the List object 
              Iterator iter = allImages.iterator();  
              int i = 0 ;  
              while (iter.hasNext()) {  
                                
                  //Get the node content type and name  
                  CRCResult sinContent = (CRCResult)iter.next();  
                  String nodeType =  sinContent.getNodeType(); 
                  String name = sinContent.getNodeName(); 
                  System.out.println("The node type is "+nodeType  +". The node name is "+name);   
              } 
         } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
  
 
```

## クイックスタート（SOAP モード）:Java API（非推奨）を使用した Content Services コンテンツの検索 {#quick-start-soap-mode-search-content-services-content-using-the-java-api-deprecated}

次の Java コードでは、MortgageForm というテキストを含むドキュメントを/Company Home で検索します。 サブフォルダーも検索されます。

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-contentservices-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. activation.jar (required for SOAP mode) 
     * 7. axis.jar (required for SOAP mode) 
     * 8. commons-codec-1.3.jar (required for SOAP mode) 
     * 9.  commons-collections-3.1.jar  (required for SOAP mode) 
     * 10. commons-discovery.jar (required for SOAP mode) 
     * 11. commons-logging.jar (required for SOAP mode) 
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 14. jaxrpc.jar (required for SOAP mode) 
     * 15. log4j.jar (required for SOAP mode) 
     * 16. mail.jar (required for SOAP mode) 
     * 17. saaj.jar (required for SOAP mode) 
     * 18. wsdl4j.jar (required for SOAP mode) 
     * 19. xalan.jar (required for SOAP mode) 
     * 20. xbean.jar (required for SOAP mode) 
     * 21. xercesImpl.jar (required for SOAP mode) 
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
     * SOAP required JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include these additional JAR files 
     * 
     * For information about the SOAP  
     * mode, see "Setting connection properties" in Programming  
     * with AEM Forms 
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.livecycle.contentservices.client.ResultSet; 
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl; 
 import com.adobe.livecycle.contentservices.client.impl.QueryImpl; 
 import com.adobe.livecycle.contentservices.client.impl.StatementImpl; 
  
 public class SearchSpaceSoap { 
  
     public static void main(String[] args) { 
          
         try{ 
             //Set connection properties required to invoke AEM Forms using SOAP mode                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a DocumentManagementServiceClientImpl object 
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory);  
              
             //Specify the name of the store and node 
             String path ="/Company Home";  
              String storeName = "SpacesStore"; 
              
             //Create a Query expression 
             QueryImpl qImpl = new QueryImpl(); 
             String myName = "{https://www.alfresco.org/model/content/1.0}name"; 
             StatementImpl statement = new StatementImpl(myName, StatementImpl.OPERATOR_CONTAINS, "MortgageForm" ); 
             qImpl.addStatement(statement);  
          
             //Perform the search for a document that contains the text MortgageForm 
             ResultSet rs = docManager.searchRepository(storeName, path, true, qImpl, 200); 
             long resultSize = rs.getResultSize();  
              
             //Determine if the document is located in Content space 
             if (resultSize > 0) 
             { 
                 System.out.println("MortgageForm is located in the Repository"); 
             } 
         } 
     catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
  
 
```

## クイックスタート（SOAP モード）:Java API（非推奨）を使用した Content Services 権限の設定 {#quick-start-soap-mode-setting-content-services-permissions-using-the-java-api-deprecated}

次の Java コードの例では、tony blue という名前のユーザーに権限を設定します。 指定されたドメインがデフォルトのドメインです。 消費者権限が指定され、ノードが `/Company Home/Test Directory`.

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-contentservices-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. activation.jar (required for SOAP mode) 
     * 7. axis.jar (required for SOAP mode) 
     * 8. commons-codec-1.3.jar (required for SOAP mode) 
     * 9.  commons-collections-3.1.jar  (required for SOAP mode) 
     * 10. commons-discovery.jar (required for SOAP mode) 
     * 11. commons-logging.jar (required for SOAP mode) 
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 14. jaxrpc.jar (required for SOAP mode) 
     * 15. log4j.jar (required for SOAP mode) 
     * 16. mail.jar (required for SOAP mode) 
     * 17. saaj.jar (required for SOAP mode) 
     * 18. wsdl4j.jar (required for SOAP mode) 
     * 19. xalan.jar (required for SOAP mode) 
     * 20. xbean.jar (required for SOAP mode) 
     * 21. xercesImpl.jar (required for SOAP mode) 
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
     * SOAP required JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include these additional JAR files 
     * 
     * For information about the SOAP  
     * mode, see "Setting connection properties" in Programming  
     * with AEM Forms 
     */ 
  
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl; 
 import com.adobe.livecycle.contentservices.client.impl.ContentAccessPermission; 
  
 public class SetPermissionsSoap { 
  
     public static void main(String[] args) { 
          
         try{ 
          
             //Set connection properties required to invoke AEM Forms using SOAP mode     
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a DocumentManagementServiceClientImpl object 
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory); 
              
             //Specify the store and node name 
             String storeName ="SpacesStore";  
             String nodeName = "/Company Home/Test Directory/"; 
              
              //Create a new permission 
             ContentAccessPermission permission = new ContentAccessPermission(); 
             permission.setAuthority("tblue/DefaultDom");  
             permission.setIsAllowed(false); 
             permission.setPermission("Consumer"); 
              
             //Create a collection to hold the values 
             List<ContentAccessPermission> permissionList = new ArrayList<ContentAccessPermission>(); 
             permissionList.add(0,permission); 
                          
             //Set the permission 
             docManager.writePermissions(storeName,  
                      nodeName, 
                      permissionList, 
                     false);  
     } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
 
```

## クイックスタート（SOAP モード）:Java API を使用した関連付けの作成（廃止） {#quick-start-soap-mode-creating-associations-using-the-java-api-deprecated}

次の Java コードは、XML データファイルとPDFフォームの関連付けを作成します。 このタイプの関連付けの名前は LinkedBy です。PDFドキュメントには、アスペクトリンクが可能なアスペクトが適用されている必要があります。

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-contentservices-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. activation.jar (required for SOAP mode) 
     * 7. axis.jar (required for SOAP mode) 
     * 8. commons-codec-1.3.jar (required for SOAP mode) 
     * 9.  commons-collections-3.1.jar  (required for SOAP mode) 
     * 10. commons-discovery.jar (required for SOAP mode) 
     * 11. commons-logging.jar (required for SOAP mode) 
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 14. jaxrpc.jar (required for SOAP mode) 
     * 15. log4j.jar (required for SOAP mode) 
     * 16. mail.jar (required for SOAP mode) 
     * 17. saaj.jar (required for SOAP mode) 
     * 18. wsdl4j.jar (required for SOAP mode) 
     * 19. xalan.jar (required for SOAP mode) 
     * 20. xbean.jar (required for SOAP mode) 
     * 21. xercesImpl.jar (required for SOAP mode) 
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
     * SOAP required JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/thirdparty 
     * 
     * If you want to invoke a remote forms server instance and there is a 
     * firewall between the client application and the server, then it is  
     * recommended that you use the SOAP mode. When using the SOAP mode,  
     * you have to include these additional JAR files 
     * 
     * For information about the SOAP  
     * mode, see "Setting connection properties" in Programming  
     * with AEM Forms 
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.livecycle.contentservices.client.impl.DocumentManagementServiceClientImpl; 
  
 public class CreateAssociationsSoap { 
  
     public static void main(String[] args) { 
          
         try{ 
          
             //Set connection properties required to invoke AEM Forms using SOAP mode                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a DocumentManagementServiceClientImpl object 
             DocumentManagementServiceClientImpl    docManager = new DocumentManagementServiceClientImpl(myFactory); 
              
             //Specify the input values  
             String storeName ="SpacesStore"; 
             String associationType = "{https://www.adobe.com/lc/datacapture/1.0}linkedBy"; 
             String aspect = "{https://www.adobe.com/lc/datacapture/1.0}linkable"; 
             String parentPath= "/Company Home/MortgageForm.pdf"; 
             String childPath= "/Company Home/Loan.xml"; 
                      
             //Set the linkable aspect to MortgageForm.pdf 
             List<String> aspectList = new ArrayList(); 
             aspectList.add(aspect); 
              
             //Create an attribute map 
             Map<String,Object> inputs = new HashMap<String,Object>(); 
              
             //Specify attributes that belong to the new content 
             String creator = "{https://www.alfresco.org/model/content/1.0}creator"; 
             String description = "{https://www.alfresco.org/model/content/1.0}description";  
              
             inputs.put(creator,"Tony Blue"); 
             inputs.put(description,"Link the PDF document to loan data"); 
              
             //Set the aspects 
             docManager.setContentAttributes(storeName,parentPath,aspectList,inputs); 
  
             //Create an association between MortgageForm.pdf and Loan.xml  
             docManager.createAssociation(storeName,  
                     associationType, 
                     parentPath, 
                     childPath);  
         } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 
```
