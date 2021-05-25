---
title: SPA の動的モデルとコンポーネントのマッピング
seo-title: SPA の動的モデルとコンポーネントのマッピング
description: この記事では、AEM 用 JavaScript SPA SDK で動的モデルとコンポーネントとのマッピングがどのようにおこなわれるかを説明します。
seo-description: この記事では、AEM 用 JavaScript SPA SDK で動的モデルとコンポーネントとのマッピングがどのようにおこなわれるかを説明します。
uuid: 337b8d90-efd7-442e-9fac-66c33cc26212
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: spa
content-type: reference
discoiquuid: 8b4b0afc-8534-4010-8f34-cb10475a8e79
exl-id: 2bbbfbaa-b0a1-4f8a-9445-51325d80e368
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 83%

---

# SPA の動的モデルとコンポーネントのマッピング{#dynamic-model-to-component-mapping-for-spas}

このドキュメントでは、AEM 用 JavaScript SPA SDK で動的モデルとコンポーネントのマッピングがどのようにおこなわれるかを説明します。

>[!NOTE]
>シングルページアプリケーション(SPA)エディター機能には、AEM 6.4サービスパック2以降が必要です。
>
>SPA Editorは、SPAフレームワークベースのクライアントサイドレンダリング(ReactやAngularなど)が必要なプロジェクトで推奨されるソリューションです。

## ComponentMapping モジュール {#componentmapping-module}

`ComponentMapping` モジュールは、プロントエンドプロジェクトに NPM パッケージとして提供されます。フロントエンドコンポーネントを格納し、単一ページアプリケーションがフロントエンドコンポーネントを AEM リソースタイプにマップする方法を提供します。これにより、アプリケーションの JSON モデルを構文解析する際に、コンポーネントの動的な解決が可能になります。

モデル内の各項目には、AEM リソースタイプを表示する `:type` フィールドが含まれます。フロントエンドコンポーネントは、マウントされると、基になるライブラリから受け取ったモデルのフラグメントを使用して自分自身をレンダリングできます。

モデル解析とモデルへのフロントエンドコンポーネントアクセスの詳細については、[SPA ブループリント](/help/sites-developing/spa-blueprint.md)ドキュメントを参照してください。

npmパッケージも参照してください。[https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

## モデル駆動型単一ページアプリケーション {#model-driven-single-page-application}

AEM 用 JavaScript SPA SDK を利用する単一ページアプリケーションは、モデル主導です。

1. フロントエンドコンポーネントは、自らを[コンポーネントマッピングストア](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module)に登録します。
1. 次に、[コンテナ](/help/sites-developing/spa-blueprint.md#container)は、 [モデルプロバイダー](/help/sites-developing/spa-blueprint.md#the-model-provider)がモデルを提供した後、そのモデルコンテンツ（`:items`）を反復します。

1. ページの場合、その子（`:children`）は、最初に [](/help/sites-developing/spa-blueprint.md#componentmapping) コンポーネントマッピングからコンポーネントクラスを取得し、次にインスタンス化します。

## アプリの初期化 {#app-initialization}

各コンポーネントは、 [ `ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider)の機能で拡張されます。 初期化は、次の一般的な形式をとります。

1. 各モデルプロバイダーは自身を初期化し、内部コンポーネントに対応するモデルの部分に対しておこなわれる変更をリッスンします。
1. [ `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager)は、[初期化フロー](/help/sites-developing/spa-blueprint.md)で表されるように初期化する必要があります。

1. 保存されると、ページモデルマネージャーはアプリの完全なモデルを返します。
1. 次に、このモデルは、アプリケーションのフロントエンドルート[コンテナ](/help/sites-developing/spa-blueprint.md#container)コンポーネントに渡されます。
1. モデルの断片は、最後に個々の子コンポーネントに伝播されます。

![app_model_initialization](assets/app_model_initialization.png)
