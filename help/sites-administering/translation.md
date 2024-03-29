---
title: 多言語サイトのコンテンツの翻訳
seo-title: Translating Content for Multilingual Sites
description: 多言語サイトのコンテンツを翻訳する方法を説明します。
seo-description: Learn how to translate content for multilingual sites.
uuid: b8047f6f-e86a-495d-9b80-731ac7d83c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 67faa2ee-cb12-44b0-8bfb-534d1d6c360a
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
feature: Language Copy
exl-id: 3a3f5c4d-6c3f-4201-acc8-dbd138bb59ba
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 66%

---

# 多言語サイトのコンテンツの翻訳{#translating-content-for-multilingual-sites}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ページコンテンツ、アセット、ユーザー生成コンテンツの翻訳を自動化して、多言語の Web サイトを作成および管理します。 翻訳ワークフローを自動化するには、翻訳サービスプロバイダーをAEMと統合し、コンテンツを複数の言語に翻訳するためのプロジェクトを作成します。 AEMは、人間による翻訳ワークフローと機械翻訳ワークフローをサポートしています。

* 人間による翻訳：コンテンツが翻訳プロバイダーに送信され、専門の翻訳者によって翻訳されます。翻訳が完了すると、翻訳済みコンテンツが返されて、AEM に読み込まれます。翻訳プロバイダーが AEM に統合されると、コンテンツは AEM と翻訳プロバイダーの間で自動的に送信されます。
* 機械翻訳：機械翻訳サービスでは、コンテンツがすぐに翻訳されます。

コンテンツの翻訳には次の手順が含まれます。

1. [AEM を翻訳プロバイダーサービスに接続](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)して、[翻訳統合フレームワーク設定を作成](/help/sites-administering/tc-tic.md)します。

1. 翻訳サービスとフレームワークの設定に[言語マスターのページを関連付け](/help/sites-administering/tc-tic.md#configuring-pages-for-translation)ます。
1. 翻訳する[コンテンツのタイプを特定](/help/sites-administering/tc-rules.md)します。
1. [翻訳するコンテンツを準備](/help/sites-administering/tc-prep.md)します。そのためには、言語マスターをオーサリングして、言語コピーのルートページを作成します。
1. [翻訳プロジェクトを作成](/help/sites-administering/tc-manage.md)して、翻訳するコンテンツを収集し、翻訳プロセスを準備します。
1. 翻訳プロジェクトを使用して、[コンテンツの翻訳プロセスを管理](/help/sites-administering/tc-manage.md)します。

AEM との統合のためのコネクタが翻訳サービスプロバイダーに用意されていない場合、AEM では翻訳コンテンツ（XML 形式）の手動による抽出と再挿入がサポートされます。

>[!NOTE]
>
>言語コピー機能を使用するには、ユーザーが project-administrators グループのメンバーである必要があります。

## ベストプラクティス {#best-practices}

[翻訳のベストプラクティス](/help/sites-administering/tc-bp.md)には、実装に関する重要な情報が記載されています。
