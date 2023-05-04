---
title: フォームリスター項目にカスタムアクションボタンを追加
seo-title: Adding custom action on form lister items
description: フォーム開発者は、フォームポータルページ上のフォームのリストに、さらにアクションを追加できます。 デフォルトでは、フォームリストを使用すると、フォームにアクセスし、入力して送信できます。
seo-description: Form developers can add more actions to the listing of forms on the forms portal page. By default, the form listing allows you to access the form, fill it, and submit it.
uuid: 02c64f7d-f726-4a5b-a303-ec96934e9c01
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
discoiquuid: 0e0a9b6b-fd2f-4cec-b233-500c940ee4d5
exl-id: d8f60be3-474a-4dd1-aaa5-7b6a97e1a9bd
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 31%

---

# フォームリスター項目にカスタムアクションボタンを追加 {#adding-custom-action-on-form-lister-items}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Formsでは、使用可能なフォームをリストするポータルページを作成できます。 デフォルトでは、ポータルページ上のフォームを検索してリストすることができます。 フォームを開いて、情報を入力し、送信することができます。 ポータルページにリストされたフォームでは、レンダリングアクションのみが標準で提供されます。 ポータルページの利用可能なアクションの詳細については、[フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)を参照してください。

ポータルページに他のオプションを追加できます。 フォームポータルのテンプレートをカスタマイズすることで、これらのオプションやアクションをカスタマイズできます。

この記事では、フォームポータルページから直接フォームのリンクを送信するボタンを作成する方法を説明します。 このカスタマイズを行うには、Search &amp; Lister コンポーネントのテンプレートを更新する必要があります。

テンプレートにアクションを追加するために必要なコードは、以下で使用できます。 コードスニペットの `onclick` 属性にはメールでフォームのリンクを送信するスクリプトがあります。

```mxml
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
  <div class="__FP_boxes-thumbnail">
            <img src ="${contextPath}${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png">
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">Apply</a>
                <a class="__FP_button" title="Email a friend" href="#" onclick="javascript:window.location=&apos;mailto:?subject=Interesting information&body=I thought you might find {name} form helpful :  &apos;+window.location.protocol+window.location.host+&apos;${formUrl}&apos; ;">Email</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">Download</a>
            </div>
        </div>
    </div>
</div>
```

カスタムテンプレートに同様のアクションを追加できます。 JavaScript 関数を定義するには、ページレベルのスクリプトに関数を追加し、必要なHTML要素にリンクします。 上記の例では、`onclick` 式はリンク関数です。

テンプレートに編集を行った後、サンプルのポータルページには、以下のようにフォームのリンクをメールで送信するボタンが含まれています。

![メール](assets/email.png)
