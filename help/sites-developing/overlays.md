---
title: オーバーレイ
seo-title: Overlays
description: AEM は、オーバーレイという原理を利用して、コンソールおよびその他の機能を拡張し、カスタマイズできるようにします
seo-description: AEM uses the principle of overlays to allow you to extend and customize the consoles and other functionality
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: c0678bb6-5e57-4ebb-b6dc-5240bafbc79e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 65%

---

# オーバーレイ{#overlays}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM（以前は、CQ）は、オーバーレイの原則を使用して、 [コンソール](/help/sites-developing/customizing-consoles-touch.md) その他の機能 ( 例： [ページオーサリング](/help/sites-developing/customizing-page-authoring-touch.md)) をクリックします。

オーバーレイは様々なコンテキストで使用される用語です。このコンテキスト (AEMの拡張 ) では、オーバーレイとは、事前定義された機能に対して独自の定義を強制的に付加する（標準の機能をカスタマイズする）ことを意味します。

標準インスタンスでは、事前定義された機能は `/libs` 以下に置かれるので、オーバーレイ（カスタマイズ）は `/apps` ブランチ以下に定義することが推奨されます。AEM がリソースを検索するときは検索パスを使用します。具体的には、最初に `/apps` ブランチを検索し、次に `/libs` ブランチを検索します（[検索パスは必要に応じて設定可能](#configuring-the-search-paths)）。このメカニズムにより、オーバーレイ（およびそこに定義されているカスタマイズ）が優先されます。

AEM 6.0 以降、オーバーレイの実装方法と使用方法が変更されました。

* AEM 6.0 以降 - [Granite](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/index.html) 関連のオーバーレイ（つまりタッチ操作対応 UI）

   * 方法

      * `/apps` の下に適切な `/libs` 構造を再構築します。

         これには 1:1 のコピーは不要です。[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) は、必要な元の定義を相互参照するために使用されるからです。Sling Resource Merger は、差分メカニズムによってリソースにアクセスおよびマージするためのサービスを提供します。

      * 変更は `/apps` 以下で行います。
   * メリット

      * `/libs` 以下の変更に対する堅牢性が高まります。
      * 実際に必要な項目のみを再定義できます。


* Granite 以外によるオーバーレイおよび AEM 6.0 より前のバージョンでのオーバーレイ

   * メソッド

      * コンテンツを `/libs` から `/apps` にコピーします。

         プロパティを含むサブブランチ全体をコピーする必要があります。

      * 変更は `/apps` 以下で行います。
   * デメリット

      * `/libs` 以下で変更しても変更内容は失われませんが、`/apps` 以下のオーバーレイでは一部の変更作業をやり直す必要がある場合があります。


>[!CAUTION]
>
>[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) および関連する手法は、[Granite](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/index.html) と併用する場合に限り使用できます。つまり、スケルトン構造を持つオーバーレイの作成は、標準のタッチ操作対応 UI にのみ適しています。
>
>他の領域（クラシック UI を含む）のオーバーレイでは、適切なノードとサブ構造全体をコピーし、必要な変更を行います。

オーバーレイは、[コンソールの設定](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console)、[サイドパネル内にあるアセットブラウザーへの選択カテゴリの作成](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser)（ページのオーサリング時に使用）など、多くの変更において推奨される方法です。オーバーレイは、次の理由で必要になります。

* `/libs`ブランチ&#x200B;**では&#x200B;***変更しないでください*。
このブランチは次のように常に変更される可能性があるため、変更内容が失われる可能性があります。

   * インスタンスにアップグレードします
   * ホットフィックスの適用
   * 機能パックをインストールする

* オーバーレイにより、変更を 1 箇所に集中させることができます。そのため、必要に応じて変更の追跡、移行、バックアップ、デバッグを実行しやすくなります。

## 検索パスの設定 {#configuring-the-search-paths}

オーバーレイの場合、配信されるリソースは、取得されたリソースとプロパティの集計で、定義可能な検索パスに応じて表されます。

* リソース **Resolver Search Path** ( [OSGi 設定](/help/sites-deploying/configuring-osgi.md) の **Apache Sling Resource Resolver Factory**.

   * 検索パスの上から下に並ぶ順序は、それぞれの優先度を示します。
   * 標準インストールの場合、主なデフォルトは `/apps` と `/libs` で、`/apps` のコンテンツの方が `/libs` のコンテンツより優先されます（つまり、前者が後者を&#x200B;*オーバーレイ*&#x200B;します）。

* スクリプトの保存場所への JCR:READ アクセス権を 2 人のサービスユーザーに付与する必要があります。この 2 人のユーザーは、components-search-service（com.day.cq.wcm.core でコンポーネントのアクセス／キャッシュに使用）と sling-scripting（org.apache.sling.servlets.resolver でサーブレットの検索に使用）です。
* 次の設定も、スクリプトの保存場所に応じて設定する必要があります（この例では /etc、/libs または /apps の下）。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最後に、Servlet Resolver を設定する必要もあります（この例では /etc も追加します）。

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver  
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## 使用例 {#example-of-usage}

以下に例を示します。

* [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)
* [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)
