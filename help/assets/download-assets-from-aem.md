---
title: ' [!DNL Adobe Experience Manager]からデジタルアセットをダウンロードします。'
description: ' [!DNL Adobe Experience Manager] からアセットをダウンロードし、ダウンロード機能を有効または無効にする方法を説明します。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: ddfcb74451f41cea911700a64abceaaf47e7af49
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 74%

---


# [!DNL Adobe Experience Manager] からのアセットのダウンロード {#download-assets-from-aem}

静的レンディションおよび動的レンディションを含むアセットをダウンロードできます。または、アセットへのリンクを含む電子メールを [!DNL Adobe Experience Manager Assets] から直接送信できます。ダウンロードされたアセットは、ZIP ファイルにバンドルされています。書き出しジョブ用に圧縮する ZIP ファイルの最大サイズは 1 GB です。書き出しジョブあたり、最大で 500 個のアセットの合計を指定できます。

>[!NOTE]
>
>電子メールの受信者は、電子メールメッセージに含まれる ZIP ダウンロードリンクにアクセスするためには、`dam-users` グループのメンバーである必要があります。アセットをダウンロードするためには、アセットのダウンロードを起動するワークフローを開始する権限が必要です。

画像セット、スピンセット、混在メディアセット、カルーセルセットの各アセットタイプはダウンロードできません。

アセットをダウンロードするには、次の手順に従います。

1. AEMの左上隅にあるAEMロゴをタップし、左のナビゲーションバーの&#x200B;**[!UICONTROL ナビゲーション]**&#x200B;をタップします。
1. ナビゲーションページで、**[!UICONTROL アセット]**/**[!UICONTROL ファイルをタップします。]**
1. ダウンロードするアセットを含むフォルダーに移動します。
1. フォルダーを選択するか、フォルダー内の 1 つ以上のアセットを選択します。
1. ツールバーで、**[!UICONTROL ダウンロードをタップします。]**

   ![Experience Manager Assets からアセットをダウンロードする際に使用できるオプション](/help/assets/assets/asset_download_dialog.png)

   *図：ダウンロードダイアログボックスのオプション*

1. ダウンロードダイアログボックスで、目的のダウンロードオプションを選択します。

   | 書き出しまたはダウンロードオプション | 説明 |
   |---|---|
   | **[!UICONTROL アセットごとに別のフォルダーを作成]** | このオプションを選択すると、ダウンロードした各アセット（アセットの親フォルダーの下にネストされた子フォルダー内のアセットを含む）が、ローカルコンピューター上の 1 つのフォルダーに含まれます。このオプションを選択しない場合、デフォルトでは、フォルダー階層は無視され、すべてのアセットがローカルコンピューターの 1 つのフォルダーにダウンロードされます。 |
   | **[!UICONTROL 電子メール]** | ユーザーに電子メール通知が送信されます。次の場所にある標準の電子メールテンプレートを利用できます。<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> デプロイメント時にカスタマイズしたテンプレートは、次の場所で利用できます。 <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul>テナント固有のカスタムテンプレートは、次の場所に保存できます。<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`.</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`.</li></ul> |
   | **[!UICONTROL Assets]** | レンディションを含めずに、元の形式でアセットをダウンロードする場合に、このオプションを選択します。<br>オリジナルアセットにサブアセットがある場合は、サブアセットオプションを使用できます。 |
   | **[!UICONTROL レンディション]** | レンディションは、アセットのバイナリ表現です。アセットは、（アップロードされたファイルの）一次表現を持ちます。アセットは任意の数の追加の表現を持つことができます。<br>このオプションを選択すると、ダウンロードするレンディションを選択できます。使用できるレンディションは、選択したアセットに応じて異なります。 このオプションは、アセットにレンディションがある場合に使用できます。 |
   | **[!UICONTROL 動的レンディション]** | 一連の代替レンディションをリアルタイムで生成するには、このオプションを選択します。このオプションを選択する場合は、[画像プリセット](image-presets.md)リストから選択して、動的に作成するレンディションも選択します。 <br>さらに、サイズ、測定単位、形式、カラースペース、解像度および、画像の反転用などのオプションの画像修飾子を選択できます。このオプションは、[!DNL Dynamic Media] を有効にしている場合にのみ使用できます。 |

1. ダイアログボックスで、**[!UICONTROL 「ダウンロード」をタップします。]**

ダウンロードするフォルダーを選択すると、そのフォルダーの下位のアセットの階層全体がダウンロードされます。ダウンロードする各アセット（親フォルダーの下にネストされている子フォルダーのアセットを含む）を個々のフォルダーに格納するには、「**[!UICONTROL アセットごとに別のフォルダーを作成]**」を選択します。

## アセットダウンロードサーブレットの有効化 {#enable-asset-download-servlet}

[!DNL Experience Manager]のデフォルトサーブレットは、認証済みユーザーが、サーバーやネットワークに負荷をかける可能性のあるアセットのZIPファイルを作成するための、任意の大きさで同時にダウンロード要求を発行できるようにします。 この機能で生じる可能性がある DoS リスクを軽減するために、パブリッシュインスタンスに対しては、`AssetDownloadServlet` OSGi コンポーネントがデフォルトで無効になっています。

例えば Asset Share Commons やポータルのような実装などを使用する場合に DAM からアセットをダウンロードできるようにするには、OSGi 設定を通じてサーブレットを手動で有効にします。日常的なダウンロードの要件に影響を与えない範囲で、許容ダウンロードサイズをできるだけ小さく設定することをお勧めします。この値を大きくすれば、パフォーマンスに影響を与える可能性があります。

1. 発行実行モード(`config.publish`)をターゲットする命名規則を持つフォルダーを作成します。`/apps/<your-app-name>/config.publish`. 実行モードの設定プロパティを定義するには、[実行モード](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode)を参照してください。
1. Configurationフォルダーに、`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config`という名前の`nt:file`型のファイルを作成します。
1. `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` に以下を入力します。ダウンロードの最大サイズ（バイト単位）を `asset.download.prezip.maxcontentsize` の値として設定します。以下のサンプルでは、ZIP ダウンロードの最大サイズを 100 KB を超えないように設定しています。

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## アセットダウンロードサーブレットの無効化 {#disable-asset-download-servlet}

 パブリッシュインスタンスの `Asset Download Servlet` を無効にするには、アセットダウンロード要求をすべてブロックするように Dispatcher 設定を更新します。[!DNL Experience Manager]サーブレットは、OSGi コンソールから手動で直接無効にすることもできます。

1. ディスパッチャー設定を使用してアセットのダウンロード要求をブロックするには、`dispatcher.any`設定を編集し、[フィルターセクション](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#configuring-access-to-content-filter)にルールを追加します。`/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. 発行インスタンスでOSGiコンポーネントを無効にするには、`http://[aem_server]:[port]/system/console/components`にあるOSGiコンソールにアクセスします。 `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` を探して、「**[!UICONTROL 無効にする]**」をクリックします。

>[!MORELIKETHIS]
>
>* [DRM で保護されたアセットのダウンロード](drm.md)。
>* [Windows／Mac OS デスクトップで Adobe Experience Manager デスクトップアプリケーションを使用したアセットのダウンロード](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app.html).
>* [サポートされている Adobe Creative Cloud アプリ内から Adobe Asset Link を使用したアセットのダウンロード](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html).

