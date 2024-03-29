---
title: テンプレート
seo-title: Templates
description: テンプレートは、新しいページのベースとして使用するページを作成する際に使用します
seo-description: Templates are used when creating a page which will be used as the base for the new page
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 4ecb6e10-1d6b-4065-917f-e86215687e29
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 78%

---

# テンプレート{#templates}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

テンプレートは、AEMの様々なポイントで使用されます。

* 条件 [テンプレートを選択する必要があるページの作成](#templates-pages);これは、新しいページのベースとして使用されます。 テンプレートは、結果ページの構造、初期コンテンツ、および [コンポーネント](/help/sites-authoring/default-components.md) 使用可能（デザインプロパティ）

* [コンテンツフラグメントの作成時にテンプレートを選択](#templates-content-fragments)します。このテンプレートは、構造、初期要素およびバリエーションを定義します。

ここでは、次のテンプレートについて詳しく説明します。

* [ページテンプレート - 編集可能](/help/sites-developing/page-templates-editable.md)
* [ページテンプレート - 静的](/help/sites-developing/page-templates-static.md)
* [コンテンツフラグメントテンプレート](/help/sites-developing/content-fragment-templates.md)
* [アダプティブテンプレートレンダリング](/help/sites-developing/templates-adaptive-rendering.md)

## テンプレート — ページ {#templates-pages}

AEMには、ページを作成するための 2 つの基本的なタイプのテンプレートが用意されています。

>[!NOTE]
>
>[新しいページを作成](/help/sites-authoring/managing-pages.md#creating-a-new-page)するときにテンプレートを使用する際、ページ編集者にとって見た目的な違いはなく、またどちらのタイプのテンプレートを使用しているかについての表示もありません。

### 編集可能なテンプレート {#editable-templates}

編集可能テンプレートは、AEMを使用した開発のベストプラクティスと考えられるようになりました。

編集可能テンプレートの利点は次のとおりです。

* 可能 [作成済み](/help/sites-authoring/templates.md#creating-a-new-template-template-author) および [編集済み](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 作成者によって

* テンプレートで作成されたすべてのページで以下を定義できるようにが導入されました。

   * 構造
   * 初期コンテンツ
   * コンテンツポリシー

* 新しいページの作成後も、そのページとテンプレートの間に動的接続が維持されます。つまり、テンプレートの構造に対する変更は、そのテンプレートを使用して作成されるすべてのページに反映されます（初期コンテンツに対する変更は反映されません）。
* デザインプロパティを保持するには、テンプレートエディターから編集できるコンテンツポリシーを使用します（ページエディター内のデザインモードは使用しません）。
* `/conf` に保存されます。
* 詳しくは、[編集可能テンプレート](/help/sites-developing/page-templates-editable.md)を参照してください。

>[!NOTE]
>
>AEM コミュニティの記事の[編集可能テンプレートを使用した Adobe Experience Manager 6.4 の web サイトの作成](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html)では、編集可能テンプレートを使用して Experience Manager サイトを開発する方法を説明しています。

### 静的テンプレート {#static-templates}

静的テンプレート：

* 開発者が定義および設定する必要があります。
* これは AEM のオリジナルのテンプレートシステムで、多くのバージョンで使用されています。
* 静的テンプレートは、作成するページと同じ構造を持ち、実際のコンテンツを持たないノードの階層です。
* 新しいページを作成するためにコピーされます。その後、動的接続は存在しません。
* デザインプロパティを保持するには、[デザインモード](/help/sites-authoring/default-components-designmode.md)を使用します。
* `/apps` に保存されます
* 詳しくは、[静的テンプレート](/help/sites-developing/page-templates-static.md)を参照してください。

>[!NOTE]
>
>AEM 6.4 以降では、静的テンプレートの使用はベストプラクティスとは見なされていません。その代わりに編集可能テンプレートを使用してください。
>
>[AEM 最新化](modernization-tools.md)ツールは、静的テンプレートから編集可能テンプレートへの移行に役立ちます。

### 使用可能なテンプレート {#template-availability}

>[!CAUTION]
>
>AEM は、複数のプロパティをオファーして、**Sites** で許可されるテンプレートを制御します。ただし、組み合わせることで非常に複雑なルールになり、追跡や管理が困難になる可能性があります。
>
>したがって、アドビでは、次の項目を定義して、単純に開始することをお勧めします。
>
>* プロパティは `cq:allowedTemplates` のみ
>
>* サイトのルートにのみ
>
>例えば、We.Retail `/content/we-retail/jcr:content` を参照してください。
>
>プロパティ `allowedPaths`、`allowedParents`、`allowedChildren` をテンプレートに配置して、より高度なルールを定義することもできます。ただし、可能な場合、許可されるテンプレートをさらに制限する必要がある場合は、サイトのサブセクションでさらに `cq:allowedTemplates` プロパティを定義する方が&#x200B;*はるかに*&#x200B;簡単です。
>
>また、**ページプロパティ**&#x200B;の「**詳細**」タブで、作成者が `cq:allowedTemplates` プロパティを更新できるという利点もあります。その他のテンプレートプロパティは、（標準）UI を使用して更新することはできないので、変更するたびに、ルールとコードのデプロイメントを管理する開発者が必要になります。

サイト管理インターフェイスで新しいページを作成する場合、使用可能なテンプレートのリストは、新しいページの場所と、各テンプレートで指定されている配置制限によって異なります。

次のプロパティは、新しいページをページ `P` の子として配置する場合に、テンプレート `T` を使用できるかどうかを決定します。これらの各プロパティは、0 個以上の正規表現を保持する複数値の文字列で、パスの照合に使用されます。

* `jcr:content` サブノードの `P` または `P` の上位ページの `cq:allowedTemplates` プロパティ。

* `T` の `allowedPaths` プロパティ。

* `T` の `allowedParents` プロパティ。

* `P` のテンプレートの `allowedChildren` プロパティ。

評価は次のように行われます。

* `P` で始まるページ階層を昇順にしているときに見つかった、最初の空でない `cq:allowedTemplates` プロパティは、`T` のパスと一致します。一致する値がない場合、`T` は拒否されます。

* `T` に空でない `allowedPaths` プロパティがあるものの、 `P` のパスと一致する値がない場合、`T` は拒否されます。

* 上記のプロパティの両方が空または存在しない場合、`P` と同じアプリケーションに属さない限り、`T` は拒否されます。`T` は、`T` のパスの 2 番目のレベルの名前が `P` のパスの 2 番目のレベルの名前と同じである場合に限り、`P` と同じアプリケーションに属します。例えば、テンプレート `/apps/geometrixx/templates/foo` は、ページ `/content/geometrixx` と同じアプリに属しています。

* `T` に空でない `allowedParents` プロパティがあるものの、`P` のパスと一致する値がない場合、`T` は拒否されます。

* `P` のテンプレートに空でない `allowedChildren` プロパティがあるものの、`T` のパスと一致する値がない場合、`T` は拒否されます。

* その他すべての場合は、`T` は許可されます。

以下の図は、テンプレートの評価プロセスを示しています。

![chlimage_1-176](assets/chlimage_1-176.png)

#### 子ページで使用するテンプレートの制限 {#limiting-templates-used-in-child-pages}

特定のページの下に子ページを作成するために使用できるテンプレートを制限するには、ページの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用して、子ページとして許可するテンプレートのリストを指定します。例えば、`/apps/geometrixx/templates/contentpage` リストの各値は、許可されている子ページのテンプレートへの絶対パスである必要があります。

テンプレートの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用すると、このテンプレートを使用するすべての新規作成ページにこの設定を適用できます。

テンプレート階層に関する制約などをさらに追加する場合は、テンプレートの `allowedParents/allowedChildren` プロパティを使用できます。その後、テンプレート T から作成されたページが、テンプレート T から作成されたページと親子である必要があることを明示的に指定できます。

## テンプレート — コンテンツフラグメント {#templates-content-fragments}

詳しくは、 [コンテンツフラグメントテンプレート](/help/sites-developing/content-fragment-templates.md) を参照してください。
