---
title: ネストされたグループの作成
seo-title: ネストされたグループの作成
description: ネストされたグループの作成
seo-description: ネストされたグループの作成
uuid: b478454a-24c6-4e1c-a6e0-afeb1bc4992c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 955a1876-4882-4926-82e9-846bc8bb332c
translation-type: tm+mt
source-git-commit: 2d1e39120d79de029927011d48f7397b53ad91bc
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 53%

---


# ネストされたグループの作成  {#authoring-nested-groups}

## オーサー環境でのグループの作成 {#creating-groups-on-author}

オーサー環境で、グローバルナビゲーションから、

* **[!UICONTROL コミュニティ/サイト]**&#x200B;を選択します
* **[!UICONTROL エンゲージメントフォルダー]**&#x200B;を選択して開きます
* **[!UICONTROL はじめに/チュートリアル]**&#x200B;英語サイトのカードを選択します
   * カードの画像を選択
   * アイコンを&#x200B;*選択しない*

そうすると、[グループコンソール](groups.md)に移動します。

![chlimage_1-53](assets/chlimage_1-53.png)

グループ機能は、グループのインスタンスが作成されるフォルダーとして表示されます。グループフォルダーを選択して、開きます。公開時に作成されたグループは表示されます。

![chlimage_1-54](assets/chlimage_1-54.png)

## メインの Arts グループの作成 {#create-main-arts-group}

このグループを作成できるのは、engage のサイト構造にグループ機能が含まれているからです。サイトの`Reference Template`内の関数の設定は、デフォルトで有効なグループテンプレートの選択を許可します。 したがって、この新しいグループに対して選択されるテンプレートは`Reference Group`になります。

これらのコンソールは、コミュニティサイトコンソールによく似ています。

* 「**[!UICONTROL グループを作成]**」を選択します
*  `1 Community Group Template` の下）で、次の手順をおこないます。
   * コミュニティグループのタイトル：Arts
   * コミュニティグループの説明：A parent group for various arts groups.
   * コミュニティグループのルート：デフォルトのまま&#x200B;**
   * 追加の使用可能なコミュニティグループの言語：プルダウンメニューを使用して、使用可能なコミュニケーショングループの言語を選択します。このメニューには、親コミュニティサイトを作成できる言語がすべて表示されます。この中から言語を選択することで、1 回の手順で複数のロケールにグループを作成できます。指定した複数の言語で、それぞれのコミュニティサイトのグループコンソールに同じグループが作成されます。
   * コミュニティグループ名：arts
   * テンプレート：プルダウンして`Reference Group`を選択します。
   *  `Next`

      ![parenttonestedgroup](assets/parenttonestedgroup.png)

引き続き、他のパネルで以下の値を設定します。

* **2 デザイン**
   * デザインを変更したり、親サイトのデザインをデフォルトにすることができます
   * 「**[!UICONTROL 次へ]**」を選択します。
* **3 設定**
   * **モデレート**
      * 空のままにする（親サイトから継承）
   * **メンバーシップ**
      * デフォルト`Optional Membership`を使用
   * **サムネール**
      * `optional`
   *  `Next`
* 「**[!UICONTROL 作成]**」を選択します。

### Arts グループ内でのグループのネスト {#nesting-groups-within-arts-group}

これで、`groups`フォルダーに2つのグループが含まれるはずです（ページの更新が必要な場合があります）。

![createcommunitygroup](assets/createcommunitygroup.png)

#### グループの公開 {#publish-group}

`arts` グループ内でネストされるグループを作成する前に、`arts` カードにカーソルを合わせ、公開アイコンを選択してそのグループを公開します。

![chlimage_1-55](assets/chlimage_1-55.png)

グループが公開されたことが確認されるまで待機します。

![chlimage_1-56](assets/chlimage_1-56.png)

`arts`グループには`groups`フォルダーも含める必要がありますが、空で新しいグループを作成できるフォルダーも含まれます。 アートグループフォルダーに移動し、3つのネストされたグループを作成します。それぞれ異なるメンバーシップ設定になります。

1. Visiual
   * タイトル: `Visual Arts`
   * 名前：`visual`
   * テンプレート: `Reference Group`
   * メンバーシップ：`Optional Membership`を選択
すべての会員が参加できるパブリック・グループ
1. Auditory
   * タイトル: `Auditory Arts`
   * 名前：`auditory`
   * テンプレート: `Reference Group`
   * メンバーシップ：`Required Membership`を選択
メンバーが参加できる、開かれたグループ

1. History

   * タイトル: `Art History`
   * 名前：`history`
   * テンプレート: `Reference Group`
   * メンバーシップ：`Restricted Membership`を選択
例えば、招待メンバーにのみ表示されるシークレットグループ、invite 
[デモユーザー](tutorials.md#demo-users) `emily.andrews@mailinator.com`

ページを更新して、ネストされた 3 つのグループ（サブコミュニティ）すべてを表示します。

必要に応じて、コミュニティサイトコンソールからネストされたグループに移動するには、次の手順を実行します。

* **[!UICONTROL エンゲージメントフォルダー]**&#x200B;を選択
* **[!UICONTROL はじめに]**&#x200B;カードを選択
* **[!UICONTROL Groups folder]**&#x200B;を選択
* **[!UICONTROL アートカード]**&#x200B;を選択
* **[!UICONTROL Groups folder]**&#x200B;を選択

![chlimage_1-57](assets/chlimage_1-57.png)

## グループの公開 {#publishing-groups}

![chlimage_1-58](assets/chlimage_1-58.png)

メインのコミュニティサイトを公開したら、以下のことが必要になります。

* 各グループを個別に公開
   * グループが公開されたことの確認を待っています
* Publish parent group before publish any groups nested within
   * すべてのグループは、トップダウン方式で公開する必要があります。

![chlimage_1-59](assets/chlimage_1-59.png)

## パブリッシュ環境でのエクスペリエンス {#experience-on-publish}

サインイン時に、様々なグループを体験できます。例えば、[](tutorials.md#demo-users)

* Art/History グループメンバー：emily.andrews@mailinator.com／password
   * 制限付き（秘密）グループ、アート/履歴が表示されます
   * オプションの（パブリック）グループを表示できます。
   * 制限付き（開いている）グループに参加できます
* グループマネージャー：aaron.mcdonald@mailinator.com／password
   * オプションの（パブリック）グループを表示できます。
   * 制限された（オープン）グループに参加できます。
   * 制限付き（秘密）グループは表示されません

オーサー環境で Communities の[メンバーコンソールとグループコンソール](members.md)にアクセスすると、コミュニティグループに対応する様々なメンバーグループに他のユーザーを追加できます。
