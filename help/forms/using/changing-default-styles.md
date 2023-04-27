---
title: HTML5 フォームのデフォルトスタイルの変更
seo-title: Changing default styles of HTML5 forms
description: HTML5 フォームのスタイル設定は CSS に基づいています。 フォームのデフォルトのスタイルを変更できます。
seo-description: HTML5 forms styling is based on CSS. You can change the default styles of the form.
uuid: dab888b1-d1a9-4990-ab21-96570beafd26
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: a9ab5a78-2add-46e1-a8f2-444d0f25f43a
feature: Mobile Forms
exl-id: 74e54d96-e418-40aa-9b93-561fbdd6312d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 44%

---

# HTML5 フォームのデフォルトスタイルの変更 {#changing-default-styles-of-html-forms}

HTML5 のフォームはHTML5 機能を使用してレンダリングされ、レンダリングされたフォームのスタイル設定は CSS を使用しておこなわれます。 HTML5 フォームのデフォルトの外観は、PDFレンディションに似ています。 開発者は、カスタム CSS を使用して、HTML5 フォームのデフォルトの外観を変更できます。

この記事では、HTML5 フォームのスタイルを変更するための詳細手順を説明します。[スタイルの概要](/help/forms/using/css-styles.md)の記事では、HTML5 フォームのさまざまなスタイル設定を詳しく解説します。この記事に記載されている手順を実行する前に、「スタイルの概要」の記事を必ずお読みください。

次の 2 つの画像はデフォルトのスタイルとカスタマイズされたスタイルの違いを示しています。

![pictures-002-small](assets/pictures-002-small.png)

## フォームのスタイル設定 {#style-your-forms}

1. **カスタムスタイルを追加するプロファイルを選択**

   **https://&lt;server>:&lt;port>/crx/de** の URL で CRX DE インターフェイスにアクセスし、プロファイルを作成するか、既存のプロファイルを選択します。プロファイルの作成方法について学ぶには、[プロファイルの新規作成](/help/forms/using/custom-profile.md)を参照してください。

1. **HTML5 フォームのスタイル設定用の CSS スタイルシートの作成**

   プロファイルレンダラーを作成したフォルダーに移動し、CSS スタイルシートファイルを作成します。 以下の手順に従います。

   1. フォルダーを右クリックし、「 」を選択します。 **作成** -> **ファイルを作成** メニューから
   HTML5 フォーム内の特定のコンポーネントに対して作成する CSS クラスについては、 [スタイルの概要](/help/forms/using/css-styles.md).

1. **プロファイルレンダラーにスタイルシートを含める**

   CRX DE でプロファイルレンダラーページ（jsp ファイル）を開き、CSS ファイルを XFA クライアントライブラリのすぐ下のページに含めます。 次の手順を実行して、CSS ファイルをプロファイルに含めます。

   1. レンダラーページで次の行を検索します。

      &lt;cq:includeClientLib categories=&quot;xfaforms.profile&quot; />

   1. 次の行を上記の行の下に挿入して、スタイルシートを含めます。

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1.  ファイルを保存します。
