---
title: 管理コンソール
seo-title: 管理コンソール
description: AEM で使用可能な管理コンソールの使用方法について学習します。
seo-description: AEM で使用可能な管理コンソールの使用方法について学習します。
uuid: 701dc57c-f7b4-421e-a847-577ae2585e80
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: 98ba3093-1edb-4891-abbe-47cf6e4f1feb
translation-type: tm+mt
source-git-commit: 1ebe1e871767605dd4295429c3d0b4de4dd66939
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 72%

---


# 管理コンソール{#admin-consoles}

管理コンソールからクラシック UI に切り替える機能は、デフォルトで無効になっています。以前は、コンソールアイコンの上にマウスを移動すると、クラシック UI にアクセスするためのポップアップアイコンが表示されていましたが、このアイコンは表示されなくなりました。

![screen_shot_2018-03-23at11956](assets/screen_shot_2018-03-23at111956.png)

Every console that has a Classic UI version in `/libs/cq/core/content/nav` can be re-enabled individually so that the **Classic UI** option once again pops up over the console icon when it is moused over.

以下の例では、サイトコンソールのクラシック UI を再有効化しています。

1. CRXDE Liteを使用して、クラシックUIを再有効化する管理コンソールに対応するノードを探します。 目的のノードは次の場所にあります。

   `/libs/cq/core/content/nav`

   例：

   [ `http://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](http://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. クラシック UI を再有効化するコンソールのノードを選択します。この例では、サイトコンソールのクラシック UI を再有効化します。

   `/libs/cq/core/content/nav/sites`

1. Create an overlay using the **Overlay Node** option; for example:

   * **パス**: `/apps/cq/core/content/nav/sites`
   * **オーバーレイの場所**: `/apps/`
   * **ノードタイプを一致させる**：アクティブ（チェックボックスをオン）

1. オーバーレイノードに次のブールプロパティを追加します。

   `enableDesktopOnly = {Boolean}true`

1. 「**クラシック UI**」オプションが、管理コンソールに再びポップアップされるようになります。

   ![screen_shot_2018-03-23at11924](assets/screen_shot_2018-03-23at111924.png)

クラシック UI バージョンへのアクセスを再有効化する各コンソールに対して、これらの手順を繰り返します。
