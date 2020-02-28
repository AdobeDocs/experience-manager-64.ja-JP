---
title: ページの公開
seo-title: ページの公開
description: 'null'
seo-description: 'null'
uuid: 1222859d-ef8d-462e-a125-b76e6cfec26d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8f2714bc-9d6c-4e6f-97a1-3b4f977348c5
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340

---


# ページの公開{#publishing-pages}

オーサー環境でコンテンツを作成およびレビューした後は、[公開 Web サイト（パブリッシュ環境）でコンテンツを利用できるようにする](/help/sites-authoring/author.md#concept-of-authoring-and-publishing)ことが目標となります。

この操作は、ページの公開と呼ばれます。パブリッシュ環境からページを削除する場合は、非公開と呼びます。ページは、公開／非公開を切り替えても、削除するまでは、さらなる変更に備えてオーサー環境で使用できます。

また、ページの公開または非公開は、即座におこなうことも、後で事前定義済みの日時におこなうこともできます。

>[!NOTE]
>
>公開に関する用語には、紛らわしいものがあります。
>
>* **発行／非公開**
   >  コンテンツを公開環境で公開できる（または公開できない）アクションの主な用語は次のとおりです。
   >
   >
* **アクティブ化/非アクティブ化**
   >  これらの用語は、発行/非公開と同義語です。
   >
   >
* **レプリケート／レプリケーション**
   >  これらは、ユーザーのコメントを発行または逆複製する場合など、ある環境から別の環境へのデータ（ページのコンテンツ、ファイル、コード、ユーザーのコメントなど）の移動を説明する技術用語です。
>



>[!NOTE]
>
>特定のページを公開するために必要な権限がない場合。
>
>* ワークフローがトリガーされ、公開リクエストの適切なユーザーに通知されます。
>* この[ワークフローは、開発チームによってカスタマイズされている](/help/sites-developing/workflows-models.md)ことがあります。
>* ワークフローがトリガーされたことを通知するメッセージが少しの間表示されます。
>



## ページの公開 {#publishing-pages-2}

場所に応じて、次から公開できます。

* [ページエディターから](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)
* [サイトコンソールから](/help/sites-authoring/publishing-pages.md#publishing-from-the-console)

### エディターからの公開 {#publishing-from-the-editor}

ページを編集している場合、エディターから直接公開できます。

1. Select the **Page Information** icon to open the menu and then the **Publish Page** option.

   ![screen_shot_2018-03-21at152734](assets/screen_shot_2018-03-21at152734.png)

1. 公開が必要な参照がページに含まれているかどうかに応じて、次の操作をおこないます。

   * 公開する参照がない場合、ページが直接公開されます。
   * 公開が必要な参照がページに含まれている場合は、それらのリストが&#x200B;**発行**&#x200B;ウィザードに表示され、ウィザードで次のいずれかを実行できます。

      * Specify which of the assets/tags/etc. you want to publish together with the page, then use **Publish** to complete the process.
      * 「**キャンセル**」を使用してアクションを中止します。
   ![chlimage_1-50](assets/chlimage_1-50.png)

1. Selecting **Publish** will replicate the page to the publish environment. ページエディターに、公開アクションを確認する情報バナーが表示されます。

   ![screen_shot_2018-03-21at152840](assets/screen_shot_2018-03-21at152840.png)

   コンソールで同じページを表示すると、更新された公開ステータスが表示されます。

   ![screen_shot_2018-03-21at152951](assets/screen_shot_2018-03-21at152951.png)

>[!NOTE]
>
>エディターからの公開は、浅い公開です。つまり、選択したページだけが公開され、子ページは公開されません。

### コンソールからの公開 {#publishing-from-the-console}

サイトコンソールには、2 つの公開オプションがあります。

* [クイック公開](/help/sites-authoring/publishing-pages.md#quick-publish)
* [公開を管理](/help/sites-authoring/publishing-pages.md#manage-publication)

#### クイック公開 {#quick-publish}

**クイック公開**&#x200B;は、単純な場合のためのもので、選択したページが即座に公開されます。他に何か操作する必要はありません。このため、すべての非公開の参照も自動的に公開されます。

クイック公開でページを公開するには、次の手順を実行します。

1. Select the page or pages in the sites console and click on the **Quick Publish** button.

   ![screen_shot_2018-03-21at153115](assets/screen_shot_2018-03-21at153115.png)

1. クイック公開ダイアログで、「**公開**」をクリックして公開を確認するか、「**キャンセル**」をクリックしてキャンセルします。すべての非公開の参照も自動的に公開されることに注意してください。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. ページが公開される際に、公開を確認するアラートが表示されます。

>[!NOTE]
>
>クイック公開は、浅い公開です。つまり、選択したページだけが公開され、子ページは公開されません。

#### 公開を管理 {#manage-publication}

**「パブリケーションの管理** 」には、「クイック発行」よりも多くのオプションが用意されており、子ページを含めたり、参照をカスタマイズしたり、該当するワークフローを開始したり、後日公開するオプションを提供したりできます。

公開を管理を使用してページを公開または非公開にするには、次の手順を実行します。

1. サイトコンソールで 1 つまたは複数のページを選択し、「**公開を管理**」ボタンをクリックします。

   ![screen_shot_2018-03-21at153309](assets/screen_shot_2018-03-21at153309.png)

1. **公開を管理**&#x200B;ウィザードが起動します。最初の手順の&#x200B;**オプション**&#x200B;では、次のことができます。

   * 選択したページの公開または非公開を選択する。
   * そのアクションを今すぐ実行するか後日実行するかを選択する。
   後で公開することを選択すると、指定した時間に選択したページを公開するワークフローが開始されます。逆に、後で非公開にすることを選択すると、特定の時間に選択したページを非公開にするワークフローが開始されます。

   公開／非公開を後からキャンセルする場合は、[ワークフローコンソール](/help/sites-administering/workflows.md)に移動して、対応するワークフローを終了します。

   ![chlimage_1-52](assets/chlimage_1-52.png)

   「**次へ**」をクリックして次に進みます。

1. In the next step of the Manage Publication wizard, **Scope**, you can define the scope of the publication/unpublication such as including to include child pages and/or including references.

   ![screen_shot_2018-03-21at153354](assets/screen_shot_2018-03-21at153354.png)

   公開を管理ウィザードを開始する前に選択し忘れた場合は、「**コンテンツを追加**」ボタンを使用して、公開するページのリストにページを追加できます。

   「コンテンツを追加」ボタンをクリックすると、[パスブラウザー](/help/sites-authoring/author-environment-tools.md#path-browser)が開き、コンテンツを選択できます。

   Select the required pages and then click **Select** to add the content to the wizard or **Cancel **to cancel the selection and return to the wizard.

   ウィザードに戻ると、リストの項目を選択して、次のような追加のオプションを設定できます。

   * その子を含める。
   * 選択から削除する。
   * その公開済みの参照を管理する。
   ![screen_shot_2018-03-21at153450](assets/screen_shot_2018-03-21at153450.png)

   「**子を含める**」をクリックすると、次のことができるダイアログが開きます。

   * 直近の子のみを含める。
   * 変更されたページのみを含める。
   * 既に公開済みのページのみを含める。
   「**追加**」をクリックして、選択オプションに基づいて公開または非公開にするページのリストに子ページを追加します。「**キャンセル**」をクリックして選択をキャンセルし、ウィザードに戻ります。

   ![chlimage_1-53](assets/chlimage_1-53.png)

   ウィザードに戻ると、子を含めるダイアログでのオプションの選択に基づいて、ページが追加されていることを確認できます。

   ページを選択して「**公開済みの参照**」ボタンをクリックすると、ページに対して公開または非公開にする参照を表示および変更できます。

   ![screen_shot_2018-03-21at153801](assets/screen_shot_2018-03-21at153801.png)

   **公開済みの参照**&#x200B;ダイアログに、選択したコンテンツの参照が表示されます。デフォルトでは、それらはすべて選択され、公開／非公開にされますが、チェックボックスをオフにすると、選択を解除してそれらをアクションに含めないようにすることができます。

   「**完了**」をクリックして変更を保存するか、「**キャンセル**」をクリックして選択をキャンセルし、ウィザードに戻ります。

   ![screen_shot_2018-03-21at153824](assets/screen_shot_2018-03-21at153824.png)

   ウィザードに戻ると、「**参照**」列が更新されて、公開または非公開にする参照の選択が反映されます。

   ![screen_shot_2018-03-21at153925](assets/screen_shot_2018-03-21at153925.png)

1. Click **Publish** to complete.

   サイトコンソールに戻ると、公開を確認する通知メッセージが表示されます。

   ![screen_shot_2018-03-21at153951](assets/screen_shot_2018-03-21at153951.png)

1. If the published pages are associated with workflows, they may be shown in a final **Workflows** step of the publication wizard.

   >[!NOTE]
   >
   >**ワークフロー**&#x200B;手順は、ユーザーの権限に基づいて表示されます。See the [previous note on this page](/help/sites-authoring/publishing-pages.md) regarding publishing privileges as well as [Managing Access to Workflows](/help/sites-administering/workflows-managing.md) and [Applying Workflows to Pages](/help/sites-authoring/workflows-applying.md) for details.

   リソースは、トリガーされたワークフローでグループ化され、それぞれに次のオプションがあります。

   * ワークフローのタイトルを定義する。
   * ワークフローが[複数のリソースをサポートする](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)場合、ワークフローパッケージを維持する。
   * ワークフローパッケージを維持するオプションが選択されている場合、ワークフローパッケージのタイトルを定義する。
   Click **Publish** or **Publish Later **to complete the publication.

   ![chlimage_1-54](assets/chlimage_1-54.png)

## ページを非公開にする {#unpublishing-pages}

ページを非公開にすると、そのページがパブリッシュ環境から削除され、読者に公開されなくなります。

In a [manner similar to publishing](/help/sites-authoring/publishing-pages.md#publishing-pages), one or more pages can be unpublished:

* [ページエディターから](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-editor)
* [サイトコンソールから](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-console)

### エディターから非公開にする {#unpublishing-from-the-editor}

ページを編集する際に、そのページを非公開にする場合、[ページを公開](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)するときと同じように、**ページ情報**&#x200B;メニューで「**ページを非公開にする**」を選択します。

### コンソールから非公開にする {#unpublishing-from-the-console}

[「公開を管理」オプションを使用して公開する](/help/sites-authoring/publishing-pages.md#manage-publication)場合と同様に、「公開を管理」オプションを使用して非公開にできます。

1. サイトコンソールで 1 つまたは複数のページを選択し、「**公開を管理**」ボタンをクリックします。
1. **公開を管理**&#x200B;ウィザードが起動します。最初の手順の&#x200B;**オプション**&#x200B;で、デフォルトオプションの&#x200B;**公開**&#x200B;の代わりに&#x200B;**非公開**&#x200B;を選択します。

   ![chlimage_1-55](assets/chlimage_1-55.png)

   後で公開することを選択するとこのバージョンのページを公開するワークフローが指定した時間に開始されるのと同じように、後でアクティベートを解除することを選択すると、選択したページを非公開にするワークフローが特定の時間に開始されます。

   公開／非公開を後からキャンセルする場合は、[ワークフローコンソール](/help/sites-administering/workflows.md)に移動して、対応するワークフローを終了します。

1. 非公開の操作を完了するには、[ページを公開する](/help/sites-authoring/publishing-pages.md#manage-publication)場合と同様にウィザードを続行します。

## ツリーの公開と非公開 {#publishing-and-unpublishing-a-tree}

多数のコンテンツページを入力または更新した場合、これらのページがすべて同じルートページの下にあれば、ツリー全体を 1 回の操作で簡単に公開できます。

サイトコンソールにある「[公開を管理](/help/sites-authoring/publishing-pages.md#manage-publication)」オプションを使用すると、これをおこなうことができます。

1. サイトコンソールで、公開または非公開するツリーのルートページを選択し、「**公開を管理**」を選択します。
1. **公開を管理**&#x200B;ウィザードが起動します。公開または非公開と実行するタイミングを選択して、「**次へ**」を選択して続行します。
1. **範囲**&#x200B;の手順で、ルートページを選択して、「**子を含める**」を選択します。

   ![chlimage_1-56](assets/chlimage_1-56.png)

1. **子を含める**&#x200B;ダイアログで、次のオプションのチェックボックスをオフにします。

   * 直近の子のみを含める
   * 既に公開済みのページのみを含める
   これらのオプションは、デフォルトで選択されているので、忘れずに選択解除する必要があります。「**追加**」をクリックして、コンテンツを公開／非公開に追加します。

   ![chlimage_1-57](assets/chlimage_1-57.png)

1. **公開を管理**&#x200B;ウィザードにツリーのコンテンツがリストされていることを確認します。ページを追加したりそれらの選択を削除したりすることで、選択をさらにカスタマイズできます。

   ![screen_shot_2018-03-21at154237](assets/screen_shot_2018-03-21at154237.png)

   Remember that you can also review the references to be published via the **Published References** option.

1. [通常どおり[パブリケーションの管理](#manage-publication) ]ウィザードを続行し、ツリーのパブリケーションまたは非公開を完了します。

## 公開ステータスの判別 {#determining-publication-status}

ページの公開ステータスを判別できます。

* [サイトコンソールのリソースの概要情報](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   ![screen_shot_2018-03-21at154336](assets/screen_shot_2018-03-21at154336.png)

   公開ステータスは、サイトコンソールの[カード](/help/sites-authoring/basic-handling.md#card-view)、[列](/help/sites-authoring/basic-handling.md#column-view)および[リスト](/help/sites-authoring/basic-handling.md#list-view)表示に表示されます。

* In the [timeline](/help/sites-authoring/basic-handling.md#timeline)

   ![screen_shot_2018-03-21at154420](assets/screen_shot_2018-03-21at154420.png)

* In the [Page Information menu](/help/sites-authoring/author-environment-tools.md#page-information) when editing a page

   ![screen_shot_2018-03-21at154456](assets/screen_shot_2018-03-21at154456.png)

