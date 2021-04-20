---
title: AEM 3D でのステージの使用
seo-title: AEM 3D でのステージの使用
description: ステージは軽量の 3D シーンファイルで、基本的な表示環境を提供します。
seo-description: ステージは軽量の 3D シーンファイルで、基本的な表示環境を提供します。
uuid: 9098278c-0467-45ea-98ad-7f345c314d9e
contentOwner: Rick Brough
topic-tags: 3D
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
discoiquuid: 7b9d3b81-3bb4-4ca6-b6e1-f9adfb455855
exl-id: 6d82fec0-608e-4eaa-aebd-b3ce2f7d8088
feature: 3D Assets
role: Business Practitioner
translation-type: tm+mt
source-git-commit: f9faa357f8de92d205f1a297767ba4176cfd1e10
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 70%

---

# AEM 3D でのステージの使用 {#about-the-use-of-stages-in-aem-d}

ステージは軽量の 3D シーンファイルで、基本的な表示環境（ライト、背景、グラウンドプレーンまたは他の固定ジオメトリ）、オプションの事前定義済みカメラ、サードパーティ製レンダラーのレンダリング設定を提供します。

>[!NOTE]
>
>**[!UICONTROL OBJ 3D]**&#x200B;形式はライトをサポートしていません。 したがって、この形式を使用して AEM 3D にステージを提供することはできません。

ステージのファイル形式によって、そのステージで使用できるレンダラーが決まります。たとえば、高品質レンダリングにAutodesk® Maya®を使用する場合、ステージは`.ma`または`.mb`の形式にする必要があります。 デフォルトの Rapid Refine™ レンダラーのみを使用する場合は、サポートされているすべてのステージファイル形式を使用できます。

AEMにアップロードする前に、出力画像のタイプとサイズを除くAEM 3Dのすべてのレンダリング設定を事前に設定し、ステージファイルに保存する必要があります。
