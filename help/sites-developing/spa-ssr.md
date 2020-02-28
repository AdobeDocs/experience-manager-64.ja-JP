---
title: SPAとサーバ側のレンダリング
seo-title: SPAとサーバ側のレンダリング
description: 'null'
seo-description: 'null'
uuid: fbf7d0d1-865d-45d2-aeec-a7e3caf3fcb2
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: spa
content-type: reference
discoiquuid: 30d25772-0df7-468e-bcbd-c6fb2e962662
translation-type: tm+mt
source-git-commit: 2abf448e0231eb6fcd9295f498a24e81e1ead11a

---


# SPAとサーバ側のレンダリング{#spa-and-server-side-rendering}

>[!NOTE]
>シングルページアプリケーション(SPA)エディター機能を使用するには、 [AEM 6.4サービスパック2](https://helpx.adobe.com/experience-manager/6-4/release-notes/sp-release-notes.html) 以降が必要です。
>
>SPAフレームワークベースのクライアント側レンダリング（ReactやAngularなど）を必要とするプロジェクトには、SPA Editorが推奨されるソリューションです。

>[!NOTE]
>
>このドキュメントで説明するSPAサーバー側のレンダリング機能を使用するには、AEM 6.4.5.0以降が必要です。

## 概要 {#overview}

シングルページアプリ(SPA)では、ネイティブアプリケーションと同様に、使い慣れた方法で反応し、動作するリッチで動的なエクスペリエンスをユーザーに提供できます。 [これは、クライアントを利用して前方にコンテンツを読み込み、ユーザー操作の処理を大幅に短縮し](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) 、クライアントとサーバー間の通信量を最小限に抑えて、アプリの反応性を高めることで達成されます。

ただし、特にSPAが大きく、コンテンツに富む場合は、初期読み込み時間が長くなる可能性があります。 読み込み時間を最適化するために、コンテンツの一部はサーバー側でレンダリングできます。 サーバー側レンダリング(SSR)を使用すると、ページの初期読み込みを高速化し、さらにクライアント上でレンダリングを渡すことができます。

## SSRを使用するタイミング {#when-to-use-ssr}

SSRは、すべてのプロジェクトで必要とされるわけではありません。 AEMはSPAに対してJS SSRを完全にサポートしていますが、アドビでは、すべてのプロジェクトに対して体系的に実装することをお勧めしません。

SSRの導入を決定する際は、まず、SSRの追加的な複雑さ、労力、およびコストの追加が、長期保守を含む、プロジェクトに対してリアルに表現されるものを見積もる必要があります。 SSRアーキテクチャは、加算値が見積もりコストを明確に超える場合にのみ選択する必要があります。

SSRは、次の質問のいずれかに対して明確な「はい」がある場合、通常、ある程度の値を提供します。

* **** SEO:トラフィックをもたらす検索エンジンによってサイトのインデックスが正しく作成されるには、SSRが実際には必要ですか。 メインの検索エンジンクローラーがJSを評価するようになりました。
* **** ページ速度：SSRは、実生活環境における測定可能なスピードの向上を実現し、全体的なユーザーエクスペリエンスに追加しますか。

お客様のプロジェクトに対して、これら2つの質問のうち1つ以上が明確な「はい」を使用して回答された場合にのみ、アドビはSSRの実装をお勧めします。 以下の節では、Adobe I/O Runtimeを使用してこれを行う方法について説明します。

## Adobe I/Oランタイム {#adobe-io-runtime}

プロジェクト [にSSRの実装が必要であることが確実な場合は](#when-to-use-ssr)、Adobe I/O Runtimeを使用することを推奨します。

Adobe I/O Runtimeについて詳しくは、

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html) — サービスの概要
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) — プラットフォームに関する詳細なドキュメント

次の節では、Adobe I/O Runtimeを使用してSPAにSSRを実装する方法を2つの異なるモデルについて説明します。

* [AEM主導型通信フロー](#aem-driven-communication-flow)
* [Adobe I/O-Runtime駆動通信フロー](#adobe-io-driven-communication-flow)

>[!NOTE]
>
>アドビでは、AEM環境（作成者、発行、ステージなど）ごとに別々のAdobe I/Oランタイムインスタンスを使用することをお勧めします。

## リモートコンテンツレンダラーの設定 {#remote-content-renderer-configuration}

AEMは、リモートでレンダリングされたコンテンツを取得できる場所を知っている必要があります。 SSR用にどのモ [デルを実装するかに関係なく](#adobe-io-runtime)、AEMに対してこのリモートレンダリングサービスへのアクセス方法を指定する必要があります。

これは、RemoteContentRenderer - Configuration Factory **** OSGiサービスを介して行われます。 Webコンソール設定コンソール()で、「RemoteContentRenderer」という文字列を検索しま `http://<host>:<port>/system/console/configMgr`す。

![](assets/rendererconfig.png)

この設定では、次のフィールドを使用できます。

* **コンテンツパスパターン** — 必要に応じて、コンテンツの一部を一致させるための正規表現。
* **リモートエンドポイントURL** — コンテンツの生成を担当するエンドポイントのURL
   * ローカルネットワークにない場合は、保護されたHTTPSプロトコルを使用します。
* **追加のリクエストヘッダー** — リモートエンドポイントに送信されるリクエストに追加するヘッダー
   * Pattern: `key=value`
* **要求タイムアウト** — リモートホスト要求タイムアウト（ミリ秒）

>[!NOTE]
>
>[AEM駆動の通信フローや](#aem-driven-communication-flow) Adobe I/Oランタイム駆動フローを実装する場合は [](#adobe-io-driven-communication-flow)、リモートコンテンツレンダラーの設定を定義する必要があります。
>
>また、カスタムNode.jsサーバーを使用する場合は、こ [の設定を定義する必要があります](#using-node-js)。

>[!NOTE]
>
>この設定では、追加の拡張オプシ [ョンとカスタマイズオプションを使用できる](#remote-content-renderer)、リモートコンテンツレンダラーを利用します。

## AEM主導型通信フロー {#aem-driven-communication-flow}

SSRを使用する場合、AEMの [SPAのコンポーネントインタラクションワークフローに](/help/sites-developing/spa-overview.md#workflow) 、Adobe I/O Runtimeによってアプリの初期コンテンツが生成される段階が含まれます。

1. ブラウザーがAEMからSSRコンテンツを要求します。
1. AEMは、モデルをAdobe I/O Runtimeに投稿します。
1. Adobe I/O Runtimeが生成されたコンテンツを返す
1. AEMは、Adobe I/O RuntimeがバックエンドページコンポーネントのHTLテンプレートを介して返すHTMLを提供します。

![server-side-rendering-cms-drivenamenode](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

### Adobe I/Oランタイム主導型通信フロー {#adobe-io-driven-communication-flow}

「 [AEM-Driven Communication Flow](#aem-driven-communication-flow) 」では、AEMがコンテンツのブートストラップと提供を実行するAEMのSPAに関して、サーバー側レンダリングの標準的な推奨実装について説明します。

または、Adobe I/O Runtimeがブートストラップを行い、通信フローを効果的に逆にするようにSSRを実装することもできます。

両方のモデルが有効で、AEMでサポートされています。 ただし、特定のモデルを実装する前に、それぞれのメリットとデメリットを考慮する必要があります。

| ブートストラップ | メリット | デメリット |
|---|---|---|
| AEM経由 | AEMは、必要な場所でライブラリの<br>挿入を管理します。AEM上でのリソースの管理のみ必要です | SPA開発者に馴染みのない可能性がある |
| adobe I/O Runtimeを使用 | SPA開発者にとってより親しみのある方法 | CSSやJavaScriptなどのアプリケーションに必要なClientlibリソースは、AEM開発者がAEMとAdobe I/O [`allowProxy`](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)<br><br>Runtimeの間で使用可能にする必要があります。SPAのオーサリングを有効にするには、Adobe I/O Runtimeのプロキシサーバーが必要な場合があります |

## SSRの計画 {#planning-for-ssr}

通常、サーバー側でレンダリングする必要があるのはアプリケーションの一部のみです。 一般的な例は、ページの初回読み込み時に一画面に表示されるコンテンツが、サーバー側でレンダリングされる必要がある場合です。 これにより、既にレンダリングされたコンテンツをクライアントに配信することで、時間を節約できます。 ユーザーがSPAを操作すると、追加のコンテンツがクライアントによってレンダリングされます。

SPAに対してサーバー側のレンダリングを実装する場合は、SSRを必要とするアプリの部分を確認する必要があります。

## SSRを使用したSPAの開発 {#developing-an-spa-using-ssr}

SPAコンポーネントは、クライアント（ブラウザー内）またはサーバー側でレンダリングできます。 サーバー側でレンダリングする場合、ウィンドウサイズや場所などのブラウザープロパティは存在しません。 したがって、SPAコンポーネントは同形的で、レンダリングされる場所を前提としません。

SSRを利用するには、コードをAEMにデプロイするだけでなく、サーバー側のレンダリングを担当するAdobe I/O Runtimeにデプロイする必要があります。 ほとんどのコードは同じですが、サーバー固有のタスクは異なります。

## AEMのSPA用SSR {#ssr-for-spas-in-aem}

AEMのSPA用SSRにはAdobe I/O Runtimeが必要です。これは、アプリケーションコンテンツサーバー側のレンダリングに呼び出されます。 アプリケーションのHTL内で、Adobe I/O Runtime上のリソースが呼び出され、コンテンツがレンダリングされます。

AEMがAngularおよびReact SPAフレームワークをサポートするのと同様に、AngularおよびReactアプリでもサーバー側のレンダリングがサポートされます。 詳しくは、両方のフレームワークに関するNPMのドキュメントを参照してください。

* 反応：https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component [](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* 角度：https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component [](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

簡単な例については、 [We.Retail Journalアプリを参照してください](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)。 アプリケーションサーバー側全体がレンダリングされます。 これは実際の例ではありませんが、SSRの実装に必要なものを示しています。

>[!CAUTION]
>We.Retail Journalア [プリはデモ用にのみ使用されるので](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) 、推奨されるAdobe I/O Runtimeの代わりにNode.jsを単純な例として使用します。 この例は、どのプロジェクト作業にも使用しないでください。

>[!NOTE]
>AEM上のすべてのSPAプロジェクトは、SPAスターターキットの [Mavenアーキタイプに基づく必要があります](https://github.com/adobe/aem-spa-project-archetype)。

## Node.jsの使用 {#using-node-js}

AEMでSPAにSSRを実装する場合は、Adobe I/O Runtimeが推奨されるソリューションです。

オンプレミスAEMインスタンスの場合は、上記と同じ方法で、カスタムNode.jsインスタンスを使用してSSRを実装することもできます。 これはアドビでサポートされていますが、お勧めしません。

Node.jsは、アドビがホストするAEMインスタンスに対してはサポートされていません。

>[!NOTE]
>
>SSRをNode.js経由で実装する必要がある場合、アドビでは各AEM環境（作成者、発行、ステージなど）に対して個別のNode.jsインスタンスを使用することをお勧めします。

## リモートコンテンツレンダラ {#remote-content-renderer}

AEMでSSRをSPA [と共に使用するために必要なリモートコンテンツレンダラー設定は](#remote-content-renderer-configuration) 、ニーズに合わせて拡張およびカスタマイズ可能な、より一般的なレンダリングサービスにタップします。

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` は、Adobe I/Oなどのリモートサーバー上でレンダリングされたコンテンツを取得するOSGiサービスです。リモートサーバーに送信されるコンテンツは、渡されたリクエストパラメーターに基づきます。

`RemoteContentRenderingService` は、追加のコンテンツ操作が必要な場合に、カスタムSlingモデルまたはサーブレットに依存関係を反転して挿入できます。

このサービスは、RemoteContentRendererRequestHandlerServletによって内部的に使用 [されます](#remotecontentrendererrequesthandlerservlet)。

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

を使用 `RemoteContentRendererRequestHandlerServlet` して、リクエストの設定をプログラムで行うことができます。 `DefaultRemoteContentRendererRequestHandlerImpl`では、デフォルトのリクエストハンドラー実装が提供され、コンテンツ構造内の場所をリモートエンドポイントにマッピングするために、複数のOSGi設定を作成できます。

カスタムリクエストハンドラーを追加するには、インターフェイスを実装 `RemoteContentRendererRequestHandler` します。 コンポーネントのプロ `Constants.SERVICE_RANKING``DefaultRemoteContentRendererRequestHandlerImpl`パティは、100より大きい整数(

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### デフォルトハンドラのOSGi設定の設定 {#configure-default-handler}

デフォルトハンドラーの設定は、「リモートコンテンツレンダラーの設定」の節の説明に従っ [て設定する必要があります](#remote-content-renderer-configuration)。

###  リモートコンテンツレンダラーの使用 {#usage}

サーブレットが取得し、ページに挿入できるコンテンツを返すには：

1. リモートサーバーにアクセスできることを確認します。
1. AEMコンポーネントのHTLテンプレートに、次のスニペットのいずれかを追加します。
1. 必要に応じて、OSGi設定を作成または変更します。
1. サイトのコンテンツの参照

通常、ページコンポーネントのHTLテンプレートは、このような機能のメインの受信者です。

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### 要件 {#requirements}

サーブレットは、Slingモデルエクスポーターを利用してコンポーネントデータをシリアライズします。 デフォルトでは、との両方がSlingモ `com.adobe.cq.export.json.ContainerExporter` デルアダ `com.adobe.cq.export.json.ComponentExporter` プタとしてサポートされています。 必要に応じて、リクエストを使用して実装する必要のあるクラスを追 `RemoteContentRendererServlet` 加できます `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`。 追加のクラスは、を拡張する必要がありま `ComponentExporter`す。
