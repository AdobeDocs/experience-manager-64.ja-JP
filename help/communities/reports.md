---
title: レポートコンソール
seo-title: レポートコンソール
description: レポートのアクセス方法について説明します
seo-description: レポートのアクセス方法について説明します
uuid: 580f5eb8-24b2-4404-90d4-81f7108d1ee6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0042893e-3d2c-469e-8759-404be16e7436
translation-type: tm+mt
source-git-commit: 63001012f0d865c2548703ea387c780679128ee7

---


# レポートコンソール {#reports-console}

## 概要 {#overview}

AEM Communities には様々なレポートがあり、オーサー環境から複数の方法でアクセスできます。

通常、レポートには以下のものがあります。

* [割り当てレポート](#assignments-report) — 有効化コミ [ュニティ用に](overview.md#enablement-community)、SCORM標準を実装する場合の関連スコアを含む、学習者の割り当てに関する進捗の概要が表示されます。
* [表示回数レポート](#views-report) — コミュニティメンバーやコミュニティサイトの訪問者別のコンテンツのビュー数を示すグラフが表示されます。
* [投稿レポート](#posts-report) — コミュニティメンバーがコミュニティサイトに投稿した様々なタイプの投稿をグラフで表示します。

[Adobe Analyticsが有効な場合](sites-console.md#analytics)、レポートには各有効化リソースのビュー数、再生数、コメント数および評価数が時間の経過と共に含まれます

表形式のレポートは .csv 形式でエクスポートして別の処理に使用できます。

## レポートコンソール {#reporting-consoles}

### コミュニティサイトのレポート {#reports-for-community-sites}

* From global navigation: **[!UICONTROL Navigation > Communities > Reports]**
* 次から選択
   * **[!UICONTROL 割り当てレポート]**
      * 選択したコミュニティサイト、ユーザーまたはグループ、割り当てのレポートを生成します
   * **[!UICONTROL 投稿レポート]**
      * 選択したコミュニティサイト、コンテンツタイプ、期間のレポートを生成します
   * **[!UICONTROL 表示レポート]**
      * 選択したコミュニティサイト、コンテンツタイプ、期間のレポートを生成します
         ![chlimage_1-156](assets/chlimage_1-156.png)

### イネーブルメントリソースと学習パスのレポート {#reports-for-enablement-resources-and-learning-paths}

* From global navigation: **[!UICONTROL Navigation > Communities > Resources]**
* 既存の有効化コミュニティサイトを選択します
   * Select **[!UICONTROL Report]** icon to generate reports which cover all enablement resources
   * 有効化学習パスの選択
   * Select **[!UICONTROL Report]** icon to generate reports for
      * 付属の有効化リソース
      * 学習パスに割り当てられた学習者
* 以下のレポートが提供されます。
   * 表データ（CSV形式でダウンロード可能）
      * 学習者の識別
      * 彼らの地位
      * カタログを使用して割り当てるかアクセスするか
      * コメントの数
      * 星評価

詳しくは、リソースコンソールの[レポートセクション](resources.md#report)を参照してください。

## 割り当てレポート {#assignments-report}

割り当てコンソールでは、イネーブルメントコミュニティサイト、ユーザー、グループおよび割り当てによってレポートをフィルタリングできます。

このレポートには、進捗状況に関する情報と、コメントや評価がある場合はそれも表示されます。

![chlimage_1-157](assets/chlimage_1-157.png)

レポートのフィルタリング条件を選択します。

* **[!UICONTROL サイト有]**&#x200B;効化コミュニティサイトを選択
* **[!UICONTROL ユーザーまたはグループ]**
   * 「ユーザー」を選択して、1人の学習者のレポートを生成します
   * 「グループ」を選択して学習者グループのレポートを生成しますトンネルサービスは、発行環境からメンバーおよびメンバーグループにアクセスします
* **[!UICONTROL 割り当て]**&#x200B;選択した学習者に割り当てられているイネーブルメントリソースの中から選択します。

「**[!UICONTROL 生成]**」を選択してレポートを作成します。

![chlimage_1-158](assets/chlimage_1-158.png)

## Views Report {#views-report}

表示コンソールでは、指定した期間におけるコミュニティ機能別のページ表示回数のレポートを生成できます。

![chlimage_1-159](assets/chlimage_1-159.png)

レポートのフィルタリング条件を選択します。

* **[!UICONTROL サイト]**&#x200B;コミュニティサイトの選択
* **[!UICONTROL コンテンツタイプ]**「すべて」を選択するか、サイトに存在する機能の1つを選択できます。
* 時間枠次のいずれかを選択します。
   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

「**[!UICONTROL 生成]**」を選択してレポートを作成します。

![chlimage_1-160](assets/chlimage_1-160.png)

## Posts Report {#posts-report}

投稿コンソールでは、指定した期間におけるコミュニティ機能への投稿数のレポートを生成できます。

![chlimage_1-161](assets/chlimage_1-161.png)

レポートのフィルタリング条件を選択します。

* **[!UICONTROL サイト]**&#x200B;コミュニティサイトの選択
* **[!UICONTROL コンテンツタイプ]**「すべて」を選択するか、サイトに存在する機能の1つを選択できます。
* 時間枠次のいずれかを選択します。
   * 過去 7 日間
   * 過去 30 日間
   * 過去 90 日間
   * 昨年

「**[!UICONTROL 生成]**」を選択してレポートを作成します。

![chlimage_1-162](assets/chlimage_1-162.png)

## トラブルシューティング {#troubleshooting}

### コミュニティサイトが 1 つも表示されない {#no-community-sites-listed}

コミュニティサイトが 1 つも表示されない場合は、Adobe Analytics がサイトに対して有効になっているかを確認してください。割り当てに関するレポートを選択する場合は、割り当て機能がコミュニティサイトの構造内にあることを確認します。
