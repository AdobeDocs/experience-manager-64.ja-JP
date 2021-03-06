---
title: AEM 6.4 へのアップグレード
seo-title: Upgrading to AEM 6.4
description: 古い AEM のインストールを AEM 6.4 にアップグレードするための基礎について説明します。
seo-description: Learn about the basics of upgrading an older AEM installation to AEM 6.4.
uuid: aa878528-5161-4df3-9fed-cc779fb6bdbe
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
discoiquuid: 81ceb91d-039e-45f0-9b0c-b8233901dea8
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 791da16c-bf2c-47a9-86a4-0a601a1b017e
source-git-commit: edba9586711ee5c0e5549dbe374226e878803178
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 93%

---

# AEM 6.4 へのアップグレード{#upgrading-to-aem}

この節では、AEM 6.4 への AEM インストール環境のアップグレードについて説明します。

* [アップグレードの計画](/help/sites-deploying/upgrade-planning.md)
* [パターン検出を使用したアップグレードの複雑性の評価](/help/sites-deploying/pattern-detector.md)
* [AEM 6.4 における後方互換性](/help/sites-deploying/backward-compatibility.md)
* [アップグレード手順](/help/sites-deploying/upgrade-procedure.md)
* [コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md)
* [アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [インプレースアップグレードの実行](/help/sites-deploying/in-place-upgrade.md)
* [アップグレード後のチェックおよびトラブルシューティング](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [持続可能なアップグレード](/help/sites-deploying/sustainable-upgrades.md)
* [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md)
* [AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md)

この手順に出てくる AEM インスタンスをわかりやすく区別するために、以下のように呼ぶことにします。

* アップグレード元の AEM インスタンスを「ソース」インスタンスと呼びます&#x200B;*。*
* アップグレード先のインスタンスを「ターゲット」インスタンスと呼びます&#x200B;*。*

>[!NOTE]
>
>アップグレードの信頼性を向上させる取り組みの一環として、AEM 6.4 では包括的なリポジトリ再構築がおこなわれました。 新しい構造に合わせる方法について詳しくは、 [AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md)

## 変更点 {#what-has-changed}

以下に、AEM の最近のいくつかのリリースでの注目すべき主な変更点を示します。

AEM 6.0 で、新しい Jackrabbit Oak リポジトリが導入されました。Persistence Manager は、[マイクロカーネル](/help/sites-deploying/recommended-deploys.md)で置き換えられました。バージョン 6.1 から CRX2 がサポートされなくなりました。5.6.1 のインスタンスから CRX2 リポジトリを移行するには、crx2oak という移行ツールを実行する必要があります。詳しくは、[CRX2OAK 移行ツールの使用](/help/sites-deploying/using-crx2oak.md)を参照してください。

アセットインサイトを使用し、AEM 6.2 より前のバージョンからアップグレードする場合は、アセットを移行し、JMX Bean で ID を生成する必要があります。アドビの内部テストでは TarMK 環境の 12.5 万個のアセットが 1 時間で移行されましたが、ユーザーの結果は異なる場合があります。

AEM 6.3 では、 `SegmentNodeStore`:TarMK 実装の基礎です。 AEM 6.3 よりも古いバージョンからアップグレードする場合は、アップグレードの一環としてリポジトリの移行が必要になり、システムのダウンタイムが発生します。

アドビのエンジニアリング部は、この移行には約 20 分かかると予測しています。インデックスの再作成は必要ないことに注意してください。また、新しいリポジトリ形式で機能するように crx2oak ツールの新しいバージョンがリリースされました。

**AEM 6.3 から AEM 6.4 へのアップグレード時には、この移行は必要ありません。**

アップグレード前のメンテナンスタスクは、自動化をサポートするように最適化されました。

crx2oak ツールのコマンドライン使用オプションは、自動化しやすく、より多くのアップグレードパスをサポートするように変更されました。

アップグレード後のチェックも自動化しやすくなりました。

リビジョンの定期的ガベージコレクションと、データストアのガベージコレクションは、一定期間ごとに実行する必要がある定期メンテナンスタスクです。AEM 6.3 の導入に伴い、アドビはオンラインリビジョンクリーンアップをサポートし、推奨するようになりました。これらのタスクの設定方法については、[リビジョンクリーンアップ](/help/sites-deploying/revision-cleanup.md)を参照してください。

**AEM 6.4** では、アップグレードの計画時に役立つ、アップグレードの複雑性評価のための[パターン検出](/help/sites-deploying/pattern-detector.md)が導入されました。また、6.4 では、機能の[後方互換性](/help/sites-deploying/backward-compatibility.md)が非常に重視されています。[持続可能なアップグレード](/help/sites-deploying/sustainable-upgrades.md)のためのベストプラクティスも追加されています。

最近の AEM バージョンの変更点について詳しくは、完全版のリリースノートを参照してください。

* [https://helpx.adobe.com/jp/experience-manager/6-2/release-notes.html](https://helpx.adobe.com/jp/experience-manager/6-2/release-notes.html)
* [https://helpx.adobe.com/jp/experience-manager/6-3/release-notes.html](https://helpx.adobe.com/jp/experience-manager/6-3/release-notes.html)
* [https://helpx.adobe.com/jp/experience-manager/6-4/release-notes.html](https://helpx.adobe.com/jp/experience-manager/6-4/release-notes.html)

## アップグレードの概要 {#upgrade-overview}

AEM のアップグレードには複数の段階があり、場合によっては数ヶ月のプロセスとなります。以下に、アップグレードプロジェクトに含まれる作業、およびこのドキュメントに含まれる内容の概要を示します。

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## 6.4 でのアップグレードの機能強化を含むアップグレードフロー {#upgrade-overview-1}

以下の図は、アップグレードの方法を示す、全体的なアップグレード推奨フローです。導入された新機能も示されています。アップグレードは、まずパターン検出から始まります（[パターン検出を使用したアップグレードの複雑性の評価](/help/sites-deploying/pattern-detector.md)を参照）。ここで生成されたレポートのパターンに基づき、AEM 6.4 との互換性を確保するためにどのパスを使用するかを決定できます。

6.4 では、すべての新機能において後方互換性を保つことが非常に重視されています。ただし、後方互換性の問題が生じる場合は、互換モードを使用することで、カスタムコードを 6.4 準拠にする開発作業を一時的に先送りできます。この方法を使用することで、アップグレード後すぐに開発をおこなう必要がなくなります（[AEM 6.4 における後方互換性](/help/sites-deploying/backward-compatibility.md)を参照）。

6.4 の開発サイクルでは、持続可能なアップグレード（[持続可能なアップグレード](/help/sites-deploying/sustainable-upgrades.md)を参照）の下で導入された機能により、今後のアップグレードをより効率的かつシームレスにするためのベストプラクティスに従いやすくなります。

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
