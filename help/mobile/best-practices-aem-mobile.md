---
title: ベストプラクティス
seo-title: Best Practices
description: このページでは、モバイルアプリのテンプレートとコンポーネントを作成する経験豊富なAEM開発者向けのベストプラクティスとガイドラインを説明します。
seo-description: Follow this page to  learn best practices and guidelines that will help experienced AEM developers for sites, who want to build mobile app templates and components.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
exl-id: 042974ee-2c0a-411d-accf-6a17b8e95f90
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 2%

---

# ベストプラクティス {#best-practices}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

AEM Mobile On-demand Servicesアプリの構築は、Cordova（または PhoneGap）シェルで直接実行するアプリの構築とは異なります。 開発者は、以下に関する知識が必要です。

* 標準でサポートされるプラグインおよびAEM Mobile固有のプラグイン。

>[!NOTE]
>
>プラグインの詳細については、次のリソースを参照してください。
>
>* [AEM Mobileでの Cordova プラグインの使用](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [AEM Mobile固有の Cordova 対応プラグインの使用](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>


* プラグイン機能を使用するテンプレートは、プラグインブリッジが存在しない状態で、ブラウザーで引き続きオーサリング可能な状態で記述する必要があります。

   * 例えば、 *deviceready* 関数を使用して、プラグインの API にアクセスしようとします。

## AEM Developers 向けガイドライン {#guidelines-for-aem-developers}

次のガイドラインは、モバイルアプリのテンプレートとコンポーネントを作成する経験豊富なAEM開発者を支援します。

**再利用と拡張性を促進するAEMサイトテンプレートを構築する**

* 1 つのモノリシックスクリプトよりも複数のコンポーネントスクリプトファイルを優先

   * 次のような空の拡張ポイントが多数提供されます。 *customheaderlibs.html* および *customfooterlibs.html*&#x200B;できるだけコアコードをほとんど複製せずに、開発者がページテンプレートを変更できるようにします。
   * その後、Sling の *sling:resourceSuperType* 機構

* テンプレート言語として JSP よりも Sightly/HTL を優先

   * この方法を使用すると、マークアップからコードを分離し、XSS 保護に組み込まれたオファーを提供し、より身近な構文を持つようになります

**デバイス上でのパフォーマンスを最適化**

* 記事固有のスクリプトとスタイルシートは、dps-article contentsync テンプレートを使用して、記事のペイロードに含める必要があります
* 複数の記事で共有されるスクリプトやスタイルシートは、 dps-HTMLResources contentsync テンプレートを使用して、共有リソースに含める必要があります
* レンダリングブロックの外部スクリプトを参照しない

>[!NOTE]
>
>レンダリングをブロックする外部スクリプトについて詳しくは、 [ここ](https://developers.google.com/speed/docs/insights/BlockingJS).

**Web 固有のライブラリよりも、アプリ固有のクライアント側 JS および CSS ライブラリを優先**

* jQuery Mobile などのライブラリで大量のデバイスやブラウザーを処理する際のオーバーヘッドを回避する
* テンプレートをアプリの Web ビューで実行する場合、アプリがサポートするプラットフォームとバージョン、および JavaScript のサポートが存在することを把握できます。 例えば、jQuery Mobile よりも Ionic （おそらく CSS のみ）、Bootstrapよりも Onsen UI の方が望ましい。

>[!NOTE]
>
>jQuery モバイルについて詳しくは、以下を参照してください： [ここ](https://jquerymobile.com/browser-support/1.4/).

**フルスタックよりもマイクロライブラリを優先**

* コンテンツをデバイスのグラスに置くのに要する時間は、記事が依存するライブラリごとに遅くなります。 新しい Web ビューを使用してすべての記事をレンダリングすると、この低速化が伴うので、各ライブラリを最初から再び初期化する必要があります
* 記事がSPA （シングルページアプリ）としてビルドされていない場合、Angularなどのフルスタックライブラリを含める必要がない可能性があります
* 小規模で単一目的のライブラリを好み、ページに必要なインタラクティビティを追加します。例： [Fastclick](https://github.com/ftlabs/fastclick) または [Velocity.js](https://velocityjs.org)

**記事のペイロードのサイズを最小化**

* サポートする最大のビューポートを効果的にカバーできる最小のアセットを、適切な解像度で使用します。
* 次のようなツールを使用 *ImageOptim* 画像上の余分なメタデータを削除します。

## 先に進む {#getting-ahead}

その他の 2 つの役割と責務について詳しくは、以下のリソースを参照してください。

* [管理者](/help/mobile/aem-mobile.md)
* [オーサー](/help/mobile/aem-mobile-on-demand.md)
