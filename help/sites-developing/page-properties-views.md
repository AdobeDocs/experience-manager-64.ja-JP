---
title: ページプロパティのビューのカスタマイズ
seo-title: Customizing Views of Page Properties
description: 各ページには、必要に応じて編集できる一連のプロパティがあります
seo-description: Every page has a set of properties that you can edit as required
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 25dad368-8227-424d-960b-1664d8e20a21
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 79%

---

# ページプロパティのビューのカスタマイズ{#customizing-views-of-page-properties}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

どのページにも、ユーザーが表示および編集できる一連の[プロパティ](/help/sites-authoring/editing-page-properties.md)があります。ページ作成時に使用されるプロパティもあれば（作成ビュー）、後の段階で表示および編集できるプロパティもあります（編集ビュー）。これらのページプロパティは、適切なページコンポーネントのダイアログ（`cq:dialog`）で定義し、使用できるようにします。

>[!CAUTION]
>
>ページプロパティのビューは、クラシック UI ではカスタマイズできません。

各ページプロパティのデフォルト状態は次のとおりです。

* 作成ビューでは非表示（例：**ページを作成**&#x200B;ウィザード）

* 編集ビューでは表示（例：**プロパティを表示**）

変更が必要な場合は、フィールドを具体的に設定する必要があります。 これは、次の適切なノードプロパティを使用しておこないます。

* 作成ビューで利用できるページプロパティ（例：**ページを作成**&#x200B;ウィザード）：

   * 名前：`cq:showOnCreate`
   * 型：`Boolean`

* 編集ビューで利用できるページプロパティ（例：**表示**／**編集**）**プロパティ**&#x200B;オプション）：

   * 名前：`cq:hideOnEdit`
   * 型：`Boolean`

例として、基盤となるページコンポーネントの「**基本**」タブの「**その他のタイトルと説明**」の下にグループ化されたフィールドの設定を参照してください。`cq:showOnCreate` が `true` に設定されているので、これらのフィールドは&#x200B;**ページを作成**&#x200B;ウィザードに表示されます。

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>ページプロパティのカスタマイズ方法については、「[ページプロパティの拡張チュートリアルl](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html?lang=ja) 」を参照してください。

## ページプロパティの設定 {#configuring-your-page-properties}

また、ページコンポーネントのダイアログを設定し、適切なノードプロパティを適用することで、使用可能なフィールドを設定できます。

例えば、デフォルトでは、[**ページを作成**&#x200B;ウィザード](/help/sites-authoring/managing-pages.md#creating-a-new-page)には「**その他のタイトルと説明**」の下にグループ化されたフィールドが表示されます。これらのフィールドを非表示にするには、次のように設定します。

1. `/apps` の下にページコンポーネントを作成します。
1. ページコンポーネントの`basic`セクションにオーバーライドを作成します（[Sling リソースマネージャー](/help/sites-developing/sling-resource-merger.md) が提供する *ダイアログの差分* を使用）。例を以下に示します。

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
   >ただし、`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
   >
   >`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
   >
   >設定およびその他の変更に推奨される方法は次のとおりです。
   >
   >1. 必要な項目（`/libs`内に存在）を、`/apps`の下で再作成します。
   >1. `/apps` 内で変更作業をおこないます。


1. `basic` の `path` プロパティに、基本タブのオーバーライドを指すように設定します（次の手順も参照してください）。次に例を示します。

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 対応するパスに「`basic` - `moretitles` 」セクションのオーバーライドを作成します。例：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 適切なノードプロパティを適用します。

   * **名前**：`cq:showOnCreate`
   * **型**：`Boolean`
   * **値**：`false`

   **ページを作成**&#x200B;ウィザードに「**その他のタイトルと説明**」セクションが表示されなくなります。

>[!NOTE]
>
>ライブコピーで使用するページプロパティを設定する場合は、 [ページプロパティに対する MSM ロックの設定](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) を参照してください。

## ページプロパティの設定例 {#sample-configuration-of-page-properties}

この例では、[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) のダイアログ差分比較の手法を示しており、[`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties) が使用されています。`cq:showOnCreate` と `cq:hideOnEdit` の両方を使用することも説明されています。

GitHub のコード

このページのコードは GitHub にあります

* [aem-authoring-extension-page-dialog プロジェクトを GitHub で公開する](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
