---
title: コンテンツフラグメントの管理
seo-title: Managing Content Fragments
description: コンテンツフラグメントは アセットとして保存されるので、主にアセットコンソールから管理します。
seo-description: Content Fragments are stored as Assets, so are primarily managed from the Assets console.
uuid: 0659cf03-b4e8-4b8b-bec7-0082f980115a
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: da8f968b-91cc-45a8-ae4b-757b4f840b8e
exl-id: b21ba7a1-6e6f-4b95-9336-b49f7e932af5
feature: Content Fragments
role: User
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 59%

---

# コンテンツフラグメントの管理 {#managing-content-fragments}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!CAUTION]
>
>一部のコンテンツフラグメント機能には、 [AEM 6.4 Service Pack 2(6.4.2.0) 以降](/help/release-notes/sp-release-notes.md).

コンテンツフラグメントは **[!UICONTROL アセット]** として保存されるので、主に **[!UICONTROL アセット]** コンソールから管理します。

>[!NOTE]
>
>その後、コンテンツフラグメントはページのオーサリングで使用されます。参照 [コンテンツフラグメントを使用したページのオーサリング](/help/sites-authoring/content-fragments.md).

## コンテンツフラグメントの作成 {#creating-content-fragments}

### コンテンツモデルの作成 {#creating-a-content-model}

構造化コンテンツを含むコンテンツフラグメントを作成する前に、[コンテンツフラグメントモデル](content-fragments-models.md)を有効にして作成できます。

>[!NOTE]
>
>詳しくは、 [コンテンツフラグメントの開発](/help/sites-developing/customizing-content-fragments.md) を参照してください。シンプルなコンテンツフラグメントに使用します。

### コンテンツフラグメントの作成 {#creating-a-content-fragment}

コンテンツフラグメントの作成方法は（基本的に）シンプルなフラグメントと構造化されたフラグメントの両方で同じです。

1. フラグメントを作成する **[!UICONTROL Assets]** フォルダーに移動します。
1. 「**[!UICONTROL 作成]**」を選択し、「**[!UICONTROL コンテンツフラグメント]**」を選択して、ウィザードを開きます。
1. ウィザードの最初の手順では、新しいフラグメントの基盤を指定することを求められます。

   * 次のことが考えられます。

      * [](/help/sites-developing/content-fragment-templates.md)テンプレート - **[!UICONTROL 単純なフラグメント]**&#x200B;など
      * [モデル](content-fragments-models.md)  — 構造化コンテンツを必要とするフラグメントの作成に使用します。例： **空港** モデル
   * 使用可能なすべてのテンプレートとモデルが表示されます。

   選択した後、「**[!UICONTROL 次へ]**」を使用して続けます。

   ![cfm-6420-15](assets/cfm-6420-15.png)

1. 「**[!UICONTROL プロパティ]**」の手順で次を指定します。

   * **[!UICONTROL 基本]**

      * **[!UICONTROL タイトル]**

         フラグメントタイトル。

         必須です。

      * **[!UICONTROL 説明]**
      * **[!UICONTROL タグ]**
   * **[!UICONTROL 詳細]**

      * **[!UICONTROL 名前]**

         URL の作成に使用される名前です。

         必須。タイトルから自動的に派生しますが、変更が可能です。


1. 「**[!UICONTROL 作成]**」を選択して操作を完了してから、編集するためにフラグメントを&#x200B;**[!UICONTROL 開く]**&#x200B;か、「**[!UICONTROL 完了]**」でコンソールに戻ります。

## コンテンツフラグメントのアクション {#actions-for-a-content-fragment}

**[!UICONTROL Assets]** コンソールでは、次のいずれかからコンテンツフラグメントに対して様々なアクションを使用できます。

* ツールバーから。フラグメントを選択した後は、適切なアクションをすべて使用できます。
* 形式 [クイックアクション](/help/sites-authoring/basic-handling.md#quick-actions);個々のフラグメントカードで使用できるアクションのサブセット。

![cfm-6420-17](assets/cfm-6420-17.png)

フラグメントを選択して、次の適用可能なアクションを含むツールバーを表示します。

* **[!UICONTROL ダウンロード]**

   * フラグメントを ZIP ファイルとして保存します。要素、バリエーション、メタデータを含めるかどうかを定義できます。

* **[!UICONTROL 作成]**
* **[!UICONTROL チェックアウト]**
* **[!UICONTROL プロパティ]**

   * フラグメントのメタデータを表示または編集できます。

* **[!UICONTROL 編集]**

   * フラグメントの要素、バリエーション、および関連付けられているコンテンツやメタデータと共に[コンテンツを編集するためにフラグメントを開く](content-fragments-variations.md)ことができます。

* **[!UICONTROL タグを管理]**
* **[!UICONTROL コレクションに追加]**

   * フラグメントをコレクションに追加します。
   * これは、 [コレクションとフラグメントの関連付け](content-fragments-assoc-content.md#adding-associated-content).

* **[!UICONTROL コピー/貼り付け]**
* **[!UICONTROL 移動]**
* **[!UICONTROL クイック公開]**
* **[!UICONTROL 公開を管理]**
* **[!UICONTROL 削除]**

>[!NOTE]
>
>これらの多くは、[Assets](managing-assets-touch-ui.md) や [ デスクトップアプリケーション](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app.html)に対する標準的なアクションです。

## フラグメントエディターを開く {#opening-the-fragment-editor}

編集するためにフラグメントを開くには：

>[!CAUTION]
>
>コンテンツフラグメントを編集するには、 [適切な権限](/help/sites-developing/customizing-content-fragments.md#asset-permissions). 問題が発生している場合は、システム管理者に問い合わせてください。

1. **[!UICONTROL Assets]** コンソールを使用して、コンテンツフラグメントの場所に移動します。
1. 次のいずれかの方法で、フラグメントを編集用に開きます。

   * フラグメントまたはフラグメントリンクをクリックまたはタップします（これは、コンソール表示によって異なります）。
   * フラグメントを選択してから、ツールバーの「**[!UICONTROL 編集]**」を選択。

   フラグメントエディターが開きます。

   ![cfm-6420-18](assets/cfm-6420-18.png)

   >[!NOTE]
   >
   >1. フラグメントがコンテンツページで既に参照されている場合は、メッセージが表示されます。
   >
   >2. **[!UICONTROL サイドパネルを切り替え]**&#x200B;アイコンを使用してサイドパネルを非表示／表示できます。


1. サイドパネルのアイコンを使用して、3 つのモード間を移動します。

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

   最新の変更を保存し、エディターを終了します。

   >[!CAUTION]
   >
   >コンテンツフラグメントを編集するには、 [適切な権限](/help/sites-developing/customizing-content-fragments.md#asset-permissions). 問題が発生している場合は、システム管理者に問い合わせてください。

   >[!NOTE]
   >
   >を選択する前に、エディターに留まって一連の変更を加えることができます。 **[!UICONTROL 保存]**.

   >[!CAUTION]
   >
   >「**[!UICONTROL 保存]**」では、変更を保存するだけでなく、参照を更新し、必要に応じて Dispatcher がフラッシュされます。これらの変更の処理には時間がかかる場合があります。 このため、大規模/複雑/負荷の高いシステムにパフォーマンスが影響を与える可能性があります。
   >
   >
   >ご使用の際は、次の点に留意してください **[!UICONTROL 保存]** その後、フラグメントエディターにすばやく再度入力して、さらに変更を加えて保存します。

* **[!UICONTROL キャンセル]**

   最新の変更を保存せずにエディターを終了します。

コンテンツフラグメントの編集中に、AEMは自動的にバージョンを作成し、 **[!UICONTROL キャンセル]** 変更：

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

フラグメントを開いたら、 [バリエーション](content-fragments-variations.md) タブを使用して、コンテンツを作成します。

## フラグメント内のバリエーションの作成と管理 {#creating-and-managing-variations-within-your-fragment}

プライマリコンテンツを作成したら、そのコンテンツの[バリエーション](content-fragments-variations.md)を作成して管理できます。

## コンテンツとフラグメントの関連付け {#associating-content-with-your-fragment}

また、 [コンテンツを関連付け](content-fragments-assoc-content.md) フラグメントを含む これにより、アセット（画像）をフラグメントと共に（オプションで）コンテンツページに追加する際に使用できるようにする接続が提供されます。

## フラグメントのメタデータ（プロパティ）の表示と編集 {#viewing-and-editing-the-metadata-properties-of-your-fragment}

「[[!UICONTROL メタデータ]](content-fragments-metadata.md)」タブを使用し、フラグメントのプロパティを表示して編集できます。

## コンテンツフラグメントのタイムライン {#timeline-for-content-fragments}

標準オプションに加えて、 [タイムライン](managing-assets-touch-ui.md#timeline) には、コンテンツフラグメントに固有の情報とアクションの両方が用意されています。

* バージョン、コメント、注釈に関する情報の表示
* バージョンに対するアクション

   * **[[!UICONTROL このバージョンに戻る]](#reverting-to-a-version)**（既存のフラグメントを選択してから特定のバージョンを選択）
   * **[[!UICONTROL 現在のバージョンと比較]](#comparing-fragment-versions)**（既存のフラグメントを選択してから特定のバージョンを選択）
   * **[!UICONTROL ラベル]**&#x200B;や&#x200B;**[!UICONTROL コメント]**&#x200B;の追加（既存のフラグメントを選択してから特定のバージョンを選択）
   * **[!UICONTROL バージョンとして保存]** （既存のフラグメントを選択してから、タイムラインの下部にある上向き矢印を選択）

* 注釈のアクション

   * **[!UICONTROL 削除]**

>[!NOTE]
>
>コメントは次のとおりです。
>
>* すべてのアセットの標準機能
>* タイムラインで作成
>* フラグメントアセットに関連
>
>注釈（コンテンツフラグメント用）は次のとおりです。
>
>* フラグメントエディターに入力
>* フラグメント内の選択したテキストセグメントに固有


次に例を示します。

![cfm-6420-19](assets/cfm-6420-19.png)

## フラグメントのバージョンの比較 {#comparing-fragment-versions}

この **[!UICONTROL 現在と比較]** アクションは、 [[!UICONTROL タイムライン]](https://helpx.adobe.com/experience-manager/6-3/assets/using/content-fragments-managing.html#timeline-for-content-fragments) 特定のバージョンを選択した後。

開く：

* **[!UICONTROL 現在]**（最新）のバージョン（左）

* 選択されたバージョン **v&lt;*x.y*>**（右）

これらは並べて表示され、次の場所にあります。

* 違いが強調表示されます

   * 削除されたテキスト — 赤
   * 挿入されたテキスト - 緑
   * 置換されたテキスト — 青

* 全画面表示アイコンを使用すれば、どちらかのバージョンで開いた後で、並列表示に切り替えることができます
* 以下が可能です。 **[!UICONTROL 元に戻す]** 特定のバージョンに
* **[!UICONTROL 完了]** コンソールに戻ります

>[!NOTE]
>
>フラグメントの比較時にフラグメントコンテンツを編集することはできません。

![cfm-6420-20](assets/cfm-6420-20.png)

## 特定のバージョンへの復帰   {#reverting-to-a-version}

フラグメントの特定のバージョンに戻すことができます。

* 直接 [[!UICONTROL タイムライン]](content-fragments-managing.md#timeline-for-content-fragments).

   必要なバージョンを選択した後、「**[!UICONTROL このバージョンに戻す]**」アクションを選択します。

* [あるバージョンと現在のバージョンを比較](content-fragments-managing.md#comparing-fragment-versions)し、選択したバージョンに&#x200B;**[!UICONTROL 戻す]**&#x200B;ことができます。

## フラグメントの公開と参照 {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>フラグメントがモデルに基づいている場合、 [モデルが公開されました](content-fragments-models.md#publishing-a-content-fragment-model).
>
>まだ公開されていないモデルのコンテンツフラグメントを公開すると、選択リストにそのことが示され、モデルがフラグメントと共に公開されます。

コンテンツフラグメントをパブリッシュ環境で使用するには、公開する必要があります。 次の方法で公開できます。

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
   >この **[!UICONTROL 削除]** アクションは、クイックアクションとして使用できません。

1. ツールバーから「**[!UICONTROL 削除]**」を選択します。
1. 「**[!UICONTROL 削除]**」アクションを確認します。

   >[!CAUTION]
   >
   >フラグメントが既にページで参照されている場合は、警告メッセージが表示されます。「**[!UICONTROL 削除を強制]**」を選択して続行を確認する必要があります。フラグメントはコンテンツフラグメントコンポーネントと一緒に、すべてのコンテンツページから削除されます。
