---
title: レンダラーのためのドキュメントの詳細
seo-title: Document details for renderer
description: サポートされる様々なフォームやファイルタイプをレンダリングする AEM Forms Workspace のレンダーの動作方法についての概念情報。
seo-description: Conceptual information on how renders work in AEM Forms workspace to render the various supported form and file types.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 192ba4c4-a133-4e16-9882-98005f25ba7f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 64%

---

# レンダラーのためのドキュメントの詳細 {#document-details-for-renderer}

## はじめに {#introduction}

AEM Forms Workspace では、複数のフォームタイプをシームレスにサポートしています。次の機能が含まれます。

* PDF フォーム（XDP / Acroform / Flat PDF）
* 新規 HTML フォーム
* 画像
* サードパーティアプリケーション（たとえば、Correspondence Management など）

このドキュメントでは、表示を中断することなく顧客の要件を満たすように、セマンティックカスタマイゼーションおよびコンポーネントの再利用の観点からこれらのレンダラーの動作を説明します。AEM Forms Workspace ではユーザーインターフェイスやセマンティックの変更が可能ですが、様々なフォームタイプのレンダリングロジックは変更しないことをお勧めします。そうしないと、予測できない結果が生じる場合があります。 このドキュメントは、別々のポータルで同じワークスペースコンポーネントを使用する、同じフォームのレンダリングをサポートするためのガイド／ナレッジであり、レンダリングロジック自体を変更するためのものではありません。

## PDF フォーム {#pdf-forms}

PDF formsは `PdfTaskForm View`.

XDP フォームが PDF としてレンダリングされると、FormsAugmenter サービスは `FormBridge` JavaScript™ を追加します。この JavaScript™ （PDF フォーム内）が、フォーム送信、フォーム保存、またはフォームをオフラインにするなどのアクションを実行する手助けをします。

AEM Forms Workspace では、PDFTaskForm ビューは `FormBridge`javascript( にある中間HTML経由 ) `/lc/libs/ws/libs/ws/pdf.html`. フローを以下に示します。

**PDFTaskForm 表示 - pdf.html**

次を使用する通信 `window.postMessage` / `window.attachEvent('message')`

このメソッドは、親フレームと I フレーム間の標準的な通信方法です。以前に開いていた PDF フォームからの既存のイベントリスナーは、新しく追加する前に削除されます。この削除では、タスクの詳細表示でフォームタブと履歴タブを切り替えることも考慮しています。

**レンダリングされた PDF 内の pdf.html - `FormBridge` javascript**

次を使用する通信 `pdfObject.postMessage` / `pdfObject.messageHandler`

このメソッドは、HTML からの PDF javascript との標準的な通信方法です。PdfTaskForm 表示は、フラット PDF にも対応していて、平面的にレンダリングします。

>[!NOTE]
>
>pdf.html / PdfTaskForm 表示の内容はを変更しないことをお勧めします。

## 新規 HTML フォーム {#new-html-forms}

新規 HTML フォームは、NewHTMLTaskForm 表示によってレンダリングされます。

XDP フォームが CRX にデプロイされたモバイルフォームのパッケージを使用して HTML としてレンダリングされた場合は、追加の `FormBridge` javascript もフォームに追加します。これは、フォームデータを保存して送信するのに異なるメソッドを示します。

この javascript は上記の PDF フォームで言及したものとは異なりますが、同じ用途に使用できます。

>[!NOTE]
>
>NewHTMLTaskForm ビューのコンテンツを変更することはお勧めしません。

## Flex フォームおよびガイド {#flex-forms-and-guides}

Flex フォームは SwfTaskForm によってレンダリングされ、ガイドは HtmlTaskForm 表示によってレンダリングされます。

AEM Forms Workspace では、これらの表示は、にある中間SWFを使用して Flex フォーム/ガイドを構成する実際のSWFと通信します。 `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

通信は `swfObject.postMessage` / `window.flexMessageHandler`.

このプロトコルは `WsNextAdapter.swf` によって定義されています。ウィンドウオブジェクトの既存の `flexMessageHandlers` は、新しく追加される前に、以前に開いていた SWF フォームから削除されます。このロジックでは、タスクの詳細表示でフォームタブと履歴タブを切り替えることも考慮しています。`WsNextAdapter.swf` は、保存や送信などの様々なフォームアクションの実行に使用されます。

>[!NOTE]
>
>`WSNextAdapter.swf` または SwfTaskForm / HtmlTaskForm 表示の内容を変更することはお勧めしません。

## サードパーティアプリケーション（たとえば、Correspondence Management など） {#third-party-applications-for-example-correspondence-management}

サードパーティアプリケーションは、ExtAppTaskForm 表示を使用してレンダリングされます。

**AEM Forms Workspace との通信に対するサードパーティアプリケーション**

AEM Forms workspace のリッスン `window.global.postMessage([Message],[Payload])`

[メッセージ] は、 `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`内 `runtimeMap`. サードパーティアプリケーションは、必要に応じてAEM Forms Workspace に通知するには、このインターフェイスを使用する必要があります。 AEM Forms Workspace はタスクウィンドウをクリーンアップできるように、タスクの送信時を知っている必要があるので、このインターフェイスの使用は必須です。

**AEM Forms workspace とサードパーティアプリケーションとの通信**

AEM Forms Workspace の直接アクションボタンが表示されている場合は、を呼び出します。 `window.[External-App-Name].getMessage([Action])`で、 `[Action]` が `routeActionMap`. サードパーティアプリケーションは、このインターフェイスをリッスンして、 `postMessage ()` API

例えば、Flexアプリケーションは `ExternalInterface.addCallback('getMessage', listener)` この通信をサポートするために。 サードパーティアプリケーションが独自のボタンを使用してフォームの送信を処理する場合は、次を指定する必要があります `hideDirectActions = true() in the runtimeMap` この聞き手をスキップしてもかまいません。 従って、この構築はオプションです。

サードパーティアプリケーションの Correspondence Management との統合の詳細については、「[AEM Forms Workspace での Correspondence Management の統合](/help/forms/using/integrating-correspondence-management-html-workspace.md)」を参照してください。
