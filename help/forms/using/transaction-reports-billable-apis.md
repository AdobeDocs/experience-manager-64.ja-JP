---
title: トランザクションレポート請求可能 API
seo-title: Transaction Reports Billable APIs
description: トランザクションとして計上されるすべての API のリスト
seo-description: List of all the APIs that are accounted as transactions
uuid: 8861e325-7393-4d2c-9ec1-17f391ca3909
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-manager
discoiquuid: 82e72ffb-2faa-45fe-8bb2-f485d8fa043e
exl-id: 18b5c6e2-3b0c-4ec8-9e65-c4105b47be4e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 10%

---

# トランザクションレポート請求可能 API {#transaction-reports-billable-apis}

トランザクションとして計上されるすべての API のリスト

AEM Formsには、フォームの送信、ドキュメントの処理、ドキュメントのレンダリングを行うための API がいくつか用意されています。 一部の API はトランザクションとして計上され、それ以外は自由に使用できます。 このドキュメントでは、トランザクションレポートでトランザクションとして計上されるすべての API のリストを示します。 課金対象の API が使用される一般的なシナリオを次に示します。

* アダプティブフォーム、HTML5 フォーム、フォームセットの送信
* インタラクティブ通信の印刷バージョンまたは Web バージョンのレンダリング
* ある形式から別の形式へのドキュメントの変換
* ダイナミックPDFドキュメントの統合
* レコードのドキュメントの生成
* インタラクティブPDFドキュメントと別のPDFドキュメントの結合
* AEM Workflows のタスク割り当て手順とドキュメントサービス手順の使用
* アダプティブフォーム内でのアダプティブフォームの使用

請求 API は、ページ数、ドキュメントまたはフォームの長さ、レンダリングされたドキュメントの最終的な形式を考慮しません。 トランザクションレポートでは、トランザクションを次の 3 つのカテゴリに分けます。処理されたドキュメント、レンダリングされたドキュメント、およびFormsが送信されました。

* **Forms Submitted:** AEM Formsで作成された任意のタイプのフォームからデータが送信され、そのデータが任意のデータストレージリポジトリまたはデータベースに送信された場合、そのデータはフォーム送信と見なされます。 例えば、アダプティブフォーム、HTML5 フォーム、PDF forms、フォームセットは、送信されたフォームとして計上されます。 フォームセット内の各フォームは、送信と見なされます。 例えば、フォームセットに 5 つのフォームが含まれている場合、フォームセットが送信されると、トランザクションレポートサービスはそのフォームセットを 5 件の送信としてカウントします。
* **レンダリングされたドキュメント：** テンプレートとデータを組み合わせたドキュメントの生成、ドキュメントのデジタル署名または認証、ドキュメントサービスの課金可能なドキュメントサービス API の使用、ある形式から別の形式へのドキュメントの変換は、ドキュメントとして計上されます。

>[!NOTE]
>
>トランザクションレポート UI には、次の 3 つのカテゴリが表示されます。Forms送信済み、レンダリングされたドキュメント、処理されたドキュメント。 レンダリングされたドキュメントと処理されたドキュメントの両方が、レンダリングされたドキュメントとして計上されます。

## 課金対象のドキュメントサービス API {#billable-document-services-apis}

### GeneratePDFサービス {#generate-pdf-service}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td> 
   <td>サポートされているファイルタイプからAdobe PDFを作成します。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td> 
   <td>サポートされているファイルタイプからAdobe PDFを作成します。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td> 
   <td>Adobe PDFをサポートされるファイルタイプに変換します。 </td> 
   <td>処理済みドキュメント<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td> 
   <td>Adobe PDFをサポートされるファイルタイプに変換します。 </td> 
   <td>処理済みドキュメント<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td> 
   <td>Adobe PDFをサポートされるファイルタイプに変換します。 </td> 
   <td>処理済みドキュメント<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td> 
   <td><p>PDFページからHTMLを作成</p> </td> 
   <td>処理済みドキュメント<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td> 
   <td>PDFページを指す URL からHTMLを作成します。</td> 
   <td>処理済みドキュメント<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td> 
   <td>PDFページを指す URL からHTMLを作成します。</td> 
   <td>処理済みドキュメント<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td> 
   <td>PDFを最適化し、画質に影響を与えることなく不要なメタデータを削除してファイルサイズを縮小します。</td> 
   <td>処理済みドキュメント<br /> </td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

### Distiller Service {#distiller-service}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td> 
   <td>サポートされているファイルタイプからAdobe PDFを作成します。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td> 
   <td>サポートされているファイルタイプからAdobe PDFを作成します。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

### レコードのドキュメントサービス（DoR サービス） {#document-of-record-service-dor-service}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td> 
   <td>指定されたレンダリングメソッドを呼び出して、指定されたパラメータを使用してレコードのドキュメントを生成します。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

### Output サービス {#output-service}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td> 
   <td>データとテンプレートを結合して、テンプレートドキュメントをPDFします。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td> 
   <td>データとテンプレートを結合して、一連のテンプレートドキュメントをPDFします。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td> 
   <td>XDP およびPDFドキュメントを PostScript(PS)、Printer Command Language(PCL) および ZPL ファイル形式に変換します。 </td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td> 
   <td>XDP およびPDFドキュメントを PostScript(PS)、Printer Command Language(PCL) および ZPL ファイル形式に変換します。 </td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td> 
   <td>XDP およびPDFドキュメントのセットを、PostScript(PS)、Printer Command Language(PCL) および ZPL の各ファイル形式に変換します。 </td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

### Forms サービス {#forms-service}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">｢renderPDFForm｣操作</a></td> 
   <td>PDFフォームを XDP テンプレートからレンダリングします。 XP テンプレートは、Forms Designer で作成されます。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td> 
   <td>テンプレートフォームまたは XDPPDFからデータを抽出します</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

### 変換PDFサービス {#convert-pdf-service}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td> 
   <td>PDFドキュメントを画像ドキュメントのリストに変換します。 サポートされる画像形式は、JPEG、JPEG2K、PNG、TIFFです。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td> 
   <td>オプション仕様で指定されたPDFを使用して、フラットオプションファイルを PostScript 形式に変換します。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

### Barcoded Forms サービス {#barcoded-forms-service}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td> 
   <td>Document オブジェクト内のすべてのバーコードをデコードし、バーコードから取得されたデータを含む org.w3c.dom.Document オブジェクトを返します。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

### Assembler サービス {#assembler-service}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">呼び出し</a></td> 
   <td>指定した DDX ドキュメントを実行し、 <a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> 結果のドキュメントを含むオブジェクト。 </td> 
   <td>処理済みドキュメント</td> 
   <td>次の操作はトランザクションとして計上されません。
    <ul> 
     <li>パッケージまたはポートフォリオの作成</li> 
     <li>複数の XDP のステッチ </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">呼び出し</a></td> 
   <td>指定した DDX ドキュメントを実行し、 <a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html"> AssemblerResult</a> 結果のドキュメントを含むオブジェクト。 </td> 
   <td>処理済みドキュメント</td> 
   <td>Assembler サービスは、PDFGenerator、Formsおよび Output サービスがサポートするすべての入力ファイル形式を、出力ファイル形式としてサポートします。 </td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-" target="_blank">toPDFA</a></td> 
   <td>指定したオプションを使用して、指定したドキュメントをPDF/A に変換します。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Assembler サービスの invoke API は、入力に応じて別のサービスの課金対象 API を内部的に呼び出すことができます。 したがって、呼び出し API は、なし、単一または複数のトランザクションとして計上できます。 カウントされるトランザクションの数は、入力と呼び出される内部 API によって異なります。
>* Assembler サービスを使用して生成された単一のPDFドキュメントは、なし、単一または複数のトランザクションとして計上できます。 カウントされるトランザクションの数は、指定された DDX コードによって異なります。

>


### PDFユーティリティサービス  {#pdf-utility-service}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td> 
   <td>PDFドキュメントを XDP ファイルに変換します。 PDFドキュメントを XDP ファイルに正しく変換するには、PDFドキュメントに AcroForms ディクショナリ内の XFA ストリームが含まれている必要があります。</td> 
   <td>処理済みドキュメント</td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

### Doc Assurance サービス {#doc-assurance-service}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/docassurance/client/api/DocAssuranceService.html#secureDocument-com.adobe.aemfd.docmanager.Document-com.adobe.fd.docassurance.client.api.EncryptionOptions-com.adobe.fd.docassurance.client.api.SignatureOptions-com.adobe.fd.docassurance.client.api.ReaderExtensionOptions-com.adobe.fd.signatures.pdf.inputs.UnlockOptions-">secureDocument</a></td> 
   <td>API を使用すると、ドキュメントを保護できます。 API を使用して、PDFドキュメントの署名、認証、Reader 用の拡張、暗号化を行うことができます。 </td> 
   <td>処理済みドキュメント</td> 
   <td>の操作の署名と認証のみ <a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/docassurance/client/api/DocAssuranceService.html#secureDocument-com.adobe.aemfd.docmanager.Document-com.adobe.fd.docassurance.client.api.EncryptionOptions-com.adobe.fd.docassurance.client.api.SignatureOptions-com.adobe.fd.docassurance.client.api.ReaderExtensionOptions-com.adobe.fd.signatures.pdf.inputs.UnlockOptions-">secureDocument</a> が請求されます。</td> 
  </tr>
 </tbody>
</table>

## 課金対象のデータキャプチャ API {#billable-data-capture-apis}

アダプティブフォーム、HTML5 Formsおよびフォームセットのすべての送信イベントは、トランザクションとして計上されます。 デフォルトでは、トランザクションフォームのPDFはトランザクションとして計上されません。 提供された [トランザクションレポート API](record-transaction-custom-implementation.md) トランザクションとしてPDF formsの送信を記録する。

### アダプティブフォーム {#adaptive-forms}

<table> 
 <tbody>
  <tr>
   <td><p>ユースケース</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td>アダプティブフォームの送信</td> 
   <td>アダプティブフォームを設定済みの送信アクションに送信します。 </td> 
   <td>送信済みフォーム</td> 
   <td>
    <ul> 
     <li>送信が成功した場合、1 つまたは 2 つのトランザクションが考慮されます。 カウントされるトランザクションの数は、送信に使用する送信アクションのタイプによって異なります。 例えば、電子メール送信アクションを使用したPDFの送信は、2 回のトランザクション数を考慮します。 フォーム送信用のトランザクションと、レコードのドキュメント (DOR) サービスを使用してPDFが生成されるトランザクションです。 </li> 
     <li>アダプティブフォーム（アダプティブフォームフォームセット）内でアダプティブフォームを使用すると、1 回のトランザクションのみが考慮されます。 アダプティブフォーム内には、任意の数のアダプティブフォームを含めることができます。</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

### HTML5 のフォーム {#html-forms}

<table> 
 <tbody>
  <tr>
   <td><p>ユースケース</p> </td> 
   <td>説明 </td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td>HTML5 フォームの送信</td> 
   <td>フォームで設定された URL を送信するためにHTML5 フォームを送信します。</td> 
   <td>送信済みフォーム</td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

### フォームセット {#form-set}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td>フォームセットの送信</td> 
   <td>フォームセットを、フォームセットで設定された送信 URL に送信します。</td> 
   <td>送信済みフォーム</td> 
   <td>
    <ul> 
     <li>アダプティブフォーム（アダプティブフォームフォームセット）内でアダプティブフォームを使用すると、1 回のトランザクションのみが考慮されます。 アダプティブフォーム内には、任意の数のアダプティブフォームを含めることができます。</li> 
     <li>HTML5 Formsフォームセット内の各フォームは、別々のトランザクションとしてアカウントされます。 </li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

## OSGi API 上の課金対象のインタラクティブ通信とフォーム中心のAEMワークフロー {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

OSGi 上の Form 中心のAEM Workflows のタスクとドキュメントサービスのステップと、インタラクティブ通信のすべてのレンディションを割り当てます。これらはトランザクションとして計上されます。 オーサーインスタンス上でインタラクティブ通信をプレビューし、エージェント UI を使用してパブリッシュインスタンス上でプレビューすることは、トランザクションとしては考慮されません。 ワークフローステップでトランザクションが考慮され、ワークフローの完了に失敗した場合、トランザクション数は元に戻されません。

### インタラクティブ通信 - Web チャネル {#interactive-communication-web-channel}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td>Web チャネルのレンダリング</td> 
   <td>インタラクティブ通信の Web バージョンを開きます。</td> 
   <td>レタリング済みドキュメント</td> 
   <td>
    <div> 
    </div> </td> 
  </tr>
 </tbody>
</table>

### インタラクティブ通信 — 印刷チャネル {#interactive-communication-print-channel}

<table> 
 <tbody>
  <tr>
   <td><p>API</p> </td> 
   <td>説明</td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">レンダー</a> ( 変換してPDF)</td> 
   <td>インタラクティブPDFの通信バージョンを生成します。</td> 
   <td>レタリング済みドキュメント</td> 
   <td>
    <div> 
    </div> </td> 
  </tr>
 </tbody>
</table>

### OSGi 上のフォームベース AEM ワークフロー  {#form-centric-aem-workflows-on-osgi}

<table> 
 <tbody>
  <tr>
   <td><p>使用例</p> </td> 
   <td>トランザクションレポートカテゴリ</td> 
   <td>追加情報</td> 
  </tr>
  <tr>
   <td>タスクの割り当てステップの送信</td> 
   <td>送信済みフォーム</td> 
   <td>
    <div> 
    </div> </td> 
  </tr>
  <tr>
   <td>ワークフローアプリケーションのスタートポイントの送信 </td> 
   <td>送信済みフォーム</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>エージェント UI からワークフローへのインタラクティブ通信（印刷チャネル）の送信</td> 
   <td>レタリング済みドキュメント</td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

## カスタムコードのトランザクションとしての課金対象 API の記録 {#recording-billable-apis-as-transactions-for-custom-code}

PDFフォームの送信、エージェント UI によるインタラクティブ通信のプレビュー、非標準のフォーム送信、カスタム実装のトランザクションとしての対応は考慮されません。 AEM Formsは、トランザクションなどのアクションを記録する API を提供します。 カスタム実装から API を呼び出して、 [取引を記録する](https://www.bdnsw.gov.bn/PublishingImages/page-under-construction.jpg).

## 関連記事 {#related-articles}

* [トランザクションレポートの概要](/help/forms/using/transaction-reports-overview.md)
* [取引レポートの表示と理解](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [カスタム実装のトランザクションの記録](/help/forms/using/record-transaction-custom-implementation.md)
