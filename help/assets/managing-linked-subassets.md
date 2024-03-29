---
title: 複合アセットを管理し、サブアセットを生成します。
description: への参照を作成する方法を説明します。 [!DNL Experience Manager] InDesign、Adobe Illustrator、Photoshopの各ファイル内のアセット また、ページビューア機能を使用して複数ページファイルの個々のページを表示する方法についても説明します。
contentOwner: AG
feature: Asset Management
role: User,Admin
exl-id: 9fa44b26-76f7-48e2-a9df-4fd1c0074158
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 55%

---

# サブアセットを含む複合アセットの管理 {#managing-compound-assets}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager Assets では、アップロードされたファイルに、リポジトリ内の既存のアセットへの参照が含まれているかどうかを確認できます。 この機能は、サポート対象のファイル形式でのみ使用できます。アップロードされたアセットに [!DNL Experience Manager] アセットへの参照が含まれている場合、アップロードされたアセットと参照先のアセットの間に双方向のリンクが作成されます。

冗長性の排除に加え、参照 [!DNL Experience Manager] Adobe Creative Cloudアプリケーションのアセットは、コラボレーションを強化し、ユーザーの効率と生産性を向上させます。

[!DNL Experience Manager] Assets がサポート **双方向参照**. 参照元のアセットは、アップロードされたファイルのアセットの詳細ページで確認できます。さらに、の参照ファイルを表示できます。 [!DNL Experience Manager] 参照元のアセットのアセットの詳細ページにあるアセット。

参照は、参照元のアセットのパス、ドキュメント ID およびインスタンス ID に基づいて解決されます。

## Adobe Illustrator:アセットを参照として追加 {#refai}

既存の [!DNL Experience Manager] Adobe Illustratorファイル内のアセット。

1. [[!DNL Experience Manager]  デスクトップアプリケーション](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app.html)を使用して、 Assets リポジトリをローカルコンピューター上のドライブとしてマウントします。[!DNL Experience Manager]マウントされたドライブ内で、参照するアセットの場所に移動します。
1. マウントしたドライブからIllustratorファイルにアセットをドラッグします。
1. Illustrator ファイルをマウントしたドライブに保存するか、 リポジトリに[アップロード](managing-assets-touch-ui.md#uploading-assets)します。[!DNL Experience Manager]
1. ワークフローが完了したら、そのアセットのアセットの詳細ページに移動します。既存への参照 [!DNL Experience Manager] アセットは、 **[!UICONTROL 依存関係]** 内 **[!UICONTROL 参照]** 列。

   ![chlimage_1-258](assets/chlimage_1-258.png)

1. 「**[!UICONTROL 依存関係]**」に表示される参照元のアセットは、現在のファイルとは異なるファイルからも参照できます。参照先のファイルのリストを表示するには、「**[!UICONTROL 依存関係]**」にあるアセットをクリックします。

   ![chlimage_1-259](assets/chlimage_1-259.png)

1. ツールバーの「**[!UICONTROL プロパティを表示]**」アイコンをクリックします。プロパティページで、現在のアセットを参照しているファイルのリストが「**[!UICONTROL 基本]**」タブの「**[!UICONTROL 参照]**」列に表示されます。

   ![chlimage_1-260](assets/chlimage_1-260.png)

## Adobe InDesign:アセットを参照として追加 {#add-aem-assets-as-references-in-adobe-indesign}

参照する [!DNL Experience Manager] アセットファイル内からInDesignをドラッグ [!DNL Experience Manager] アセットをInDesignファイルに書き出すか、InDesignファイルを ZIP ファイルとして書き出します。

参照元のアセットはに既に存在します [!DNL Experience Manager] アセット。 サブアセットは、 [InDesignサーバーの設定](indesign.md). InDesign ファイルに組み込まれたアセットがサブアセットとして抽出されます。

>[!NOTE]
>
>InDesignサーバーがプロキシ化されている場合、InDesignファイルのプレビューがXMPメタデータ内に埋め込まれます。 この場合、サムネールの抽出は明示的には必要ありません。ただし、InDesignサーバーがプロキシされていない場合は、サムネールをInDesignファイル用に明示的に抽出する必要があります。

INDD ファイルがアップロードされると、`xmpMM:InstanceID` および `xmpMM:DocumentID` プロパティがリポジトリにあるアセットにクエリを実行することで、参照が取得されます。

### アセットをドラッグして参照を作成  {#create-references-by-dragging-aem-assets}

この手順は、 [Adobe Illustratorでアセットを参照として追加](#refai).

### ZIP ファイルに書き出してアセットの参照を作成 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. の手順を実行します。 [ワークフローモデルの作成](/help/sites-developing/workflows-models.md) をクリックして、新しいワークフローを作成します。
1. 以下を使用： [Adobe InDesignのパッケージ機能](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) をクリックして、ドキュメントを書き出します。Adobe InDesignは、ドキュメントとリンクされたアセットをパッケージとして書き出すことができます。 この場合、書き出されたフォルダーには `Links` フォルダーファイル内のサブアセットを格納するInDesignー。 この `Links` フォルダーが INDD ファイルと同じフォルダーに存在する。
1. ZIP ファイルを作成し、このファイルを [!DNL Experience Manager] リポジトリにアップロードします。
1. 解凍ワークフローを開始します。
1. ワークフローが完了すると、リンクフォルダー内の参照がサブアセットとして自動的に参照されます。参照元のアセットのリストを表示するには、InDesign アセットのアセットの詳細ページに移動して、[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

## Adobe Photoshop:アセットを参照として追加 {#refps}

1. WebDav クライアントを使用して、マウントします。 [!DNL Experience Manager] ドライブとしてのアセット。
1. への参照を作成するには [!DNL Experience Manager] Photoshopファイル内のアセットで、Photoshopの「リンクを配置」機能を使用して、マウントされたドライブ内の対応するアセットに移動します。

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. Photoshopファイルをマウントしたドライブに保存するか、 [アップロード](managing-assets-touch-ui.md#uploading-assets) から [!DNL Experience Manager] リポジトリ。
1. ワークフローが完了したら、既存の [!DNL Experience Manager] アセットへの参照がアセットの詳細ページに一覧表示されます。

   参照元のアセットを表示するには、アセットの詳細ページで[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

1. 参照元のアセットには、参照元のアセットのリストも含まれています。参照元のアセットのリストを表示するには、アセットの詳細ページに移動して、 [パネル](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>複合アセット内のアセットも、ドキュメント ID とインスタンス ID に基づいて参照できます。この機能は、Adobe IllustratorおよびAdobe Photoshopバージョンでのみ使用できます。 その他の場合は、AEMの以前のバージョンと同様に、メイン複合アセット内のリンクされたアセットの相対パスに基づいて参照がおこなわれます。

## サブアセットの作成 {#generate-subassets}

複数ページ形式 (PDFファイル、AI ファイル、Microsoft PowerPoint およびApple Keynote ファイル、Adobe InDesignファイル ) のアセットをサポートする場合 [!DNL Experience Manager] では、元のアセットの個々のページに対応するサブアセットを生成できます。 これらのサブアセットは&#x200B;*親*&#x200B;アセットにリンクされ、複数ページ表示を容易にします。その他の目的では、サブアセットはAEMでは通常のアセットと同じように扱われます。

サブアセットの生成はデフォルトでは無効になっています。サブアセットの生成を有効にするには、次の手順に従います。

1. 管理者としてExperience Managerにログインします。 **[!UICONTROL ツール／ワークフロー／モデル]**&#x200B;にアクセスします。
1. **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを選択し、**[!UICONTROL 編集]**&#x200B;をクリックしてください。
1. **[!UICONTROL サイドパネルを切り替え]**&#x200B;をクリックし、**[!UICONTROL サブアセットを作成]**&#x200B;のステップを探してください。ワークフローにステップを追加します。**[!UICONTROL 同期]**&#x200B;をクリックします。

サブアセットを生成するには、以下のいずれかの操作を行います。

* 新しいアセット：この [!UICONTROL DAM アセットの更新] ワークフローは、AEMにアップロードされた新しいアセットで実行されます。 複数ページの新しいアセットに対してサブアセットが自動生成されます。
* 既存の複数ページアセット：手動で [!UICONTROL DAM アセットの更新]ワークフローを次のいずれかのステップに従って実行します。

   * アセットを選択し、[!UICONTROL タイムライン]をクリックして、左側のパネルを開きます。または、キーボードショートカット `alt + 3` を使用します。[!UICONTROL ワークフローを開始]をクリックし、[!UICONTROL DAM アセットの更新]を選択して、[!UICONTROL 開始]をクリックしてから、[!UICONTROL 続行]をクリックしてください。
   * アセットを選択し、ツールバーから[!UICONTROL 作成／ワークフロー]をクリックしてください。ポップアップダイアログで、[!UICONTROL DAM アセットの更新]ワークフローを選択して、[!UICONTROL 開始]をクリックしてから、[!UICONTROL 続行]をクリックしてください。

特に Microsoft Word ドキュメントの場合は、**[!UICONTROL DAM Word ドキュメントの解析]**&#x200B;ワークフローを実行します。これにより、`cq:Page`コンポーネントを Microsoft Word ドキュメントのコンテンツから生成します。このドキュメントから抽出された画像は `cq:Page` コンポーネントから参照されます。これらの画像は、サブアセットの生成が無効な場合も抽出されます。

## サブアセットの表示 {#viewing-subassets}

サブアセットが生成され、選択した複数ページのアセットで使用できる場合にのみ、サブアセットが表示されます。生成されたサブアセットを表示するには、複数ページのアセットを開きます。ページの左上の領域で、 ![左パネルアイコン](assets/do-not-localize/aem_leftrail_contentonly.png) をクリックし、 **[!UICONTROL サブアセット]** を選択します。 リストから&#x200B;**[!UICONTROL サブアセット]**&#x200B;を選択した場合。または、キーボードショートカット `alt + 5` を使用します。

![複数ページアセットのサブアセットの表示](assets/view_subassets_simulation.gif)

## 複数ページファイルのページの表示 {#view-pages-of-a-multi-page-file}

ページビューア機能 ( [!DNL Experience Manager] アセット。 複数ページのアセットを開き、ページの左上隅にある&#x200B;**[!UICONTROL ページを表示]**&#x200B;をクリックしてください。開いたページビューアにはアセットのページと、各ページを参照およびズームするためのコントロールが表示されます。

![複数ページアセットのページの表示](assets/view_multipage_asset_fmr.gif)

InDesignの場合は、ページサーバーを使用してInDesignを抽出できます。 ページのプレビューがInDesignファイルの作成中に保存される場合、InDesign Serverはページを抽出する必要はありません。

ツールバー、左側のレールおよびページビューアコントロールで、次のオプションを使用できます。

* [!DNL Experience Manager] デスクトップアプリケーションを使用して、特定のサブアセットを開くまたは表示する&#x200B;**[!UICONTROL デスクトップアクション]**。[!DNL Experience Manager] デスクトップアプリケーションを使用している場合は、[デスクトップアクションの設定](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#desktopactions-v2)を参照してください。

* **[!UICONTROL プロパティ]**&#x200B;オプションを選択すると、特定のサブアセットの[!UICONTROL プロパティ]ページが開きます。

* **[!UICONTROL 注釈]**&#x200B;オプションを使用すると、特定のサブアセットに注釈を付けることができます。別のサブアセットで使用する注釈は、親アセットを表示用に開いたときに収集および表示されます。

* 「**[!UICONTROL ページ概要]**」オプションを選択すると、すべてのサブアセットが同時に表示されます。

* **[!UICONTROL タイムライン]** 「 」オプションをクリックし、 ![左パネルアイコン](assets/do-not-localize/aem_leftrail_contentonly.png) ファイルのアクティビティストリームを表示します。

## ベストプラクティスと制限事項 {#best-practice-limitation-tips}

* サブアセットの生成は、あらゆるリソースのデプロイメントで非常にExperience Managerを消費する可能性があります。 複雑なアセットがアップロードされたときにサブアセットを生成する場合は、DAM アセットの更新ワークフローにこのステップを追加してください。オンデマンドでサブアセットを生成する場合は、別のワークフローを作成してサブアセットを生成します。専用のワークフローを使用すると、DAM アセットの更新ワークフローの他の手順をスキップし、計算リソースを節約することができます。

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager デスクトップアプリケーションの使用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)

