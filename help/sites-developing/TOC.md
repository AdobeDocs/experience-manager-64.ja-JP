---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: AEM 6.4 開発ユーザーガイド
breadcrumb-title: 開発ガイド
user-guide-description: このガイドでは、AEM インスタンスの構築方法について説明します。
feature: Developing
role: Developer
hide: true
source-git-commit: b61797a9096c0473658d6aabfb584a53e42095b7
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 99%

---


# AEM 6.4 開発ユーザーガイド {#developing}

+ [開発ユーザーガイドの概要](home.md)
+ デベロッパー向けの概要{#introduction}
   + [AEM Sites の開発の手引き - WKND チュートリアル](getting-started.md)
   + [AEM の中心概念](the-basics.md)
   + [AEM タッチ操作対応 UI の構造](touch-ui-structure.md)
   + [AEM タッチ操作対応 UI の概念](touch-ui-concepts.md)
   + [AEM の開発 - ガイドラインとベストプラクティス](dev-guidelines-bestpractices.md)
   + [クライアントサイドライブラリの使用](clientlibs.md)
   + [開発とページの差分](pagediff.md)
   + [編集者の制限事項](editor-limitations.md)
   + [CSRF 対策フレームワーク](csrf-protection.md)
   + [データモデリング - David Nuescheler のモデル](model-data.md)
   + [AEM への貢献](contributing-to-cq.md)
   + [セキュリティ](security.md)
   + [参照資料](reference-materials.md)
   + [完全に機能する Web サイトの作成（クラシック UI）](website.md)
   + [デザインとデザイナー（クラシック UI）](designer.md)
+ Platform{#platform}
   + [Sling チートシート](sling-cheatsheet.md)
   + [Sling アダプターの使用](sling-adapters.md)
   + [タグライブラリ](taglib.md)
   + テンプレート{#templates}
      + [テンプレート](templates.md)
      + [ページテンプレート - 編集可能 ](page-templates-editable.md)
      + [ページテンプレート - 静的](page-templates-static.md)
      + [コンテンツフラグメントテンプレート](content-fragment-templates.md)
      + [アダプティブテンプレートレンダリング](templates-adaptive-rendering.md)
   + [AEM での Sling Resource Merger の使用](sling-resource-merger.md)
   + [オーバーレイ](overlays.md)
   + [命名規則](naming-conventions.md)
   + [新しい Granite UI フィールドコンポーネントの作成](granite-ui-component.md)
   + Query Builder{#query-builder}
      + [Query Builder 用のカスタム述語エバリュエーターの実装](implementing-custom-predicate-evaluator.md)
      + [Query Builder の述語リファレンス](querybuilder-predicate-reference.md)
      + [Query Builder API](querybuilder-api.md)
   + タグ付け{#tagging}
      + [タグ付け](tags.md)
      + [AEM タグ付けフレームワーク](framework.md)
      + [AEM アプリケーションへのタグ付けの構築](building.md)
   + [エラーハンドラーによって表示されるページのカスタマイズ](customizing-errorhandler-pages.md)
   + [カスタムノードタイプ](custom-nodetypes.md)
   + [グラフィックレンダリング用のフォントの追加](adding-fonts.md)
   + [SQL データベースへの接続](jdbc.md)
   + [URL の外部化](externalizer.md)
   + [オフロードのためのジョブの作成と使用](dev-offloading.md)
   + [Cookie の使用法の設定](cookie-optout.md)
   + [AEM JCR へのプログラムからのアクセス方法](access-jcr.md)
   + [JMX コンソールを使用したサービスの統合](jmx-integration.md)
   + [Bulk Editor の開発](dev-bulk-editor.md)
   + [レポートの開発](dev-reports.md)
   + e コマース{#ecommerce}
      + [e コマース](ecommerce.md)
      + [開発（汎用）](generic.md)
      + [SAP Commerce Cloud を使用した開発](sap-commerce-cloud.md)
+ コンポーネント{#components}
   + [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)
   + [スタイルシステム](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/siteandpage/style-system.html?lang=ja)
   + [コンポーネントの概要](components.md)
   + [AEM コンポーネント - 基本](components-basics.md)
   + [AEM コンポーネントの開発](developing-components.md)
   + [AEM コンポーネントの開発 - コードサンプル](developing-components-samples.md)
   + [コンテンツサービス用の JSON エクスポーター](json-exporter.md)
   + [コンポーネントの JSON 書き出しの有効化](json-exporter-components.md)
   + [画像エディター](image-editor.md)
   + [装飾タグ](decoration-tag.md)
   + [非表示条件の使用](hide-conditions.md)
   + [複数のインプレースエディターの設定](multiple-inplace-editors.md)
   + [開発者モード](developer-mode.md)
   + [UI のテスト](hobbes.md)
   + [コンテンツフラグメント用コンポーネント](components-content-fragments.md)
   + [JSON 形式のページ情報の取得](pageinfo.md)
   + 国際化{#internationalization}
      + [コンポーネントの国際化](i18n.md)
      + [UI 文字列の国際化](i18n-dev.md)
      + [トランスレーターを使用した辞書の管理](i18n-translator.md)
      + [翻訳のための文字列の抽出](i18n-extract.md)
   + クラシック UI コンポーネント{#classic-ui-components}
      + [AEM コンポーネントの開発（クラシック UI）](developing-components-classic.md)
      + [ウィジェットの使用および拡張（クラシック UI）](widgets.md)
      + [xtype の使用（クラシック UI）](xtypes.md)
      + [Forms の開発（クラシック UI）](developing-forms.md)
+ ヘッドレスエクスペリエンス管理{#headless}
   + [ヘッドレスおよび AEM とのハイブリッド](https://business.adobe.com/content/dam/dx/us/en/products/experience-manager/sites/headless-content-management-system/pdfs/aem-hybrid-architecture-wp-1-18-19.pdf)
   + [コンポーネントの JSON 書き出しの有効化](https://experienceleague.adobe.com/docs/experience-manager-64/developing/components/json-exporter-components.html?lang=ja)
   + 単一ページアプリケーション{#spas}
      + [SPA の概要およびガイド](spa-walkthrough.md)
      + [SPA WKND チュートリアル](spa-wknd.md)
      + [React を使用した AEM での SPA の概要](spa-getting-started-react.md)
      + [AEM での SPA の概要 - Angular](spa-getting-started-angular.md)
      + [SPA への React コンポーネントの実装 ](spa-implementing-react-component.md)
      + [SPA の詳細](spa-deep-dives.md)
      + [SPA エディターの概要](spa-overview.md)
      + [AEM 向け SPA の開発](spa-architecture.md)
      + [SPA ブループリント](spa-blueprint.md)
      + [SPA ページコンポーネント](spa-page-component.md)
      + [コンポーネントマッピングの動的モデルSPA の場合](spa-dynamic-model-to-component-mapping.md)
      + [SPA モデルルーティング](spa-routing.md)
      + [SPA と Adobe Experience Platform Launch の統合](spa-launch.md)
      + [SPA およびサーバーサイドレンダリング ](spa-ssr.md)
      + [SPA 参照資料](spa-reference-materials.md)
   + [HTTP API](https://experienceleague.adobe.com/docs/experience-manager-64/assets/extending/mac-api-assets.html?lang=ja)
   + [コンテンツフラグメント](https://experienceleague.adobe.com/docs/experience-manager-64/assets/fragments/content-fragments.html)
   + [エクスペリエンスフラグメント](https://experienceleague.adobe.com/docs/experience-manager-64/authoring/authoring/experience-fragments.html?lang=ja)
+ 開発ツール{#devtools}
   + [開発ツール](dev-tools.md)
   + [AEM モダナイゼーションツール](modernization-tools.md)
   + [ダイアログエディター](dialog-editor.md)
   + [ダイアログ変換ツール](dialog-conversion.md)
   + [CRXDE Lite による開発](developing-with-crxde-lite.md)
   + [Maven を使用したパッケージの管理](vlt-mavenplugin.md)
   + [Eclipse を使用して AEM プロジェクトを開発する方法](howto-projects-eclipse.md)
   + [Apache Maven を使用して AEM プロジェクトをビルドする方法](ht-projects-maven.md)
   + [IntelliJ IDEA を使用して AEM プロジェクトを開発する方法](ht-intellij.md)
   + [VLT ツールを使用する方法](ht-vlttool.md)
   + [プロキシサーバーツールを使用する方法](ht-proxy-server.md)
   + [AEM Brackets 拡張](aem-brackets.md)
   + [Eclipse 用 AEM 開発者ツール ](aem-eclipse.md)
   + [AEM Repo ツール](aem-repo-tool.md)
+ パーソナライズ機能{#personlization}
   + [ContextHub](contexthub.md)
   + [ContextHub JavaScript API リファレンス](contexthub-api.md)
   + [ContextHub の拡張](ch-extend.md)
   + [ページへの ContextHub の追加とストアへのアクセス](ch-adding.md)
   + [ContextHub ストア候補のサンプル](ch-samplestores.md)
   + [ContextHub UI モジュールタイプのサンプル](ch-samplemodules.md)
   + [ContextHub の診断](ch-diagnostics.md)
   + [ターゲットコンテンツの開発](target.md)
   + ClientContext{#client-context}
      + [ClientContext の詳細](client-context.md)
      + [ClientContext JavaScript API](ccjsapi.md)
+ AEM の拡張{#extending-aem}
   + [ページオーサリングのカスタマイズ](customizing-page-authoring-touch.md)
   + [コンソールのカスタマイズ](customizing-consoles-touch.md)
   + [ページプロパティのビューのカスタマイズ](page-properties-views.md)
   + [ページプロパティの一括編集のためのページの設定](bulk-editing.md)
   + [コンテンツフラグメントのカスタマイズと拡張](customizing-content-fragments.md)
   + ワークフローの拡張{#extending-workflows}
      + [ワークフローの開発と拡張](workflows.md)
      + [ワークフローモデルの作成](workflows-models.md)
      + [ワークフロー機能の拡張](workflows-customizing-extending.md)
      + [プログラムによるワークフローとのやり取り](workflows-program-interaction.md)
      + [ワークフローステップのリファレンス](workflows-step-ref.md)
      + [ワークフローのベストプラクティス](workflows-best-practices.md)
      + [ワークフロープロセスのリファレンス](workflows-process-ref.md)
   + [Multi Site Manager の拡張](extending-msm.md)
   + トラッキングと分析{#extending-analytics}
      + [イベント追跡の拡張](extending-analytics.md)
      + [コンポーネントへの Adobe Analyticsトラッキングの追加](extending-analytics-components.md)
      + [Adobe Analytics Framework のカスタマイズ](extending-analytics-framework.md)
      + [Analytics 用のサーバーサイドのページネーミングの実装](extending-analytics-pa-naming.md)
   + Cloud Services {#extending-cloud-services}
      + [クラウドサービスの設定](extending-cloud-config.md)
      + [カスタムクラウドサービスの作成](extending-cloud-config-custom-cloud.md)
   + [カスタムエクステンションの作成](extending-campaign-extensions.md)
   + Forms{#extending-forms}
      + [カスタムフォームマッピングの作成](extending-campaign-form-mapping.md)
      + [Adobe Campaign フォームコンポーネントを使用したカスタム AEM ページテンプレートの作成](extending-campaign-custom-template.md)
      + [リクエスト分析スクリプト](analyze-request.md)
   + [JMX コンソールを使用したサービスの統合](https://experienceleague.adobe.com/docs/experience-manager-64/developing/platform/jmx-integration.html?lang=ja)
   + [Bulk Editor の開発](https://experienceleague.adobe.com/docs/experience-manager-64/developing/platform/dev-bulk-editor.html?lang=ja)
   + クラシック UI の拡張{#extending-classic-ui}
      + [Web サイトコンソールのカスタマイズ（クラシック UI）](customizing-siteadmin.md)
      + [ようこそコンソールのカスタマイズ（クラシック UI）](customizing-the-welcome-console.md)
      + [レポートの開発](https://experienceleague.adobe.com/docs/experience-manager-64/developing/platform/dev-reports.html?lang=ja)
+ テスト{#testing}
   + [計画](planning.md)
   + [必要になるテスト環境の種類](test-environments.md)
   + [テストケースの定義](test-cases.md)
   + [テスト - 実行のタイミングとテスター](when-who.md)
   + [テスト計画の策定](test-plan.md)
   + [結果の追跡とフィードバックの提供](results-and-feedback.md)
   + [テストツールおよび追跡ツール](tools.md)
   + [受け入れとサインオフ](acceptance-signoff.md)
   + [次期リリース](the-next-release.md)
   + [チェックリスト](checklists.md)
   + [Tough Day](tough-day.md)
   + [UI のテスト](https://experienceleague.adobe.com/docs/experience-manager-64/developing/components/hobbes.html?lang=ja)
+ ベストプラクティス{#bestpractices}
   + [ベストプラクティスの概要](best-practices.md)
   + [AEM の開発ガイドラインとベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-64/developing/introduction/dev-guidelines-bestpractices.html?lang=ja)
   + [開発のベストプラクティス](development-practices.md)
   + [コンテンツのアーキテクチャ](content-architecture.md)
   + [ソフトウェアのアーキテクチャ](software-architecture.md)
   + We.Retail 参照実装{#we-retail}
      + [We.Retail 参照実装](we-retail.md)
      + [We.Retail のコンテンツフラグメントの使用](we-retail-content-fragments.md)
      + [We.Retail のコアコンポーネントの使用](we-retail-core-components.md)
      + [We.Retail の編集可能テンプレートの使用](we-retail-editable-templates.md)
      + [We.Retail のレスポンシブレイアウトの使用](we-retail-responsive-layout.md)
      + [We.Retail のグローバル化されたサイト構造の使用](we-retail-globalized-site-structure.md)
      + [We.Retail のコンテンツフラグメントの使用](we-retail-experience-fragments.md)
   + [コーディングのヒント](coding-tips.md)
   + [コードの落とし穴](code-pitfalls.md)
   + [OSGi バンドル](osgi-bundles.md)
   + [JCR 統合](jcr-integration.md)
   + [コードサンプル](code-samples.md)
   + [処理に時間のかかるクエリのトラブルシューティング](troubleshooting-slow-queries.md)
+ モバイル web{#mobileweb}
   + [モバイル web](mobile-web.md)
   + [デバイスグループフィルターの作成](groupfilters.md)
   + [Web ページのレスポンシブデザイン](responsive.md)
   + [モバイルデバイス用サイトの作成](mobile.md)
   + [エミュレーター](emulators.md)

<!--
Deleted link to broken helpx video:
    + [Understanding Content Fragments and Content Services in AEM](https://helpx.adobe.com/experience-manager/kt/sites/using/content-fragments-content-services-feature-video-understand.html)
-->
