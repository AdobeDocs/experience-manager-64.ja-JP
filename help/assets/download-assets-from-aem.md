---
title: からのデジタルアセットのダウンロード [!DNL Adobe Experience Manager].
description: ' [!DNL Adobe Experience Manager]  からアセットをダウンロードする方法とダウンロード機能を有効または無効にする方法について説明します。'
contentOwner: AG
feature: Asset Management,Asset Distribution
role: User
exl-id: bfe4d597-1080-4de5-a100-73a5175863d7
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 75%

---

# [!DNL Adobe Experience Manager] からのアセットのダウンロード  {#download-assets-from-aem}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

静的レンディションおよび動的レンディションを含むアセットをダウンロードできます。または、アセットへのリンクを含むメールを [!DNL Adobe Experience Manager Assets] から直接送信できます。ダウンロードされたアセットは、ZIP ファイルにバンドルされています。書き出しジョブ用に圧縮する ZIP ファイルの最大サイズは 1 GB です。書き出しジョブあたり、最大で 500 個のアセットの合計を指定できます。

>[!NOTE]
>
>メールの受信者は、メールメッセージに含まれる ZIP ダウンロードリンクにアクセスするためには、`dam-users` グループのメンバーである必要があります。アセットをダウンロードするためには、アセットのダウンロードを起動するワークフローを開始する権限が必要です。

画像セット、スピンセット、混在メディアセット、カルーセルセットの各アセットタイプはダウンロードできません。

アセットをダウンロードするには、次の手順に従います。

1. AEMの左上隅にある [!DNL Experience Manager] ロゴをクリックし、左側のレールでをタップします。 **[!UICONTROL ナビゲーション]**.
1. ナビゲーションページで、 **[!UICONTROL Assets]** > **[!UICONTROL ファイル。]**
1. ダウンロードするアセットを含むフォルダーに移動します。
1. フォルダーを選択するか、フォルダー内の 1 つ以上のアセットを選択します。
1. ツールバーで、 **[!UICONTROL ダウンロード。]**

   ![Experience Manager Assets からアセットをダウンロードする際に使用できるオプション](/help/assets/assets/asset_download_dialog.png)

   *図：ダウンロードダイアログボックスのオプション*

1. ダウンロードダイアログボックスで、目的のダウンロードオプションを選択します。

   | エクスポートまたはダウンロードのオプション | 説明 |
   |---|---|
   | **[!UICONTROL アセットごとに別のフォルダーを作成]** | このオプションを選択すると、ダウンロードした各アセット（アセットの親フォルダーの下にネストされた子フォルダー内のアセットを含む）が、ローカルコンピューター上の 1 つのフォルダーに含まれます。このオプションを選択しない場合、デフォルトでは、フォルダー階層は無視され、すべてのアセットがローカルコンピューターの 1 つのフォルダーにダウンロードされます。 |
   | **[!UICONTROL メール]** | ユーザーに電子メール通知が送信されます。 次の場所にある標準のメールテンプレートを利用できます。<ul><li>`/libs/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/libs/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> デプロイメント時にカスタマイズしたテンプレートは、次の場所で利用できます。 <ul><li>`/apps/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/apps/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul>テナント固有のカスタムテンプレートは、次の場所に保存できます。<ul><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/downloadasset`。</li><li>`/conf/<tenant_specific_config_root>/settings/dam/workflow/notification/email/transientworkflowcompleted`。</li></ul> |
   | **[!UICONTROL Assets]** | レンディションを含めずに、元の形式でアセットをダウンロードする場合に、このオプションを選択します。<br>オリジナルアセットにサブアセットがある場合は、サブアセットオプションを使用できます。 |
   | **[!UICONTROL レンディション]** | レンディションは、アセットのバイナリ表現です。 アセットには、アップロードされたファイルの主な表現があります。 アセットは任意の数の追加の表現を持つことができます。<br>このオプションを選択すると、ダウンロードするレンディションを選択できます。使用できるレンディションは、選択したアセットによって異なります。アセットにレンディションがある場合は、レンディションオプションを使用できます。 |
   | **[!UICONTROL 動的レンディション]** | 一連の代替レンディションをリアルタイムで生成するには、このオプションを選択します。また、このオプションを選択すると、動的に作成するレンディションを、 [画像プリセット](image-presets.md) リスト。 <br>さらに、サイズ、測定単位、形式、カラースペース、解像度および、画像の反転用などのオプションの画像修飾子を選択できます。このオプションは、[!DNL Dynamic Media] を有効にしている場合にのみ使用できます。 |

1. ダイアログボックスで、 **[!UICONTROL ダウンロード。]**.

ダウンロードするフォルダーを選択すると、そのフォルダーの下のアセット階層全体がダウンロードされます。 ダウンロードする各アセット（親フォルダーの下にネストされている子フォルダー内のアセットを含む）を個々のフォルダーに含めるには、 **[!UICONTROL アセットごとに別のフォルダーを作成]**.

## アセットダウンロードサーブレットの有効化 {#enable-asset-download-servlet}

[!DNL Experience Manager] のデフォルトサーブレットを使用すると、認証されたユーザーは、表示可能なアセットの ZIP ファイルを作成するために任意のサイズの同時ダウンロード要求を発行することができますが、その結果、サーバーやネットワークに過剰な負荷をかけるおそれがあります。この機能で生じる可能性がある DoS リスクを軽減するために、パブリッシュインスタンスに対しては、`AssetDownloadServlet` OSGi コンポーネントがデフォルトで無効になっています。

DAM からアセットをダウンロードできるようにするには（例えば、 Asset Share Commons や他のポータルのような実装を使用する場合）、OSGi 設定を介してサーブレットを手動で有効にします。 Adobeでは、日々のダウンロード要件に影響を与えることなく、許容されるダウンロードサイズをできる限り小さく設定することをお勧めします。 この値を大きくすれば、パフォーマンスに影響を与える可能性があります。

1. 次のように、パブリッシュ実行モードを対象とする命名規則（`config.publish`）でフォルダーを作成します：`/apps/<your-app-name>/config.publish`。実行モードの設定プロパティを定義するには、 [実行モード](/help/sites-deploying/configure-runmodes.md#defining-configuration-properties-for-a-run-mode)を参照してください。
1. config フォルダーに、`nt:file` タイプのファイル `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` を作成します。
1. `com.day.cq.dam.core.impl.servlet.AssetDownloadServlet.config` に以下を入力します。ダウンロードの最大サイズ（バイト単位）を `asset.download.prezip.maxcontentsize` の値として設定します。以下のサンプルでは、ZIP ダウンロードの最大サイズを 100 KB を超えないように設定しています。

   ```conf
   enabled=B"true"
   asset.download.prezip.maxcontentsize=I"102400"
   ```

## アセットダウンロードサーブレットの無効化 {#disable-asset-download-servlet}

 パブリッシュインスタンスの `Asset Download Servlet` を無効にするには、アセットダウンロード要求をすべてブロックするように Dispatcher 設定を更新します。[!DNL Experience Manager]サーブレットは、OSGi コンソールから手動で直接無効にすることもできます。

1. Dispatcher 設定を通じてアセットダウンロード要求をブロックするには、`dispatcher.any` 設定を編集し、[フィルターセクション](https://experienceleague.adobe.com/docs/?lang=jaexperience-manager-dispatcher/using/configuring/dispatcher-configuration.html#configuring-access-to-content-filter)にルールを追加します。`/0100 { /type "deny" /url "*.assetdownload.zip/assets.zip*" }`

1. パブリッシュインスタンスで OSGi コンポーネントを無効にするには、`http://[aem_server]:[port]/system/console/components` で OSGi コンソール にアクセスします。`com.day.cq.dam.core.impl.servlet.AssetDownloadServlet` を探して、「**[!UICONTROL 無効にする]**」をクリックします。

>[!MORELIKETHIS]
>
>* [DRM で保護されたアセットのダウンロード](drm.md)。
>* [Windows／Mac OS デスクトップで Experience Manager デスクトップアプリケーションを使用したアセットのダウンロード](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app.html)。
>* [サポートされている Adobe Creative Cloud アプリ内から Adobe Asset Link を使用したアセットのダウンロード](https://helpx.adobe.com/jp/enterprise/using/manage-assets-using-adobe-asset-link.html)。

