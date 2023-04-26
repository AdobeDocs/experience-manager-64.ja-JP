---
title: 開発者モード
seo-title: Developer Mode
description: デベロッパーモードでは、いくつかのタブを持つサイドパネルが開き、現在のページに関する情報をデベロッパーに提供します
seo-description: Developer mode opens a side panel with several tabs that provide a developer with infomation about the current page
uuid: 2ff0d85e-fe49-4506-b6d6-74cc060d7ea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: components
content-type: reference
discoiquuid: efbe46a3-c37f-4b67-8b3a-188cfc75118b
exl-id: 733eddf1-48f9-45c2-a1b4-138cf32b4b59
source-git-commit: 51358642a2fa8f59f3f5e3996b0c37269632c4cb
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 47%

---

# 開発者モード{#developer-mode}

AEMでページを編集する場合、複数の [モード](/help/sites-authoring/author-environment-tools.md#page-modes) は、開発者モードを含めて使用できます。 これにより、いくつかのタブを持つサイドパネルが開き、現在のページに関する情報を開発者が提供します。 次の 3 つのタブがあります。

* **[コンポーネント](#components)** を参照してください。
* **[テスト](#tests)** テストを実行し、結果を分析する場合。
* **[エラー](#errors)** をクリックして、発生している問題を確認します。

これらのタブで、開発者は以下を実行できます。

* 検出：ページの構成要素
* デバッグ：発生したエラーとその場所およびタイミングを特定して、問題の修正に役立てます。
* テスト：アプリケーションが期待どおりに動作するかを示します。

>[!CAUTION]
>
>開発者モード：
>
>* （ページの編集時に）タッチ操作対応 UI でのみ使用できます。
>* モバイルデバイスまたはデスクトップ上の小さいウィンドウでは、スペースの制約があるので使用できません。
   >   * ウィンドウの幅が 1024 px 未満の場合は使用できません。
>* `administrators` グループに所属しているユーザーのみ使用できます。


>[!CAUTION]
>
>開発者モードは、nosamplecontent 実行モードを使用していない標準のオーサーインスタンスでのみ使用できます。
>
>必要に応じて、次のように設定して使用できます。
>
>* nosamplecontent 実行モードを使用しているオーサーインスタンス
>* パブリッシュインスタンス
>
>使用後は再度無効にする必要があります。

>[!NOTE]
>
>詳しくは以下を参照してください。
>
>* ナレッジベース記事、 [AEM TouchUI の問題のトラブルシューティング](https://helpx.adobe.com/jp/experience-manager/kb/troubleshooting-aem-touchui-issues.html)（その他のヒントとツールについて）
>* AEM Gems セッションの概要 [AEM 6.0 開発者モード](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html).


## 開発者モードを開く {#opening-developer-mode}

開発者モードは、ページエディターのサイドパネルとして実装されます。 パネルを開くには、ページエディターのツールバーにあるモードセレクターから「**開発者**」を選択します。

![chlimage_1-229](assets/chlimage_1-229.png)

パネルは、次の 2 つのタブで構成されています。

* **[コンポーネント](/help/sites-developing/developer-mode.md#components)** - コンポーネントツリーが表示されます。これは、作成者向けの[コンテンツツリー](/help/sites-authoring/author-environment-tools.md#content-tree)に似ています。

* **[エラー](/help/sites-developing/developer-mode.md#errors)** - 問題が発生すると、各コンポーネントの詳細が表示されます。

### コンポーネント {#components}

![chlimage_1-230](assets/chlimage_1-230.png)

コンポーネントツリーが表示されます。次の機能があります。

* ページ上にレンダリングされるコンポーネントとテンプレートのチェーンの概要を示します（SLY、JSP など）。このツリーを展開して、階層内のコンテキストを表示できます。
* コンポーネントのレンダリングに必要なサーバー側の計算時間を示します。
* ツリーを展開し、ツリー内の特定のコンポーネントを選択できます。 「選択」を選択すると、コンポーネントの詳細にアクセスできます。例：

   * リポジトリーパス
   * スクリプトへのリンク (CRXDE Lite)

* コンテンツフロー内で選択されたコンポーネント（青い境界線で示される）がコンテンツツリー内でハイライト表示されます（その逆も同様です）。

これは次の目的に役立ちます。

* コンポーネントごとのレンダリング時間を判断し、比較します。
* 階層を確認し、理解します。
* 時間がかかっているコンポーネントを把握することで、ページの読み込み時間について理解し、向上させます。

各コンポーネントエントリには、次の項目が表示されます（例： ）。

![chlimage_1-231](assets/chlimage_1-231.png)

* **詳細を表示**:以下を表示するリストへのリンク：

   * コンポーネントのレンダリングに使用するすべてのコンポーネントスクリプト。
   * この特定のコンポーネントのリポジトリコンテンツのパス。

   ![chlimage_1-232](assets/chlimage_1-232.png)

* **スクリプトを編集**:次のリンク：

   * コンポーネントスクリプトをCRXDE Liteで開きます。

* コンポーネントエントリ（矢印）を展開すると、次の項目も表示されます。

   * 選択したコンポーネント内の階層。
   * 選択したコンポーネントの単独でのレンダリング時間、その中にネストされた個々のコンポーネント、および結合された合計。

   ![chlimage_1-233](assets/chlimage_1-233.png)

>[!CAUTION]
>
>`/libs` の下にあるスクリプトを指すリンクもあります。ただし、これらのリンクは参照専用とし、`/libs` の下層にあるものは何も編集&#x200B;**しないでください**。変更しても無駄になる可能性があるからです。このブランチは、アップグレードしたり、ホットフィックス／機能パックを適用するたびに変更される傾向にあります。必要な変更はすべて `/apps` の下層でおこなう必要があります。詳しくは[オーバーレイとオーバーライド](/help/sites-developing/overlays.md)を参照してください。

### エラー {#errors}

![chlimage_1-234](assets/chlimage_1-234.png)

**エラー**&#x200B;タブは常に（上図のように）何も表示されないのが理想ですが、問題が発生すると、コンポーネントごとに以下の詳細が表示されます。

* 警告とエラーの詳細および CRXDE Lite 内の適切なコードへの直接リンク（コンポーネントによってエラーログにエントリが作成された場合）
* 警告（コンポーネントによって管理セッションが開かれた場合）

例えば、未定義のメソッドが呼び出された場合、結果のエラーは **エラー** タブ：

![chlimage_1-235](assets/chlimage_1-235.png)

「コンポーネント」タブのツリー内のコンポーネントエントリにも、エラーが発生したときにインジケーターが表示されます。

### テスト {#tests}

>[!CAUTION]
>
>AEM 6.2 では、開発者モードのテスト機能がスタンドアロンのツールアプリケーションとして再実装されました。
>
>詳しくは、[UI のテスト](/help/sites-developing/hobbes.md)を参照してください。
