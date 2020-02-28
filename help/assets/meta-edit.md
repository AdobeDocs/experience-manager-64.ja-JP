---
title: メタデータの編集と追加
description: AEM Assets のアセットメタデータを編集する様々な方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0d70a672a2944e2c03b54beb3b5f734136792ab1

---


# メタデータの編集と追加 {#how-to-edit-or-add-metadata}

メタデータは、検索可能なアセットに関する追加情報です。画像をアップロードすると自動的に抽出されます。既存のメタデータを編集したり、新しいメタデータプロパティを既存のフィールドに追加する（例えば、メタデータフィールドが空白の場合など）ことができます。

どの企業でも、メタデータの語彙を制御して信頼性を確保する必要があります。そのため、AEM Assets では、新しいメタデータプロパティをアドホックに追加することはできません。作成者は、アセットの新しいメタデータフィールドを追加することはできませんが、開発者は追加できます。[アセットの新しいメタデータプロパティの作成](meta-edit.md#editing-metadata-schema)を参照してください。

## アセットのメタデータの編集 {#editing-metadata-for-an-asset}

メタデータを編集するには、次の手順に従います。

1. 次のいずれかの操作をおこないます。

   * From the Assets UI, select the asset and click/tap the **[!UICONTROL View Properties]** icon from the toolbar.
   * From the asset thumbnail, select the **[!UICONTROL View Properties]** quick action.
   * From the asset page, click/tap the **[!UICONTROL View Properties]** icon ![info icon](assets/do-not-localize/info_icon.png) from the toolbar.
   アセットページに、アセットのメタデータがすべて表示されます。このメタデータは、AEM Assets にアップロードされた（取り込まれた）ときに、自動的に抽出されたものです。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. 必要に応じて、様々なタブの下でメタデータを編集したら、ツールバーの「**[!UICONTROL 保存]**」をクリックまたはタップして、変更内容を保存します。「**[!UICONTROL 閉じる]**」をクリックまたはタップして、Assets Web インターフェイスに戻ります。

   >[!NOTE]
   >
   >テキストフィールドが空の場合、現在設定されているメタデータはありません。フィールドに値を入力して保存すると、そのメタデータプロパティを追加できます。

アセットのメタデータに対する変更は、XMPデータの一部として元のバイナリに書き戻されます。 この操作は、AEM のメタデータの書き戻しワークフローによって実行されます。既存のプロパティ（`dc:title` など）への変更は上書きされ、新しく作成されたプロパティ（`cq:tags` などのカスタムプロパティを含む）はスキーマとともに追加されます。

XMP の書き戻しは、[技術要件](/help/sites-deploying/technical-requirements.md)に示されたプラットフォームおよびファイル形式でサポートされ、有効になります。

## メタデータスキーマの編集 {#editing-metadata-schema}

For details on how to edit metadata schema, see [Editing metadata schema forms](metadata-schemas.md#editing-metadata-schema-forms).

## AEM 内でのカスタム名前空間の登録 {#registering-a-custom-namespace-within-aem}

AEM 内での独自の名前空間を追加できます。cq、jcr、sling など事前に定義された名前空間があるように、リポジトリメタデータと xml 処理用の名前空間を設定できます。

1. Go to the node type administration page `https://[AEM_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Click or tap **[!UICONTROL Namespaces]** at the top of the page. ウィンドウに名前空間管理ページが表示されます。

1. To add a namespace, click or tap **[!UICONTROL New]** at the bottom.
1. Specify a custom namespace in the XML namespace convention (Specify the id in the form of a URI and an associated prefix for the id), and click or tap **[!UICONTROL Save]**.
