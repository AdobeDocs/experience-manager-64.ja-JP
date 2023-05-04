---
title: AEMでのアセットの並べ替えの強化
description: 方法 [!DNL Experience Manager] Assets：サーバー側の並べ替えがデプロイされ、クライアント側でバッチで並べ替えるのではなく、1 回でフォルダーアセットや検索クエリを並べ替えることができます。
contentOwner: AG
feature: Search
role: User
exl-id: aa24ca68-d94e-4bd4-a5cc-113906650a2e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 6%

---

# でのアセットの並べ替えの強化 [!DNL Experience Manager] {#enhanced-sorting-of-assets-in-aem}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

方法 [!DNL Experience Manager] Assets：サーバー側の並べ替えがデプロイされ、クライアント側でバッチで並べ替えるのではなく、1 回でフォルダーアセットや検索クエリを並べ替えることができます。

Adobe Experience Manager Assets の検索機能が強化され、フォルダーのリスト表示と検索結果ページで大量のアセットを効率的に並べ替えることができるようになりました。 タイムラインエントリを並べ替えることもできます。

[!DNL Experience Manager] Assets：サーバー側の並べ替えがデプロイされ、クライアント側でバッチで並べ替えるのではなく、フォルダー内のアセット全体（どれだけ大きくても対応可能）や検索クエリを一度に並べ替えることができます。 これにより、プリフェッチされた結果をユーザーインターフェイスにすばやく表示でき、並べ替え操作がより応答性と高速におこなわれます。

## リスト表示でのアセットの並べ替え {#sorting-assets-in-list-view}

[!DNL Experience Manager] Assets では、次のフィールドに基づいてフォルダーアセットを並べ替えることができます。

* ロケール
* ステータス
* タイプ
* サイズ
* レーティング
* 変更日
* 公開日
* 使用方法
* クリック
* インプレッション
* チェックアウト済み

1. 多数のアセットを含むフォルダーに移動します。
1. レイアウトアイコンをクリックまたはタップし、リスト表示に切り替えます。

   ![chlimage_1-394](assets/chlimage_1-394.png)

1. アセットのリストで、任意の列ヘッダーの横にある並べ替えアイコンをクリックまたはタップします。

   ![chlimage_1-395](assets/chlimage_1-395.png)

   アセットのリストは、フィールド値に基づいて並べ替えられます。

   ![chlimage_1-396](assets/chlimage_1-396.png)

>[!NOTE]
>
>の値を並べ替えるには `Name` または `Title`列、オーバーレイ `/libs/dam/gui/content/commons/availablecolumns` をクリックし、 `sortable` から `True`.

## 検索結果内のアセットの並べ替え {#sorting-assets-in-search-results}

次のフィールドに基づいて検索結果を並べ替えることができます。

* タイトル
* ステータス
* タイプ
* サイズ
* 変更日
* 公開日

1. オムニサーチボックスから、目的の条件に基づいてアセットを検索します。

   ![chlimage_1-397](assets/chlimage_1-397.png)

1. レイアウトアイコンをクリックまたはタップし、リスト表示に切り替えます。 検索結果がリスト表示に既に表示されている場合は、この手順をスキップしてください。
1. アセットのリストで、任意の列ヘッダーの横にある並べ替えアイコンをクリックまたはタップします。 アセットのリストは、フィールド値に基づいて並べ替えられます。

   ![chlimage_1-398](assets/chlimage_1-398.png)

## タイムラインでのアセットの並べ替え {#sorting-assets-in-timeline}

[!DNL Assets] では、注釈、バージョン、ワークフロー、アクティビティなどのタイムラインエントリを時系列に並べ替えることができます。

1. Assets UI で、タイムラインを表示するアセットを選択します。
1. グローバルナビゲーションアイコンをクリックまたはタップし、「 」を選択します。 **[!UICONTROL タイムライン]**.

   ![chlimage_1-399](assets/chlimage_1-399.png)

1. タイムラインで、リストからエントリを選択します。 例えば、「 **[!UICONTROL コメント]** ：アセットに関連付けられている注釈のリストを表示します。

   ![chlimage_1-400](assets/chlimage_1-400.png)

1. 次をクリックまたはタップします。 **[!UICONTROL 並べ替え]** 横のアイコン **[!UICONTROL 日付]** ラベル 選択内容に基づいて、注釈はアセットに追加された時系列または時系列順に表示されます。

   ![chlimage_1-401](assets/chlimage_1-401.png)
