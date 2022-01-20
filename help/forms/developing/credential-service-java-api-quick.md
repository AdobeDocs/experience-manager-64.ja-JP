---
title: 資格情報サービス Java API QuickStart(SOAP)
seo-title: Credential Service Java API QuickStart(SOAP)
description: 資格情報サービス Java API を使用して、資格情報を読み込んだり、削除したりします。
seo-description: Use the Credential Service Java API to import and delete credentials.
uuid: a00eabfa-3a52-41dd-bcba-c60d00394384
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: b624e255-ae71-4d9c-8554-d48f3e77b799
role: Developer
exl-id: a81b2360-9d17-46c7-9443-51b366b0724a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 資格情報サービス Java API クイックスタート (SOAP) {#credential-service-java-api-quickstart-soap}

Credential サービスで Java API Quick Start(SOAP) を使用できます。

[クイックスタート（SOAP モード）:Java API を使用した資格情報の読み込み](credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[クイックスタート（SOAP モード）:Java API を使用した資格情報の削除](credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

AEM Formsの操作は、AEM Formsの厳密に型指定された API を使用して実行できます。接続モードは、SOAP に設定する必要があります。

>[!NOTE]
>
>「 AEM forms によるプログラミング」のクイックスタートは、JBoss および Windows オペレーティングシステムにデプロイされる FormsServer に基づいています。 ただし、Unix などの別のオペレーティングシステムを使用している場合は、Windows 固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。 同様に、別の J2EE アプリケーションサーバーを使用している場合は、有効な接続プロパティを指定する必要があります。 詳しくは、 [接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

>[!NOTE]
>
>Web サービスを使用して Credential サービスの操作を実行することはできません。

## クイックスタート（SOAP モード）:Java API を使用した資格情報の読み込み {#quick-start-soap-mode-importing-credentials-using-the-java-api}

次のコードの例では、という名前のファイルに基づいて秘密鍵証明書を読み込みます *cred.p12*. 秘密鍵証明書の読み込みに使用するエイリアスの値は、 `Secure`. ( [Trust Manager API を使用した資格情報の読み込み](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api).)

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-truststore-client.jar 
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
 import java.io.FileInputStream; 
 import java.util.Properties; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.truststore.client.CredentialServiceClient; 
  
 public class ImportCredentialSoap { 
      
     public static void main(String[] args) { 
            try { 
           
          //Set connection properties required to invoke AEM Forms using SOAP mode                                 
              Properties connectionProps = new Properties(); 
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
               
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
              
             //Create a CredentialServiceClient instance 
             CredentialServiceClient certClient = new CredentialServiceClient(myFactory); 
              
             //Reference a credential based on a P12 file 
             FileInputStream myCred = new FileInputStream("C:\\Adobe\cred.p12"); 
             Document credential = new Document(myCred); 
          
             //Create a string array to store usage values 
             String[] usage = new String[1]; 
             usage[0] = "truststore.usage.type.sign"; 
              
             //Import the credential 
             certClient.importCredential("secure",credential,"password",usage); 
             System.out.println("Credential was uploaded"); 
      
            }catch (Exception e) { 
                e.printStackTrace(); 
            } 
      
            } 
 } 
  
  
 
```

## クイックスタート（SOAP モード）:Java API を使用した資格情報の削除 {#quick-start-soap-mode-deleting-credentials-using-the-java-api}

次のコードの例では、エイリアス値に基づいて秘密鍵証明書を削除します *secure*. ( [Trust Manager API を使用した資格情報の削除](/help/forms/developing/credentials.md#deleting-credentials-by-using-the-trust-manager-api).)

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-truststore-client.jar 
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
  
 import java.util.Properties; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.truststore.client.CredentialServiceClient; 
  
 public class DeleteCertificateSoap { 
  
      
     public static void main(String[] args)  
     { 
     try { 
           
         //Set connection properties required to invoke AEM Forms using SOAP mode                                 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
  
         //Create a ServiceClientFactory object 
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
          
         //Create a CredentialServiceClient instance 
         CredentialServiceClient certClient = new CredentialServiceClient(myFactory); 
          
         //Delete the certificate 
         certClient.deleteCredential("secure"); 
         System.out.println("Credential was deleted"); 
      
        }catch (Exception e) { 
            e.printStackTrace(); 
        } 
      
        } 
  
 } 
 
```
