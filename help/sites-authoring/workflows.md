---
title: ワークフローの操作
seo-title: Working with Workflows
description: AEMのワークフローを使用すると、ページまたはアセットで実行される一連の手順を自動化できます。
seo-description: Workflows in AEM allow you to automate a series of steps that are performed on a page or asset.
uuid: c4442d2a-c6b0-49d4-a1ce-384017c45bf0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 7cb99618-d903-4cfb-b0d9-b23d189f6e78
exl-id: 8d318fd5-3d8f-4144-95c8-d90685378a91
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 26%

---

# ワークフローの操作 {#working-with-workflows}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEMワークフローを使用すると、（1 つ以上の）ページやアセットで実行される一連の手順を自動化できます。

例えば、パブリッシュ時にエディターは、サイトの管理者がページをアクティベートする前にコンテンツをレビューする必要があります。この例を自動化するワークフローでは、必要な作業を実行するときが来たことが各参加者に通知されます。

1. 作成者が、ページにワークフローを適用します。
1. エディターは、ページのコンテンツを確認する必要があることを示す作業項目を受け取ります。 完了すると、作業項目が完了したことを示します。
1. 次に、サイト管理者が、ページのアクティベートを要求する作業項目を受け取ります。 完了すると、作業項目が完了したことを示します。

通常は次のようになります。

* コンテンツ作成者は、ページにワークフローを適用し、ワークフローに参加します。
* 使用するワークフローは、組織のビジネスプロセスに固有のものです。

以下のページでは、

* [ページへのワークフローの適用 ](/help/sites-authoring/workflows-applying.md)
* [ワークフローへの参加 ](/help/sites-authoring/workflows-participating.md)
