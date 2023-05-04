---
title: 国際化対応オプションの設定
seo-title: Setting internationalization options
description: フォームのレンダリングに使用するロケールを指定する方法、および出力ストリームのエンコードに使用する文字セットを指定する方法について説明します。
seo-description: Learn how to specify the locale used to render forms and how to specify the character set used to encode the output stream.
uuid: bb77f5f3-634f-4285-9b10-c4dd40085e69
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: e845d13f-bef2-442d-af9a-4f92d7616a46
exl-id: 1fb51e4a-e0e8-4a58-8877-98337fe29fac
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 31%

---

# 国際化対応オプションの設定{#setting-internationalization-options}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## フォームのレンダリングに使用するロケールを指定します {#specify-the-locale-used-to-render-forms}

ロケールフォームのレンダリング時に使用するロケールをPDFできます。 PDFフォーム上のフィールドは、指定されたロケールを使用してデータを表示します。 例えば、ロケールがドイツ語に設定されている場合、フォームでは数値にドイツ語の小数点区切り文字が使用されます。 また、ロケールは、Web ブラウザーなどのクライアントデバイスに検証メッセージを、HTML変換の一部として送信する場合にも使用されます。

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「国際化対応」の「言語」リストで、フォームのレンダリングに使用するロケールを選択します。 デフォルト値は英語（米国）です。
1. 「保存」をクリックします。

## 出力ストリームのエンコードに使用する文字セットを指定します {#specify-the-character-set-used-to-encode-the-output-stream}

1. 「国際化対応」の「文字セット」リストで、文字セットを選択します。この設定は、renderHTMLForm または renderPDFForm のどちらかで、使用される API によって異なります。 リストにない文字セットを指定するには、「カスタム」を選択し、表示されたボックスでエンコーディング値を指定します。

   HTML の変換について AEM Forms で使用できるエンコーディング値は、`java.nio.charset` パッケージで定義されています。sFormPreference が PDFForm の場合は、特定の文字セットのみがサポートされます。文字セットは、有効な正規名である必要があります。 デフォルト値は ISO-8859-1 です。

1. 「保存」をクリックします。
