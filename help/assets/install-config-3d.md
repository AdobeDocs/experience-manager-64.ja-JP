---
title: AEM 3D のインストールと設定
seo-title: AEM 3D のインストールと設定
description: AEM 3D のインストールおよび設定方法を説明します。
seo-description: AEM 3D のインストールおよび設定方法を説明します。
uuid: a60732ff-fd66-4f29-b901-42a3cfd58b65
contentOwner: Rick Brough
topic-tags: 3D
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 5898d084-4b45-41bc-ad2e-2fcc65b0392c
translation-type: tm+mt
source-git-commit: 11b65cf2d180f04168d4c5d0929957c95a372e3c
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 31%

---


# AEM 3D のインストールと設定 {#installing-and-configuring-aem-d}

>[!IMPORTANT]
>
>AEM 6.4でのAEM 3Dのサポートは終了しました。 Adobeでは、 [AEMの3Dアセット機能をCloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/dynamicmedia/assets-3d.html)[またはAEM 6.5.3以降として使用することをお勧めします。](https://docs.adobe.com/content/help/en/experience-manager-65/assets/dynamic/assets-3d.html)

AEM 3D（バージョン3.0）のインストールと設定には、次が含まれます。

1. Autodesk® FBX® SDKライブラリをインストールする。
1. ネイティブ 3D コードパッケージをダウンロード、インストールします。
1. 3D アセット取り込みワークフローを設定して、AEM を再起動します。
1. AEM 3D の設定を確認します。

[3D アセットの使用](assets-3d.md)も参照してください。

前提条件、サポートするブラウザー、その他重要なリリース情報については、[AEM 3D Assets リリースノート](/help/release-notes/aem3d-release-notes.md)も参照してください。

[3D サイトのコンポーネントの使用](using-the-3d-sites-component.md)も参照してください。

>[!NOTE]
>
>3Dパッケージをダウンロードしてインストールする前に、必要なAEMパッケージがすべて正常にインストールされていることを確認してください。 [AEM 3D リリースノート](install-config-3d.md)を参照してください。

## Autodesk FBX SDK ライブラリのインストール {#installing-the-autodesk-fbx-sdk-library}

ネイティブ AEM 3D コードには、FBX ファイル形式をサポートする Autodesk FBX ライブラリが必要です。（アドビは、現在このライブラリを再配布できません。）

[詳細設定](advanced-config-3d.md)を参照してください。

1. AEM がインストールされたホストにログオンします。

   * Windows Server 導入の場合は、管理者としてサーバーにログオンします。
   * Mac または Windows デスクトップの場合は、管理者権限があることを確認します。

1. オペレーティングシステムに応じた適切なリンクを使用して **FBX SDK バージョン 2016.1.2** をダウンロードします。

   * **Windows**

      [https://download.autodesk.com/us/fbx_release_older/2016.1.2/fbx20161_2_fbxsdk_vs2010_win.exe](https://download.autodesk.com/us/fbx_release_older/2016.1.2/fbx20161_2_fbxsdk_vs2010_win.exe)

   * **OS X**

      [https://download.autodesk.com/us/fbx_release_older/2016.1.2/fbx20161_2_fbxsdk_clang_mac.pkg.tgz](https://download.autodesk.com/us/fbx_release_older/2016.1.2/fbx20161_2_fbxsdk_clang_mac.pkg.tgz)

   * **Linux**

      [https://download.autodesk.com/us/fbx_release_older/2016.1.2/fbx20161_2_fbxsdk_linux.tar.gz](https://download.autodesk.com/us/fbx_release_older/2016.1.2/fbx20161_2_fbxsdk_linux.tar.gz)

1. FBX SDK をインストールします。

   * Windows. AEMがあるドライブと同じドライブにインストールします。
   * Mac：AEM が配置されているのと同じパーティションにインストールします。
   * Linux. Extract the downloaded package and follow the instructions in `<yourFBXSDKpath>/Install_FbxFileSdk.txt`. Install the SDK to `/usr`.

## ネイティブ 3D コードパッケージのダウンロードとインストール {#downloading-and-installing-the-native-d-code-package}

>[!NOTE]
>
>AEM 3D のインストールおよび設定に進む前に、該当するサービスパックおよび他の関連する機能パックをすべて導入することをお勧めします。[AEM 3D リリースノート](/help/release-notes/aem3d-release-notes.md)を参照してください。

[詳細設定](advanced-config-3d.md)を参照してください。

**ネイティブ3Dコードパッケージをインストールするには**:

1. 次のいずれかの操作をおこないます。

   * Windows Server の導入の場合は、管理者としてサーバーにログオンします。
   * MacまたはWindowsデスクトップの場合は、管理者権限を持っていることを確認します。

1. AEM へのアクセスに利用できる、サポートされているブラウザーがあることを確認します。

   [システム要件](/help/release-notes/aem3d-release-notes.md#system-requirements)を参照してください。

1. ソフトウェア [配布ポータルにアクセスします](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)。 機能パックのバージョン3.0.1を探してダウンロード `AEM-6.4-DynamicMedia-3D` します。

1. AEM で、**[!UICONTROL ツール／管理／導入／パッケージマネージャー]**&#x200B;をクリックします。

1. ダウンロードした機能パックをAEMにアップロードします。 インストール先を探し、「 **[!UICONTROL インストール]**」をクリックします。

1. In the **[!UICONTROL Install Package]** dialog box, expand **Advanced Settings**, then set **[!UICONTROL Access Control Handling]** to **Merge**.
1. 「**[!UICONTROL インストール]**」をクリックしてパッケージのインストールを開始します。

   The file `sample-3D-content.zip` is placed in the **[!UICONTROL Assets]** root folder. 詳細は[AEM 3D の設定の確認](#validating-the-setup-of-aem-d)を参照してください。

## 3D アセット取り込みワークフローの設定と AEM の再起動 {#configuring-the-d-asset-ingestion-workflow-and-restarting-aem}

**3Dアセット取り込みワークフローを設定するには**:

1. In AEM, click the AEM logo to access the global navigation console, then click the **[!UICONTROL Tools]** icon and navigate to **[!UICONTROL Workflow > Models]**.
1. On the **[!UICONTROL Workflow Models]** page, hover over the **[!UICONTROL DAM Update Asset]** workflow, and when the check mark appears, select it.

1. ツールバーで、「**[!UICONTROL 編集]**」をクリックします。
1. **[!UICONTROL DAMアセットを更新画面のAEMフローティングパネルで、「ワークフロー」の右にある]** プラス **** (+)アイコンをクリックして、リストを展開します。 リストで、「**[!UICONTROL プロセスステップ]**」を選択します。
1. 「 **[!UICONTROL 処理手順]** 」をドラッグして、ワークフローの最後近くにある **[!UICONTROL DAM Update Asset Workflow Completed]** コンポーネントの直前にドロップします。

   ![3d_process_step_underaem6-4](assets/3d_process_step_underaem6-4.png)

1. 新たに追加されたプロセスステップをダブルクリックします。
1. **[!UICONTROL 手順のプロパティ]** ダイアログボックスの「 **[!UICONTROL 共通]** 」タブの「 **[!UICONTROL タイトル]** 」フィールドに、プロセスに適した説明（など）を入力し `Process 3D content`ます。
1. 「**[!UICONTROL プロセス]**」タブをクリックします。

1. From the **[!UICONTROL Process]** drop-down menu, select **[!UICONTROL Geometric 3D Object Service]**, then select the **[!UICONTROL Handler Advance]** check box.

   ![3d_install-process-steppropertiesdlg](assets/3d_install-process-steppropertiesdlg.png)

1. ダイアログボックスの右上隅近くにあるチェックマークアイコンをクリックして、DAMのアセットを更新ページに戻ります。
1. 「 **[!UICONTROL DAM Update Asset]** （アセットを更新） **[!UICONTROL 」ページの右上隅近くにある「]** 同期」をクリックし、編集したワークフローモデルを保存します。
1. AEM を再起動します。

   再起動後は、3Dコンテンツをアップロードし、AEMで処理する準備が整いました。

   [AEM 3D の設定の確認](#validating-the-setup-of-aem-d)に進みます。

## AEM 3D の設定の確認 {#validating-the-setup-of-aem-d}

1. AEM で、**[!UICONTROL ツール／アセット]**&#x200B;をクリックし、`sample-3D-content.zip` をダウンロードして、ダウンロードしたファイルを展開します。(AEMでは削除でき `sample-3D-content.zip` るようになりました)。

   残りの手順でアップロードおよび処理のフィードバックを表示できるように、**[!UICONTROL カード表示]**&#x200B;になっていることを確認します。

1. Create a folder named `test3d` to receive test content.
1. Upload all files from `sample-3D-content/images` to the `test3d` folder.
1. アップロードと処理が完了するのを待機します。ブラウザーの更新が必要な場合があります。

   Upload the three `.fbx` files from `sample-3D-content/` to the `test3d` folder.

   .ma モデルファイルはまだアップロードしないでください。 

1. カード表示で、3D アセットカードに表示されるメッセージバナーを観察します。

   各アセットでは、複数の処理ステップがおこなわれます。When the **[!UICONTROL Creating Preview...]** processing step completes, the card is updated with a thumbnail image. 最後の処理が完了すると、バナーが「**[!UICONTROL 新規]**」というインジケーターに置き換えられます。

   >[!NOTE]
   >
   >3D 処理中は、CPU 使用率が非常に高くなります。使用可能な CPU の処理能力によっては、すべての処理を完了するまでに相当の時間を要することがあります。

   ![screenshot_2017-01-2518-29-32](assets/screenshot_2017-01-2518-29-32.png)

1. 次に、ファイルの依存関係の解決方法について説明します。

   On the **[!UICONTROL Unresolved Dependencies]** banner for the `stage-helipad.fbx` card, click the **[!UICONTROL Exclamation Point]** icon to navigate to the asset&#39;s properties and open the **Dependencies** tab.

   ![chlimage_1-372](assets/chlimage_1-372.png)

1. Click the **[!UICONTROL Folder/Magnifying Glass]** icon to the right of the file name to open the asset browser and resolve the dependencies as follows:

   ![chlimage_1-373](assets/chlimage_1-373.png)

1. Click **[!UICONTROL Save]** and **[!UICONTROL Close]** to finish processing the asset and return to the **[!UICONTROL Card View]**, respectively.
1. When processing is complete, you see the following in **[!UICONTROL Card View]**:

   ![chlimage_1-374](assets/chlimage_1-374.png)

1. On the test3d page, click the `logo-sphere.fbx` card to open the model in **[!UICONTROL Detail View]**.

   logo-sphere.fbx ページの右上隅にあるステージスポットライトアイコンをクリックしてドロップダウンメニューを開き、`stage-spotlights.fbx` を選択します。

   ![chlimage_1-375](assets/chlimage_1-375.png)

1. From the **[!UICONTROL Stage Spotlight]** drop-down list, select `stage-helipad.fbx`.

   左マウスボタンを使用して、表示を調整します。背景およびモデルのライティングが変更され、新しいステージ選択が反映されます。

   ![chlimage_1-376](assets/chlimage_1-376.png)

## Adobe Dimensionアセットのサポートの設定 {#configuring-support-for-adobe-dimension-assets}

>[!NOTE]
>
>この設定タスクはオプションです。

必要に応じて、AEM 3DでのAdobe Dimensionアセットのサポートを設定できます。

AEM内のAdobe Dimension3Dアセットの取り込み、プレビュー、および公開を許可するには、外部変換サービスを設定する必要があります。 このサービスは、独自仕様のAdobe Dimension(`.dn`)形式から、Dnアセットと共にレンディションとして保存されるglTF(フ `.glb` ァイル形式)のバリアントに変換します。 この `.glb` レンディションは、AEM Assets、サイト、画面での3DアセットのWebベースの表示に使用され、サードパーティのアプリケーションで使用する場合にもダウンロードできます。

>[!NOTE]
>
>コンバージョンサービスは、AmazonAWSのAdobeによってホストされています。 サービスを適切に設定した後、AEMにアップロードされた `.dn` ファイルは、AmazonS3で一時ストレージを介して、安全に変換サービスにコピーされます。 変換結果は、一時的なS3ストレージを介してAEMに転送される。 すべての転送とストレージが保護されます。 また、コンテンツはS3でのみ保持され、コンバージョンサービスは短時間（通常、数分以内）です。

**Adobe Dimensionアセットのサポートを設定するには**:

1. AEM3Dサービスの資格情報を要求するには、AdobeのAEMアカウントマネージャー、プロビジョニングのエキスパート、またはサポート担当者に **お問い合わせください**。

   >[!NOTE]
   >
   >各組織に必要な資格情報のセットは1つだけです。資格情報がインストールされているAEMインスタンスの数に関係ありません。

1. 次の情報を受け取ったことを確認します。

   * accountId
   * customerId
   * password
   * identityPoolId
   * userPoolId
   * clientId

1. 管理者として、資格情報をインストールするAEM作成者インスタンスにログインし、 **[!UICONTROL CRXDE Liteを開きます]**。
1. CRXDE Liteで次の手順を実行して、新しい秘密鍵証明書の情報を設定します。

   1. に移動 `/libs/settings/dam/v3D/services/dncr` し、 `clientId` プロパティを新しい値に設定します。
   1. に移動 `/libs/settings/dam/v3D/services/aws` し、 `accountId`、 `customerId`、 `identityPoolId`および `userPoolId` プロパティを新しい値に設定します。
   1. プロパティに新しいパスワード値を読み込み `encryptedPassword` ます。 この値は、「すべて **[!UICONTROL 保存]**」をタップすると自動的に暗号化されます。
   1. 「すべて **[!UICONTROL 保存]**」をタップし、ページを再読み込みして、 `encryptedPassword` プロパティに別の文字列が波括弧で囲まれて表示されていることを確認します。 この表示は、パスワードが正しく暗号化され、セキュリティで保護されていることを示します。

1. 次の `.glb` CRXDE Liteを実行して、変換レンディションの形式を指定します ****。

   1. 「 `/libs/settings/dam/v3D/services/dncr` CRXDE Lite **[!UICONTROL 内」に移動します]**。
   1. この `outputFormat` プロパティをまたはに設定し `Dn` ま `generic`す。

      に設定 `Dn`すると、AEMでDnアセットを表示する際の画質を最適にするために、 `.glb` 変換にはAdobe固有の拡張（IBL照明など）が含まれます。 ただし、変換された.glbレンディションは、サードパーティのアプリケーションでは正しくレンダリングされない場合があります。

      に設定した場合 `generic``.glb` 、レンディションは汎用で、Adobe固有の拡張子はありません。 この設定を使用すると、AEM 3D Viewerでの表示が最適でない場合に、サードパーティアプリケーションでの使用が可能になります。

1. **[!UICONTROL CRXDE Liteで次の操作を行い、Dnファイル形式を有効にします]**。

   1. `/libs/settings/dam/v3D/assetTypes/Dn` に移動します。
   1. Set the `Enabled` property to true.

1. 次の手順を実行して、設定を検証します。

   1. AEM Assetsを開けて。
   1. フォルダ `logo_sphere.dn` ーにアップロード `test3d` します。 ファイルはにあり `sample-3D-content/models`ます。

      `sample-3D-content.zip` は、基本の 3D 機能を検証するため、以前にダウンロード済みです。 
   1. Return to the **[!UICONTROL Card View]** and observe the message banner shown on the uploaded asset. 変換処理中は、 **[!UICONTROL 変換形式。.]** .バナーが表示されます。
   1. すべての処理が完了したら、 **** 詳細表示でアセットを開き、変換されたアセットが正しく表示され、ビューアのナビゲーションコントロールが使用可能であることを確認します。

   ![image2018-11-2_15-51-19](assets/image2018-11-2_15-51-19.png)

   10 ～ 15分後に **[!UICONTROL カード表示のDnアセットに「Processing Error」と表示される場合は]** 、変換に失敗しました。

   その場合は、次の手順を実行して、変換のトラブルシューティングを行うことができます。

   * アセットを削除してから、もう一度アップロードします。
   * すべての設定パラメーターが **[!UICONTROL CRXDE Liteで正しく設定されていることを確認します]**。
   * 変換サービスとAWSエンドポイントへのアクセスをブロックしているファイアウォールがないことを確認します。
