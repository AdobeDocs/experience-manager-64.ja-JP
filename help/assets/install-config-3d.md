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
source-git-commit: e2bb2f17035e16864b1dc54f5768a99429a3dd9f

---


# AEM 3D のインストールと設定 {#installing-and-configuring-aem-d}

AEM 3D（バージョン3.0）のインストールと設定には、次のものが含まれます。

1. Autodesk® FBX® SDKライブラリをインストールします。
1. ネイティブ 3D コードパッケージをダウンロード、インストールします。
1. 3D アセット取り込みワークフローを設定して、AEM を再起動します。
1. AEM 3D の設定を確認します。

[3D アセットの使用](assets-3d.md)も参照してください。

前提条件、サポートするブラウザー、その他重要なリリース情報については、[AEM 3D Assets リリースノート](/help/release-notes/aem3d-release-notes.md)も参照してください。

[3D サイトのコンポーネントの使用](using-the-3d-sites-component.md)も参照してください。

>[!NOTE]
>
>3Dパッケージをダウンロードしてインストールする前に、必要なすべてのAEMパッケージが正常にインストールされていることを確認してください。 [AEM 3D リリースノート](install-config-3d.md)を参照してください。

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

   * Windows. AEMが存在するドライブと同じドライブにインストールします。
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
   * Mac または Windows デスクトップの場合は、管理者権限が必要です。

1. AEM へのアクセスに利用できる、サポートされているブラウザーがあることを確認します。

   [システム要件](/help/release-notes/aem3d-release-notes.md#system-requirements)を参照してください。

1. サポートされているブラウザーを使用して、管理者権限で AEM にログオンします。
1. In AEM, click the AEM logo to access the global navigation console, then click the **[!UICONTROL Tools]** icon and navigate to **[!UICONTROL Administration > Deployment > Package Share]**.
1. アドビのページで、Adobe ID 資格情報を使用して Adobe Creative Cloud アカウントにログオンします。
1. On the Adobe packages page, locate version 3.0.1 of `AEM-6.4-DynamicMedia-3D` feature pack, then download it.

1. AEM で、**[!UICONTROL ツール／管理／導入／パッケージマネージャー]**&#x200B;をクリックします。
1. ダウンロードした機能パックを検索して、「**[!UICONTROL インストール]**」をクリックします。

1. In the **[!UICONTROL Install Package]** dialog box, expand **Advanced Settings**, then set **[!UICONTROL Access Control Handling]** to **Merge**.
1. 「**[!UICONTROL インストール]**」をクリックしてパッケージのインストールを開始します。

   The file `sample-3D-content.zip` is placed in the **[!UICONTROL Assets]** root folder. 詳細は[AEM 3D の設定の確認](#validating-the-setup-of-aem-d)を参照してください。

## 3D アセット取り込みワークフローの設定と AEM の再起動 {#configuring-the-d-asset-ingestion-workflow-and-restarting-aem}

**3Dアセット取り込みワークフローを設定するには**:

1. In AEM, click the AEM logo to access the global navigation console, then click the **[!UICONTROL Tools]** icon and navigate to **[!UICONTROL Workflow > Models]**.
1. On the **[!UICONTROL Workflow Models]** page, hover over the **[!UICONTROL DAM Update Asset]** workflow, and when the check mark appears, select it.

1. ツールバーで、「**[!UICONTROL 編集]**」をクリックします。
1. On the **[!UICONTROL DAM Update Asset]** screen, in the AEM floating panel, click the **[!UICONTROL Plus]** icon to the right of Workflow to expand the list. リストで、「**[!UICONTROL プロセスステップ]**」を選択します。
1. 「 **[!UICONTROL Process Step]** 」をドラッグし、ワークフローの終わり近くにある **[!UICONTROL DAM Update Asset Workflow Completed]** コンポーネントの直前にドロップします。

   ![3d_process_step_underaem6-4](assets/3d_process_step_underaem6-4.png)

1. 新たに追加されたプロセスステップをダブルクリックします。
1. In the **[!UICONTROL Step Properties]** dialog box, under the **[!UICONTROL Common]** tab, in the **[!UICONTROL Title]** field, enter a suitable description for the process such as `Process 3D content`.
1. 「**[!UICONTROL プロセス]**」タブをクリックします。

1. From the **[!UICONTROL Process]** drop-down menu, select **[!UICONTROL Geometric 3D Object Service]**, then select the **[!UICONTROL Handler Advance]** check box.

   ![3d-install-process-steppropertiesdlg](assets/3d_install-process-steppropertiesdlg.png)

1. ダイアログボックスの右上隅近くにあるチェックマークアイコンをクリックして、DAMアセットを更新ページに戻ります。
1. 「 **[!UICONTROL DAMアセットを更新」ページの右上隅近くにある]** 「同期」をクリックし **** て、編集したワークフローモデルを保存します。
1. AEM を再起動します。

   再起動後、3Dコンテンツをアップロードし、AEMで処理する準備が整いました。

   [AEM 3D の設定の確認](#validating-the-setup-of-aem-d)に進みます。

## AEM 3D の設定の確認 {#validating-the-setup-of-aem-d}

1. AEM で、**[!UICONTROL ツール／アセット]**&#x200B;をクリックし、`sample-3D-content.zip` をダウンロードして、ダウンロードしたファイルを展開します。(AEMで削除できるよう `sample-3D-content.zip` になりました。)

   残りの手順でアップロードおよび処理のフィードバックを表示できるように、**[!UICONTROL カード表示]**&#x200B;になっていることを確認します。

1. Create a folder named `test3d` to receive test content.
1. Upload all files from `sample-3D-content/images` to the `test3d` folder.
1. アップロードと処理が完了するのを待機します。ブラウザーの更新が必要な場合があります。

   Upload the three `.fbx` files from `sample-3D-content/` to the `test3d` folder.

   .ma モデルファイルはまだアップロードしないでください。 

1. カード表示で、3D アセットカードに表示されるメッセージバナーを観察します。

   各アセットでは、複数の処理ステップがおこなわれます。**[!UICONTROL プレビュー]**&#x200B;の作成時…処理ステップが完了すると、カードがサムネール画像で更新されます。 最後の処理が完了すると、バナーが「**[!UICONTROL 新規]**」というインジケーターに置き換えられます。

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

AEM 3DでのAdobe Dimensionアセットのサポートをオプションで設定できます。

AEMでAdobe Dimension 3Dアセットの取り込み、プレビュー、および公開を可能にするには、外部変換サービスを設定する必要があります。 このサービスは、独自のAdobe Dimension(`.dn`)形式から、DNアセットと共にレンディションとして保存されるglTF（ファイル形式）の `.glb` バリアントに変換されます。 レンデ `.glb` ィションは、AEM Assets、Sites、Screensでの3DアセットのWebベースの表示に使用され、サードパーティアプリケーションでもダウンロードして使用できます。

>[!NOTE]
>
>コンバージョンサービスは、Amazon AWSでアドビがホストします。 サービスが適切に設定されると、AEM `.dn` にアップロードされたファイルは、Amazon S3の一時的なストレージを介して、安全に変換サービスにコピーされます。 変換結果は、一時的なS3ストレージを介してAEMに転送される。 すべての転送とストレージが保護されます。 また、コンテンツはS3およびコンバージョンサービスで短時間（通常は数分以下）のみ維持されます。

**Adobe Dimensionアセットのサポートを設定するには**:

1. アドビのAEMアカウントマネージャー、プロビジョニングエキスパートまたはサポート担当者に連絡して、 **AEM3Dサービスの資格情報を要求します**。

   >[!NOTE]
   >
   >各組織に必要な秘密鍵証明書のセットは1つだけです。秘密鍵証明書がインストールされているAEMインスタンスの数に関係ありません。

1. 次の情報を受け取ったことを確認します。

   * accountId
   * customerId
   * password
   * identityPoolId
   * userPoolId
   * clientId

1. 管理者として、資格情報をインストールするAEM作成者インスタンスにログインし、 **[!UICONTROL CRXDE Liteを開きます]**。
1. CRXDE liteで次の手順を実行して、新しい資格情報を設定します。

   1. に移動し、 `/libs/settings/dam/v3D/services/dncr` プロパティを `clientId` 新しい値に設定します。
   1. に移動し `/libs/settings/dam/v3D/services/aws` 、、、およびプロパテ `accountId`ィを新 `customerId`しい `identityPoolId``userPoolId` 値に設定します。
   1. 新しいパスワード値をプロパティに読み込 `encryptedPassword` みます。 この値は、「すべて保存」をタップすると自動的に **[!UICONTROL 暗号化されます]**。
   1. 「すべ **[!UICONTROL て保存]**」をタップし、ページを再読み込みして、プロパティに波括弧で囲まれた `encryptedPassword` 別の文字列が表示されていることを確認します。 この表示は、パスワードが正しく暗号化され、セキュリティで保護されていることを示します。

1. CRXDE Liteで次の操作を行って、 `.glb` 変換レンディションの形式を指 **[!UICONTROL 定します]**。

   1. CRXDE Liteでに移 `/libs/settings/dam/v3D/services/dncr` 動 **[!UICONTROL します]**。
   1. プロパティ `outputFormat` をまたはに設 `Dn` 定しま `generic`す。

      に設定すると、AEM `Dn`でDNア `.glb` セットを表示する際の画質を最適にするために、変換にはIBL照明などのアドビ固有の拡張機能が含まれます。 ただし、変換された.glbレンディションは、サードパーティアプリケーションでは正しくレンダリングされない場合があります。

      に設定した場合、レ `generic`ンディシ `.glb` ョンはAdobe固有の拡張子を持たない汎用になります。 この設定を使用すると、サードパーティアプリケーションで使用できますが、AEM 3D viewerでの表示は視覚的に最適化されません。

1. CRXDE liteで次の操作を行って、DNファイル形式を有効 **[!UICONTROL にします]**。

   1. `/libs/settings/dam/v3D/assetTypes/Dn` に移動します。
   1. Set the `Enabled` property to true.

1. 次の手順を実行して、設定を検証します。

   1. AEM Assetsを開きます。
   1. フォルダ `logo_sphere.dn` ーにアップロード `test3d` します。 ファイルはにあります `sample-3D-content/models`。

      `sample-3D-content.zip` は、基本の 3D 機能を検証するため、以前にダウンロード済みです。 
   1. Return to the **[!UICONTROL Card View]** and observe the message banner shown on the uploaded asset. **[!UICONTROL 変換]**&#x200B;形式…バナーは、変換処理の進行中に表示されます。
   1. すべての処理が完了したら、詳細ビューでアセットを開き **** 、変換されたアセットが正しく表示され、ビューアのナビゲーションコントロールが使用できることを確認します。
   ![image2018-11-2_15-51-19](assets/image2018-11-2_15-51-19.png)

   10 ～ 15分後にカード表示のDNアセットに「処理エラー」と表示さ **[!UICONTROL れた場合]** 、変換に失敗しました。

   その場合は、次の手順を実行して、コンバージョンのトラブルシューティングを行うことができます。

   * アセットを削除し、再度アップロードします。
   * CRXDE Liteですべての設定パラメーターが正しく設定されているこ **[!UICONTROL とを確認します]**。
   * 変換サービスとAWSエンドポイントへのアクセスをブロックしているファイアウォールがないことを確認します。
