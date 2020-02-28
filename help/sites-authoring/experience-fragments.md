---
title: エクスペリエンスフラグメント
seo-title: エクスペリエンスフラグメント
description: 'null'
seo-description: 'null'
uuid: be1aceef-eb6e-47e5-a920-be5cc6de6191
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 1fe58af0-3005-46fc-8717-5d32557947ed
translation-type: tm+mt
source-git-commit: 6f6952686446359485f180050219a12db9d3969a

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

エクスペリエンスフラグメントを使用できます。

* 作成者がページの一部（エクスペリエンスのフラグメント）を再利用する場合は、そのフラグメントをコピーして貼り付ける必要があります。これらのエクスペリエンスのコピー／貼り付けの作成と管理には時間がかかり、ユーザーエラーが発生しがちです。エクスペリエンスフラグメントは、コピー／貼り付けを不要にします。
* ヘッドレスCMSユースケースをサポートする。 作成者は、オーサリングのみにAEMを使用し、顧客への配信には使用しない。 サードパーティシステム／タッチポイントは、そのエクスペリエンスを使用してエンドユーザーに配信します。

>[!NOTE]
>
>エクスペリエンスフラグメントの書き込みアクセス権には、次のグループに登録されたユーザーアカウントが必要です。
>
>`experience-fragments-editors`
>
>問題が発生している場合は、システム管理者にお問い合わせください。

## エクスペリエンスフラグメントを使用するタイミング {#when-should-you-use-experience-fragments}

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

次の操作を行うことをお勧めします。
* フォルダーを使用してエクスペリエンスフラグメントを整理する、

* [これらのフォルダーで許可するテンプレートを設定します](#configure-allowed-templates-folder)。

フォルダを作成すると、次の操作を行うことができます。

* エクスペリエンスフラグメントに対して意味のある構造を作成する。例えば、分類に従って

   >[!NOTE]
   >
   >エクスペリエンスフラグメントの構造をサイトのページ構造に揃える必要はありません。

* [許可されたテンプレートをフォルダーレベルで割り当てる](#configure-allowed-templates-folder)

   >[!NOTE]
   >
   >[テンプレートエディター](/help/sites-authoring/templates.md)を使用すると、独自のテンプレートを作成できます。

次の例は、に従って構造化されたエクスペリエンスフラグメントを示していま `Contributors`す。 また、マルチサイト管理（言語コピーを含む）などのその他の機能の使用方法も説明します。

>[!CAUTION]
>
>次のスクリーンショットは、Adobe Experience Managerをクラウドサービスとして使用したWKNDサイトからのものです。

![エクスペリエンスフラグメントのフォルダー](assets/xf-folders.png)

## エクスペリエンスフラグメント用のフォルダーの作成と設定 {#creating-and-configuring-a-folder-for-your-experience-fragments}

エクスペリエンスフラグメント用のフォルダーを作成および設定するには、次の操作を行うことをお勧めします。

1. [フォルダーの作成](/help/sites-authoring/managing-pages.md#creating-a-new-folder).

1. [そのフォルダーに対して許可するエクスペリエンスフラグメントテンプレートを設定しま](#configure-allowed-templates-folder)す。

>[!NOTE]
>
>また、インスタンスに許可されているテンプ [レートを設定することもできますが](#configure-allowed-templates-instance)、アップグレード時に値が上書きさ **れる可能性があるので** 、この方法は推奨されません。

### フォルダーに許可するテンプレートの設定 {#configure-allowed-templates-folder}

>[!NOTE]
>
>アップグレード時に値が上書きされないので ****、「許可されているテンプレート」を指定する場合は、この方法をお勧めします。

1. 必要な&#x200B;**[!UICONTROL エクスペリエンスフラグメント]**&#x200B;フォルダーに移動します。

1. フォルダを選択し、[プロパティ] **[!UICONTROL を選択しま]**&#x200B;す。

1. 「許可されているテンプレート」フィールドで、必要なテンプレートを取得するた **[!UICONTROL めの正規表現を指定]** します。

   次に例を示します。
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   ![エクスペリエンスフラグメントプロパティ — 許可されたテンプレート](assets/xf-folders-templates.png)

1. Select **[!UICONTROL Save and Close]**.

### インスタンスに許可するテンプレートの設定 {#configure-allowed-templates-instance}

>[!CAUTION]
>
>アップグレード時に指定したテンプレートが上書きさ **[!UICONTROL れる場合があるので]** 、この方法で許可されているテンプレートを変更することはお勧めしません。
>
>このダイアログは、情報を提供する目的でのみ使用してください。

1. Navigate to the required **[!UICONTROL Experience Fragments]** console.

1. 「**[!UICONTROL 設定オプション]**」をクリックします。

   ![設定ボタン](assets/xf-folders-18.png)

1. **[!UICONTROL エクスペリエンスフラグメントを設定]**&#x200B;ダイアログで、必要なテンプレートを指定します。

   ![エクスペリエンスフラグメントを設定](assets/xf-folders-19.png)

1. 「**[!UICONTROL 保存]**」をクリックします。

## エクスペリエンスフラグメントの作成 {#creating-an-experience-fragment}

エクスペリエンスフラグメントを作成するには、次の手順に従います。

1. Select **[!UICONTROL Experience Fragments]** from the Global Navigation.

   ![screen_shot_2018-04-05at92221am1](assets/screen_shot_2018-04-05at92221am1.png)

1. 目的のフォルダーに移動し、「作成」を選 **[!UICONTROL 択します]**。

1. 「エクスペリエ **[!UICONTROL ンスフラグメント]** 」を選択して **[!UICONTROL 、エクスペリエンスフラグメ]** ントを作成ウィザードを開きます。

   適切な&#x200B;**[!UICONTROL テンプレート]**&#x200B;を選択して、「**[!UICONTROL 次へ]**」を選択します。

   ![xf-authoring-02](assets/xf-authoring-02.png)


1. エクスペリエンスフラグメントの&#x200B;**[!UICONTROL プロパティ]**&#x200B;を入力します。

   **[!UICONTROL タイトル]**&#x200B;は必須です。**[!UICONTROL 名前]**&#x200B;が空欄のままの場合、**[!UICONTROL タイトル]**&#x200B;から派生されます。

   ![xf-authoring-03](assets/xf-authoring-03.png)

1. 「**[!UICONTROL 作成]**」をクリックします。

   メッセージが表示されます。以下から選択します。

   * 「**[!UICONTROL 完了]**」を選択すると、コンソールに戻ります。
   * 「**[!UICONTROL 開く]**」を選択すると、フラグメントエディターを開きます。

## エクスペリエンスフラグメントの編集 {#editing-your-experience-fragment}

エクスペリエンスフラグメントエディターには、通常のページエディターと似た機能があります。See [Editing Page Content](/help/sites-authoring/editing-content.md) for more information on how to use it.

次の手順の例では、商品のティーザーを作成する方法を示します。

1. [コンポーネントブラウザー](/help/sites-authoring/author-environment-tools.md#components-browser)から&#x200B;**[!UICONTROL カテゴリティーザー]**&#x200B;をドラッグ＆ドロップします。

   ![xf-authoring-04](assets/xf-authoring-04.png)

1. コンポーネントツールバーから&#x200B;**[!UICONTROL 設定](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)**を選択します。
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
   * **[!UICONTROL バリエーションをライブコピーとして]**.

1. 必要なプロパティを定義します。

   * **[!UICONTROL テンプレート]**
   * **[!UICONTROL タイトル]**
   * **[!UICONTROL 名前]**（空欄のままの場合、タイトルから派生される）
   * **[!UICONTROL 説明]**
   * **[!UICONTROL バリエーションのタグ]**
   ![xf-authoring-06](assets/xf-authoring-07.png)

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

* マスターに移動：マスターバリエーションを新しいタブで開く
* 名前を変更
* 削除

![xf-authoring-16](assets/xf-authoring-16.png)

### 構築ブロックの使用 {#using-a-building-block}

任意のコンポーネントと同様に、構築ブロックをフラグメントの段落システムにドラッグできます。

## プレーン HTML レンディション {#the-plain-html-rendition}

Using the `.plain.` selector in the URL, you can access the plain HTML rendition.

これはブラウザーから利用できますが、主な目的は、他のアプリケーション（例えば、サードパーティ Web アプリ、カスタムモバイル実装など）が、URL のみを使用して、エクスペリエンスフラグメントのコンテンツに直接アクセスできるようにすることです。

プレーン HTML レンディションは、次のようなパスにプロトコル、ホストおよびコンテキストパスを追加します。

* のタイプ： `src`、 `href`または `action`

* or end with: `-src`, or `-href`

次に例を示します。

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>リンクは、常に、パブリッシュインスタンスを参照します。リンクは、サードパーティによって使用されることを意図しているので、オーサーインスタンスではなく、常にパブリッシュインスタンスから呼び出されます。

![xf-authoring-17](assets/xf-authoring-17.png)

## エクスペリエンスフラグメントの書き出し {#exporting-experience-fragments}

デフォルトでは、エクスペリエンスフラグメントは HTML 形式で配信され、AEM とサードパーティチャネルのどちらでも同じ様に使用できます。

Adobe targetへの書き出しには、HTMLが使用されます。 詳しくは、[Adobe Target とエクスペリエンスフラグメントの統合](/help/sites-administering/experience-fragments-target.md)を参照してください。

