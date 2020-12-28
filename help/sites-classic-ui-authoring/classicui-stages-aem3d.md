---
title: AEM 3D でのステージの使用
seo-title: AEM 3D でのステージの使用
description: ステージは軽量の 3D シーンファイルで、基本的な表示環境（ライト、背景、グラウンドプレーンまたは他の固定ジオメトリ）、オプションの事前定義済みカメラ、サードパーティ製レンダラーのレンダリング設定を提供します。
seo-description: ステージは軽量の 3D シーンファイルで、基本的な表示環境（ライト、背景、グラウンドプレーンまたは他の固定ジオメトリ）、オプションの事前定義済みカメラ、サードパーティ製レンダラーのレンダリング設定を提供します。
uuid: 303ecbbd-131e-4c6f-812a-1e056b1e1d63
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: cbcfbe88-e60c-446c-bbfe-2509831d6c22
translation-type: tm+mt
source-git-commit: 7b39a715166eeefdf20eb22a4449068ff1ed0e42
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 78%

---


# AEM 3D でのステージの使用{#about-the-use-of-stages-in-aem-d}

ステージは軽量の 3D シーンファイルで、基本的な表示環境（ライト、背景、グラウンドプレーンまたは他の固定ジオメトリ）、オプションの事前定義済みカメラ、サードパーティ製レンダラーのレンダリング設定を提供します。

>[!NOTE]
>
>OBJ 3D 形式はライトをサポートしていません。したがって、この形式を使用して AEM 3D にステージを提供することはできません。

ステージのファイル形式によって、そのステージで使用できるレンダラーが決まります。たとえば、高品質レンダリングにAutodesk® Maya®を使用する場合、ステージは`.ma`または`.mb`の形式にする必要があります。 デフォルトの Rapid Refine™ レンダラーのみを使用する場合は、サポートされているすべてのステージファイル形式を使用できます。

AEM 3Dのすべてのレンダリング設定（出力画像のタイプとサイズを除く）は、AEMにアップロードする前に、事前に設定してステージファイルに保存する必要があります。

