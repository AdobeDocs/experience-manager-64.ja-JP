---
title: ノードの作成
seo-title: Create Nodes
description: 'コメントシステムのオーバーレイ '
seo-description: Overlay the comments system
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
exl-id: fc044a4e-0037-405f-8c26-b388c6a98733
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 42%

---

# ノードの作成 {#create-nodes}

最小限の数の必要なファイルを /libs から /apps にコピーし、/apps 内で変更することにより、コメントシステムをカスタムバージョンでオーバーレイします。

>[!CAUTION]
>
>再インストールやアップグレードをおこなうと、/libs フォルダーは削除されたり、置換されたりすることがありますが、/apps フォルダーの内容が変更されることはないので、/libs フォルダーの内容を編集することはありません。

使用 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) オーサーインスタンスで、まず、/libs フォルダー内のオーバーレイされたコンポーネントへのパスと同じパスを/apps フォルダーに作成します。

複製するパスは次のとおりです。

* `/libs/social/commons/components/hbs/comments/comment`

パス内の一部のノードはフォルダーで、一部はコンポーネントです。

1. 参照先 [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 作成 `/apps/social` （まだ存在しない場合）
   * 選択 `/apps` ノード
   * **[!UICONTROL 作成／フォルダー...]** を選択します。
      * 名前を入力: `social`
1. 選択 `social` ノード
   * **[!UICONTROL 作成／フォルダー...]** を選択します。
      * 名前を入力: `commons`
1. 選択 `commons` ノード
   * **[!UICONTROL 作成／フォルダー...]** を選択します。
      * 名前を入力: `components`
1. 選択 `components` ノード
   * **[!UICONTROL 作成／フォルダー...]** を選択します。
      * 名前を入力: `hbs`
1. 選択 `hbs` ノード
   * **[!UICONTROL 作成／コンポーネントを作成...]** を選択します。
      * ラベルを入力： `comments`
      * タイトルを入力： `Comments`
      * 説明を入力： `List of comments without showing avatars`
      * スーパータイプ：`social/commons/components/comments`
      * グループを入力： `Communities`
      * クリック **[!UICONTROL 次へ]** 次まで **[!UICONTROL OK]**
1. 選択 `comments` ノード

   * **[!UICONTROL 作成／コンポーネントを作成...]** を選択します。

      * ラベルを入力： `comment`
      * タイトルを入力： `Comment`
      * 説明を入力： `A comment instance without avatars`
      * スーパータイプ：`social/commons/components/comments/comment`
      * グループを入力： `.hidden`
      * クリック **[!UICONTROL 次へ]** 次まで **[!UICONTROL OK]**
   * 「**[!UICONTROL すべて保存]**」を選択します。
1. デフォルトの `comments.jsp`
   * ノードを選択 `/apps/social/commons/components/hbs/comments/comments.jsp`
   * 選択 **[!UICONTROL 削除]**
1. デフォルトの comment.jsp を削除します。
   *  ノードを選択します`/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 選択 **[!UICONTROL 削除]**
   * 「**[!UICONTROL すべて保存]**」を選択します。

>[!NOTE]
>
>継承チェーンを保持するには、 `Super Type` （プロパティ） `sling:resourceSuperType`) が `Super Type` （この場合は）オーバーレイされるコンポーネント
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`
>


オーバーレイ自体 `Type`（プロパティ） `sling:resourceType`) は、/apps に見つからないコンテンツが/libs 内で検索されるように、相対的な自己参照である必要があります。
* 名前：`sling:resourceType`
* タイプ：`String`
* 値：`social/commons/components/hbs/comments`

1. 緑を選択 `[+] Add`
   * 名前：`sling:resourceType`
   * タイプ：`String`
   * 値：`social/commons/components/hbs/comments/comment`
1. 緑を選択 `[+] Add`
   * 「**[!UICONTROL すべて保存]**」を選択します。

![chlimage_1-4](assets/chlimage_1-4.png)
