---
title: レンディションへの XMP の書き戻し
description: XMP の書き戻し機能を使用して、アセットのメタデータの変更を、そのアセットのすべてのレンディションまたは特定のレンディションに反映させる方法を学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5ef4c4e42165819191c6e3810c36183110f3f34a

---


# レンディションへの XMP の書き戻し {#xmp-writeback-to-renditions}

Adobe Experience Manager（AEM）Assets のこの XMP の書き戻し機能は、アセットメタデータの変更をアセットのレンディションにレプリケートします。

AEM Assets内から、またはアセットのアップロード中に、アセットのメタデータを変更すると、変更はCrx-Deのアセットノード内に最初に保存されます。

XMPの書き戻し機能は、アセットのすべてのレンディションまたは特定のレンディションにメタデータの変更を反映します。

Consider a scenario where you modify the [!UICONTROL Title] property of the asset titled `Classic Leather` to `Nylon`.

![メタデータ](assets/metadata.png)

この場合、AEM Assets ではこの「**[!UICONTROL タイトル]**」プロパティへの変更が、アセット階層に格納されたアセットメタデータ用の `dc:title` パラメーターに保存されます。

![metadata_stored](assets/metadata_stored.png)

ただし、AEM Assets では、メタデータの変更はアセットのレンディションに自動的に反映されません。

XMPの書き戻し機能を使用すると、メタデータの変更をアセットのすべてのレンディションまたは特定のレンディションに反映できます。 ただし、変更はアセット階層の metadata ノード以下には保存されません。代わりに、この機能によって、レンディションのバイナリファイル内に変更内容が埋め込まれます。

## XMPの書き戻しを有効にする {#enabling-xmp-writeback}

To enable the metadata changes to be propagated to the renditions of the asset when uploading it, modify the **Adobe CQ DAM Rendition Maker** configuration in Configuration Manager.

1. からConfiguration Managerを開きま `https://[aem_server]:[port]/system/console/configMgr`す。
1. **[!UICONTROL Adobe CQ DAM Rendition Makerの設定を開きます]** 。
1. Select the **[!UICONTROL Propagate XMP]** option, and then save the changes.

   ![chlimage_1-346](assets/chlimage_1-346.png)

## Enable XMP writeback for specific renditions {#enabling-xmp-writeback-for-specific-renditions}

XMP の書き戻し機能によって、選択されたレンディションにメタデータの変更が反映されるようにするには、これらのレンディションを DAM メタデータ書き戻しワークフローの「XMP の書き戻しプロセスワークフロー」ステップに指定します。デフォルトでは、このステップには元のレンディションが設定されています。

XMP の書き戻し機能でメタデータをレンディションサムネール 140.100.png および 319.319.png に反映するには、次の手順を実行します。

1. Experience Managerで、ツール/ワークフロー/ **[!UICONTROL モデルに移動します]**。
1. From the [!UICONTROL Models] page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. **[!UICONTROL DAM メタデータの書き戻し]**&#x200B;ページで、「**[!UICONTROL XMP の書き戻しプロセス]**」ステップを開きます。
1. **[!UICONTROL ステップのプロパティ]**&#x200B;ダイアログボックスで、「**[!UICONTROL プロセス]**」タブをタップまたはクリックします。
1. 「 **[!UICONTROL Arguments]** 」ボックスにを追加しま `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`す。「 **[!UICONTROL OK」をタップまたはクリックしま]**&#x200B;す。

   ![step_properties](assets/step_properties.png)

1. To regenerate the pyramid TIFF renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata Writeback workflow.
PTIFFレンディションは、ダイナミックメディアハイブリッドモードでのみローカルに作成および保存されます。 ワークフローを保存します。

The metadata changes are propagated to the renditions `thumbnail.140.100.png` and `thumbnail.319.319.png` of the asset, and not the others.

>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## XMPメタデータのフィルタ {#filtering-xmp-metadata}

AEM Assetsは、アセットバイナリから読み取られ、アセットの取り込み時にJCRに保存されるXMPメタデータのプロパティ/ノードのブラックリストフィルターとホワイトリストフィルターの両方をサポートしています。

ブラックリストフィルターは、除外するよう指定されたプロパティを除く、すべての XMP メタデータプロパティを読み込みます。ただし、膨大な量の XMP メタデータ（例えば、10,000 個のプロパティを持つ 1,000 個のノード）を含む INDD ファイルなどのアセットタイプの場合、フィルタリングするノードの名前が必ずしも事前にわかるわけではありません。ブラックリストフィルターで、大量の XMP メタデータを含む膨大な量のアセットを読み込むと、監視キューの遅滞など、安定性に関する問題が、AEM インスタンス／クラスターで発生する可能性があります。

この問題は、XMP メタデータのホワイトリストフィルターで解決できます。このフィルターは、読み込む XMP プロパティを定義するので、そこに定義されていない XMP プロパティや不明な XMP プロパティは無視されます。これらのプロパティをいくつかブラックリストフィルターに追加することで、後方互換性を確保できます。

>[!NOTE]
>
>フィルタリングは、アセットバイナリの XMP ソースから派生したプロパティに対してのみ機能します。EXIF 形式や IPTC 形式などの XMP 以外のソースから派生したプロパティについては、フィルタリングは機能しません。例えば、アセットの作成日は、`CreateDate` という名前のプロパティに EXIF TIFF 形式で格納されています。AEM では、この値を `exif:DateTimeOriginal`.という名前のメタデータフィールドに格納します。この場合は XMP 以外のソースなので、このプロパティにはフィルタリングは機能しません。

1. からConfiguration Managerを開きま `https://[aem_server]:[port]/system/console/configMgr`す。
1. **[!UICONTROL Adobe CQ DAM XmpFilter設定を開きます]** 。
1. ホワイトリストフィルターを適用するには、「**[!UICONTROL XMP プロパティにホワイトリストを追加]**」を選択し、「**[!UICONTROL XMP フィルタリングのホワイトリスト登録 XML 名]**」ボックスで読み込むプロパティを指定します。

   ![chlimage_1-347](assets/chlimage_1-347.png)

1. ホワイトリストフィルターを適用した後、ブラックリストに登録された XMP プロパティを除外するには、それらのプロパティを「**[!UICONTROL フィルタリングのブラックリスト登録 XML 名]**」ボックスに指定します。変更内容を保存します。

   >[!NOTE]
   >
   >「**[!UICONTROL Apply Blacklist to XMP Properties]**」チェックボックスは、デフォルトでオンになっています。つまり、ブラックリストフィルターは、デフォルトで有効になっています。To disable blacklist filtering, deselect **[!UICONTROL Apply Blacklist to XMP Properties]**.
