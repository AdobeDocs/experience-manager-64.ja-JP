---
title: メタデータプロファイルを使用して、フォルダー内のすべてのアセットに初期設定のメタデータを適用する
description: アセットのメタデータプロファイルについて理解します。また、メタデータプロファイルを作成し、フォルダーのアセットに適用する方法も学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: af1955ab1fdcf16dd9a9d3ad36336e6c1aac9312

---


# メタデータプロファイル {#metadata-profiles}

メタデータプロファイルを使用すると、フォルダー内のアセットに初期設定のメタデータを適用できます。メタデータプロファイルを作成し、フォルダーに適用します。その後フォルダーにアップロードするアセットは、メタデータプロファイルで設定したデフォルトのメタデータを継承します。

## メタデータプロファイルの追加 {#adding-a-metadata-profile}

1. Tap or click the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**, and then tap **[!UICONTROL Create]**.
1. メタデータプロファイルのタイトル（「サンプルメタデータ」など）を入力し、「**[!UICONTROL 送信]**」をクリックします。The **[!UICONTROL Edit Form]** for the Metadata Profile is displayed.

   ![chlimage_1-480](assets/chlimage_1-480.png)

1. Click a component and configure its properties in the **[!UICONTROL Settings]** tab. For example, click the **[!UICONTROL Description]** component and edit its properties.

   ![chlimage_1-481](assets/chlimage_1-481.png)

   Edit the following properties for the **[!UICONTROL Description]** component:

   * **[!UICONTROL フィールドラベル]**:メタデータプロパティの表示名です。 ユーザーの参照用のみで使用します。
   * **[!UICONTROL プロパティにマッピング]**：このプロパティの値には、リポジトリに保存される場所にあるアセットノードへの相対パスまたは名前を指定します。The value should always start with `./` because it indicates that the path is under the asset&#39;s node.
   ![chlimage_1-482](assets/chlimage_1-482.png)

   「**[!UICONTROL プロパティにマッピング]**」に指定した値は、アセットの metadata ノードの下のプロパティとして保存されます。例えば、次のように指定するとします。`/jcr:content/metadata/dc:desc` aem Assetsは、プロパテ **[!UICONTROL ィにマップの名前として]**、アセットのメタデ `dc:desc` ータノードに値を格納します。

   * **[!UICONTROL デフォルト値]**：メタデータコンポーネントのデフォルト値を追加するには、このプロパティを使用します。For example, if you specify &quot;My description&quot; then this value is assigned to the property `dc:desc` at the asset&#39;s metadata node.
   ![chlimage_1-483](assets/chlimage_1-483.png)

   >[!NOTE]
   >
   >新しいメタデータプロパティにデフォルト値を追加する（にまだ存在しない）。 `/jcr:content/metadata` ノード)は、デフォルトではアセットのプロパティページにプロパティとその値を表 **[!UICONTROL 示しま]** せん。 アセットの [!UICONTROL Propertiesページに新しいプロパティを表示するには] 、対応するスキーマフォームを変更します。

1. (Optional) Add more components to the **[!UICONTROL Edit Form]** from the **[!UICONTROL Build Form]** tab, and configure their properties in the **[!UICONTROL Settings]** tab. The following properties are available from the **[!UICONTROL Build Form]** tab:

| コンポーネント | プロパティ |
|---|---|
| [!UICONTROL セクションヘッダー] | フィールドラベル、 <br> 説明 |
| [!UICONTROL 1 行のテキスト] | フィールドラベル、 <br> プロパティにマップ、デ <br> フォルト値 |
| [!UICONTROL 複数値テキスト] | フィールドラベル、 <br> プロパティにマップ、デ <br> フォルト値 |
| [!UICONTROL 番号] | フィールドラベル、 <br> プロパティにマップ、デ <br> フォルト値 |
| [!UICONTROL 日付] | フィールドラベル、 <br> プロパティにマップ、デ <br> フォルト値 |
| [!UICONTROL 標準タグ] | フィールドラベル、 <br> プロパティにマップ、デ <br> フォルト値、説 <br> 明 |

![chlimage_1-484](assets/chlimage_1-484.png)

1. Click **[!UICONTROL Done]**. The metadata profile is added to the list of profiles in the **[!UICONTROL Metadata Profiles]** page.

   ![chlimage_1-485](assets/chlimage_1-485.png)

## メタデータプロファイルのコピー {#copying-a-metadata-profile}

1. From the **[!UICONTROL Metadata Profiles]** page, select a profile to make a copy of it.

   ![chlimage_1-486](assets/chlimage_1-486.png)

1. Click **[!UICONTROL Copy]** from the toolbar.
1. In the **[!UICONTROL Copy Metadata Profile]** dialog, enter a title for the new copy of the profile.
1. 「**[!UICONTROL コピー]**」をクリックします。A copy of the profile appears in the list of profiles in the **[!UICONTROL Metadata Profiles]** page.

   ![chlimage_1-487](assets/chlimage_1-487.png)

## メタデータプロファイルの削除 {#deleting-a-metadata-profile}

1. **[!UICONTROL メタデータプロファイル]**&#x200B;ページで、削除するプロファイルを選択します。

   ![chlimage_1-488](assets/chlimage_1-488.png)

1. Click **[!UICONTROL Delete Metadata Profiles]** in the toolbar.
1. In the dialog box, click **[!UICONTROL Delete]** to confirm the delete operation. メタデータプロファイルがリストから削除されます。

## Apply a metadata profile to folders {#applying-a-metadata-profile-to-folders}

フォルダーにメタデータプロファイルを割り当てると、サブフォルダーは自動的に親フォルダーのプロファイルを継承します。つまり、フォルダーに適用できるのは 1 つのメタデータプロファイルのみとなります。そのため、アセットをアップロード、保存、使用およびアーカイブする場所のフォルダー構造については入念に検討してください。

フォルダーに異なるメタデータプロファイルを割り当てた場合、新しいプロファイルが以前のプロファイルよりも優先されます。以前に存在していたフォルダーのアセットは変更されずに維持されます。新しいプロファイルは、その後にフォルダーに追加されるアセットに対して適用されます。

プロファイルが割り当てられているフォルダーは、ユーザーインターフェイスでカード名にプロファイルの名前が表示されます。

![chlimage_1-489](assets/chlimage_1-489.png)

特定のフォルダーまたはすべてのアセットにグローバルにメタデータプロファイルを適用できます。

### Apply metadata profiles to specific folders {#applying-metadata-profiles-to-specific-folders}

**[!UICONTROL ツール]**&#x200B;メニュー内から、またはフォルダー内にいる場合は「**[!UICONTROL プロパティ]**」から、メタデータプロファイルをフォルダーに適用できます。このセクションでは、メタデータプロファイルをフォルダーに適用する両方の方法について説明します。

既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

#### Apply metadata profiles to folders from Profiles user interface {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. 1 つまたは複数のフォルダーに適用するメタデータプロファイルを選択します。

   ![chlimage_1-490](assets/chlimage_1-490.png)

1. Tap **[!UICONTROL Apply Metadata Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and tap **[!UICONTROL Done]**. 既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

#### Apply metadata profiles to folders from Properties {#applying-metadata-profiles-to-folders-from-properties}

1. In the left rail, tap **[!UICONTROL Assets]** then navigate to the folder that you want to apply a metadata profile to.
1. On the folder, tap the check mark to select it, then tap  **[!UICONTROL Properties]**.

1. 「**[!UICONTROL メタデータプロファイル]**」タブを選択し、ドロップダウンメニューからプロファイルを選択して、「**[!UICONTROL 保存]**」をクリックします。

   ![chlimage_1-491](assets/chlimage_1-491.png)

   既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。

### Apply a metadata profile globally {#applying-a-metadata-profile-globally}

特定のフォルダーにプロファイルを適用できるだけでなく、グローバルにプロファイルを適用することもできます。これにより、AEM アセットにアップロードされている、すべてのフォルダー内にあるすべてのコンテンツに、選択したプロファイルを適用できます。メタデータプロファイルをグローバルに適用するには、次の手順に従います。

1. 次のいずれかの操作をおこないます。

   * Navigate to `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` and apply the appropriate profile and tap or click **[!UICONTROL Save]**.

      ![chlimage_1-492](assets/chlimage_1-492.png)

   * Navigate to CRXDE Lite to the following node: `/content/dam/jcr:content`. プロパティを追加し、「す `metadataProfile:/etc/dam/metadata/dynamicmedia/<name_of_metadata_profile>` べて保存」 **[!UICONTROL をタップしま]**&#x200B;す。

      ![chlimage_1-493](assets/chlimage_1-493.png)

## Remove a metadata profile from folders {#removing-a-metadata-profile-from-folders}

フォルダーからメタデータプロファイルを削除すると、サブフォルダーは自動的に親フォルダーのプロファイルの削除状態を継承します。ただし、フォルダー内で実行されたファイルの処理はそのまま維持されます。

**[!UICONTROL ツール]**&#x200B;メニュー内から、またはフォルダー内にいる場合は「**[!UICONTROL プロパティ]**」から、メタデータプロファイルをフォルダーから削除できます。このセクションでは、メタデータプロファイルをフォルダーから削除する両方の方法について説明します。

### Remove metadata profiles from folders via Profiles user interface {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

プロファイルユーザーインターフェイスを使用してフォルダーからメタデータプロファイルを削除するには、次の手順に従います。

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Metadata Profiles]**.
1. 1 つまたは複数のフォルダーから削除するメタデータプロファイルを選択します。
1. Tap **[!UICONTROL Remove Metadata Profile from Folder(s)]** and select the folder or multiple folders you want use to remove a profile from, then tap **[!UICONTROL Done]**.

   名前がフォルダー名の下に表示されなくなっていることで、メタデータプロファイルがフォルダーに適用されていないことを確認できます。

### Remove metadata profiles from folders by way of Properties {#removing-metadata-profiles-from-folders-via-properties}

1. Tap the AEM logo and navigate **[!UICONTROL Assets]** and then to the folder that you want to remove an metadata profile from.
1. On the folder, tap the check mark to select it, then tap **[!UICONTROL Properties]**.
1. 「メタデー **[!UICONTROL タプロファイル]** 」タブを選択し、ドロ **[!UICONTROL ップダウンメニューから「なし]** 」を選択します。 「**[!UICONTROL 保存]**」をタップします。

既にプロファイルが割り当てられているフォルダーには、フォルダー名のすぐ下にプロファイルの名前が表示されます。
