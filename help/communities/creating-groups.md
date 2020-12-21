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

この機能は、[groups関数](functions.md#groups-function)が[コミュニティサイト](sites-console.md)構造に存在する場合に存在します。

[コミュニティグループテンプレート](tools-groups.md)は、コミュニティグループが動的に作成された場合に、コミュニティグループページのデザインを提供します。

グループ機能をコミュニティサイトの構造またはコミュニティサイトテンプレートに追加すると、1 つ以上のテンプレートがグループ機能用に選択されます。このリストのグループテンプレートは、コミュニティサイト内から動的に新しいグループを作成するメンバーまたは作成者に表示されます。

## 新しいグループの作成 {#creating-a-new-group}

新しいコミュニティグループを作成する機能は、` [Reference Site Template](sites.md)`から作成されたグループ機能など、コミュニティサイトの存在に依存します。

次の例では、[AEM Communitiesの使い始めに/](getting-started.md)チュートリアルで説明されているように、`Reference Site Template`から作成したコミュニティサイトを使用します。

これは、**[!UICONTROL グループ]**&#x200B;メニュー項目が選択されている場合に、発行時に読み込まれるページです。

![chlimage_1-236](assets/chlimage_1-236.png)

「**[!UICONTROL 新しいグループ]**」アイコンを選択すると、編集ダイアログが開きます。

「**[!UICONTROL 設定]**」タブでは、グループの基本機能を指定します。

![chlimage_1-237](assets/chlimage_1-237.png)

* **[!UICONTROL グループ名]**&#x200B;コミュニティサイトに表示するグループのタイトルです。

* **[!UICONTROL 説明]**&#x200B;コミュニティサイトに表示するグループの説明です。

* **[!UICONTROL 招待]**&#x200B;グループに参加するように招待するメンバーのリストです。先行入力検索によって、招待する推奨コミュニティメンバーが表示されます。

* **[!UICONTROL グループ URL 名]** URL の一部になるグループページの名前です。

* **[!UICONTROL GroupSelectingを開]**
く 
`Open Group` は、匿名サイト訪問者がコンテンツに表示を与える可能性があることを示し、選択が解除され `Member Only Group`ます。

* **[!UICONTROL メンバーのみの]**
グループの選択 
`Member Only Group` グループのメンバーのみがコンテンツを表示でき、選択を解除 `Open Group`します。

[**[!UICONTROL テンプレート]**]タブには、コミュニティサイトの構造やコミュニティサイトのテンプレートにグループ機能が含まれていたときに指定したコミュニティグループテンプレートのリストから選択できる機能があります。

![chlimage_1-238](assets/chlimage_1-238.png)

「**[!UICONTROL 画像]**」タブでは、コミュニティサイトのグループページにグループ用に表示する画像をアップロードできます。初期設定のスタイルシートでは、画像のサイズが170 x 90ピクセルに設定されます。

![chlimage_1-239](assets/chlimage_1-239.png)

「**[!UICONTROL グループを作成]**」ボタンを選択すると、選択したテンプレートをベースとしてグループのページが作成され、ユーザーグループがメンバーシップ用に作成され、新しいサブコミュニティを表示するようにグループページが更新されます。

例えば、画像サムネイルがアップロードされた「Focus Group」というタイトルの新しいサブコミュニティを含むグループページは、次のように表示されます（引き続きコミュニティグループ管理者としてサインインしています）。

![chlimage_1-240](assets/chlimage_1-240.png)

`Focus Group`リンクを選択すると、ブラウザーにフォーカスグループページが開きます。このページは、選択したテンプレートに基づいて初期表示され、メインコミュニティサイトのメニューの下にサブメニューが含まれます。

![chlimage_1-241](assets/chlimage_1-241.png)

## コミュニティグループメンバーのリストコンポーネント {#community-group-member-list-component}

`Community Group Member List`コンポーネントは、グループテンプレートの開発者が使用することを目的としています。

## 追加情報 {#additional-information}

詳しくは、[Community Group Essentials](essentials-groups.md)ページを参照してください。

コミュニティグループに関連するその他の情報は、[ユーザーとユーザーグループの管理](users.md)を参照してください。
