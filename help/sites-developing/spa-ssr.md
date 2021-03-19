---
title: SPA およびサーバーサイドレンダリング
seo-title: SPA およびサーバーサイドレンダリング
description: '"SPA およびサーバーサイドレンダリング"'
seo-description: 'null'
uuid: fbf7d0d1-865d-45d2-aeec-a7e3caf3fcb2
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: spa
content-type: reference
discoiquuid: 30d25772-0df7-468e-bcbd-c6fb2e962662
translation-type: tm+mt
source-git-commit: 160cc2669ac19aacdce5e96d1ba1eb4bafcb6d58
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 64%

---


# SPA およびサーバーサイドレンダリング {#spa-and-server-side-rendering}

>[!NOTE]
>シングルページアプリケーション(SPA)エディタ機能には、[AEM 6.4サービスパック2](https://helpx.adobe.com/jp/experience-manager/6-4/release-notes/sp-release-notes.html)以降が必要です。
>
>SPAフレームワークベースのクライアント側レンダリング(ReactやAngularなど)を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

>[!NOTE]
>
>SPAサーバ側のレンダリング機能を使用するには、このドキュメントで説明するようにAEM 6.4.5.0以降が必要です。

## 概要 {#overview}

シングルページアプリ(SPA)では、多くの場合ネイティブアプリケーションと同様、使い慣れた方法で反応し、動作するリッチで動的なエクスペリエンスをオファーできます。 [これは、コンテンツを事前に読み込こんでからユーザーとのやり取りを処理するという負荷のかかる作業をクライアントにまかせることで](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work)、クライアントとサーバーの間で必要な通信量を最小限に抑え、アプリケーションの反応を良くすることで達成できます。

ただし、SPA のサイズが大きくコンテンツが豊富な場合などは、初期読み込み時間が長くなる可能性があります。読み込み時間を最適化するために、コンテンツの一部はサーバーサイドでレンダリングできます。サーバーサイドレンダリング（SSR）を使用すると、ページの初期読み込みが高速化し、その後、クライアントにさらにレンダリングを渡すことができます。

## SSR を使用するタイミング {#when-to-use-ssr}

SSR が必要なのは一部のプロジェクトだけです。AEMはSPA向けにJS SSRを完全にサポートしていますが、Adobeは、すべてのプロジェクトに対して体系的にJS SSRを実装することをお勧めしません。

SSR を実装することに決めたら、長期的なメンテナンスを含め、SSRを追加することがプロジェクトにとって現実的にどのような複雑さ、労力、コストをもたらすかをまず評価する必要があります。SSR アーキテクチャは、付加価値が予測コストを明確に上回る場合にのみ選択する必要があります。

次の質問のいずれかへの答えが明確に「はい」である場合、通常、SSR には価値があります。

* **SEO：**&#x200B;トラフィックをもたらす検索エンジンでサイトのインデックスを適切に作成するために SSR が実際に必要ですか。メインの検索エンジンクローラーが JS を評価するようになったことに注意してください。
* **ページ速度：** SSR によって実際の環境の速度が大幅に上がり、全体的なユーザーエクスペリエンスが向上しますか。

この2つの質問のうち少なくとも1つに対して明確な「はい」を付けて回答がなされた場合に限り、AdobeはSSRの実装を推奨します。 次の節では、Adobe I/O Runtime を使用してこれをおこなう方法について説明します。

## Adobe I/O Runtime {#adobe-io-runtime}

プロジェクトにSSR](#when-to-use-ssr)の実装が必要であると確信している場合、Adobeが推奨するソリューションはAdobe I/O Runtimeを使用することです。[

Adobe I/O Runtime について詳しくは、以下を参照してください。

* [Https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) - サービスの概要
* [Https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) - プラットフォームに関する詳細なドキュメント

次の節では、2 つの異なるモデルで、SPA に SSR を実装する際に Adobe I/O Runtime を使用する方法について詳しく説明します。

* [AEM 主導の通信フロー](#aem-driven-communication-flow)
* [Adobe I/O・ランタイム主導型通信フロー](#adobe-io-driven-communication-flow)

>[!NOTE]
>
>AEM 環境（オーサー、パブリッシュ、ステージなど）ごとに個別の Adobe I/O Runtime インスタンスを作成することをお勧めします。

## リモートコンテンツレンダラーの設定{#remote-content-renderer-configuration}

AEM は、リモートレンダリングされたコンテンツをどこで取得できるかを把握している必要があります。[SSR](#adobe-io-runtime)にどのモデルを実装するかに関係なく、AEMに対してこのリモートレンダリングサービスへのアクセス方法を指定する必要があります。

これは、**** RemoteContentRenderer - Configuration Factory OSGi サービスを介しておこなわれます。`http://<host>:<port>/system/console/configMgr` の Web コンソール設定コンソールで、文字列「RemoteContentRenderer」を検索します。

![](assets/rendererconfig.png)

この設定では、次のフィールドを使用できます。

* **コンテンツパスパターン** - 必要に応じて、コンテンツの一部を一致させるための正規表現。
* **リモートエンドポイント URL** - コンテンツの生成を担当するエンドポイントの URL。
   * ローカルネットワークにない場合は、保護された HTTPS プロトコルを使用します。
* **追加の要求ヘッダー** - リモートエンドポイントに送信される要求に追加するヘッダー。
   * パターン：`key=value`
* **要求タイムアウト** - リモートホスト要求のタイムアウト（ミリ秒）。

>[!NOTE]
>
>[AEM駆動の通信フロー](#aem-driven-communication-flow)や[Adobe I/O Runtime駆動のフロー](#adobe-io-driven-communication-flow)を実装する場合には、リモートコンテンツレンダラーの設定を定義する必要があります。
>
>また、カスタムNode.jsサーバ](#using-node-js)を[使用する場合は、この設定も定義する必要があります。

>[!NOTE]
>
>この設定では、[リモートコンテンツレンダラー](#remote-content-renderer)が利用されます。このレンダラーには、追加の拡張機能とカスタマイズ機能が用意されています。

## AEM 主導の通信フロー {#aem-driven-communication-flow}

SSRを使用する場合、AEMのSPAの[コンポーネントの対話ワークフロー](/help/sites-developing/spa-overview.md#workflow)には、Adobe I/O Runtimeによってアプリの初期コンテンツが生成される段階が含まれます。

1. ブラウザーは AEM から SSR コンテンツを要求します。
1. AEM は、モデルを Adobe I/O Runtime に投稿します。
1. Adobe I/O Runtimeは生成された内容を返す
1. AEM は、バックエンドページコンポーネントの HTL テンプレートを介して Adobe I/O Runtime から返される HTML を提供します。

![server-side-rendering-cms-drivenaemnode](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

### Adobe I/O Runtime 主導の通信フロー {#adobe-io-driven-communication-flow}

[AEM駆動通信フロー](#aem-driven-communication-flow)の節では、AEMがコンテンツのブートストラップと提供を行うSPAに関するサーバ側レンダリングの標準および推奨実装について説明します。

あるいは、SSR を実装して通信フローを効果的に逆転させ、Adobe I/O Runtime がブートストラップをおこなうようにすることもできます。

どちらのモデルも AEM で有効でサポートされています。ただし、特定のモデルを実装する前に、それぞれのメリットとデメリットを考慮する必要があります。

| ブートストラップ | メリット | デメリット |
|---|---|---|
| AEM 経由 | AEMは、必要な場所でライブラリの挿入を管理<br>リソースの管理のみがAEMで必要 | SPA デベロッパーに馴染みのない場合がある |
| Adobe I/O Runtime 経由 | SPA デベロッパーに馴染みがある | CSSやJavaScriptなどのアプリケーションに必要なClientlibリソースは、AEM開発者が[`allowProxy`プロパティ](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)<br>ResourcesをAEMとAdobe I/O Runtime<br>の間で同期する必要があります。SPAのオーサリングを有効にするには、Adobe I/O Runtimeのプロキシサーバーが必要な場合があります |

## SSR の計画 {#planning-for-ssr}

通常は、アプリケーションの一部のみをサーバーサイドでレンダリングする必要があります。一般的な例は、ページの初回読み込み時に、サーバー側でレンダリングする必要があるコンテンツが1画面に表示される場合です。 既にレンダリングされたコンテンツをクライアントに配信することで時間を節約できます。ユーザーが SPA とやり取りすると、追加のコンテンツがクライアントによってレンダリングされます。

SPAに対してサーバー側のレンダリングを実装する場合は、SSRが必要となるアプリの部分を確認する必要があります。

## SSR を使用した SPA の開発 {#developing-an-spa-using-ssr}

SPA コンポーネントは、クライアント（ブラウザー内）またはサーバーサイドでレンダリングできます。サーバーサイドでレンダリングすると、ウィンドウのサイズや位置などのブラウザーのプロパティは存在しません。したがって、SPA のコンポーネントは、レンダリングされる場所を前提としない、同型のものである必要があります。

SSR を活用するには、サーバーサイドレンダリングを担当する Adobe I/O Runtime だけでなく、AEM にもコードをデプロイする必要があります。ほとんどのコードは同じですが、サーバー固有のタスクは異なります。

## AEM の SPA 向け SSR {#ssr-for-spas-in-aem}

AEM の SPA 向け SSR では、Adobe I/O Runtime が必要です。これは、アプリケーションコンテンツサーバーサイドのレンダリングのために呼び出されます。アプリの HTL 内で、コンテンツをレンダリングするために Adobe I/O Runtime のリソースが呼び出されます。

AEM が標準で Angular および React SPA フレームワークをサポートするのと同様に、Angular および React アプリケーションでもサーバーサイドレンダリングがサポートされます。詳しくは、両方のフレームワークの NPM ドキュメントを参照してください。

* 反応：[https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular:[https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

単純な例については、[We.Retailジャーナルアプリ](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)を参照してください。 アプリケーションサーバー側全体がレンダリングされます。 これは実際の例ではありませんが、SSRの実装に必要なものを示しています。

>[!CAUTION]
>[We.Retailジャーナルアプリ](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)はデモ目的でのみ使用されるので、推奨されるAdobe I/O Runtimeの代わりにNode.jsを単純な例として使用します。 この例は、どのプロジェクト作業にも使用しないでください。

>[!NOTE]
>AEM プロジェクトでは、 [AEM プロジェクトアーキタイプ](https://docs.adobe.com/content/help/ja/experience-manager-core-components/using/developing/archetype/overview.html)を活用します。このアーキタイプは、React または Angular を使用する SPA プロジェクトをサポートし、SPA SDK を活用します。

## Node.jsの使用{#using-node-js}

Adobe I/O Runtimeは、AEMでSPAにSSRを実装する場合に推奨されるソリューションです。

オンプレミスAEMインスタンスの場合は、上記と同様に、カスタムNode.jsインスタンスを使用してSSRを実装することもできます。 これはAdobeでサポートされていますが、お勧めしません。

Node.jsは、AdobeがホストするAEMインスタンスではサポートされていません。

>[!NOTE]
>
>SSRをNode.js経由で実装する必要がある場合、AdobeではAEM環境（作成者、発行、ステージなど）ごとに個別のNode.jsインスタンスを推奨します。

## リモートコンテンツレンダラー {#remote-content-renderer}

AEM で SSR を SPA と使用するために必要な[リモートコンテンツレンダラー設定](#remote-content-renderer-configuration)は、ニーズに合わせて拡張およびカスタマイズできる、より一般化されたレンダリングサービスです。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` は、Adobe I/O からなど、リモートサーバーでレンダリングされるコンテンツを取得する OSGi サービスです。リモートサーバーに送信されるコンテンツは、渡されたリクエストパラメーターに基づきます。

`RemoteContentRenderingService` は、追加のコンテンツ操作が必要な場合に、カスタム Sling モデルまたはサーブレットに依存関係を反転してインジェクトできます。

このサービスは、[RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet) によって内部的に使用されます。

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

`RemoteContentRendererRequestHandlerServlet` を使用して、要求の設定をプログラムで作成できます。`DefaultRemoteContentRendererRequestHandlerImpl` では、デフォルトのリクエストハンドラーの実装が提供されており、コンテンツ構造内の場所をリモートエンドポイントにマップするために、複数の OSGi 設定を作成できます。

カスタム要求ハンドラーを追加するには、`RemoteContentRendererRequestHandler` インターフェイスを実装します。`Constants.SERVICE_RANKING` コンポーネントプロパティは、100（`DefaultRemoteContentRendererRequestHandlerImpl` のランク）より大きい整数に設定してください。

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### デフォルトハンドラーの OSGi 設定の作成 {#configure-default-handler}

デフォルトハンドラーの設定は、「[リモートコンテンツレンダラーの設定](#remote-content-renderer-configuration)」の説明に従って作成する必要があります。

###  リモートコンテンツレンダラーの使用 {#usage}

サーブレットがページにインジェクト可能なコンテンツを取得して返すには、以下をおこないます。

1. リモートサーバーがアクセス可能であることを確認します。
1. AEM コンポーネントの HTL テンプレートに次のスニペットのいずれかを追加します。
1. 必要に応じて、OSGi 設定を作成または変更します。
1. サイトコンテンツの参照

通常、ページコンポーネントの HTL テンプレートは、この機能のメイン受信者です。

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要件 {#requirements}

このサーブレットでは、Sling モデルエクスポーターを活用してコンポーネントデータをシリアライズします。デフォルトでは、`com.adobe.cq.export.json.ContainerExporter` および `com.adobe.cq.export.json.ComponentExporter` の両方が Sling モデルアダプターとしてサポートされています。必要に応じて、`RemoteContentRendererServlet` を使用して `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses` を実装するように要求を適合させる必要があるクラスを追加できます。追加のクラスは、`ComponentExporter` を拡張する必要があります。
