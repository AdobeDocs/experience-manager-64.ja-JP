---
title: ワークフローの操作
seo-title: Working with Workflows
description: AEM のワークフローでは、ページまたはアセットで実行される一連の手順を自動化できます。
seo-description: Workflows in AEM allow you to automate a series of steps that are performed on a page or asset.
uuid: c4442d2a-c6b0-49d4-a1ce-384017c45bf0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 7cb99618-d903-4cfb-b0d9-b23d189f6e78
exl-id: 8d318fd5-3d8f-4144-95c8-d90685378a91
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 100%

---

# ワークフローの操作 {#working-with-workflows}

AEM ワークフローでは、（1 つ以上の）ページおよびアセットで実行される一連の手順を自動化できます。

例えば、パブリッシュ時にエディターは、サイトの管理者がページをアクティベートする前にコンテンツをレビューする必要があります。この例を自動化するワークフローでは、必要な作業を実行するときが来たことが各参加者に通知されます。

1. 作成者がワークフローをページに適用します。
1. エディターは、ページの内容をレビューする必要があることを示す作業項目を受け取ります。これが完了すると、作業項目が完了したことが示されます。
1. 次に、サイトの管理者は、ページのアクティベートを要求する作業項目を受け取ります。これが完了すると、作業項目が完了したことが示されます。

一般的に、以下のようになります。

* コンテンツの作成者がワークフローをページに適用し、ワークフローに参加します。
* 使用するワークフローは、組織のビジネスプロセスに固有です。

参考資料：

* [ページへのワークフローの適用 ](/help/sites-authoring/workflows-applying.md)
* [ワークフローへの参加 ](/help/sites-authoring/workflows-participating.md)
