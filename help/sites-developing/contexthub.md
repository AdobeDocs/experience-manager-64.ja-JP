---
title: ContextHub
seo-title: ContextHub
description: ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。
seo-description: ContextHub is a framework for storing, manipulating, and presenting context data
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
exl-id: 0a6b815a-5055-4c44-96d1-ff238b4285f3
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 63%

---

# ContextHub{#contexthub}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。クライアントサイド JavaScript API を使用してデータにアクセスし、コンテンツをパーソナライズします。

>[!NOTE]
>
>[We.Retail 参照実装](/help/sites-developing/we-retail.md)は、ContextHub を実装しており、ContextHub をプロジェクトに組み込む際の参考になります。

>[!CAUTION]
>
>[We.Retail 参照実装](/help/sites-developing/we-retail.md)で使用される ContextHub 設定のサンプルを含むパス（`/libs/settings/cloudsettings/legacy`）は、独自の設定を作成する際の参考としてご利用ください。
>
>独自の ContextHub 設定としてプロジェクトで使用しないでください。

## 永続性 {#persistence}

ContextHub ストアは、コンテキストデータをクライアント上に保持します。ContextHub JavaScript API を使用してストアにアクセスし、必要に応じてデータを作成、更新および削除できます。したがって、ContextHub はページ上のデータレイヤーに相当します。

個々の ContextHub ストアは、事前定義されたストアタイプのインスタンスです。

* ContextHub には、次の機能が用意されています。 [サンプルストアタイプ](/help/sites-developing/ch-samplestores.md).
* AEMコンソールを使用して [ストアを作成](/help/sites-administering/contexthub-config.md#creating-a-contexthub-store).
* デベロッパーは、[カスタムストアタイプを作成](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)できます。
* 開発者が実行できる操作 [ストアデータにアクセス](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) JavaScript を使用。

## セグメント化 {#segmentation}

ContextHub には、セグメントを管理し、現在のコンテキストに対して解決されるセグメントを決定するセグメント化エンジンが含まれています。 複数のセグメントが定義されています。 JavaScript API を使用して、[解決されたセグメントを判断](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)できます。

## プレゼンテーション {#presentation}

マーケティング担当者と作成者は、[ContextHub ツールバー](/help/sites-authoring/ch-previewing.md)を使用してストアデータを表示および操作し、ページのオーサリング時にユーザーエクスペリエンスをシミュレートできます。ツールバーは、ContextHub ストアへのアクセスを提供する UI モジュールのグループで構成されます。

各 ContextHub UI モジュールは、事前定義されたモジュールタイプのインスタンスです。

* ContextHub には、次の機能が用意されています。 [サンプルモジュールタイプ](/help/sites-developing/ch-samplemodules.md).
* AEMコンソールを使用して [UI モジュールの追加](/help/sites-administering/contexthub-config.md#adding-a-ui-module)、および [UI モードでグループ化](/help/sites-administering/contexthub-config.md#adding-a-ui-mode).

* 開発者が実行できる操作 [カスタムモジュールタイプの作成](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

開発者は、 [ページに ContextHub コンポーネントを追加する](/help/sites-developing/ch-adding.md).
