---
title: カスタム実装のトランザクションの記録
seo-title: Record a transaction for custom implementations
description: トランザクションとして自動的に計上されないアクションを記録するには、TransactionRecorder API を使用します
seo-description: Use the TransactionRecorder API to record actions which are not accounted as transactions automatically
uuid: a22b1a0b-7553-4a17-8fb4-a3bee97b4a98
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-manager
discoiquuid: 0d961630-573b-4c8e-902f-996f1d1265b6
exl-id: e97ecb77-96a0-44cf-8da9-1e85cc122011
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 88%

---

# カスタム実装のトランザクションの記録 {#record-a-transaction-for-custom-implementations}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

トランザクションとして自動的に計上されないアクションを記録するには、TransactionRecorder API を使用します

カスタムコードを使用すると、PDFフォームを送信したり、エージェント UI のプレビュー URL をエンドユーザーに送信してインタラクティブ通信をプレビューしたり、AEM Forms で使用できる送信メソッドの代わりにカスタムメソッドを使用してフォームを送信したりできます。前述の AEM Forms API のすべてのアクションとカスタム実装は、トランザクションとはみなされません。AEM Forms は、トランザクションなどのアクションを記録するために、[TransactionRecorder](https://helpx.adobe.com/experience-manager/6-4/forms/javadocs/com/adobe/aem/transaction/core/ITransactionRecorder.html) という API を備えています。

トランザクションを記録するには、 [標準 Sling サーブレット](https://helpx.adobe.com/experience-manager/using/custom-sling-servlets.html) を書き込み、サーブレットをクライアントから呼び出してトランザクションを記録します。AJAX またはその以外の標準的な方法を使用して、サーブレットを呼び出すことができます。

## サーバー側コードのサンプル {#sample-server-sided-code}

下のサンプルコードを使用すると、カスタム OSGi バンドルを使用して JAVA クラスから TransactionRecorder API を実行できます。

```java
import com.adobe.aem.transaction.core.ITransactionRecorder;
import com.adobe.aem.transaction.core.model.TransactionRecord;
import com.adobe.aem.transaction.core.exception.TransactionException;
import com.adobe.aem.transaction.core.FormsTransactionConstants;

@Reference
private ITransactionRecorder transactionRecorder;
 
doPost (SlingHttpServletRequest request, SlingHttpServletResponse response) {
    transactionRecorder.startContext();
    TransactionRecord txRecord = extractTxRecordFromRequest(request); //extract transaction relevant data from request
    try {
        bool success = doBillableWork();
        if (success) {
            transactionRecorder.recordTransaction(txRecord);
        }
    } catch (Exception e) {
        //exception handling
    } finally {
        transactionRecorder.endContext();
    }
}

//Here, it is assumed that txInfo is passed in Stringified json form in the ajax call (in data parameter). You can pass txInfo from client in any way that you find suitable.
private TransactionRecord extractTxRecordFromRequest(SlingHttpServletRequest request) {
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(request.getInputStream()));
    Map<String, Object> txDataMap = new HashMap<String, Object>();
    String txData = bufferedReader.readLine();
    JSONObject txInfo= new JSONObject(txData );
    try {
        String resourceType= txInfo.getString("resourceType");
        String transactionType = txInfo.getString("transactionType");
        Integer transactionCount = (Integer)txInfo.get("transactionCount");
        //Extract all the relevant tx record attributes similarly and pass them in Transaction Record constructor as per the java doc}
        return new TransactionRecord(transactionCount, transactionType, resourceType, ..);
    } catch (JSONException e) {
        //exception handling
    } finally {
        bufferedReader.close();
    }
}
```

## クライアントサイドコードのサンプル {#sample-client-side-code}

以下のサンプルコードを使用して、 `TransactionRecorder` API を持つサーブレットを

```
$.ajax({
   type: 'POST',
   url: url, //servlet url
   contentType: 'application/json; UTF-8',
   data: JSON.stringify({transactionCount : 1, 
                        transactionType: "SUBMIT",
                        resourceType: "FORM",
                        resourceSubType: "ADAPTIVE-FORM"}),
   success: successHandler,
   error: faultHandler
})
```

## 関連記事 {#related-articles}

* [トランザクションレポートの概要](/help/forms/using/transaction-reports-overview.md)
* [トランザクションレポートの表示と理解](/help/forms/using/viewing-and-understanding-transaction-reports.md)
* [トランザクションレポート請求可能 API](/help/forms/using/transaction-reports-billable-apis.md)
