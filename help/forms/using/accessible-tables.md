---
title: アクセス可能な複雑なテーブルを HTML5 フォームで作成する
seo-title: Create accessible complex tables in HTML5 forms
description: 'アクセス可能なテーブルを HTML5 フォームで作成する方法について説明します。 '
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
ht-degree: 81%

---

# アクセス可能な複雑なテーブルを HTML5 フォームで作成する {#create-accessible-complex-tables-in-html-forms}

HTML5 フォームでのテーブルのデフォルト実装では、テーブルのレンダリングに HTML DIV 要素が使用されます。さらに、アクセシビリティ要件を満たす目的で ARIA ロールも使用されます。

データテーブルで使用される ARIA-roles を完全にサポートしていないスクリーンリーダーでのアクセシビリティの問題を回避するため、HTML5 Formsでは、テーブル用の代替レンディションを提供しています。 これらのテーブルは、Designer で導入された新しいテーブル形式に基づいており、次の項目もサポートしています。

* 行ヘッダー
* 行幅

HTML5 フォームで新しい形式を使用するには、テーブルを複雑なテーブルとしてマークする必要があります。複雑なテーブルとしてマークするには、テーブルのサブフォームの XML ソースに `extras` タグを次のように追加します。

```
</extras>
 <text name="complexTable">1</text>
 </extras>
```

次のマークが付いたテーブル *complexTable* ネイティブのHTMLレンディションに従い、特定のスクリーンリーダーに対してより優れたアクセシビリティサポートを提供する。  行幅を作成するには、テーブル内の 1 つの列で連続する複数のセルを選択し、選択範囲を右クリックして、「**[!UICONTROL セルの結合]**」をクリックします。

***注：**行幅の作成は一番左のセルでのみ機能します。*

行を行ヘッダーとしてマークするには、その行のすべてのセルを選択し、選択範囲を右クリックして、「**[!UICONTROL ヘッダーをマーク]**」をクリックします。

セルを列ヘッダーとしてマークするには、その列内の任意のセルを選択し、選択範囲を右クリックして、「**[!UICONTROL ヘッダーをマーク]**」をクリックします。

新しい機能の制限 *AccessibleTable* 形式：

* テーブルに行幅を設定する場合は、拡大可能なフィールドを使用できない
* ネストされたテーブル（テーブルのセルに含まれている別のテーブル）は使用できない
* 行幅はヘッダー行とヘッダーセルのみに適用できる
* 使用可能なテーブルは標準テーブルのみである
* 行幅が 1 を超えるテーブルではデータを事前入力できない
