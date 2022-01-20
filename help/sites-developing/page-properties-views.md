---
title: ページプロパティのビューのカスタマイズ
seo-title: Customizing Views of Page Properties
description: どのページにも、必要に応じて編集できる一連のプロパティがあります
seo-description: Every page has a set of properties that you can edit as required
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 25dad368-8227-424d-960b-1664d8e20a21
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 74%

---

# ページプロパティのビューのカスタマイズ{#customizing-views-of-page-properties}

どのページにも、ユーザーが表示および編集できる一連の[プロパティ](/help/sites-authoring/editing-page-properties.md)があります。ページ作成時に使用されるプロパティもあれば（作成ビュー）、後の段階で表示および編集できるプロパティもあります（編集ビュー）。これらのページプロパティは、適切なページコンポーネントのダイアログ（`cq:dialog`）によって定義され、使用可能になります。

>[!CAUTION]
>
>ページプロパティのビューのカスタマイズは、クラシック UI では使用できません。

各ページプロパティのデフォルト状態は次のとおりです。

* 作成ビューでは非表示（例：**ページを作成**&#x200B;ウィザード）

* 編集ビューでは表示（例：**プロパティを表示**）

変更が必要な場合は、フィールドを明確に設定する必要があります。それには適切なノードプロパティを使用します。

* 作成ビューで表示するページプロパティ（例：**ページを作成**&#x200B;ウィザード）：

   * 名前：`cq:showOnCreate`
   * 型：`Boolean`

* 編集ビューで使用できるページプロパティ ( 例： **表示**/**編集**) **プロパティ** オプション ):

   * 名前：`cq:hideOnEdit`
   * 型：`Boolean`

例として、基盤となるページコンポーネントの「**基本**」タブの「**他のタイトルと説明**」の下にグループ化されたフィールドの設定を参照してください。**が** に設定されているので、これらのフィールドは`cq:showOnCreate`ページを作成`true`ウィザードに表示されます。

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>詳しくは、 [ページプロパティの拡張チュートリアル](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) を参照してください。

## ページプロパティの設定 {#configuring-your-page-properties}

ページコンポーネントのダイアログを設定し、適切なノードプロパティを適用することによって、表示するフィールドを設定することもできます。

例えば、デフォルトでは、[**ページを作成**&#x200B;ウィザード](/help/sites-authoring/managing-pages.md#creating-a-new-page)には「**その他のタイトルと説明**」の下にグループ化されたフィールドが表示されます。これらのフィールドを非表示にするには、次のように設定します。

1. の下にページコンポーネントを作成します。 `/apps`.
1. 上書きの作成 ( *ダイアログ差分* 提供元： [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)) `basic` セクション内に配置する必要があります。例：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >リファレンスとして、以下を参照してください。
   >
   >
   ```
   >/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog
   >```
   >
   >ただし、 ***必須*** 内容を変えない `/libs` パス。
   >
   >`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
   >
   >設定およびその他の変更に推奨される方法は次のとおりです。
   >
   >1. 必要な項目（内に存在）を再作成します。 `/libs`) `/apps`
   >1. `/apps` 内で変更作業をおこないます。


1. を `path` プロパティ： `basic` をクリックして、「基本」タブの上書きを指定します（次の手順も参照してください）。 次に例を示します。

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. オーバーライド `basic` - `moretitles` セクションを指定します。例：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 適切なノードプロパティを適用します。

   * **名前**：`cq:showOnCreate`
   * **型**：`Boolean`
   * **値**: `false`

   **ページを作成**&#x200B;ウィザードに「**その他のタイトルと説明**」セクションが表示されなくなります。

>[!NOTE]
>
>ライブコピーと一緒に使用するページプロパティを設定する場合、詳しくは、[ページプロパティに対する MSM ロックの設定](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui)を参照してください。

## ページプロパティの設定サンプル {#sample-configuration-of-page-properties}

このサンプルは、[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) のダイアログ差分比較の手法を示しており、[`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties) が使用されています。また、これらの両方の使用方法を示しています `cq:showOnCreate` および `cq:hideOnEdit`.

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-authoring-extension-page-dialog プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
