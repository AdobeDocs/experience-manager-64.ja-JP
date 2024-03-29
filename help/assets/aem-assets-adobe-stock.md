---
title: ' [!DNL Adobe Experience Manager Assets] での [!DNL Adobe Stock] アセットの管理。'
description: ' [!DNL Adobe Experience Manager] 内から [!DNL Adobe Stock] アセットを、検索、取得、ライセンス、管理します。ライセンスされたアセットをその他のデジタルアセットとして使用します。'
contentOwner: AG
feature: Search,Adobe Stock
role: User,Admin
exl-id: f360abaf-a812-46ed-a160-ff569b6bec1c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 89%

---

# [!DNL Adobe Experience Manager Assets] での [!DNL Adobe Stock] アセットの使用 {#use-adobe-stock-assets-in-aem-assets}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[!DNL Adobe Stock] エンタープライズプランと [!DNL Experience Manager Assets] を統合すると、[!DNL Experience Manager] の強力なアセット管理機能を使用して、ライセンスが必要なアセットをクリエイティブプロジェクトやマーケティングプロジェクトに幅広く活用できます。

[!DNL Adobe Stock] サービスは、あらゆるクリエイティブプロジェクトに使用できる、適切にキュレーションされ、著作権使用料が不要で質の高い何百万点もの写真、ベクター、イラスト、ビデオ、テンプレートおよび 3D アセットを提供します。[!DNL Experience Manager] ユーザーは、[!DNL Experience Manager] に保存されている [!DNL Adobe Stock] アセットの検出、プレビューおよびライセンスの取得を、[!DNL Experience Manager] インターフェイスからすばやく実行できます。

## 前提条件 {#prerequisites}

この統合を利用するには、[Adobe Stock エンタープライズプラン](https://stockenterprise.adobe.com/jp/)[!DNL Experience Manager]と、最新のサービスパック 2 を展開した 6.4 が必要です。の場合 [!DNL Experience Manager] 6.4 サービスパックの詳細は、次を参照してください [リリースノート](/help/release-notes/sp-release-notes.md).

## [!DNL Experience Manager] と [!DNL Adobe Stock] の統合  {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager] と [!DNL Adobe Stock] の間でやり取りができるようにするには、[!DNL Experience Manager] 内で IMS 設定と [!DNL Adobe Stock] 設定を作成します。

>[!NOTE]
>
>統合は、組織の [!DNL Experience Manager] 管理者と [!DNL Admin Console] 管理者のみ実行できます。統合の実行には管理者特権が必要です。

### IMS 設定の作成 {#create-an-ims-configuration}

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／**[!UICONTROL セキュリティ]**／**[!UICONTROL Adobe IMS 設定]**&#x200B;に移動します。「**[!UICONTROL 作成]**」をクリックし、**[!UICONTROL クラウドソリューション]**／**[!UICONTROL Adobe Stock]** を選択します。
1. 既存の証明書を再利用するか、「 」を選択します **[!UICONTROL 新しい証明書を作成]**.
1. 「**[!UICONTROL 証明書を作成]**」をクリックします。公開鍵を作成したら、ダウンロードします。 「**[!UICONTROL 次へ]**」をクリックします。必要な値をすぐに指定する場合は、[!UICONTROL Adobe IMS テクニカルアカウント設定]画面を開いたままにします。
1. [アドビ開発者コンソール](https://console.adobe.io)にアクセスします。自身のアカウントに、統合するために必要な、組織の管理者権限があることを確認します。
1. 「**[!UICONTROL 新しいプロジェクトを作成]**」をクリックし、「**[!UICONTROL API を追加]**」をクリックします。使用可能な API のリストから **[!UICONTROL Adobe Stock]** を選択します。「[!UICONTROL OAUTH 2.0 Web]」を選択します。
1. 「**[!UICONTROL デフォルトのリダイレクト URI]**」と「**[!UICONTROL リダイレクト URI パターン]**」の値を指定します。「**[!UICONTROL 設定済み API を保存]**」をクリックします。生成された ID と秘密鍵をコピーします。
1. [!UICONTROL Adobe IMS テクニカルアカウント設定]画面で、「**[!UICONTROL タイトル]**」、「**[!UICONTROL 認証サーバー]**」、「**[!UICONTROL API キー]**」、「**[!UICONTROL クライアントの秘密鍵]**」、「**[!UICONTROL ペイロード]**」の各ボックスに値を入力します。これらの値について詳しくは、[JWT 認証のクイックスタート](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)（英語）を参照してください。

<!-- TBD: Update the URL when the new URL is available. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### [!DNL Adobe Stock] での [!DNL Experience Manager] 設定の作成  {#create-adobe-stock-configuration-in-aem}

1. [!DNL Experience Manager] ユーザーインターフェイスで、**[!UICONTROL ツール]**／ **[!UICONTROL Cloud Services]** ／ **[!UICONTROL Adobe Stock]** に移動します。
1. 「**[!UICONTROL 作成]**」をクリックして設定を作成し、その設定を既存の IMS 設定に関連付けます。環境パラメーターとして「`PROD`」を選択します。
1. 「**[!UICONTROL ライセンスが必要なアセットのパス]**」フィールドの場所をそのまま残します。この場所を [!DNL Adobe Stock] アセットを保存する場所に変更しないでください。
1. 必要なプロパティをすべて追加して、作成を完了します。 「**[!UICONTROL 保存して閉じる]**」をクリックします。
1. アセットのライセンスを取得できる [!DNL Experience Manager] ユーザーまたはグループを追加します。

>[!NOTE]
>
>複数の [!DNL Adobe Stock] の設定を行う場合は、ユーザーの環境設定パネルで目的の設定を選択します (**[!UICONTROL AEM]** > **[!UICONTROL ユーザーアイコン]** > **[!UICONTROL ユーザーの環境設定]** > **[!UICONTROL 在庫設定]**) をクリックします。

## [!DNL Adobe Stock] での [!DNL Experience Manager] アセットの使用と管理  {#usemanage}

この機能を使用すると、[!DNL Experience Manager Assets] で [!DNL Adobe Stock] アセットを操作できます。[!DNL Experience Manager] のユーザーインターフェイス内から [!DNL Adobe Stock] アセットを検索し、必要なアセットのライセンスを取得できます。

[!DNL Experience Manager] 内で [!DNL Adobe Stock] アセットのライセンスを取得すると、そのアセットを通常のアセットと同様に使用および管理できます。ユーザーは [!DNL Experience Manager] 内でアセットの検索およびプレビュー、アセットのコピーおよび公開、[!DNL Brand Portal] でのアセットの共有、[!DNL Experience Manager] デスクトップアプリケーション経由でのアセットのアクセスおよび使用を行うことができます。

![Adobe Experience Manager Workspace からのAdobe Stock Assets の検索と結果のフィルタリング](assets/adobe-stock-search-results-workspace.png)

*図：を検索 [!DNL Adobe Stock] アセットとフィルターの結果 [!DNL Experience Manager] インターフェイス。*

**A.** [!DNL Adobe Stock] ID が指定されているアセットと類似しているアセットを検索します。**B.** 選択した形状や向きと一致するアセットを検索します。**C.** サポートされているアセットタイプのいずれかを検索します。**D.** フィルターウィンドウを開く／折りたたみます。**E.** 選択したアセットのライセンスを取得して [!DNL Experience Manager] に保存します。**F.** アセットを透かし付きで [!DNL Experience Manager] に保存します。**G.** 選択したアセットと類似したアセットを [!DNL Adobe Stock] の web サイトで調べます。**H.** 選択したアセットを [!DNL Adobe Stock] の web サイトに表示します。**I.** 検索結果から選択したアセットの数。**J.** カード表示とリスト表示を切り替えます。

### アセットの検索 {#find-assets}

[!DNL Experience Manager] ユーザーは、[!DNL Experience Manager] と [!DNL Adobe Stock] の両方でアセットを検索できます。検索場所を [!DNL Adobe Stock] に限定しない場合は、[!DNL Experience Manager] と [!DNL Adobe Stock] からの検索結果が表示されます。

* [!DNL Adobe Stock] アセットを検索するには、**[!UICONTROL ナビゲーション]**／**[!UICONTROL アセット]**／**[!UICONTROL Adobe Stock を検索]**&#x200B;をクリックします。

* 複数のアセットを検索するには [!DNL Adobe Stock] および [!DNL Experience Manager Assets]、検索をクリック ![search_icon](assets/search_icon.png).

また、アセットを選択するには、検索バーに「`Location: Adobe Stock`」と入力します。[!DNL Adobe Stock][!DNL Experience Manager] は、検索されたアセットに対する高度なフィルタリング機能を備えており、サポートされているアセットのタイプや画像の向き、ライセンスの状態などのフィルターを使用して、必要なアセットをすばやく見つけることができます。

>[!NOTE]
>
>[!DNL Adobe Stock] から検索されたアセットは [!DNL Experience Manager] に表示されるだけです。[アセットを保存](/help/assets/aem-assets-adobe-stock.md#saveassets)するか、[アセットにライセンスを付与して保存](/help/assets/aem-assets-adobe-stock.md#licenseassets)した後でないと、[!DNL Adobe Stock] アセットを取得して [!DNL Experience Manager] リポジトリーに保存することはできません。既に [!DNL Experience Manager] に保存されているアセットが表示され、参照やアクセスが簡単にできるようにハイライトされます。また、[!DNL Stock] アセットは、ソースが [!DNL Stock] であることを示すいくつかの追加メタデータとともに保存されます。

![ Experience Manager の検索フィルターと、検索結果内でハイライトされている Adobe Stock アセット](assets/aem-search-filters2.jpg)

*図：[!DNL Experience Manager] の検索フィルターと、検索結果内でハイライトされている [!DNL Adobe Stock] アセット。*

### 必要なアセットの保存と表示 {#saveassets}

[!DNL Experience Manager] に保存するアセットを選択します。上部ツールバーの「[!UICONTROL 保存]」をクリックし、アセットの名前と保存場所を指定します。ライセンスが不要なアセットはローカルに透かし付きで保存されます。

アセットの検索を次回実行すると、保存済みのアセットは、[!DNL Experience Manager Assets] で使用可能であることを示すバッジ付きでハイライトされます。

>[!NOTE]
>
>最近追加されたアセットには、ライセンスが許諾されていることを示すバッジではなく、新しいアセットであることを示すバッジが表示されます。

### アセットのライセンス取得 {#licenseassets}

[!DNL Adobe Stock] エンタープライズプランの割り当てを使用することで、[!DNL Adobe Stock] アセットのライセンスを取得できます。ライセンスを許諾されたアセットは透かしなしで保存され、[!DNL Experience Manager Assets] で検索することも使用することも可能になります。

![Adobe Stock アセットのライセンスを許諾して Experience Manager Assets に保存するためのダイアログ](assets/aem-stock_licenseandsave.jpg)

*図：[!DNL Experience Manager Assets] で [!DNL Adobe Stock] アセットのライセンスを取得して保存するダイアログ。*

### メタデータおよびアセットプロパティへのアクセス {#access-metadata-and-asset-properties}

メタデータ（[!DNL Experience Manager] に保存されているアセットの [!DNL Adobe Stock] メタデータプロパティを含む）にアクセスしてプレビューし、アセットの&#x200B;**[!UICONTROL ライセンス参照]**&#x200B;を追加できます。ただし、ライセンス参照の更新は [!DNL Experience Manager] と [!DNL Adobe Stock] Web サイトの間で同期されません。

ユーザーは、ライセンスを許諾されたアセットとライセンスを許諾されていないアセットの両方を表示できます。

![保存されているアセットのメタデータとライセンス参照の表示、アクセス](assets/metadata_properties.jpg)

*図：保存されているアセットのメタデータとライセンス参照の表示、アクセス。*

## 既知の制限事項 {#known-limitations}

* **編集画像の警告が表示されない**：画像のライセンスを取得する場合、ユーザーは画像が「編集のみ使用」かどうか確認できません。管理者は誤用を防ぐために、Admin Console から編集用アセットへのアクセスをオフにできます。

* **間違ったライセンスの種類が表示される**：[!DNL Experience Manager] で、アセットに対して正しくないライセンスタイプが表示される可能性があります。[!DNL Adobe Stock] Web サイトにログインすると、ライセンスタイプを確認できます。

* **参照フィールドとメタデータが同期されない**：ユーザーがライセンス参照フィールドを更新すると、そのライセンス参照情報は [!DNL Experience Manager] で更新されますが、[!DNL Adobe Stock] Web サイト上では更新されません。同様に、[!DNL Adobe Stock] Web サイトで参照フィールドを更新すると、更新情報が [!DNL Experience Manager] には反映されません。

>[!MORELIKETHIS]
>
>* [ [!DNL Experience Manager Assets] での  [!DNL Adobe Stock]  アセットの使用について説明するビデオチュートリアル](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html?lang=ja)
>* [[!DNL Adobe Stock] エンタープライズプランのヘルプ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-stock-enterprise.ug.html)
>* [[!DNL Adobe Stock] FAQ](https://helpx.adobe.com/jp/stock/faq.html)

