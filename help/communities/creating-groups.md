---
title: コミュニティグループ
seo-title: Community Groups
description: コミュニティグループの作成
seo-description: Creating community groups
uuid: 05429b23-9083-498c-9eb3-d49b049d9446
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 868a3d5d-d505-4ce5-8776-5bbe68a30ccb
exl-id: 4b663228-9cb6-45c0-99dd-8dd7fc2aa4a6
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 45%

---

# コミュニティグループ {#community-groups}

コミュニティグループ機能を使用すると、パブリッシュ環境とオーサー環境から、許可されたユーザー（コミュニティメンバーと作成者）がコミュニティサイト内でサブコミュニティを動的に作成できます。

この機能は、 [グループ機能](functions.md#groups-function) が [コミュニティサイト](sites-console.md) 構造。

A [コミュニティグループテンプレート](tools-groups.md) コミュニティグループを動的に作成する際のコミュニティグループページのデザインを提供します。

グループ機能をコミュニティサイトの構造またはコミュニティサイトテンプレートに追加すると、1 つ以上のテンプレートがグループ機能用に選択されます。このグループテンプレートのリストは、コミュニティサイト内から新しいグループを動的に作成するメンバーまたは作成者に表示されます。

## 新しいグループの作成 {#creating-a-new-group}

新しいコミュニティグループを作成する機能は、グループ機能を含むコミュニティサイトの存在に依存します。例えば、 ` [Reference Site Template](sites.md)`.

以下の例では、 `Reference Site Template` 例えば、 [AEM Communitiesの概要](getting-started.md) チュートリアル

これは、 **[!UICONTROL グループ]** メニュー項目が選択されている：

![chlimage_1-236](assets/chlimage_1-236.png)

「**[!UICONTROL 新しいグループ]**」アイコンを選択すると、編集ダイアログが開きます。

「**[!UICONTROL 設定]**」タブでは、グループの基本機能を指定します。

![chlimage_1-237](assets/chlimage_1-237.png)

* **[!UICONTROL グループ名]**&#x200B;コミュニティサイトに表示するグループのタイトルです。

* **[!UICONTROL 説明]**&#x200B;コミュニティサイトに表示するグループの説明です。

* **[!UICONTROL 招待]**&#x200B;グループに参加するように招待するメンバーのリストです。先行入力検索によって、招待する推奨コミュニティメンバーが表示されます。

* **[!UICONTROL グループ URL 名]** URL の一部になるグループページの名前です。

* **[!UICONTROL グループを開く]**
選択 
`Open Group` 匿名のサイト訪問者がコンテンツを閲覧できることを示し、選択を解除します。 `Member Only Group`.

* **[!UICONTROL メンバーのみのグループ]**
選択 
`Member Only Group` グループのメンバーのみがコンテンツを表示でき、選択を解除できることを示します `Open Group`.

以下 **[!UICONTROL テンプレート]** 「 」タブでは、コミュニティサイトの構造やコミュニティサイトテンプレートにグループ機能が含まれたときに指定されたコミュニティグループテンプレートのリストから選択できます。

![chlimage_1-238](assets/chlimage_1-238.png)

「**[!UICONTROL 画像]**」タブでは、コミュニティサイトのグループページにグループ用に表示する画像をアップロードできます。デフォルトのスタイルシートでは、画像のサイズが 170 x 90 ピクセルに設定されます。

![chlimage_1-239](assets/chlimage_1-239.png)

「**[!UICONTROL グループを作成]**」ボタンを選択すると、選択したテンプレートをベースとしてグループのページが作成され、ユーザーグループがメンバーシップ用に作成され、新しいサブコミュニティを表示するようにグループページが更新されます。

例えば、画像サムネイルがアップロードされた「Focus Group」というタイトルの新しいサブコミュニティを含むグループページは、次のように表示されます（引き続きコミュニティグループ管理者としてサインインしています）。

![chlimage_1-240](assets/chlimage_1-240.png)

の選択 `Focus Group` リンクは、ブラウザーでフォーカスグループページを開きます。このページは、選択したテンプレートに基づいて初期表示され、メインコミュニティサイトのメニューの下にサブメニューが含まれます。

![chlimage_1-241](assets/chlimage_1-241.png)

## コミュニティグループメンバーのリストコンポーネント {#community-group-member-list-component}

この `Community Group Member List` コンポーネントは、グループテンプレートの開発者が使用することを目的としています。

## 追加情報 {#additional-information}

詳しくは、 [コミュニティグループの基本事項](essentials-groups.md) 開発者向けのページ

コミュニティグループに関連するその他の情報は、[ユーザーとユーザーグループの管理](users.md)を参照してください。
