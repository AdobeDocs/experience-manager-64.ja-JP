---
title: オーバーレイ
seo-title: Overlays
description: 'AEM は、オーバーレイという原理を利用して、開発者がコンソールおよびその他の機能を拡張し、カスタマイズできるようにします '
seo-description: AEM uses the principle of overlays to allow you to extend and customize the consoles and other functionality
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: c0678bb6-5e57-4ebb-b6dc-5240bafbc79e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 63%

---

# オーバーレイ{#overlays}

AEM（旧称 CQ）は、以前からオーバーレイという原理を利用して、開発者が[コンソール](/help/sites-developing/customizing-consoles-touch.md)およびその他の機能（[ページオーサリング](/help/sites-developing/customizing-page-authoring-touch.md)など）を拡張し、カスタマイズできるようにしてきました。

オーバーレイは様々なコンテキストで使用される用語です。このコンテキスト（AEM の拡張）では、オーバーレイとは、「事前定義済みの機能に対して独自の定義を強制的に付加する（標準の機能をカスタマイズする）こと」を表します。

標準インスタンスでは、事前定義された機能は `/libs` オーバーレイ（カスタマイズ）は、 `/apps` 分岐。 AEMは、検索パスを使用してリソースを検索し、最初に `/apps` 分岐してから `/libs` 分岐 ( [検索パスを設定できます](#configuring-the-search-paths)) をクリックします。 このメカニズムにより、オーバーレイ（およびそこに定義されているカスタマイズ）が優先されることになります。

AEM 6.0 以降、オーバーレイの実装方法と使用方法が次のように変更されました。

* AEM 6.0 以降 - [Granite](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/index.html) 関連のオーバーレイ（つまりタッチ操作対応 UI）

   * 方法

      * `/apps` の下に適切な `/libs` 構造を再構築します。

         1:1 コピーは不要で、 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) は、必要な元の定義を相互参照するために使用されます。 Sling Resource Merger は、差分メカニズムによってリソースにアクセスおよびマージするためのサービスを提供します。

      * 変更は `/apps` 以下で行います。
   * メリット

      * `/libs` 以下の変更に対する堅牢性が高まります。
      * 実際に必要な項目のみを再定義できます。


* Granite 以外によるオーバーレイおよび AEM 6.0 より前のバージョンでのオーバーレイ

   * メソッド

      * コンテンツのコピー元 `/libs` から `/apps`

         プロパティを含め、サブブランチ全体をコピーする必要があります。

      * 変更は `/apps` 以下で行います。
   * デメリット

      * ただし、以下で何かが変更された場合に変更内容が失われることはありません。 `/libs`の下のオーバーレイで発生する特定の変更を再作成する必要が生じる場合があります `/apps`.


>[!CAUTION]
>
>[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) および関連する手法は、[Granite](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/index.html) と併用する場合に限り使用できます。つまり、オーバーレイをスケルトン構造で作成する方法は、標準のタッチ操作対応 UI でのみ使用できます。
>
>他の領域（クラシック UI など）でのオーバーレイには、該当するノードとサブ構造全体をコピーして、必要な変更を加えます。

オーバーレイは、[コンソールの設定](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console)、[サイドパネル内にあるアセットブラウザーへの選択カテゴリの作成](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser)（ページのオーサリング時に使用）など、多くの変更において推奨される方法です。オーバーレイは、次の理由で必要になります。

* あなた ***次の値を指定する* 変更を加える `/libs` 分岐&#x200B;**このブランチは、次の操作を行うたびに変更される可能性が高いので、加えた変更はすべて失われる可能性があります。

   * インスタンス上のアップグレード
   * ホットフィックスの適用
   * 機能パックのインストール

* オーバーレイにより、変更を 1 箇所に集中させることができます。そのため、必要に応じて変更の追跡、移行、バックアップ、デバッグを実行しやすくなります。

## 検索パスの設定 {#configuring-the-search-paths}

オーバーレイの場合、配信されるリソースは、取得されたリソースとプロパティの集合体で、定義可能な以下の検索パスに応じます。

* **OSGi 設定**&#x200B;で [Apache Sling Resource Resolver Factory](/help/sites-deploying/configuring-osgi.md) 用に定義された、リソースの **Resolver Search Path**。

   * 検索パスの順序は、上から下の順で、それぞれの優先順位を示します。
   * 標準インストールでは、プライマリのデフォルトは次のようになります。 `/apps`, `/libs`  — その内容は `/apps` ～よりも優先度が高い `/libs` ( 例： *overlays* )。

* 2 人のサービスユーザーは、スクリプトが格納される場所への JCR:READ アクセス権が必要です。 次のユーザーが該当します。components-search-service (com.day.cq.wcm.coreto access/cache コンポーネントで使用 ) および sling-scripting （サーブレットを検索するために org.apache.sling.servlets.resolver で使用）。
* 次の設定も、スクリプトを配置する場所に応じて設定する必要があります（この例では、/etc、/libs または/apps の下）。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最後に、サーブレットリゾルバーも設定する必要があります（この例では/etc も追加します）。

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver  
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## 使用例 {#example-of-usage}

以下のページで、一部の例が紹介されています。

* [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)
* [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)
