---
title: コンテンツフラグメントモデル
seo-title: コンテンツフラグメントモデル
description: コンテンツフラグメントモデルは、構造化コンテンツを含むコンテンツフラグメントを作成するために使用します。
seo-description: コンテンツフラグメントモデル は、構造化されたコンテンツを使用してコンテンツフラグメントを作成するために使用します。
uuid: 59176a32-1255-4a46-ad00-344bde843ea6
content-type: reference
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 45e67357-4524-4d25-b5f1-21182b8e803c
translation-type: tm+mt
source-git-commit: 8b83be510a67fadaa666f2ba96fbb3fc82b9cb3d

---


# コンテンツフラグメントモデル {#content-fragment-models}

>[!CAUTION]
>
>一部のコンテンツフラグメント機能では、 [AEM 6.4 Service Pack 2(6.4.2.0)以降が必要です](../release-notes/sp-release-notes.md)。

コンテンツフラグメントモデルは、[コンテンツフラグメント](content-fragments.md)のコンテンツの構造を定義します。

## コンテンツフラグメントモデルの有効化 {#enable-content-fragment-models}

>[!CAUTION]
>
>If you do not enable **[!UICONTROL Content Fragment Models]**, the **[!UICONTROL Create]** option will not be available for creating new models.

コンテンツフラグメントモデルを有効にするには、次の操作を実行する必要があります。

* Configuration Manager でのコンテンツフラグメントモデル使用の有効化
* アセットフォルダーへの設定の適用

### Configuration Manager でのコンテンツフラグメントモデルの有効化 {#enable-content-fragment-models-in-configuration-manager}

[新しいコンテンツフラグメントモデルを作成する](#creating-a-content-fragment-model)には、最初に Configuration Manager を使用してコンテンツフラグメントモデルを有効にする&#x200B;**必要があります**。

1. **[!UICONTROL ツール]**／**[!UICONTROL 一般]**&#x200B;に移動し、「**[!UICONTROL 設定ブラウザー]**」を開きます。
1. Web サイトに適した場所を選択します。
1. Use **[!UICONTROL Create]** to open the dialog, where you:

   1. **[!UICONTROL タイトル]**&#x200B;を指定します。
   1. Select **[!UICONTROL Content Fragment Models]** to enable their use.
   ![cfm-6420-09](assets/cfm-6420-09.png)

1. Select **[!UICONTROL Create]** to save the definition.

### アセットフォルダーへの設定の適用 {#apply-the-configuration-to-your-assets-folder}

When the configuration **[!UICONTROL global]** is enabled for content fragment models, then any models that users create can be used in any Assets folder.

他の設定（グローバル以外）を同等の Assets フォルダーで使用するには、接続を定義する必要があります。そのためには、適切なフォルダーの「**[!UICONTROL フォルダーのプロパティ]**」の「**[!UICONTROL クラウドサービス]**」タブで「**[!UICONTROL 設定]**」を使用します。

## コンテンツフラグメントモデルの作成 {#creating-a-content-fragment-model}

1. Navigate to **[!UICONTROL Tools]**, **[!UICONTROL Assets]**, then open **[!UICONTROL Content Fragment Models]**.
1. 目的の[設定](#enable-content-fragment-models)に適したフォルダーに移動します。
1. 「**[!UICONTROL 作成]**」を使用してウィザードを開きます。

   >[!CAUTION]
   >
   >[コンテンツフラグメントモデルの使用が有効になっていない](#enable-content-fragment-models)場合、「**作成**」オプションは使用できません。

1. **[!UICONTROL モデルタイトル]**&#x200B;を指定します。必要に応じて&#x200B;**[!UICONTROL 説明]**&#x200B;を追加することもできます。

   ![cfm-6420-10](assets/cfm-6420-10.png)

1. 「**[!UICONTROL 作成]**」を使用して空のモデルを保存します。操作の成功を示すメッセージが表示されます。「**[!UICONTROL 開く]**」を選択してモデルをすぐに編集するか、「**[!UICONTROL 完了]**」を選択してコンソールに戻ることができます。

## コンテンツフラグメントモデルの定義 {#defining-your-content-fragment-model}

コンテンツフラグメントモデルは、生成されるコンテンツフラグメントの構造を効果的に定義します。モデルエディターを使用して、必要なフィールドを追加および設定できます。

>[!CAUTION]
>
>既存のコンテンツフラグメントモデルを編集すると、依存するフラグメントが影響を受ける可能性があります。

1. Navigate to **[!UICONTROL Tools]**, **[!UICONTROL Assets]**, then open **[!UICONTROL Content Fragment Models]**.

1. コンテンツフラグメントモデルが含まれているフォルダーに移動します。
1. 必要なモデルを&#x200B;**[!UICONTROL 編集]**&#x200B;用に開きます。クイック操作を使用するか、モデルを選択してツールバーから操作を選択します。

   モデルを開くと、モデルエディターに次の情報が表示されます。

   * 左：既に定義されているフィールド
   * 右：フィールドの作成に使用できる&#x200B;**[!UICONTROL データタイプ]**（およびフィールドの作成後に使用する&#x200B;**[!UICONTROL プロパティ]**）
   >[!NOTE]
   >
   >When a field is **Required**, the **Label** indicated in the left pane will be marked with an asterix (**&amp;ast;**).

   ![cfm-6420-11](assets/cfm-6420-12.png)

1. **フィールドを追加するには**

   * 必要なデータタイプをフィールドの必要な場所にドラッグします。
   ![cfm-6420-11](assets/cfm-6420-11.png)

   * フィールドがモデルに追加されると、その特定のデータタイプに対して定義できる&#x200B;**プロパティ**&#x200B;が右側のパネルに表示されます。ここで、そのフィールドに必要な項目を定義することができます。次に例を示します。
   ![cfm-6420-13](assets/cfm-6420-13.png)

1. **フィールドを削除するには**

   必要なフィールドを選択し、ごみ箱アイコンをクリックまたはタップします。この操作の確認が求められます。

   ![cf-32](assets/cf-32.png)

1. After adding all required fields, and defining the properties, use **[!UICONTROL Save]** to persist the definition. 次に例を示します。

   ![cfm-6420-14](assets/cfm-6420-14.png)

## コンテンツフラグメントモデルの削除 {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>コンテンツフラグメントモデルを削除すると、依存するフラグメントが影響を受ける可能性があります。

コンテンツフラグメントモデルを削除するには：

1. Navigate to **[!UICONTROL Tools]**, **[!UICONTROL Assets]**, then open **[!UICONTROL Content Fragment Models]**.

1. コンテンツフラグメントモデルが含まれているフォルダーに移動します。
1. モデルを選択し、次にツールバーの「**[!UICONTROL 削除]**」を選択します。

   >[!NOTE]
   >
   >モデルが参照されている場合は、警告が表示されます。適切に対処します。

## コンテンツフラグメントモデルの公開 {#publishing-a-content-fragment-model}

コンテンツフラグメントモデルは、依存するコンテンツフラグメントの公開時または公開前に公開する必要があります。

コンテンツフラグメントモデルを公開するには：

1. Navigate to **[!UICONTROL Tools]**, **[!UICONTROL Assets]**, then open **[!UICONTROL Content Fragment Models]**.

1. コンテンツフラグメントモデルが含まれているフォルダーに移動します。
1. モデルを選択し、次にツールバーの「**[!UICONTROL 公開]**」を選択します。

   >[!NOTE]
   >
   >まだ公開されていないモデルのコンテンツフラグメントを公開すると、選択リストにそのことが示され、モデルがフラグメントと共に公開されます。

