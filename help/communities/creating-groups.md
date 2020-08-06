---
title: コミュニティグループ
seo-title: コミュニティグループ
description: コミュニティグループの作成
seo-description: コミュニティグループの作成
uuid: 05429b23-9083-498c-9eb3-d49b049d9446
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 868a3d5d-d505-4ce5-8776-5bbe68a30ccb
translation-type: tm+mt
source-git-commit: 8c66f2b0053882bd1c998d8e01dbb0573881bc87
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 46%

---


# コミュニティグループ {#community-groups}

コミュニティグループ機能は、サブコミュニティを発行ユーザーと発言者環境から許可されたユーザー（コミュニティのメンバーと発言者）がコミュニティサイト内で動的に作成する機能です。

This ability is present when the [groups function](functions.md#groups-function) is present in the [community site](sites-console.md) structure.

A [community group template](tools-groups.md) provides the design of the community group page when a community group is dynamically created.

グループ機能をコミュニティサイトの構造またはコミュニティサイトテンプレートに追加すると、1 つ以上のテンプレートがグループ機能用に選択されます。このリストのグループテンプレートは、コミュニティサイト内から動的に新しいグループを作成するメンバーまたは作成者に表示されます。

## 新しいグループの作成 {#creating-a-new-group}

The ability to create a new community group relies on the existance of a community site which includes the groups function, such as one created from the ` [Reference Site Template](sites.md)`.

The examples that follow use the community site created from the `Reference Site Template` as described in the [Getting Started with AEM Communities](getting-started.md) tutorial.

This is the page that loads on publish when the **[!UICONTROL Groups]** menu item is selected:

![chlimage_1-236](assets/chlimage_1-236.png)

「**[!UICONTROL 新しいグループ]**」アイコンを選択すると、編集ダイアログが開きます。

「**[!UICONTROL 設定]**」タブでは、グループの基本機能を指定します。

![chlimage_1-237](assets/chlimage_1-237.png)

* **[!UICONTROL グループ名]**&#x200B;コミュニティサイトに表示するグループのタイトルです。

* **[!UICONTROL 説明]**&#x200B;コミュニティサイトに表示するグループの説明です。

* **[!UICONTROL 招待]**&#x200B;グループに参加するように招待するメンバーのリストです。先行入力検索によって、招待する推奨コミュニティメンバーが表示されます。

* **[!UICONTROL グループ URL 名]** URL の一部になるグループページの名前です。

* **[!UICONTROL グループ]**&#x200B;選択を開く 
`Open Group` は、匿名サイト訪問者がコンテンツに表示を与える可能性があることを示し、選択が解除され `Member Only Group`ます。

* **[!UICONTROL メンバーのみのグループ]**&#x200B;の選択 
`Member Only Group` グループのメンバーのみがコンテンツを表示でき、選択を解除 `Open Group`します。

Under the **[!UICONTROL Template]** tab is the ability to select from the list of community group templates that were specified when the groups function was included in the community site&#39;s structure or in a community site template.

![chlimage_1-238](assets/chlimage_1-238.png)

「**[!UICONTROL 画像]**」タブでは、コミュニティサイトのグループページにグループ用に表示する画像をアップロードできます。初期設定のスタイルシートでは、画像のサイズが170 x 90ピクセルに設定されます。

![chlimage_1-239](assets/chlimage_1-239.png)

「**[!UICONTROL グループを作成]**」ボタンを選択すると、選択したテンプレートをベースとしてグループのページが作成され、ユーザーグループがメンバーシップ用に作成され、新しいサブコミュニティを表示するようにグループページが更新されます。

例えば、画像サムネイルがアップロードされた「Focus Group」というタイトルの新しいサブコミュニティを含むグループページは、次のように表示されます（引き続きコミュニティグループ管理者としてサインインしています）。

![chlimage_1-240](assets/chlimage_1-240.png)

Selecting the `Focus Group` link will open the Focus Group page in the browser, which has an initial appearance based on the chosen template, and includes a sub-menu underneath the main community site&#39;s menu:

![chlimage_1-241](assets/chlimage_1-241.png)

## コミュニティグループメンバーのリストコンポーネント {#community-group-member-list-component}

この `Community Group Member List` コンポーネントは、グループテンプレートの開発者が使用することを目的としています。

## 追加情報 {#additional-information}

More information may be found on the [Community Group Essentials](essentials-groups.md) page for developers.

コミュニティグループに関連するその他の情報は、[ユーザーとユーザーグループの管理](users.md)を参照してください。
