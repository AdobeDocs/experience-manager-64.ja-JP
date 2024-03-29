---
title: メタデータ、画像およびビデオを処理するためのプロファイル
description: プロファイル：フォルダーにアップロードされるアセットに適用されるオプションに関する一連のルールです。 アップロードするビデオアセットに適用するメタデータプロファイルおよびビデオエンコーディングプロファイルを指定します。 画像アセットの場合、画像アセットを適切に切り抜くために、画像アセットに適用するイメージプロファイルを指定することもできます。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: administering
content-type: reference
feature: Workflow,Asset Management,Renditions
role: User,Admin
exl-id: 78d76b4f-a46c-4ffc-b772-ed925eb8e34c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 80%

---

# メタデータ、画像およびビデオを処理するためのプロファイルについて {#profiles-for-processing-metadata-images-and-videos}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

プロファイルとは、フォルダーにアップロードされるアセットに適用するオプションを指定したファイルです。例えば、アップロードするビデオアセットに適用するメタデータプロファイルおよびビデオエンコーディングプロファイルを指定できます。また、画像アセットを適切に切り抜くために画像アセットに適用するイメージプロファイルを指定できます。

例えば、メタデータの追加、画像のスマート切り抜き、ビデオエンコーディングプロファイルの確立などをおこなえます。 AEMでは、3 種類のプロファイルを作成できます。次のリンク先では、これらのプロファイルについて詳しく説明しています。

* [メタデータプロファイル](metadata-profiles.md)
* [イメージプロファイル](image-profiles.md)
* [ビデオプロファイル](video-profiles.md)

メタデータ、画像またはビデオプロファイルを作成、編集および削除するには、管理者権限が必要です。

メタデータ、画像またはビデオプロファイルを作成したら、新しくアップロードするアセットのアップロード先として使用する 1 つ以上のフォルダーにそのプロファイルを割り当てます。

でのプロファイルの使用に関する重要な概念 [!DNL Experience Manager] アセットは、フォルダーに割り当てられます。 プロファイル内では、メタデータプロファイルの形式で、ビデオプロファイルまたはイメージプロファイルと共に設定されています。これらの設定は、フォルダーのコンテンツを（そのサブフォルダーのコンテンツを含めて）処理します。したがって、ファイルやフォルダーの命名方法、サブフォルダーの配置方法、これらのフォルダー内のファイルの処理方法は、プロファイルによるこれらのアセットの処理方法に大きな影響を与えます。 適切なメタデータプラクティスと一緒に、一貫性のある適切なファイルおよびフォルダーの命名戦略を使用することで、デジタルアセットコレクションを最大限に活用して、適切なファイルを適切なプロファイルによって処理することができます。例については、 [フォルダーを使用してアセットを整理する](organize-assets.md#organize-using-folders).

>[!NOTE]
>
>あるフォルダーから別のフォルダーに移動するアセットは再処理されません。例えば、フォルダー 1 にプロファイル A が割り当てられ、フォルダー 2 にプロファイル B が割り当てられているとします。アセットをフォルダー 1 からフォルダー 2 に移動しても、そのアセットには、元の処理がフォルダー 1 から引き継がれます。
>
>同じプロファイルが割り当てられている 2 つのフォルダー間でアセットを移動する場合にも、同じことが言えます。

## フォルダー内のアセットの再処理 {#reprocessing-assets}

>[!NOTE]
>
> 6.4.7.0 以降の *Dynamic Media ー Scene7 mode* にのみ適用されます。[!DNL Experience Manager]

後で変更した既存の処理プロファイルがあるフォルダー内のアセットを再処理できます。

例えば、画像プロファイルを作成してフォルダーに割り当てたとします。フォルダーにアップロードした画像アセットには、画像プロファイルが自動的にアセットに適用されます。ただし、後でプロファイルに新しいスマート切り抜き率を追加することにします。その場合は、もう一度アセットを選択してフォルダーに再度アップロードするのではなく、「*Scene7 : アセットを再処理*」ワークフローを実行するだけです。

処理が初めて失敗したアセットに対して、再処理ワークフローを実行できます。したがって、処理プロファイルを編集していない場合や適用していない場合でも、アセットのフォルダーに対していつでも再処理ワークフローを実行できます。

オプションで、再処理ワークフローのバッチサイズを、デフォルトの 50 アセットから最大 1,000 アセットまで調整できます。フォルダーに対して「_Scene7：アセットを再処理_」ワークフローを実行すると、アセットは一括でグループ化された後、Dynamic Media サーバーに送信されて処理されます。処理の後、バッチセット全体の各アセットのメタデータが AEM 上で更新されます。バッチサイズが非常に大きい場合は、処理に遅延が生じる可能性があります。また、バッチサイズが小さすぎると、Dynamic Media サーバーへのラウンドトリップの数が多くなりすぎるおそれがあります。

詳しくは、[再処理ワークフローのバッチサイズの調整](#adjusting-load)を参照してください。

>[!NOTE]
>
>Dynamic Media Classic から AEM へのアセットの一括移行を実行する場合は、Dynamic Media サーバー上で移行レプリケーションエージェントを有効にする必要があります。移行が完了したら、このエージェントを必ず無効にします。再処理ワークフローが期待どおりに動作するように、Dynamic Media サーバー上で移行公開エージェントを無効にする必要があります。

<!-- Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. -->

**フォルダー内のアセットを再処理するには**：

1. AEM のアセットページで、処理プロファイルが割り当てられている、「**Scene7 : アセットを再処理**」ワークフローの適用対象となるアセットフォルダーに移動します。

   既に処理プロファイルが割り当てられているフォルダーには、カード表示のフォルダー名のすぐ下にプロファイルの名前が表示されます。

1. フォルダーを選択します。

   * 選択したフォルダー内のすべてのファイルがワークフローで再帰的に考慮されます。
   * 選択したメインフォルダー内にアセットを含んだ 1 つ以上のサブフォルダーが存在する場合、ワークフローはフォルダー階層内のあらゆるアセットを再処理します。
   * ベストプラクティスとしては、1,000 個を超えるアセットを含んだフォルダー階層に対しては、このワークフローを実行しないでください。

1. ページの左上隅付近にあるドロップダウンリストで「**[!UICONTROL タイムライン]**」をクリックします。
1. ページ左下隅付近の「コメント」フィールドの右側にあるカラットアイコン（**^**）をクリックします。

   ![アセット再処理ワークフロー（その 1）](/help/assets/assets/reprocess-assets1.png)

1. 「**[!UICONTROL ワークフローを開始]**」をクリックします。
1. 「**[!UICONTROL ワークフローを開始]**」ドロップダウンリストから「**[!UICONTROL Scene7：アセットを再処理]**」を選択します。
1. （オプション）「**ワークフローのタイトルを入力**」テキストフィールドに、ワークフローの名前を入力します。必要に応じて、ワークフローインスタンスを参照する名前を使用できます。

   ![アセット再処理ワークフロー（その 2）](/help/assets/assets/reprocess-assets2.png)

1. 「**[!UICONTROL 開始]**」をクリックした後、「**[!UICONTROL 確認]**」をクリックします。

   ワークフローを監視したり、進行状況を確認するには、「 [!DNL Experience Manager] メインコンソールページ、「 **[!UICONTROL ツール/ワークフロー]**. ワークフローインスタンスページで、ワークフローを選択します。メニューバーの「**[!UICONTROL 履歴を開く]**」をクリックします。同じワークフローインスタンスページで、選択したワークフローの終了、休止、名前変更を行うこともできます。

### 再処理ワークフローのバッチサイズの調整 {#adjusting-load}

（オプション）再処理ワークフローのデフォルトのバッチサイズは、1 ジョブあたり 50 アセットです。この最適なバッチサイズは、再処理の実行対象となるアセットの平均アセットサイズと MIME タイプによって決まります。値を大きくすると、1 回の再処理ジョブのファイル数が多くなります。従って、処理バナーはオンのままになる [!DNL Experience Manager] アセットを長時間使用できます。 ただし、平均ファイルサイズが小さい（1 MB 以下の）場合は、値を数百個（1000 以下）に増やすことをお勧めします。平均ファイルサイズが大きい（数百 MB の）場合は、バッチサイズを最大 10 までに減らすことをお勧めします。

**再処理ワークフローのバッチサイズを調整するには（オプション）**：

1. Adobe Experience Manager で、「**[!UICONTROL Adobe Experience Manager]**」をタップしてグローバルナビゲーションコンソールにアクセスし、**[!UICONTROL ツール]**（ハンマーアイコン）／**[!UICONTROL ワークフロー／モデル]**&#x200B;をタップします。
1. ワークフローモデルページのカード表示またはリスト表示で、「**[!UICONTROL Scene7：アセットを再処理]**」を選択します。

   ![カード表示で「Scene7：アセットを再処理」ワークフローが選択されたワークフローモデルページ](/help/assets/assets-dm/reprocess-assets7.png)

1. ツールバーの「**[!UICONTROL 編集]**」をクリックします。新しいブラウザータブに、「Scene7：アセットを再処理」ワークフローモデルページが開きます。
1. 「Scene7：アセットを再処理」ワークフローページで、右上隅付近の「**[!UICONTROL 編集]**」をタップして、ワークフローを「ロック解除」します。
1. ワークフローで、Scene7 バッチアップロードコンポーネントを選択してツールバーを開き、ツールバーの「**[!UICONTROL 設定]**」をタップします。

   ![Scene7 バッチアップロードコンポーネント](/help/assets/assets-dm/reprocess-assets8.png)

1. **[!UICONTROL Scene7 へのバッチアップロード ー ステップのプロパティ]**&#x200B;ダイアログボックスで、以下の設定をおこないます。
   * 「**[!UICONTROL タイトル]**」および「**[!UICONTROL 説明]**」テキストフィールドに、必要に応じて、ジョブの新しいタイトルと説明を入力します。
   * ハンドラーが次のステップに進む場合は、「**[!UICONTROL ハンドラー処理の設定]**」を選択します。
   * 「**[!UICONTROL タイムアウト]**」フィールドに、外部プロセスのタイムアウト（秒）を入力します。
   * 「**[!UICONTROL 期間]**」フィールドに、外部プロセスが完了したかどうかを確認するポーリング間隔（秒）を入力します。
   * 「**[!UICONTROL バッチ]**」フィールドに、Dynamic Media サーバーのアップロードジョブのバッチ処理で処理するアセットの最大数（50～1,000）を入力します。
   * タイムアウトに達したときに先に進む場合は、「**[!UICONTROL タイムアウトで先に進む]**」を選択します。タイムアウトに達したときにインボックスまで進む場合は、選択を解除します。

   ![プロパティダイアログボックス](/help/assets/assets-dm/reprocess-assets3.png)

1. **[!UICONTROL Scene7 へのバッチアップロード - ステップのプロパティ]**&#x200B;ダイアログボックスの右上隅にある「**[!UICONTROL 完了]**」をタップします。

1. 「Scene7：アセットを再処理」ワークフローモデルページの右上隅にある「**[!UICONTROL 同期]**」をタップします。見た時 **[!UICONTROL 同期済み]**&#x200B;の場合、ワークフローランタイムモデルは正常に同期され、フォルダー内のアセットを再処理する準備が整います。

   ![ワークフローモデルの同期](/help/assets/assets-dm/reprocess-assets1.png)

1. 「Scene7：アセットを再処理」ワークフローモデルを表示しているブラウザータブを閉じます。

<!-- 1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/assets/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/assets/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main [!DNL Experience Manager] console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model. -->
