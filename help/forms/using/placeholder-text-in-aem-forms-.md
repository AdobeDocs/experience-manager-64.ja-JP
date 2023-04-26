---
title: AEM Forms のプレースホルダーテキスト
seo-title: Placeholder text in AEM Forms
description: プレースホルダーテキストは、コントロールに値がない場合にユーザーがデータ入力を容易にするためのものです。 値の例や、期待される形式の簡単な説明を指定できます。
seo-description: Placeholder text is intended to aid the user with data entry when the control has no value. It could be a sample value or a brief description of the expected format.
uuid: 553ed988-ad2c-4bdb-bf1e-332e48cf7dfa
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: 2d7367fa-6cb8-40a1-8566-1fd0d46fdfde
feature: Adaptive Forms
exl-id: 26a1a5f7-b4d4-4f38-81a4-5f2d39702138
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 61%

---

# AEM Forms のプレースホルダーテキスト {#placeholder-text-in-aem-forms}

プレースホルダーテキストは、単語または短いフレーズを表します。 これは、コントロールに値がない場合に、ユーザーのデータ入力を支援するためのものです。 プレースホルダーテキストには、サンプル値や、必要な形式の簡単な説明を指定できます。 プレースホルダーテキストはユーザーが値を入力する前に表示され、ユーザーが値を入力または選択すると削除されます。

>[!NOTE]
>
>プレースホルダーテキストを指定する場合、改行文字を含まない値にする必要があります。

![プレースホルダーテキストを伴う／伴わない日付コンポーネント](assets/dat-picker-place-holder-text.png)

**A.** プレースホルダーテキストを伴う日付コンポーネント **B.** プレースホルダーテキストを伴わない日付コンポーネント

AEM Forms では、パスワードボックス、日付選択、数値ボックス、テキストボックスフィールドでプレースホルダーテキストを使用できます。\
プレースホルダーテキストはネイティブの HTML5 日付ウィジェットには対応していません。プレースホルダーテキストを指定するには、以下のようにします。

1. プレースホルダーテキストをサポートするコンポーネントを右クリックし、 **編集**. コンポーネントを編集ダイアログボックスが表示されます。

1. 「**タイトルとテキスト**」タブを開きます。
1. **プレースホルダーテキストボックス**&#x200B;に単語または短い語句を指定します。「**OK**」をクリックします。

>[!NOTE]
>
>プレースホルダーテキストは Microsoft Internet Explorer 9 ではサポートされていません。
