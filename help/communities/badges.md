---
title: バッジコンソール
seo-title: バッジコンソール
description: Communities のバッジコンソールを使用すると、バッジを獲得（授与された）したとき、またはコミュニティで特定の役割についた（割り当てられた）ときにメンバーに表示できるカスタムバッジを追加できます
seo-description: Communities のバッジコンソールを使用すると、バッジを獲得（授与された）したとき、またはコミュニティで特定の役割についた（割り当てられた）ときにメンバーに表示できるカスタムバッジを追加できます
uuid: 9eeba240-f0d4-4937-baba-8bac0e0b2a36
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4194278f-5127-4105-b181-60961c7a1def
translation-type: tm+mt
source-git-commit: 59d40b5bddc42a4ac057ef600243f396aefc926b
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 65%

---


# バッジコンソール {#badges-console}

## バッジについて {#about-badges}

Communities のバッジコンソールでは、バッジを獲得（授与された）したとき、またはコミュニティで特定の役割についた（割り当てられた）ときにメンバーに表示できるカスタムバッジを追加できます

### バッジの表示 {#badge-visibility}

現在、コミュニティメンバーが獲得するバッジ、またはコミュニティメンバーに割り当てられるバッジは、次の場所にメンバーの名前とアバターとともに表示されます。

* プロファイル
* [フォーラム](forum.md)
* [Q&amp;A](working-with-qna.md)
* [リーダーボード](enabling-leaderboard.md)
* [アイディエーション](ideation-feature.md)

オーサー環境でバッジコンソールに接続するには

* From global navigation: **[!UICONTROL Tools > Communities > Badges]**

このコンソールでは、現在利用可能なバッジが表示され、新しいバッジを追加できます。

![chlimage_1-242](assets/chlimage_1-242.png)

## バッジを作成 {#create-badge}

バッジを作成するには、適度に小さい画像（高さが 26 から 32 ピクセルの 72 dpi）をアップロードし、名前を入力します。The badge image is stored in the repository at `/etc/community/badging/images` and is automatically replicated to the publish environment.

パブリッシュ環境がパブリッシャーのファームである場合、[ユーザーの同期](sync.md)を設定する必要があります。

![chlimage_1-243](assets/chlimage_1-243.png)

* **[!UICONTROL 画像をアップロード]**

   (*Required*) A badge image with a recommended size of 32 x 32 pixels at 72dpi in either the JPEG or PNG format.

* **[!UICONTROL 名前]**

   (*Required*) The badge name. It is the default `Display Name` as well as the repository node name. If the `Name` is not a valid repository node name, it will be modified.

* **[!UICONTROL 表示名]**

   (*Optional*) The name to display for the badge in the UI. Default is the unaltered text entered for the `Name`.

* **[!UICONTROL 説明]**

   (*Optional*) A description for the badge.

## 追加情報 {#additional-information}

For details on setting up scoring and badging rules, see [Scoring and Badges](implementing-scoring.md).

メンバーのバッジの管理については、[メンバーコンソール](members.md)を参照してください。
