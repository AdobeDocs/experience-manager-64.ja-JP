---
title: アダプティブフォームのフィールドの事前入力
seo-title: Prefill adaptive form fields
description: 既存データを使用して、アダプティブフォームのフィールドを事前入力します。
seo-description: With adaptive forms, you users can prefill basic information in a form by logging in with their social profiles. This article describes how you can accomplish this.
uuid: 05d74a59-3950-4513-bfce-6ff3d9d5318c
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: 2ddb33a5-0d62-46f4-8f8c-0f0807a975cb
feature: Adaptive Forms
exl-id: 67bb208a-042b-4fa1-9ab1-23325e0c7e4c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '2037'
ht-degree: 62%

---

# アダプティブフォームのフィールドの事前入力 {#prefill-adaptive-form-fields}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

既存データを使用して、アダプティブフォームのフィールドを事前入力します。

## はじめに {#introduction}

既存のデータを使用して、アダプティブフォームのフィールドに事前に値を設定することができます。 ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。アダプティブフォーム内のデータを事前入力するには、アダプティブフォームの事前入力データ構造に準拠した形式で、ユーザーデータを事前入力 XML/JSON として使用できるようにします。

## 事前入力データの構造 {#the-prefill-structure}

アダプティブフォームには、連結されたフィールドと連結されていないフィールドが混在している場合があります。連結されたフィールドは、「コンテンツファインダー」タブからドラッグされたフィールドです。フィールドの編集ダイアログには、空ではない `bindRef` プロパティ値が含まれています。連結されていないフィールドは、サイドキックのコンポーネントブラウザーから直接ドラッグされ、`bindRef` 値が含まれています。

アダプティブフォームの連結されたフィールドと連結されていないフィールドの両方を事前に入力することができます。 事前入力データには、アダプティブフォームの連結されたフィールドと連結されていないフィールドの両方を事前入力する afBoundData セクションと afUnBoundData セクションが含まれています。 `afBoundData` セクションには連結されたフィールドとパネルの事前入力データが含まれています。このデータは関連するフォームモデルスキーマに準拠している必要があります。

* アダプティブフォームの場合は、 [XFA フォームテンプレート](/help/forms/using/prepopulate-adaptive-form-fields.md)の場合は、XFA テンプレートのデータスキーマに準拠している事前入力 XML を使用します。
* アダプティブフォームの場合： [XML スキーマ](#xml-schema-af)の場合は、XML スキーマ構造に準拠している事前入力 XML を使用します。
* アダプティブフォームの場合： [JSON スキーマ](/help/forms/using/prepopulate-adaptive-form-fields.md#json-schema-based-adaptive-forms)の場合は、JSON スキーマに準拠している事前入力 JSON を使用します。
* FDM スキーマを使用しているアダプティブフォームの場合は、FDM スキーマに準拠している事前入力 JSON を使用します。
* を含むアダプティブフォームの場合 [フォームモデルがありません](/help/forms/using/prepopulate-adaptive-form-fields.md#p-adaptive-form-with-no-form-model-p)、連結されたデータがありません。 すべてのフィールドは、連結されていないフィールドであり、連結されていない XML を使用して事前入力されています。

### 事前入力 XML 構造のサンプル {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         . 
         .              
    </data>
  </afUnboundData>
</afData>
```

### 事前入力 JSON 構造のサンプル {#sample-prefill-json-structure}

```
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

同じ bindref を持つ連結されているフィールド、または同じ名前を持つ連結されていないフィールドの場合、XML タグまたは JSON オブジェクトで指定したデータがすべてのフィールドに入力されます。例えば、フォーム内の 2 つのフィールドは、事前入力データの名前 `textbox` にマップされます。ランタイム時、最初のテキストボックスに「A」が含まれる場合、この「A」が 2 番目のテキストボックスに自動的に挿入されます。このリンクは、アダプティブフォームフィールドのライブリンクと呼ばれます。

## XFA フォームテンプレートを使用したアダプティブフォーム {#xfa-based-af}

 XFA ベースのアダプティブフォームの事前入力 XML と送信済み XML の構造は次のとおりです。

* **事前入力 XML 構造**：XFA ベースのアダプティブフォームのための事前入力 XML は、XFA フォームテンプレートのデータスキーマに準拠していなければなりません。連結されていないフィールドを事前入力するには、事前入力 XML 構造を `/afData/afBoundData` タグにラップします。

* **送信済み XML 構造**：事前入力 XML が使用されていない場合、送信済み XML の `afData` ラッパータグには、連結されたフィールドと連結されていないフィールドの両方のデータが含まれます。事前入力 XML が使用された場合、送信済み XML は、事前入力 XML と同じ構造をしています。事前入力 XML が `afData` のルートタグで開始する場合、出力 XML もまた同じフォーマットとなります。事前入力 XML に `afData/afBoundData` のラッパーが無く、直接 `employeeData` のようなスキーマルートタグから開始する場合は、送信済み XML もまた `employeeData` タグから開始します。

Prefill-Submit-Data-ContentPackage.zip

[ファイルを取得](assets/prefill-submit-data-contentpackage.zip)
事前入力データと送信済みデータが含まれているサンプル

## XML スキーマベースのアダプティブフォーム  {#xml-schema-af}

XML スキーマに基づくアダプティブフォームの事前入力 XML と送信済み XML の構造は、次のとおりです。

* **事前入力 XML 構造**：事前入力 XML は、関連する XML スキーマに準拠していなければなりません。連結されていないフィールドを事前入力するには、事前入力 XML 構造を /afData/afBoundData タグにラップします。
* **送信済み XML 構造**：事前入力 XML が使用されていない場合、送信済み XML は、`afData` のラッパータグに連結されたフィールドと連結されていないフィールド両方のデータを含みます。事前入力 XML が使用された場合、送信済み XML は、事前入力 XML と同じ構造をしています。事前入力 XML が `afData` のルートタグで開始する場合、出力 XML は同じフォーマットとなります。事前入力 XML に `afData/afBoundData` のラッパーが無く、直接 `employeeData` のようなスキーマルートタグから開始する場合は、送信済み XML もまた `employeeData` タグから開始します。

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">
 
    <xs:element name="sample" type="SampleType"/>
         
    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

XML スキーマをモデルとするフィールドの場合、以下の XML のサンプルに示すように、`afBoundData` タグのデータは事前入力されます。これは、1 つ以上の連結されていないテキストフィールドでアダプティブフォームを事前入力する場合に使用できます。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>連結されているパネル（サイドキックまたは「データソース」タブからコンポーネントをドラッグして作成された、空ではない `bindRef` が含まれているパネル）では、連結されていないフィールドを使用しないことをお勧めします。これらの連結していないフィールドのデータの損失を招くことがあります。また、フィールド名は、特に連結されていないフィールドに対して、フォーム間で一意にすることをお勧めします。

### afData および afBoundData ラッパーを使用しない例 {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

## JSON スキーマベースのアダプティブフォーム {#json-schema-based-adaptive-forms}

JSON スキーマに基づくアダプティブフォームの場合、事前入力 JSON と送信済み JSON の構造を以下に示します。 詳しくは、 [JSON スキーマを使用したアダプティブフォームの作成](/help/forms/using/adaptive-form-json-schema-form-model.md).

* **事前入力 JSON スキーマ**：事前入力 JSON は、関連する JSON スキーマに準拠している必要があります。連結していないフィールドの事前入力も行う場合は、オプションで、/afData/afBoundData オブジェクトにまとめることが可能です。
* **送信済み JSON 構造**：事前入力 JSON が使用されていない場合、送信済み JSON は、afData のラッパータグに連結されたフィールドと連結されていないフィールド両方のデータを含みます。事前入力 JSON が使用された場合、送信済み JSON は、事前入力 JSON と同じ構造をしています。事前入力 JSON が afData のルートオブジェクトで開始する場合、出力 JSON もまた同じフォーマットとなります。事前入力 JSON に afData/afBoundData のラッパーが無く、直接ユーザーのようなスキーマルートオブジェクトから開始する場合は、送信済み JSON もま user オブジェクトから開始します。

```
{
    "id": "https://some.site.somewhere/entry-schema#",
    "$schema": "https://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "address": {
            "type": "object",
            "properties": { 
    "name": {
     "type": "string"
    },
    "age": {
     "type": "integer"
}}}}}
```

JSON スキーマモデルを使用するフィールドの場合、以下の JSON のサンプルに示すように、afBoundData オブジェクトのデータは事前入力されます。これは、1 つ以上の連結されていないテキストフィールドでアダプティブフォームを事前入力する場合に使用できます。以下は `afData/afBoundData` ラッパーが含まれるデータの一例です。

```
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

以下は `afData/afBoundData` ラッパーが含まれない場合の一例です。

```
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>連結パネル（サイドキックまたは「データソース」タブからコンポーネントをドラッグして作成された、空でない bindRef を含むパネル）で、連結されていないフィールドを使用すると、 **not** 非連結フィールドのデータが失われる可能性があるので、お勧めします。 特に連結されていないフィールドに対しては、フォーム全体に一意のフィールド名を付けることをお勧めします。

## フォームモデルのないアダプティブフォーム {#adaptive-form-with-no-form-model}

フォームモデルが含まれていないアダプティブフォームの場合、すべてのフィールドのデータは、`<afUnboundData> tag` の `<data>` タグの下にあります。

また、次の点にも注意してください。

各種フィールドに送信されたユーザーデータのための XML タグは、フィールド名を使用して生成されます。したがって、フィールド名は一意である必要があります。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## 設定マネージャーを使用した事前入力サービスの設定 {#configuring-prefill-service-using-configuration-manager}

事前入力サービスを有効にするには、AEM Web コンソール設定で「デフォルトの事前入力サービス設定」を指定する必要があります。次の手順を使用して、事前入力サービスを設定します。

>[!NOTE]
>
>事前入力サービスの設定は、アダプティブフォーム、HTML5 フォーム、HTML5 フォームセットに適用できます。

1. 次の URL を使用して、**[!UICONTROL Adobe Experience Manager Web コンソール設定]**&#x200B;を開きます。\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. 「**[!UICONTROL デフォルトの事前入力サービス設定]**」を選択して開きます。

   ![prefill_config](assets/prefill_config.png)

1. データの場所または正規表現を「**[!UICONTROL データファイルの場所]**」に入力します。有効なデータファイルの場所の例は次のとおりです。

   * file:///C:/Users/public/Document/Prefill/.&amp;ast;
   * http://localhost:8000/somesamplexmlfile.xml

   >[!NOTE]
   >
   >デフォルトでは、事前入力はすべての種類のアダプティブフォーム（XSD、XDP、JSON、FDM、フォームモデルベースなし）で crx ファイルを通じて許可されます。事前入力は JSON ファイルおよび XML ファイルでのみ許可されます。

1. これで、事前入力サービスがフォームに対して設定されました。

   >[!NOTE]
   >
   >crx プロトコルは、事前入力済みデータのセキュリティを管理するので、デフォルトで許可されています。汎用正規表現を使用する他のプロトコルを介した事前入力は、脆弱性の原因となる場合があります。 設定で、データを保護するためのセキュア URL 設定を指定します。

## 繰り返し可能なパネルの好奇心が強いケース {#the-curious-case-of-repeatable-panels}

通常、連結（フォームスキーマ）フィールドと連結されていないフィールドは、同じアダプティブフォームで作成されますが、連結が繰り返し可能な場合に、次の例外がいくつかあります。

* XFA フォームテンプレート、XSD、JSON スキーマ、FDM スキーマを使用したアダプティブフォームでは、連結されていない繰り返し可能なパネルはサポートされていません。
* 連結された繰り返し可能パネルで、連結されていないフィールドを使用しないでください。

>[!NOTE]
>
>連結されていないフィールドにエンドユーザーが入力したデータ内で、連結されたフィールドと連結されていないフィールドが重なっている場合、それらのフィールドを混在させないでください。 可能な場合は、スキーマまたは XFA フォームテンプレートを変更し、連結されていないフィールドのエントリを追加して、連結されたデータも、送信されたデータ内の他のフィールドと同様に使用できるようにする必要があります。

## ユーザーデータの事前入力でサポートされるプロトコル {#supported-protocols-for-prefilling-user-data}

有効な正規表現を使用して設定されている場合は、以下のプロトコルを使用して、事前入力データ形式のユーザーデータでアダプティブフォームを事前入力することができます。

### The crx:// protocol {#the-crx-protocol}

```xml
http://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

特定のノードには、`jcr:data` と呼ばれるプロパティがあり、データを保持していなければなりません。

### The file:// protocol  {#the-file-protocol-nbsp}

```xml
http://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

参照元ファイルは、同じサーバー上になければなりません。

### The https:// protocol {#the-http-protocol}

```xml
http://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=http://localhost:8000/somesamplexmlfile.xml
```

### service:// プロトコル {#the-service-protocol}

```xml
http://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME とは OSGI 事前入力サービスの名前を指します。[事前入力サービスの作成と実行](/help/forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)を参照してください。
* 識別情報とは、OSGI 事前入力サービスが事前入力データを取得するために必要なメタデータを指します。ログインしたユーザーの識別子は、使用できるメタデータの例です。

>[!NOTE]
>
>認証パラメーターの引き渡しはサポートされていません。

### slingRequest でのデータ属性の設定 {#setting-data-attribute-in-slingrequest}

以下のサンプルコードが示すように、`data` 属性が XML または JSON を含む文字列である、`slingRequest` の `data` 属性を設定することもできます（以下は XML が含まれている場合の例です）。

```java
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

すべてのデータを含む単純な XML または JSON 文字列を記述し、slingRequest に設定できます。 これは、slingRequest data 属性を設定するページに含むすべてのコンポーネントのレンダラー JSP で、簡単にできます。

例えば、特定のタイプのヘッダーを持つページに特定のデザインを使用する場合などです。 これを達成するには、頁コンポーネントに含んで、`header.jsp` 属性を設定することができる独自の `data` を作成します。

例えば、Facebook、Twitter、LinkedIn などのソーシャルアカウントを使用して、ログイン時にデータを事前入力するとします。この場合、`header.jsp`ユーザーアカウントからデータを取得し、データパラメーターを設定するに単純な JSP を含めることができます。

prefill-page component.zip

[ファイルを取得](assets/prefill-page-component.zip)
ページコンポーネントのサンプル prefill.jsp

## AEM Forms カスタム事前入力サービス {#aem-forms-custom-prefill-service}

事前定義されたソースからデータを頻繁に読み取る必要がある場合は、カスタム事前入力サービスを使用できます。事前入力サービスは、定義済みのデータソースからデータを読み取り、事前入力データファイルの内容を使用して、アダプティブフォームのフィールドに事前入力します。 事前入力データをアダプティブフォームと永続的に関連付ける場合にも役立ちます。

### 事前入力サービスの作成と実行 {#create-and-run-a-prefill-service}

事前入力サービスは OSGi サービスで、OSGi バンドルを使用してパッケージ化します。OSGi バンドルを作成し、アップロードして、AEM Formsバンドルにインストールします。 バンドルの作成を開始する前に、以下を行います。

* [AEM Forms Client SDK のダウンロード](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)
* [ボイラープレートパッケージをダウンロードします](assets/prefill-sumbit-xmlsandcontentpackage.zip)

* データ（事前入力データ）ファイルを crx-repository に配置します。ファイルは crx-repository の \contents フォルダー内の任意の場所に配置できます。

#### 事前入力サービスの作成 {#create-a-prefill-service}

ボイラープレートパッケージ（サンプルの事前入力サービスパッケージ）には、AEM Forms事前入力サービスのサンプル実装が含まれています。 コードエディターでテンプレートパッケージを開きます。 例えば、Eclipse でテンプレートプロジェクトを開いて編集します。 コードエディターでテンプレートパッケージを開いた後、次の手順を実行してサービスを作成します。

1. src\main\java\com\adobe\test\Prefill.javaファイルを編集用に開きます。
1. コードで、次の値を設定します。

   * `nodePath:` crx-repository の場所を指すノードパス変数には、データ（事前入力）ファイルのパスが含まれています。例：/content/prefilldata.xml
   * `label:` label パラメーターは、サービスの表示名を指定します。例：Default Prefill Service

1. `Prefill.java` ファイルを保存して閉じます。
1. `AEM Forms Client SDK` パッケージをボイラープレートプロジェクトのビルドパスに追加します。
1. プロジェクトをコンパイルし、バンドルの.jar を作成します。

#### 事前入力サービスを開始して使用する {#start-and-use-the-prefill-service}

事前入力サービスを起動するには、JAR ファイルを AEM Forms Web コンソールにアップロードし、サービスをアクティブ化します。これで、変換サービスがアダプティブフォームエディターに表示され始めます。 事前入力サービスをアダプティブフォームに関連付けるには、次の手順を実行します。

1. Forms Editor でアダプティブフォームを開き、フォームコンテナのプロパティパネルを開きます。
1. プロパティコンソールで、に移動します。 **[!UICONTROL AEM Formsコンテナ/基本/事前入力サービス]**.
1. デフォルトの事前入力サービスを選択し、 **[!UICONTROL 保存]**. サービスはフォームに関連付けられます。
