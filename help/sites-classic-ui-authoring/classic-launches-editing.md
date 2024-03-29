---
title: ローンチの編集
seo-title: Editing Launches
description: ページ（またはページのセット）にローンチが作成されている場合、ページのローンチコピーのコンテンツを編集できます。
seo-description: When a launch has been created for a page (or set of pages) you can edit the content in the launch copy of the page(s).
uuid: 3a310eeb-553d-4d2b-98b5-c5bc523b2aca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 666b967a-e94b-4f94-a676-00adf150580f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 98bccd13-431a-4cba-bb93-75cdcc98830a
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 39%

---

# ローンチの編集 {#editing-launches}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## ローンチページの編集 {#editing-launch-pages}

ページ（またはページのセット）にローンチが作成されている場合、ページのローンチコピーのコンテンツを編集できます。

1. 編集するページを開きます。
1. サイドキックで、 **バージョン管理** タブをクリックし、 **起動回数** グループ化します。 現在編集中のローンチのタイトルは太字フォントを使用しています。

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. 作業対象のローンチを選択し、「 **切り替え**.
1. 編集を開始します。

   >[!NOTE]
   >
   >サイドキックの「**ページ**」タブを使用して、**子ページを作成**&#x200B;するなどのアクションを実行できます。

## Launch 設定の編集 {#editing-a-launch-configuration}

ローンチを作成した後、ローンチ名とローンチ日を変更できます。 ローンチに関連付ける画像を指定することもできます。

1. ローンチの管理ページ（[http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html)）を開きます。

1. 必要なローンチを選択し、 **編集** ダイアログを開くには：

   * 内 **一般** 「 」タブでは、次の項目を編集できます。

      * **タイトル**
      * **開始日**：ローンチ日と同じ
      * **実稼動準備完了**

      詳しくは、 [ローンチ — イベントの順序](/help/sites-authoring/launches.md#launches-the-order-of-events) を参照してください。

   * 内 **画像** 「 」タブでは、画像ファイルをアップロードできます。


1. 「**保存**」をクリックします。

## ページのローンチステータスの確認 {#discovering-the-launch-status-of-a-page}

ページのローンチを編集しているときに、ローンチに関する情報が **バージョン管理** サイドキックのタブ：

* ローンチの名前。
* 前回の変更からの経過時間。
* 最後の変更を実行したユーザー。
* 「**実稼動準備完了**」フラグのステータス（オレンジ = 未設定、緑 = 設定済み）。

![chlimage_1-186](assets/chlimage_1-186.png)
