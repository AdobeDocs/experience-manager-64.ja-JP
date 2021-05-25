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
exl-id: 4b663228-9cb6-45c0-99dd-8dd7fc2aa4a6
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 46%

---

# コミュニティグループ {#community-groups}

コミュニティグループ機能は、パブリッシュ環境とオーサー環境から許可されたユーザー（コミュニティメンバーと作成者）がコミュニティサイト内でサブコミュニティを動的に作成する機能です。

この機能は、[グループ関数](functions.md#groups-function)が[コミュニティサイト](sites-console.md)構造に存在する場合に使用できます。

[コミュニティグループテンプレート](tools-groups.md)は、コミュニティグループが動的に作成される際のコミュニティグループページのデザインを提供します。

グループ機能をコミュニティサイトの構造またはコミュニティサイトテンプレートに追加すると、1 つ以上のテンプレートがグループ機能用に選択されます。このグループテンプレートのリストは、コミュニティサイト内から新しいグループを動的に作成するメンバーまたは作成者に表示されます。

## 新しいグループの作成 {#creating-a-new-group}

新しいコミュニティグループを作成する機能は、` [Reference Site Template](sites.md)`から作成したグループ機能を含むコミュニティサイトの存在に依存します。

以降の例では、 [AEM Communities](getting-started.md)使用の手引きのチュートリアルで説明したように、 `Reference Site Template`から作成したコミュニティサイトを使用します。

これは、**[!UICONTROL Groups]**&#x200B;メニュー項目が選択された場合にパブリッシュ時に読み込まれるページです。

![chlimage_1-236](assets/chlimage_1-236.png)

「**[!UICONTROL 新しいグループ]**」アイコンを選択すると、編集ダイアログが開きます。

「**[!UICONTROL 設定]**」タブでは、グループの基本機能を指定します。

![chlimage_1-237](assets/chlimage_1-237.png)

* **[!UICONTROL グループ名]**&#x200B;コミュニティサイトに表示するグループのタイトルです。

* **[!UICONTROL 説明]**&#x200B;コミュニティサイトに表示するグループの説明です。

* **[!UICONTROL 招待]**&#x200B;グループに参加するように招待するメンバーのリストです。先行入力検索によって、招待する推奨コミュニティメンバーが表示されます。

* **[!UICONTROL グループ URL 名]** URL の一部になるグループページの名前です。

* **[!UICONTROL GroupSelectingを]**
開く 
`Open Group` は、匿名のサイト訪問者がコンテンツを表示できることを示し、選択を解除しま `Member Only Group`す。

* **[!UICONTROL メンバーのみのグル]**
ープ選択 
`Member Only Group` は、グループのメンバーのみがコンテンツを表示できることを示し、選択を解除しま `Open Group`す。

「**[!UICONTROL テンプレート]**」タブでは、コミュニティサイトの構造またはコミュニティサイトテンプレートにグループ機能を含めたときに指定したコミュニティグループテンプレートのリストから選択できます。

![chlimage_1-238](assets/chlimage_1-238.png)

「**[!UICONTROL 画像]**」タブでは、コミュニティサイトのグループページにグループ用に表示する画像をアップロードできます。デフォルトのスタイルシートでは、画像のサイズが170 x 90ピクセルに設定されます。

![chlimage_1-239](assets/chlimage_1-239.png)

「**[!UICONTROL グループを作成]**」ボタンを選択すると、選択したテンプレートをベースとしてグループのページが作成され、ユーザーグループがメンバーシップ用に作成され、新しいサブコミュニティを表示するようにグループページが更新されます。

例えば、画像サムネイルがアップロードされた「Focus Group」というタイトルの新しいサブコミュニティを含むグループページは、次のように表示されます（引き続きコミュニティグループ管理者としてサインインしています）。

![chlimage_1-240](assets/chlimage_1-240.png)

`Focus Group`リンクを選択すると、ブラウザーでフォーカスグループページが開きます。このページは、選択したテンプレートに基づいて初期表示され、メインコミュニティサイトのメニューの下にサブメニューが表示されます。

![chlimage_1-241](assets/chlimage_1-241.png)

## コミュニティグループメンバーのリストコンポーネント {#community-group-member-list-component}

`Community Group Member List`コンポーネントは、グループテンプレートの開発者が使用することを目的としています。

## 追加情報 {#additional-information}

詳しくは、開発者向けの[コミュニティグループの基本事項](essentials-groups.md)ページを参照してください。

コミュニティグループに関連するその他の情報は、[ユーザーとユーザーグループの管理](users.md)を参照してください。
