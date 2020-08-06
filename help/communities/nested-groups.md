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


# ネストされたグループの作成 {#authoring-nested-groups}

## オーサー環境でのグループの作成 {#creating-groups-on-author}

オーサー環境で、グローバルナビゲーションから、

* Select **[!UICONTROL Communities > Sites]**
* Select **[!UICONTROL engage folder]** to open it
* Select the card for the **[!UICONTROL Getting Started Tutorial]**  English site
   * カードの画像を選択
   * Do *not* select an icon

そうすると、[グループコンソール](groups.md)に移動します。

![chlimage_1-53](assets/chlimage_1-53.png)

グループ機能は、グループのインスタンスが作成されるフォルダーとして表示されます。グループフォルダーを選択して、開きます。公開時に作成されたグループは表示されます。

![chlimage_1-54](assets/chlimage_1-54.png)

## メインの Arts グループの作成 {#create-main-arts-group}

このグループを作成できるのは、engage のサイト構造にグループ機能が含まれているからです。The configuration of the function in the site&#39;s `Reference Template` defaults to allowing the selection of any enabled group template. Thus, the template chosen for this new group will be the `Reference Group`.

これらのコンソールは、コミュニティサイトコンソールによく似ています。

* Select **[!UICONTROL Create Group]**
*  `1 Community Group Template` の下）で、次の手順をおこないます。
   * コミュニティグループのタイトル：Arts
   * コミュニティグループの説明：A parent group for various arts groups.
   * コミュニティグループのルート：デフォルトのまま&#x200B;**
   * 追加の使用可能なコミュニティグループの言語：プルダウンメニューを使用して、使用可能なコミュニケーショングループの言語を選択します。このメニューには、親コミュニティサイトを作成できる言語がすべて表示されます。この中から言語を選択することで、1 回の手順で複数のロケールにグループを作成できます。指定した複数の言語で、それぞれのコミュニティサイトのグループコンソールに同じグループが作成されます。
   * コミュニティグループ名：arts
   * テンプレート： 下に降りて～を選ぶ `Reference Group`
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
      * use default `Optional Membership`
   * **サムネール**
      * `optional`
   *  `Next`
* 「**[!UICONTROL 作成]**」を選択します。

### Arts グループ内でのグループのネスト {#nesting-groups-within-arts-group}

The `groups` folder should now contain two groups (it may be necessary to refresh the page).

![createcommunitygroup](assets/createcommunitygroup.png)

#### グループの公開 {#publish-group}

`arts` グループ内でネストされるグループを作成する前に、`arts` カードにカーソルを合わせ、公開アイコンを選択してそのグループを公開します。

![chlimage_1-55](assets/chlimage_1-55.png)

グループが公開されたことが確認されるまで待機します。

![chlimage_1-56](assets/chlimage_1-56.png)

The `arts` group should also contain a `groups` folder, but one that is empty and in which new groups can be created. アートグループフォルダーに移動し、3つのネストされたグループを作成します。それぞれ異なるメンバーシップ設定になります。

1. Visiual
   * タイトル: `Visual Arts`
   * 名前：`visual`
   * テンプレート: `Reference Group`
   * Membership: select `Optional Membership`
A public group, open to all members
1. Auditory
   * タイトル: `Auditory Arts`
   * 名前：`auditory`
   * テンプレート: `Reference Group`
   * Membership: select `Required Membership`
An open group, available for members to join

1. History

   * タイトル: `Art History`
   * 名前：`history`
   * テンプレート: `Reference Group`
   * メンバーシップ： 「 `Restricted Membership`秘密グループ」を選択します。例えば、招待されたメンバーにのみ表示され、招待を行います。 
[デモユーザー](tutorials.md#demo-users) `emily.andrews@mailinator.com`

ページを更新して、ネストされた 3 つのグループ（サブコミュニティ）すべてを表示します。

必要に応じて、コミュニティサイトコンソールからネストされたグループに移動するには、次の手順を実行します。

* Select **[!UICONTROL engage folder]**
* Select **[!UICONTROL Getting Started Tutorial]** card
* Select **[!UICONTROL Groups folder]**
* Select **[!UICONTROL arts card]**
* Select **[!UICONTROL Groups folder]**

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

It is possible to experience the different groups when signed in, for example with the [demo users](tutorials.md#demo-users) used for

* Art/History グループメンバー：emily.andrews@mailinator.com／password
   * 制限付き（秘密）グループ、アート/履歴が表示されます
   * オプションの（パブリック）グループを表示できます。
   * 制限付き（開いている）グループに参加できます
* グループマネージャー：aaron.mcdonald@mailinator.com／password
   * オプションの（パブリック）グループを表示できます。
   * 制限された（オープン）グループに参加できます。
   * 制限付き（秘密）グループは表示されません

オーサー環境で Communities の[メンバーコンソールとグループコンソール](members.md)にアクセスすると、コミュニティグループに対応する様々なメンバーグループに他のユーザーを追加できます。
