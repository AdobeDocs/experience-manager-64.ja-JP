---
title: AEM Formsプロセスについて
seo-title: Understanding AEM Forms Processes
description: AEM Formsビジネスプロセスを使用して操作を自動化する方法を説明します。 プロセスをアクティブ化してサービスを作成し、他のサービスと同様に呼び出せるようにします。 プロセスは、短時間のみ有効でも長期間有効でもかまいません。
seo-description: Learn how to use AEM Forms business processes to automate operations. Activate the processes to create a service so that you can invoke it like other services. Processes can be short-lived or long-lived.
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
role: Developer
exl-id: 0ae0ddbf-ded6-4494-bf94-bf6cf7f1fd46
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 2%

---

# AEM Formsプロセスについて {#understanding-aem-forms-processes}

一般的な使用例としては、一連のAEM Formsサービスが単一のドキュメントを操作する場合が考えられます。 Workbench を使用してプロセスを作成することで、サービスコンテナにリクエストを送信できます。 プロセスとは、自動化するビジネスプロセスを表します。 プロセスの作成について詳しくは、 [Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63).

プロセスがアクティブ化されると、そのプロセスはサービスになり、他のサービスと同様に呼び出すことができます。 Encryption サービスなどの標準サービスと、プロセスから生成されたサービスの違いの 1 つは、後者には多くのアクションを実行する 1 つの操作があるという点です。 これに対し、標準のサービスには多くの操作があります。 通常、各操作は 1 回の操作（ドキュメントへのポリシーの適用やドキュメントの暗号化など）を実行します。

プロセスは、短時間のみ有効でも長期間有効でもかまいません。 短時間のみ有効なプロセスとは、呼び出し元の同じ実行スレッドで同期的に実行される操作です。 短時間のみ有効な操作は、ほとんどのプログラミング言語で見られる標準的な動作に相当します。クライアントアプリケーションはメソッドを呼び出し、戻り値を待ちます。

ただし、次のような要因により、プロセスを同期的に完了できない場合があります。

* 1 つのプロセスが長い時間を要する場合があります。
* プロセスは、組織の境界にまたがることができます。
* プロセスを完了するには、外部入力が必要です。 例えば、不在のマネージャーにフォームが送信される場合を考えてみます。 この場合、マネージャーがフォームに戻って入力するまで、プロセスは完了しません。

   これらのタイプのプロセスは、長期間有効なプロセスと呼ばれます。 長期間有効なプロセスは非同期で実行され、リソースが許可するとシステムがやり取りし、操作の追跡と監視を可能にします。 長期間有効なプロセスが呼び出されると、AEM Formsは、長期間有効なプロセスのステータスを追跡するレコードの一部として呼び出し識別子の値を作成します。 レコードはAEM Formsデータベースに保存されます。 長期間有効なプロセスレコードは、不要になった場合にパージできます。

>[!NOTE]
>
>AEM Formsは、短時間のみ有効なプロセスが呼び出された場合、レコードを作成しません。

呼び出し識別子の値を使用して、長期間有効なプロセスのステータスを追跡できます。 例えば、プロセス呼び出し識別子の値を使用して、実行中のプロセスインスタンスの終了など、Process Manager の操作を実行できます。

**短時間のみ有効なプロセスの例**

以下の図は、という名前の短時間のみ有効なプロセスの例です。 *MyApplication/EncryptDocument*.

>[!NOTE]
>
>このプロセスは、既存の AEM Forms プロセスに基づいていません。このプロセスを呼び出す方法を説明するコード例に従うには、という名前のプロセスを作成します。 `MyApplication/EncryptDocument` Workbench の使用を参照してください。 （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

この短時間有効なプロセスが呼び出されると、次のアクションが実行されます。

1. プロセスに渡されたPDFドキュメントを入力値として取得します。
1. PDF ドキュメントをパスワードで暗号化します。このプロセスの入力パラメーターの名前は、 `inDoc` データタイプは document です。
1. パスワードで暗号化されたPDF・ドキュメントをPDF・ファイルとしてローカル・ファイル・システムに保存します。 このプロセスは、暗号化されたPDFドキュメントを出力値として返します。 このプロセスの出力パラメーターの名前は、 `outDoc` データタイプは document です。

   このプロセスは、呼び出された同じ実行スレッドで同期的に完了します。 この短時間のみ有効なプロセスの名前は、 `MyApplication/EncryptDocument`そしてその動作は `invoke`.

   >[!NOTE]
   >
   >通常、短時間のみ有効なプロセスは 3 つ以上のアクションで構成されます。 Workbench を使用してプロセスを作成します。 （[Workbench の使用](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照。）

   *AEM forms によるプログラミング*&#x200B;では、この短時間のみ有効なプロセスをプログラムで呼び出す方法について説明します。

   * [AEM Forms Remoting を使用して保護されていないドキュメントを渡すことによる、短時間のみ有効なプロセスの呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (Flexアプリケーションの使用 )
   * [呼び出し API を使用した短時間のみ有効なプロセスの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) （Java 呼び出し API）
   * [Base64 エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) （Web サービスの例）
   * [MTOM を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) （Web サービスの例）
   * [SwaRef を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) （Web サービスの例）
   * [HTTP 経由での BLOB データを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) （Web サービスの例）
   * [DIME を使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) （Web サービスの例）
   * [REST を使用した MyApplication/EncryptDocument プロセスの呼び出し](/help/forms/developing/invoking-aem-forms-using-rest.md)

**長期間有効なプロセスの例**

次の図は、長期間有効なプロセスの例です。

このプロセスは、申込者がローンフォームを送信すると呼び出されます。 ローン担当者がローン申し込みを承認または却下するまで、処理は完了しません。 この長期間有効なプロセスの名前は* FirstAppSolution/PreLoanProcess *で、操作は `invoke_Async`. このプロセスは非同期で呼び出す必要があります。 この長期間有効なプロセスをプログラムで呼び出す方法については、 [人間中心の長期間有効なプロセスの呼び出し](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>このプロセスは、 [最初のAEM Formsアプリケーションの作成](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).
