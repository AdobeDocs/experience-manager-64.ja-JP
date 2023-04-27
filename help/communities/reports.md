---
title: レポートコンソール
seo-title: Reports Console
description: レポートへのアクセス方法を説明します
seo-description: Learn how to access reports
uuid: 580f5eb8-24b2-4404-90d4-81f7108d1ee6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0042893e-3d2c-469e-8759-404be16e7436
role: Admin
exl-id: 766711ea-f3d3-49ab-8346-4e4477c261bd
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 7%

---

# レポートコンソール {#reports-console}

## 概要 {#overview}

AEM Communitiesの場合、オーサー環境から様々な方法でアクセスできるレポートがあります。

一般に、様々なレポートは次のようになります。

* [割り当てレポート](#assignments-report) - [実施可能コミュニティ](overview.md#enablement-community)は、SCORM 標準を実装する場合に関連するスコアを含め、学習者の割り当てに関する進捗の概要を提供します
* [表示レポート](#views-report)  — コミュニティサイトのコミュニティメンバーおよびサイト訪問者別に、コンテンツのビュー数のグラフを表示します。
* [投稿レポート](#posts-report)  — コミュニティメンバーがコミュニティサイトに投稿した様々なタイプの投稿のグラフを表示します

条件 [Adobe Analyticsが有効](sites-console.md#analytics)を使用すると、各イネーブルメントリソースの表示数、再生数、コメント数、評価数がレポートに含まれます

表形式のレポートは、後で処理するために.csv 形式で書き出すことができます。

## レポートコンソール {#reporting-consoles}

### コミュニティサイトのレポート {#reports-for-community-sites}

* グローバルナビゲーションから： **[!UICONTROL ナビゲーション/コミュニティ/レポート]**
* 次から選択：
   * **[!UICONTROL 割り当てレポート]**
      * 選択したコミュニティサイト、ユーザーまたはグループ、および割り当てに関するレポートを生成する
   * **[!UICONTROL 投稿レポート]**
      * 選択したコミュニティサイト、コンテンツタイプ、期間に関するレポートを生成します
   * **[!UICONTROL 表示レポート]**
      * 選択したコミュニティサイト、コンテンツタイプ、期間に関するレポートを生成します
         ![chlimage_1-156](assets/chlimage_1-156.png)

### イネーブルメントリソースおよび学習パスに関するレポート {#reports-for-enablement-resources-and-learning-paths}

* グローバルナビゲーションから： **[!UICONTROL ナビゲーション/コミュニティ/リソース]**
* 既存のイネーブルメントコミュニティサイトを選択
   * 選択 **[!UICONTROL レポート]** すべてのイネーブルメントリソースをカバーするレポートを生成するアイコン
   * イネーブルメント学習パスを選択
   * 選択 **[!UICONTROL レポート]** アイコン
      * 含まれるイネーブルメントリソース
      * 学習パスに割り当てられた学習者
* 以下のレポートが表示されます。
   * テーブルデータ（CSV としてダウンロード可能）
      * 学習者の識別
      * ステータス
      * カタログを通じて割り当てるかアクセスするか
      * 行われたコメント数
      * 与えられた星評価

詳しくは、 [レポートセクション](resources.md#report) 」と入力します。

## 割り当てレポート {#assignments-report}

割り当てコンソールを使用すると、イネーブルメントコミュニティサイト、ユーザーまたはグループ、割り当てによってレポートをフィルタリングできます。

レポートには、進行状況に関する情報と、提供されたコメントや評価が表示されます。

![chlimage_1-157](assets/chlimage_1-157.png)

レポートの条件を選択します。

* **[!UICONTROL サイト]**
イネーブルメントコミュニティサイトを選択
* **[!UICONTROL ユーザーまたはグループ]**
   * 「ユーザー」を選択して、1 人の学習者に関するレポートを生成します
   * 「グループ」を選択して学習者グループのレポートを生成するトンネルサービスは、パブリッシュ環境からメンバーとメンバーグループにアクセスします
* **[!UICONTROL 割り当て]**
選択した学習者に割り当てられたイネーブルメントリソースの中から選択します。

選択 **[!UICONTROL 生成]** レポートを作成するには：

![chlimage_1-158](assets/chlimage_1-158.png)

## 表示レポート {#views-report}

表示コンソールを使用すると、特定の期間、コミュニティ機能別にページビューにレポートを生成できます。

![chlimage_1-159](assets/chlimage_1-159.png)

レポートの条件を選択します。

* **[!UICONTROL サイト]**
コミュニティサイトを選択
* **[!UICONTROL コンテンツタイプ]**
[ すべてのコンテンツ ] を選択するか、サイトに存在する機能の 1 つを選択します
* 時間枠次のいずれかを選択します。
   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

選択 **[!UICONTROL 生成]** レポートを作成するには：

![chlimage_1-160](assets/chlimage_1-160.png)

## 投稿レポート {#posts-report}

投稿コンソールを使用すると、一定期間にコミュニティ機能に対する投稿数に関するレポートを生成できます。

![chlimage_1-161](assets/chlimage_1-161.png)

レポートの条件を選択します。

* **[!UICONTROL サイト]**
コミュニティサイトを選択
* **[!UICONTROL コンテンツタイプ]**
[ すべてのコンテンツ ] を選択するか、サイトに存在する機能の 1 つを選択します
* 時間枠次のいずれかを選択します。
   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

選択 **[!UICONTROL 生成]** レポートを作成するには：

![chlimage_1-162](assets/chlimage_1-162.png)

## トラブルシューティング {#troubleshooting}

### コミュニティサイトが一覧に表示されていません {#no-community-sites-listed}

コミュニティサイトが表示されない場合は、Adobe Analyticsがサイトに対して有効になっていることを確認します。 割り当てに関するレポートを選択する場合は、割り当て機能がコミュニティサイトの構造内にあることを確認します。
