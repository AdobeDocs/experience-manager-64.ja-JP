---
title: SPA エディターの概要
seo-title: SPA Editor Overview
description: この記事では、SPA エディターの包括的な概要と動作の仕組み（AEM 内での SPA エディターの詳細なインタラクションワークフローなど）を説明します。
seo-description: This article gives a comprehensive overview of the SPA Editor and how it works included detailed workflows of interaction of the SPA Editor within AEM.
uuid: 600f1100-5cfa-4b75-a58c-f773395b5e05
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: spa
content-type: reference
discoiquuid: 897ff73f-15a5-484f-a3a2-616de8ac59dc
exl-id: 5145b6ab-588a-458f-946f-b730ae319f61
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 78%

---

# SPA エディターの概要{#spa-editor-overview}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

単一ページアプリケーション（SPA）により、Web サイトのユーザーに魅力的なエクスペリエンスを提供することができます。開発者はSPAフレームワークを使用してサイトを構築できるようにしたいと考え、作成者は、そのようなフレームワークを使用して構築されたサイトのコンテンツをAEM内でシームレスに編集したいと考えています。

SPA エディターには、AEM 内で SPA をサポートするための包括的なソリューションが用意されています。このページでは、AEMでのSPAサポートの構造と、SPAエディターの仕組み、SPAフレームワークとAEMの同期の仕組みの概要を説明します。

>[!NOTE]
>
>シングルページアプリケーション (SPA) エディター機能には、 [AEM 6.4 service pack 2](/help/release-notes/sp-release-notes.md) 以降
>
>SPA エディターは、SPA フレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトで有効なソリューションです。

## はじめに {#introduction}

React やAngularなどの一般的なSPAフレームワークを使用して構築されたサイトは、動的 JSON を介してコンテンツを読み込むので、AEMページエディターで編集コントロールを配置するために必要なHTML構造は提供されません。

AEM 内で SPA の編集を有効にするには、SPA の JSON 出力と AEM リポジトリーのコンテンツモデルとの間でマッピングを行い、変更をコンテンツに保存できるようにする必要があります。

AEMでのSPAのサポートには、イベントの送信に使用できるページエディターに読み込まれる際にSPA JS コードとやり取りするシン JS レイヤーが導入され、編集コントロールの場所をアクティブにして、コンテキスト内編集が可能になります。 この機能は、SPAのコンテンツを Content Services 経由で読み込む必要があるので、Content Services API エンドポイントの概念に基づいて構築されます。

AEMでのSPAについて詳しくは、次のドキュメントを参照してください。

* [SPA Blueprint](/help/sites-developing/spa-blueprint.md) SPAの技術要件
* シンプルな SPA のクイックツアーについては、[AEM での SPA 仕様の手引き](/help/sites-developing/spa-getting-started-react.md)を参照してください。

## デザイン {#design}

SPAのページコンポーネントは、JSP ファイルまたは HTL ファイルを介して子コンポーネントのHTML要素を提供しません。 この処理は SPA フレームワークに委任されます。子コンポーネントまたはモデルの表現は、JCR から JSON データ構造として取得されます。次に、その構造に従ってSPAコンポーネントがページに追加されます。 この動作は、ページコンポーネントの初期本文の構成をSPA以外の対応するものと区別します。

### ページモデルの管理  {#page-model-management}

ページモデルの解決と管理は、指定の `PageModel` ライブラリに委任されます。SPA エディターで初期化とオーサリングを行うには、SPA でこのページモデルライブラリを使用する必要があります。このページモデルライブラリは、`aem-react-editable-components` npm によって AEM のページコンポーネントに間接的に提供されます。ページモデルは、AEM と SPA 間のインタープリターであるので、常に存在している必要があります。ページを作成したら、ページエディターとの通信を可能にするために、`cq.authoring.pagemodel.messaging` ライブラリを追加する必要があります。

SPA ページのコンポーネントがページのコアコンポーネントから継承される場合、`cq.authoring.pagemodel.messaging` クライアントライブラリのカテゴリを使用可能にするオプションが 2 つあります。

* テンプレートが編集可能な場合、テンプレートをページポリシーに追加する。
* `customfooterlibs.html` を使用して、カテゴリを追加する。

書き出されたモデル内の各リソースに対して、SPAは、\
レンダリング。 JSON 形式で表現されたモデルは、コンテナ内のコンポーネントマッピングを使用してレンダリングされます。\
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>`cq.authoring.pagemodel.messaging` カテゴリの追加は、SPA エディターのコンテキストに限定する必要があります。

### 通信データタイプ {#communication-data-type}

`cq.authoring.pagemodel.messaging` カテゴリがページに追加されると、ページエディターにメッセージが送信され、JSON 通信データタイプが確立されます。通信データタイプが JSON に設定されると、GET リクエストにより、コンポーネントの Sling Model エンドポイントとの通信が行われます。ページエディターで更新が実行されると、更新されたコンポーネントの JSON 表現がページモデルのライブラリに送信されます。次に、ページモデルライブラリが、SPAに更新を通知します。

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## ワークフロー {#workflow}

SPA と AEM 間のインタラクションのフローは、SPA エディターが両者の仲介役になっていると考えると理解することができます。

* ページエディターと SPA 間の通信は、HTML ではなく JSON を使用して行われます。
* ページエディターは、iframe およびメッセージング API を使用して、SPAにページモデルの最新バージョンを提供します。
* ページモデルマネージャーがエディターに通知します。ページモデルは編集の準備が整い、JSON 構造として渡されます。
* エディターは、作成しているページの DOM 構造を変更したり、アクセスしたりすることなく、最新のページモデルを提供します。

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### SPA エディターの基本的なワークフロー {#basic-spa-editor-workflow}

SPA エディターの主な要素に留意すると、AEM 内での SPA 編集の高度なワークフローは、作成者の観点では次のようになります。

![untitled1](assets/untitled1.gif)

1. SPA エディターが読み込まれます。

1. SPA が別個のフレームに読み込まれます。
1. SPA が JSON コンテンツを要求し、コンポーネントをクライアント側でレンダリングします。
1. SPA エディターが、レンダリングされたコンポーネントを検出し、オーバーレイを生成します。
1. 作成者がオーバーレイをクリックし、コンポーネントの編集ツールバーを表示します。
1. SPA エディターが、サーバーへの POST リクエストを使用して編集内容を保存します。
1. SPA エディターが、更新された JSON を要求します。これは DOM イベントで SPA に送信されます。
1. SPA が、関係するコンポーネントを再レンダリングし、DOM を更新します。

>[!NOTE]
>
>次の点に注意してください。
>
>* SPA は常にその表示を担当している
>* SPA エディターは SPA 自体から切り離されている
>* 実稼働環境（パブリッシュ）では SPA エディターは読み込まれない
>


### クライアントサーバーのページ編集ワークフロー {#client-server-page-editing-workflow}

下図は、SPA を編集する際のクライアントとサーバーのインタラクションの概要をより詳しく説明したものです。

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. SPA がそれ自体を初期化し、Sling Model Exporter にあるページモデルをリクエストします。

1. Sling Model Exporter がリポジトリーに、ページを構成するリソースをリクエストします。

1. リポジトリーがリソースを返します。

1. Sling Model Exporter がページのモデルを返します。

1. SPA がページモデルに基づいてコンポーネントをインスタンス化します。

1. **6a** コンテンツがエディターに、オーサリングの準備ができたことを通知します。

   **6b** ページエディターがコンポーネントオーサリング設定を要求します。

   **6c** ページエディターがコンポーネント設定を受け取ります。

1. 作成者がコンポーネントを編集すると、ページエディターがデフォルトの POST サーブレットに変更リクエストをポストします。

1. リソースがリポジトリーで更新されます。

1. 更新されたリソースが POST サーブレットに提供されます。

1. デフォルトの POST サーブレットがページエディターに、リソースが更新されたことを通知します。

1. ページエディターが新しいページモデルをリクエストします。

1. （リポジトリーにある）ページを構成するリソースが、リクエストされます。

1. ページを構成するリソースが、リポジトリーから Sling Model Exporter に提供されます。

1. 更新されたページモデルがエディターに返されます。

1. ページエディターが SPA のページモデル参照を更新します。

1. SPA が新しいページモデル参照に基づいてコンポーネントを更新します。

1. ページエディターのコンポーネント設定が更新されます。

   **17a** SPA がページエディターに、コンテンツの準備ができたことを通知します。

   **17b** ページエディターが SPA にコンポーネント設定を提供します。

   **17c** SPA が、更新されたコンポーネント設定を提供します。

### オーサリングワークフロー {#authoring-workflow}

下図は、オーサリングエクスペリエンスに重点を置いた、より詳細な概要です。

![spa_content_authoringmodel](assets/spa_content_authoringmodel.png)

1. SPA がページモデルを取得します。

1. **2A** ページモデルがエディターに、オーサリングに必要なデータを提供します。

   **2b** 通知を受けると、コンポーネントオーケストレーターがページのコンテンツ構造を更新します。

1. コンポーネントオーケストレーターが、AEM リソースタイプと SPA コンポーネントの間のマッピングについて問い合わせます。

1. コンポーネントオーケストレーターが、ページモデルとコンポーネントマッピングに基づいて、SPA コンポーネントを動的にインスタンス化します。

1. ページエディターがページモデルを更新します。

1. **6a** ページモデルがページエディターに、更新されたオーサリングデータを提供します。

   **6b** ページモデルがコンポーネントオーケストレーターに変更を発行します。

1. コンポーネントオーケストレーターがコンポーネントマッピングを取得します。

1. コンポーネントオーケストレーターがページのコンテンツを更新します。

1. SPA がページコンテンツの更新を完了すると、ページエディターがオーサリング環境を読み込みます。

## 要件と制限事項 {#requirements-limitations}

作成者がページエディターを使用して SPA のコンテンツを編集できるようにするには、AEM SPA Editor SDK とやり取りする SPA アプリケーションを実装する必要があります。動作させるために必要な基本的な知識については、[AEM での SPA の概要](/help/sites-developing/spa-getting-started-react.md)を参照してください。

### サポートされているフレームワーク {#supported-frameworks}

SPA Editor SDK では、最低限、次のバージョンをサポートしています。

* React 16.x 以上
* Angular 6.x 以上

これらのフレームワークの旧バージョンは、AEM SPA Editor SDK で動作する可能性はありますが、サポートされていません。

### その他のフレームワーク {#additional-frameworks}

AEM SPA Editor SDK で動作する他の SPA フレームワークを追加で実装することができます。AEM SPA エディターで動作するモジュール、コンポーネント、サービスで構成されるフレームワーク固有のレイヤーを作成するためにフレームワークが満たすべき要件については、[SPA ブループリント](/help/sites-developing/spa-blueprint.md)ドキュメントを参照してください。

### 複数のセレクターの使用 {#multiple-selectors}

カスタムセレクターの定義を追加すると、AEM SPA SDK 用に開発された SPA の一部として使用することができます。ただし、これをサポートするには、`model` セレクターを最初のセレクターにし、[JSON Exporter の要件](json-exporter-components.md#multiple-selectors)に応じて拡張子を `.json` にする必要があります。

### テキストエディターの要件 {#text-editor-requirements}

SPA で作成したテキストコンポーネントのインプレースエディタを使用する場合は、追加の設定が必要です。

1. テキスト HTML を含んだコンテナラッパー要素に（任意の）属性を設定します。WKND Journal サンプルコンテンツでは、`<div>` 要素がこれに該当し、`data-rte-editelement` がセレクターとして使用されています。
1. 対応する AEM テキストコンポーネントの `cq:InplaceEditingConfig` で、そのセレクター（例：`data-rte-editelement` など）を指す設定 `editElementQuery` を指定します。これにより、HTML テキストを折り返す HTML 要素をエディターが把握できます。

この処理の例については、[WKND Journal サンプルコンテンツ](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)を参照してください。

`editElementQuery` プロパティとリッチテキストエディターの設定について詳しくは、[リッチテキストエディターの設定](/help/sites-administering/rich-text-editor.md)を参照してください。

### 制限事項 {#limitations}

AEM SPA Editor SDK は、AEM 6.4 サービスパック 2 で導入されました。AEM SPA Editor SDK はアドビで完全にサポートされており、新機能として機能強化と拡張が続けられています。次のAEM機能は、SPA Editor ではまだ対応していません。

* ターゲットモード
* ContextHub
* インライン画像編集
* 設定の編集（例：リスナー）
* スタイルシステム
* 取り消し／やり直し
* ページの差分とタイムワープ
* リンクチェッカー、CDN 書き直しサービス、URL 短縮など、サーバー側で HTML の書き換えを実行する機能
* 開発者モード
* AEM ローンチ
