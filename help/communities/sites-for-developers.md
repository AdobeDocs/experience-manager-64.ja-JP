---
title: コミュニティサイトの基本事項
seo-title: コミュニティサイトの基本事項
description: コミュニティサイトのエクスポートと削除およびカスタムサイトテンプレートの作成
seo-description: コミュニティサイトのエクスポートと削除およびカスタムサイトテンプレートの作成
uuid: f0ec0e71-64e9-415a-b14a-939a9b1611c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: dc7a085e-d6de-4bc8-bd7e-6b43f8d172d2
exl-id: 2b26d937-4ebf-4a67-9715-a21c8fc45e1e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 64%

---

# コミュニティサイトの基本事項  {#community-site-essentials}

## カスタムサイトテンプレート {#custom-site-template}

カスタムサイトテンプレートは、コミュニティサイトの言語コピーごとに個別に指定できます。

そうするには、次の手順を実行します。

* カスタムテンプレートの作成
* 既定のサイトテンプレートパスをオーバーレイ
* オーバーレイパスにカスタムテンプレートを追加する
* `page-template`プロパティを`configuration`ノードに追加して、カスタムテンプレートを指定します。

**デフォルトのテンプレート**：

/**libs**/social/console/components/hbs/sitepage/**sitepage**.hbs

**オーバーレイのパスのカスタムテンプレート**：

/**apps**/social/console/components/hbs/sitepage/**&lt;*template-name*>**.hbs

**プロパティ**:page-template\
**種類**：string\
**値**: &lt;>template-name *> （拡張子なし）*

**設定ノード**：

/content/&lt;*コミュニティサイトのパス*/&lt;*lang*/configuration

例：/content/sites/engage/en/configuration

>[!NOTE]
>
>オーバーレイされたパスのすべてのノードのタイプは、`Folder` である必要があります。

>[!CAUTION]
>
>カスタムテンプレートに&#x200B;*sitepage.hbs,*&#x200B;という名前を付けると、すべてのコミュニティサイトがカスタマイズされます。

### カスタムサイトテンプレートの例 {#custom-site-template-example}

例えば、`vertical-sitepage.hbs`はサイトテンプレートで、メニューリンクをバナーの下に水平方向ではなく、ページの左側に垂直方向に配置します。

[FilePlaceカス](assets/vertical-sitepage.hbs)
タムサイトテンプレートをオーバーレイフォルダーに配置します。

/**apps**/social/console/components/hbs/sitepage/**vertical-sitepage**.hbs

設定ノードに`page-template`プロパティを追加して、カスタムテンプレートを識別します。

/content/sites/sample/en/configuration

![chlimage_1-80](assets/chlimage_1-80.png)

「**すべて保存**」を選択してカスタムコードをすべての AEM インスタンスにレプリケートしてください（コミュニティサイトコンテンツがコンソールから公開された時点ではカスタムコードは含まれていません）。

カスタムコードをレプリケートするには、[パッケージを作成](../../help/sites-administering/package-manager.md#creating-a-new-package)し、すべてのインスタンスにデプロイすることをお勧めします。

## コミュニティサイトの書き出し  {#exporting-a-community-site}

コミュニティサイトが作成されたら、パッケージマネージャーに保存され、ダウンロードおよびアップロードできる AEM パッケージとしてそのサイトを書き出すことができます。

書き出しは、[コミュニティサイトコンソール](sites-console.md#exporting-the-site)からおこなうことができます。

UGC とカスタムコードはコミュニティサイトパッケージに含まれていないことに注意してください。

UGCを書き出すには、GitHubで利用可能なオープンソース移行ツールである[AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)を使用します。

## コミュニティサイトの削除 {#deleting-a-community-site}

AEM Communities 6.3 Service Pack 1 以降では、コミュニティ／サイトコンソール内でコミュニティサイトにマウスポインターを置くと、サイトを削除アイコンが表示されます。開発中にコミュニティサイトを削除して新規に開始したい場合は、この機能を使用できます。 コミュニティサイトを削除すると、そのサイトに関連付けられている次のアイテムが削除されます。

* [UGC](#user-generated-content)
* [ユーザーグループ](#community-user-groups)
* [Assets](#enablement-assets)
* [データベースレコード](#database-records)

### Community Unique Site ID {#community-unique-site-id}

CRXDE を使用して、コミュニティに関連付けられている一意のサイト ID を識別するには、次の手順に従います。

* サイトの言語ルート（例：`/content/sites/*<site name>*/en/rep:policy`）に移動します。

* `rep:principalName`を持つ`allow<#>`ノードを、次の形式で検索します。 `rep:principalName = *community-enable-nrh9h-members*`

* サイトIDは、`rep:principalName`の3番目のコンポーネントです。
例えば、 
`rep:principalName = community-enable-nrh9h-members`

   * **サイト名** = *enable*
   * **サイトID**  =  *nrh9h*
   * **一意のサイト ID** = *enable-nrh9h*

### ユーザー生成コンテンツ {#user-generated-content}

Github から communities-srp-tools プロジェクトを取得します。

* [https://github.com/Adobe-Marketing-Cloud/communities-srp-tools](https://github.com/Adobe-Marketing-Cloud/communities-srp-tools)

これには、任意の SRP からすべての UGC を削除できるサーブレットが含まれています。

次の例に示すように、特定のサイトを対象としてすべての UGC を削除できます。

* path=/content/usergenerated/asi/mongo/content/sites/engage

この場合、（パブリッシュインスタンスで入力された）ユーザー生成コンテンツのみが削除され、（オーサーインスタンスで入力された）作成コンテンツは削除されません。したがって、[シャドウノード](srp.md#shadownodes)は影響を受けません。

### コミュニティユーザーグループ {#community-user-groups}

すべてのオーサーインスタンスおよびパブリッシュインスタンスで、[セキュリティコンソール](../../help/sites-administering/security.md)から、以下に該当する[ユーザーグループ](users.md)を検索して削除します。

* 先頭に`community`が付きます。
* [一意のサイトID](#community-unique-site-id)が続きます。

（例：`community-engage-x0e11-members`）。

### イネーブルメントアセット {#enablement-assets}

メインコンソールから、次の手順に従います。

* **[!UICONTROL アセット]**&#x200B;を選択します。
* **[!UICONTROL 選択]**&#x200B;モードに入ります
* [一意のサイトID](#community-unique-site-id)を持つという名前のフォルダーを選択します。
* 「**[!UICONTROL 削除]**」を選択します（場合によっては、「**[!UICONTROL 詳細…」から選択する必要があります）。]**)

### データベースレコード {#database-records}

特定のイネーブルメントコミュニティサイトの 1 つを対象として、データベースエントリを選択的に削除するためのツールはありません。

すべてのコミュニティサイトを削除する場合は、MySQL Workbench を使用して enablementdb および scormenginedb を削除します。
