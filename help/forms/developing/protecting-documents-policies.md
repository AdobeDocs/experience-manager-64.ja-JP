---
title: ポリシーを使用したドキュメントの保護
seo-title: Protecting Documents with Policies
description: Document Security サービスを使用すると、機密設定をAdobe PDFドキュメントに動的に適用し、ドキュメントを制御できます。 また、Document Security サービスを使用すると、ユーザーは、ポリシーで保護されたPDFドキュメントを受信者が使用する方法を制御できます。
seo-description: Use the Document Security service to dynamically apply confidentiality settings to Adobe PDF documents and to maintain control over the documents. The Document Security service also enables the users to maintain control over how recipients use the policy-protected PDF document.
uuid: 6feb69ef-7b61-4d0b-8c87-d65d98bae9b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: 9b1d2bf3-f28c-41b2-9026-1f3311556422
role: Developer
exl-id: 88065c4d-8ca9-4dfb-8663-ac8772e5e556
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '15500'
ht-degree: 4%

---

# ポリシーを使用したドキュメントの保護 {#protecting-documents-with-policies}

**Document Security Service について**

Document Security サービスを使用すると、ユーザーは、Adobe PDFドキュメントに機密設定を動的に適用し、ドキュメントの配布範囲に関わらず、そのドキュメントを制御できます。

Document Security サービスは、ポリシーで保護されたPDFドキュメントを受信者がどのように使用するかをユーザーが管理できるようにすることで、ユーザーの手の届かない範囲で情報が広がるのを防ぎます。 ユーザーは、ドキュメントを開くユーザーを指定し、ドキュメントの使用方法を制限し、配布後にドキュメントを監視できます。 また、ユーザーは、ポリシーで保護されたドキュメントへのアクセスを動的に制御し、ドキュメントへのアクセスを動的に取り消すこともできます。

また、Document Security サービスは、Microsoft Word ファイル（DOC ファイル）などの他のファイルタイプも保護します。 Document Security Client API を使用して、これらのファイルタイプを操作できます。 次のバージョンがサポートされています。

* Microsoft Office 2003 ファイル（DOC、XLS、PPT ファイル）
* Microsoft Office 2007 ファイル（DOCX、XLSX、PPTX ファイル）
* PTC Pro/E ファイル

次の 2 つのセクションで、Word ドキュメントの使用方法を説明します。

* [Word ドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-word-documents)
* [Word ドキュメントからポリシーを削除する](protecting-documents-policies.md#removing-policies-from-word-documents)

Document Security サービスを使用して、次のタスクを実行できます。

* ポリシーの作成. 詳しくは、 [ポリシーの作成](protecting-documents-policies.md#creating-policies).
* ポリシーを変更します。 詳しくは、 [ポリシーの変更](protecting-documents-policies.md#modifying-policies).
* ポリシーを削除します。 詳しくは、 [ポリシーの削除](protecting-documents-policies.md#deleting-policies).
* ポリシーをPDF・ドキュメントに適用 詳しくは、 [ポリシー・ドキュメントへのPDFの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents).
* ポリシードキュメントからPDFを削除します。 詳しくは、 [ポリシー・ドキュメントからのPDFの削除](protecting-documents-policies.md#removing-policies-from-pdf-documents).
* Inspectのポリシーで保護されたドキュメント。 詳しくは、 [ポリシーで保護されたPDF文書の検査](protecting-documents-policies.md#inspecting-policy-protected-pdf-documents).
* PDFドキュメントへのアクセスを取り消します。 詳しくは、 [ドキュメントへのアクセスの取り消し](protecting-documents-policies.md#revoking-access-to-documents).
* 取り消されたドキュメントへのアクセス権を回復します。 詳しくは、 [取り消されたドキュメントへのアクセスの回復](protecting-documents-policies.md#reinstating-access-to-revoked-documents).
* 透かしを作成する。 詳しくは、 [透かしの作成](protecting-documents-policies.md#creating-watermarks).
* イベントを検索します。 詳しくは、 [イベントの検索](protecting-documents-policies.md#searching-for-events).

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

## ポリシーの作成 {#creating-policies}

Document Security Java API または Web サービス API を使用して、プログラムでポリシーを作成できます。 A *ポリシー* は、Document Security の設定、許可されたユーザー、使用権限などの情報を集めたものです。 様々な状況やユーザーに適したセキュリティ設定を使用して、任意の数のポリシーを作成および保存できます。

ポリシーを使用すると、次のタスクを実行できます。

* ドキュメントを開くことのできる個人を指定します。 受信者は、所属することも、組織の外部に属することもできます。
* 受信者によるドキュメントの使用方法を指定します。 AcrobatとAdobe Readerの様々な機能へのアクセスを制限できます。 これらの機能には、テキストの印刷とコピー、署名の追加、ドキュメントへのコメントの追加機能が含まれます。
* ポリシーで保護されたドキュメントを配布した後でも、いつでもアクセスおよびセキュリティ設定を変更できます。
* ドキュメントを配布した後で、ドキュメントの使用を監視します。 ドキュメントがどのように使用され、誰が使用しているかを確認できます。 例えば、誰かがドキュメントを開いた日時を調べることができます。

### Web サービスを使用したポリシーの作成 {#creating-a-policy-using-web-services}

Web サービス API を使用してポリシーを作成する場合は、そのポリシーを記述する既存の Portable Document Rights Language(PDRL)XML ファイルを参照します。 ポリシー権限とプリンシパルは、 PDRL ドキュメントで定義されます。 次の XML ドキュメントは、PDRL ドキュメントの一例です。

```as3
 <?xml version="1.0" encoding="UTF-8" standalone="yes"?> 
 <Policy PolicyInstanceVersion="1" PolicyID="5DA3F847-DE76-F9CC-63EA-49A8D59154DE" PolicyCreationTime="2004-08-30T00:02:28.294+00:00" PolicyType="1" PolicySchemaVersion="1.0" PolicyName="SDK Test Policy -4344050357301573237" PolicyDescription="An SDK Test policy" xmlns="https://www.adobe.com/schema/1.0/pdrl"> 
       <PolicyEntry> 
          <ns1:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns1="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
  
          <ns2:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns2="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
  
          <ns3:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns3="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
  
          <ns4:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns4="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
          <Principal PrincipalNameType="SYSTEM"> 
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain> 
  
             <PrincipalName>all_internal_users</PrincipalName> 
          </Principal> 
       </PolicyEntry> 
       <PolicyEntry> 
          <ns5:Permission PermissionName="com.adobe.aps.onlineOpen" Access="ALLOW" xmlns:ns5="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
  
          <ns6:Permission PermissionName="com.adobe.aps.offlineOpen" Access="ALLOW" xmlns:ns6="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
  
          <ns7:Permission PermissionName="com.adobe.aps.pdf.copy" Access="ALLOW" xmlns:ns7="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
  
          <ns8:Permission PermissionName="com.adobe.aps.pdf.printLow" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns8="https://www.adobe.com/schema/1.0/pdrl" /> 
  
          <ns9:Permission PermissionName="com.adobe.aps.policySwitch" Access="ALLOW" xmlns:ns9="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
  
          <ns10:Permission PermissionName="com.adobe.aps.revoke" Access="ALLOW" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" xmlns:ns10="https://www.adobe.com/schema/1.0/pdrl" /> 
  
          <ns11:Permission PermissionName="com.adobe.aps.pdf.edit" Access="ALLOW" xmlns:ns11="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
  
          <ns12:Permission PermissionName="com.adobe.aps.pdf.editNotes" Access="ALLOW" xmlns:ns12="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
  
          <ns13:Permission PermissionName="com.adobe.aps.pdf.fillAndSign" Access="ALLOW" xmlns:ns13="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
  
          <ns14:Permission PermissionName="com.adobe.aps.pdf.printHigh" Access="ALLOW" xmlns:ns14="https://www.adobe.com/schema/1.0/pdrl" xmlns="https://www.adobe.com/schema/1.0/pdrl-ex" /> 
  
          <Principal PrincipalNameType="SYSTEM"> 
             <PrincipalDomain>EDC_SPECIAL</PrincipalDomain> 
  
             <PrincipalName>publisher</PrincipalName> 
          </Principal> 
       </PolicyEntry> 
  
       <OfflineLeasePeriod> 
          <Duration>P31D</Duration> 
       </OfflineLeasePeriod> 
  
       <AuditSettings isTracked="true" /> 
  
       <PolicyValidityPeriod isAbsoluteTime="false"> 
          <ValidityPeriodRelative> 
             <NotBeforeRelative>PT0S</NotBeforeRelative> 
  
             <NotAfterRelative>P20D</NotAfterRelative> 
          </ValidityPeriodRelative> 
       </PolicyValidityPeriod> 
 </Policy> 
 
```

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

ポリシーを作成するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Document Security クライアント API オブジェクトを作成します。
1. ポリシーの属性を設定します。
1. ポリシーエントリを作成します。
1. ポリシーを登録します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-rightsmanagement-client.jar
* namespace.jar (AEM Formsが JBoss にデプロイされている場合 )
* jaxb-api.jar(AEM Formsが JBoss にデプロイされている場合 )
* jaxb-impl.jar(AEM Formsが JBoss にデプロイされている場合 )
* jaxb-libs.jar(AEM Formsが JBoss にデプロイされている場合 )
* jaxb-xjc.jar(AEM Formsが JBoss にデプロイされている場合 )
* relaxingDatatype.jar(AEM Formsが JBoss にデプロイされている場合 )
* xsdlib.jar(AEM Formsが JBoss にデプロイされている場合 )
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar
* jbossall-client.jar(AEM Formsが JBoss にデプロイされていない場合は、別の JAR ファイルを使用 )

これらの JAR ファイルの場所について詳しくは、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成します。

**ポリシーの属性を設定します**

ポリシーを作成するには、ポリシー属性を設定します。 必須属性は、ポリシー名です。 ポリシー名は、ポリシーセットごとに一意である必要があります。 ポリシーセットは、単にポリシーの集まりです。 ポリシーが別々のポリシーセットに属している場合は、同じ名前の 2 つのポリシーを使用できます。 ただし、1 つのポリシーセット内の 2 つのポリシーが同じポリシー名を持つことはできません。

もう 1 つの有効な属性は、有効期間です。 有効期間とは、権限を持つ受信者がポリシーで保護されたドキュメントにアクセスできる期間を指します。 この属性を設定しない場合、ポリシーは常に有効です。

有効期間は、次のいずれかのオプションに設定できます。

* ドキュメントが公開されてからドキュメントにアクセスできる日数
* ドキュメントにアクセスできない終了日
* ドキュメントにアクセスできる特定の日付範囲
* 常に有効

開始日のみを指定できます。指定した日付を指定した場合、ポリシーは開始日より後に有効になります。 終了日のみを指定した場合、ポリシーは終了日まで有効です。 ただし、開始日と終了日の両方が定義されていない場合は、例外が発生します。

ポリシーに属する属性を設定する場合は、暗号化設定も設定できます。 これらの暗号化設定は、ポリシーがドキュメントに適用される際に影響を受けます。 次の暗号化値を指定できます。

* **AES256**:256 ビットキーを持つ AES 暗号化アルゴリズムを表します。
* **AES128**:128 ビットキーを持つ AES 暗号化アルゴリズムを表します。
* **暗号化なし：** 暗号化を表しません。

を指定する場合、 `NoEncryption` オプションを選択した場合、 `PlaintextMetadata` 選択肢 `false`. その場合は、例外が発生します。

>[!NOTE]
>
>設定可能なその他の属性については、 `Policy` インターフェイスの説明 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**ポリシーエントリを作成する**

ポリシーエントリは、プリンシパル（グループとユーザー、および権限）をポリシーに添付します。 ポリシーには少なくとも 1 つのポリシーエントリが必要です。 例えば、次のタスクを実行したとします。

* ポリシーエントリを作成して登録します。このエントリを使用すると、グループはオンライン状態でドキュメントのみを表示でき、受信者はドキュメントをコピーできなくなります。
* ポリシーにポリシーエントリを添付します。
* Acrobatを使用して、ポリシーでドキュメントを保護します。

これらのアクションを実行すると、受信者はドキュメントをオンラインで表示するだけで、コピーできなくなります。 ドキュメントからセキュリティが削除されるまで、ドキュメントは安全なままです。

**ポリシーを登録**

新しいポリシーを使用するには、そのポリシーを登録する必要があります。 ポリシーを登録した後は、そのポリシーを使用してドキュメントを保護できます。

### Java API を使用したポリシーの作成 {#create-a-policy-using-the-java-api}

Document Security API(Java) を使用してポリシーを作成します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーの属性を設定します。

   * の作成 `Policy` を呼び出すことによってオブジェクトを取得 `InfomodelObjectFactory` オブジェクトの静的 `createPolicy` メソッド。 このメソッドは、 `Policy` オブジェクト。
   * を呼び出して、ポリシーの名前属性を設定します。 `Policy` オブジェクトの `setName` メソッドを使用し、ポリシー名を指定する string 値を渡す。
   * を呼び出して、ポリシーの説明を設定します。 `Policy` オブジェクトの `setDescription` メソッドを使用して、ポリシーの説明を指定する string 値を渡すことができます。
   * を呼び出して、新しいポリシーが属するポリシーセットを設定します。 `Policy` オブジェクトの `setPolicySetName` メソッドを使用し、ポリシーセット名を指定する string 値を渡す。 ( `null` を返します。 *マイポリシー* ポリシーセット )
   * を呼び出して、ポリシーの有効期間を作成します。 `InfomodelObjectFactory` オブジェクトの静的 `createValidityPeriod` メソッド。 このメソッドは、 `ValidityPeriod` オブジェクト。
   * ポリシーで保護されたドキュメントにアクセスできる日数を、 `ValidityPeriod` オブジェクトの `setRelativeExpirationDays` メソッドを使用し、日数を指定する整数値を渡す方法と方法。
   * を呼び出して、ポリシーの有効期間を設定します。 `Policy` オブジェクトの `setValidityPeriod` メソッドおよび `ValidityPeriod` オブジェクト。

1. ポリシーエントリを作成します。

   * を呼び出してポリシーエントリを作成する `InfomodelObjectFactory` オブジェクトの静的 `createPolicyEntry` メソッド。 このメソッドは、 `PolicyEntry` オブジェクト。
   * を呼び出して、ポリシーの権限を指定します。 `InfomodelObjectFactory` オブジェクトの静的 `createPermission` メソッド。 に属する静的データメンバーを渡す `Permission` 権限を表すインターフェイス。 このメソッドは、 `Permission` オブジェクト。 例えば、ポリシーで保護されたPDF・ドキュメントからのデータのコピーをユーザーに許可する権限を追加するには、 `Permission.COPY`. （追加する権限ごとに、この手順を繰り返します）。
   * を呼び出して、ポリシーエントリに権限を追加します。 `PolicyEntry` オブジェクトの `addPermission` メソッドおよび `Permission` オブジェクト。 ( この手順を各 `Permission` 作成したオブジェクト )。
   * を呼び出して、ポリシープリンシパルを作成します。 `InfomodelObjectFactory` オブジェクトの静的 `createSpecialPrincipal` メソッド。 に属するデータメンバーを渡す `InfomodelObjectFactory` プリンシパルを表すオブジェクト。 このメソッドは、 `Principal` オブジェクト。 例えば、ドキュメントのパブリッシャーをプリンシパルとして追加するには、 `InfomodelObjectFactory.PUBLISHER_PRINCIPAL`.
   * を呼び出して、プリンシパルをポリシーエントリに追加します。 `PolicyEntry` オブジェクトの `setPrincipal`メソッドおよび `Principal` オブジェクト。
   * を呼び出して、ポリシーにポリシーエントリを追加します。 `Policy` オブジェクトの `addPolicyEntry` メソッドおよび `PolicyEntry` オブジェクト。

1. ポリシーを登録します。

   * の作成 `PolicyManager` を呼び出すことによってオブジェクトを取得 `DocumentSecurityClient` オブジェクトの `getPolicyManager` メソッド。
   * を呼び出して、ポリシーを登録します。 `PolicyManager` オブジェクトの `registerPolicy` メソッドを使用して、次の値を渡します。

      * この `Policy` 登録するポリシーを表すオブジェクト。
   * ポリシーが属するポリシーセットを表す string 値です。

   接続設定でAEM forms 管理者アカウントを使用して `DocumentSecurityClient` オブジェクトを選択し、 `registerPolicy` メソッド。 次の `null` ポリシーセットの値。ポリシーは管理者に作成されます *マイポリシー* ポリシーセット。

   接続設定内で Document Security ユーザーを使用する場合は、次のオプションを指定して `registerPolicy` ポリシーのみを受け入れるメソッド。 つまり、ポリシーセット名を指定する必要はありません。 ただし、ポリシーは、 *マイポリシー*. このポリシーセットに新しいポリシーを追加しない場合は、 `registerPolicy` メソッド。

   >[!NOTE]
   >
   >ポリシーを作成する場合は、既存のポリシーセットを参照します。 存在しないポリシーセットを指定すると、例外が発生します。

Document Security サービスを使用するコード例については、次を参照してください。

* 「クイックスタート（SOAP モード）:Java API を使用したポリシーの作成»

### Web サービス API を使用してポリシーを作成する {#create-a-policy-using-the-web-service-api}

Document Security API（Web サービス）を使用してポリシーを作成します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security Client API オブジェクトを作成します。

   * の作成 `DocumentSecurityServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `RightsManagementServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. ポリシーの属性を設定します。

   * コンストラクタを使用して `PolicySpec` オブジェクトを作成します。
   * ポリシーの名前を設定するには、 `PolicySpec` オブジェクトの `name` データメンバー。
   * ポリシーの説明を設定するには、 `PolicySpec` オブジェクトの `description` データメンバー。
   * ポリシーが属するポリシーセットを設定するには、 `PolicySpec` オブジェクトの `policySetName` データメンバー。 既存のポリシーセット名を指定する必要があります。 ( `null` を返します。 *マイポリシー*.)
   * ポリシーのオフラインリース期間を設定するには、 `PolicySpec` オブジェクトの `offlineLeasePeriod` データメンバー。
   * を `PolicySpec` オブジェクトの `policyXml` PDRL XML データを表す string 値を持つデータメンバー。 このタスクを実行するには、.NET を作成します。 `StreamReader` オブジェクトを指定します。 ポリシーを表す PDRL XML ファイルの場所を `StreamReader` コンストラクタ。 次に、 `StreamReader` オブジェクトの `ReadLine` メソッドを使用して戻り値を文字列変数に割り当てます。 反復処理 `StreamReader` オブジェクトを `ReadLine` メソッドは null を返します。 文字列変数を `PolicySpec` オブジェクトの `policyXml` データメンバー。

1. ポリシーエントリを作成します。

   Document Security Web サービス API を使用してポリシーを作成する場合は、ポリシーエントリを作成する必要はありません。 ポリシーエントリは、 PDRL ドキュメントで定義されます。

1. ポリシーを登録します。

   を呼び出して、ポリシーを登録します。 `DocumentSecurityServiceClient` オブジェクトの `registerPolicy` メソッドを使用して、次の値を渡します。

   * この `PolicySpec` 登録するポリシーを表すオブジェクト。
   * ポリシーが属するポリシーセットを表す string 値です。 次の項目を指定できます。 `null` の値を指定すると、ポリシーが *マイポリシー* ポリシーセット。

   接続設定でAEM forms 管理者アカウントを使用して `DocumentSecurityClient` オブジェクトの場合は、 `registerPolicy` メソッド。

   接続設定内で Document SecurityDocument Security ユーザーを使用する場合は、オーバーロードされた `registerPolicy` ポリシーのみを受け入れるメソッド。 つまり、ポリシーセット名を指定する必要はありません。 ただし、ポリシーは、 *マイポリシー*. このポリシーセットに新しいポリシーを追加しない場合は、 `registerPolicy` メソッド。

   >[!NOTE]
   >
   >ポリシーを作成し、ポリシーセットを指定する場合は、既存のポリシーセットを必ず指定してください。 存在しないポリシーセットを指定すると、例外が発生します。

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したポリシーの作成»
* クイックスタート (SwaRef):Web サービス API を使用したポリシーの作成»

## ポリシーの変更 {#modifying-policies}

既存のポリシーは、Document Security Java API または Web サービス API を使用して変更できます。 既存のポリシーを変更するには、そのポリシーを取得し、変更してから、サーバー上のポリシーを更新します。 例えば、既存のポリシーを取得し、その有効期間を延長したとします。 変更を有効にする前に、ポリシーを更新する必要があります。

ビジネス要件が変更され、ポリシーがこれらの要件を反映しなくなった場合は、ポリシーを変更できます。 新しいポリシーを作成する代わりに、既存のポリシーを更新するだけで済みます。

Web サービスを使用してポリシー属性を変更するには（例えば、JAX-WS で作成された Java プロキシクラスを使用）、ポリシーが Document Security サービスに登録されていることを確認する必要があります。 その後、 `PolicySpec.getPolicyXml` メソッドを使用してポリシー属性を編集し、該当するメソッドを使用して変更します。 たとえば、 `PolicySpec.setOfflineLeasePeriod` メソッド。

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

既存のポリシーを変更するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. 既存のポリシーを取得します。
1. ポリシー属性を変更します。
1. ポリシーを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成する必要があります。 Java API を使用している場合は、 `RightsManagementClient` オブジェクト。 Document Security Web サービス API を使用している場合は、 `RightsManagementServiceService` オブジェクト。

**既存のポリシーの取得**

既存のポリシーを変更するには、そのポリシーを取得する必要があります。 ポリシーを取得するには、ポリシー名とポリシーが属するポリシーセットを指定します。 次を指定した場合、 `null` ポリシーセット名の値。ポリシーは *マイポリシー* ポリシーセット。

**ポリシーの属性を設定します**

ポリシーを変更するには、ポリシー属性の値を変更します。 変更できない唯一の policy 属性は name 属性です。 たとえば、ポリシーのオフラインリース期間を変更するには、ポリシーのオフラインリース期間属性の値を変更します。

Web サービスを使用してポリシーのオフラインリース期間を変更する場合、 `offlineLeasePeriod` フィールド `PolicySpec` インターフェイスは無視されます。 オフラインリース期間を更新するには、 `OfflineLeasePeriod` 要素を含める必要があります。 次に、 `PolicySpec` インターフェイスの `policyXML` データメンバー。

>[!NOTE]
>
>設定可能なその他の属性については、 `Policy` インターフェイスの説明 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**ポリシーを更新します**

ポリシーに対して行った変更を反映する前に、Document Security サービスを使用してポリシーを更新する必要があります。 ドキュメントを保護するポリシーに対する変更は、ポリシーで保護されたドキュメントが次回 Document Security サービスと同期されたときに更新されます。

### Java API を使用した既存のポリシーの変更 {#modify-existing-policies-using-the-java-api}

Document Security API(Java) を使用して既存のポリシーを変更します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 既存のポリシーを取得します。

   * の作成 `PolicyManager` を呼び出すことによってオブジェクトを取得 `RightsManagementClient` オブジェクトの `getPolicyManager` メソッド。
   * の作成 `Policy` を呼び出して更新するポリシーを表すオブジェクト `PolicyManager` オブジェクトの `getPolicy` メソッドを使用して次の値を渡す»

      * ポリシーが属するポリシーセット名を表す string 値です。 次を指定できます。 `null` 結果は `MyPolicies` 使用されているポリシーセットです。
      * ポリシー名を表す string 値です。

1. ポリシーの属性を設定します。

   ビジネス要件に合わせてポリシーの属性を変更します。 たとえば、ポリシーのオフラインリース期間を変更するには、 `Policy` オブジェクトの `setOfflineLeasePeriod` メソッド。

1. ポリシーを更新します。

   を呼び出してポリシーを更新する `PolicyManager` オブジェクトの `updatePolicy` メソッド。 パス `Policy` 更新するポリシーを表すオブジェクト。

**コード例**

Document Security サービスを使用するコード例については、クイックスタート（SOAP モード）を参照してください。「Java API」セクションを使用してポリシーを変更する。

### Web サービス API を使用して既存のポリシーを変更する {#modify-existing-policies-using-the-web-service-api}

Document Security API（Web サービス）を使用して既存のポリシーを変更します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security クライアント API オブジェクトを作成します。

   * の作成 `RightsManagementServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `RightsManagementServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `RightsManagementServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. 既存のポリシーを取得します。

   の作成 `PolicySpec` を呼び出して変更するポリシーを表すオブジェクト `RightsManagementServiceClient` オブジェクトの `getPolicy` メソッドを使用して、次の値を渡します。

   * ポリシーが属するポリシーセット名を指定する string 値です。 次を指定できます。 `null` 結果は `MyPolicies` 使用されているポリシーセットです。
   * ポリシーの名前を指定する string 値です。

1. ポリシーの属性を設定します。

   ビジネス要件に合わせてポリシーの属性を変更します。

1. ポリシーを更新します。

   を呼び出してポリシーを更新する `RightsManagementServiceClient` オブジェクトの `updatePolicyFromSDK` メソッドおよび `PolicySpec` 更新するポリシーを表すオブジェクト。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したポリシーの変更»
* クイックスタート (SwaRef):Web サービス API を使用したポリシーの変更»

## ポリシーの削除 {#deleting-policies}

既存のポリシーは、Document Security Java API または Web サービス API を使用して削除できます。 ポリシーを削除すると、そのポリシーをドキュメントの保護に使用できなくなります。 ただし、ポリシーを使用している既存のポリシーで保護されたドキュメントは、引き続き保護されます。 新しいポリシーが利用可能になったら、ポリシーを削除できます。

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

既存のポリシーを削除するには、次の手順に従います。

1. プロジェクトファイルを含める
1. Document Security Client API オブジェクトを作成します。
1. ポリシーを削除します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成する必要があります。 Java API を使用している場合は、 `RightsManagementClient` オブジェクト。 Document Security Web サービス API を使用している場合は、 `RightsManagementServiceService` オブジェクト。

**ポリシーを削除**

ポリシーを削除するには、削除するポリシーと、そのポリシーが属するポリシーセットを指定します。 AEM Formsの呼び出しに設定を使用するユーザーは、ポリシーを削除する権限が必要です。それ以外の場合は、例外が発生します。 同様に、存在しないポリシーを削除しようとすると、例外が発生します。

### Java API を使用したポリシーの削除 {#delete-policies-using-the-java-api}

Document Security API(Java) を使用してポリシーを削除します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。

1. Document Security クライアント API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーを削除します。

   * の作成 `PolicyManager` を呼び出すことによってオブジェクトを取得 `RightsManagementClient` オブジェクトの `getPolicyManager` メソッド。
   * を呼び出してポリシーを削除する `PolicyManager` オブジェクトの `deletePolicy` メソッドを使用して、次の値を渡します。

      * ポリシーが属するポリシーセット名を指定する string 値です。 次を指定できます。 `null` 結果は `MyPolicies` 使用されているポリシーセットです。
      * 削除するポリシーの名前を指定する string 値です。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAP モード）:Java API を使用したポリシーの削除»

### Web サービス API を使用したポリシーの削除 {#delete-policies-using-the-web-service-api}

Document Security API（Web サービス）を使用してポリシーを削除します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security クライアント API オブジェクトを作成します。

   * の作成 `RightsManagementServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `RightsManagementServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `RightsManagementServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. ポリシーを削除します。

   を呼び出してポリシーを削除する `RightsManagementServiceClient` オブジェクトの `deletePolicy` メソッドを使用して、次の値を渡します。

   * ポリシーが属するポリシーセット名を指定する string 値です。 次を指定できます。 `null` 結果は `MyPolicies` 使用されているポリシーセットです。
   * 削除するポリシーの名前を指定する string 値です。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したポリシーの削除»
* クイックスタート (SwaRef):Web サービス API を使用したポリシーの削除»

## ポリシー・ドキュメントへのPDFの適用 {#applying-policies-to-pdf-documents}

ドキュメントを保護するために、PDFドキュメントにポリシーを適用できます。 ポリシーをPDFドキュメントに適用すると、ドキュメントへのアクセスを制限できます。 ドキュメントが既にポリシーで保護されている場合、ドキュメントにポリシーを適用することはできません。

ドキュメントを開いている間は、テキストの印刷とコピー、変更、ドキュメントへの署名とコメントの追加など、AcrobatとAdobe Readerの機能へのアクセスを制限することもできます。 また、ユーザーがドキュメントにアクセスできなくなった場合に、ポリシーで保護されたPDFドキュメントを失効させることもできます。

ポリシーで保護されたドキュメントを配布した後で、そのドキュメントの使用を監視できます。 つまり、ドキュメントの使用方法と使用者を確認できます。 例えば、誰かがドキュメントを開いた日時を知ることができます。

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

ポリシーをポリシードキュメントにPDFするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. ポリシーが適用されるPDF・ドキュメントを取得します。
1. ポリシードキュメントに既存のPDFを適用します。
1. ポリシーで保護されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成します。 Java API を使用している場合は、 `DocumentSecurityClient` オブジェクト。 Document Security Web サービス API を使用している場合は、 `DocumentSecurityServiceService` オブジェクト。

**PDF文書の取得**

ポリシーを適用するPDFドキュメントを取得できます。 ポリシーをポリシードキュメントに適用すると、PDFを使用する際にユーザーが制限されます。 例えば、ポリシーでドキュメントをオフラインで開くことができない場合、ユーザーがドキュメントを開くにはオンラインである必要があります。

**ポリシードキュメントに既存のPDFを適用**

ポリシーをPDFドキュメントに適用するには、既存のポリシーを参照し、ポリシーが属するポリシーセットを指定します。 接続プロパティを設定するユーザーは、指定したポリシーにアクセスできる必要があります。 そうでない場合は、例外が発生します。

**PDF文書を保存**

Document Security サービスによってPDFがポリシードキュメントに適用された後、ポリシーで保護されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ドキュメントへのアクセスの取り消し](protecting-documents-policies.md#revoking-access-to-documents)

### Java API を使用したPDFドキュメントへのポリシーの適用 {#apply-a-policy-to-a-pdf-document-using-the-java-api}

Document Security API(Java) を使用して、PDFドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDF文書を取得

   * の作成 `java.io.FileInputStream` コンストラクタを使用してPDF・ドキュメントを表すオブジェクト。 PDFドキュメントの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ポリシードキュメントに既存のPDFを適用します。

   * の作成 `DocumentManager` を呼び出すことによってオブジェクトを取得 `RightsManagementClient` オブジェクトの `getDocumentManager` メソッド。
   * を呼び出して、PDFドキュメントにポリシーを適用する `DocumentManager` オブジェクトの `protectDocument` メソッドを使用して、次の値を渡します。

      * この `com.adobe.idp.Document` ポリシーが適用されるPDF・ドキュメントを含むオブジェクト。
      * ドキュメントの名前を指定する string 値。
      * ポリシーが属するポリシーセットの名前を指定する string 値です。 次の項目を指定できます。 `null` 結果として `MyPolicies` 使用されているポリシーセットです。
      * ポリシー名を指定する string 値です。
      * ドキュメントのパブリッシャであるユーザーのユーザーマネージャードメインの名前を表す string 値です。 このパラメータの値はオプションで、null にすることができます（このパラメータが null の場合、次のパラメータの値は null にする必要があります）。
      * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名の名前を表す string 値です。 このパラメーター値はオプションで、 `null` ( このパラメーターが null の場合、前のパラメーター値は `null`) をクリックします。
      * A `com.adobe.livecycle.rightsmanagement.Locale` MS Office テンプレートの選択に使用されるロケールを表す このパラメーター値はオプションで、PDFドキュメントには使用されません。 PDF・ドキュメントを保護するには、 `null`.

      この `protectDocument` メソッドは、 `RMSecureDocumentResult` ポリシーで保護されたPDF・ドキュメントを含むオブジェクト。


1. PDF文書を保存します。

   * を呼び出す `RMSecureDocumentResult` オブジェクトの `getProtectedDoc` メソッドを使用して、ポリシーで保護されたPDFドキュメントを取得します。 このメソッドは、 `com.adobe.idp.Document` オブジェクト。
   * の作成 `java.io.File` オブジェクトに置き換え、ファイル拡張子がPDFであることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します ( `Document` が返したオブジェクト `getProtectedDoc` メソッド )。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（EJB モード）:Java API を使用したPDFドキュメントへのポリシーの適用»
* 「クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントへのポリシーの適用»

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してPDFドキュメントにポリシーを適用する {#apply-a-policy-to-a-pdf-document-using-the-web-service-api}

Document Security API（Web サービス）を使用して、PDFドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security クライアント API オブジェクトを作成します。

   * の作成 `RightsManagementServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `RightsManagementServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をFormsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `RightsManagementServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. PDF文書を取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、ポリシーが適用されるPDF・ドキュメントを格納するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズを、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. ポリシードキュメントに既存のPDFを適用します。

   を呼び出して、PDFドキュメントにポリシーを適用する `RightsManagementServiceClient` オブジェクトの `protectDocument` メソッドを使用して、次の値を渡します。

   * この `BLOB` ポリシーが適用されるPDF・ドキュメントを含むオブジェクト。
   * ドキュメントの名前を指定する string 値。
   * ポリシーが属するポリシーセットの名前を指定する string 値です。 次の項目を指定できます。 `null` 結果として `MyPolicies` 使用されているポリシーセットです。
   * ポリシー名を指定する string 値です。
   * ドキュメントのパブリッシャであるユーザーのユーザーマネージャードメインの名前を表す string 値です。 このパラメーター値はオプションで、null にすることができます ( このパラメーターが null の場合、次のパラメーター値は `null`) をクリックします。
   * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名の名前を表す string 値です。 このパラメーター値はオプションで、null にすることができます ( このパラメーターが null の場合、前のパラメーター値を `null`) をクリックします。
   * A `RMLocale` ロケール値を指定する値 ( 例： `RMLocale.en`) をクリックします。
   * ポリシー識別子の値を格納するために使用される文字列出力パラメーターです。
   * ポリシーで保護された識別子の値を保存するために使用される文字列出力パラメーターです。
   * MIME タイプを保存するために使用される文字列出力パラメーター ( 例： `application/pdf`) をクリックします。

   この `protectDocument` メソッドは、 `BLOB` ポリシーで保護されたPDF・ドキュメントを含むオブジェクト。

1. PDF文書を保存します。

   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `protectDocument` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用してPDFドキュメントにポリシーを適用する»
* クイックスタート (SwaRef):Web サービス API「 」を使用してPDFドキュメントにポリシーを適用する

## ポリシー・ドキュメントからのPDFの削除 {#removing-policies-from-pdf-documents}

ポリシーで保護されたドキュメントからポリシーを削除して、ドキュメントからセキュリティを削除できます。 つまり、ドキュメントをポリシーで保護したくない場合です。 ポリシーで保護されたドキュメントを新しいポリシーで更新する場合は、ポリシーを削除して更新されたポリシーを追加する代わりに、ポリシーを切り替える方が効率的です。

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

ポリシーで保護されたポリシードキュメントからPDFを削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. Document Security クライアント API オブジェクトを作成します。
1. ポリシーで保護されたPDFドキュメントを取得します。
1. ポリシードキュメントからPDFを削除します。
1. 保護されていないPDF文書を保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成します。

**ポリシーで保護されたPDF・ドキュメントの取得**

ポリシーを削除するために、ポリシーで保護されたPDFドキュメントを取得することができます。 ポリシーで保護されていないPDFドキュメントからポリシーを削除しようとすると、例外が発生します。

**ポリシードキュメントからPDFを削除**

接続設定で管理者が指定されている場合は、ポリシーで保護されたPDFドキュメントからポリシーを削除できます。 そうでない場合、ドキュメントの保護に使用するポリシーには、 `SWITCH_POLICY` ポリシードキュメントからポリシーを削除するPDF。 また、AEM Forms接続設定で指定したユーザーにも、その権限が必要です。 それ以外の場合は、例外がスローされます。

**保護されていないPDF文書を保存**

Document Security サービスがPDFドキュメントからポリシーを削除した後、保護されていないPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ポリシー・ドキュメントへのPDFの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java API を使用してPDFドキュメントからポリシーを削除する {#remove-a-policy-from-a-pdf-document-using-the-java-api}

Document Security API(Java) を使用して、ポリシーで保護されたPDFドキュメントからポリシーを削除します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたPDFドキュメントを取得します。

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことによって、ポリシーで保護されたPDFドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ポリシードキュメントからPDFを削除します。

   * の作成 `DocumentManager` を呼び出すことによってオブジェクトを取得 `DocumentSecurityClient` オブジェクトの `getDocumentManager` メソッド。
   * を呼び出して、PDFドキュメントからポリシーを削除する `DocumentManager` オブジェクトの `removeSecurity` メソッドおよび `com.adobe.idp.Document` ポリシーで保護されたPDF・ドキュメントを含むオブジェクト。 このメソッドは、 `com.adobe.idp.Document` 保護されていないPDFドキュメントを含むオブジェクト。

1. 保護されていないPDF文書を保存します。

   * の作成 `java.io.File` オブジェクトに置き換え、ファイル拡張子がPDFであることを確認します。
   * を呼び出す `Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します ( `Document` が返したオブジェクト `removeSecurity` メソッド )。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAP モード）:Java API を使用したPDFドキュメントからのポリシーの削除»

### Web サービス API を使用してポリシーを削除する {#remove-a-policy-using-the-web-service-api}

Document Security API（Web サービス）を使用して、ポリシーで保護されたPDFドキュメントからポリシーを削除します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security クライアント API オブジェクトを作成します。

   * の作成 `DocumentSecurityServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `DocumentSecurityServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. ポリシーで保護されたPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、ポリシーが削除される、ポリシーで保護されたPDF・ドキュメントの保存に使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. ポリシードキュメントからPDFを削除します。

   を呼び出して、PDFドキュメントからポリシーを削除します。 `DocumentSecurityServiceClient` オブジェクトの `removePolicySecurity` メソッドおよび `BLOB` ポリシーで保護されたPDF・ドキュメントを含むオブジェクト。 このメソッドは、 `BLOB` 保護されていないPDFドキュメントを含むオブジェクト。

1. 保護されていないPDF文書を保存します。

   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `removePolicySecurity` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` フィールドに入力します。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API「 」を使用したPDFドキュメントからのポリシーの削除
* クイックスタート (SwaRef):Web サービス API を使用したPDFドキュメントからのポリシーの削除»

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ドキュメントへのアクセスの取り消し {#revoking-access-to-documents}

ポリシーで保護されたPDFドキュメントへのアクセスを取り消すと、そのドキュメントのすべてのコピーに対してユーザーからアクセスできなくなります。 取り消されたPDFドキュメントを開こうとすると、ユーザーは指定された URL にリダイレクトされ、この URL で変更されたドキュメントを表示できます。 ユーザーのリダイレクト先の URL をプログラムで指定する必要があります。 ドキュメントへのアクセスを取り消すと、ユーザーが次回、ポリシーで保護されたドキュメントをオンラインで開くことで Document Security サービスと同期したときに、変更が反映されます。

ドキュメントへのアクセスを取り消す機能により、セキュリティが強化されます。 例えば、新しいバージョンのドキュメントが使用可能で、古いバージョンを表示するユーザーが不要になるとします。 この場合、古いドキュメントへのアクセスを取り消し、アクセス権が回復されない限り、誰もドキュメントを表示できません。

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

ポリシーで保護されたドキュメントを失効するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. ポリシーで保護されたPDFドキュメントを取得します。
1. ポリシーで保護されたドキュメントを失効させます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成する必要があります。

**ポリシーで保護されたPDF・ドキュメントの取得**

ポリシーで保護されたPDFドキュメントを取り消す必要があります。 失効済みのドキュメントや、ポリシーで保護されたドキュメントではないドキュメントは失効できません。

ポリシーで保護されたドキュメントのライセンス識別子の値がわかっている場合は、ポリシーで保護されたPDFドキュメントを取得する必要はありません。 ただし、ほとんどの場合、ライセンス識別子の値を取得するには、PDFドキュメントを取得する必要があります。

**ポリシーで保護されたドキュメントを失効**

ポリシーで保護されたドキュメントを失効するには、ポリシーで保護されたドキュメントのライセンス識別子を指定します。 さらに、取り消されたドキュメントを開こうとしたときにユーザーが表示できるドキュメントの URL を指定できます。 つまり、古いドキュメントが取り消されたとします。 取り消されたドキュメントを開こうとすると、取り消されたドキュメントではなく、更新されたドキュメントが表示されます。

>[!NOTE]
>
>既に失効済みのドキュメントを失効しようとすると、例外が発生します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ポリシー・ドキュメントへのPDFの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[取り消されたドキュメントへのアクセスの回復](protecting-documents-policies.md#reinstating-access-to-revoked-documents)

### Java API を使用したドキュメントへのアクセスの取り消し {#revoke-access-to-documents-using-the-java-api}

Document Security API(Java) を使用して、ポリシーで保護されたPDFドキュメントへのアクセスを取り消します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。

1. Document Security クライアント API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護されたPDF・ドキュメントの取得

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことによって、ポリシーで保護されたPDFドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ポリシーで保護されたドキュメントを失効

   * の作成 `DocumentManager` を呼び出すことによってオブジェクトを取得 `DocumentSecurityClient` オブジェクトの `getDocumentManager` メソッド。
   * を呼び出して、ポリシーで保護されたドキュメントのライセンス識別子の値を取得します。 `DocumentManager` オブジェクトの `getLicenseId` メソッド。 パス `com.adobe.idp.Document` ポリシーで保護されたドキュメントを表すオブジェクト。 このメソッドは、ライセンス識別子の値を表す string 値を返します。
   * の作成 `LicenseManager` を呼び出すことによってオブジェクトを取得 `DocumentSecurityClient` オブジェクトの `getLicenseManager` メソッド。
   * を呼び出して、ポリシーで保護されたドキュメントを失効させます。 `LicenseManager` オブジェクトの `revokeLicense` メソッドを使用して、次の値を渡します。

      * ポリシーで保護されたドキュメントのライセンス識別子の値を指定する string 値 ( `DocumentManager` オブジェクトの `getLicenseId` メソッド )。
      * 静的データメンバー `License` ドキュメントを失効させる理由を指定するインターフェイス。 例えば、次の項目を指定できます。 `License.DOCUMENT_REVISED`.
      * A `java.net.URL` 改訂済みドキュメントの場所を指定する値。 ユーザーを別の URL にリダイレクトしたくない場合、 `null`.

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAP モード）:Java API を使用したドキュメントの取り消し»

### Web サービス API を使用してドキュメントへのアクセスを取り消す {#revoke-access-to-documents-using-the-web-service-api}

Document Security API（Web サービス）を使用して、ポリシーで保護されたPDFドキュメントへのアクセスを取り消します。

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security クライアント API オブジェクトの作成

   * の作成 `DocumentSecurityServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `DocumentSecurityServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. ポリシーで保護されたPDF・ドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、取り消されたポリシーで保護されたPDF・ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、取り消すポリシーで保護されたPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによってオブジェクトを取得します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. ポリシーで保護されたドキュメントを失効

   * を呼び出して、ポリシーで保護されたドキュメントのライセンス識別子の値を取得します。 `DocumentSecurityServiceClient` オブジェクトの `getLicenseID` メソッドおよび `BLOB` ポリシーで保護されたドキュメントを表すオブジェクト。 このメソッドは、ライセンス識別子を表す string 値を返します。
   * を呼び出して、ポリシーで保護されたドキュメントを失効させます。 `DocumentSecurityServiceClient` オブジェクトの `revokeLicense` メソッドを使用して、次の値を渡します。

      * ポリシーで保護されたドキュメントのライセンス識別子の値を指定する string 値 ( `DocumentSecurityServiceService` オブジェクトの `getLicenseId` メソッド )。
      * 静的データメンバー `Reason` ドキュメントを失効させる理由を指定する列挙。 例えば、次の項目を指定できます。 `Reason.DOCUMENT_REVISED`.
      * A `string` 改訂されたドキュメントの URL の場所を指定する値。 ユーザーを別の URL にリダイレクトしたくない場合、 `null`.

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したドキュメントの取り消し»
* クイックスタート (SwaRef):Web サービス API を使用したドキュメントの取り消し»

**関連トピック**

[Word ドキュメントからポリシーを削除する](protecting-documents-policies.md#removing-policies-from-word-documents)

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 取り消されたドキュメントへのアクセスの回復 {#reinstating-access-to-revoked-documents}

取り消されたPDFドキュメントへのアクセス権を回復すると、取り消されたドキュメントのすべてのコピーにユーザーがアクセスできるようになります。 ユーザーが失効した回復済みドキュメントを開くと、そのドキュメントを表示できます。

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-6}

取り消されたPDF・ドキュメントへのアクセス権を回復するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security クライアント API オブジェクトを作成します。
1. 取り消されたライセンスドキュメントのPDF識別子を取得します。
1. 取り消されたPDF・ドキュメントへのアクセス権を回復します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成する必要があります。 Java API を使用している場合は、 `DocumentSecurityClient` オブジェクト。 Document Security Web サービス API を使用している場合は、 `DocumentSecurityServiceService` オブジェクト。

**失効したライセンスドキュメントのライセンスPDFを取得**

失効したPDFドキュメントを回復するには、失効したPDFドキュメントのライセンス識別子を取得する必要があります。 ライセンス識別子の値を取得した後、失効したドキュメントを回復できます。 失効していないドキュメントを回復しようとすると、例外が発生します。

**取り消されたPDF文書へのアクセス権の回復**

取り消されたPDFドキュメントへのアクセスを回復するには、取り消されたドキュメントのライセンス識別子を指定する必要があります。 失効していないPDF・ドキュメントへのアクセス権を元に戻そうとすると、例外が発生します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ポリシー・ドキュメントへのPDFの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

[ドキュメントへのアクセスの取り消し](protecting-documents-policies.md#revoking-access-to-documents)

### Java API を使用した、取り消されたドキュメントへのアクセス権の回復 {#reinstate-access-to-revoked-documents-using-the-java-api}

Document Security API(Java) を使用して、取り消されたドキュメントへのアクセス権を回復します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 取り消されたライセンスドキュメントのPDF識別子を取得します。

   * の作成 `java.io.FileInputStream` コンストラクタを使用し、PDFドキュメントの場所を指定する string 値を渡すことによって、取り消されたPDFドキュメントを表すオブジェクト。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * の作成 `DocumentManager` を呼び出すことによってオブジェクトを取得 `DocumentSecurityClient` オブジェクトの `getDocumentManager` メソッド。
   * を呼び出して、取り消されたドキュメントのライセンス識別子の値を取得します。 `DocumentManager` オブジェクトの `getLicenseId` メソッドおよび `com.adobe.idp.Document` 失効したドキュメントを表すオブジェクト。 このメソッドは、ライセンス識別子を表す string 値を返します。

1. 取り消されたPDF・ドキュメントへのアクセス権を回復します。

   * の作成 `LicenseManager` を呼び出すことによってオブジェクトを取得 `DocumentSecurityClient` オブジェクトの `getLicenseManager` メソッド。
   * を呼び出して、取り消されたPDFドキュメントへのアクセスを回復する `LicenseManager` オブジェクトの `unrevokeLicense` 取り消されたドキュメントのメソッドおよびライセンス識別子の値を渡す方法。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAP モード）:Web サービス API を使用した取り消されたドキュメントへのアクセス権の回復»

### Web サービス API を使用した、取り消されたドキュメントへのアクセス権の回復 {#reinstate-access-to-revoked-documents-using-the-web-service-api}

Document Security API（Web サービス）を使用して、取り消されたドキュメントへのアクセスを回復します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security Client API オブジェクトを作成します。

   * の作成 `DocumentSecurityServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `DocumentSecurityServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. 取り消されたライセンスドキュメントのPDF識別子を取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、アクセス権が回復された失効済みPDF・ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを呼び出し、取り消されたPDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡すことによってオブジェクトを取り出します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. 取り消されたPDF・ドキュメントへのアクセス権を回復します。

   * を呼び出して、取り消されたドキュメントのライセンス識別子の値を取得します。 `DocumentSecurityServiceClient` オブジェクトの `getLicenseID` メソッドおよび `BLOB` 失効したドキュメントを表すオブジェクト。 このメソッドは、ライセンス識別子を表す string 値を返します。
   * を呼び出して、取り消されたPDFドキュメントへのアクセスを回復する `DocumentSecurityServiceClient` オブジェクトの `unrevokeLicense` メソッドを使用し、取り消されたPDFドキュメントのライセンス識別子の値を指定する string 値を渡す ( `DocumentSecurityServiceClient` オブジェクトの `getLicenseId` メソッド )。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用した取り消されたドキュメントへのアクセス権の回復»
* クイックスタート (SwaRef):Web サービス API を使用した取り消されたドキュメントへのアクセス権の回復»

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## ポリシーで保護されたPDF文書の検査 {#inspecting-policy-protected-pdf-documents}

Document Security Service API（Java および Web サービス）を使用して、ポリシーで保護されたPDFドキュメントを検査できます。 ポリシーで保護されたPDFドキュメントを検査すると、ポリシーで保護されたPDFドキュメントに関する情報が返されます。 例えば、ドキュメントの保護に使用されたポリシーやドキュメントの保護日を指定できます。

使用しているバージョンが 8.x 以前のLiveCycleの場合、このタスクを実行できません。 ポリシーで保護されたドキュメントの検査に関するサポートがAEM Formsに追加されました。 LiveCycle8.x（またはそれ以前）を使用してポリシーで保護されたドキュメントを検査しようとすると、例外がスローされます。

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-7}

ポリシーで保護されたPDF・ドキュメントを検査するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Document Security クライアント API オブジェクトを作成します。
1. 検査するポリシーで保護されたドキュメントを取得します。
1. ポリシーで保護されたドキュメントに関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成します。 Java API を使用している場合は、 `RightsManagementClient` オブジェクト。 Document Security Web サービス API を使用している場合は、 `RightsManagementServiceService` オブジェクト。

**ポリシーで保護されたドキュメントを取得して検査する**

ポリシーで保護されたドキュメントを検査するには、ドキュメントを取得します。 ポリシーで保護されていないドキュメントや、取り消されたドキュメントを検査しようとすると、例外がスローされます。

**Inspect**

ポリシーで保護されたドキュメントを取得した後に、それを検査することができます。

**ポリシーで保護されたドキュメントに関する情報を取得する**

ポリシーで保護されたPDFドキュメントを検査した後、そのドキュメントに関する情報を取得できます。 例えば、ドキュメントの保護に使用するポリシーを指定できます。

マイポリシーに属するポリシーでドキュメントを保護した場合は、を呼び出します。 `RMInspectResult.getPolicysetName` または `RMInspectResult.getPolicysetId`の場合、null が戻されます。

ポリシーセットに含まれるポリシー（マイポリシー以外）を使用してドキュメントを保護する場合は、 `RMInspectResult.getPolicysetName` および `RMInspectResult.getPolicysetId` 有効な文字列を返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したInspectポリシーで保護されたPDFドキュメント {#inspect-policy-protected-pdf-documents-using-the-java-api}

Inspect Document Security Service API(Java) を使用して、ポリシーで保護されたPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、 adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. Document Security Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 検査するポリシーで保護されたドキュメントを取得します。

   * の作成 `java.io.FileInputStream` コンストラクタを使用して、ポリシーで保護されたPDF・ドキュメントを表すオブジェクト。 PDFドキュメントの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. Inspectドキュメント。

   * の作成 `DocumentManager` を呼び出すことによってオブジェクトを取得 `RightsManagementClient` オブジェクトの `getDocumentManager` メソッド。
   * Inspectを呼び出して、ポリシーで保護されたドキュメントを `LicenseManager` オブジェクトの `inspectDocument` メソッド。 パス `com.adobe.idp.Document` ポリシーで保護されたPDF・ドキュメントを含むオブジェクト。 このメソッドは、 `RMInspectResult` ポリシーで保護されたドキュメントに関する情報を含むオブジェクト。

1. ポリシーで保護されたドキュメントに関する情報を取得します。

   ポリシーで保護されたドキュメントに関する情報を取得するには、に属する適切なメソッドを呼び出します `RMInspectResult` オブジェクト。 例えば、ポリシー名を取得するには、 `RMInspectResult` オブジェクトの `getPolicyName` メソッド。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAP モード）:Java API を使用したPDF保護ポリシードキュメントの検査»

### Web サービス API を使用したInspect Policy ProtectedPDFドキュメント {#inspect-policy-protected-pdf-documents-using-the-web-service-api}

Inspect Document Security Service API（Web サービス）を使用して、ポリシーで保護されたPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security クライアント API オブジェクトを作成します。

   * の作成 `RightsManagementServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `RightsManagementServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `RightsManagementServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. 検査するポリシーで保護されたドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、検査するPDFドキュメントを格納するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。 PDFドキュメントのファイルの場所と、ファイルを開くモードを表す string 値を渡します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. Inspectドキュメント。

   Inspectを呼び出して、ポリシーで保護されたドキュメントを `RightsManagementServiceClient` オブジェクトの `inspectDocument` メソッド。 パス `BLOB` ポリシーで保護されたPDF・ドキュメントを含むオブジェクト。 このメソッドは、 `RMInspectResult` ポリシーで保護されたドキュメントに関する情報を含むオブジェクト。

1. ポリシーで保護されたドキュメントに関する情報を取得します。

   ポリシーで保護されたドキュメントに関する情報を取得するには、 `RMInspectResult` オブジェクト。 例えば、ポリシー名を取得するには、 `RMInspectResult` オブジェクトの `policyName` フィールドに入力します。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したPDF保護ドキュメントの検査»
* クイックスタート (SwaRef):Web サービス API を使用したPDF保護ドキュメントの検査»

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 透かしの作成 {#creating-watermarks}

透かしは、ドキュメントを一意に識別し、著作権侵害を制御することで、ドキュメントのセキュリティを確保するのに役立ちます。 例えば、ドキュメントのすべてのページに機密を示す透かしを作成して配置できます。 透かしを作成した後は、その透かしをポリシーの一部として含めることができます。 つまり、新しく作成した透かしにポリシーの透かし属性を設定できます。 透かしを含むポリシーがドキュメントに適用されると、その透かしはポリシーで保護されたドキュメントに表示されます。

>[!NOTE]
>
>透かしを作成できるのは、Document Security 管理者権限を持つユーザーのみです。 つまり、Document Security サービスクライアントオブジェクトの作成に必要な接続設定を定義する際には、このようなユーザーを指定する必要があります。

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-8}

透かしを作成するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. 透かし属性を設定します。
1. 透かしを Document Security サービスに登録します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成する必要があります。 Java API を使用している場合は、 `RightsManagementClient` オブジェクト。 Document Security Web サービス API を使用している場合は、 `RightsManagementServiceService` オブジェクト。

**透かし属性の設定**

新しい透かしを作成するには、透かし属性を設定する必要があります。 name 属性を常に定義する必要があります。 name 属性に加えて、次の属性の少なくとも 1 つを設定する必要があります。

* カスタムテキスト
* DateIncluded
* UserIdIncluded
* UserNameIncluded

次の表に、Web サービスを使用して透かしを作成する際に必要なキーと値のペアを示します。

<table> 
 <thead> 
  <tr> 
   <th><p>キー名</p></th> 
   <th><p>説明</p></th> 
   <th><p>値</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p><code>WaterBackCmd:IS_USERNAME_ENABLED</code></p></td> 
   <td><p>ドキュメントを開くユーザーのユーザー名が透かしの一部であるかどうかを指定します。</p></td> 
   <td><p>True または False</p></td> 
  </tr> 
  <tr> 
   <td><p><code>WaterBackCmd:IS_USERID_ENABLED</code></p></td> 
   <td><p>ドキュメントを開くユーザーの ID が透かしの一部であるかどうかを指定します。</p></td> 
   <td><p>True または False</p></td> 
  </tr> 
  <tr> 
   <td><p><code>WaterBackCmd:IS_CURRENTDATE_ENABLED</code></p></td> 
   <td><p>現在の日付が透かしの一部であるかどうかを指定します。</p></td> 
   <td><p>True または False</p></td> 
  </tr> 
  <tr> 
   <td><p><code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code></p></td> 
   <td><p>この値が true の場合、カスタムテキストの値は <code>WaterBackCmd:SRCTEXT</code>.</p></td> 
   <td><p>True または False</p></td> 
  </tr> 
  <tr> 
   <td><p><code>WaterBackCmd:OPACITY</code></p></td> 
   <td><p>透かしの不透明度を指定します。 指定しない場合、デフォルト値は 0.5 です。</p></td> 
   <td><p>0.0 ～ 1.0 の値。</p></td> 
  </tr> 
  <tr> 
   <td><p><code>WaterBackCmd:ROTATION</code></p></td> 
   <td><p>透かしの回転を指定します。 デフォルト値は 0 度です。</p></td> 
   <td><p>0 ～ 359 の値。</p></td> 
  </tr> 
  <tr> 
   <td><p><code>WaterBackCmd:SCALE</code></p></td> 
   <td><p>この値を指定した場合、 <code>WaterBackCmd:IS_SIZE_ENABLED</code> が存在し、値が true である必要があります。 この属性を指定しない場合、デフォルトの動作がページに合わせて適用されます。</p></td> 
   <td><p>0.0 より大きく 1.0 以下の値。</p></td> 
  </tr> 
  <tr> 
   <td><p><code>WaterBackCmd:HORIZ_ALIGN</code></p></td> 
   <td><p>透かしの水平方向の位置を指定します。 デフォルト値は center です。</p></td> 
   <td><p>左、中央、右</p></td> 
  </tr> 
  <tr> 
   <td><p><code>WaterBackCmd:VERT_ALIGN</code></p></td> 
   <td><p>透かしの垂直方向の位置を指定します。 デフォルト値は center です。</p></td> 
   <td><p>上、中央、下</p></td> 
  </tr> 
  <tr> 
   <td><p><code>WaterBackCmd:IS_USE_BACKGROUND</code></p></td> 
   <td><p>透かしが背景かどうかを指定します。 デフォルト値は false です。</p></td> 
   <td><p>True または False</p></td> 
  </tr> 
  <tr> 
   <td><p><code>WaterBackCmd:IS_SIZE_ENABLED</code></p></td> 
   <td><p>True を指定すると、カスタム尺度が指定されます。 この値が true の場合は、SCALE も指定する必要があります。 この値が false の場合、デフォルトはページに合わせて適用されます。</p></td> 
   <td><p>True または False</p></td> 
  </tr> 
  <tr> 
   <td><p><code>WaterBackCmd:SRCTEXT</code></p></td> 
   <td><p>透かしのカスタムテキストを指定します。 この値が存在する場合、 <code>WaterBackCmd:IS_CUSTOMTEXT_ENABLED</code> また、が存在し、true に設定されている必要があります。</p></td> 
   <td><p>True または False</p></td> 
  </tr> 
 </tbody> 
</table>

すべての透かしには、次の属性のいずれかが定義されている必要があります。

* `WaterBackCmd:IS_USERNAME_ENABLED`
* `WaterBackCmd:IS_USERID_ENABLED`
* `WaterBackCmd:IS_CURRENTDATE_ENABLED`
* `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`

その他の属性はすべてオプションです。

**透かしの登録**

新しい透かしを使用するには、その透かしを Document Security サービスに登録しておく必要があります。 透かしを登録した後、その透かしをポリシー内で使用できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ポリシー・ドキュメントへのPDFの適用](protecting-documents-policies.md#applying-policies-to-pdf-documents)

### Java API を使用した透かしの作成 {#create-watermarks-using-the-java-api}

Document Security API(Java) を使用して透かしを作成します。

1. プロジェクトファイルを含めます。

   クライアント JAR ファイルを含める ( 例： `adobe-rightsmanagement-client.jar`Java プロジェクトのクラスパスに含まれます。

1. Document Security クライアント API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 透かし属性の設定

   * の作成 `Watermark` を呼び出すことによってオブジェクトを取得 `InfomodelObjectFactory` オブジェクトの静的 `createWatermark` メソッド。 このメソッドは、 `Watermark` オブジェクト。
   * を呼び出して、透かしの名前属性を設定します。 `Watermark` オブジェクトの `setName` メソッドを使用し、ポリシー名を指定する string 値を渡す。
   * を呼び出して、透かしの背景属性を設定します。 `Watermark` オブジェクトの `setBackground` メソッドとパス `true`. この属性を設定すると、透かしがドキュメントの背景に表示されます。
   * を呼び出して、透かしのカスタムテキスト属性を設定する `Watermark` オブジェクトの `setCustomText` メソッドを使用して透かしのテキストを表す string 値を渡すことができます。
   * 透かしの不透明度アトリビュートを設定するには、 `Watermark` オブジェクトの `setOpacity` メソッドを使用し、不透明度レベルを指定する整数値を渡す。 値 100 は透かしが完全に不透明であることを示し、値 0 は透かしが完全に透明であることを示します。

1. 透かしを登録します。

   * の作成 `WatermarkManager` を呼び出すことによってオブジェクトを取得 `RightsManagementClient` オブジェクトの `getWatermarkManager` メソッド。 このメソッドは、 `WatermarkManager` オブジェクト。
   * を呼び出して透かしを登録します。 `WatermarkManager` オブジェクトの `registerWatermark` メソッドおよび `Watermark` 登録する透かしを表すオブジェクト。 このメソッドは、透かしの識別値を表す string 値を返します。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAP モード）:Java API を使用した透かしの作成»

### Web サービス API を使用した透かしの作成 {#create-watermarks-using-the-web-service-api}

Document Security API（Web サービス）を使用して透かしを作成します。

1. Document Security クライアント API オブジェクトを作成します。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security クライアント API オブジェクトを作成します。

   * の作成 `RightsManagementServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `RightsManagementServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `RightsManagementServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. 透かし属性を設定します。

   * の作成 `WatermarkSpec` を呼び出すことによってオブジェクトを取得 `WatermarkSpec` コンストラクタ。
   * 透かしの名前を設定するには、 `WatermarkSpec` オブジェクトの `name` データメンバー。
   * 透かしの `id` 属性を設定するために、 `WatermarkSpec` オブジェクトの `id` データメンバー。
   * 透かしプロパティを設定するたびに、個別に `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。
   * キーの値を設定するには、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` データメンバー ( 例： `WaterBackCmd:OPACITY)`.
   * 値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` データメンバー ( 例： `.25`) をクリックします。
   * の作成 `MyArrayOf_xsd_anyType` オブジェクト。 各 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト、 `MyArrayOf_xsd_anyType` オブジェクトの `Add` メソッド。 パス `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。
   * を `MyArrayOf_xsd_anyType` オブジェクトを `WatermarkSpec` オブジェクトの `values` データメンバー。

1. 透かしを登録します。

   を呼び出して透かしを登録します。 `RightsManagementServiceClient` オブジェクトの `registerWatermark` メソッドおよび `WatermarkSpec` 登録する透かしを表すオブジェクト。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用した透かしの作成»
* クイックスタート (SwaRef):Web サービス API を使用した透かしの作成»

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 透かしの変更 {#modifying-watermarks}

既存の透かしは、Document Security Java API または Web サービス API を使用して変更できます。 既存の透かしを変更するには、その透かしを取得し、その属性を変更して、サーバー上で更新します。 例えば、透かしを取得し、その不透明度属性を変更したとします。 変更を有効にする前に、透かしを更新する必要があります。

透かしを変更すると、その透かしが適用された後のドキュメントに変更が影響します。 つまり、透かしを含む既存のPDFドキュメントは影響を受けません。

>[!NOTE]
>
>透かしを変更できるのは、Document Security 管理者権限を持つユーザーだけです。 つまり、Document Security サービスクライアントオブジェクトの作成に必要な接続設定を定義する際には、このようなユーザーを指定する必要があります。

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-9}

透かしを変更するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Document Security Client API オブジェクトを作成します。
1. 変更する透かしを取得します。
1. 透かし属性を設定します。
1. 透かしを更新します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成する必要があります。 Java API を使用している場合は、 `DocumentSecurityClient` オブジェクト。 Document Security Web サービス API を使用している場合は、 `DocumentSecurityServiceService` オブジェクト。

**変更する透かしを取得します**

透かしを変更するには、既存の透かしを取得する必要があります。 透かしを取得するには、名前を指定するか、識別子の値を指定します。

**透かし属性の設定**

既存の透かしを変更するには、1 つ以上の透かし属性の値を変更します。 Web サービスを使用してプログラムによって透かしを更新する場合、値が変更されなくても、元々設定されていたすべての属性を設定する必要があります。 例えば、次の透かし属性が設定されているとします。 `WaterBackCmd:IS_USERID_ENABLED`, `WaterBackCmd:IS_CUSTOMTEXT_ENABLED`, `WaterBackCmd:OPACITY`、および `WaterBackCmd:SRCTEXT`. 変更する属性は次のみです。 `WaterBackCmd:OPACITY`の場合は、他の値は正常に設定する必要があります。

>[!NOTE]
>
>Java API を使用して透かしを変更する場合、すべての属性を指定する必要はありません。 変更する透かし属性を設定します。

>[!NOTE]
>
>透かし属性の名前について詳しくは、 [透かしの作成](protecting-documents-policies.md#creating-watermarks).

**透かしの更新**

透かしの属性を変更した後、透かしを更新する必要があります。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[透かしの作成](protecting-documents-policies.md#creating-watermarks)

### Java API を使用した透かしの変更 {#modify-watermarks-using-the-java-api}

Document Security API(Java) を使用して透かしを変更します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、 adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。

1. Document Security クライアント API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変更する透かしを取得します。

   の作成 `WatermarkManager` を呼び出すことによってオブジェクトを取得 `DocumentSecurityClient` オブジェクトの `getWatermarkManager` メソッドを使用して透かしの名前を指定する string 値を渡します。 このメソッドは、 `Watermark` 変更する透かしを表すオブジェクト。

1. 透かし属性を設定します。

   透かしの不透明度アトリビュートを設定するには、 `Watermark` オブジェクトの `setOpacity` メソッドを使用し、不透明度レベルを指定する整数値を渡す。 値 100 は透かしが完全に不透明であることを示し、値 0 は透かしが完全に透明であることを示します。

   >[!NOTE]
   >
   >次の使用例は、不透明度の属性のみを変更します。

1. 透かしを更新します。

   * を呼び出して透かしを更新する `WatermarkManager` オブジェクトの `updateWatermark` メソッドを使用して、 `Watermark` 属性が変更されたオブジェクト。

**コード例**

Document Security サービスを使用するコード例については、クイックスタート（SOAP モード）を参照してください。「Java API」セクションを使用した透かしの変更

### Web サービス API を使用した透かしの変更 {#modify-watermarks-using-the-web-service-api}

Document Security API（Web サービス）を使用して透かしを変更します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security Client API オブジェクトを作成します。

   * の作成 `DocumentSecurityServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `RightsManagementServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `DocumentSecurityServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. 変更する透かしを取得します。

   を呼び出して、変更する透かしを取得します。 `DocumentSecurityServiceClient` オブジェクトの `getWatermarkByName` メソッド。 透かしの名前を指定する string 値を渡します。 このメソッドは、 `WatermarkSpec` 変更する透かしを表すオブジェクト。

1. 透かし属性を設定します。

   * 透かしプロパティを更新するたびに、個別に `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。
   * キーの値を設定するには、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` データメンバー ( 例： `WaterBackCmd:OPACITY)`.
   * 値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` データメンバー ( 例： `.50`) をクリックします。
   * の作成 `MyArrayOf_xsd_anyType` オブジェクト。 各 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト、 `MyArrayOf_xsd_anyType` オブジェクトの `Add` メソッド。 パス `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクト。
   * を `MyArrayOf_xsd_anyType` オブジェクトを `WatermarkSpec` オブジェクトの `values` データメンバー。

1. 透かしを更新します。

   を呼び出して透かしを更新する `DocumentSecurityServiceClient` オブジェクトの `updateWatermark` メソッドおよび `WatermarkSpec` 変更する透かしを表すオブジェクト。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用した透かしの変更»

## イベントの検索 {#searching-for-events}

Rights Managementサービスは、特定のアクション（ドキュメントへのポリシーの適用、ポリシーで保護されたドキュメントの開封、ドキュメントへのアクセスの取り消しなど）の発生時に追跡を行います。 イベントサービスに対してイベント監査を有効にする必要があります。Rights Managementが追跡されない場合は、イベント監査を有効にする必要があります。

イベントは、次のカテゴリのいずれかに分類されます。

* 管理者イベントは、新しい管理者アカウントの作成など、管理者に関連するアクションです。
* ドキュメントイベントは、ポリシーで保護されたドキュメントを閉じるなど、ドキュメントに関連するアクションです。
* ポリシーイベントは、新しいポリシーの作成など、ポリシーに関連するアクションです。
* サービスイベントは、ユーザーディレクトリとの同期など、Rights Managementサービスに関連するアクションです。

Rights ManagementJava API または Web サービス API を使用して、特定のイベントを指定して検索できます。 イベントを検索すると、特定のイベントのログファイルの作成などのタスクを実行できます。

>[!NOTE]
>
>Rights Management [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-10}

イベントイベントを検索するには、次のRights Managementを実行します。

1. プロジェクトファイルを含めます。
1. Rights Managementクライアント API オブジェクトを作成します。
1. 検索するイベントを指定します。
1. イベントを検索します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Rights Managementクライアント API オブジェクトの作成**

プログラムによってRights Managementサービスの操作を実行する前に、Rights Managementサービスクライアントオブジェクトを作成する必要があります。 Java API を使用している場合は、 `DocumentSecurityClient` オブジェクト。 Rights ManagementWeb サービス API を使用している場合、 `DocumentSecurityServiceService` オブジェクト。

**検索するイベントを指定**

検索するイベントを指定する必要があります。 例えば、新しいポリシーの作成時に発生するポリシー create イベントを検索できます。

**イベントの検索**

検索するイベントを指定した後、Rights ManagementJava API またはRights ManagementWeb サービス API を使用して、イベントを検索できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したイベントの検索 {#search-for-events-using-the-java-api}

イベント API(Java) を使用してRights Managementを検索します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。

1. Rights Managementクライアント API オブジェクトの作成

   の作成 `DocumentSecurityClient` オブジェクトのコンストラクタを使用し、 `ServiceClientFactory` 接続プロパティを含むオブジェクト。

1. 検索するイベントを指定

   * の作成 `EventManager` を呼び出すことによってオブジェクトを取得 `DocumentSecurityClient` オブジェクトの `getEventManager` メソッド。 このメソッドは、 `EventManager` オブジェクト。
   * の作成 `EventSearchFilter` オブジェクトを指定します。
   * を呼び出して検索するイベントを指定します。 `EventSearchFilter` オブジェクトの `setEventCode` メソッドを使用して、 `EventManager` 検索するイベントを表すクラス。 例えば、ポリシーの作成イベントを検索するには、 `EventManager.POLICY_CREATE_EVENT`.

   >[!NOTE]
   >
   >を呼び出すことで、追加の検索条件を定義できます `EventSearchFilter` オブジェクトメソッド。 例えば、 `setUserName` メソッドを使用して、イベントに関連付けられているユーザーを指定します。

1. イベントの検索

   を呼び出してイベントを検索する `EventManager` オブジェクトの `searchForEvents` メソッドおよび `EventSearchFilter` イベントの検索条件を定義するオブジェクト。 このメソッドは、 `Event` オブジェクト。

**コード例**

Rights Managementサービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (SOAP):Java API を使用したイベントの検索»

### Web サービス API を使用したイベントの検索 {#search-for-events-using-the-web-service-api}

Rights ManagementAPI（Web サービス）を使用してイベントを検索します。

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Rights Managementクライアント API オブジェクトの作成

   * の作成 `DocumentSecurityServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `DocumentSecurityServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. 検索するイベントを指定

   * の作成 `EventSpec` オブジェクトを指定します。
   * イベントが発生した期間の開始を指定するには、 `EventSpec` オブジェクトの `firstTime.date` 次のデータメンバー `DataTime` イベントが発生した日付範囲の開始を表すインスタンス。
   * 値を割り当て `true` から `EventSpec` オブジェクトの `firstTime.dateSpecified` データメンバー。
   * イベントが発生した期間の終わりを指定するには、 `EventSpec` オブジェクトの `lastTime.date` 次のデータメンバー `DataTime` イベントが発生した日付範囲の終わりを表すインスタンス。
   * 値を割り当て `true` から `EventSpec` オブジェクトの `lastTime.dateSpecified` データメンバー。
   * 検索するイベントを設定するには、 `EventSpec` オブジェクトの `eventCode` データメンバー。 次の表に、このプロパティに割り当てることができる数値を示します。

   <table> 
    <thead> 
    <tr> 
    <th><p>イベントタイプ</p></th> 
    <th><p>値</p></th> 
    </tr> 
    </thead> 
    <tbody>
    <tr> 
    <td><p><code>ALL_EVENTS</code></p></td> 
    <td><p>999</p></td> 
    </tr> 
    <tr> 
    <td><p><code>USER_CHANGE_PASSWORD_EVENT</code></p></td> 
    <td><p>1000</p></td> 
    </tr> 
    <tr> 
    <td><p><code>USER_REGISTER_EVENT</code></p></td> 
    <td><p>1001</p></td> 
    </tr> 
    <tr> 
    <td><p><code>USER_PREREGISTER_EVENT</code></p></td> 
    <td><p>1002</p></td> 
    </tr> 
    <tr> 
    <td><p><code>USER_ACTIVATE_EVENT</code></p></td> 
    <td><p>1003</p></td> 
    </tr> 
    <tr> 
    <td><p><code>USER_DEACTIVATE_EVENT</code></p></td> 
    <td><p>1004</p></td> 
    </tr> 
    <tr> 
    <td><p><code>USER_AUTHENTICATE_EVENT</code></p></td> 
    <td><p>1005</p></td> 
    </tr> 
    <tr> 
    <td><p><code>USER_AUTHENTICATE_DENY_EVENT </code></p></td> 
    <td><p>1006</p></td> 
    </tr> 
    <tr> 
    <td><p><code>USER_ACCOUNT_LOCK_EVENT</code></p></td> 
    <td><p>1007</p></td> 
    </tr> 
    <tr> 
    <td><p><code>USER_DELETE_EVENT </code></p></td> 
    <td><p>1008</p></td> 
    </tr> 
    <tr> 
    <td><p><code>USER_UPDATE_PROFILE_EVENT </code></p></td> 
    <td><p>1009</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_VIEW_EVENT </code></p></td> 
    <td><p>2,000</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_PRINT_LOW_EVENT </code></p></td> 
    <td><p>2001 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_PRINT_HIGH_EVENT </code></p></td> 
    <td><p>2002 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_SIGN_EVENT </code></p></td> 
    <td><p>2003 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_ADD_ANNOTATION_EVENT </code></p></td> 
    <td><p>2004 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_FORM_FILL_EVENT </code></p></td> 
    <td><p>2005 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_CLOSE_EVENT </code></p></td> 
    <td><p>2006</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_MODIFY_EVENT </code></p></td> 
    <td><p>2007 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_CHANGE_SECURITY_HANDLER_EVENT </code></p></td> 
    <td><p>2008</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_SWITCH_POLICY_EVENT </code></p></td> 
    <td><p>2009 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_REVOKE_EVENT </code></p></td> 
    <td><p>2010 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>$1</code></p></td> 
    <td><p>2011 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_SECURE_EVENT </code></p></td> 
    <td><p>2012 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_UNKNOWN_CLIENT_EVENT </code></p></td> 
    <td><p>2013 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DOCUMENT_CHANGE_REVOKE_URL_EVENT </code></p></td> 
    <td><p>2014 年</p></td> 
    </tr> 
    <tr> 
    <td><p><code>POLICY_CHANGE_EVENT </code></p></td> 
    <td><p>3000</p></td> 
    </tr> 
    <tr> 
    <td><p><code>POLICY_ENABLE_EVENT </code></p></td> 
    <td><p>3001</p></td> 
    </tr> 
    <tr> 
    <td><p><code>POLICY_DISABLE_EVENT </code></p></td> 
    <td><p>3002</p></td> 
    </tr> 
    <tr> 
    <td><p><code>POLICY_CREATE_EVENT </code></p></td> 
    <td><p>3003</p></td> 
    </tr> 
    <tr> 
    <td><p><code>POLICY_DELETE_EVENT </code></p></td> 
    <td><p>3004</p></td> 
    </tr> 
    <tr> 
    <td><p><code>POLICY_CHANGE_OWNER_EVENT </code></p></td> 
    <td><p>3005</p></td> 
    </tr> 
    <tr> 
    <td><p><code>SERVER_CLIENT_SYNC_EVENT </code></p></td> 
    <td><p>4000</p></td> 
    </tr> 
    <tr> 
    <td><p><code>SERVER_SYNC_DIR_INFO_EVENT </code></p></td> 
    <td><p>4001</p></td> 
    </tr> 
    <tr> 
    <td><p><code>SERVER_SYNC_DIR_COMPLETE_EVENT </code></p></td> 
    <td><p>4002</p></td> 
    </tr> 
    <tr> 
    <td><p><code>SERVER_VERSION_MISMATCH_EVENT </code></p></td> 
    <td><p>4003</p></td> 
    </tr> 
    <tr> 
    <td><p><code>SERVER_CONFIG_CHANGE_EVENT </code></p></td> 
    <td><p>4004</p></td> 
    </tr> 
    <tr> 
    <td><p><code>SERVER_ENABLE_OFFLINE_ACCESS_EVENT </code></p></td> 
    <td><p>4005</p></td> 
    </tr> 
    <tr> 
    <td><p><code>ADMIN_ADD_EVENT </code></p></td> 
    <td><p>5,000</p></td> 
    </tr> 
    <tr> 
    <td><p><code>ADMIN_DELETE_EVENT </code></p></td> 
    <td><p>5001</p></td> 
    </tr> 
    <tr> 
    <td><p><code>ADMIN_EDIT_EVENT </code></p></td> 
    <td><p>5002</p></td> 
    </tr> 
    <tr> 
    <td><p><code>ADMIN_ACTIVATE_EVENT </code></p></td> 
    <td><p>5003</p></td> 
    </tr> 
    <tr> 
    <td><p><code>ADMIN_DEACTIVATE_EVENT </code></p></td> 
    <td><p>5004</p></td> 
    </tr> 
    <tr> 
    <td><p><code>ERROR_DIRECTORY_SERVICE_EVENT </code></p></td> 
    <td><p>6000</p></td> 
    </tr> 
    <tr> 
    <td><p><code>CREATED_POLICYSET_EVENT</code></p></td> 
    <td><p>7000</p></td> 
    </tr> 
    <tr> 
    <td><p><code>DELETED_POLICYSET_EVENT</code></p></td> 
    <td><p>7001</p></td> 
    </tr> 
    <tr> 
    <td><p><code>MODIFIED_POLICYSET_EVENT</code></p></td> 
    <td><p>7002</p></td> 
    </tr> 
    </tbody> 
    </table>

1. イベントの検索

   を呼び出してイベントを検索する `DocumentSecurityServiceClient` オブジェクトの `searchForEvents` メソッドおよび `EventSpec` 検索するイベントと結果の最大数を表すオブジェクト。 このメソッドは、 `MyArrayOf_xsd_anyType` 各要素が `AuditSpec` インスタンス。 の使用 `AuditSpec` 例えば、イベントが発生した時刻などの情報を取得できます。 この `AuditSpec` インスタンスに次が含まれる `timestamp` この情報を指定するデータメンバー。

**コード例**

Rights Managementサービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用したイベントの検索»
* クイックスタート (SwaRef):Web サービス API を使用したイベントの検索»

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Word ドキュメントへのポリシーの適用 {#applying-policies-to-word-documents}

Rights Management サービスは、PDFドキュメントに加えて、Microsoft Word ドキュメント（DOC ファイル）などのドキュメント形式や、その他の Microsoft Office ファイル形式もサポートしています。 例えば、Word 文書を保護するために、Word 文書にポリシーを適用できます。 Word 文書にポリシーを適用すると、文書へのアクセスが制限されます。 ドキュメントが既にポリシーで保護されている場合、ドキュメントにポリシーを適用することはできません。

ポリシーで保護された Word 文書を配布した後で、その文書の使用状況を監視できます。 つまり、ドキュメントの使用方法と使用者を確認できます。 例えば、誰かがドキュメントを開いた日時を知ることができます。

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-11}

Word 文書にポリシーを適用するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Document Security クライアント API オブジェクトを作成します。
1. ポリシーが適用される Word ドキュメントを取得します。
1. Word ドキュメントに既存のポリシーを適用します。
1. ポリシーで保護された Word ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成する必要があります。

**Word ドキュメントの取得**

ポリシーを適用するには、Word ドキュメントを取得する必要があります。 Word ドキュメントにポリシーを適用すると、ドキュメントの使用時にユーザーが制限されます。 例えば、ポリシーでドキュメントをオフラインで開くことができない場合、ユーザーがドキュメントを開くにはオンラインである必要があります。

**Word ドキュメントに既存のポリシーを適用する**

Word 文書にポリシーを適用するには、既存のポリシーを参照し、そのポリシーが属するポリシーセットを指定する必要があります。 接続プロパティを設定するユーザーは、指定したポリシーにアクセスできる必要があります。 そうでない場合は、例外が発生します。

**Word 文書を保存する**

Document Security サービスによって Word ドキュメントにポリシーが適用されたら、ポリシーで保護された Word ドキュメントを DOC ファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[ドキュメントへのアクセスの取り消し](protecting-documents-policies.md#revoking-access-to-documents)

### Java API を使用して Word ドキュメントにポリシーを適用する {#apply-a-policy-to-a-word-document-using-the-java-api}

Document Security API(Java) を使用して、Word ドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   Java プロジェクトのクラスパスに、adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。

1. Document Security クライアント API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentSecurityClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Word 文書を取得します。

   * の作成 `java.io.FileInputStream` Word ドキュメントを表すオブジェクトです。このオブジェクトのコンストラクタを使用し、Word ドキュメントの場所を指定する string 値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. Word ドキュメントに既存のポリシーを適用します。

   * の作成 `DocumentManager` を呼び出すことによってオブジェクトを取得 `DocumentSecurityClient` オブジェクトの `getDocumentManager` メソッド。
   * を呼び出して、Word ドキュメントにポリシーを適用する `DocumentManager` オブジェクトの `protectDocument` メソッドを使用して、次の値を渡します。

      * この `com.adobe.idp.Document` ポリシーが適用される Word ドキュメントを含むオブジェクト。
      * ドキュメントの名前を指定する string 値。
      * ポリシーが属するポリシーセットの名前を指定する string 値です。 次の項目を指定できます。 `null` 結果として `MyPolicies` 使用されているポリシーセットです。
      * ポリシー名を指定する string 値です。
      * ドキュメントのパブリッシャであるユーザーのユーザーマネージャードメインの名前を表す string 値です。 このパラメータの値はオプションで、null にすることができます（このパラメータが null の場合、次のパラメータの値は null にする必要があります）。
      * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名の名前を表す string 値です。 このパラメーター値はオプションで、 `null` ( このパラメーターが `null`を指定した場合、前のパラメーター値は `null`) をクリックします。
      * A `com.adobe.livecycle.rightsmanagement.Locale` MS Office テンプレートの選択に使用されるロケールを表す このパラメーター値はオプションで、次を指定できます。 `null`.

      この `protectDocument` メソッドは、 `RMSecureDocumentResult` ポリシーで保護された Word ドキュメントを含むオブジェクト。


1. Word ドキュメントを保存します。

   * を呼び出す `RMSecureDocumentResult` オブジェクトの `getProtectedDoc` メソッドを使用して、ポリシーで保護された Word ドキュメントを取得します。 このメソッドは、 `com.adobe.idp.Document` オブジェクト。
   * の作成 `java.io.File` オブジェクトを探し、ファイル拡張子が DOC であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します ( `Document` が返したオブジェクト `getProtectedDoc` メソッド )。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAP モード）:Java API を使用して Word ドキュメントにポリシーを適用する»

### Web サービス API を使用して Word ドキュメントにポリシーを適用する {#apply-a-policy-to-a-word-document-using-the-web-service-api}

Document Security API（Web サービス）を使用して、Word ドキュメントにポリシーを適用します。

1. プロジェクトファイルを含めます。

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/DocumentSecurityService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security Client API オブジェクトを作成します。

   * の作成 `DocumentSecurityServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `DocumentSecurityServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/DocumentSecurityService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `DocumentSecurityServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `DocumentSecurityServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. Word 文書を取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、ポリシーが適用される Word ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズを、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. Word ドキュメントに既存のポリシーを適用します。

   を呼び出して、Word ドキュメントにポリシーを適用する `DocumentSecurityServiceClient` オブジェクトの `protectDocument` メソッドを使用して、次の値を渡します。

   * この `BLOB` ポリシーが適用される Word ドキュメントを含むオブジェクト。
   * ドキュメントの名前を指定する string 値。
   * ポリシーが属するポリシーセットの名前を指定する string 値です。 次の項目を指定できます。 `null` 結果として `MyPolicies` 使用されているポリシーセットです。
   * ポリシー名を指定する string 値です。
   * ドキュメントのパブリッシャであるユーザーのユーザーマネージャードメインの名前を表す string 値です。 このパラメーター値はオプションで、null にすることができます ( このパラメーターが null の場合、次のパラメーター値は `null`) をクリックします。
   * ドキュメントのパブリッシャーであるユーザーマネージャーユーザーの正規名の名前を表す string 値です。 このパラメーター値はオプションで、null にすることができます ( このパラメーターが null の場合、前のパラメーター値を `null`) をクリックします。
   * A `RMLocale` ロケール値を指定する値 ( 例： `RMLocale.en`) をクリックします。
   * ポリシー識別子の値を格納するために使用される文字列出力パラメーターです。
   * ポリシーで保護された識別子の値を保存するために使用される文字列出力パラメーターです。
   * MIME タイプを保存するために使用される文字列出力パラメーター ( 例： `application/doc`) をクリックします。

   この `protectDocument` メソッドは、 `BLOB` ポリシーで保護された Word ドキュメントを含むオブジェクト。

1. Word ドキュメントを保存します。

   * の作成 `System.IO.FileStream` オブジェクトを作成するには、コンストラクタを呼び出し、ポリシーで保護された Word ドキュメントのファイルの場所を表す string 値を渡します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `protectDocument` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。
   * バイト配列の内容を Word ファイルに書き込むには、 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用して Word ドキュメントにポリシーを適用する

## Word ドキュメントからポリシーを削除する {#removing-policies-from-word-documents}

ポリシーで保護された Word ドキュメントからポリシーを削除して、ドキュメントのセキュリティを解除できます。 つまり、ドキュメントをポリシーで保護したくない場合です。 ポリシーで保護された Word ドキュメントを新しいポリシーで更新する場合は、ポリシーを削除して更新したポリシーを追加する代わりに、ポリシーを切り替える方が効率的です。

>[!NOTE]
>
>Document Security サービスについて詳しくは、 [AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-12}

ポリシーで保護された Word 文書からポリシーを削除するには、次の手順を実行します。

1. プロジェクトファイルを含める
1. Document Security Client API オブジェクトを作成します。
1. ポリシーで保護された Word ドキュメントを取得します。
1. Word ドキュメントからポリシーを削除します。
1. 保護されていない Word ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Document Security クライアント API オブジェクトの作成**

Document Security サービスの操作をプログラムで実行する前に、Document Security サービスのクライアントオブジェクトを作成します。

**ポリシーで保護された Word ドキュメントの取得**

ポリシーを削除するには、ポリシーで保護された Word ドキュメントを取得する必要があります。 ポリシーで保護されていない Word 文書からポリシーを削除しようとすると、例外が発生します。

**Word ドキュメントからポリシーを削除する**

接続設定で管理者が指定されている場合は、ポリシーで保護された Word ドキュメントからポリシーを削除できます。 そうでない場合、ドキュメントの保護に使用するポリシーには、 `SWITCH_POLICY` Word ドキュメントからポリシーを削除する権限です。 また、AEM Forms接続設定で指定したユーザーにも、その権限が必要です。 それ以外の場合は、例外がスローされます。

**保護されていない Word 文書を保存する**

Document Security サービスで Word ドキュメントからポリシーを削除した後、保護されていない Word ドキュメントを DOC ファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Word ドキュメントへのポリシーの適用](protecting-documents-policies.md#applying-policies-to-word-documents)

### Java API を使用して Word ドキュメントからポリシーを削除する {#remove-a-policy-from-a-word-document-using-the-java-api}

Document Security API(Java) を使用して、ポリシーで保護された Word ドキュメントからポリシーを削除します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-rightsmanagement-client.jar などのクライアント JAR ファイルを含めます。

1. Document Security クライアント API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `RightsManagementClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. ポリシーで保護された Word ドキュメントの取得

   * の作成 `java.io.FileInputStream` オブジェクトを返します。このオブジェクトは、Word ドキュメントの場所を指定する文字列値を渡し、コンストラクタを使用してポリシーで保護された Word ドキュメントを表します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. Word ドキュメントからポリシーを削除する

   * の作成 `DocumentManager` を呼び出すことによってオブジェクトを取得 `RightsManagementClient` オブジェクトの `getDocumentManager` メソッド。
   * を呼び出して、Word ドキュメントからポリシーを削除する `DocumentManager` オブジェクトの `removeSecurity` メソッドおよび `com.adobe.idp.Document` ポリシーで保護された Word ドキュメントを含むオブジェクト。 このメソッドは、 `com.adobe.idp.Document` 保護されていない Word ドキュメントを含むオブジェクト。

1. 保護されていない Word 文書を保存する

   * の作成 `java.io.File` オブジェクトを探し、ファイル拡張子が DOC であることを確認します。
   * を呼び出す `Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します ( `Document` が返したオブジェクト `removeSecurity` メソッド )。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート（SOAP モード）:Java API &quot;を使用した Word ドキュメントからのポリシーの削除

### Web サービス API を使用して Word ドキュメントからポリシーを削除する {#remove-a-policy-from-a-word-document-using-the-web-service-api}

Document Security API（Web サービス）を使用して、ポリシーで保護された Word ドキュメントからポリシーを削除します。

1. プロジェクトファイルを含める

   MTOM を使用するMicrosoft .NET プロジェクトを作成します。 次の WSDL 定義を使用していることを確認します。 `http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >置換 `localhost` を、AEM Formsをホストするサーバーの IP アドレスに設定します。

1. Document Security クライアント API オブジェクトの作成

   * の作成 `RightsManagementServiceClient` オブジェクトのデフォルトのコンストラクタを使用します。
   * の作成 `RightsManagementServiceClient.Endpoint.Address` オブジェクトを `System.ServiceModel.EndpointAddress` コンストラクタ。 WSDL をAEM Formsサービスに渡す文字列値 ( 例： `http://localhost:8080/soap/services/RightsManagementService?WSDL`.) を使用する必要はありません。 `lc_version` 属性。 この属性は、サービス参照を作成する際に使用されます )。
   * の作成 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、 `RightsManagementServiceClient.Endpoint.Binding` フィールドに入力します。 戻り値を `BasicHttpBinding` にキャストします。
   * を `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値は、MTOM が確実に使用されるようにします。
   * 次のタスクを実行して、基本的な HTTP 認証を有効にします。

      * フィールドにAEM forms ユーザー名を割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.UserName`.
      * 対応するパスワード値をフィールドに割り当てます。 `RightsManagementServiceClient.ClientCredentials.UserName.Password`.
      * 定数値を割り当て `HttpClientCredentialType.Basic` フィールドに `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 定数値を割り当て `BasicHttpSecurityMode.TransportCredentialOnly` フィールドに `BasicHttpBindingSecurity.Security.Mode`.


1. ポリシーで保護された Word ドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、ポリシーが削除される、ポリシーで保護された Word ドキュメントを保存するために使用されます。
   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * コンテンツを格納するバイト配列を作成します。 `System.IO.FileStream` オブジェクト。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリーム長を渡す。
   * 次の項目に `BLOB` オブジェクトを割り当てる `MTOM` フィールドにバイト配列の内容を入力します。

1. Word ドキュメントからポリシーを削除する

   を呼び出して、Word ドキュメントからポリシーを削除します。 `RightsManagementServiceClient` オブジェクトの `removePolicySecurity` メソッドおよび `BLOB` ポリシーで保護された Word ドキュメントを含むオブジェクト。 このメソッドは、 `BLOB` 保護されていない Word ドキュメントを含むオブジェクト。

1. 保護されていない Word 文書を保存する

   * の作成 `System.IO.FileStream` オブジェクトを指定します。
   * のデータコンテンツを格納するバイト配列を作成します。 `BLOB` が返したオブジェクト `removePolicySecurity` メソッド。 バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` フィールドに入力します。
   * の作成 `System.IO.BinaryWriter` オブジェクトのコンストラクタを呼び出し、 `System.IO.FileStream` オブジェクト。

**コード例**

Document Security サービスを使用するコード例については、次のクイックスタートを参照してください。

* 「クイックスタート (MTOM):Web サービス API を使用した Word ドキュメントからのポリシーの削除»

**関連トピック**

[MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
