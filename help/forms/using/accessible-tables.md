---
title: アクセス可能な複雑なテーブルを HTML5 フォームで作成する
seo-title: Create accessible complex tables in HTML5 forms
description: アクセシブルなテーブルを作成する方法については、HTML5 フォームを参照してください。
seo-description: Learn how to create accessible tables in HTML5 forms.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: Mobile Forms
exl-id: a3337bb1-635c-4dc9-b438-3a829d4a9e03
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 38%

---

# アクセス可能な複雑なテーブルを HTML5 フォームで作成する {#create-accessible-complex-tables-in-html-forms}

HTML5 Formsのテーブルのデフォルト実装では、HTMLDIV 要素を使用してテーブルをレンダリングします。 レンダリングでは、アクセシビリティ要件を満たすために ARIA ロールを使用する必要があります。

ARIA ロールとデータテーブルの組み合わせを完全にはサポートしていないスクリーンリーダーでアクセシビリティの問題が発生するのを防ぐには、HTML5 フォームでテーブル用の代替レンディションを使用します。これらのテーブルは、Designer で導入された新しいテーブル形式に基づいています。この形式では、次のものもサポートしています。

* 行ヘッダー
* 行幅

HTML5 Formsで新しい形式を使用するには、テーブルを複雑なものとしてマークします。 複雑なテーブルとしてマークするには、テーブルのサブフォームの XML ソースに `extras` タグを次のように追加します。

```
</extras>
 <text name="complexTable">1</text>
 </extras>
```

*complexTable* としてマークされたテーブルはネイティブの HTML レンディションに従うため、特定のスクリーンリーダーのアクセシビリティの範囲が拡大します。行幅を作成するには、テーブル内の 1 つの列で連続する複数のセルを選択し、選択範囲を右クリックして、「**[!UICONTROL セルの結合]**」をクリックします。

***注意：**行幅の作成は、一番左のセルに対してのみ機能します。*

行を行ヘッダーとしてマークするには、行のすべてのセルを選択し、選択範囲を右クリックして、 **[!UICONTROL ヘッダーをマーク]**.

セルを列見出しとしてマークするには、列内の任意のセルを選択し、選択範囲を右クリックして、 **[!UICONTROL ヘッダーをマーク]**.

新しい *AccessibleTable* 形式には次の制限事項があります。

* テーブルで行スパンが使用されている場合、拡大可能なフィールドがサポートされない
* ネストされたテーブル（テーブルセル内のテーブル）はサポートされません
* 行スパンのサポートは、ヘッダー行とヘッダーセルに限られています
* サポートは通常のテーブルに制限されています
* 行範囲が 1 を超えるテーブルでのデータの事前入力はサポートされません
