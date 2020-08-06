---
title: AEM 3DとAutodesk 3ds Maxの統合
seo-title: AEM 3DとAutoDesk 3ds Maxの統合
description: AEM 3DをAutodesk 3ds Maxソフトウェアと統合し、ネイティブ3ds Maxファイル(.MAX)をサポートすることもできます。 現在、3ds Maxによるレンダリングはサポートされていません。
seo-description: AEM 3DをAutodesk 3ds Maxソフトウェアと統合し、ネイティブ3ds Maxファイル(.MAX)をサポートすることもできます。 現在、3ds Maxによるレンダリングはサポートされていません。
uuid: 6c160ad3-6b6f-43f5-9e97-5b5d962a8d1a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
content-type: reference
topic-tags: 3D
discoiquuid: 0d7fefc0-6923-4ac3-9e90-335c08fa56f0
translation-type: tm+mt
source-git-commit: e2bb2f17035e16864b1dc54f5768a99429a3dd9f
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 8%

---


# AEM 3DとAutodesk 3ds Maxの統合 {#integrating-aem-d-with-autodesk-ds-max}

>[!NOTE]
>
>この作業はオプションで、Windows にのみ関連します。

AEM 3DをAutodesk 3ds Maxソフトウェアと統合し、ネイティブ3ds Maxファイル(.MAX)をサポートすることもできます。 現在、3ds Maxによるレンダリングはサポートされていません。

See [Advanced configuration settings](advanced-config-3d.md).

AEM 3DとAutoDesk Mayaの [統合も参照してください](integrate-maya-with-3d.md)。

**AEM 3DをAutodesk 3ds Max**：と統合するには

1. AEM Authorノードがインストールされているサーバと同じサーバにAutodesk 3ds Maxソフトウェアをインストールします。

   インストール後、Maya を開いて使用できること、および Maya のライセンスの問題がないことを確認します。

   >[!NOTE]
   >
   >アクセス拒否の問題を回避するには、AEMと同じ管理者ユーザーアカウントを使用して3ds Maxをインストールします。

1. 3ds Maxで、 **[!UICONTROL カスタマイズ/プラグインマネージャをクリックし]**&#x200B;ます。

   ステー `FBXMAX.DLU` タス **[!UICONTROL が]** [!UICONTROL loaded ****]であることを確認します。

   [ **[!UICONTROL プラグインマネージャ]** ]ダイアログボックスを閉じ、3ds Maxを閉じます。

1. 変換スクリプトを更新します。

   AEMは、コマンドラインスクリプトを使用して3ds Maxコマンドラインユーティリティを呼び出 `3dsmaxcmd.exe`します。 3ds Max 2016以外のバージョンをインストールした場合、または3ds Maxを非標準の場所にインストールした場合、またはAEMを別のパーティションまたはドライブにインストールした場合は、このスクリプトを編集する必要があります。

   1. CRXDE Liteを開き、に移動し `/libs/settings/dam/v3D/scripts/max`ます。
   1. 重複をクリック `export-fbx.bat` して開きます。
   1. 必要に応じて、スクリプトの最初の行を編集し、ユー `3dsmaxcmd.exe` ティリティの場所を反映します。 例えば、3ds Max 2017を使用し、AEMが別のディスクドライブにインストールされている場合は、次のようになります。

   ![image2018-6-22_13-35-8](assets/image2018-6-22_13-35-8.png)

1. Near the upper-left corner of the CRXDE Lite page, tap **[!UICONTROL Save All]**.

   Near the upper-left corner of the CRXDE Lite page, tap **[!UICONTROL Save All]**.

1. 作業フォルダを削除します（.MAXファイルを取り込もうとした場合にのみ必要）。

   1. CRXDE Lite で、`/libs/settings/dam/v3D/Paths/maxWorkPath` に移動します。デフォルトでは、この設定の値はAEM installのルートフォルダーに対する相対値 `./MaxWork`です。
   1. サーバー自体にログオンし、エクスプローラーを使用してAEM installのルートフォルダーに移動します。
   1. MaxWork **** フォルダ（内容全体を含む）が存在する場合は削除します。

      次回.MAXファイルを取り込むと、フォルダは自動的に再作成されます。

1. 次の操作を行って、 3ds Maxの取り込みを有効にします。

   1. CRXDE Liteで、 `/libs/settings/dam/v3D/assetTypes/max` Enabled **[!UICONTROL /有効]** プロパティに移動し、「true」に設定します。

   ![image2018-6-22_13-50-50](assets/image2018-6-22_13-50-50.png)

1. Near the upper-left corner of the CRXDE Lite page, tap **[!UICONTROL Save All]**.

## Testing the integration of AEM 3D with Autodesk 3ds Max {#testing-the-integration-of-aem-d-with-autodesk-ds-max}

1. Open AEM Assets, then upload the `.max` file located in `sample-3D-content/models` to the **[!UICONTROL test3d]** folder.

   sample-3D-content.zip は、基本の 3D 機能を検証するため、以前にダウンロード済みです。 

1. Return to the **[!UICONTROL Card]** view and observe the message banners shown on the uploaded assets.

   [変換形式]バナーは、3ds Maxがネイティブの3ds Max形式を.FBXに変換する際に表示されます。

1. 処理が完了したら、 `logo-sphere.max` 詳細 **** 表示でを開きます。

   プレビューエクスペリエンスは、と同じで `logo_sphere.fbx`す。

