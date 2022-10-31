---
title: テストツールおよび追跡ツール
seo-title: Testing and Tracking Tools
description: AEM では、コンポーネント UI のテスト用フレームワークとコンポーネントのテストおよびデバッグ用メカニズムが提供されています
seo-description: AEM provides a framework for testing component UI and a mechanism for testing and debugging components
uuid: 29c43202-0a4e-41ba-9176-92fa77c627d5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: testing
content-type: reference
discoiquuid: 0f977264-fe58-4478-bd38-aca5c75f36aa
exl-id: 9387cdb4-f8de-4229-90d1-59218ac17561
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 96%

---

# テストツールおよび追跡ツール{#testing-and-tracking-tools}

## テスト {#testing}

AEM では以下が提供されます。

* [コンポーネント UI のテスト用フレームワーク](/help/sites-developing/hobbes.md)
* [コンポーネントのテストおよびデバッグ用メカニズム](/help/sites-developing/developer-mode.md)

オープンソースのテストツールには、次の 2 つがあります。

**Selenium**

Selenium は、ブラウザーでの 1 人のユーザーによる 1 アクティビティごとの機能テストに使用します。テスト手順（クリック）を HTML テーブルまたは Java クラスとして記録します。

詳しくは、[https://www.seleniumhq.org/](https://www.seleniumhq.org/) を参照してください。

**JMeter**

JMeter は、要求の追跡に使用します。機能テスト、パフォーマンステスト、ストレステストに使用できます。

詳しくは、[http://jakarta.apache.org/jmeter/](http://jakarta.apache.org/jmeter/) を参照してください。

テストの自動化やテスト計画管理のための専用ツールも数多く存在します。

## 追跡 {#tracking}

以下のツールを簡単に利用できます。ただし、どの場合でも大切なポイントは、プロジェクトチームのすべてのメンバー（パートナーやお客様を含む）がデータを利用できることです。

**Bugzilla**

独自の要件に合わせて設定できるバグ追跡システム。

**スプレッドシート**

バグ追跡専用のツールではありませんが、わかりやすく、ほとんどのユーザーが機能を使用したことがあるので、スプレッドシートは、この用途でよく「誤用」されています。

これらをトラッキングに使用する場合は、次のポイントに留意します。

* シンプルを心がける。
* 個々のスプレッドシートの数は、最小限に抑える必要があります。
* スプレッドシートは定期的に更新します。
* 1 つのマスターコピーだけを維持し、すべての関係者にマスターコピーの保存場所を通知します。
* プロジェクトメンバー全員がアクセスできるようにします。
* セキュリティが問題で（多くの場合、大企業で発生）、共通のアクセスを確立できない場合は、これらがコピーであり更新できないことを全員が理解している限り、コピーを配布できます。

繰り返しますが、バグおよび機能要件を追跡するための専用ツールも数多く存在します。
