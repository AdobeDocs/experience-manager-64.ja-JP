---
title: テストツールおよび追跡ツール
seo-title: Testing and Tracking Tools
description: AEMは、コンポーネント UI のテスト用のフレームワークと、コンポーネントのテストとデバッグをおこなうためのメカニズムを提供します
seo-description: AEM provides a framework for testing component UI and a mechanism for testing and debugging components
uuid: 29c43202-0a4e-41ba-9176-92fa77c627d5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: testing
content-type: reference
discoiquuid: 0f977264-fe58-4478-bd38-aca5c75f36aa
exl-id: 9387cdb4-f8de-4229-90d1-59218ac17561
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 52%

---

# テストツールおよび追跡ツール{#testing-and-tracking-tools}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## テスト {#testing}

AEMには次の機能があります。

* [コンポーネント UI のテスト用フレームワーク](/help/sites-developing/hobbes.md)
* [コンポーネントのテストとデバッグを行うメカニズム](/help/sites-developing/developer-mode.md).

次の 2 つのオープンソーステストツールを示します。

**Selenium**

Selenium は、アクティビティごとに 1 人のユーザーでブラウザーの機能テストに使用されます。 テスト手順（クリック）を HTML テーブルまたは Java クラスとして記録します。

詳しくは、[https://www.seleniumhq.org/](https://www.seleniumhq.org/) を参照してください。

**JMeter**

JMeter は、リクエストの追跡に使用され、機能、パフォーマンス、およびストレステストに使用できます。

詳しくは、 [http://jakarta.apache.org/jmeter/](http://jakarta.apache.org/jmeter/).

また、テストを自動化し、テスト計画を管理するための独自のツールも多数用意されています。

## トラッキング {#tracking}

以下のツールを簡単に利用できます。ただし、どの場合でも大切なポイントは、プロジェクトチームのすべてのメンバー（パートナーやお客様を含む）がデータを利用できることです。

**バグジラ**

独自の要件に合わせて設定できるバグ追跡システム。

**スプレッドシート**

バグ追跡専用のツールではありませんが、わかりやすく、ほとんどのユーザーが機能を使用したことがあるので、スプレッドシートは、この用途でよく「誤用」されています。

これらをトラッキングに使用する場合は、次のポイントに留意します。

* シンプルを心がける。
* 個々のスプレッドシートの数は、最小限に抑える必要があります。
* 定期的に更新する必要があります。
* 1 つのマスターコピーのみを管理し、すべてのユーザーがマスターコピーの場所を把握する必要があります。
* すべてのプロジェクトメンバーがアクセスできるようにする必要があります。
* セキュリティが問題で（多くの場合、大企業で発生）、共通のアクセスを確立できない場合は、これらがコピーであり更新できないことを全員が理解している限り、コピーを配布できます。

繰り返しますが、バグおよび機能要件を追跡するための専用ツールも数多く存在します。
