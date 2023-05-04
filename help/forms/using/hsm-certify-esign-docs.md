---
title: ドキュメントのデジタル署名や証明に HSM を使用する
seo-title: Use HSM to certify eSigned documents
description: HSM または eToken デバイスを使用して電子署名付きドキュメントを認証する
seo-description: Use HSM or etoken devices to certify eSigned documents
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
exl-id: ab5233dd-182e-4871-997f-b2142901bce7
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 41%

---

# ドキュメントのデジタル署名や証明に HSM を使用する {#use-hsm-to-digitally-sign-or-certify-documents}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ハードウェアセキュリティモジュール (HSM) と eToken は、専用の、堅牢な、改ざんに強いコンピューティングデバイスで、デジタルキーの安全な管理、処理、保存を目的として設計されています。 これらのデバイスは、コンピューターまたはネットワークサーバーに直接接続されます。

Adobe Experience Manager Formsは、HSM または eToken に保存された資格情報を使用して eSign を作成したり、ドキュメントにサーバー側のデジタル署名を適用したりできます。 AEM Forms 上で HSM または eToken デバイスを使用するには：

1. DocAssurance サービスを有効にします。
1. 証明書拡張機能のReaderを設定します。
1. AEM Web Console で HSM または eToken デバイスのエイリアスを作成します。
1. DocAssurance Service API を使用して、デバイスに保存されたデジタルキーでドキュメントに署名したり、ドキュメントの認証を行ったりします。

## AEM Forms で HSM または eToken デバイスを設定する前に {#configurehsmetoken}

* インストール [AEM Formsアドオン](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) パッケージ。
* AEMサーバーと同じコンピューターに HSM または eToken クライアントソフトウェアをインストールして設定します。 クライアントソフトウェアは、HSM および etoken デバイスと通信する必要があります。
* (Microsoft Windows のみ )JAVA_HOME_32 環境変数を設定し、32 ビット版の Java 8 Development Kit(JDK 8) がインストールされているディレクトリを指すようにします。 ディレクトリのデフォルトパスはC:\Program Files(x86)\Java\jdk です。&lt;version>
* (OSGi 上のAEM Formsのみ )Trust Store にルート証明書をインストールします。 これは、署名済み PDF の検証に必要です。

>[!NOTE]
>
>Microsoft Windows では、32 ビットの LunaSA または EToken クライアントのみがサポートされます。

## DocAssurance サービスを有効にする {#configuredocassurance}

デフォルトでは、DocAssurance サービスは有効になっていません。 このサービスを有効にするには、次の手順を実行します。

1. AEM Forms 環境のオーサーインスタンスを停止させます。

1. [AEM_root]\crx-quickstart\conf\sling.properties ファイルを開き、編集します。

   >[!NOTE]
   >
   >[AEM_root]\crx-quickstart\bin\start.bat ファイルを使用して AEM インスタンスを起動した場合は、[AEM_root]\crx-quickstart\sling.properties ファイルを開いて変更してください。

1. sling.properties ファイルに次のプロパティを追加（または書き換え）します。

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. sling.properties ファイルを保存して閉じます。
1. AEM インスタンスを再起動します。

## 証明書拡張機能のReaderを設定 {#set-up-certificates-for-reader-extensions}

証明書を設定するには、次の手順を実行します。

1. AEM オーサーインスタンスに管理者としてログインします。

1. グローバルナビゲーションバーで **Adobe Experience Manager** をクリックします。**ツール**／**セキュリティ**／**ユーザー**&#x200B;に移動します。
1. ユーザーアカウントの&#x200B;**名前**&#x200B;フィールドをクリックします。**ユーザー設定を編集**&#x200B;ページが開きます。
1. AEM オーサーインスタンスでは証明書がキーストアに存在します。キーストアをまだ作成していない場合は、**キーストアを作成**&#x200B;をクリックし、キーストアの新しいパスワードを設定してください。キーストアがサーバーに既に存在する場合は、このステップをスキップしてください。

1. **ユーザー設定を編集**&#x200B;ページで、**キーストアを管理**&#x200B;をクリックします。 

1. キーストアを管理ダイアログで、**秘密鍵をキーストアファイルから追加**&#x200B;オプションを展開し、エイリアスを指定してください。エイリアスは Reader Extensions の操作を実行する際に使用されます。
1. 証明書ファイルをアップロードするには、**キーストアファイルを選択**&#x200B;をクリックし、`.pfx` ファイルをアップロードします。
1. **キーストアのパスワード**、**秘密鍵のパスワード**、証明書に関連付けられている&#x200B;**秘密鍵エイリアス**&#x200B;を、各フィールドに追加します。「**送信**」をクリックします。

   >[!NOTE]
   >
   >証明書の&#x200B;**秘密鍵エイリアス**&#x200B;を決めるには、Java keytool コマンド（`keytool -list -v -keystore [keystore-file] -storetype pkcs12`）を使用することができます。

   >[!NOTE]
   >
   >**キーストアのパスワード**&#x200B;および&#x200B;**秘密鍵のパスワード**&#x200B;フィールドに、証明書ファイルとともに提供するパスワードを指定してください。

>[!NOTE]
>
>OSGi 上のAEM Formsで、署名済みPDFを検証するには、Trust Store にルート証明書がインストールされます。

>[!NOTE]
>
>実稼動環境に移行する際は、評価用の資格情報を実稼動用の資格情報に置き換えます。 期限切れの資格情報または評価用の資格情報を更新する前に、Reader Extensions の古い資格情報を削除してください。

## デバイスエイリアスの作成 {#configuredeviceinaemconsole}

エイリアスには、HSM または eToken に必要なすべてのパラメーターが含まれます。 eSign または Digital Signatures で使用する HSM または eToken 秘密鍵証明書ごとにエイリアスを作成するには、以下の手順を実行します。

1. AEMコンソールを開きます。 AEM コンソールのデフォルト URL は、https://&lt;host>:&lt;port>/system/console/configMgr です。
1. **HSM クレデンシャル設定サービス**&#x200B;を開き、次のフィールドに値を指定してください。

   * **Credential Alias**（クレデンシャルのエイリアス）：エイリアスを識別するための文字列を指定します。この値は、署名フィールドへの署名操作といった、Digital Signatures の一部の操作でプロパティとして使用されます。
   * **DLL パス**:サーバー上の HSM または eToken クライアントライブラリの完全修飾パスを指定します。 例：C:\Program Files\LunaSA\cryptoki.dll クラスター環境では、クラスター内のすべてのサーバーでこのパスが同じである必要があります。
   * **HSM PIN**：デバイスキーへのアクセスに必要なパスワードを指定します。
   * **HSM Slot Id**:整数型のスロット識別子を指定します。 スロット ID は、クライアントごとに設定されます。 2 台目のマシンを別のパーティション（同じ HSM デバイス上の HSMPART2 など）に登録した場合、スロット 1 はそのクライアントの HSMPART2 パーティションに関連付けられます。

   **注意：** *Etoken を設定する際に、「HSM Slot Id」フィールドに数値を指定します。 数値は、Signatures の操作を有効にするために必要です。*

   * **証明書 SHA1**:使用する秘密鍵証明書の公開鍵 (.cer) ファイルの SHA1 値（拇印）を指定します。 SHA1 値にスペースが使用されていないことを確認します。 物理証明書を使用している場合は、必須ではありません。
   * **HSM デバイスタイプ**：HSM（Luna など）または eToken デバイスの発行元を選択します。

   「**保存**」をクリックします。ハードウェアセキュリティモジュールは、AEM Forms用に設定されています。 これで、ハードウェアセキュリティモジュールをAEM Formsと共に使用して、ドキュメントの署名や認証を行うことができます。

## DocAssurance Service API を使用して、デバイスに保存されたデジタルキーでドキュメントに署名または証明を行います  {#programatically}

以下のサンプルコードでは、ドキュメントの署名や証明に HSM または etoken を使用しています。

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.IOException;
import java.io.InputStream;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * Digital signatures can be applied to PDF documents to provide a level of security. Digital signatures, like handwritten signatures, provide a means by which signers 
 * identify themselves and make statements about a document. The technology used to digitally sign documents helps to ensure that both the signer and recipients are clear 
 * about what was signed and confident that the document was not altered since it was signed.
 * 
 * PDF documents are signed by means of public-key technology. A signer has two keys: a public key and a private key. The private key is stored in a user's credential that 
 * must be available at the time of signing. The public key is stored in the user's certificate that must be available to recipients to validate the signature. Information
 * about revoked certificates is found in certificate revocation lists (CRLs) and Online Certificate Status Protocol (OCSP) responses distributed by Certificate Authorities (CAs). 
 * The time of signing can be obtained from a trusted source known as a Timestamping Authority.
 * 
 * The following Java code example digitally signs a PDF document that is based on a PDF file. 
 * The alias that is specified for the security credential is secure, and revocation checking is performed. 
 * Because no CRL or OCSP server information is specified, the server information is obtained from the certificate used to 
 * digitally sign the PDF document
 * 
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=Sign.class)
public class Sign{
 @Reference
 private DocAssuranceService docAssuranceService;
 
 @Reference
    private SlingRepository slingRepository;
 
 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  * 
  * @param inputFile - path to the pdf document stored at JCR node 
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void signExtend(String inputFile, String outputFile, String alias) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{
  
  Document inDoc = new Document(inputFile);
  Document outDoc = null;
  
  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {
          
          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);
             
             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //as we don't want encryption in this case, passing null for Encryption Options
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, null, getSignatureOptions(alias,resourceResolver),null,null);
        }
  catch(Exception e){
   e.printStackTrace();
  }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }
        
        //flush the output document contents to JCR Node
  flush(outDoc, outputFile);

 }
 
 /**
  * 
  * @param rr resource resolver corresponding to the user with the access to signing credential for the 
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(String alias, ResourceResolver rr){
  
  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();
  
  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);
  
  //field to sign
  String fieldName = "Signature1" ;

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;
        
        //Reason for signing/certifying
        String reason = "Test Reason";
        
        //location of the signer
        String location = "Test Location";
        
        //contact info of the signer
        String contactInfo = "Test Contact";
        
        //Create a PDFSignatureAppearanceOptions object 
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);
        
        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr, true));
  return signatureOptions;
 }
 
 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }
    
    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }
    
    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }
    
    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;
        
    }
    
    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");
        
        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver
        
        return unlockOptions;
        
    }
    /**
     * This method copies the data from {@code Document}, to the specified file at the given resourcePath.
     * @param doc
     * @param resourcePath
     * @throws IOException
     */
    private void flush(Document doc, String resourcePath) throws IOException {
   //extracts the byte data from Document
   byte[] output = doc.getInlineData();
   Binary opBin;
   Session adminSession = null;
      try {
         adminSession = slingRepository.loginAdministrative(null);
         
         //get access to the specific node
         //here we are assuming that node exists
           Node node = adminSession.getNode(resourcePath); 
          
           //convert byte[] to Binary
           opBin = adminSession.getValueFactory().createBinary((InputStream)new ByteArrayInputStream(output));
     
           //set the Binary data value to node's jcr:data
           node.getNode("jcr:content").getProperty("jcr:data").setValue(opBin);
      } catch (RepositoryException e) {

      }
      finally{
       
       if(adminSession != null && adminSession.isLive()){
        try {
      adminSession.save();
      adminSession.logout();
     } catch (RepositoryException e) {
      
     }
              
             }
      }
   
  }
}
```

AEM 6.0 Form またはAEM 6.1 Formsからアップグレードし、以前のバージョンで DocAssurance サービスを使用していた場合は、次のようになります。

* HSM や eToken デバイスを使用せずに DocAssurance サービスを使用する場合は、既存のコードを引き続き使用してください。
* DocAssurance サービスを HSM または etoken デバイスと共に使用するには、既存の CredentialContext オブジェクトコードを以下に示す API に置き換えます。

```java
/**
  * 
  * @param credentialAlias alias of the PKI Credential stored in CQ Key Store or 
  * the alias of the HSM Credential configured using HSM Credentials Configuration Service.      
  * @param resourceResolver corresponding to the user with the access to the key store and trust store.
  * @param isHSMCredential if the alias is corresponding to HSM Credential. 
  */
 public CredentialContext(String credentialAlias, ResourceResolver resourceResolver, boolean isHSMCredential);
```

DocAssurance サービスの API とサンプルコードについて詳しくは、 [AEM Document Services をプログラムで使用する](/help/forms/using/aem-document-services-programmatically.md).
