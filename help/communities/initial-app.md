---
title: 初期サンドボックスアプリケーション
seo-title: Initial Sandbox Application
description: テンプレート、コンポーネントおよびスクリプトの作成
seo-description: Create template, component, and script
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
exl-id: 3da30cb4-39b2-4495-9e8b-93567b73b644
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 58%

---

# 初期サンドボックスアプリケーション {#initial-sandbox-application}

ここでは、次のものを作成します。

* サンプル Web サイトのコンテンツページを作成する際に使用する&#x200B;**[テンプレート](#createthepagetemplate)**
* Web サイトのページをレンダリングする際に使用する&#x200B;**[コンポーネントとスクリプト](#create-the-template-s-rendering-component)**

## コンテンツテンプレートの作成 {#create-the-content-template}

テンプレートは、新しいページのデフォルトのコンテンツを定義するものです。複雑な Web サイトでは、複数のテンプレートを使用して、サイト内の様々なタイプのページを作成する場合があります。さらに、変更内容をサーバークラスターにロールアウトする際のブループリントとして一連のテンプレートを使用する場合もあります。

この演習では、すべてのページを 1 つの単純なテンプレートに基づいて作成します。

1. CRXDE Lite のエクスプローラーペインで、次の手順を実行します。

   * 選択 `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL 作成/テンプレートを作成]**

1. テンプレートを作成ダイアログで、次の値を入力し、「**[!UICONTROL 次へ]**」をクリックします。

   * ラベル: `playpage`
   * タイトル: `An SCF Sandbox Play Template`
   * 説明: `An SCF Sandbox template for play pages`
   * リソースタイプ: `an-scf-sandbox/components/playpage`
   * ランキング：&lt;デフォルトのまま>

   「ラベル」は、ノード名に使用されます。

   「リソースタイプ」は、`playpage` の jcr:content ノードにプロパティ `sling:resourceType` として表示されます。ブラウザーから要求された場合に、コンテンツをレンダリングするコンポーネント（リソース）を識別します。

   この場合、 `playpage`テンプレートは `an-scf-sandbox/components/playpage` コンポーネント。 慣例により、コンポーネントのパスは相対パスなので、Sling は、 `/apps` フォルダーおよび（見つからない場合） `/libs` フォルダー。

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. コピー／貼り付けを使用する場合は、「リソースタイプ」の値の先頭や末尾にスペースがないことを確認します。

   「**[!UICONTROL 次へ]**」をクリックします。

1. 「許可されているパス」は、**[!UICONTROL 新しいページ]**&#x200B;ダイアログにテンプレートが表示されるように、このテンプレートを使用するページのパスを参照します。

   パスを追加するには、プラスボタン `+` と入力します。 `/content(/.&ast;)?` をクリックします。 コピー/貼り付けを使用する場合は、先頭または末尾にスペースがないことを確認します。

   注意：許可されているパスプロパティの値は、 *正規表現。*&#x200B;この表現と一致するパスを持つコンテンツページでテンプレートを使用できます。この場合、正規表現は **/content** フォルダーおよびそのすべてのサブページ。

   作成者が以下のページを作成したとき `/content`、 `playpage`使用可能なテンプレートのリストに、「SCF サンドボックスページテンプレート」というタイトルのテンプレートが表示されます。

   ルートページをテンプレートから作成した後、プロパティを変更して正規表現にルートパスを含めると、テンプレートへのアクセスをその Web サイトに制限できます。次に例を示します。

   `/content/an-scf-sandbox(/.&ast;)?`

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. 「**[!UICONTROL 次へ]**」をクリックします。

   クリック **[!UICONTROL 次へ]** 内 **[!UICONTROL 許可された親]** パネル。

   クリック **[!UICONTROL 次へ]** 内 **[!UICONTROL 許可されている子]** パネル。

   「**[!UICONTROL OK]**」をクリックします。

1. 「OK」をクリックし、テンプレートの作成を終了すると、新しい `playpage` テンプレートについて、「プロパティ」タブの値の隅に赤い三角形が表示されていることがわかります。これらの赤い三角形は、編集内容が保存されていないことを示します。

   クリック **[!UICONTROL すべて保存]** をクリックして、新しいテンプレートをリポジトリに保存します。

   ![chlimage_1-77](assets/chlimage_1-77.png)

### テンプレートのレンダリングコンポーネントの作成 {#create-the-template-s-rendering-component}

コンテンツを定義し、[playpage テンプレート](#createthepagetemplate)に基づいて作成されたページをレンダリングするコンポーネントを作成します。**

1. CRXDE Liteで右クリック **`/apps/an-scf-sandbox/components`** をクリックし、 **[!UICONTROL 作成/コンポーネント]**.
1. ノード名（ラベル）を *playpage*&#x200B;の場合、コンポーネントへのパスは

   `/apps/an-scf-sandbox/components/playpage`

   再生ページテンプレートのリソースタイプに対応する ( オプションで、最初の **`/apps/`** パスの一部 )。

   **[!UICONTROL コンポーネントを作成]**&#x200B;ダイアログで、以下のプロパティ値を入力します。

   * ラベル：**playpage**
   * タイトル：**An SCF Sandbox Play Component**
   * 説明：**This is the component which renders content for An SCF Sandbox page.**
   * スーパータイプ： *&lt;leave blank=&quot;&quot;>*
   * グループ:

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. クリック **[!UICONTROL 次へ]** まで **[!UICONTROL 許可されている子]** ダイアログのパネルが表示されます

   * 「**[!UICONTROL OK]**」をクリックします。
   * クリック **[!UICONTROL すべて保存]**

1. コンポーネントのパスとテンプレートの resourceType が一致していることを確認します。

   >[!CAUTION]
   >
   >Web サイトを正しく機能させるには、playpage コンポーネントのパスと playpage テンプレートの sling:resourceType プロパティとの対応が重要です。

   ![chlimage_1-79](assets/chlimage_1-79.png)
