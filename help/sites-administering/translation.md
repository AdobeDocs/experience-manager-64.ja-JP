---
title: 多言語サイトのコンテンツの翻訳
seo-title: 多言語サイトのコンテンツの翻訳
description: 多言語サイトのコンテンツの翻訳方法について説明します。
seo-description: 多言語サイトのコンテンツの翻訳方法について説明します。
uuid: b8047f6f-e86a-495d-9b80-731ac7d83c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 67faa2ee-cb12-44b0-8bfb-534d1d6c360a
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
translation-type: tm+mt
source-git-commit: 7b39a715166eeefdf20eb22a4449068ff1ed0e42
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 87%

---


# 多言語サイトのコンテンツの翻訳{#translating-content-for-multilingual-sites}

ページコンテンツ、アセットおよびユーザー生成コンテンツの翻訳を自動化して、多言語の Web サイトを作成および管理します。翻訳ワークフローを自動化するには、翻訳サービスプロバイダーと AEM とを統合して、コンテンツを複数の言語に翻訳するためのプロジェクトを作成します。AEM では人間による翻訳と機械翻訳のワークフローがサポートされます。

* 人間による翻訳：コンテンツが翻訳プロバイダーに送信され、専門の翻訳者によって翻訳されます。完了すると、翻訳コンテンツが返されて、AEM に読み込まれます。翻訳プロバイダーが AEM と統合されると、AEM と翻訳プロバイダーとの間でコンテンツが自動的に送信されます。
* 機械翻訳：機械翻訳サービスでは、コンテンツがすぐに翻訳されます。

コンテンツの翻訳には次の手順が含まれます。

1. [AEM を翻訳プロバイダーサービスに接続](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)して、[翻訳統合フレームワーク設定を作成](/help/sites-administering/tc-tic.md)します。

1. 翻訳サービスとフレームワークの設定に[言語マスターのページを関連付け](/help/sites-administering/tc-tic.md#configuring-pages-for-translation)ます。
1. [翻訳する](/help/sites-administering/tc-rules.md) コンテンツのタイプを指定します。
1. [翻訳するコンテンツを準備](/help/sites-administering/tc-prep.md)します。そのためには、言語マスターをオーサリングして、言語コピーのルートページを作成します。
1. [翻訳](/help/sites-administering/tc-manage.md) プロジェクトを作成して、翻訳するコンテンツを収集し、翻訳プロセスを準備します。
1. 翻訳プロジェクトを使用して、[コンテンツの翻訳プロセスを管理](/help/sites-administering/tc-manage.md)します。

AEM との統合のためのコネクターが翻訳サービスプロバイダーに用意されていない場合、AEM では翻訳コンテンツ（XML 形式）の手動による抽出と再挿入がサポートされます。

>[!NOTE]
>
>言語コピー機能を使用するには、ユーザーはプロジェクト管理者グループのメンバーである必要があります。

## ベストプラクティス {#best-practices}

[翻訳のベストプラクティス](/help/sites-administering/tc-bp.md)ページには、導入に関する重要な情報が記載されています。
