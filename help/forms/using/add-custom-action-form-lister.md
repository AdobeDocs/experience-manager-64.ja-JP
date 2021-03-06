---
title: フォームリスター項目にカスタムアクションボタンを追加
seo-title: Adding custom action on form lister items
description: フォーム開発者は、フォームポータルページでフォームのリストに詳細アクションを追加できます。デフォルトでは、フォームリストはフォームにアクセス、入力および送信することができます。
seo-description: Form developers can add more actions to the listing of forms on the forms portal page. By default, the form listing allows you to access the form, fill it, and submit it.
uuid: 02c64f7d-f726-4a5b-a303-ec96934e9c01
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
discoiquuid: 0e0a9b6b-fd2f-4cec-b233-500c940ee4d5
exl-id: d8f60be3-474a-4dd1-aaa5-7b6a97e1a9bd
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 100%

---

# フォームリスター項目にカスタムアクションボタンを追加 {#adding-custom-action-on-form-lister-items}

AEM Forms では、使用可能なフォームをリストしたポータルページを作成できます。デフォルトの設定では、ポータルページで検索したりフォームをリストしたりできます。フォームを開いて、情報を入力および送信することができます。レンダリングアクションのみポータルページにリストされているフォームにデフォルトで提供されています。ポータルページの利用可能なアクションの詳細については、[フォームポータルページの作成](/help/forms/using/creating-form-portal-page.md)を参照してください。

ポータルページには、その他のオプションも追加することができます。フォームポータルのテンプレートをカスタマイズすることで、これらのオプションをカスタマイズできます。

この記事は、フォームポータルページから直接フォームのリンクを送信するボタンの作成方法を示します。このカスタマイズは、Search &amp; Listerコンポーネントのテンプレートのアップデートを必要とします。

テンプレートにアクションを追加するのに必要なコードは以下の通りです。コードスニペットの `onclick` 属性にはメールでフォームのリンクを送信するスクリプトがあります。

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

カスタムテンプレートで同様のアクションを追加できます。JavaScript関数を定義するには、その機能をページレベルで追加して、必要なHTML要素にリンクします。上記の例では、`onclick` 式はリンク関数です。

テンプレートに編集を行った後、サンプルのポータルページには、以下のようにフォームのリンクをメールで送信するボタンが含まれています。

![メール](assets/email.png)
