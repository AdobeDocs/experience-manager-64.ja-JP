---
title: フォームのフィールドのための文脈依存ヘルプの作成
seo-title: Authoring in-context help for form fields
description: AEM Formsでは、アダプティブフォームのフィールドやパネルに文脈依存ヘルプをテキストまたはビデオなどのリッチメディアとして追加できます。
seo-description: AEM Forms allows you to add in-context help to adaptive form fields and panels, as text or rich media, including videos.
uuid: 07427ddd-9d35-41f6-a807-0e418aade199
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: 893a72c7-d68f-464f-9765-ec2272189e58
feature: Adaptive Forms
exl-id: 0c761c0c-fbe4-4129-8a90-c4ef1127a762
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 63%

---

# フォームフィールド用の文脈依存ヘルプの作成 {#authoring-in-context-help-for-form-fields}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## はじめに {#introduction}

エンドユーザーがフォームに記入しているときに、特定のフォームフィールドへの記入方法がわからない場合があります。このような問題に対処するため、アダプティブフォームでは、テキストの追加や、フォームフィールドへの豊富な文脈依存ヘルプの追加がサポートされています。 これにより、フォーム入力エクスペリエンスを向上し、エンドユーザーにとっての曖昧さを回避することができます。

この記事では、アダプティブフォームのオーサリング中に文脈依存ヘルプを追加する方法について説明しますForms。

## 文脈依存ヘルプの追加 {#add-in-context-help}

文脈依存ヘルプは、サイドバーにある「プロパティ」タブの「ヘルプコンテンツ」セクションの次のオプションを使用して指定できます。

* [簡単な説明](/help/forms/using/authoring-in-field-help.md#p-short-description-p)
* [詳細な説明](/help/forms/using/authoring-in-field-help.md#p-long-description-p)

![フォームのフィールドのための文脈依存ヘルプ](assets/descriptions.png)

>[!NOTE]
>
>詳細な説明は簡単な説明をオーバーライドします。両方を指定した場合は、詳細な説明のみが表示されます。

### 簡単な説明 {#short-description}

簡単な説明フィールドは、フォームフィールドの記入に関する短く簡単なヒントを提供するためにあります。簡単な説明内で指定されたテキストは、フィールドの上にカーソルを移動させると、ツールヒントとして表示されます。

![フォームフィールドへの文脈依存ヘルプの追加の簡単な説明](assets/tooltip.png)

>[!NOTE]
>
>ヘルプテキストを常にフィールドの下に表示するには、「**簡単な説明を常に表示する**」を選択します。

![フィールドの下に永久的に表示される簡単な文脈依存ヘルプ](assets/short1.png)

### 詳細な説明 {#long-description}

「詳細な説明」フィールドを使って、文脈依存ヘルプに長いテキストを指定したり、ビデオなどのリッチメディアコンテンツを埋め込んだりすることができます。例えば、次の画像では文脈依存ヘルプとしてビデオを埋め込む方法を示しています。

![フォームフィールドのための文脈依存ヘルプとしてのリッチメディアの追加](assets/long-descriptions.png)

詳細な説明を追加すると、**が表示されますか？** アイコンがフィールドの隣に表示されます。アイコンをクリックすると、詳細な説明セクションに追加されたコンテンツが表示されます。

![リッチメディアを使用した文脈依存ヘルプの例](assets/photoshop.png)

### パネルレベルのヘルプ {#panel-level-help}

フォームフィールドの文脈依存ヘルプに加え、パネル編集ダイアログの「ヘルプコンテンツ」タブから、パネルレベルでヘルプを指定することができます。

![フォームパネルへの文脈依存ヘルプの追加](assets/panel-level-help.png)

パネルにヘルプを追加すると、**が表示されますか？** アイコンがパネルの説明の隣に表示されます。このアイコンをクリックすると、パネル編集ダイアログの「ヘルプコンテンツ」セクションに追加されたコンテンツが表示されます。

![フォームパネルレベルでの文脈依存ヘルプの例](assets/photoshop-1.png)
