---
title: BrightEdge Content Optimizer との結合
seo-title: Integrating with BrightEdge Content Optimizer
description: AEMと BrightEdge Content Optimizer の統合について説明します。
seo-description: Learn about integrating AEM with BrightEdge Content Optimizer.
uuid: 7075dd3c-2fd6-4050-af1c-9b16ad4366ec
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: cf25c9a8-0555-4c67-8aa5-55984fd8d301
exl-id: 46d0513c-04b2-41ed-bb56-e0778fa5fd10
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 9%

---

# BrightEdge Content Optimizer との結合{#integrating-with-brightedge-content-optimizer}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

BrightEdge アカウントの資格情報を使用してAEMが接続できるように、BrightEdge クラウド設定を作成します。 複数のアカウントを使用する場合は、複数の設定を作成できます。

設定を作成する際に、タイトルを指定します。 ユーザーが設定を BrightEdge アカウントと関連付けられるように、タイトルはわかりやすいものにする必要があります。 ページ作成者または管理者が Web ページを BrightEdge アカウントに関連付けると、このタイトルがドロップダウンリストに表示されます。

1. レールで、ツール/操作/クラウド/Cloud Servicesをクリックします。
1. BrightEdge Content Optimizer セクションに表示されるリンクをクリックします。 BrightEdge 設定が作成されているかどうかによって、リンクテキストが決まります。

   * 今すぐ設定：このリンクは、設定が作成されていない場合に表示されます。
   * 設定を表示：このリンクは、1 つ以上の設定が作成されたときに表示されます。

   ![chlimage_1-4](assets/chlimage_1-4.png)

1. 「設定を表示」をクリックした場合は、「使用可能な設定」の横の「 + 」リンクをクリックします。
1. 設定のタイトルを入力します。 必要に応じて、リポジトリに設定を保存するために使用するノードの名前を入力します。 「作成」をクリックします。
1. [BrightEdge Content Optimizer 設定 ] ダイアログで、BrightEdge アカウントのユーザー名とパスワードを入力し、[OK] をクリックします。

## BrightEdge 設定の編集 {#editing-a-brightedge-configuration}

必要に応じて、BrightEdge 設定のユーザー名とパスワードを変更します。 変更は、設定を使用するすべてのページに影響します。

1. レールで、ツール/操作/クラウド/Cloud Servicesをクリックします。
1. 「BrightEdge Content Optimizer」セクションで、「設定を表示」をクリックします。

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 編集する設定の名前をクリックします。
1. [ 編集 ] をクリックし、プロパティ値を変更して、[OK] をクリックします。

## BrightEdge 設定へのページの関連付け {#associating-pages-with-a-brightedge-configuration}

ページを BrightEdge 設定に関連付けて、分析用にページデータを BrightEdge サービスに送信します。 ページを設定に関連付けると、子ページは関連付けを継承します。 通常は、サイトのホームページを関連付けて、すべてのページのデータが BrightEdge に送信されるようにします。

1. 従来の Web サイトコンソールを開きます。 ([http://localhost:4502/siteadmin#/content](http://localhost:4502/siteadmin#/content))
1. Web サイトツリーで、BrightEdge 設定に関連付けるページを含むフォルダーまたはページを選択します。
1. ページのリストで、設定するページを右クリックし、「プロパティ」をクリックします。
1. 「Cloud Services」タブで、「サービスを追加」ボタンをクリックし、Cloud Servicesダイアログで「BrightEdge Content Optimizer」を選択して、「OK」をクリックします。
1. BrightEdge Content Optimizer リストで、ページに関連付ける BrightEdge 設定を選択し、「OK」をクリックします。

   ![chlimage_1-6](assets/chlimage_1-6.png)

## BrightEdge 設定のアクティブ化 {#activating-a-brightedge-configuration}

BrightEdge 設定をアクティベートして、パブリッシュインスタンスにレプリケートし、公開済みのページで BrightEdge サービスとやり取りできるようにします。

1. レールで、「サイト」をクリックし、BrightEdge 設定に関連付けたページを参照して選択します。
1. 「公開」アイコンをクリックまたはタップし、「公開」をクリックまたはタップします。

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. 表示される設定のリストで、BrightEdge 設定が選択されていることを確認して、「公開」をクリックします。

   ![chlimage_1-8](assets/chlimage_1-8.png)
