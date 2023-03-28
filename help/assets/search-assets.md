---
title: AEMでのアセットの検索
description: フィルターパネルを使用した [!DNL Experience Manager] での必要なアセットの検索方法と検索で表示されたアセットの使用方法を説明します。
contentOwner: AG
feature: Search,Metadata
role: User
exl-id: cc1a5946-e13d-4433-a25a-d297fd07e2e4
source-git-commit: a778c3bbd0e15bb7b6de2d673b4553a7bd146143
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 22%

---

# [!DNL Experience Manager] でのアセットの検索  {#search-assets-in-aem}

フィルターパネルを使用した[!DNL Experience Manager]での必要なアセットの検索方法と検索で表示されたアセットの使用方法を説明します。

アセット、フォルダー、タグおよびメタデータを検索するには、フィルターパネルを使用します。ワイルドカードのアスタリスクを使用して、文字列の一部を検索できます。

フィルターパネルでは、一般的な分類順ではなく、複数の方法でアセットやフォルダーを検索する様々なオプションを提供します。

次のオプション（述語）に基づいて検索できます。

* ファイルタイプ
* ファイルサイズ
* フィールド名
* 最終変更
* ステータス
* 向き
* スタイル
* インサイト

<!-- TBD keystroke 65 article and port applicable changes here. This content goes. -->

フィルターパネルをカスタマイズし、[検索ファセット](search-facets.md)を使用して検索述語を追加したり、削除したりすることができます。フィルターパネルを表示するには、次の手順を実行します。

1. Assets ユーザーインターフェイスで、をタップまたはクリックします。 ![search_icon](assets/search_icon.png) をクリックして、「オムニサーチ」ボックスを表示します。
1. 検索語句を入力し、Enter キーを押します。 または、検索語句を入力せずに Enter キーを押します。 先頭にスペースを入れないでください。スペースを入れると、検索が機能しません。

1. グローバルナビゲーションアイコンをタップまたはクリックします。 フィルターパネルが表示されます。

   ![filters_panel-1](assets/filters_panel-1.png)

   検索する項目のタイプに応じて、検索結果の上部に一致数が表示されます。

   ![number_of_searches](assets/number_of_searches.png)

## ファイルタイプを検索 {#search-for-file-types}

フィルターパネルを使用すると、より精度の高い検索を実現でき、より多くの用途に使用できる検索機能を提供できます。 必要な詳細レベルまで簡単にドリルダウンできます。

例えば、画像を探している場合、 **[!UICONTROL ファイルタイプ]** 述語：ビットマップ画像とベクトル画像のどちらを使用するかを選択します。

![image_type](assets/image_type.png)

画像の MIME タイプを指定することで、検索範囲をさらに絞り込むことができます。

![mime_type](assets/mime_type.png)

同様に、ドキュメントを検索する場合は、PDF や MS Word などの形式を指定できます。

![文書](assets/documents.png)

## ファイルサイズに基づいて検索 {#search-based-on-file-size}

以下を使用： **ファイルサイズ** サイズに基づいてアセットを検索するための述語。 サイズ範囲の上限と下限を指定して、検索を絞り込むことができます。 また、単位（キロバイト、メガバイトなど）を指定することもできます。

![unit_of_measure](assets/unit_of_measure.png)

## アセットが最後に変更された日時に基づいて検索 {#search-based-on-when-assets-are-last-modified}

作業中のアセットを管理している場合や、レビューワークフローを監視している場合は、正確なタイムスタンプに基づいて、アセットが最後に変更された日時を検索できます。 例えば、アセットが変更された前または後の日付を指定します。

![last_modified_dates](assets/last_modified_dates.png)

また、次のオプションを使用して、検索の精度を高めることもできます。

![timestamp](assets/timestamp.png)

## ステータスに基づいて検索 {#search-based-on-status}

以下を使用： **ステータス** 公開、承認、チェックアウト、有効期限など、様々なタイプのステータスに基づいてアセットを検索するための述語。

![status](assets/status.png)

例えば、アセットの公開を監視する場合、適切なオプションを使用して、公開されているアセットを検索できます。

![publish](assets/publish.png)

アセットのレビューステータスを監視する場合は、該当するオプションを使用して、承認されているアセットまたは承認待ちのアセットを検索します。

![承認](assets/approval.png)

## インサイトデータに基づく検索 {#search-based-on-insights-data}

以下を使用： **インサイト** 様々な Creative アプリから取得した使用状況の統計に基づいてアセットを検索するための述語。 使用状況データは、次のカテゴリに分類されます。

* 使用状況のスコア
* インプレッション
* クリック
* アセットが表示されるメディアチャネル

![インサイト](assets/insights.png)
