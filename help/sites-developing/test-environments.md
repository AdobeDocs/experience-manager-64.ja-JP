---
title: 必要なテスト環境の種類
seo-title: Which Test Environments are needed?
description: テストの一部として考慮する必要がある環境はいくつかあります
seo-description: Several environments should be considered as part of testing
uuid: bb725e50-edae-4c20-8107-d1c8df2e60e2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: testing
content-type: reference
discoiquuid: db528b9b-3407-462d-8254-20b3cc2c3ccf
exl-id: c3c7c007-4814-4bd1-987e-534df4575a4a
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 67%

---

# 必要になるテスト環境の種類{#which-test-environments-will-be-needed}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

テストする設定を定義するには、次の点を考慮する必要があります。

**開発** — 単体テスト、特定の統合テストの場合。

**テスト** — 大部分のテスト用。

**ライブ** — 最終的なパフォーマンステストとストレステスト。顧客の受け入れテスト用。

また、必要なインスタンスを決定する必要があります（通常、すべてのレベルのテスト用に各インスタンスの少なくとも 1 つ）。

**作成者** — このインスタンスで、作成者がコンテンツを入力したり公開したりできます。

**公開** — このインスタンスは、訪問者がアクセスするための、公開済みの形式の Web サイトを表します。

Dispatcher と合わせてテストする必要があります。

最後に、実際のハードウェアを考慮する必要があります。パフォーマンステストは、可能な限り最終的な実稼働環境に近い設定で、システム上で行う必要があります。 このため、プロジェクトの開始は、次の場所に分割することをお勧めします。

**ソフトローンチ** — 可用性を制限。実稼動環境の現実的な条件下でパフォーマンステスト、チューニングおよび最適化をおこなうための時間を確保できます。

**ハードローンチ** — 完全な可用性。
