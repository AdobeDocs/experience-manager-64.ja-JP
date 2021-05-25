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
exl-id: 89e45231-885a-4d35-839b-2b50239503ad
source-git-commit: cc31f2fa2f79154749776260f7621f6631e9db4a
workflow-type: tm+mt
source-wordcount: '1781'
ht-degree: 62%

---

# SPA およびサーバーサイドレンダリング {#spa-and-server-side-rendering}

>[!NOTE]
>シングルページアプリケーション(SPA)エディター機能には、[AEM 6.4サービスパック2](https://helpx.adobe.com/jp/experience-manager/6-4/release-notes/sp-release-notes.html)以降が必要です。
>
>SPA Editorは、SPAフレームワークベースのクライアントサイドレンダリング(ReactやAngularなど)が必要なプロジェクトで推奨されるソリューションです。

>[!NOTE]
>
>このドキュメントで説明するSPAサーバー側レンダリング機能を使用するには、AEM 6.4.5.0以降が必要です。

## 概要 {#overview}

シングルページアプリケーション(SPA)では、多くの場合、ネイティブアプリケーションと同様に、使い慣れた方法で反応して動作する、リッチで動的なエクスペリエンスをユーザーに提供できます。 [これは、コンテンツを事前に読み込こんでからユーザーとのやり取りを処理するという負荷のかかる作業をクライアントにまかせることで](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work)、クライアントとサーバーの間で必要な通信量を最小限に抑え、アプリケーションの反応を良くすることで達成できます。

ただし、SPA のサイズが大きくコンテンツが豊富な場合などは、初期読み込み時間が長くなる可能性があります。読み込み時間を最適化するために、コンテンツの一部はサーバーサイドでレンダリングできます。サーバーサイドレンダリング（SSR）を使用すると、ページの初期読み込みが高速化し、その後、クライアントにさらにレンダリングを渡すことができます。

## SSR を使用するタイミング {#when-to-use-ssr}

SSR が必要なのは一部のプロジェクトだけです。AEM は SPA 向けに JS SSR を完全にサポートしていますが、すべてのプロジェクトに対して体系的に JS SSR を実装することは推奨していません。

SSR を実装することに決めたら、長期的なメンテナンスを含め、SSRを追加することがプロジェクトにとって現実的にどのような複雑さ、労力、コストをもたらすかをまず評価する必要があります。SSR アーキテクチャは、付加価値が予測コストを明確に上回る場合にのみ選択する必要があります。

次の質問のいずれかへの答えが明確に「はい」である場合、通常、SSR には価値があります。

* **SEO：**&#x200B;トラフィックをもたらす検索エンジンでサイトのインデックスを適切に作成するために SSR が実際に必要ですか。メインの検索エンジンクローラーが JS を評価するようになったことに注意してください。
* **ページ速度：** SSR によって実際の環境の速度が大幅に上がり、全体的なユーザーエクスペリエンスが向上しますか。

これらの2つの質問のうち少なくとも1つに対して明確な「はい」で回答が得られた場合にのみ、プロジェクトでSSRの実装がAdobeによって推奨されます。 次の節では、Adobe I/O Runtime を使用してこれをおこなう方法について説明します。

## Adobe I/O Runtime {#adobe-io-runtime}

プロジェクトにSSR](#when-to-use-ssr)の実装が必要であると確信できる場合は、Adobe I/O Runtimeを使用することをAdobeにお勧めします。[

Adobe I/O Runtime について詳しくは、以下を参照してください。

* [Https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) - サービスの概要
* [Https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) - プラットフォームに関する詳細なドキュメント

次の節では、2 つの異なるモデルで、SPA に SSR を実装する際に Adobe I/O Runtime を使用する方法について詳しく説明します。

* [AEM 主導の通信フロー](#aem-driven-communication-flow)
* [Adobe I/O実行時主導の通信フロー](#adobe-io-driven-communication-flow)

>[!NOTE]
>
>Adobeでは、環境（ステージング、実稼動、テストなど）ごとに個別のAdobe I/O Runtimeワークスペースを使用することをお勧めします。 これにより、異なる環境にデプロイされた単一アプリケーションの異なるバージョンを使用する、一般的なシステム開発ライフサイクル(SDLC)パターンを使用できます。 詳しくは、[CI/CD for Project Firefly Applications](https://www.adobe.io/apis/experienceplatform/project-firefly/docs.html#!AdobeDocs/project-firefly/master/guides/ci_cd_for_firefly_apps.md)のドキュメントを参照してください。
>
>インスタンスタイプごとのランタイム実装に違いがない限り、インスタンス（オーサー、パブリッシュ）ごとに個別のワークスペースは必要ありません。

## リモートコンテンツレンダラーの設定{#remote-content-renderer-configuration}

AEM は、リモートレンダリングされたコンテンツをどこで取得できるかを把握している必要があります。SSR](#adobe-io-runtime)に実装するモデル[に関係なく、このリモートレンダリングサービスへのアクセス方法をAEMに指定する必要があります。

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
>[AEM駆動の通信フロー](#aem-driven-communication-flow)と[Adobe I/O Runtime駆動のフロー](#adobe-io-driven-communication-flow)のどちらを実装するかに関係なく、リモートコンテンツレンダラー設定を定義する必要があります。
>
>また、[カスタムNode.jsサーバー](#using-node-js)を使用する場合も、この設定を定義する必要があります。

>[!NOTE]
>
>この設定では、[リモートコンテンツレンダラー](#remote-content-renderer)が利用されます。このレンダラーには、追加の拡張機能とカスタマイズオプションが用意されています。

## AEM 主導の通信フロー {#aem-driven-communication-flow}

SSRを使用する場合、AEMのSPAの[コンポーネントインタラクションワークフロー](/help/sites-developing/spa-overview.md#workflow)には、アプリの初期コンテンツがAdobe I/O Runtimeによって生成される段階が含まれます。

1. ブラウザーは AEM から SSR コンテンツを要求します。
1. AEM は、モデルを Adobe I/O Runtime に投稿します。
1. Adobe I/O Runtimeは生成されたコンテンツを返します
1. AEM は、バックエンドページコンポーネントの HTL テンプレートを介して Adobe I/O Runtime から返される HTML を提供します。

![server-side-rendering-cms-drivenaemnode](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

### Adobe I/O Runtime 主導の通信フロー {#adobe-io-driven-communication-flow}

[AEM主導の通信フロー](#aem-driven-communication-flow)の節では、AEMがブートストラップとコンテンツの提供を実行するAEMのSPAに関する、サーバーサイドレンダリングの標準的な推奨実装について説明します。

あるいは、SSR を実装して通信フローを効果的に逆転させ、Adobe I/O Runtime がブートストラップをおこなうようにすることもできます。

どちらのモデルも AEM で有効でサポートされています。ただし、特定のモデルを実装する前に、それぞれのメリットとデメリットを考慮する必要があります。

| ブートストラップ | メリット | デメリット |
|---|---|---|
| AEM 経由 | AEMは、必要に応じてライブラリの挿入を管理します。<br>リソースはAEM上でのみ維持する必要があります。 | SPA デベロッパーに馴染みのない場合がある |
| Adobe I/O Runtime 経由 | SPA デベロッパーに馴染みがある | CSSやJavaScriptなどのアプリケーションで必要なClientlibリソースは、[`allowProxy`プロパティ](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)<br>を通じてAEM開発者が利用できるようにする必要があります。AEMとAdobe I/O Runtime<br>との間でリソースを同期する必要があります。 |

## SSR の計画 {#planning-for-ssr}

通常は、アプリケーションの一部のみをサーバーサイドでレンダリングする必要があります。一般的な例としては、ページの初回読み込み時に一画面に表示されるコンテンツは、サーバーサイドでレンダリングする必要があります。 既にレンダリングされたコンテンツをクライアントに配信することで時間を節約できます。ユーザーが SPA とやり取りすると、追加のコンテンツがクライアントによってレンダリングされます。

SPAにサーバーサイドレンダリングを実装する場合は、SSRが必要なアプリの部分を確認する必要があります。

## SSR を使用した SPA の開発 {#developing-an-spa-using-ssr}

SPA コンポーネントは、クライアント（ブラウザー内）またはサーバーサイドでレンダリングできます。サーバーサイドでレンダリングすると、ウィンドウのサイズや位置などのブラウザーのプロパティは存在しません。したがって、SPA のコンポーネントは、レンダリングされる場所を前提としない、同型のものである必要があります。

SSR を活用するには、サーバーサイドレンダリングを担当する Adobe I/O Runtime だけでなく、AEM にもコードをデプロイする必要があります。ほとんどのコードは同じですが、サーバー固有のタスクは異なります。

## AEM の SPA 向け SSR {#ssr-for-spas-in-aem}

AEM の SPA 向け SSR では、Adobe I/O Runtime が必要です。これは、アプリケーションコンテンツサーバーサイドのレンダリングのために呼び出されます。アプリの HTL 内で、コンテンツをレンダリングするために Adobe I/O Runtime のリソースが呼び出されます。

AEM が標準で Angular および React SPA フレームワークをサポートするのと同様に、Angular および React アプリケーションでもサーバーサイドレンダリングがサポートされます。詳しくは、両方のフレームワークの NPM ドキュメントを参照してください。

* React:[https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular:[https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

簡単な例については、[We.Retailジャーナルアプリ](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)を参照してください。 アプリケーションサーバー側全体をレンダリングします。 これは実際の例ではありませんが、SSRの実装に何が必要かを示しています。

>[!CAUTION]
>[We.Retailジャーナルアプリ](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)はデモ目的でのみ使用され、推奨されるAdobe I/O Runtimeの代わりにNode.jsを単純な例として使用します。 この例は、どのプロジェクト作業にも使用しないでください。

>[!NOTE]
>AEM プロジェクトでは、 [AEM プロジェクトアーキタイプ](https://docs.adobe.com/content/help/ja/experience-manager-core-components/using/developing/archetype/overview.html)を活用します。このアーキタイプは、React または Angular を使用する SPA プロジェクトをサポートし、SPA SDK を活用します。

## Node.jsの使用{#using-node-js}

Adobe I/O Runtimeは、AEMでSPA用のSSRを実装する場合に推奨されるソリューションです。

オンプレミスのAEMインスタンスの場合は、上記と同じ方法で、カスタムのNode.jsインスタンスを使用してSSRを実装することもできます。 これはAdobeでサポートされていますが、お勧めしません。

Node.jsは、AdobeがホストするAEMインスタンスに対してはサポートされていません。

>[!NOTE]
>
>SSRをNode.jsを使用して実装する必要がある場合は、AEM環境（オーサー、パブリッシュ、ステージなど）ごとに個別のNode.jsインスタンスを作成することをAdobeにお勧めします。

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
