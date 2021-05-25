---
title: ノードの作成
seo-title: ノードの作成
description: 'コメントシステムのオーバーレイ '
seo-description: 'コメントシステムのオーバーレイ '
uuid: 802ae28b-9989-4c2c-b466-ab76a724efd3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cd4f53ee-537b-4f10-a64f-474ba2c44576
exl-id: fc044a4e-0037-405f-8c26-b388c6a98733
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 41%

---

# ノードの作成 {#create-nodes}

最小限の数の必要なファイルを /libs から /apps にコピーし、/apps 内で変更することにより、コメントシステムをカスタムバージョンでオーバーレイします。

>[!CAUTION]
>
>再インストールやアップグレードをおこなうと、/libs フォルダーは削除されたり、置換されたりすることがありますが、/apps フォルダーの内容が変更されることはないので、/libs フォルダーの内容を編集することはありません。

オーサーインスタンスで[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)を使用して、まず/libsフォルダー内のオーバーレイされたコンポーネントのパスと同じパスを/appsフォルダーに作成します。

複製するパスは次のとおりです。

* `/libs/social/commons/components/hbs/comments/comment`

パス内の一部のノードはフォルダーで、一部はコンポーネントです。

1. [http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)を参照します。
1. `/apps/social`を作成します（まだ存在しない場合）
   * `/apps`ノードを選択
   * **[!UICONTROL 作成／フォルダー...]** を選択します。
      * 名前を入力: `social`
1. `social`ノードを選択
   * **[!UICONTROL 作成／フォルダー...]** を選択します。
      * 名前を入力: `commons`
1. `commons`ノードを選択
   * **[!UICONTROL 作成／フォルダー...]** を選択します。
      * 名前を入力: `components`
1. `components`ノードを選択
   * **[!UICONTROL 作成／フォルダー...]** を選択します。
      * 名前を入力: `hbs`
1. `hbs`ノードを選択
   * **[!UICONTROL 作成／コンポーネントを作成...]** を選択します。
      * ラベルを入力：`comments`
      * タイトルを入力：`Comments`
      * 説明を入力：`List of comments without showing avatars`
      * スーパータイプ：`social/commons/components/comments`
      * グループを入力：`Communities`
      * 「**[!UICONTROL 次へ]**」をクリックして、「**[!UICONTROL OK]**」をクリックします。
1. `comments`ノードを選択

   * **[!UICONTROL 作成／コンポーネントを作成...]** を選択します。

      * ラベルを入力：`comment`
      * タイトルを入力：`Comment`
      * 説明を入力：`A comment instance without avatars`
      * スーパータイプ：`social/commons/components/comments/comment`
      * グループを入力：`.hidden`
      * 「**[!UICONTROL 次へ]**」をクリックして、「**[!UICONTROL OK]**」をクリックします。
   * 「**[!UICONTROL すべて保存]**」を選択します。
1. デフォルトの`comments.jsp`を削除します。
   * ノード`/apps/social/commons/components/hbs/comments/comments.jsp`を選択します。
   * **[!UICONTROL 削除]**&#x200B;を選択します。
1. デフォルトのcomment.jspを削除します。
   * ノード`/apps/social/commons/components/hbs/comments/comment/comment.jsp`を選択します。
   * **[!UICONTROL 削除]**&#x200B;を選択します。
   * 「**[!UICONTROL すべて保存]**」を選択します。

>[!NOTE]
>
>継承チェーンを保持するために、オーバーレイコンポーネントの`Super Type`（プロパティ`sling:resourceSuperType`）が、オーバーレイされるコンポーネントの`Super Type`と同じ値に設定されます(この場合は
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

>



オーバーレイ自体の`Type`（プロパティ`sling:resourceType`）は、/appsで見つからないコンテンツが/libs内で検索されるように、相対的な自己参照である必要があります。
* 名前：`sling:resourceType`
* 型：`String`
* 値：`social/commons/components/hbs/comments`

1. 緑色の`[+] Add`を選択します。
   * 名前：`sling:resourceType`
   * 型：`String`
   * 値：`social/commons/components/hbs/comments/comment`
1. 緑色の`[+] Add`を選択します。
   * 「**[!UICONTROL すべて保存]**」を選択します。

![chlimage_1-4](assets/chlimage_1-4.png)
