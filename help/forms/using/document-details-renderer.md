---
title: レンダラーのドキュメントの詳細
seo-title: Document details for renderer
description: AEM Forms Workspace でのレンダリングがサポートされている様々なフォームやファイルタイプをレンダリングする方法に関する概念情報です。
seo-description: Conceptual information on how renders work in AEM Forms workspace to render the various supported form and file types.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 192ba4c4-a133-4e16-9882-98005f25ba7f
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 51%

---

# レンダラーのドキュメントの詳細 {#document-details-for-renderer}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## はじめに {#introduction}

AEM Forms Workspace では、複数のフォームタイプをシームレスにサポートします。 次の機能が含まれます。

* PDF forms(XDP、Acroform、フラットPDF)
* 新規HTMLフォーム
* 画像
* サードパーティアプリケーション（Correspondence Management など）

このドキュメントでは、セマンティックのカスタマイズ/コンポーネントの再利用の観点から、これらのレンダラーの動作を説明し、レンディションを壊すことなく、顧客の要件を満たすようにします。 AEM Forms Workspace では、ユーザーインターフェイスおよびセマンティックの変更が可能ですが、異なるフォームタイプのレンダリングロジックは変更しないことをお勧めします。変更してしまうと、予測外の結果になる場合があります。このドキュメントは、異なるポータルで同じワークスペースコンポーネントを使用し、同じフォームのレンダリングをサポートするガイダンス/知識を提供するためのもので、レンダリングロジック自体を変更するためのものではありません。

## PDF forms {#pdf-forms}

PDF フォームは `PdfTaskForm View` でレンダリングされます。

XDP フォームが PDF としてレンダリングされると、FormsAugmenter サービスは `FormBridge` JavaScript™ を追加します。この JavaScript™ （PDF フォーム内）が、フォーム送信、フォーム保存、またはフォームをオフラインにするなどのアクションを実行する手助けをします。

AEM Forms Workspace では、PDFTaskForm 表示は、`/lc/libs/ws/libs/ws/pdf.html` にある仲介としての役割を果たす HTML 経由で `FormBridge` javascript と通信します。フローは次のとおりです。

**PDFTaskForm 表示 — pdf.html**

`window.postMessage`／`window.attachEvent('message')` を使用した通信

この方法は、親フレームと iframe 間の標準的な通信方法です。 以前に開いたイベントの既存のPDF formsリスナーは、新しく追加する前に削除されます。 このパージでは、タスクの詳細ビューでのフォームタブと履歴タブの切り替えも考慮されます。

**pdf.html - `FormBridge`レンダリングされた PDF 内の javascript**

`pdfObject.postMessage`／`pdfObject.messageHandler` を使用した通信

この方法は、HTMLからPDFJavaScript との標準的な通信方法です。 PdfTaskForm 表示では、フラットPDFも処理し、単純にレンダリングします。

>[!NOTE]
>
>pdf.html / PdfTaskForm 表示のコンテンツを変更することはお勧めしません。

## 新しいHTMLForms {#new-html-forms}

新しいHTMLフォームは、NewHTMLTaskForm ビューによってレンダリングされます。

XDP フォームが CRX にデプロイされた mobile forms パッケージを使用してHTMLとしてレンダリングされると、追加のフォームも追加されます `FormBridge` javascript をフォームに追加することで、フォームデータの保存と送信のための様々な方法を公開できます。

この JavaScript は、上記のPDF formsとは異なりますが、同じ目的を果たします。

>[!NOTE]
>
>NewHTMLTaskForm 表示の内容は変更しないことをお勧めします。

## Flex Formsとガイド {#flex-forms-and-guides}

Flex Formsは SwfTaskForm でレンダリングされ、ガイドは HtmlTaskForm ビューでレンダリングされます。

AEM Forms Workspace では、これらの表示は実際の SWF と通信します。これにより、`/lc/libs/ws/libs/ws/WSNextAdapter.swf` にある仲介としての役割を果たす SWF を使用して Flex フォーム／ガイドを作成します。

通信は `swfObject.postMessage`／`window.flexMessageHandler` を使用して行われます。

このプロトコルは `WsNextAdapter.swf` によって定義されています。ウィンドウオブジェクトの既存の `flexMessageHandlers` は、新しく追加される前に、以前に開いていた SWF フォームから削除されます。このロジックでは、タスクの詳細表示でフォームタブと履歴タブを切り替えることも考慮しています。`WsNextAdapter.swf` は、保存や送信などの様々なフォームアクションの実行に使用されます。

>[!NOTE]
>
>`WSNextAdapter.swf` または SwfTaskForm / HtmlTaskForm 表示の内容を変更することはお勧めしません。

## サードパーティアプリケーション（Correspondence Management など） {#third-party-applications-for-example-correspondence-management}

サードパーティアプリケーションは、ExtAppTaskForm ビューを使用してレンダリングされます。

**サードパーティアプリケーションから AEM Forms Workspace への通信**

AEM Forms Workspace は `window.global.postMessage([Message],[Payload])` をリッスンします。

[Message] は、`runtimeMap` で `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage` として指定される文字列にすることができます。サードパーティアプリケーションが必要に応じて AEM Forms Workspace に通知するには、このインターフェイスを使用する必要があります。AEM Forms Workspace がタスクウィンドウをクリーンアップするには、タスクが送信されたことを知る必要があるため、このインターフェイスの使用は必須です。

**AEM Forms Workspace からサードパーティアプリケーションへの通信**

AEM Forms Workspace の直接アクションボタンが表示されている場合は、`window.[External-App-Name].getMessage([Action])` を呼び出します。この際、`[Action]` は `routeActionMap` から読み取られます。サードパーティアプリケーションは、このインターフェイスをリッスンして `postMessage ()` API 経由で AEM Forms Workspace に通知する必要があります。

例えば、Flex アプリケーションは、この通信をサポートするために `ExternalInterface.addCallback('getMessage', listener)` を定義することができます。サードパーティアプリケーションで独自のボタンを使用してフォーム送信を処理する場合は、`hideDirectActions = true() in the runtimeMap` を指定する必要があり、そうするとリスナーをスキップすることができます。したがって、この構文はオプションです。

Correspondence Management に関するサードパーティアプリケーションの統合について詳しくは、 [AEM Forms Workspace での Correspondence Management の統合](/help/forms/using/integrating-correspondence-management-html-workspace.md).
