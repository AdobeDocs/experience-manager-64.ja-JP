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
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 35%

---

# 必要になるテスト環境の種類{#which-test-environments-will-be-needed}

テストする設定を定義するには、次の点を考慮する必要があります。

**開発**  — 単体テスト、特定の統合テストの場合。

**テスト**  — テストの大部分。

**ライブ**  — 最終的なパフォーマンステストとストレステスト。 顧客の受け入れテスト用。

また、必要なインスタンスを決定する必要があります（通常、すべてのレベルのテスト用に各インスタンスの少なくとも 1 つ）。

**作成者**  — このインスタンスを使用すると、作成者はコンテンツを入力および公開できます。

**公開**  — このインスタンスは、訪問者がアクセスできるよう、公開済みの形式で Web サイトを表示します。

Dispatcher と合わせてテストする必要があります。

最後に、実際のハードウェアを検討する必要があります。パフォーマンステストはすべて、最終的なライブ環境とできる限り類似した構成のシステムでおこなう必要があります。このため、プロジェクトの開始を次の 2 つに分けることをお勧めします。

**ソフトローンチ**  — 可用性の低減これにより、実稼働環境での実際の状況下でのパフォーマンステスト、チューニング、最適化に要する時間を確保できます。

**ハード起動**  — 完全な可用性。
