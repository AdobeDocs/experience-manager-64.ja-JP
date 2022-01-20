---
title: Formsのレンダリング
seo-title: Rendering Forms
description: Formsサービスを使用して、通常 Designer で作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成します。 フォーム作成者は、Formsサービスが様々なブラウザー環境でPDF、SWFまたはHTMLでレンダリングする、単一のフォームデザインを開発できます。
seo-description: Use the Forms service to create interactive data capture client applications that validate, process, transform, and deliver forms typically created in Designer. Form authors can develop a single form design that the Forms service renders in PDF, SWF, or HTML in various browser environments.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: 61d63c89-26e8-4a50-b6a3-1bcf1a1b4c54
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# Formsのレンダリング {#rendering-forms}

**Formsサービスについて**

Formsサービスを使用すると、通常 Designer で作成されるフォームを検証、処理、変換および配信する、インタラクティブなデータキャプチャクライアントアプリケーションを作成できます。 フォーム作成者は、Formsサービスが様々なブラウザー環境でPDF、SWFまたはHTMLでレンダリングする、単一のフォームデザインを開発できます。

エンドユーザーがフォームを要求すると、クライアントアプリケーションがFormsサービスに要求を送信し、このサービスが適切な形式でフォームを返します。 Formsサービスは、要求を受け取るとすぐにデータをフォームデザインと結合し、目的の形式でフォームを配信します。 Form サービスの出力は、インタラクティブなフォーム ( 通常はPDFドキュメント ) です。 インタラクティブフォームを使用すると、ユーザーはフォーム上のフィールドに入力できます。

クライアントアプリケーションの種類に応じて、フォームをクライアント Web ブラウザーに書き込んだり、フォームをPDFファイルとして保存したりできます。 Web ベースのアプリケーションは、Web ブラウザーにフォームを書き込むことができます。 デスクトップアプリケーションは、フォームをPDFファイルとして保存できます。 Web ブラウザーとPDFファイルに書き出す方法を示すために、クイックスタートは *Formsのレンダリング* セクションは、次のように整理されます。

* Java API で厳密に型指定された（SOAP モード）の例は Java サーブレットです。
* Web サービス (Java Base64) の例は Java サーブレットです。
* Web サービス (MTOM) の例は、コンソールアプリケーションです（すべてのクイックスタートに MTOM の例があるわけではありません）。

   >[!NOTE]
   >
   >Java サーブレットを使用してFormsサービスを呼び出す Web アプリケーションの作成について詳しくは、 [Formsをレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md).

   次の 2 つの方法のいずれかを使用して、フォームデザイン（XDP ファイル）またはPDFドキュメントをFormsサービスに渡すことができます。

* URL 値を使用してフォームデザインを参照できます。 この方法では、 `URLSpec` オブジェクト。 コンテンツルートは、 `URLSpec` オブジェクトの `setContentRootURI` メソッド。 フォームデザイン名 ( `formQuery`) は別のパラメーターとして渡されます。 2 つの値が連結され、フォームデザインへの絶対参照が取得されます。 ( ほとんどのクイックスタートは、 *Formsのレンダリング* 節では、この方法を使用します )。
* 次の条件を満たす場合に、 `com.adobe.idp.Document` フォームデザインを含んだFormsサービスへの 次の 2 つの新しいメソッド： `renderPDFForm2` および `renderHTMLForm2` 受け入れる `com.adobe.idp.Document` フォームデザインを含むオブジェクト。 ( [Forms Service にドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

Formsサービスを使用して、次のタスクを実行できます。

* インタラクティブPDF formsのレンダリング ( [インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* クライアントでフォームをレンダリングします。 ( [クライアントでのFormsのレンダリング](/help/forms/developing/rendering-forms-client.md).)
* フラグメントに基づいてフォームをレンダリングする。( [フラグメントに基づくFormsのレンダリング](/help/forms/developing/rendering-forms-based-fragments.md).)
* 権限が有効なフォームをレンダリングします。 ( [レンダリング権限が有効なForms](/help/forms/developing/rendering-rights-enabled-forms.md).)
* フォームをHTMLとしてレンダリング ( [FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms-html.md).)
* カスタム CSS ファイル ([カスタム CSS ファイルを使用したHTMLFormsのレンダリング](/help/forms/developing/rendering-html-forms-using-custom.md).)
* 送信されたフォームを処理します。 ( [送信済みFormsの処理](/help/forms/developing/handling-submitted-forms.md).)
* 送信済み XML データを使用したPDFドキュメントの作成 ( [送信済み XMLPDFでのデータ・ドキュメントの作成](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* フォームの事前入力 ( [編集可能なレイアウトを使用したFormsの事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* ドキュメントを渡す。 ( [Forms Service にドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)
* フォームデータを計算します。 ( [フォームデータの計算](/help/forms/developing/calculating-form-data.md).)
* アプリケーションを最適化する。 ( [Forms Service のパフォーマンスの最適化](/help/forms/developing/optimizing-performance-forms-service.md).)

