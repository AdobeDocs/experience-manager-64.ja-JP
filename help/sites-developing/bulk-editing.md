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
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 59%

---

# ページプロパティの一括編集のためのページの設定 {#configuring-your-page-for-bulk-editing-of-page-properties}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[ページプロパティの一括編集](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) では、複数のページのプロパティを一度に編集できます。

異なる値が存在する可能性があるので、ページプロパティはデフォルトでは一括編集が有効になっていません。 明示的に許可（有効）する必要があります。 一括編集で使用できるようにページプロパティを定義する場合は、次のような特定の影響を考慮する必要があります。

* ページタイトルのように、通常は一意なフィールドがあります。1 つの値を適用した場合に、そのようなフィールドの一括編集を有効にして意味があるかどうかを判断する必要があります。
* 特定のフィールドには、複数の値を持たせることができます。そのためには、レンダリング時に意味のある表現が必要です。

   例えば、「公開準備完了」を示すチェックボックス。これには、一括編集の前にいくつかの値を持つ場合があります（例：準備完了、レビュー中、処理中）。

>[!CAUTION]
>
>ページプロパティの一括編集には次の特徴があります。
>
>* クラシック UI では使用できません。
>* ライブコピー内のページでは使用できません。
>* 同じリソースタイプを持つページでのみ使用できます。
>


>[!NOTE]
>
>一括編集はアセットに対しても使用できます。操作はよく似ていますが、いくつかの点が異なります。詳しくは、[複数のアセットのプロパティの編集](/help/assets/managing-multiple-assets.md)を参照してください。[スキーマエディター](/help/assets/metadata-schemas.md)を使用すると、アセット用の一括メタデータエディターでフィールドをカスタマイズできます。

## フィールドの有効化 {#enabling-a-field}

>[!NOTE]
>
>特定のフィールドには、複数の値を持たせることができます。そのためには、レンダリング時に意味のある表現が必要です。このため、次のフィールドタイプのみを有効にする必要があります。
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>


フィールドは、（テンプレートではなく）ページコンポーネントで有効化します&#x200B;*。*

1. CRXDE Lite（または同等の方法）を使用して、ページコンポーネントを開きます。

   例：`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >この例では、コアコンポーネントがインスタンスにインストールされていることを前提としています。これは、インスタンスが We.Retail サンプルコンテンツと共に実行されている場合です。 詳しくは、 [コアコンポーネントのドキュメント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) を参照してください。

1. `cq:dialog` 定義内の必要なフィールドに移動します。
1. フィールドノードで次のプロパティを定義します。

   * **名前**：`allowBulkEdit`
   * **型**：`Boolean`
   * **値**：`true`

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
   >    1. 必要な項目（`/libs`内に存在）を、`/apps`の下で再作成します。
   >    1. `/apps` 内で変更作業をおこないます。


1. 「**すべて保存**」を選択して更新内容を保持します。
