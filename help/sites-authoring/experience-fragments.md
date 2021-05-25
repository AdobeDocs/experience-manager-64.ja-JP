---
title: エクスペリエンスフラグメント
seo-title: エクスペリエンスフラグメント
description: エクスペリエンスフラグメント
seo-description: 'null'
uuid: be1aceef-eb6e-47e5-a920-be5cc6de6191
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1fe58af0-3005-46fc-8717-5d32557947ed
exl-id: 8906b3ab-cb08-4b3e-8796-334e36b1e491
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1312'
ht-degree: 90%

---

# エクスペリエンスフラグメント{#experience-fragments}

エクスペリエンスフラグメントは、ページ内で参照できるコンテンツおよびレイアウトを含む 1 つ以上のコンポーネントのグループです。任意のコンポーネントを含めることができます。

エクスペリエンスフラグメントは、

* エクスペリエンス（ページ）の一部です。
* 複数ページで使用できます。
* テンプレートに基づいており（編集可能なもののみ）、構造とコンポーネントを定義します。
* 段落システムにレイアウトを含む 1 つ以上のコンポーネントで構成されています。
* 他のエクスペリエンスフラグメントを含めることができます。
* 他のコンポーネント（他のエクスペリエンスフラグメントを含む）と組み合わせて、完全なページ（エクスペリエンス）を作成できます。
* 複数のバリエーションを持つことができ、コンテンツやコンポーネントを共有できます。
* フラグメントの複数のバリエーションで使用できる構築ブロックに分類できます。

エクスペリエンスフラグメントを使用できるのは、次の場合です。

* 作成者がページの一部（エクスペリエンスのフラグメント）を再利用する場合は、そのフラグメントをコピーして貼り付ける必要があります。これらのエクスペリエンスのコピー／貼り付けの作成と管理には時間がかかり、ユーザーエラーが発生しがちです。
エクスペリエンスフラグメントは、コピー／貼り付けを不要にします。
* ヘッドレス CMS の使用例をサポートする場合。
作成者は AEM をオーサリングにのみ使用し、顧客への配信には使用しないようにします。サードパーティシステム／タッチポイントは、そのエクスペリエンスを使用してエンドユーザーに配信します。

>[!NOTE]
>
>エクスペリエンスフラグメントの書き込みアクセス権には、次のグループに登録されたユーザーアカウントが必要です。
>
>`experience-fragments-editors`
>
>問題が発生している場合は、システム管理者にお問い合わせください。

## エクスペリエンスフラグメントを使用するタイミング    {#when-should-you-use-experience-fragments}

エクスペリエンスフラグメントは次の場合に使用します。

* エクスペリエンスを再利用する場合。

   * 同じコンテンツまたは似たコンテンツで再利用されるエクスペリエンス

* サードパーティのためのコンテンツ配信プラットフォームとして AEM を使用する場合。

   * コンテンツ配信プラットフォームとして AEM を使用するソリューション
   * サードパーティのタッチポイントへのコンテンツの埋め込み

* 異なるバリエーションまたはレンディションを持つエクスペリエンスがある場合。

   * チャネルまたはコンテキスト固有のバリエーション
   * グループに対応したエクスペリエンス（チャネル間で異なるエクスペリエンスを持つキャンペーンなど）

* オムニチャネルコマースを使用する場合。

   * 規模に応じたソーシャルメディアチャネルでのコマース関連コンテンツの共有
   * タッチポイントのトランザクション化

## エクスペリエンスフラグメントの整理 {#organizing-your-experience-fragments}

以下をお勧めします。
* フォルダーを使用してエクスペリエンスフラグメントを整理する。

* [これらのフォルダーで使用可能なテンプレートを設定する](#configure-allowed-templates-folder)。

フォルダーを作成すると、次の操作をおこなうことができます。

* エクスペリエンスフラグメントにとって意味のある構造（例：分類に従った構造）を作成する。

   >[!NOTE]
   >
   >エクスペリエンスフラグメントの構造をサイトのページ構造に合わせる必要はありません。

* [許可されたテンプレートをフォルダーレベルで割り当てる。](#configure-allowed-templates-folder)

   >[!NOTE]
   >
   >[テンプレートエディター](/help/sites-authoring/templates.md)を使用すると、独自のテンプレートを作成できます。

次の例は、`Contributors`に従って構造化されたエクスペリエンスフラグメントを示しています。 また、使用される構造は、マルチサイト管理（言語コピーを含む）などの他の機能の使用方法の例も示します。

>[!CAUTION]
>
>Adobe Experience ManagerをCloud Serviceとして使用したWKNDサイトのスクリーンショットを次に示します。

![エクスペリエンスフラグメントのフォルダー](assets/xf-folders.png)

## エクスペリエンスフラグメントのフォルダーの作成と設定 {#creating-and-configuring-a-folder-for-your-experience-fragments}

エクスペリエンスフラグメントのフォルダーを作成および設定するには、次の操作をお勧めします。

1. [フォルダーを作成](/help/sites-authoring/managing-pages.md#creating-a-new-folder)します。

1. [そのフォルダーに使用できるエクスペリエンスフラグメントテンプレートを設定](#configure-allowed-templates-folder)します。

>[!NOTE]
>
>また、インスタンスに[許可されたテンプレート](#configure-allowed-templates-instance)を設定することもできますが、アップグレード時に値が上書きされる可能性があるので、この方法は&#x200B;**お勧めしません**。

### フォルダーに使用できるテンプレートの設定 {#configure-allowed-templates-folder}

>[!NOTE]
>
>アップグレード時に値が上書きされないので、「**[!UICONTROL 許可されたテンプレート]**」を指定する場合は、この方法をお勧めします。

1. 必要な&#x200B;**[!UICONTROL エクスペリエンスフラグメント]**&#x200B;フォルダーに移動します。

1. フォルダーを選択してから、「**[!UICONTROL プロパティ]**」を選択します。

1. 必要なテンプレートを取得するための正規表現を「**[!UICONTROL 許可されたテンプレート]**」フィールドに指定します。

   例：
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   ![エクスペリエンスフラグメントのプロパティ - 許可されたテンプレート](assets/xf-folders-templates.png)

1. 「**[!UICONTROL 保存して閉じる]**」を選択します。

### インスタンスに使用できるテンプレートの設定 {#configure-allowed-templates-instance}

>[!CAUTION]
>
>指定したテンプレートがアップグレード時に上書きされる可能性があるので、この方法で「**[!UICONTROL 許可されたテンプレート]**」を変更することはお勧めしません。
>
>このダイアログは、情報を提供する目的でのみ使用してください。

1. 必要な&#x200B;**[!UICONTROL エクスペリエンスフラグメント]**&#x200B;コンソールに移動します。

1. 「**[!UICONTROL 設定オプション]**」を選択します。

   ![設定ボタン](assets/xf-folders-18.png)

1. **[!UICONTROL エクスペリエンスフラグメントを設定]**&#x200B;ダイアログで、必要なテンプレートを指定します。

   ![エクスペリエンスフラグメントを設定](assets/xf-folders-19.png)

1. 「**[!UICONTROL 保存]**」を選択します。

## エクスペリエンスフラグメントの作成 {#creating-an-experience-fragment}

エクスペリエンスフラグメントを作成するには、次の手順に従います。

1. グローバルナビゲーションから「**[!UICONTROL エクスペリエンスフラグメント]**」を選択します。

   ![screen_shot_2018-04-05at92221am1](assets/screen_shot_2018-04-05at92221am1.png)

1. 必要なフォルダーに移動し、「**[!UICONTROL 作成]**」を選択します。

1. 「**[!UICONTROL エクスペリエンスフラグメント]**」を選択して、**[!UICONTROL エクスペリエンスフラグメントを作成]**&#x200B;ウィザードを開きます。

   適切な&#x200B;**[!UICONTROL テンプレート]**&#x200B;を選択して、「**[!UICONTROL 次へ]**」を選択します。

   ![xf-authoring-02](assets/xf-authoring-02.png)


1. **[!UICONTROL エクスペリエンスフラグメント]**&#x200B;のプロパティを入力します。

   **[!UICONTROL タイトル]**&#x200B;は必須です。**[!UICONTROL 名前]**&#x200B;が空欄のままの場合、**[!UICONTROL タイトル]**&#x200B;から派生されます。

   ![xf-authoring-03](assets/xf-authoring-03.png)

1. 「**[!UICONTROL 作成]**」をクリックします。

   メッセージが表示されます。以下から選択します。

   * 「**[!UICONTROL 完了]**」を選択すると、コンソールに戻ります。
   * 「**[!UICONTROL 開く]**」を選択すると、フラグメントエディターを開きます。

## エクスペリエンスフラグメントの編集 {#editing-your-experience-fragment}

エクスペリエンスフラグメントエディターには、通常のページエディターと似た機能があります。使い方の詳細については、[ページのコンテンツの編集](/help/sites-authoring/editing-content.md)を参照してください。

次の手順の例では、商品のティーザーを作成する方法を示します。

1. [コンポーネントブラウザー](/help/sites-authoring/author-environment-tools.md#components-browser)から&#x200B;**[!UICONTROL カテゴリティーザー]**&#x200B;をドラッグ＆ドロップします。

   ![xf-authoring-04](assets/xf-authoring-04.png)

1. コンポーネントツールバーから&#x200B;**[[!UICONTROL 設定]](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)**&#x200B;を選択します。
1. 必要に応じて&#x200B;**[!UICONTROL アセット]**&#x200B;を追加して&#x200B;**[!UICONTROL プロパティ]**&#x200B;を定義します。
1. **[!UICONTROL 完了]**（チェックマークアイコン）をクリックして定義を確定します。
1. 必要に応じてその他のコンポーネントを追加します。

## エクスペリエンスフラグメントのバリエーションの作成 {#creating-an-experience-fragment-variation}

必要に応じて、エクスペリエンスフラグメントのバリエーションを作成できます。

1. [編集](/help/sites-authoring/experience-fragments.md#editing-your-experience-fragment)するフラグメントを開きます。
1. 「**[!UICONTROL バリエーション]**」タブを開きます。

   ![xf-authoring-06](assets/xf-authoring-06.png)

1. 「**作成**」を使用すると、以下を作成できます。

   * **[!UICONTROL バリエーション]**
   * **[!UICONTROL バリエーションをライブコピーとして]**。

1. 必要なプロパティを定義します。

   * **[!UICONTROL テンプレート]**
   * **[!UICONTROL タイトル]**
   * **[!UICONTROL 名前]**（空欄のままの場合、タイトルから派生される）
   * **[!UICONTROL 説明]**
   * **[!UICONTROL バリエーションのタグ]**

   ![xf-authoring-07](assets/xf-authoring-07.png)

1. **[!UICONTROL 完了]**（チェックマークアイコン）で確定すると、新しいバリエーションがパネルに表示されます。

   ![xf-authoring-08](assets/xf-authoring-08.png)

## エクスペリエンスフラグメントの使用 {#using-your-experience-fragment}

ページをオーサリングする際に、エクスペリエンスフラグメントを使用できるようになりました。

1. 編集するページを開きます。

   例：[http://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html](http://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html)

1. コンポーネントブラウザーからページ段落システムにコンポーネントをドラッグして、エクスペリエンスフラグメントコンポーネントのインスタンスを作成します。

   ![xf-authoring-09](assets/xf-authoring-09.png)

1. 次のいずれかの方法で、実際のエクスペリエンスフラグメントをコンポーネントインスタンスに追加します。

   * アセットブラウザーから必要なフラグメントをドラッグして、コンポーネントにドロップします。
   * コンポーネントツールバーから&#x200B;**[!UICONTROL 設定]**&#x200B;を選択して、使用するフラグメントを指定し、**完了**（チェックマーク）で確定します。

   ![xf-authoring-10](assets/xf-authoring-10.png)

   >[!NOTE]
   >
   >コンポーネントツールバーの「編集」は、フラグメントエディターでフラグメントを開くためのショートカットとして動作します。

## 構築ブロック {#building-blocks}

1 つ以上のコンポーネントを選択して、フラグメント内で再利用するための構築ブロックを作成できます。

### 構築ブロックの作成 {#creating-a-building-block}

新しい構築ブロックを作成するには、次の手順に従います。

1. エクスペリエンスフラグメントエディターで、再利用するコンポーネントを選択します。

   ![xf-authoring-12](assets/xf-authoring-12.png)

1. コンポーネントツールバーから、「**[!UICONTROL 構築ブロックに変換]**」を選択します。

   ![xf-authoring-13-icon](assets/xf-authoring-13-icon.png)

   次に例を示します。

   ![xf-authoring-13](assets/xf-authoring-13.png)

1. **[!UICONTROL 構築ブロック]**&#x200B;の名前を入力して、「**[!UICONTROL 変換]**」で確定します。

   ![xf-authoring-14](assets/xf-authoring-14.png)

1. **構築ブロック**&#x200B;がタブに表示され、段落システムで選択できます。

   ![xf-authoring-15](assets/xf-authoring-15.png)

### 構築ブロックの管理 {#managing-a-building-block}

構築ブロックは、「**[!UICONTROL 構築ブロック]**」タブに表示されます。各ブロックでは、次の操作をおこなえます。

* マスターに移動（マスターバリエーションを新しいタブで開く）
* 名前を変更
* 削除

![xf-authoring-16](assets/xf-authoring-16.png)

### 構築ブロックの使用 {#using-a-building-block}

任意のコンポーネントと同様に、構築ブロックをフラグメントの段落システムにドラッグできます。

## プレーン HTML レンディション {#the-plain-html-rendition}

URL で `.plain.` セレクターを使用すると、プレーン HTML レンディションにアクセスできます。

これはブラウザーから利用できますが、主な目的は、他のアプリケーション（例えば、サードパーティ Web アプリ、カスタムモバイル実装など）が、URL のみを使用して、エクスペリエンスフラグメントのコンテンツに直接アクセスできるようにすることです。

プレーン HTML レンディションは、次のようなパスにプロトコル、ホストおよびコンテキストパスを追加します。

* タイプが `src`、`href`、`action` のいずれか

* または、`-src` か `-href` で終わる

次に例を示します。

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>リンクは、常に、パブリッシュインスタンスを参照します。リンクは、サードパーティによって使用されることを意図しているので、オーサーインスタンスではなく、常にパブリッシュインスタンスから呼び出されます。

![xf-authoring-17](assets/xf-authoring-17.png)

## エクスペリエンスフラグメントの書き出し {#exporting-experience-fragments}

デフォルトでは、エクスペリエンスフラグメントは HTML 形式で配信され、AEM とサードパーティチャネルのどちらでも同じように使用できます。

Adobe Targetに書き出す場合は、HTMLが使用されます。 詳しくは、[Adobe Target とエクスペリエンスフラグメントの統合](/help/sites-administering/experience-fragments-target.md)を参照してください。
