---
title: 編集者
seo-title: 編集者
description: クラシック UI エディターへの切り替え方法について説明します。
seo-description: クラシック UI エディターへの切り替え方法について説明します。
uuid: 78ba4db0-affa-4081-bf29-a3306720c968
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5fca5401-502d-483b-bfc1-ef53e2c041b7
exl-id: 04a9c595-9a73-4a8a-99ae-c2292882338f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 91%

---

# 編集者{#editor}

エディターからクラシック UI に切り替える機能は、デフォルトで無効になっています。

![chlimage_1-9](assets/chlimage_1-9.png)

**ページ情報**&#x200B;メニューのオプション「**クラシック UI で開く**」を再度有効にするには、次の手順に従います。

1. CRXDE Lite を使用して、次のノードを見つけます。

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   例：

   `http://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](http://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

1. **Overlay Node**&#x200B;オプションを使用してオーバーレイを作成します。例：

   * **パス**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **オーバーレイの場所**: `/apps/`
   * **ノードタイプを一致させる**：アクティブ（チェックボックスをオン）

1. オーバーレイノードに次の複数値テキストプロパティを追加します。

   `sling:hideProperties = ["granite:hidden"]`

1. ページの編集時に、「**クラシック UI で開く**」オプションが&#x200B;**ページ情報**&#x200B;メニューで再度使用可能になります。

   ![chlimage_1-10](assets/chlimage_1-10.png)
