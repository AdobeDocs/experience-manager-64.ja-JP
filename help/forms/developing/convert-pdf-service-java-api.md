---
title: Convert PDF サービス Java API クイックスタート（SOAP）
seo-title: Convert PDF Service Java API QuickStart(SOAP)
description: ConvertPDFサービス Java API を使用して、PDFドキュメントを PostScript およびJPEGファイルに変換します。
seo-description: Use the Convert PDF service Java API to convert a PDF document to PostScript and JPEG files.
uuid: 97253ac7-f0c1-4766-a7bd-c19af52adf51
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: bdd9bb56-14f6-448b-be4a-7c11f670e901
role: Developer
exl-id: af0cb623-c29c-4b9e-9ffd-736047a45b8d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 79%

---

# Convert PDF サービス Java API クイックスタート（SOAP） {#convert-pdf-service-java-api-quickstart-soap}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Convert PDF サービス API では、次のクイックスタートを使用できます。

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントの PostScript への変換](convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントの JPEG ファイルへの変換](convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

AEM Forms の操作は、AEM Forms の厳密に型指定された API を使用して実行できます。接続モードは、SOAP に設定する必要があります。

>[!NOTE]
>
>AEM Forms によるプログラミングにあるクイックスタートは、JBoss Application Server とMicrosoft Windows オペレーティングシステムにデプロイされる Forms Server に基づいています。ただし、UNIX などの別のオペレーティングシステムを使用している場合は、Windows 固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。同様に、別の J2EE アプリケーションサーバーを使用している場合は、有効な接続プロパティを必ず指定してください。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照）。

## クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントの PostScript への変換 {#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api}

次のコード例では、*Loan.pdf* という PDF ドキュメントを *Loan.ps* という PostScript ドキュメントに変換します。（[PDF ドキュメントを PostScript に変換](/help/forms/developing/converting-pdf-postscript-image-files.md#converting-pdf-documents-to-postscript)を参照。）

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-convertpdf-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. activation.jar (required for SOAP mode) 
     * 5. axis.jar (required for SOAP mode) 
     * 6. commons-codec-1.3.jar (required for SOAP mode) 
     * 7.  commons-collections-3.1.jar  (required for SOAP mode) 
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
 import java.io.FileInputStream; 
 import java.util.Properties; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.livecycle.convertpdfservice.client.ConvertPdfServiceClient; 
 import com.adobe.livecycle.convertpdfservice.client.ToPSOptionsSpec; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.Color; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.LineWeight; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.PSLevel; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.PageSize; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.Color; 
  
 public class JavaAPIConvertPDFtoPSSOAP 
 { 
     public static void main(String[] args) 
     { 
     try 
         { 
         //Set connection properties required to invoke AEM Forms using SOAP mode                                 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
         //Create a ServiceClientFactory object 
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
          
         //Create a ConvertPdfServiceClient object 
         ConvertPdfServiceClient convertPDFClient= new ConvertPdfServiceClient(myFactory); 
  
         //Get a PDF file document to convert to a PS document  
         //and populate a com.adobe.idp.Document object 
         String inputFileName = "C:\\Adobe\Loan.pdf"; 
         FileInputStream fileInputStream = new FileInputStream(inputFileName); 
         Document inDoc = new Document(fileInputStream); 
          
         //Create a ToPSOptionsSpec object that defines run-time options 
         ToPSOptionsSpec psSpec = new ToPSOptionsSpec();  
         psSpec.setPsLevel(PSLevel.LEVEL_3); 
         psSpec.setShrinkToFit(true); 
         psSpec.setPageSize(PageSize.A4); 
         psSpec.setRotateAndCenter(true); 
         psSpec.setColor(Color.compositeGray); 
         psSpec.setLineWeight(LineWeight.point25); 
          
         //Convert the PDF document to a PostScript file 
         Document createdDocument =convertPDFClient.toPS2( 
             inDoc, 
             psSpec 
             ); 
  
         //Save the PostScript file 
         createdDocument.copyToFile(new File("C:\\Adobe\Loan.ps")); 
         } 
     catch (Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 }
```

## クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントの JPEG ファイルへの変換 {#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api}

次の Java コード例では、*Loan.pdf* という PDF ドキュメントを一連の JPEG ファイルに変換して、C:\Adobe ディレクトリに格納します。各ファイルの名前は *tempFile[index].jpg*（最初の画像ファイルの名前はです） *tempFile0.jpg*. （[PDF ドキュメントを画像形式に変換](/help/forms/developing/converting-pdf-postscript-image-files.md#converting-pdf-documents-to-image-formats)を参照。）

```as3
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-convertpdf-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. activation.jar (required for SOAP mode) 
     * 5. axis.jar (required for SOAP mode) 
     * 6. commons-codec-1.3.jar (required for SOAP mode) 
     * 7.  commons-collections-3.1.jar  (required for SOAP mode) 
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
 import java.io.FileInputStream; 
 import java.util.Iterator; 
 import java.util.List; 
 import java.util.Properties; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.livecycle.convertpdfservice.client.ConvertPdfServiceClient; 
 import com.adobe.livecycle.convertpdfservice.client.ToImageOptionsSpec; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.CMYKPolicy; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.ColorCompression; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.ColorSpace; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.GrayScaleCompression; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.GrayScalePolicy; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.ImageConvertFormat; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.Interlace; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.JPEGFormat; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.MonochromeCompression; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.PNGFilter; 
 import com.adobe.livecycle.convertpdfservice.client.enumeration.RGBPolicy; 
  
 public class JavaAPIConvertPDFtoImageSOAP { 
  
     public static void main(String[] args) 
     { 
     try 
     { 
         //Set connection properties required to invoke AEM Forms using SOAP mode                                 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://[server]:[port]"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
         //Create a ServiceClientFactory object 
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
         //Create the ConvertPDF service client 
         ConvertPdfServiceClient serviceClient = new ConvertPdfServiceClient(myFactory); 
          
         //Get a PDF file document to convert to a JPEG document and populate a com.adobe.idp.Document object 
         String inputFileName = "C:\\Adobe\Loan.pdf"; 
         FileInputStream fileInputStream = new FileInputStream(inputFileName); 
         Document inDoc = new Document(fileInputStream); 
  
         // Set up the runtime options for the new JPEG file to be created 
         ToImageOptionsSpec spec = new ToImageOptionsSpec(); 
         spec.setImageConvertFormat(ImageConvertFormat.JPEG); 
         spec.setGrayScaleCompression(GrayScaleCompression.Low); 
         spec.setColorCompression(ColorCompression.Low); 
         spec.setFormat(JPEGFormat.BaselineOptimized); 
         spec.setRgbPolicy(RGBPolicy.Off); 
         spec.setCmykPolicy(CMYKPolicy.Off); 
         spec.setColorSpace(ColorSpace.RGB); 
         spec.setResolution("72"); 
         spec.setMonochrome(MonochromeCompression.None); 
         spec.setFilter(PNGFilter.Sub); 
         spec.setInterlace(Interlace.Adam7); 
         spec.setTileSize(180); 
         spec.setGrayScalePolicy(GrayScalePolicy.Off); 
          
         //Perform the conversion and get the containing the newly created JPEG files 
         List allImages = serviceClient.toImage2( 
             inDoc, 
             spec 
         ); 
          
         //Create an Iterator object and iterate through  
         //the List object to get all images 
         Iterator iter = allImages.iterator();  
         int i = 0 ;  
         while (iter.hasNext()) {  
             Document file = (Document)iter.next();  
             file.copyToFile(new File("C:\\Adobe\tempFile"+i+".jpg")); 
             i++;  
         } 
     } 
     catch (Exception e) { 
         e.printStackTrace(); 
         } 
     } 
 }
```
