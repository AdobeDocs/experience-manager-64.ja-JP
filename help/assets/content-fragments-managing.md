---
title: コンテンツフラグメントの管理
seo-title: コンテンツフラグメントの管理
description: コンテンツフラグメントは Assets として保存されるので、主に Assets コンソールから管理します。
seo-description: コンテンツフラグメントは Assets として保存されるので、主に Assets コンソールから管理します。
uuid: 0659cf03-b4e8-4b8b-bec7-0082f980115a
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: da8f968b-91cc-45a8-ae4b-757b4f840b8e
exl-id: b21ba7a1-6e6f-4b95-9336-b49f7e932af5
feature: コンテンツフラグメント
role: Business Practitioner
translation-type: tm+mt
source-git-commit: f9faa357f8de92d205f1a297767ba4176cfd1e10
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 98%

---

# コンテンツフラグメントの管理 {#managing-content-fragments}

>[!CAUTION]
>
>一部のコンテンツフラグメント機能では、[AEM 6.4 Service Pack 2 (6.4.2.0)以降](/help/release-notes/sp-release-notes.md)のアプリケーションが必要です。

コンテンツフラグメントは **[!UICONTROL Assets]** として保存されるので、主に **[!UICONTROL Assets]** コンソールから管理します。

>[!NOTE]
>
>コンテンツフラグメントは、ページのオーサリングで使用します。[コンテンツフラグメントを使用したページのオーサリング](/help/sites-authoring/content-fragments.md)を参照してください。

## コンテンツフラグメントの作成 {#creating-content-fragments}

### コンテンツモデルの作成 {#creating-a-content-model}

構造化コンテンツを含むコンテンツフラグメントを作成する前に、[コンテンツフラグメントモデル](content-fragments-models.md)を有効にして作成できます。

>[!NOTE]
>
>単純なコンテンツフラグメントに使用されるテンプレートについて詳しくは、[コンテンツフラグメントの開発](/help/sites-developing/customizing-content-fragments.md)を参照してください。

### コンテンツフラグメントの作成 {#creating-a-content-fragment}

コンテンツフラグメントの作成方法は基本的に単純なフラグメントと構造化フラグメントで同じです。

1. フラグメントを作成する **[!UICONTROL Assets]** フォルダーに移動します。
1. 「**[!UICONTROL 作成]**」を選択し、「**[!UICONTROL コンテンツフラグメント]**」を選択して、ウィザードを開きます。
1. ウィザードの最初の手順では、新しいフラグメントの基盤を指定することを求められます。

   * 以下を指定します。

      * [](/help/sites-developing/content-fragment-templates.md)テンプレート - **[!UICONTROL 単純なフラグメント]**&#x200B;など
      * [モデル](content-fragments-models.md) - **空港**&#x200B;モデルなど、構造化コンテンツを必要とするフラグメントの作成に使用されます
   * 使用可能なテンプレートとモデルがすべて表示されます。

   選択した後、「**[!UICONTROL 次へ]**」を使用して続けます。

   ![cfm-6420-15](assets/cfm-6420-15.png)

1. 「**[!UICONTROL プロパティ]**」の手順で次を指定します。

   * **[!UICONTROL 基本]**

      * **[!UICONTROL タイトル]**

          フラグメントタイトル。

          必須です。

      * **[!UICONTROL 説明]**
      * **[!UICONTROL タグ]**
   * **[!UICONTROL アドバンス]**

      * **[!UICONTROL 名前]**

         URL の作成に使用される名前です。

          必須。タイトルから自動的に派生しますが、変更が可能です。


1. 「**[!UICONTROL 作成]**」を選択して操作を完了してから、編集するためにフラグメントを&#x200B;**[!UICONTROL 開く]**&#x200B;か、「**[!UICONTROL 完了]**」でコンソールに戻ります。

## コンテンツフラグメントのアクション {#actions-for-a-content-fragment}

**[!UICONTROL Assets]** コンソールでは、次のいずれかからコンテンツフラグメントに対して様々なアクションを使用できます。

* ツールバーから。フラグメントを選択すると、該当するすべてのアクションを使用できるようになります。
* [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions)として。個別のフラグメントカードに使用可能なアクションのサブセット。

![cfm-6420-17](assets/cfm-6420-17.png)

フラグメントを選択して、次の適用可能なアクションを含むツールバーを表示します。

* **[!UICONTROL ダウンロード]**

   * フラグメントを ZIP ファイルとして保存します。要素、バリエーション、メタデータを含めるかどうかを定義できます。

* **[!UICONTROL 作成]**
* **[!UICONTROL チェックアウト]**
* **[!UICONTROL プロパティ]**

   * フラグメントのメタデータを表示したり、編集したりできます。

* **[!UICONTROL 編集]**

   * フラグメントの要素、バリエーション、および関連付けられているコンテンツやメタデータと共に[コンテンツを編集するためにフラグメントを開く](content-fragments-variations.md)ことができます。

* **[!UICONTROL タグを管理]**
* **[!UICONTROL コレクションに追加]**

   * フラグメントをコレクションに追加します。
   * これは、[コレクションをフラグメントと関連付ける](content-fragments-assoc-content.md#adding-associated-content)際に実行できます。

* **[!UICONTROL コピー／貼り付け]**
* **[!UICONTROL 移動]**
* **[!UICONTROL クイック公開]**
* **[!UICONTROL 公開を管理]**
* **[!UICONTROL 削除]**

>[!NOTE]
>
>これらの多くは、[Assets](managing-assets-touch-ui.md) や [ デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)に対する標準的なアクションです。

## フラグメントエディターを開く {#opening-the-fragment-editor}

編集するためにフラグメントを開くには：

>[!CAUTION]
>
>コンテンツフラグメントを編集するには、[適切な権限](/help/sites-developing/customizing-content-fragments.md#asset-permissions)が必要になります。問題が発生している場合は、システム管理者にお問い合わせください。

1. **[!UICONTROL Assets]** コンソールを使用して、コンテンツフラグメントの場所に移動します。
1. フラグメントを開いて編集するには、以下のいずれかを実行します。

   * フラグメントまたはフラグメントリンクをクリック／タップ（これはコンソールビューによって異なります）。
   * フラグメントを選択してから、ツールバーの「**[!UICONTROL 編集]**」を選択。

   フラグメントエディターが開きます。

   ![cfm-6420-18](assets/cfm-6420-18.png)

   >[!NOTE]
   >
   >1. フラグメントがコンテンツページで既に参照されている場合は、メッセージが表示されます。
      >
      >
   2. **[!UICONTROL サイドパネルを切り替え]**&#x200B;アイコンを使用してサイドパネルを非表示／表示できます。


1. サイドパネルのアイコンを使用して、3 つのモデル間を移動します。

   * バリエーション：[コンテンツの編集](#editing-the-content-of-your-fragment)と[バリエーションの管理](#creating-and-managing-variations-within-your-fragment)
   * [注釈](content-fragments-variations.md#annotating-a-content-fragment)
   * [関連コンテンツ](#associating-content-with-your-fragment)
   * [メタデータ](#viewing-and-editing-the-metadata-properties-of-your-fragment)

   ![cfm-10](assets/cfm-10.png)

1. 変更を加えた後、必要に応じて「**[!UICONTROL 保存して閉じる]**」または「**[!UICONTROL キャンセル]**」をクリックします。

   >[!NOTE]
   >
   >「**[!UICONTROL 保存して閉じる]**」または「**[!UICONTROL キャンセル]**」のどちらをクリックした場合も、エディターが終了します。これらの両方のオプションがコンテンツフラグメントにどのように動作するかについて詳しくは、[保存、キャンセルおよびバージョン](#save-cancel-and-versions)を参照してください。

## 保存、キャンセルおよびバージョン {#save-cancel-and-versions}

>[!NOTE]
>
>バージョン[を作成／比較したり元に戻したりする操作は、タイムラインから](https://helpx.adobe.com/experience-manager/6-3/assets/using/content-fragments-managing.html#timeline-for-content-fragments)もおこなえます。

エディターには次の 2 つのオプションがあります。

* **[!UICONTROL 保存]**

   最後の変更を保存し、エディターを終了します。

   >[!CAUTION]
   >
   >コンテンツフラグメントを編集するには、[適切な権限](/help/sites-developing/customizing-content-fragments.md#asset-permissions)が必要になります。問題が発生している場合は、システム管理者にお問い合わせください。

   >[!NOTE]
   >
   >エディターを開いたまま、一連の変更を加えてから「**[!UICONTROL 保存]**」を選択することもできます。

   >[!CAUTION]
   >
   >「**[!UICONTROL 保存]**」では、変更を保存するだけでなく、参照を更新し、必要に応じて Dispatcher がフラッシュされます。これらの変更が処理されるまでに時間がかかることがあります。このため、大きなシステムや複雑なシステム、高負荷のシステムのパフォーマンスに影響することがあります。
   >
   >
   >「**[!UICONTROL 保存]**」を使用する際はこの点に留意し、フラグメントエディターを迅速に開いて、変更をおこない、保存してください。

* **[!UICONTROL キャンセル]**

   最後の変更を保存せずにエディターを終了します。

コンテンツフラグメントを編集する際には、AEM によって自動的にバージョンが作成されます。これにより、変更内容を&#x200B;**[!UICONTROL キャンセル]**&#x200B;しても以前のコンテンツを復元できるようになります。

1. コンテンツフラグメントを開いて編集しようとすると、AEM は&#x200B;*編集セッション*&#x200B;が存在しているかどうかを示す cookie ベースのトークンの存在を確認します。

   1. トークンが見つかると、そのフラグメントは既存の編集セッションの一部であると見なされます。
   1. トークンがないときにユーザーが編集を開始すると、バージョンが作成され、この新しい編集セッションのトークンがクライアントに送られ、cookie に保存されます&#x200B;*。*

1. アクティブな編集セッションがあるとき、編集中のコンテンツは自動的に 600 秒ごとに保存されます（デフォルト）*。*

   >[!NOTE]
   >
   >自動保存間隔は `/conf` メカニズムを使用して設定できます。
   >
   >デフォルト値については、以下を参照してください。
   >
   >`/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

1. ユーザーが「**[!UICONTROL キャンセル]**」を選択して編集をキャンセルすると、編集セッションの開始時に作成されたバージョンが復元され、トークンが削除されて編集セッションが終了します。
1. ユーザーが編集内容の「**[!UICONTROL 保存]**」を選択すると、更新された要素とバリエーションが保存され、トークンが削除されて編集セッションが終了します。

## フラグメントのコンテンツの編集 {#editing-the-content-of-your-fragment}

フラグメントを開いたら、「[バリエーション](content-fragments-variations.md)」タブを使用してコンテンツをオーサリングできます。

## フラグメント内のバリエーションの作成と管理  {#creating-and-managing-variations-within-your-fragment}

マスターコンテンツを作成したら、そのコンテンツの[バリエーション](content-fragments-variations.md)を作成して管理できます。

## コンテンツをフラグメントと関連付ける  {#associating-content-with-your-fragment}

フラグメントに[コンテンツを関連付ける](content-fragments-assoc-content.md)こともできます。これにより関連性を付加して、フラグメントをコンテンツページに追加するときに、アセット（画像など）を（オプションで）フラグメントと一緒に使用できるようになります。

## フラグメントのメタデータ（プロパティ）の表示と編集  {#viewing-and-editing-the-metadata-properties-of-your-fragment}

「[[!UICONTROL メタデータ]](content-fragments-metadata.md)」タブを使用し、フラグメントのプロパティを表示して編集できます。

## コンテンツフラグメントのタイムライン  {#timeline-for-content-fragments}

[タイムライン](managing-assets-touch-ui.md#timeline)では標準のオプションに加え、コンテンツフラグメントに固有の情報とアクションの両方が提供されます。

* バージョン、コメントおよび注釈に関する情報の表示
* バージョンに関するアクション

   * **[[!UICONTROL このバージョンに戻る]](#reverting-to-a-version)**（既存のフラグメントを選択してから特定のバージョンを選択）
   * **[[!UICONTROL 現在のバージョンと比較]](#comparing-fragment-versions)**（既存のフラグメントを選択してから特定のバージョンを選択）
   * **[!UICONTROL ラベル]**&#x200B;や&#x200B;**[!UICONTROL コメント]**&#x200B;の追加（既存のフラグメントを選択してから特定のバージョンを選択）
   * **[!UICONTROL バージョンとして保存]**（既存のフラグメントを選択してからタイムライン下部の上矢印を選択）

* 注釈に関するアクション

   * **[!UICONTROL 削除]**

>[!NOTE]
>
>コメントは次のとおりです。
>
>* すべてのアセットの標準機能
>* タイムラインで追加
>* フラグメントアセットに関連付けられる

>
>
注釈（コンテンツフラグメント用）は次のとおりです。
>
>* フラグメントエディターで入力
>* フラグメント内の選択されたテキストセグメントに固有


次に例を示します。

![cfm-6420-19](assets/cfm-6420-19.png)

## フラグメントのバージョンの比較 {#comparing-fragment-versions}

特定のバージョンを選択したら、「[[!UICONTROL タイムライン]」から「**[!UICONTROL 現在のバージョンと比較]**」アクションを利用できるようになります。](https://helpx.adobe.com/experience-manager/6-3/assets/using/content-fragments-managing.html#timeline-for-content-fragments)

これにより、次の情報が表示されます。

* **[!UICONTROL 現在]**（最新）のバージョン（左）

* 選択されたバージョン **v&lt;*x.y*>**（右）

これらは左右に並んで表示されます。この画面について以下で説明します。

* すべての相違点がハイライト表示されます

   * 削除されたテキスト - 赤
   * 挿入されたテキスト - 緑
   * 置き換えられたテキスト - 青

* 全画面表示アイコンを使用すれば、どちらかのバージョンで開いた後で、並列表示に切り替えることができます
* 特定のバージョンに&#x200B;**[!UICONTROL 戻す]**&#x200B;ことができます
* 「**[!UICONTROL 完了]**」を選択すると、コンソールに戻ります

>[!NOTE]
>
>フラグメントの比較中にフラグメントコンテンツを編集することはできません。

![cfm-6420-20](assets/cfm-6420-20.png)

## 特定のバージョンへの復帰 {#reverting-to-a-version}

次の方法で特定のバージョンのフラグメントに戻すことができます。

* 直接[[!UICONTROL タイムライン]](content-fragments-managing.md#timeline-for-content-fragments)から。

   必要なバージョンを選択した後、「**[!UICONTROL このバージョンに戻す]**」アクションを選択します。

* [あるバージョンと現在のバージョンを比較](content-fragments-managing.md#comparing-fragment-versions)し、選択したバージョンに&#x200B;**[!UICONTROL 戻す]**&#x200B;ことができます。

## フラグメントの公開と参照 {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>フラグメントがモデルに基づいている場合、その[モデルが公開されている](content-fragments-models.md#publishing-a-content-fragment-model)ことを確認してください。
>
>まだ公開されていないモデルのコンテンツフラグメントを公開すると、選択リストにそのことが示され、モデルがフラグメントと共に公開されます。

コンテンツフラグメントを使用するには、パブリッシュ環境で公開する必要があります。次の方法で公開できます。

* 作成後に **[!UICONTROL Assets]** コンソールから。
* [フラグメントを使用するページを公開](/help/sites-authoring/content-fragments.md#publishing)するとき。フラグメントはページ参照にリスト表示されます。

>[!CAUTION]
>
>フラグメントが公開または参照（あるいは両方）された後に、作成者がフラグメントを開いて編集しようとすると警告が表示され、フラグメントを変更すると、参照されているページにも影響が及ぶことが警告されます。

## フラグメントの削除 {#deleting-a-fragment}

フラグメントを削除するには：

1. **[!UICONTROL Assets]** コンソールで、コンテンツフラグメントの場所に移動します。
1. フラグメントを選択します。

   >[!NOTE]
   >
   >**[!UICONTROL 削除]**&#x200B;アクションはクイックアクションとして実行できません。

1. ツールバーから「**[!UICONTROL 削除]**」を選択します。
1. 「**[!UICONTROL 削除]**」アクションを確認します。

   >[!CAUTION]
   >
   >フラグメントが既にページで参照されている場合は、警告メッセージが表示されます。「**[!UICONTROL 削除を強制]**」を選択して続行を確認する必要があります。フラグメントはコンテンツフラグメントコンポーネントと一緒に、すべてのコンテンツページから削除されます。
