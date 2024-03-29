---
title: ページの公開
seo-title: Publishing Pages
description: ページの公開
seo-description: null
uuid: 1222859d-ef8d-462e-a125-b76e6cfec26d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8f2714bc-9d6c-4e6f-97a1-3b4f977348c5
exl-id: 3de608f3-569f-438d-8ce7-24e82e5c1ec6
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 61%

---

# ページの公開 {#publishing-pages}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

オーサー環境でコンテンツを作成およびレビューしたら、目標は次のとおりです。 [公開 Web サイトで利用できるようにする](/help/sites-authoring/author.md#concept-of-authoring-and-publishing) （パブリッシュ環境）。

これは、ページの公開と呼ばれます。 パブリッシュ環境からページを削除する場合は、ページの非公開と呼ばれます。ページの公開と非公開を行う場合、ページを削除するまで、オーサー環境では引き続き変更を加えることができます。

また、ページの公開/非公開は、即座におこなうことも、後で事前定義済みの日時におこなうこともできます。

>[!NOTE]
>
>公開に関連する特定の用語が混同される場合があります。
>
>* **公開／非公開**
   >  環境でコンテンツを公開する（または非公開にする）アクションに対して主に使用される用語です。
>
>* **アクティブ化／非アクティブ化**
   >  公開／非公開と同義です。
>
>* **レプリケート／レプリケーション**
   >  公開やユーザーコメントのリバースレプリケーションの際などに行われる、環境間でのデータ（ページコンテンツ、ファイル、コード、ユーザーコメントなど）の移動を表す技術用語です。
>


>[!NOTE]
>
>特定のページを公開するために必要な特権がない場合。
>
>* ワークフローがトリガーされ、適切なユーザーに公開リクエストが通知されます。
>* この [ワークフローはカスタマイズされている可能性があります](/help/sites-developing/workflows-models.md) 開発チームによって。
>* ワークフローがトリガーされたことを通知するメッセージが少しの間表示されます。
>


## ページの公開  {#publishing-pages-2}

場所に応じて、次から公開できます。

* [ページエディターから](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)
* [サイトコンソールから](/help/sites-authoring/publishing-pages.md#publishing-from-the-console)

### エディターからの公開 {#publishing-from-the-editor}

ページを編集している場合、エディターから直接公開できます。

1. **ページ情報**&#x200B;アイコンを選択してメニューを開き、「**ページを公開**」オプションを選択します。

   ![screen_shot_2018-03-21at152734](assets/screen_shot_2018-03-21at152734.png)

1. 公開が必要な参照がページに含まれているかどうかに応じて、次の操作を行います。

   * 公開する参照がない場合、ページが直接公開されます。
   * 公開が必要な参照がページに含まれている場合は、それらのリストが&#x200B;**公開**&#x200B;ウィザードに表示され、ウィザードで次のいずれかを実行できます。

      * ページと一緒に公開するアセットやタグなどを指定し、「**公開**」を使用してプロセスを完了します。
      * 「**キャンセル**」を使用してアクションを中止します。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. 「**公開**」を選択して、パブリッシュ環境にページをレプリケートします。ページエディターに、公開アクションを確認する情報バナーが表示されます。

   ![screen_shot_2018-03-21at152840](assets/screen_shot_2018-03-21at152840.png)

   コンソールで同じページを表示すると、更新された公開ステータスが表示されます。

   ![screen_shot_2018-03-21at152951](assets/screen_shot_2018-03-21at152951.png)

>[!NOTE]
>
>エディターからの公開は、浅い公開です。つまり、選択したページだけが公開され、子ページは公開されません。

>[!NOTE]
>
>エディターで[エイリアス](/help/sites-authoring/editing-page-properties.md#advanced)を使用してアクセスしたページは公開できません。エディターの「公開」オプションは、実際のパスからアクセスするページでのみ使用できます。

### コンソールからの公開 {#publishing-from-the-console}

サイトコンソールには、2 つの公開オプションがあります。

* [クイック公開](/help/sites-authoring/publishing-pages.md#quick-publish)
* [公開を管理](/help/sites-authoring/publishing-pages.md#manage-publication)

#### クイック公開 {#quick-publish}

**クイック公開** は単純な場合に使用し、選択したページを直ちに公開します。操作は必要ありません。 このため、非公開の参照も自動的に公開されます。

クイック公開でページを公開するには：

1. サイトコンソールで 1 つ以上のページを選択し、「**クイック公開**」ボタンをクリックします。

   ![screen_shot_2018-03-21at153115](assets/screen_shot_2018-03-21at153115.png)

1. クイック公開ダイアログで、「**公開**」をクリックして公開を確認するか、「**キャンセル**」をクリックしてキャンセルします。すべての非公開の参照も自動的に公開されることに注意してください。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. ページが公開されると、公開を確認するアラートが表示されます。

>[!NOTE]
>
>クイック公開は、浅い公開です。つまり、選択したページ（複数可）のみが公開され、子ページは公開されません。

#### 公開を管理 {#manage-publication}

**公開を管理**&#x200B;には、クイック公開よりも多くのオプションがあります。子ページを含めたり、参照をカスタマイズしたり、使用可能なワークフローを開始したり、後日公開するためのオプションを提供したりします。

「公開を管理」を使用してページを公開または非公開にするには：

1. サイトコンソールで 1 つ以上のページを選択し、 **公開を管理** 」ボタンをクリックします。

   ![screen_shot_2018-03-21at153309](assets/screen_shot_2018-03-21at153309.png)

1. **公開を管理**&#x200B;ウィザードが起動します。最初のステップは **オプション**&#x200B;を使用すると、次のことができます。

   * 選択したページの公開または非公開を選択する。
   * 今すぐ実行するか、後日実行するかを選択します。

   後で公開すると、選択したページを指定した時間に公開するワークフローが開始されます。 逆に、後で非公開にすると、特定の時間に選択したページを非公開にするワークフローが開始されます。

   公開／非公開を後からキャンセルする場合は、[ワークフローコンソール](/help/sites-administering/workflows.md)に移動して、対応するワークフローを終了します。

   ![chlimage_1-52](assets/chlimage_1-52.png)

   「**次へ**」をクリックして次に進みます。

1. 公開を管理ウィザードの次の手順の&#x200B;**範囲**&#x200B;では、子ページを含めたり、参照を含めたりするなど、公開／非公開の範囲を定義できます。

   ![screen_shot_2018-03-21at153354](assets/screen_shot_2018-03-21at153354.png)

   公開を管理ウィザードを開始する前に選択し忘れた場合は、「**コンテンツを追加**」ボタンを使用して、公開するページのリストにページを追加できます。

   「コンテンツを追加」ボタンをクリックすると、[パスブラウザー](/help/sites-authoring/author-environment-tools.md#path-browser)が開き、コンテンツを選択できます。

   必要なページを選択し、「**選択**」をクリックしてコンテンツをウィザードに追加するか、「キャンセル」をクリックして選択をキャンセルして、ウィザードに戻ります。

   ウィザードに戻ると、リスト内の項目を選択して、次のようなその他のオプションを設定できます。

   * 子を含めます。
   * 選択範囲から削除します。
   * 公開済みの参照を管理します。

   ![screen_shot_2018-03-21at153450](assets/screen_shot_2018-03-21at153450.png)

   クリック **子を含める** ダイアログが開き、次の操作が可能になります。

   * 直近の子のみを含める。
   * 変更されたページのみを含める。
   * 既に公開済みのページのみを含める。

   クリック **追加** をクリックし、選択オプションに基づいて、公開または非公開にするページのリストに子ページを追加します。 「**キャンセル**」をクリックすると、選択がキャンセルされ、ウィザードに戻ります。

   ![chlimage_1-53](assets/chlimage_1-53.png)

   ウィザードに戻ると、子を含めるダイアログでのオプションの選択に基づいて追加されたページが表示されます。

   ページを選択して「**公開済みの参照**」ボタンをクリックすると、ページに対して公開または非公開にする参照を表示および変更できます。

   ![screen_shot_2018-03-21at153801](assets/screen_shot_2018-03-21at153801.png)

   この **公開済みの参照** ダイアログには、選択したコンテンツの参照が表示されます。 デフォルトでは、これらはすべて選択され、公開/非公開にされますが、「 」をオフにして選択を解除し、アクションに含めないようにすることができます。

   クリック **完了** 変更を保存するか、 **キャンセル** をクリックして選択をキャンセルし、ウィザードに戻ります。

   ![screen_shot_2018-03-21at153824](assets/screen_shot_2018-03-21at153824.png)

   ウィザードに戻ると、「**参照**」列が更新されて、公開または非公開にする参照の選択が反映されます。

   ![screen_shot_2018-03-21at153925](assets/screen_shot_2018-03-21at153925.png)

1. 「**公開**」をクリックして完了します。

   サイトコンソールに戻ると、公開を確認する通知メッセージが表示されます。

   ![screen_shot_2018-03-21at153951](assets/screen_shot_2018-03-21at153951.png)

1. 公開したページがワークフローに関連付けられている場合、公開ウィザードの最後の&#x200B;**ワークフロー**&#x200B;ステップに表示されます。

   >[!NOTE]
   >
   >**ワークフロー**&#x200B;手順は、ユーザーの権限に基づいて表示されます。詳しくは、公開権限に関する[このページの前述の注意事項](/help/sites-authoring/publishing-pages.md)、[ワークフローへのアクセスの管理](/help/sites-administering/workflows-managing.md)および[ページへのワークフローの適用](/help/sites-authoring/workflows-applying.md)を参照してください。

   リソースは、トリガーされたワークフローによってグループ化され、次の各オプションが提供されます。

   * ワークフローのタイトルを定義します。
   * ワークフローに含まれる場合、ワークフローパッケージを維持する [マルチリソースのサポート](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).
   * ワークフローパッケージを維持するオプションが選択されている場合、ワークフローパッケージのタイトルを定義する。

   クリック **公開** または「**後で公開**」をクリックして、公開を完了します。

   ![chlimage_1-54](assets/chlimage_1-54.png)

## ページを非公開にする {#unpublishing-pages}

ページを非公開にすると、そのページがパブリッシュ環境から削除され、読者に公開されなくなります。

[公開と同様の方法](/help/sites-authoring/publishing-pages.md#publishing-pages)で、1 つ以上のページを非公開にすることができます。

* [ページエディターから](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-editor)
* [サイトコンソールから](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-console)

### エディターから非公開にする {#unpublishing-from-the-editor}

ページの編集時に、そのページを非公開にする場合は、「 **ページを非公開にする** 内 **ページ情報** メニューは、 [ページを公開](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor).

>[!NOTE]
>
>エディターで[エイリアス](/help/sites-authoring/editing-page-properties.md#advanced)を使用してアクセスしたページは、非公開にすることができません。エディターの「公開」オプションは、実際のパスからアクセスするページでのみ使用できます。

### コンソールから非公開にする {#unpublishing-from-the-console}

[「公開を管理」オプションを使用して公開する](/help/sites-authoring/publishing-pages.md#manage-publication)場合と同様に、「公開を管理」オプションを使用して非公開にできます。

1. サイトコンソールで 1 つ以上のページを選択し、 **公開を管理** 」ボタンをクリックします。
1. **公開を管理**&#x200B;ウィザードが起動します。最初の手順の&#x200B;**オプション**&#x200B;で、デフォルトオプションの&#x200B;**公開**&#x200B;の代わりに&#x200B;**非公開**&#x200B;を選択します。

   ![chlimage_1-55](assets/chlimage_1-55.png)

   後で公開することを選択するとこのバージョンのページを公開するワークフローが指定した時間に開始されるのと同じように、後でアクティベートを解除することを選択すると、選択したページを非公開にするワークフローが特定の時間に開始されます。

   公開／非公開を後からキャンセルする場合は、[ワークフローコンソール](/help/sites-administering/workflows.md)に移動して、対応するワークフローを終了します。

1. 非公開の操作を完了するには、ウィザードを続行します。 [ページを公開](/help/sites-authoring/publishing-pages.md#manage-publication).

## ツリーの公開と非公開 {#publishing-and-unpublishing-a-tree}

多数のコンテンツページを入力または更新した場合（すべて同じルートページの下に存在）、ツリー全体を 1 回の操作で簡単に公開できます。

サイトコンソールにある「[公開を管理](/help/sites-authoring/publishing-pages.md#manage-publication)」オプションを使用すると、これを行うことができます。

1. サイトコンソールで、公開または非公開にするツリーのルートページを選択し、「 」を選択します **公開を管理**.
1. **公開を管理**&#x200B;ウィザードが起動します。公開または非公開にするタイミングと、実行するタイミングを選択して、 **次へ** をクリックして続行します。
1. 内 **範囲** ステップで、ルートページを選択し、 **子を含める**.

   ![chlimage_1-56](assets/chlimage_1-56.png)

1. 内 **子を含める** ダイアログで、次のオプションをオフにします。

   * 直近の子のみを含める
   * 既に公開済みのページのみを含める

   これらのオプションはデフォルトで選択されているので、忘れずに選択を解除する必要があります。 クリック **追加** をクリックして、コンテンツを公開/非公開に追加します。

   ![chlimage_1-57](assets/chlimage_1-57.png)

1. この **公開を管理** ウィザードは、レビュー用にツリーの内容をリストします。 追加のページを追加したり、選択したページを削除したりして、選択をさらにカスタマイズできます。

   ![screen_shot_2018-03-21at154237](assets/screen_shot_2018-03-21at154237.png)

   「**公開済みの参照**」オプションを使用して、公開する参照を確認することもできます。

1. [通常どおりに公開を管理ウィザードを続行](#manage-publication)して、ツリーの公開または非公開を完了します。

## 公開ステータスの判別 {#determining-publication-status}

ページの公開ステータスを次のように決定できます。

* [サイトコンソールのリソースの概要情報](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   ![screen_shot_2018-03-21at154336](assets/screen_shot_2018-03-21at154336.png)

   公開ステータスは、サイトコンソールの[カード](/help/sites-authoring/basic-handling.md#card-view)、[列](/help/sites-authoring/basic-handling.md#column-view)および[リスト](/help/sites-authoring/basic-handling.md#list-view)表示に表示されます。

* [タイムライン](/help/sites-authoring/basic-handling.md#timeline)

   ![screen_shot_2018-03-21at154420](assets/screen_shot_2018-03-21at154420.png)

* （ページ編集時の）[ページ情報メニュー](/help/sites-authoring/author-environment-tools.md#page-information)

   ![screen_shot_2018-03-21at154456](assets/screen_shot_2018-03-21at154456.png)
