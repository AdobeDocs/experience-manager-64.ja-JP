---
title: AEM PhoneGap の起動
seo-title: Starting AEM PhoneGap
description: このページでは、開発者向けの starterkit について説明します。
seo-description: Follow this page to learn about the starterkit for developers.
uuid: 952bf9f9-5c79-4212-91b7-1d3850ec2402
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 2ecf05ed-4e56-4e0b-89cf-5161741f9001
exl-id: 8e9a8739-76cd-4507-9c6c-86a5ad486618
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 4%

---

# AEM PhoneGap の起動 {#starting-aem-phonegap}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

デベロッパーにとって、まず github のAdobe Experience Manager Mobile Starterkit を見てみるのが最適です

https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit

このスタートキットでは、AEM Mobile開発の基本を順を追って説明し、プロジェクトの作成とガバナンス、必要なツールのインストール、Maven アーキタイプの定義、構築、デプロイ、独自のエクスペリエンスの作成を行います。

開発者は、この例を PhoneGap を使用してAEM Mobileアプリケーションを試す出発点として使用できます。 スターターキットと参照アプリケーションを実行すると、リッチなモバイルアプリケーションを作成するための基本を明確に理解できます。

* 以下を使用： [AEM PhoneGap スターターキット](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit) :AEM Mobileカタログに適したアプリを作成します。
* A [参照アプリ](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 既存のアプリをAEM Mobileに移行する場合も、新規に開始する場合も、AEM Mobileの新機能の多くを示す完全なソースが作成されています。
* すべてのサンプルは GitHub にあります。 [https://github.com/Adobe-Marketing-Cloud-Apps](https://github.com/Adobe-Marketing-Cloud-Apps) Maven でプロジェクトをブートストラップする機能を含めます。
* ほとんどの会議交渉は、 [Kitchen Sink のチュートリアル](https://github.com/blefebvre/aem-phonegap-kitchen-sink)は GitHub でも検索でき、Apache Cordova のネイティブ拡張機能の使用に重点を置いています。

>[!NOTE]
>
>スターターキットに慣れる機会があれば、Adobe Experience Managerについて学ぶことが重要です *コンポーネントとテンプレート*

## テンプレートとコンポーネント {#templates-and-components}

AEM *テンプレート* および *コンポーネント* 事業部門の所有者がカスタムエクスペリエンスを作成できるようにします。 テンプレートと *コンポーネント* は、標準で用意されている場合も、開発者が既存のコンポーネントを拡張する場合も、緑のフィールド（詳細）を作成する場合も、ユーザーがカスタムで開発する場合もあります。 *テンプレート* および *コンポーネント* AEM オーサーがドラッグ&amp;ドロップして、魅力的で関連性の高いエクスペリエンスを作成できるようにします。

1. [コンポーネントの作成](/help/sites-developing/components.md)
1. [テンプレートの作成](/help/sites-developing/templates.md)

上記の 2 つの手順について明確に理解したら、次の手順に進みます。

1. [AEM Mobileアプリの構造](/help/mobile/phonegap-structure-an-app.md)
1. [AEM Mobileアプリの詳細な構造](/help/mobile/phonegap-apps-arch.md)
1. [既存のアプリのAEM Mobile対応状態](/help/mobile/phonegap-adding-content-to-imported-app.md)

## 次の手順 {#the-next-steps}

1. [AEM Mobileアプリのエクスペリエンスを開始する](/help/mobile/starting-aem-phonegap-app.md)
1. [アプリのコンテンツを管理](/help/mobile/phonegap-manage-app-content.md)
1. [アプリケーションのビルド](/help/mobile/building-app-mobile-phonegap.md)
1. [アプリのモバイル分析を使用してAdobeのパフォーマンスを追跡する](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Targetでパーソナライズされたアプリエクスペリエンスを配信](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [ユーザーに重要なメッセージを送信する](/help/mobile/phonegap-push-notifications.md)
