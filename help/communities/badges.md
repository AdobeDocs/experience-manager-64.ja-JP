---
title: バッジコンソール
seo-title: Badges Console
description: Communities のバッジコンソールを使用すると、バッジを獲得（授与された）したとき、またはコミュニティで特定の役割についた（割り当てられた）ときにメンバーに表示できるカスタムバッジを追加できます
seo-description: The Communities Badges console lets you add custom badges that can be displayed for members when earned (awarded) or when they take on a specific role in the community (assigned)
uuid: 9eeba240-f0d4-4937-baba-8bac0e0b2a36
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 4194278f-5127-4105-b181-60961c7a1def
role: Admin
exl-id: b6aa9d73-4e20-446a-a1fc-78f8968d6844
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 61%

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

* グローバルナビゲーションから： **[!UICONTROL ツール/コミュニティ/バッジ]**

このコンソールでは、現在利用可能なバッジが表示され、新しいバッジを追加できます。

![chlimage_1-242](assets/chlimage_1-242.png)

## バッジを作成 {#create-badge}

バッジを作成するには、適度に小さい画像（高さが 26 から 32 ピクセルの 72 dpi）をアップロードし、名前を入力します。バッジの画像は、リポジトリ ( ) の `/etc/community/badging/images` とは、パブリッシュ環境に自動的にレプリケートされます。

パブリッシュ環境がパブリッシャーのファームである場合、[ユーザーの同期](sync.md)を設定する必要があります。

![chlimage_1-243](assets/chlimage_1-243.png)

* **[!UICONTROL 画像をアップロード]**

   (*必須*)JPEGまたは PNG 形式の 72dpi での推奨サイズが 32 x 32 ピクセルのバッジ画像。

* **[!UICONTROL 名前]**

   (*必須*) バッジ名。 これがデフォルトです `Display Name` リポジトリのノード名。 この `Name` は有効なリポジトリノード名ではありません。変更されます。

* **[!UICONTROL 表示名]**

   (*オプション*) UI でバッジに表示する名前です。 デフォルトは、 `Name`.

* **[!UICONTROL 説明]**

   (*オプション*) バッジの説明。

## 追加情報 {#additional-information}

スコアルールとバッジルールの設定について詳しくは、 [スコアとバッジ](implementing-scoring.md).

メンバーのバッジの管理については、[メンバーコンソール](members.md)を参照してください。
