---
title: テストツールおよび追跡ツール
seo-title: テストツールおよび追跡ツール
description: AEM では、コンポーネント UI のテスト用フレームワークとコンポーネントのテストおよびデバッグ用メカニズムが提供されています
seo-description: AEM では、コンポーネント UI のテスト用フレームワークとコンポーネントのテストおよびデバッグ用メカニズムが提供されています
uuid: 29c43202-0a4e-41ba-9176-92fa77c627d5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: testing
content-type: reference
discoiquuid: 0f977264-fe58-4478-bd38-aca5c75f36aa
translation-type: tm+mt
source-git-commit: 60f36a33471dbbd9ca877dbbedc82ade606a125c

---


# テストツールおよび追跡ツール{#testing-and-tracking-tools}

## テスト {#testing}

AEM には次の機能があります。

* [コンポーネント UI のテスト用フレームワーク](/help/sites-developing/hobbes.md)
* [コンポーネントのテストおよびデバッグ用メカニズム](/help/sites-developing/developer-mode.md)

オープンソースのテストツールには、次の 2 つがあります。

**Selenium**

Selenium は、ブラウザーでの 1 人のユーザーによる 1 アクティビティごとの機能テストに使用します。テスト手順（クリック）は、HTMLテーブルまたはJavaクラスとして記録されます。

For more information see [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**JMeter**

JMeter は、要求の追跡に使用します。機能テスト、パフォーマンステスト、ストレステストに使用できます。

詳しくは、[http://jakarta.apache.org/jmeter/](http://jakarta.apache.org/jmeter/) を参照してください。

テストの自動化やテスト計画管理のための専用ツールも数多く存在します。

## 追跡 {#tracking}

以下のツールは簡単に入手できます。 ただし、どのような場合でも重要な問題は、プロジェクトチームのすべてのメンバー（パートナーと顧客）がデータを利用できることです。

**Bugzilla**

独自の要件に合わせて設定できるバグ追跡システム。

**スプレッドシート**

バグ追跡専用のツールではありませんが、わかりやすく、ほとんどのユーザーが機能を使用したことがあるので、スプレッドシートは、この用途でよく「誤用」されています。

これらをトラッキングに使用する場合：

* 彼らは簡単にしておくべきだ。
* 個々のスプレッドシートの数は最小限に抑える必要があります。
* スプレッドシートは定期的に更新します。
* 1 つのマスターコピーだけを維持し、すべての関係者にマスターコピーの保存場所を通知します。
* プロジェクトメンバー全員がアクセスできるようにします。
* セキュリティの問題が発生し（大企業で多くの場合）、一般的なアクセスが不可能な場合は、すべてのユーザーがコピーであり、更新できないことを認識している限り、コピーを配布できます。

繰り返しますが、バグおよび機能要件を追跡するための専用ツールも数多く存在します。
