---
title: 管理コンソール
seo-title: Admin Consoles
description: AEMで使用可能なAdmin Consoleの使用方法を説明します。
seo-description: Lear how to use the Admin Consoles available in AEM.
uuid: 701dc57c-f7b4-421e-a847-577ae2585e80
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: 98ba3093-1edb-4891-abbe-47cf6e4f1feb
exl-id: f3c03562-aaeb-4d43-aee1-d92d661ee329
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 36%

---

# 管理コンソール{#admin-consoles}

デフォルトでは、管理コンソールからクラシック UI に切り替える機能は無効になっています。 したがって、特定のコンソールアイコンにマウスを合わせると表示されるポップアップアイコン（クラシック UI にアクセスできる）は表示されなくなりました。

![screen_shot_2018-03-23at111956](assets/screen_shot_2018-03-23at111956.png)

各コンソールのクラシック UI バージョンは `/libs/cq/core/content/nav` にあり、個別に再有効化できます。それぞれのクラシック UI を有効にすれば、コンソールアイコンの上にマウスを移動したときに、「**クラシック UI**」オプションが再度ポップアップするようになります。

以下の例では、サイトコンソールのクラシック UI を再有効化しています。

1. CRXDE Liteを使用して、クラシック UI を再度有効にする管理コンソールに対応するノードを探します。 目的のノードは次の場所にあります。

   `/libs/cq/core/content/nav`

   例：

   [ `http://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav`](http://localhost:4502/crx/de/index.jsp#/libs/cq/core/content/nav)

1. クラシック UI を再度有効にする、コンソールに対応するノードを選択します。 この例では、サイトコンソールのクラシック UI を再度有効にします。

   `/libs/cq/core/content/nav/sites`

1. 「**オーバーレイノード**」オプションを使用してオーバーレイを作成します。次に例を示します。

   * **パス**: `/apps/cq/core/content/nav/sites`
   * **オーバーレイの場所**: `/apps/`
   * **ノードタイプを一致させる**:アクティブ（チェックボックスを選択）

1. オーバーレイノードに次のブールプロパティを追加します。

   `enableDesktopOnly = {Boolean}true`

1. この **クラシック UI** オプションは、admin console で再びポップオーバーオプションとして使用できます。

   ![screen_shot_2018-03-23at111924](assets/screen_shot_2018-03-23at111924.png)

クラシック UI バージョンへのアクセスを再度有効にする各コンソールに対して、これらの手順を繰り返します。
