---
title: メタデータの編集と追加
description: でのアセットメタデータについて説明します。 [!DNL Experience Manager] アセットには様々な方法があり、この方法でアセットのメタデータを編集できます。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: f0522343-f8a9-4d89-8ce8-b3357ae3fe70
source-git-commit: 937c9425e276f67486fba1d4563799fe68d35cc7
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 77%

---

# メタデータの編集と追加 {#how-to-edit-or-add-metadata}

メタデータは、検索可能なアセットに関する追加情報です。画像をアップロードすると自動的に抽出されます。既存のメタデータを編集したり、新しいメタデータプロパティを既存のフィールドに追加（例えば、メタデータフィールドが空白の場合など）したりすることができます。

メタデータの語彙を制御し、信頼性を確保する必要があるので、 [!DNL Experience Manager] Assets では、新しいメタデータプロパティをアドホックに追加することはできません。 作成者は、アセットの新しいメタデータフィールドを追加することはできませんが、開発者は追加できます。[アセットの新しいメタデータプロパティの作成](meta-edit.md#editing-metadata-schema)を参照してください。

## アセットのメタデータの編集 {#editing-metadata-for-an-asset}

メタデータを編集するには、次の手順に従います。

1. 次のいずれかの操作をおこないます。

   * Assets UI でアセットを選択し、ツールバーの「**[!UICONTROL プロパティを表示]**」アイコンをクリックまたはタップします。
   * アセットのサムネールから、「**[!UICONTROL プロパティを表示]**」クイックアクションを選択します。
   * アセットページで、 **[!UICONTROL プロパティを表示]** アイコン ![情報アイコン](assets/do-not-localize/info_icon.png) をクリックします。

   アセットページに、アセットのメタデータがすべて表示されます。このメタデータは、にアップロード（取り込み）された際に自動的に抽出されました。 [!DNL Experience Manager] アセット。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. 様々なタブで必要に応じてメタデータを編集したら、ツールバーの「**[!UICONTROL 保存]**」をクリックまたはタップして、変更内容を保存します。「**[!UICONTROL 閉じる]**」をクリックまたはタップして、Assets Web インターフェイスに戻ります。

   >[!NOTE]
   >
   >テキストフィールドが空の場合、現在設定されているメタデータはありません。フィールドに値を入力して保存すると、そのメタデータプロパティを追加できます。

アセットのメタデータへの変更内容は、XMP データの一部として元のバイナリに書き戻されます。この操作は、AEM のメタデータの書き戻しワークフローによって実行されます。既存のプロパティ（`dc:title` など）への変更は上書きされ、新しく作成されたプロパティ（`cq:tags` などのカスタムプロパティを含む）はスキーマとともに追加されます。

XMP の書き戻しは、[技術要件](/help/sites-deploying/technical-requirements.md)に示されたプラットフォームおよびファイル形式でサポートされ、有効になります。

## メタデータスキーマの編集 {#editing-metadata-schema}

メタデータスキーマの編集方法について詳しくは、[メタデータスキーマフォームの編集](metadata-schemas.md#editing-metadata-schema-forms)を参照してください。

##  内でのカスタム名前空間の登録 [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

AEM 内での独自の名前空間を追加できます。cq、jcr、sling など事前に定義された名前空間があるように、リポジトリメタデータと xml 処理用の名前空間を設定できます。

1. ノードタイプ管理ページに移動します。 `https://[AEM_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. ページ上部の「**[!UICONTROL 名前空間]**」をクリックまたはタップします。ウィンドウに名前空間管理ページが表示されます。

1. 名前空間を追加するには、下部の「**[!UICONTROL 新規]**」をクリックまたはタップします。
1. XML 名前空間規則に従って、カスタム名前空間を指定（URI 形式の id と、その id に関連付けられているプレフィックスを指定）したら、「**[!UICONTROL 保存]**」をクリックまたはタップします。

## ヒントと制限事項 {#best-practices-limitations}

* タッチ UI を使用したメタデータの更新により、 `dc` 名前空間。 HTTP API を使用して更新をおこなうと、 `jcr` 名前空間。 詳しくは、 [HTTP API を使用してメタデータを更新する方法](/help/assets/mac-api-assets.md#update-asset-metadata).

>[!MORELIKETHIS]
>
>* [メタデータと Assets でのニーズについて](metadata.md)

