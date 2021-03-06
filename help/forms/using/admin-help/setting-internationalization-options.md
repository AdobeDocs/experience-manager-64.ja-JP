---
title: 国際化対応オプションの設定
seo-title: Setting internationalization options
description: フォームのレンダリングに使用するロケールの指定方法と、出力ストリームのエンコードに使用する文字セットの指定方法について説明します。
seo-description: Learn how to specify the locale used to render forms and how to specify the character set used to encode the output stream.
uuid: bb77f5f3-634f-4285-9b10-c4dd40085e69
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: e845d13f-bef2-442d-af9a-4f92d7616a46
exl-id: 1fb51e4a-e0e8-4a58-8877-98337fe29fac
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 100%

---

# 国際化対応オプションの設定{#setting-internationalization-options}

## フォームのレンダリングに使用するロケールの指定 {#specify-the-locale-used-to-render-forms}

PDF フォームをレンダリングする際に使用するロケールを指定できます。PDF フォーム上のフィールドでは、データの表示に対して指定されたロケールが使用されます。例えば、ロケールがドイツ語に設定されている場合、フォームでは、数値に対してドイツ語での小数点記号が使用されます。ロケールは、Web ブラウザーなどのクライアントデバイスに、HTML 変換の一部として検証メッセージを送信する場合にも使用されます。

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「国際化対応」の「言語」リストで、フォームのレンダリングに使用するロケールを選択します。デフォルト値は「英語（米国）」です。
1. 「保存」をクリックします。

## 出力ストリームのエンコードに使用する文字セットの指定 {#specify-the-character-set-used-to-encode-the-output-stream}

1. 「国際化対応」の「文字セット」リストで、文字セットを選択します。この設定は、使用する API（renderHTMLForm または renderPDFForm）によって異なります。リストにない文字セットを指定するには、「カスタム」を選択し、表示されたボックスでエンコーディング値を指定します。

   HTML の変換について AEM Forms で使用できるエンコーディング値は、`java.nio.charset` パッケージで定義されています。sFormPreference が PDFForm の場合は、特定の文字セットのみがサポートされます。文字セットは、有効な正規名で指定する必要があります。デフォルト値は「ISO-8859-1」です。

1. 「保存」をクリックします。
