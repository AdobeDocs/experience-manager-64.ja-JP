---
title: 複合アセットを管理し、サブアセットを生成します。
description: InDesign、Adobe Illustrator、Photoshopの各ファイル内からAEMアセットへの参照を作成する方法を説明します。 また、ページビューア機能を使用して、複数ページファイル（PDF、INDD、PPT、PPTX、AI ファイルなど）の個々のページを表示する方法についても説明します。
contentOwner: AG
feature: アセット管理
role: User,Admin
exl-id: 9fa44b26-76f7-48e2-a9df-4fd1c0074158
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 47%

---

# サブアセットを含む複合アセットの管理 {#managing-compound-assets}

Adobe Experience Manager (AEM) Assets では、アップロードされたファイルに、リポジトリ内の既存のアセットへの参照が含まれているかどうかを確認できます。この機能は、サポート対象のファイル形式でのみ使用できます。アップロードされたアセットに AEM アセットへの参照が含まれている場合、アップロードされたアセットと参照元のアセットの間に双方向のリンクが作成されます。

Adobe Creative Cloud アプリケーションで AEM アセットを参照することで、冗長性を排除するだけでなく、コラボレーションを強化し、ユーザーの作業効率と生産性を高めることができます。

AEM Assets では&#x200B;**双方向の参照**&#x200B;をサポートしています。参照元のアセットは、アップロードされたファイルのアセットの詳細ページで確認できます。さらに、AEM アセットの参照先のファイルは、参照元アセットのアセット詳細ページで確認できます。

参照は、参照元のアセットのパス、ドキュメント ID およびインスタンス ID に基づいて解決されます。

## Adobe Illustrator:アセットを参照として追加 {#refai}

既存の AEM アセットを、Adobe Illustrator ファイル内から参照できます。

1. [AEM デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)を使用して、AEM Assets リポジトリをローカルコンピューター上のドライブとしてマウントします。マウントしたドライブ内で、参照するアセットの場所に移動します。
1. マウントしたドライブから Illustrator ファイルにアセットをドラッグします。
1. Illustrator ファイルをマウントしたドライブに保存するか、AEM リポジトリに[アップロード](managing-assets-touch-ui.md#uploading-assets)します。
1. ワークフローが完了したら、そのアセットのアセットの詳細ページに移動します。既存の AEM アセットへの参照は、「**[!UICONTROL 参照]**」列の「**[!UICONTROL 依存関係]**」に一覧表示されます。

   ![chlimage_1-258](assets/chlimage_1-258.png)

1. 「**[!UICONTROL 依存関係]**」に表示される参照元のアセットは、現在のファイルとは異なるファイルからも参照できます。参照先のファイルのリストを表示するには、「**[!UICONTROL 依存関係]**」にあるアセットをクリックします。

   ![chlimage_1-259](assets/chlimage_1-259.png)

1. ツールバーの「**[!UICONTROL プロパティを表示]**」アイコンをクリックします。プロパティページで、現在のアセットを参照しているファイルのリストが「**[!UICONTROL 基本]**」タブの「**[!UICONTROL 参照]**」列に表示されます。

   ![chlimage_1-260](assets/chlimage_1-260.png)

## Adobe InDesign:アセットを参照として追加 {#add-aem-assets-as-references-in-adobe-indesign}

InDesign ファイル内から AEM アセットを参照するには、AEM アセットを InDesign ファイルにドラッグするか、InDesign ファイルを ZIP ファイルとして書き出します。

参照元のアセットは AEM Assets に既に存在します。[設定サーバー](indesign.md)でサブInDesignを抽出できます。 InDesign ファイルに組み込まれたアセットがサブアセットとして抽出されます。

>[!NOTE]
>
>InDesign サーバーにプロキシが設定されている場合、InDesign のファイルのプレビューが XMP メタデータ内に組み込まれています。この場合、サムネールの抽出は明示的には必要ありません。ただし、InDesign にプロキシが設定されていない場合、InDesign のファイルでサムネールを明示的に抽出する必要があります。

INDDファイルがアップロードされると、リポジトリ内に`xmpMM:InstanceID`プロパティと`xmpMM:DocumentID`プロパティを持つアセットに対するクエリを実行することで、参照が取得されます。

###  アセットをドラッグして参照を作成  {#create-references-by-dragging-aem-assets}

この手順は、[Adobe Illustrator](#refai)でアセットを参照として追加する場合の手順と似ています。

### ZIP ファイルに書き出してアセットの参照を作成 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. [ワークフローモデルの作成](/help/sites-developing/workflows-models.md)の手順を実行して、新しいワークフローを作成します。
1. Adobe InDesign](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html)の[パッケージ機能を使用して、ドキュメントを書き出します。Adobe InDesignは、ドキュメントとリンクされたアセットをパッケージとして書き出すことができます。 この場合、書き出されたフォルダーには、フォルダーファイル内のサブアセットを含む`Links`InDesignーが含まれます。 `Links`フォルダーは、INDDファイルと同じフォルダーに存在します。
1. ZIP ファイルを作成し、このファイルを AEM リポジトリにアップロードします。
1. 解凍ワークフローを開始します。
1. ワークフローが完了すると、リンクフォルダー内の参照がサブアセットとして自動的に参照されます。参照元のアセットのリストを表示するには、InDesign アセットのアセットの詳細ページに移動して、[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

## Adobe Photoshop:アセットを参照として追加 {#refps}

1. WebDav クライアントを使用して、AEM Assets をドライブとしてマウントします。
1. Photoshop ファイルに AEM アセットへの参照を作成するには、Photoshop のリンクを配置機能を使用して、マウントしたドライブで対応するアセットに移動します。

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. Photoshopファイルをマウントしたドライブに保存するか、AEMリポジトリに[アップロード](managing-assets-touch-ui.md#uploading-assets)します。
1. ワークフローが完了したら、既存の AEM アセットへの参照がアセットの詳細ページに一覧表示されます。

   参照元のアセットを表示するには、アセットの詳細ページで[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

1. 参照元のアセットには、参照元のアセットのリストも含まれています。参照されているアセットのリストを表示するには、アセットの詳細ページに移動して、[レール](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

>[!NOTE]
>
>複合アセット内のアセットも、ドキュメント ID とインスタンス ID に基づいて参照できます。この機能は、Adobe Illustrator と Adobe Photoshop のバージョンでのみ使用できます。その他の場合、AEM の以前のバージョンと同様に、メインの複合アセット内でリンクされたアセットの相対パスに基づいて参照が実行されます。

## サブアセットの作成 {#generate-subassets}

複数ページ形式(PDFファイル、AIファイル、Microsoft PowerPointファイル、Apple Keynoteファイル、Adobe InDesignファイル)のアセットをサポートしている場合、AEMは元のアセットの個々のページに対応するサブアセットを生成できます。 これらのサブアセットは&#x200B;*親*&#x200B;アセットにリンクされ、複数ページ表示が容易になります。 その他の目的では、サブアセットはAEMでは通常のアセットと同じように扱われます。

サブアセットの生成はデフォルトでは無効になっています。サブアセットの生成を有効にするには、次の手順に従います。

1. 管理者としてExperience Managerにログインします。 **[!UICONTROL ツール/ワークフロー/モデル]**&#x200B;にアクセスします。
1. 「**[!UICONTROL DAMアセットの更新]**」ワークフローを選択し、「**[!UICONTROL 編集]**」をクリックします。
1. **[!UICONTROL サイドパネルを切り替え]**&#x200B;をクリックし、**[!UICONTROL サブアセットを作成]**&#x200B;の手順を見つけます。 ワークフローにステップを追加します。 「**[!UICONTROL 同期]**」をクリックします。

サブアセットを生成するには、次のいずれかの操作を行います。

* 新しいアセット：AEMにアップロードされた新しいアセットに対して、[!UICONTROL DAMアセットの更新]ワークフローが実行されます。 新しい複数ページアセット用にサブアセットが自動生成されます。
* 既存の複数ページアセット：次のいずれかの手順に従って、[!UICONTROL DAMアセットの更新]ワークフローを手動で実行します。

   * アセットを選択し、「[!UICONTROL タイムライン]」をクリックして左のパネルを開きます。 または、キーボードショートカット`alt + 3`を使用します。 「[!UICONTROL ワークフローを開始]」をクリックし、「[!UICONTROL DAMアセットの更新]」を選択して、「[!UICONTROL 開始]」をクリックし、「[!UICONTROL 続行]」をクリックします。
   * アセットを選択し、ツールバーの[!UICONTROL 作成/ワークフロー]をクリックします。 ポップアップダイアログで、「[!UICONTROL DAMアセットの更新]」ワークフローを選択し、「[!UICONTROL 開始]」をクリックして、「[!UICONTROL 続行]」をクリックします。

特にMicrosoft Wordドキュメントの場合は、**[!UICONTROL DAM Wordドキュメントの解析]**&#x200B;ワークフローを実行します。 Microsoft Wordドキュメントの内容から`cq:Page`コンポーネントが生成されます。 このドキュメントから抽出された画像は `cq:Page` コンポーネントから参照されます。これらの画像は、サブアセットの生成が無効な場合も抽出されます。

## サブアセットの表示 {#viewing-subassets}

サブアセットは、サブアセットが生成され、選択した複数ページのアセットで使用できる場合にのみ表示されます。 生成されたサブアセットを表示するには、複数ページのアセットを開きます。 ページの左上にある「![左パネルアイコン](assets/do-not-localize/aem_leftrail_contentonly.png)」をクリックし、リストから「**[!UICONTROL サブアセット]**」をクリックします。 リストから「**[!UICONTROL サブアセット]**」を選択します。 または、キーボードショートカット`alt + 5`を使用します。

![複数ページアセットのサブアセットの表示](assets/view_subassets_simulation.gif)

## 複数ページファイルのページの表示 {#view-pages-of-a-multi-page-file}

AEM Assetsのページビューア機能を使用して、PDF、INDD、PPT、PPTX、AIファイルなどの複数ページファイルを表示できます。 複数ページのアセットを開き、ページの左上隅にある「**[!UICONTROL ページを表示]**」をクリックします。 アセットのページと、各ページを参照およびズームするためのコントロールが表示されるページビューア。

![複数ページアセットのページの表示と表示](assets/view_multipage_asset_fmr.gif)

InDesign では、InDesign サーバーを使用してページを抽出できます。InDesign ファイルの作成中にページのプレビューが保存されている場合は、ページを抽出するために InDesign サーバーを使用する必要はありません。

ツールバー、左側のレールおよびページビューアコントロールで、次のオプションを使用できます。

* **[!UICONTROL AEMデスク]** トップアプリケーションを使用して特定のサブアセットを開く、または表示するデスクトップアクション。AEMデスクトップアプリケーションを使用している場合は、[デスクトップアクションの設定](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#desktopactions-v2)方法を参照してください。

* **[!UICONTROL 「]** プロパティ」オプションは、特  定のサブアセットのプロパティページを開きます。

* **** 「注釈」オプションを使用すると、特定のサブアセットに注釈を付けることができます。別のサブアセットで使用する注釈は、親アセットを表示用に開く際に収集され、一緒に表示されます。

* **[!UICONTROL 「ページの]** 概要」オプションでは、すべてのサブアセットが同時に表示されます。

* **** 左パネルアイコンをクリックした後の左パネルからタイムラインオ ![プション](assets/do-not-localize/aem_leftrail_contentonly.png) に、ファイルのアクティビティストリームが表示されます。

## ベストプラクティスと制限事項 {#best-practice-limitation-tips}

* サブアセットの生成は、あらゆるリソースのデプロイメントで非常にExperience Managerを消費します。 複雑なアセットがアップロードされたときにサブアセットを生成する場合は、 DAMアセットの更新ワークフローにステップを追加します。 オンデマンドでサブアセットを生成する場合は、サブアセットを生成する別のワークフローを作成します。 専用のワークフローを使用すると、 DAMアセットの更新ワークフローの他の手順をスキップして、計算リソースを保存できます。

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager デスクトップアプリケーションの使用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)

