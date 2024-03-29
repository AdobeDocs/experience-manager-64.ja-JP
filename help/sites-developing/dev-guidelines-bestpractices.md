---
title: AEM の開発 - ガイドラインとベストプラクティス
seo-title: AEM Development - Guidelines and Best Practices
description: AEMでの開発のガイドラインとベストプラクティス
seo-description: Guidelines and best practices for developing on AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
exl-id: 26c9098b-f810-4c3d-a6c8-9a5fbcd307dd
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 28%

---

# AEM の開発 - ガイドラインとベストプラクティス{#aem-development-guidelines-and-best-practices}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## テンプレートとコンポーネントの使用に関するガイドライン {#guidelines-for-using-templates-and-components}

AEMのコンポーネントとテンプレートは、非常に強力なツールキットを形成します。 開発者は、Web サイトのレイアウトを統一（ブランド保護）したまま、Web サイトのビジネスユーザー、編集者、管理者に、変化するビジネスニーズ（コンテンツの俊敏性）に合わせた機能を提供できます。

Web サイトや一連の Web サイト（例えば、グローバル企業の支店）を担当する人が Web サイトに新しいタイプのコンテンツを表示するのは、一般的な課題です。

既に公開されている他の記事から抽出したリストを Web サイトに追加する必要があるとします。 ページのデザインと構造は、Web サイトの残りの部分と同じにする必要があります。

このような課題に対処する推奨される方法は、次のとおりです。

* 既存のテンプレートを再利用して、新しいタイプのページを作成します。 テンプレートはページ構造（ナビゲーション要素、パネルなど）を大まかに定義し、そのデザイン（CSS、グラフィック）によってさらに微調整されます。
* 新しいページで段落システム (parsys/iparsys) を使用します。
* 段落システムのデザインモードに対するアクセス権を定義し、権限を持つユーザー（通常は管理者）のみが変更できるようにします。
* 特定の段落システムで許可されるコンポーネントを定義して、編集者が必要なコンポーネントをページ上に配置できるようにします。 この場合、リストコンポーネントで、ページのサブツリーを移動し、事前定義されたルールに従って情報を抽出できます。
* 編集者は、要求された機能（情報）をビジネスに提供するために、担当のページに許可されたコンポーネントを追加および設定します。

これは、このアプローチによって、開発チームの関与なく、Web サイトの投稿ユーザーや管理者がビジネスニーズにすばやく対応できるようになることを示しています。 新しいテンプレートの作成など、代替の方法は、通常、コストのかかる課題で、変更管理プロセスと開発チームの関与が必要です。 これにより、プロセス全体が大幅に長く、コストがかかります。

したがって、AEMベースのシステムの開発者は、次を使用する必要があります。

* 統一性とブランド保護のためのテンプレートと段落システム設計へのアクセス制御
* 段落システム（柔軟性を考慮した設定オプションを含む）

デベロッパー向けの以下の一般的なルールは、通常のプロジェクトの大部分で意味を持ちます。

* テンプレートの数を少なくします。Web サイト上の基本的に異なるページ構造の数を最小限に抑えます。
* 必要な柔軟性と設定機能をカスタムコンポーネントに提供します。
* AEM段落システムの能力と柔軟性を最大限に活用 — parsys および iparsys コンポーネント。

### コンポーネントおよびその他の要素のカスタマイズ {#customizing-components-and-other-elements}

独自のコンポーネントを作成する場合や、既存のコンポーネントをカスタマイズする場合、多くの場合、既存の定義を再利用するのが最も簡単（かつ安全）です。 同じ原則が、エラーハンドラーなど、AEM 内の他の要素にも当てはまります。

これは、既存の定義をコピーしてオーバーレイすることで実行することができます。つまり、`/libs` から `/apps/<your-project>` に定義をコピーします。この新しい定義は `/apps` で、必要に応じて更新できます。

>[!NOTE]
>
>詳しくは、 [オーバーレイの使用](/help/sites-developing/overlays.md) を参照してください。

次に例を示します。

* [コンポーネントをカスタマイズ](/help/sites-developing/components.md)

   これには、コンポーネント定義のオーバーレイが含まれます。

   * 既存のコンポーネントをコピーすることにより、`/apps/<website-name>/components/<MyComponent>` に新しいコンポーネントフォルダーを作成してください。

      * 例えば、テキストコンポーネントをカスタマイズするには、次のようにコピーします。

         * コピー元：`/libs/foundation/components/text`
         * コピー先：`/apps/myProject/components/text`

* [エラーハンドラーによって表示されるページをカスタマイズ](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

   この場合、サーブレットのオーバーレイを含みます。

   * リポジトリー内で、デフォルトスクリプトを次のようにコピーします。

      * コピー元：`/libs/sling/servlet/errorhandler/`
      * コピー先：`/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>`/libs` パス内の設定は&#x200B;**一切**&#x200B;変更しないでください。
>
>`/libs` コンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。
>
>設定およびその他の変更の手順は以下のとおりです。
>
>1. `/libs` 内の項目を `/apps` にコピー
>1. `/apps` 内での変更


## JCR クエリを使用するタイミングと使用しないタイミング {#when-to-use-jcr-queries-and-when-not-to-use-them}

JCR クエリは、正しく導入された場合に強力なツールです。 次の項目に適しています。

* コンテンツに対するフルテキスト検索などの実際のエンドユーザークエリ。
* 構造化されたコンテンツをリポジトリ全体で見つける必要がある場合。

   このような場合、クエリは、コンポーネントアクティベーションやキャッシュ無効化など、絶対に必要な場合にのみ実行してください（ワークフローステップ、コンテンツ変更時にトリガーされるイベントハンドラー、フィルターなどとは対照的）。

JCR クエリは、純粋なレンダリング要求には使用しないでください。 例えば、JCR クエリは次の用途には適していません。

* レンダリングナビゲーション
* 「最新上位 10 件のニュース項目」の作成の概要
* コンテンツ項目の数の表示

コンテンツをレンダリングする場合は、JCR クエリを実行する代わりに、コンテンツツリーへのナビゲーションアクセスを使用します。

>[!NOTE]
>
>次の [Query Builder](/help/sites-developing/querybuilder-api.md)を使用する場合は、JCR クエリを使用します。Query Builder では内部で JCR クエリが生成されるからです。

## セキュリティに関する考慮事項 {#security-considerations}

>[!NOTE]
>
>[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照することもお勧めします。

### JCR（リポジトリ）セッション {#jcr-repository-sessions}

管理セッションではなく、ユーザーセッションを使用する必要があります。 つまり、次を使用する必要があります。

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### クロスサイトスクリプティング (XSS) に対するProtect {#protect-against-cross-site-scripting-xss}

クロスサイトスクリプティング (XSS) を使用すると、攻撃者は他のユーザーが閲覧した Web ページにコードを挿入できます。 このセキュリティ脆弱性は、悪意のある Web ユーザーによって悪用され、アクセス制御をバイパスする可能性があります。

AEMは、ユーザーが指定したすべてのコンテンツを出力時にフィルタリングする原則を適用します。 開発とテストの両方で、XSS の防止が最も優先されます。

また、[Apache 対応の mod_security](https://modsecurity.org) などの web アプリケーションファイアウォールを使用すると、デプロイメント環境のセキュリティを高い信頼性で一元的に制御でき、以前は検出されなかったクロスサイトスクリプティング攻撃に対する保護も可能です。

>[!CAUTION]
>
>AEMで提供されるコード例は、それ自体がそのような攻撃から保護されていない場合があり、通常は Web アプリケーションファイアウォールによるリクエストフィルタリングに依存しています。

XSS API チートシートには、XSS API を使用してAEMアプリをより安全にするために知っておく必要がある情報が含まれています。 こちらからダウンロードできます。

XSSAPI 参照シート。

[ファイルを入手](assets/xss_cheat_sheet_2016.pdf)

### 機密情報の通信の保護 {#securing-communication-for-confidential-information}

インターネットアプリケーションに関しては、機密情報を転送する際に必ずお知らせください

* トラフィックは SSL を通じて保護されます
* HTTPPOST（該当する場合）が使用されます

これは、システムに対して機密情報（設定や管理アクセスなど）と、ユーザーに対して機密情報（個人の詳細など）に当てはまります

## 個別の開発タスク {#distinct-development-tasks}

### エラーページのカスタマイズ {#customizing-error-pages}

エラーページはAEM用にカスタマイズできます。 内部サーバーエラーに対する Sling トレースがインスタンスに表示されないように、これをお勧めします。

詳しくは、 [エラーハンドラーによって表示されるエラーページのカスタマイズ](/help/sites-developing/customizing-errorhandler-pages.md) 詳細はこちら。

### Java プロセスでファイルを開く {#open-files-in-the-java-process}

AEM は多数のファイルにアクセスできるので、[Java プロセス用に開いているファイル](/help/sites-deploying/configuring.md#open-files-in-the-java-process)の数を AEM 用に明示的に設定することをお勧めします。

この問題を最小限に留めるために、開発の際は、開かれるすべてのファイルができるだけ早く（ただし合理的な範囲で）、正しく閉じられることを確認する必要があります。
