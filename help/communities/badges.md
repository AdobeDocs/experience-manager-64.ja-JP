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
role: Administrator
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 65%

---


# バッジコンソール {#badges-console}

## バッジについて {#about-badges}

Communities のバッジコンソールでは、バッジを獲得（授与された）したとき、またはコミュニティで特定の役割についた（割り当てられた）ときにメンバーに表示できるカスタムバッジを追加できます

### バッジの表示  {#badge-visibility}

現在、コミュニティメンバーが獲得するバッジ、またはコミュニティメンバーに割り当てられるバッジは、次の場所にメンバーの名前とアバターとともに表示されます。

* プロファイル
* [フォーラム](forum.md)
* [Q&amp;A](working-with-qna.md)
* [リーダーボード](enabling-leaderboard.md)
* [アイディエーション](ideation-feature.md)

オーサー環境でバッジコンソールに接続するには

* グローバルナビゲーションから：**[!UICONTROL ツール/コミュニティ/バッジ]**

このコンソールでは、現在利用可能なバッジが表示され、新しいバッジを追加できます。

![chlimage_1-242](assets/chlimage_1-242.png)

## バッジを作成 {#create-badge}

バッジを作成するには、適度に小さい画像（高さが 26 から 32 ピクセルの 72 dpi）をアップロードし、名前を入力します。バッジ画像は`/etc/community/badging/images`のリポジトリに保存され、自動的に公開環境に複製されます。

パブリッシュ環境がパブリッシャーのファームである場合、[ユーザーの同期](sync.md)を設定する必要があります。

![chlimage_1-243](assets/chlimage_1-243.png)

* **[!UICONTROL 画像をアップロード]**

   （*必須*）JPEGまたはPNG形式で、推奨サイズが32 x 32ピクセル、72 dpiのバッジ画像。

* **[!UICONTROL Name]**

   （*必須*）バッジ名。 これはデフォルトの`Display Name`とリポジトリノード名です。 `Name`が有効なリポジトリノード名でない場合は、変更されます。

* **[!UICONTROL 表示名]**

   （*オプション*） UIにバッジとして表示する名前。 デフォルトは、`Name`に対して入力された変更なしのテキストです。

* **[!UICONTROL 説明]**

   （*オプション*）バッジの説明。

## 追加情報 {#additional-information}

スコアリングルールとバッジルールの設定について詳しくは、[スコアリングとバッジ](implementing-scoring.md)を参照してください。

メンバーのバッジの管理については、[メンバーコンソール](members.md)を参照してください。
