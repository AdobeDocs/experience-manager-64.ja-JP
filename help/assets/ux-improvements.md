---
title: Assets のユーザーエクスペリエンスの強化
description: この記事では、 [!DNL Experience Manager] 6.4 アセット。
contentOwner: AG
feature: Release Information
role: Leader,User
exl-id: 65029113-987e-46eb-86eb-8028233031f9
source-git-commit: 1e3cd6ce3138113721183439f7cfb9daed6e0e58
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 66%

---

# Assets のユーザーエクスペリエンスの強化 {#user-experience-enhancements-in-assets}

[!DNL Experience Manager] 6.4 Assets には、シームレスなユーザーエクスペリエンスを提供し、生産性を向上させる、いくつかのユーザビリティの改善が含まれています。 市場開拓コンテンツの作成および管理速度の向上は、ビジネスのコンテンツ速度を改善します。

インターフェイスが応答性が高く、大規模なアセットポートフォリオを効率的に管理するのに役立ちます。 項目リストが長い場合でも、迅速に検索、表示、並べ替えおよびスムーズなスクロールをおこなうことができます。

カード、リスト、列などの様々な表示をパーソナライズできます。例えば、カード表示に表示するサムネールのサイズを設定できます。 リスト表示では、リスト内のアセットに対して表示する詳細レベルを設定できます。[!DNL Experience Manager] 6.4 Assets には新しいツリー表示が含まれています。これを使用すると、簡単にアセットリポジトリ内を移動してアセットを見つけることができます。

## 遅延読み込み {#lazy-loading}

でアセットを参照または検索するとき [!DNL Experience Manager] 6.4 Assets（一度に 200 個までのアセット）が表示されます。 結果をより速くスクロールできます。これは、長い結果リストを参照する場合に特に便利です。 大量のアセットが一度に読み込まれるので、スムーズに参照することができます。

アセットをタップまたはクリックして詳細ページをレビューした場合に、結果ページに戻るには、ツールバーの「戻る」ボタンをタップまたはクリックします。

## カード表示の改善 {#card-view-improvements}

使用するデバイスおよび必要な詳細の内容に応じて、カード表示のアセットのサムネールのサイズを変更できます。これにより、表示をパーソナライズして、表示されるサムネールの数を制御できます。

カード表示のサムネールのサイズを変更するには、次の手順を実行します。

1. ツールバーの「レイアウト」アイコンをタップまたはクリックし、 **[!UICONTROL 設定を表示]** オプション。

   ![view_settings](assets/view_settings.png)

1. 次の **[!UICONTROL 設定を表示]** ダイアログで、目的のサムネールサイズを選択し、をタップまたはクリックします。 **[!UICONTROL 更新]**.

   ![view_settings_dialog](assets/view_settings_dialog.png)

1. 選択したサイズで表示されるサムネールをレビューします。

   ![thumbnails_changed](assets/thumbnails_changed.png)

カード表示のタイルには、公開ステータスなどの追加情報が表示されています。

![publish_status](assets/publish_status.png)

## リスト表示の改善点 {#list-view-improvements}

リスト表示の最初の列には、デフォルトでアセットのファイル名が表示されます。公開ステータスや処理ステータス、ロケールなどの追加情報も表示されます。

![list_view](assets/list_view.png)

表示する詳細の内容を設定できます。「レイアウト」アイコンをタップまたはクリックして「**[!UICONTROL 設定を表示]**」オプションを選択し、**[!UICONTROL 設定を表示]**&#x200B;ダイアログで表示する列を指定します。

![view_settings_dialoglistview](assets/view_settings_dialoglistview.png)

## 列表示の改善点 {#column-view-improvements}

カード表示とリスト表示に加えて、列表示からアセットの詳細ページに移動できるようになりました。列表示のアセットを選択して、アセットのスナップショットの下の「**[!UICONTROL 詳細情報]**」をタップまたはクリックします。

![more_details](assets/more_details.png)

## ツリー表示 {#tree-view}

[!DNL Experience Manager] 6.4 Assets にはツリー表示があります。これを使用すると、簡単にアセット階層を参照して、目的のアセットやフォルダーに移動できます。

ツリー表示を開くには、 `Assets UI`を選択します。 **[!UICONTROL コンテンツツリー]** を選択します。

![content_tree](assets/content_tree.png)

コンテンツ階層から目的のアセットに移動します。

![navigate_contenttree](assets/navigate_contenttree.png)

## アセットの詳細への移動 {#navigating-asset-details}

アセットの詳細ページのツールバーに「前へ」ボタンと「次へ」ボタンが追加され、フォルダー内のすべての画像を連続して表示できるようになりました。

使用しているデバイスによって異なりますが、スワイプするか、キーボードの矢印キーを使用しても、画像間を移動できます。

選択したレイアウトによって異なりますが、次の方法でアセットの詳細ページを開くことができます。

| **表示** | **アセットの詳細ページを開く方法** |
|---|---|
| [!UICONTROL カード表示] | アセットタイルをタップまたはクリックします。 |
| [!UICONTROL リスト表示] | リスト内のアセットの行エントリをタップまたはクリックします。 |
| [!UICONTROL 列表示] | 次をタップまたはクリックします。 **[!UICONTROL 詳細]** ボタンをクリックします。 |

「前へ」ボタンと「次へ」ボタンを使用して、アセット間を移動します。

![prev_next_buttons](assets/prev_next_buttons.png)
