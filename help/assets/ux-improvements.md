---
title: Assets でのユーザーエクスペリエンスの強化
description: この記事では、 [!DNL Experience Manager] 6.4 アセット。
contentOwner: AG
feature: Release Information
role: Leader,User
exl-id: 65029113-987e-46eb-86eb-8028233031f9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# Assets でのユーザーエクスペリエンスの強化 {#user-experience-enhancements-in-assets}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[!DNL Experience Manager] 6.4 Assets には、シームレスなユーザーエクスペリエンスを提供し、生産性を向上させる、いくつかのユーザビリティの改善が含まれています。 市場投入コンテンツを作成/管理する速度が向上すると、ビジネスのコンテンツベロシティが向上します。

インターフェイスが応答性が高く、大規模なアセットポートフォリオを効率的に管理するのに役立ちます。 長い項目のリストをすばやく検索、表示、並べ替え、スムーズにスクロールできます。

カード表示、リスト表示、列表示など、様々な表示をパーソナライズできます。 例えば、カード表示に表示するサムネールのサイズを設定できます。 リスト表示では、リスト内のアセットに表示する詳細レベルを設定できます。 [!DNL Experience Manager] 6.4 Assets には、Assets リポジトリ内を移動してアセットを探すことができる新しいツリービューが追加されました。

## 遅延読み込み {#lazy-loading}

でアセットを参照または検索するとき [!DNL Experience Manager] 6.4 Assets（一度に 200 個までのアセット）が表示されます。 結果をより速くスクロールできます。これは、長い結果リストを参照する場合に特に便利です。 一度に大量のアセットが読み込まれるので、スムーズに参照できます。

アセットをタップまたはクリックして詳細ページを確認した場合は、ツールバーの「戻る」ボタンをタップまたはクリックするだけで、結果ページに戻ることができます。

## カード表示の改善 {#card-view-improvements}

使用するデバイスと必要な詳細の量に応じて、カード表示でアセットのサムネールのサイズを変更できます。 これにより、表示をパーソナライズし、表示されるサムネールの数を制御できます。

カード表示でサムネールのサイズを変更するには、次の手順を実行します。

1. ツールバーの「レイアウト」アイコンをタップまたはクリックし、 **[!UICONTROL 設定を表示]** オプション。

   ![view_settings](assets/view_settings.png)

1. 次の **[!UICONTROL 設定を表示]** ダイアログで、目的のサムネールサイズを選択し、をタップまたはクリックします。 **[!UICONTROL 更新]**.

   ![view_settings_dialog](assets/view_settings_dialog.png)

1. 選択したサイズで表示されるサムネールを確認します。

   ![thumbnails_changed](assets/thumbnails_changed.png)

カード表示のタイルに、公開ステータスなどの追加情報が表示されるようになりました。

![publish_status](assets/publish_status.png)

## リスト表示の改善点 {#list-view-improvements}

リスト表示の最初の列に、デフォルトでアセットのファイル名が表示されるようになりました。 公開や処理のステータスやロケールなどの追加情報も表示されます。

![list_view](assets/list_view.png)

表示する詳細の数を設定できます。 レイアウトアイコンをタップまたはクリックし、 **[!UICONTROL 設定を表示]** オプションを選択し、 **[!UICONTROL 設定を表示]** ダイアログ。

![view_settings_dialoglistview](assets/view_settings_dialoglistview.png)

## 列表示の改善点 {#column-view-improvements}

カード表示とリスト表示に加えて、列表示からアセットの詳細ページに移動できるようになりました。 列表示からアセットを選択し、をタップまたはクリックします。 **[!UICONTROL 詳細]** をクリックします。

![more_details](assets/more_details.png)

## ツリー表示 {#tree-view}

[!DNL Experience Manager] 6.4 Assets には、アセット階層を簡単に参照し、目的のアセットまたはフォルダーに移動できるツリービューが含まれています。

ツリー表示を開くには、 `Assets UI`を選択します。 **[!UICONTROL コンテンツツリー]** を選択します。

![content_tree](assets/content_tree.png)

コンテンツ階層から目的のアセットに移動します。

![navigate_contenttree](assets/navigate_contenttree.png)

## アセットの詳細への移動 {#navigating-asset-details}

アセットの詳細ページのツールバーに「前へ」ボタンと「次へ」ボタンが追加され、フォルダー内のすべての画像を連続して表示できるようになりました。

デバイスに応じて、スワイプまたはキーボードの矢印キーを使用して、画像間を前後に移動することもできます。

選択したレイアウトに応じて、次の方法でアセットの詳細ページを開くことができます。

| **表示** | **アセットの詳細ページを開く方法** |
|---|---|
| [!UICONTROL カード表示] | アセットタイルをタップまたはクリックします。 |
| [!UICONTROL リスト表示] | リスト内のアセットの行エントリをタップまたはクリックします。 |
| [!UICONTROL 列表示] | 次をタップまたはクリックします。 **[!UICONTROL 詳細]** ボタンをクリックします。 |

前へ/次へボタンを使用して、アセット間を前後に移動します。

![prev_next_buttons](assets/prev_next_buttons.png)
