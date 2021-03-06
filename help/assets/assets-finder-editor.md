---
title: アセットエディターページの作成と設定
description: カスタムのアセットエディターページを作成し、複数のアセットを同時に編集する方法を学習します。
contentOwner: AG
feature: Developer Tools,Asset Management
role: User,Admin
exl-id: 12899f61-9ceb-4bde-a501-6c50c93e3276
source-git-commit: 1679bbab6390808a1988cb6fe9b7692c3db31ae4
workflow-type: tm+mt
source-wordcount: '3300'
ht-degree: 76%

---

# アセットエディターページの作成と設定 {#creating-and-configuring-asset-editor-pages}

このドキュメントは次の内容について説明します。

* カスタマイズされたアセットエディターページを作成する理由。
* アセットエディターページ（メタデータの表示と編集、およびアセットに対するアクションの実行に使用する WCM ページ）の作成とカスタマイズの方法
* 複数のアセットを同時に編集する方法

>[!NOTE]
>
>アセット共有は、オープンソースの参照実装として使用できます。[Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) を参照してください。アセット共有は正式にはサポートされていません。

## アセットエディターページを作成および設定する理由 {#why-create-and-configure-asset-editor-pages}

デジタルアセット管理は、ますます広く使用されるようになっています。専門的に訓練されたユーザー（写真家や分類学者など）の小規模なユーザー・グループの小規模なソリューションから、ビジネス・ユーザー、WCM 作成者、ジャーナリストなど、より多様なユーザー・グループに移行する場合、 [!DNL Adobe Experience Manager Assets] プロフェッショナルユーザーは、多くの情報を提供しすぎる場合があり、関係者は、自身に関連するデジタルアセットへのアクセスを特定のユーザーインターフェイスまたはアプリケーションにリクエストし始めます。

そのようなアセット中心型アプリケーションの例として、従業員が展示会に参加した際の写真をアップロードできるイントラネット内のシンプルな写真ギャラリーや、公開 Web サイトでのプレスセンター（Geometrixx で提供されたサンプルなど）があります。アセット中心型アプリケーションは、ショッピングカート、チェックアウト、検証プロセスを含む完全なソリューションに拡張することもできます。

アセット中心型アプリケーションの作成の大部分は、コーディングを必要としない設定プロセスとなります。ここでは、ユーザーグループとそのニーズ、使用されるメタデータに関する知識のみが必要となります。を使用して作成されたアセット中心のアプリケーション [!DNL Assets] は拡張可能です。適度なコーディング作業で、アセットの検索、表示、変更のための再利用可能なコンポーネントを作成できます。

のアセット中心のアプリケーション [!DNL Experience Manager] は、特定のアセットの詳細を表示するために使用できるアセットエディターページで構成されます。 アセットエディターページでは、アセットにアクセスするユーザーが必要な権限を持っていれば、メタデータの編集も可能です。

## アセット共有ページの作成と設定 {#creating-and-configuring-an-asset-share-page}

DAM Finder 機能をカスタマイズし、必要なすべての機能を持つページを作成します。これらのページがアセット共有ページと呼ばれます。新しいアセット共有ページを作成するには、Geometrixx アセット共有テンプレートを使用してページを追加し、次にそのページに対してユーザーが実行できるアクションをカスタマイズします。さらに、アセットの表示方法と、ユーザーによるクエリの作成方法を決定します。

カスタマイズされたアセット共有ページを作成する用途としては次のような例が考えられます。

* ジャーナリスト向けのプレスセンター
* 社内ビジネスユーザー向けの画像検索エンジン
* Web サイトユーザー向けの画像データベース
* メタデータエディター向けのメディアタグ作成インターフェイス

### アセット共有ページの作成 {#creating-an-asset-share-page}

新しいアセット共有ページを作成する方法として、Web サイトでの作業中に作成するか、Digital Asset Manager から作成することができます。

>[!NOTE]
>
>デフォルトでは、Digital Asset Manager の「**新規**」からアセット共有ページを作成すると、アセットビューアおよびアセットエディターが自動的に作成されます。

**Web サイト**&#x200B;コンソールで新しいアセット共有ページを作成するには：

1. 「**[!UICONTROL Web サイト]**」タブで、アセット共有ページを作成する場所に移動し、「**[!UICONTROL 新規]**」をクリックします。

1. を選択します。 **[!UICONTROL アセット共有]** ページを開き、「 **[!UICONTROL 作成]**.新しいページが作成され、アセット共有ページが **[!UICONTROL Web サイト]** タブをクリックします。

![dam8](assets/dam8.png)

Geometrixx DAM アセット共有テンプレートを使用して作成した基本ページは次のイメージのようになります。

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

アセット共有ページをカスタマイズするには、サイドキックの要素を使用し、Query Builder のプロパティも編集します。ページ **[!UICONTROL Geometrixxプレスセンター]** は、このテンプレートに基づくページのカスタマイズバージョンです。

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

Digital Asset Manager を使用して新しいアセット共有ページを作成するには：

1. Digital Asset Manager の「**[!UICONTROL 新規]**」で、「**[!UICONTROL 新しいアセット共有]**」を選択します。
1. 「**[!UICONTROL タイトル]**」にアセット共有ページの名前を入力します。必要に応じて、URL の名前を入力します。

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. アセット共有ページをダブルクリックして開き、ページの設定をおこないます。

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   デフォルトでは、「**[!UICONTROL 新規]**」からアセット共有ページを作成すると、アセットビューアおよびアセットエディターが自動的に作成されます。

#### アクションのカスタマイズ {#customizing-actions}

事前定義済みの一連のアクションの中から、選択したデジタルアセットに対してユーザーが実行できるアクションを決定できます。

アセット共有ページにアクションを追加するには：

1. カスタマイズするアセット共有ページで、サイドキックの「**[!UICONTROL アクション]**」をクリックします。

   次のアクションが使用可能です。
   ![assetshare2](assets/assetshare2.bmp)

| アクション | 説明 |
|---|---|
| [!UICONTROL アクションを削除] | ユーザーが選択したアセットを削除できます。 |
| [!UICONTROL アクションをダウンロード] | ユーザーが選択したアセットをコンピューターにダウンロードできるようにします。 |
| [!UICONTROL Lightbox アクション] | アセットを「Lightbox」に保存します。Lightbox では、保存されたアセットに対して他のアクションを実行できます。これは、複数のページにまたがるアセットを操作する場合に便利です。Lightbox は、アセットの買い物かごとしても使用できます。 |
| [!UICONTROL アクションを移動] | ユーザーがアセットを別の場所に移動できます。 |
| [!UICONTROL タグアクション] | ユーザーが選択したアセットにタグを追加できるようにします。 |
| [!UICONTROL アセットアクションを表示] | ユーザーが変更できるように、アセットをアセットエディターで開きます。 |

1. 適切なアクションを **アクション** 領域に表示されます。 これによって、そのアクションを実行するボタンが作成されます。

   ![chlimage_1-387](assets/chlimage_1-387.png)

#### 検索結果の表示方法の決定 {#determining-how-search-results-are-presented}

事前定義済みのレンズリストで、結果の表示方法を指定します。

検索結果の表示方法を変更するには：

1. カスタマイズするアセット共有ページで、「**[!UICONTROL 検索]**」をクリックします。

   ![chlimage_1](assets/chlimage_1.bmp)

1. 適切なレンズをページの中央上にドラッグします。 Press Center では、レンズは既に使用可能な状態です。ユーザーは適切なレンズアイコンをクリックして、求めるとおりの検索結果を表示します。

次のレンズが使用可能です。

| レンズ | 説明 |
|---|---|
| **[!UICONTROL リストレンズ]** | 詳細情報を含むリスト形式でアセットを表示します。 |
| **[!UICONTROL モザイクレンズ]** | モザイク形式でアセットを表示します。 |

#### モザイクレンズ {#mosaic-lens}

![chlimage_1-388](assets/chlimage_1-388.png)

#### リストレンズ {#list-lens}

![chlimage_1-389](assets/chlimage_1-389.png)

#### Query Builder のカスタマイズ {#customizing-the-query-builder}

クエリビルダーでは、検索語句を入力し、アセット共有ページのコンテンツを作成できます。クエリビルダーの編集時に、1 ページに表示する検索結果数、アセットのダブルクリック時に開くアセットエディターおよびクエリ検索パスを指定し、ノード型をカスタマイズします。

クエリビルダーをカスタマイズするには：

1. カスタマイズするアセット共有ページで、QueryBuilder の「**[!UICONTROL 編集]**」をクリックします。デフォルトでは、「**[!UICONTROL 一般]**」タブが開きます。

1. 1 ページあたりの結果の数、アセットエディターのパス（カスタマイズされたアセットエディターがある場合）およびアクションタイトルを選択します。

   ![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. 次をクリック： **[!UICONTROL パス]** タブをクリックします。 検索対象とする 1 つまたは複数のパスを入力します。ユーザーがパスの述語を使用すると、これらのパスは上書きされます。

   ![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. 必要に応じて、別のノードタイプを入力します。

1. 内 **[!UICONTROL Query Builder URL]** 「 」フィールドに値を入力すると、query builder を上書きするかラップして、既存の query builder コンポーネントを使用して新しいサーブレット URL を入力できます。 「**[!UICONTROL フィード URL]**」フィールドで、フィード URL を上書きすることもできます。

   ![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. 内 **[!UICONTROL テキスト]** 「 」フィールドで、結果と結果のページ番号に表示するテキストを入力します。 変更作業が完了したら、「**[!UICONTROL OK]**」をクリックします。

   ![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### 述語の追加 {#adding-predicates}

[!DNL Experience Manager Assets] には、アセット共有ページに追加できる多数の述語が用意されています。述語を使用すると、ユーザーが検索をさらに絞り込むことができます。一部のケースでは、指定した述語がクエリビルダーのパラメーター（「パス」パラメーターなど）よりも優先されます。

述語を追加するには：

1. カスタマイズするアセット共有ページで、「**[!UICONTROL 検索]**」をクリックします。

   ![assetshare3](assets/assetshare3.bmp)

1. 適切な述語を、アセット共有ページのクエリビルダーの下にドラッグします。 これによって、適切なフィールドが作成されます。

   ![assetshare4](assets/assetshare4.bmp)

   次の述語が使用可能です。

| 述語 | 説明 |
|---|---|
| **[!UICONTROL 日付の述語]** | ユーザーが特定の日付の前後に変更されたアセットを検索できるようにします。 |
| **[!UICONTROL オプションの述語]** | サイト所有者が検索用のプロパティを指定できます（プロパティの述語などで、例えば cq:tags と指定）。また、オプションを設定するためのコンテンツツリー（タグツリーなど）を指定できます。この操作によってオプションのリストが生成され、ユーザーはこのリストから、選択されたプロパティ（タグプロパティ）に含まれる値（タグ）を選択できます。この述語を使用すれば、タグのリスト、ファイルタイプのリスト、画像の向きのリストなどのリストコントロールを作成できます。この述語は、固定数のオプションに適しています。 |
| **[!UICONTROL パスの述語]** | ユーザーがパス（および必要に応じてサブフォルダー）を定義できるようにします。 |
| **[!UICONTROL プロパティの述語]** | サイト所有者が検索対象のプロパティ（例：tiff:ImageLength）を指定すると、ユーザーが値（例：800）を入力できます。この例では、高さが 800 ピクセルのすべての画像が返されます。プロパティに任意の値を設定できる場合に有効な述語です。 |

詳しくは、[述語の Javadoc](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html) を参照してください。

1. 述語をさらに設定するには、述語をダブルクリックします。 例えば、「パスの述語」を開いたら、ルートパスを指定する必要があります。

   ![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)

## アセットエディターページの作成と設定 {#creating-and-configuring-an-asset-editor-page}

アセットエディターをカスタマイズして、ユーザーによるデジタルアセットの表示および編集方法を指定します。これをおこなうには、新規のアセットエディターページを作成してから、ユーザーがページに対して実行できる表示とアクションをカスタマイズします。

>[!NOTE]
>
>DAM アセットエディターにカスタムフィールドを追加する場合は、新しい cq:Widget ノードを `/apps/dam/content/asseteditors.`

### アセットエディターページの作成 {#creating-the-asset-editor-page}

アセットエディターページを作成する場合に、アセット共有ページのすぐ下にページを作成することをお勧めします。

アセットエディターページを作成するには：

1. 「**[!UICONTROL Web サイト]**」タブで、アセットエディターページを作成する場所に移動し、「**[!UICONTROL 新規]**」をクリックします。

1. 「**[!UICONTROL Geometrixx アセットエディター]**」を選択し、「**[!UICONTROL 作成]**」をクリックします。新しいページが作成され、ページが「**[!UICONTROL Web サイト]**」タブに表示されます。

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

Geometrixx アセットエディターテンプレートを使用して作成された基本ページは次のイメージのようになります。

![assetshare5](assets/assetshare5.bmp)

アセットエディターページをカスタマイズするには、サイドキックの要素を使用します。次の場所からアクセスするアセットエディターページ **[!UICONTROL Geometrixxプレスセンター]** は、このテンプレートに基づくページのカスタマイズバージョンです。

![assetshare6](assets/assetshare6.bmp)

#### アセット共有ページから開くアセットエディターの設定 {#setting-which-asset-editor-opens-from-an-asset-share-page}

カスタムのアセットエディターページを作成したら、アセット（作成したカスタムのアセット共有）をダブルクリックすると、カスタマイムのエディターページでアセットが開くことを確認する必要があります。

アセットエディターページを設定するには：

1. アセット共有ページで、QueryBuilder の隣にある「**[!UICONTROL 編集]**」をクリックします。

   ![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. 次をクリック： **[!UICONTROL 一般]** タブ（まだ選択されていない場合）に表示されます。

1. 内 **[!UICONTROL アセットエディターのパス]** フィールドで、アセット共有ページでアセットを開くアセットエディターのパスを入力し、「 **[!UICONTROL OK]**.

   ![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### アセットエディターコンポーネントを追加 {#adding-asset-editor-components}

アセットエディターに含める機能を指定するには、ページにコンポーネントを追加します。

アセットエディターコンポーネントを追加するには：

1. カスタマイズするアセットエディターページで、サイドキックの「**[!UICONTROL アセットエディター]**」を選択します。使用可能なすべてのアセットエディターコンポーネントが表示されます。

   >[!NOTE]
   >
   >何をカスタマイズできるかは、使用可能なコンポーネントによって異なります。コンポーネントを有効にするには、デザインモードに移動し、有効にする必要のあるコンポーネントを選択します。

1. サイドキックからアセットエディターにコンポーネントをドラッグし、コンポーネントダイアログで変更を加えます。 コンポーネントについて、次の表およびその下の詳細説明で説明します。

   >[!NOTE]
   >
   >アセットエディターページのデザイン時に、読み取り専用、編集可能のいずれかのコンポーネントを作成します。ユーザーは、そのコンポーネント内に鉛筆の画像が表示されればフィールドが編集可能であるとわかります。デフォルトでは、ほとんどのコンポーネントは読み取り専用として設定されます。

   | コンポーネント | 説明 |
   |---|---|
   | **[!UICONTROL メタデータフォーム] および [!UICONTROL メタデータテキストフィールド]** | アセットにメタデータを追加し、そのアセットに対して送信などのアクションを実行できるようにします。 |
   | **[!UICONTROL サブアセット]** | サブアセットをカスタマイズできるようにします。 |
   | **タグ** | ユーザーがタグを選択してアセットに追加できるようにします。 |
   | **[!UICONTROL サムネール]** | アセットのサムネールとファイル名を表示し、代替テキストを追加できるようにします。ここでは、アセットエディターのアクションを追加することもできます。 |
   | **[!UICONTROL タイトル]** | アセットのタイトルを表示します。このタイトルはカスタマイズ可能です。 |

   ![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### メタデータフォームとテキストフィールド - メタデータの表示コンポーネントの設定 {#metadata-form-and-text-field-configuring-the-view-metadata-component}

メタデータフォームは、開始アクションと終了アクションを含むフォームです。その間には、**[!UICONTROL テキスト]**&#x200B;フィールドを入力します。フォームの操作について詳しくは、[フォーム](../sites-authoring/default-components.md)を参照してください。

1. 「 **[!UICONTROL 編集]** （フォームの「開始」領域） 必要に応じて、「ボックスタイトル」にボックスタイトルを入力できます。デフォルトでは、ボックスタイトルは「**[!UICONTROL メタデータ]**」です。生成された Java スクリプトクライアントコードを検証する場合は、「クライアントの検証」チェックボックスをオンにします。

   ![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. 「 **[!UICONTROL 編集]** （フォームの「終了」領域） 例えば、ユーザーがメタデータの変更内容を送信できる「**[!UICONTROL 送信]**」ボタンを作成できます。また、オプションとして、メタデータを元の状態にリセットする「**[!UICONTROL リセット]**」ボタンを追加できます。

   ![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. 期間 **[!UICONTROL フォーム開始]** そして **フォーム終了**&#x200B;メタデータテキストフィールドをフォームにドラッグします。 ユーザーはこれらのテキストフィールドにメタデータを入力し、このメタデータを送信するか、他のアクションを実行することができます。

1. フィールド名をダブルクリックします（例： ）。 **タイトル** をクリックして、メタデータフィールドを開き、変更を加えます。 **[!UICONTROL コンポーネントを編集]**&#x200B;ウィンドウの「[!UICONTROL 一般]」タブで、名前空間、フィールドラベル、型（`dc:title` など）を定義します。


   ![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

   メタデータフォームで使用可能な名前空間の変更について詳しくは、[ のカスタマイズと拡張 [!DNL Assets]](extending-assets.md)を参照してください。

1. 次をクリック： **[!UICONTROL 制約]** タブをクリックします。 ここで、フィールドを必須にするかどうかを選択し、必要に応じて制約を追加できます。

   ![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. 次をクリック： **[!UICONTROL 表示]** タブをクリックします。 ここで、メタデータフィールドの列の新しい幅と列数を入力できます。「**フィールドは読み取り専用です**」チェックボックスをオフにすると、ユーザーがメタデータを編集できるようになります。

   ![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

   次に、様々なフィールドを持つメタデータフォームの例を示します。

   ![chlimage_1-390](assets/chlimage_1-390.png)

アセットエディターページでは、ユーザーはこの後メタデータフィールドに値を入力し（フィールドが編集可能な場合）、終了アクション（変更内容の送信など）を実行することができます。

#### サブアセット {#sub-assets}

サブアセットコンポーネントでは、サブアセットの表示と選択をおこなうことができます。[メインアセット](assets.md#what-are-digital-assets)とサブアセットの下に表示される名前を指定できます。

![screen_shot_2012-04-23at24025pm](assets/screen_shot_2012-04-23at24025pm.png)

サブアセットコンポーネントをダブルクリックし、サブアセットダイアログを開きます。このダイアログで、メインアセットや任意のサブアセットのタイトルを変更できます。デフォルト値は、対応するフィールドの下に表示されます。

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

次に、設定済みのサブアセットコンポーネントの例を示します。

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

例えば、あるサブアセットを選択すると、コンポーネントに適切なページが表示され、ボックスタイトルがサブアセットから兄弟アセットに変更されます。

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### タグ {#tags}

タグコンポーネントは、ユーザーがアセットに既存のタグを割り当てることのできるコンポーネントです。タグは後で構成や取得に役に立ちます。ユーザーがタグを追加できず、参照のみできるように、このコンポーネントを読み取り専用にできます。

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

タグコンポーネントをダブルクリックしてタグダイアログを開きます。このダイアログで、必要に応じてタグのタイトルを変更し、割り当て済みの名前空間を選択することができます。このフィールドを編集可能にするには、「**編集ボタンを**&#x200B;非表示にする」チェックボックスをオフにします。デフォルトでは、タグは編集可能です。

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

ユーザーがタグを編集できる場合は、鉛筆アイコンをクリックし、「Tags」ドロップダウンメニューからタグを選択して、タグを追加できます。

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

次に、設定済みのタグコンポーネントを示します。

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### サムネール {#thumbnail}

サムネイルコンポーネントでは、選択したサムネイルがアセットで表示されます（多くの形式でサムネイルは自動的に抽出されます）。さらに、コンポーネントではファイル名と、[変更可能なアクション](assets-finder-editor.md#adding-asset-editor-actions)が表示されます。

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

サムネールコンポーネントをダブルクリックすると、サムネールダイアログが開きます。このダイアログで、代替テキストを変更できます。デフォルトでは、サムネールの代替テキストは、「**[!UICONTROL Click to download asset]**」です。

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

次に、設定済みのサムネールコンポーネントの例を示します。

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### タイトル {#title}

タイトルコンポーネントでは、アセットのタイトルと説明が表示されます。

![chlimage_1-391](assets/chlimage_1-391.png)

デフォルトでは、タイトルは読み取り専用であり、ユーザーは編集できません。編集可能にするには、コンポーネントをダブルクリックし、「**編集ボタンを非表示にする**」チェックボックスをオフにします。さらに、複数のアセットのタイトルを入力します。

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

タイトルが編集可能な場合、鉛筆アイコンをクリックして&#x200B;**アセットのプロパティ**&#x200B;ウィンドウを開いて、タイトルと説明を追加できます。さらに、日時を選択してアセットのオンとオフを切り替えることができます。

ユーザーが鉛筆アイコンをクリックしてタイトルを編集する場合、「**タイトル**」と「**説明**」を変更し、アセットをオンまたはオフにする「**オンタイム**」と「**オフタイム**」を入力することができます。

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

次に、設定済みのタイトルコンポーネントの例を示します。

![chlimage_1-392](assets/chlimage_1-392.png)

#### アセットエディターのアクションを追加 {#adding-asset-editor-actions}

事前定義済みの一連のアクションの中から、選択したデジタルアセットに対してユーザーが実行できるアクションを決定できます。

アセットエディターページにアクションを追加するには：

1. カスタマイズするアセットエディターページで、 **[!UICONTROL アセットエディター]** サイドキックに<br>

   ![サイドキックでアセットエディターを選択](assets/screen_shot_2012-04-23at35515pm.png)

   次のアクションが使用可能です。

   | アクション | 説明 |
   |---|---|
   | [!UICONTROL ダウンロード] | ユーザーが選択したアセットをコンピューターにダウンロードできるようにします。 |
   | [!UICONTROL エディター] | ユーザーが画像を編集できるようにします（インタラクティブ編集）。 |
   | [!UICONTROL Lightbox] | アセットを「Lightbox」に保存します。Lightbox では、保存されたアセットに対して他のアクションを実行できます。これは、複数のページにまたがるアセットを操作する場合に便利です。 |
   | [!UICONTROL ロック] | ユーザーがアセットをロックできるようにします。この機能はデフォルトでは有効ではなく、コンポーネントのリスト内で有効にする必要があります。 |
   | [!UICONTROL 参照] | クリックすると、アセットで現在使用されているページが表示されます。 |
   | [!UICONTROL バージョン管理] | アセットのバージョンの作成と復元が可能です。 |

1. 適切なアクションを **アクション** 領域に表示されます。 これによって、そのアクションを実行するボタンが作成されます。

![chlimage_1-393](assets/chlimage_1-393.png)

## アセットエディターページでの複数アセットの編集 {#multi-editing-assets-with-the-asset-editor-page}

を使用 [!DNL Assets] 複数のアセットを一度に変更できます。 アセットを選択した後、それらのアセットの次の情報を同時に変更できます。

* タグ
* メタデータ

アセットエディターページを使用してアセットをマルチ編集するには：

1. Geometrixxを開く **[!UICONTROL 中央を押す]** ページ `http://localhost:4502/content/geometrixx/en/company/press.html`.
1. アセットを選択します。

   * Windows の場合： `Ctrl + click` 各アセット。
   * Mac: `Cmd + click` 各アセット。

   アセットの範囲を選択するには：最初のアセットをクリックしてから、 `Shift + click` 最後のアセット。

1. 「**Actions**」フィールド（ページの左側）の「**[!UICONTROL Edit Metadata]**」をクリックします。

1. Geometrixx **[!UICONTROL Press Center Asset Editor]** ページが新しいタブで開きます。アセットのメタデータが以下のように表示されます。

   * すべてのアセットではなく一部のアセットにのみ適用されるタグは、斜体で表示されます。
   * すべてのアセットに適用されるタグは、通常のフォントで表示されます。
   * タグ以外のメタデータ：フィールドの値は、選択されたすべてのアセットで同じ場合にのみ表示されます。

1. クリック **[!UICONTROL ダウンロード]** をクリックして、アセットのオリジナルのレンディションを含む ZIP ファイルをダウンロードします。
1. 「**[!UICONTROL Tags]**」フィールドの横にある鉛筆アイコンをクリックして、タグを編集します。

   * すべてのアセットではなく一部のアセットにのみ適用されるタグは、グレーの背景になります。
   * すべてのアセットに適用されるタグは白の背景になります。

   以下の操作を実行できます。

   * 「`x`」アイコンをクリックして、すべてのアセットのタグを削除します。
   * 次をクリック： `+` アイコンをクリックして、すべてのアセットにタグを追加します。
   * 次をクリック： `arrow` タグを選択して、すべてのアセットに新しいタグを追加します。

   「**[!UICONTROL OK]**」をクリックして、変更内容をフォームに書き込みます。「**Tags**」フィールドの横にあるチェックボックスが自動的にオンになります。

1. 「説明」フィールドを編集します。例えば、次のように設定します。 `This is a common description`.フィールドを編集すると、フォームの送信時に、選択したアセットの既存の値がその値によって上書きされます。 フィールドを編集すると、「 」フィールドの横にある「 」チェックボックスが自動的にオンになります。

   `This is a common description`

   フィールドを編集すると、フォームの送信時に、選択したアセットの既存の値が編集した値によって上書きされます。

   注意：フィールドを編集すると、フィールドの横にあるチェックボックスが自動的にオンになります。

1. クリック **[!UICONTROL メタデータを更新]** をクリックしてフォームを送信し、すべてのアセットの変更を保存します。チェック済みのメタデータのみが変更されます。
