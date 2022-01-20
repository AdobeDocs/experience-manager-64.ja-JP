---
title: ページプロパティの一括編集のためのページの設定
seo-title: Configuring your Page for Bulk Editing of Page Properties
description: ページプロパティの一括編集を使用すると、複数のページのプロパティを一度に編集できます
seo-description: Bulk editing of page properties allows you to edit the properties of multiple pages at once
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
exl-id: 0aefe8c0-662e-4177-a369-feab174fa510
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 81%

---

# ページプロパティの一括編集のためのページの設定 {#configuring-your-page-for-bulk-editing-of-page-properties}

[ページプロパティの一括編集](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages)を使用すると、複数のページのプロパティを一度に編集できます。

様々な値が存在する可能性があるので、ページプロパティの一括編集はデフォルトでは有効になっていません。明示的に許可する（有効にする）必要があります。一括編集できるようにページプロパティを定義する場合は、次のような避けられない影響を考慮する必要があります。

* ページタイトルなど、通常は一意なフィールドがあります。1 つの値が適用される場合に、そのようなフィールドの一括編集を有効にして意味があるかどうかを判断する必要があります。
* 特定のフィールドには、複数の値を持たせることができます。そのためには、レンダリング時に意味のある表現が必要です。

   例えば、「公開準備完了」を示すチェックボックスが表示されます。 一括編集の前に、いくつかの値が含まれる場合があります（例：準備完了、レビュー中、処理中）。

>[!CAUTION]
>
>ページプロパティの一括編集には次の特徴があります。
>
>* クラシック UI では使用できません。
>* ライブコピー内のページでは使用できません。
>* リソースタイプが同じページでのみ使用できます。

>


>[!NOTE]
>
>一括編集はアセットに対しても使用できます。これは非常に似ていますが、いくつかの点で異なります。詳しくは、 [複数のアセットのプロパティの編集](/help/assets/managing-multiple-assets.md) を参照してください。アセットの一括メタデータエディターで、 [スキーマエディター](/help/assets/metadata-schemas.md).

## フィールドの有効化 {#enabling-a-field}

>[!NOTE]
>
>特定のフィールドには、複数の値を持たせることができます。そのためには、レンダリング時に意味のある表現が必要です。このため、次のフィールドタイプのみを有効にしてください。
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`

>


フィールドは、（テンプレートではなく）ページコンポーネントで有効化します。**

1. CRXDE Lite（または同等のメソッド）を使用して、ページコンポーネントを開きます。

   例：`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >この例では、コアコンポーネントがインスタンスにインストールされ、インスタンスが We.Retail サンプルコンテンツと共に実行されていることを想定しています。詳しくは、[コアコンポーネントのドキュメント](https://docs.adobe.com/content/help/ja-JP/experience-manager-core-components/using/introduction.html)を参照してください。

1. 内の必須フィールドに移動します。 `cq:dialog` 定義。
1. フィールドノードで次のプロパティを定義します。

   * **名前**：`allowBulkEdit`
   * **型**：`Boolean`
   * **値**: `true`

   例えば、標準的なページの[基盤コンポーネント](/help/sites-authoring/default-components-foundation.md)の場合：

   `/libs/foundation/components/page`

   プロパティは次の場所で定義されます。

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >`/libs` パス内の設定は&#x200B;***一切***&#x200B;変更しないでください。
   >
   >`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
   >
   >設定およびその他の変更に推奨される方法は次のとおりです。
   >
   >    1. 必要な項目（内に存在）を再作成します。 `/libs`) `/apps`
   >    1. `/apps` 内で変更作業をおこないます。


1. 「**すべて保存**」を選択して更新内容を保持します。
