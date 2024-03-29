---
title: Designer でのページゼロコンテンツの変更
seo-title: Changing Page Zero content in Designer
description: XFAPDFをAdobe PDF以外のビューアで表示するときに、XFA メッセージの Page Zero に表示されるメッセージを変更する方法を知っていますか？
seo-description: Do you know how you can change the message displayed on Page Zero of an XFA PDF when viewing it in a non-Adobe PDF viewer?
uuid: 5697f203-bb24-437d-a692-bc4bc2609b88
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: f458054e-885c-4c7a-afcd-ad1e4465e0c1
feature: Adaptive Forms
exl-id: 0ae34ddd-9a8d-48df-af2d-80c3fe6abd62
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 39%

---

# Designer での Page Zero コンテンツの変更 {#changing-page-zero-content-in-designer}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Chrome や Firefox のデフォルトのPDFビューアなど、Adobe PDF以外のビューアでPDF/XFA フォームのコンテンツを読み取れない場合は、Page Zero コンテンツがデフォルトで表示されます。 デフォルトの Page Zero メッセージは、以下のとおりです。

![defaultpage0message](assets/defaultpage0message.png)

AEM Forms Feature Pack 1 バージョンの Designer では、Page Zero に表示されるメッセージを変更できます。 Page Zero メッセージを変更するには、以下の手順を実行します。

1. AEM Forms Feature Pack 1 バージョンの Designer がインストールされていることを確認します。 Designer のバージョン情報画面で、バージョンを確認できます。

1. Page Zero コンテンツを変更するフォームを開きます。

1. **ファイル／フォームのプロパティ**&#x200B;をクリックします。

1. フォームのプロパティダイアログで、![プラス](assets/plus.png)（プラスアイコン）をクリックしてカスタムプロパティを追加します。

1. 指定 **_pagezerocontent** をプロパティの名前として設定します。
1. 新しい Page Zero メッセージをリッチテキスト形式で値として追加します。 以下に例を示します。

   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/acrreader.</p></body>`

1. フォームを PDF として保存します。

1. PDF フォームをブラウザーで表示して、メッセージが更新されたことを確認します。前述の例は、以下のように表示されます。

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>作成したカスタムプロパティは、フォームを再度開いたときに、フォームのプロパティダイアログに正しく表示されない場合があります。 ただし、正常に機能し、フォームに更新された Page Zero メッセージが表示されます。
