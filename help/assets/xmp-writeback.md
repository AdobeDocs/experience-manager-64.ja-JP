---
title: レンディションへの XMP の書き戻し
description: XMP の書き戻し機能を使用して、アセットのメタデータの変更を、そのアセットのすべてのレンディションまたは特定のレンディションに反映させる方法を学習します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b7180dcc7b50dca1c101a3fd28e031ef8e08f37f
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 46%

---


# レンディションへの XMP の書き戻し {#xmp-writeback-to-renditions}

Adobe Experience Manager（AEM）Assets のこの XMP の書き戻し機能は、アセットメタデータの変更をアセットのレンディションにレプリケートします。

アセットのメタデータをAEM Assets内から、またはアセットのアップロード中に変更すると、変更は最初にCrx-Deのアセットノード内に保存されます。

XMPの書き戻し機能は、アセットのすべてのレンディションまたは特定のレンディションにメタデータの変更を反映します。

「`Classic Leather`」というタイトルのアセットの「[!UICONTROL タイトル]」プロパティを「`Nylon`」に変更するシナリオについて考えます。

![メタデータ](assets/metadata.png)

この場合、AEM Assets ではこの「**[!UICONTROL タイトル]**」プロパティへの変更が、アセット階層に格納されたアセットメタデータ用の `dc:title` パラメーターに保存されます。

![metadata_stored](assets/metadata_stored.png)

ただし、AEM Assets では、メタデータの変更はアセットのレンディションに自動的に反映されません。

XMPの書き戻し機能を使用すると、メタデータの変更をアセットのすべてのレンディションまたは特定のレンディションに反映できます。 ただし、変更はアセット階層の metadata ノード以下には保存されません。代わりに、この機能によって、レンディションのバイナリファイル内に変更内容が埋め込まれます。

## XMPの書き戻しを有効にする {#enabling-xmp-writeback}

アセットのアップロード時にメタデータの変更をアセットのレンディションに反映させるには、設定マネージャーで「**Adobe CQ DAM Rendition Maker**」の設定を変更します。

1. からConfiguration Managerを開き `https://[aem_server]:[port]/system/console/configMgr`ます。
1. 「**[!UICONTROL Adobe CQ DAM Rendition Maker]**」設定を開きます。
1. 「**[!UICONTROL Propagate XMP]**」オプションを選択し、変更を保存します。

   ![chlimage_1-346](assets/chlimage_1-346.png)

## Enable XMP writeback for specific renditions {#enabling-xmp-writeback-for-specific-renditions}

XMP の書き戻し機能によって、選択されたレンディションにメタデータの変更が反映されるようにするには、これらのレンディションを DAM メタデータ書き戻しワークフローの「XMP の書き戻しプロセスワークフロー」ステップに指定します。デフォルトでは、このステップには元のレンディションが設定されています。

XMP の書き戻し機能でメタデータをレンディションサムネール 140.100.png および 319.319.png に反映するには、次の手順を実行します。

1. Experience Managerで、 **[!UICONTROL ツール/ワークフロー/モデルに移動します]**。
1. From the [!UICONTROL Models] page, open the **[!UICONTROL DAM Metadata Writeback]** workflow model.
1. **[!UICONTROL DAM メタデータの書き戻し]**&#x200B;ページで、「**[!UICONTROL XMP の書き戻しプロセス]**」ステップを開きます。
1. **[!UICONTROL ステップのプロパティ]**&#x200B;ダイアログボックスで、「**[!UICONTROL プロセス]**」タブをタップまたはクリックします。
1. In the **[!UICONTROL Arguments]** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`. Tap/click **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. To regenerate the pyramid TIFF renditions for Dynamic Media images with the new attributes, add the **[!UICONTROL Dynamic Media Process Image Assets]** step to the DAM Metadata Writeback workflow.
PTIFFレンディションは、Dynamic Mediaハイブリッドモードでのみローカルに作成および保存されます。 ワークフローを保存します。

The metadata changes are propagated to the renditions `thumbnail.140.100.png` and `thumbnail.319.319.png` of the asset, and not the others.

>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## XMP メタデータのフィルタリング {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] は、アセットバイナリから読み取られ、アセットが取り込まれる際にJCRに保存されるXMPメタデータのプロパティ/ノードのブロックリストと許可リストの両方のフィルタリングをサポートしています。

ブロックリストを使用してフィルタリングすると、除外用に指定したプロパティを除く、すべてのXMPメタデータプロパティを読み込むことができます。 ただし、膨大な量の XMP メタデータ（例えば、10,000 個のプロパティを持つ 1,000 個のノード）を含む INDD ファイルなどのアセットタイプの場合、フィルタリングするノードの名前が必ずしも事前にわかるわけではありません。ブロックリストを使用してフィルタリングすると、多数のXMPメタデータを持つ大量のアセットを読み込める場合、AEMインスタンスまたはクラスターで、ログに記録された監視キューなど、安定性の問題が発生する可能性があります。

許可リストを介したXMPメタデータのフィルタリングにより、読み込むXMPプロパティを定義できるので、この問題は解決されます。 この方法では、その他のXMPプロパティや不明なXMPプロパティは無視されます。 下位互換性を確保するために、ブロックリストを使用するフィルターにこれらのプロパティの一部を追加できます。

<!-- TBD: The instructions don't seem to match the UI. I see com.day.cq.dam.commons.metadata.XmpFilterBlackWhite.description
in Config Manager. And the settings are,
com.day.cq.dam.commons.metadata.XmpFilterBlackWhite.xmp.filter.apply_whitelist.name
com.day.cq.dam.commons.metadata.XmpFilterBlackWhite.xmp.filter.whitelist.name
com.day.cq.dam.commons.metadata.XmpFilterBlackWhite.xmp.filter.apply_blacklist.name
com.day.cq.dam.commons.metadata.XmpFilterBlackWhite.xmp.filter.blacklist.name
 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>フィルタリングは、アセットバイナリの XMP ソースから派生したプロパティに対してのみ機能します。EXIF 形式や IPTC 形式などの XMP 以外のソースから派生したプロパティについては、フィルタリングは機能しません。例えば、アセットの作成日は、`CreateDate` という名前のプロパティに EXIF TIFF 形式で格納されています。AEM stores this value in the metadata field named `exif:DateTimeOriginal`. この場合は XMP 以外のソースなので、このプロパティにはフィルタリングは機能しません。

1. からConfiguration Managerを開き `https://[aem_server]:[port]/system/console/configMgr`ます。
1. 「**[!UICONTROL Adobe CQ DAM XmpFilter]**」設定を開きます。
1. To apply filtering via an allowed list, select **[!UICONTROL Apply Allowlist to XMP Properties]**, and specify the properties to be imported in the **[!UICONTROL Allowed XML Names for XMP filtering]** box.

   ![chlimage_1-347](assets/chlimage_1-347.png)

1. 許可リストを介したフィルタリングを適用した後にブロックされたXMPプロパティをフィルタリングするには、「 **[!UICONTROL Blocked XML Names for XMP filtering]** 」ボックスでプロパティを指定します。 変更内容を保存します。

   >[!NOTE]
   >
   >The **[!UICONTROL Apply Blocklist to XMP Properties]** option is selected by default. つまり、ブロックリストを使用したフィルタリングは、デフォルトで有効になっています。 To disable such filtering, deselect the **[!UICONTROL Apply Blocklist to XMP Properties]** option.
