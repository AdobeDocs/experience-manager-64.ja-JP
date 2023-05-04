---
title: サードパーティのサービスとの統合
seo-title: Integrating with Third-Party Services
description: AEMをサードパーティのサービスと統合する方法について説明します。
seo-description: Learn how to integrate AEM with third party services.
uuid: bfafd00b-46bc-4af2-b3e8-874afb1ed697
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: e0d6478a-4420-46a6-96fe-082a30ee82f0
exl-id: 9a3857fd-4f62-4293-950b-75626e4dcf50
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 43%

---

# サードパーティのサービスとの統合{#integrating-with-third-party-services}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEMを使用すると、を次の非Adobe製品の標準でと統合できます。

* Amazon SNS 接続 — Amazon Web サービス
* BrightEdge Content Optimizer — 検索用に最適化されたコンテンツ
* ExactTarget — 電子メールマーケティング
* Facebook Connect — ソーシャルネットワーキング
* 汎用分析スニペット — analytics
* Microsoft Translator またはその他の機械翻訳プロバイダー
* Pushwoosh 接続 — アプリ — プッシュ通知
* Salesforce - 販売および CRM ソフトウェア
* Silverpop Engage — マーケティングの自動化、電子メール、モバイルおよびソーシャル
* Twitter — ソーシャルネットワーキング
* YouTube — ビデオ共有

また、AEMを [Marketing Cloud](/help/sites-administering/marketing-cloud.md) そして [Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

## Salesforce との統合 {#integrating-with-salesforce}

Salesforce.com は企業向けのクラウドコンピューティングを提供し、ソーシャルエンタープライズへの移行を支援します。

AEMサイトと Salesforce の統合について詳しくは、 [Salesforce との統合](/help/sites-administering/salesforce.md).

## Silverpop Engage との統合 {#integrating-with-silverpop-engage}

>[!NOTE]
>
>Silverpop Engage 統合は、初期設定では使用できません。 AEMを Silverpop Engage と統合するには、以下を実行します。 [パッケージをダウンロード](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content) をパッケージ共有から削除します。

Silverpop Engage は、マーケティングの自動化、電子メール、モバイルおよびソーシャルを提供します。

AEMサイトと ExactTarget の統合について詳しくは、 [Silverpop Engage との統合](/help/sites-administering/silverpop.md).

## ExactTarget との統合 {#integrating-with-exacttarget}

ExactTarget の電子メールマーケティングソリューションを使用すると、あらゆる規模の組織において、ターゲットを厳選し、完全に統合された、きわめて重要な電子メールキャンペーンを企画して実施できます。

AEMサイトと ExactTarget の統合について詳しくは、 [ExactTarget の設定](/help/sites-administering/exacttarget.md).

## facebookおよびTwitterとの統合 {#integrating-with-facebook-and-twitter}

Facebook および Twitter は広く普及しているソーシャルネットワーキングサービスです。AEM と Facebook および Twitter の統合によって、組織が所有しているデジタル資産に Facebook または Twitter のログインオプションを付けて、プロファイル情報に基づいてユーザーエクスペリエンスをパーソナライズすることができます。マーケティング担当者は、プロファイル情報を他のソースのデータ（顧客関係管理システムや Web サイトのプロファイルなど）と組み合わせて、統一されたユーザービューを作成することもできます。

詳しくは、[ソーシャルログイン](/help/communities/social-login.md)を参照してください。

## その他のプロバイダーとの統合 {#integrating-with-other-providers}

AEMを使用すると、 [汎用分析スニペット。](/help/sites-administering/external-providers.md)
