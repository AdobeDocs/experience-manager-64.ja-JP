---
title: 複合アセットを管理し、サブアセットを生成します。
description: InDesign、Adobe Illustrator、Photoshopの各ファイル内からAEMアセットへの参照を作成する方法を説明します。 また、ページビューア機能を使用して、複数ページファイル（PDF、INDD、PPT、PPTX、AI ファイルなど）の個々のページを表示する方法についても説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 1532ea0f4203b269f8414d150a07bed0c42a23bc
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 52%

---


# サブアセットを含む複合アセットの管理 {#managing-compound-assets}

Adobe Experience Manager (AEM) Assets では、アップロードされたファイルに、リポジトリ内の既存のアセットへの参照が含まれているかどうかを確認できます。この機能は、サポート対象のファイル形式でのみ使用できます。アップロードされたアセットに AEM アセットへの参照が含まれている場合、アップロードされたアセットと参照元のアセットの間に双方向のリンクが作成されます。

Adobe Creative Cloud アプリケーションで AEM アセットを参照することで、冗長性を排除するだけでなく、コラボレーションを強化し、ユーザーの作業効率と生産性を高めることができます。

AEM Assets では&#x200B;**双方向の参照**&#x200B;をサポートしています。参照元のアセットは、アップロードされたファイルのアセットの詳細ページで確認できます。さらに、AEM アセットの参照先のファイルは、参照元アセットのアセット詳細ページで確認できます。

参照は、参照元のアセットのパス、ドキュメント ID およびインスタンス ID に基づいて解決されます。

## Adobe Illustrator 内で AEM アセットを参照として追加 {#refai}

既存の AEM アセットを、Adobe Illustrator ファイル内から参照できます。

1. [AEM デスクトップアプリケーション](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app.html)を使用して、AEM Assets リポジトリをローカルコンピューター上のドライブとしてマウントします。マウントしたドライブ内で、参照するアセットの場所に移動します。
1. マウントしたドライブから Illustrator ファイルにアセットをドラッグします。
1. Illustrator ファイルをマウントしたドライブに保存するか、AEM リポジトリに[アップロード](managing-assets-touch-ui.md#uploading-assets)します。
1. ワークフローが完了したら、そのアセットのアセットの詳細ページに移動します。既存の AEM アセットへの参照は、「**[!UICONTROL 参照]**」列の「**[!UICONTROL 依存関係]**」に一覧表示されます。

   ![chlimage_1-258](assets/chlimage_1-258.png)

1. 「**[!UICONTROL 依存関係]**」に表示される参照元のアセットは、現在のファイルとは異なるファイルからも参照できます。参照先のファイルのリストを表示するには、「**[!UICONTROL 依存関係]**」にあるアセットをクリックします。

   ![chlimage_1-259](assets/chlimage_1-259.png)

1. ツールバーの「**[!UICONTROL プロパティを表示]**」アイコンをクリックします。プロパティページで、現在のアセットを参照しているファイルのリストが「**[!UICONTROL 基本]**」タブの「**[!UICONTROL 参照]**」列に表示されます。

   ![chlimage_1-260](assets/chlimage_1-260.png)

## Adobe InDesign 内で AEM アセットを参照として追加 {#add-aem-assets-as-references-in-adobe-indesign}

InDesign ファイル内から AEM アセットを参照するには、AEM アセットを InDesign ファイルにドラッグするか、InDesign ファイルを ZIP ファイルとして書き出します。

参照元のアセットは AEM Assets に既に存在します。You can extract subassets by [configure InDesign server](indesign.md). InDesign ファイルに組み込まれたアセットがサブアセットとして抽出されます。

>[!NOTE]
>
>InDesign サーバーにプロキシが設定されている場合、InDesign のファイルのプレビューが XMP メタデータ内に組み込まれています。この場合、サムネールの抽出は明示的には必要ありません。ただし、InDesign にプロキシが設定されていない場合、InDesign のファイルでサムネールを明示的に抽出する必要があります。

### AEM アセットをドラッグして参照を作成 {#create-references-by-dragging-aem-assets}

この手順は、[Adobe Illustrator で AEM アセットを参照として追加する](#refai)場合の手順と同様です。

### ZIP ファイルに書き出して AEM アセットの参照を作成 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Perform the steps in [Creating Workflow Models](/help/sites-developing/workflows-models.md) to create a new workflow.
1. ドキュメントを書き出すには、Adobe InDesignのパッケージ機能を使用します。
Adobe InDesignは、ドキュメントとリンクされたアセットをパッケージとして書き出すことができます。 この場合、書き出されたフォルダーにはLinksInDesignーが含まれ、フォルダーファイル内のサブアセットが含まれます。
1. ZIP ファイルを作成し、このファイルを AEM リポジトリにアップロードします。
1. 解凍ワークフローを開始します。
1. ワークフローが完了すると、リンクフォルダー内の参照がサブアセットとして自動的に参照されます。参照元のアセットのリストを表示するには、InDesign アセットのアセットの詳細ページに移動して、[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

## Adobe Photoshop 内で AEM アセットを参照として追加 {#refps}

1. WebDav クライアントを使用して、AEM Assets をドライブとしてマウントします。
1. Photoshop ファイルに AEM アセットへの参照を作成するには、Photoshop のリンクを配置機能を使用して、マウントしたドライブで対応するアセットに移動します。

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. Photoshop ファイルをマウントしたドライブに保存するか、AEM リポジトリに[アップロード](managing-assets-touch-ui.md#uploading-assets)します。
1. ワークフローが完了したら、既存の AEM アセットへの参照がアセットの詳細ページに一覧表示されます。

   参照元のアセットを表示するには、アセットの詳細ページで[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

1. The referenced assets also contain the list of assets they are referenced from. To view a list of referenced assets, navigate to the asset details page and close the [rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>複合アセット内のアセットも、ドキュメント ID とインスタンス ID に基づいて参照できます。この機能は、Adobe Illustrator と Adobe Photoshop のバージョンでのみ使用できます。その他の場合、AEM の以前のバージョンと同様に、メインの複合アセット内でリンクされたアセットの相対パスに基づいて参照が実行されます。

## サブアセットの作成 {#generate-subassets}

PDFファイル、AIファイル、Microsoft PowerPointファイル、Apple Keynoteファイル、Adobe InDesignファイルなど、複数ページ形式のサポートされるアセットでは、AEMは、元のアセットの個々のページに対応するサブアセットを生成できます。 これらのサブアセットは *親アセットにリンクされ、複数ページの表示が容易になります* 。 その他の目的の場合、AEMでは、サブアセットは通常のアセットと同様に扱われます。

サブアセットの生成はデフォルトでは無効になっています。サブアセットの生成を有効にするには、次の手順に従います。

1. Experience Managerに管理者としてログインします。 Access **[!UICONTROL Tools > Workflow > Models]**.
1. 「 **[!UICONTROL DAM Update Asset]** workflow」を選択し、「 **[!UICONTROL 編集]**」をクリックします。
1. 「 **[!UICONTROL サイドパネルを]** 切り替え **[!UICONTROL 」をクリックし、「サブアセットを]** 作成」ステップを見つけます。 ワークフロー追加への手順です。 「**[!UICONTROL 同期]**」をクリックします。

サブアセットを生成するには、次のいずれかの操作を行います。

* 新しいアセット： AEMにアップロードされた新しいアセットに対して、 [!UICONTROL DAM Update Assets] ワークフローが実行されます。 サブアセットは、新しい複数ページのアセット用に自動生成されます。
* 既存の複数ページアセット： 次のいずれかの手順に従って、手動で [!UICONTROL DAMアセットの更新] ワークフローを実行します。

   * アセットを選択し、 [!UICONTROL タイムラインをクリックして] 、左側のパネルを開きます。 Alternately, use the keyboard shortcut `alt + 3`. 「 [!UICONTROL 開始ワークフロー]」をクリックし、「 [!UICONTROL DAM Update Asset]」を選択して「 [!UICONTROL 開始]」をクリックし、「 続行」をクリックします。
   * アセットを選択し、ツールバーで [!UICONTROL 作成/ワークフロー] をクリックします。 ポップアップダイアログから「 [!UICONTROL DAM Update Asset] workflow」を選択し、「 [!UICONTROL 開始]」をクリックし、「 [!UICONTROL 続行]」をクリックします。

特にMicrosoft Wordドキュメントの場合は、 **[!UICONTROL DAM Parse Wordドキュメント]** ・ワークフローを実行します。 Microsoft Wordドキュメントのコンテンツから `cq:Page` コンポーネントを生成します。 このドキュメントから抽出された画像は `cq:Page` コンポーネントから参照されます。これらの画像は、サブアセットの生成が無効な場合も抽出されます。

## サブアセットの表示 {#viewing-subassets}

サブアセットは、サブアセットが生成され、選択した複数ページのアセットで使用できる場合にのみ表示されます。 生成されたサブアセットを表示するには、複数ページのアセットを開きます。 ページの左上の領域で、 ![左側のパネルアイコンをクリックし](assets/do-not-localize/aem_leftrail_contentonly.png) 、リストの「 **[!UICONTROL サブアセット]** 」をクリックします。 リストから「 **[!UICONTROL サブアセット]** 」を選択した場合。 Alternately, use the keyboard shortcut `alt + 5`.

![複数ページのアセットの表示サブアセット](assets/view_subassets_simulation.gif)

## 複数ページファイルのページの表示 {#view-pages-of-a-multi-page-file}

AEM Assetsのページビューア機能を使用して、PDF、INDD、PPT、PPTX、AIファイルなどの複数ページのファイルを表示できます。 複数ページのアセットを開き、ページの左上隅にある「 **[!UICONTROL 表示ページ]** 」をクリックします。 ページビューアが開き、アセットのページが表示されます。また、各ページを参照およびズームするためのコントロールが表示されます。

![複数ページのアセットの表示とページの確認](assets/view_multipage_asset_fmr.gif)

InDesign では、InDesign サーバーを使用してページを抽出できます。InDesign ファイルの作成中にページのプレビューが保存されている場合は、ページを抽出するために InDesign サーバーを使用する必要はありません。

次のオプションは、ツールバー、左側のナビゲーションバーおよびページビューアコントロールで使用できます。

* **[!UICONTROL デスクトップアクション]** :AEMデスクトップアプリを使用して、特定のサブアセットを開いたり、表示したりします。 AEMデスクトップアプリを使用する場合は、Desktop Actions [（デスクトップアクション）を](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) 設定する方法を参照してください。

* **[!UICONTROL 「プロパティ]** 」オプションを選択すると、特定のサブアセットの  プロパティページが開きます。

* **[!UICONTROL 注釈]** 」オプションを使用すると、特定のサブアセットに注釈を付けることができます。 別のサブアセットで使用する注釈は、親アセットを表示用に開いたときに収集され、一緒に表示されます。

* **[!UICONTROL 「ページの概要]** 」オプションを選択すると、すべてのサブアセットが同時に表示されます。

* **[!UICONTROL 左側のパネルアイコンをクリックした後の左側のパネルにあるタイムライン]** アクティビティには、 ![ファイルのタイムラインストリームが表示されます](assets/do-not-localize/aem_leftrail_contentonly.png) 。

## Best practices and limitation {#best-practice-limitation-tips}

* サブアセットの生成は、どのExperience Managerのデプロイメントでもリソースを大量に消費する可能性があります。 複雑なアセットがアップロードされたときにサブアセットを生成する場合は、DAMアセットの更新ワークフローで手順を追加します。 サブアセットをオンデマンドで生成する場合は、サブアセットを生成するための別のワークフローを作成します。 専用ワークフローを使用すると、DAM Update Assetワークフローの他の手順をスキップして、計算リソースを保存できます。

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager デスクトップアプリケーションの使用](https://docs.adobe.com/content/help/ja-JP/experience-manager-desktop-app/using/using.html)