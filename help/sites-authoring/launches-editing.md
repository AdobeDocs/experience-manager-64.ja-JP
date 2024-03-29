---
title: ローンチの編集
seo-title: Editing Launches
description: ページ（またはページのセット）のローンチを作成した後、ページのローンチコピーのコンテンツを編集できます。
seo-description: After creating a launch for your page (or set of pages) you can edit the content in the launch copy of the page(s).
uuid: 851bcbbe-1dff-457f-a3bc-468ace9b4ac4
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: site-features
discoiquuid: a28539fc-c1dd-43bf-a47b-5f158c5611a7
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 9f208b13-08eb-4305-b712-379e9b9b041e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 56%

---

# ローンチの編集 {#editing-launches}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## ローンチページの編集 {#editing-launch-pages}

ページ（またはページのセット）にローンチが作成されている場合、ページのローンチコピーのコンテンツを編集できます。

1. [「参照」のローンチ（Sites コンソール）](/help/sites-authoring/launches.md#launches-in-references-sites-console)にアクセスして使用可能なアクションを表示します。
1. 選択 **ページに移動します。** をクリックして、編集するページを開きます。

### ライブコピーへのローンチページサブジェクトの編集 {#editing-launch-pages-subject-to-a-live-copy}

ローンチが [ライブコピー](/help/sites-administering/msm.md) 次の手順を実行します。

* コンポーネント（コンテンツやプロパティ）を編集する際には、ロック記号（小さな鍵アイコン）が表示されます。
* 参照 **ライブコピー** タブ **ページプロパティ**

ライブコピーは、コンテンツをソースブランチ&#x200B;*から*&#x200B;ローンチブランチ&#x200B;*に*&#x200B;同期するために使用します（ローンチを、ソースに加えられた変更を含む最新の状態に保ちます）。

標準のライブコピーを編集する場合と同じ方法で変更を加えることができます。例：

* 閉じた鍵アイコンをクリックすると、この同期が解除され、ローンチのコンテンツを新しく更新できます。 ロック解除（南京錠を開く）すると、変更は、ソースブランチ内の同じ場所で行われた変更で上書きされません。
* 特定のページの継承を&#x200B;**一時停止**（および&#x200B;**再開**）します。

詳しくは、「[ライブコピーのコンテンツの変更](/help/sites-administering/msm-livecopy.md#changing-live-copy-content)」を参照してください。

## ローンチページとそのソースページの比較 {#comparing-a-launch-page-to-its-source-page}

行った変更を追跡するために、ローンチを&#x200B;**参照**&#x200B;で表示して、ローンチページをそのソースページと比較することができます。

1. 内 **サイト** コンソール [ローンチのソースページに移動して選択します。](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. **[参照](/help/sites-authoring/basic-handling.md#references)**&#x200B;パネルを開いて、「**ローンチ**」を選択します。
1. 特定のローンチを選択してから、次のように&#x200B;**ソースと比較します**。

   ![chlimage_1-96](assets/chlimage_1-96.png)

1. 2 つのページ（ローンチとソース）が並べて開きます。

   この機能の使用方法について詳しくは、[ページの差分](/help/sites-authoring/page-diff.md)を参照してください。

## 使用するソースページの変更 {#changing-the-source-pages-used}

ローンチのソースページの範囲に対して、任意のタイミングでページを追加または削除できます。

1. 次のいずれかの方法を使用して、ローンチにアクセスして選択します。

   * [ローンチコンソール](/help/sites-authoring/launches.md#the-launches-console)：

      * 「**編集**」を選択します。
   * [「参照」（Sites コンソール）](/help/sites-authoring/launches.md#launches-in-references-sites-console)：使用可能なアクションを表示します。

      * 「**ローンチを編集**」を選択します。

   ソースページが表示されます。

1. 必要な変更を加え、「**保存**」で確定します。

   >[!NOTE]
   >
   >ローンチにページを追加するには、共通言語ルートの下に配置する必要があります。例：単一のサイト内。

## Launch 設定の編集 {#editing-a-launch-configuration}

ローンチのプロパティは、任意のタイミングで編集できます。

1. 次のいずれかの方法を使用して、ローンチにアクセスして選択します。

   * [ローンチコンソール](/help/sites-authoring/launches.md#the-launches-console)：

      * 選択 **プロパティ**.
   * [「参照」（Sites コンソール）](/help/sites-authoring/launches.md#launches-in-references-sites-console)：使用可能なアクションを表示します。

      * 「**プロパティを編集**」を選択します。

   詳細が表示されます。

1. 必要な変更を加え、「**保存**」で確定します。

   「**ローンチ日**」フィールドと「**実稼働準備完了**」フィールドの目的とインタラクションについて詳しくは、[ローンチ - イベントの順序](/help/sites-authoring/launches.md#launches-the-order-of-events)を参照してください。

## ページのローンチステータスの確認 {#discovering-the-launch-status-of-a-page}

「参照」タブから特定のローンチを選択すると、ステータスが表示されます（[「参照」のローンチ（サイトコンソール）](/help/sites-authoring/launches.md#launches-in-references-sites-console)を参照）。

![chlimage_1-97](assets/chlimage_1-97.png)
