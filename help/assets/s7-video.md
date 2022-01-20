---
title: ビデオ
description: Dynamic Media Classicに自動エンコーディング用にExperience Manager Assets用のビデオをアップロードできる、一元化されたビデオアセット管理について説明します。 Experience Manager Assetsから直接Dynamic Media Classicビデオにアクセスすることもできます。 Dynamic Media Classicビデオの統合により、自動デバイスと自動帯域幅検出を使用して、最適化されたビデオの範囲をすべての画面に広げることができます。
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: managing-assets
content-type: reference
exl-id: 081e7db0-95cc-4260-8f08-318cd7d9d5b4
feature: Video
role: User
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 30%

---

# ビデオ {#video}

Assets では、ビデオを Assets に直接アップロードして、Dynamic Media Classicに自動エンコーディングできる、一元化されたビデオアセット管理を実現しています。 Assets から直接Dynamic Media Classicビデオにアクセスして、ページをオーサリングすることもできます。

Dynamic Media Classicビデオの統合により、最適化されたビデオがすべての画面に広がります（自動デバイスと帯域幅の検出）。

この **[!UICONTROL Scene7 Video]** コンポーネントは、デスクトップ、タブレット、モバイルで適切な形式と画質のビデオを再生するために、デバイスと帯域幅の検出を自動的に実行します。

単一のビデオアセットだけでなく、アダプティブビデオセットを含めることができます。 アダプティブビデオセットは、複数の画面をシームレスに再生するために必要なすべてのビデオレンディションのコンテナです。 アダプティブビデオセットは、異なるビットレートおよび形式でエンコードされた、同じビデオのバージョンをグループ化します。 例： 400 kbps、800 kbps、1000 kbps。 複数の画面タイプにわたるアダプティブビデオのストリーミングには、S7 ビデオコンポーネントと共にアダプティブビデオセットを使用します。 例えば、デスクトップ、iOS、Android、BlackBerry、Windows モバイルデバイスなどです。

詳しくは、 [Dynamic Media Classicのアダプティブビデオセットに関するドキュメントを参照してください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/video-profiles.html#dynamicmedia).

## FFMPEG とDynamic Media Classicについて {#about-ffmpeg-and-scene}

デフォルトのビデオエンコーディングプロセスは、ビデオプロファイルとの FFMPEG ベースの統合の使用に基づいています。そのため、組み込みの DAM 収集ワークフローには、ffmpeg ベースの次の 2 つのワークフローのステップが含まれています。

* FFMPEG のサムネール
* FFMPEG エンコーディング

Dynamic Media Classic統合を有効にして設定しても、標準の DAM 取り込みワークフローからこれら 2 つのワークフローステップが自動的に削除または非アクティブ化されることはありません。 既にExperience Managerで FFMPEG ベースのビデオエンコーディングを使用している場合は、FFMPEG がオーサリング環境にインストールされている可能性があります。 この場合、DAM を使用して取り込まれた新しいビデオは 2 回エンコードされます。FFMPEG エンコーダーから、Dynamic Media Classic統合から 1 回。

AEMと FFMPEG で設定された FFMPEG ベースのビデオエンコーディングを使用している場合、DAM 取り込みワークフローから 2 つの FFMPEG ワークフローを削除できます。

## サポートされるファイル形式 {#supported-formats}

Scene7 ビデオコンポーネントでは次の形式がサポートされます。

* F4V H.264
* MP4 H.264

## ビデオのアップロード先の指定 {#deciding-where-to-upload-your-video}

ビデオアセットのアップロード先の指定は、次の条件によって決まります。

* ビデオアセットのワークフローが必要かどうか
* ビデオアセットのバージョン管理が必要かどうか

これらの質問のいずれかまたは両方に対する回答が「はい」の場合は、ビデオをAdobeDAM に直接アップロードします。 両方の質問に対する回答が「いいえ」の場合は、ビデオをDynamic Media Classicに直接アップロードします。 各シナリオのワークフローについては、次の節で説明します。

### ビデオを直接 Adobe DAM にアップロードする場合 {#if-you-are-uploading-your-video-directly-to-adobe-dam}

アセットのワークフローまたはバージョン管理が必要な場合は、まずAdobeDAM にアップロードします。 推奨されるワークフローは次のとおりです。

1. ビデオアセットをAdobeDAM にアップロードし、自動的にエンコードしてDynamic Media Classicに公開します。
1. Experience Managerで、WCM のビデオアセット ( **[!UICONTROL 映画]** 」タブをクリックします。
1. 作成者： **[!UICONTROL Scene7 Video]** または **[!UICONTROL Foundation ビデオ]** コンポーネント。

### ビデオを Scene7 にアップロードする場合 {#if-you-are-uploading-your-video-to-scene}

アセットのワークフローやバージョン管理が必要ない場合は、アセットをScene7にアップロードします。 推奨されるワークフローは次のとおりです。

1. Dynamic Media Classicでは、 [Scene7への FTP アップロードおよびエンコーディングのスケジュール設定（システムが自動化）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#preparing-your-assets-and-folders-for-uploading).
1. Experience Managerで、WCM のビデオアセット ( **[!UICONTROL Scene7]** 」タブをクリックします。
1. 作成者： **[!UICONTROL Scene7 Video]** コンポーネント。

## Scene7 ビデオとの統合の設定 {#configuring-integration-with-scene-video}

ユニバーサルプリセットを設定するには：

1. **[!UICONTROL クラウドサービス]**&#x200B;で、**[!UICONTROL Scene7]** の設定に移動して、「**[!UICONTROL 編集]**」をクリックします。
1. 「**[!UICONTROL ビデオ]**」タブを選択します。

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >クラウド設定がページにない場合は、「**[!UICONTROL ビデオ]**」タブが表示されません。

1. アダプティブビデオエンコーディングプロファイル、組み込みの単一のビデオエンコーディングプロファイルまたはカスタムビデオエンコーディングプロファイルを選択します。

   >[!NOTE]
   >
   >ビデオプリセットの意味について詳しくは、 [Dynamic Media Classicドキュメント](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >ユニバーサルプリセットを設定する際に両方のアダプティブビデオセットを選択するか、「**[!UICONTROL アダプティブビデオエンコーディング]**」オプションを選択することをお勧めします。

1. 選択したエンコーディングプロファイルは、この Scene7 クラウド設定用に指定した CQ DAM のターゲットフォルダーにアップロードされたすべてのビデオに自動的に適用されます。必要に応じて、別のターゲットフォルダーに別のエンコーディングプロファイルを適用することで、複数の Scene7 クラウド設定を指定できます。

## ビューアとエンコーディングプリセットの更新 {#updating-viewer-and-encoding-presets}

Scene7で更新された場合は、Experience Managerでビデオのビューアとエンコーディングプリセットを更新する必要があります。 その場合は、クラウド設定のScene7設定に移動し、 **[!UICONTROL ビューアとエンコーディングプリセットを更新します]**.

![chlimage_1-364](assets/chlimage_1-364.png)

## AdobeDAM からScene7にマスタービデオをアップロード中 {#uploading-your-master-video}

1. Scene7 のエンコーディングプロファイルと共にクラウド設定を指定した CQ DAM のターゲットフォルダーに移動します。
1. 「**[!UICONTROL アップロード]**」をクリックして、マスタービデオをアップロードします。DAM アセットの更新ワークフローが完了し、 **[!UICONTROL Scene7に公開]** にはチェックマークが付いています。

   >[!NOTE]
   >
   >ビデオサムネールの生成には時間がかかります。

   DAM マスタービデオをビデオコンポーネントにドラッグすると、にアクセスします *すべて* Scene7がエンコードした配信用のプロキシレンディション。

## 基盤ビデオコンポーネントと Scene7 ビデオコンポーネントの比較 {#foundation-video-component-versus-scene-video-component}

Experience Managerを使用する場合、Sites で使用できるビデオコンポーネントと、Scene7ビデオコンポーネントの両方にアクセスできます。 これらのコンポーネントに互換性はありません。

Scene7 ビデオコンポーネントは、Scene7 ビデオでのみ使用できます。基盤コンポーネントは、Experience Manager（ffmpeg を使用）およびScene7ビデオから保存されたビデオで使用できます。

次の表に、どのコンポーネントをいつ使用するかを示します。

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>標準で、S7 ビデオコンポーネントはユニバーサルビデオプロファイルを使用します。 ただし、Experience ManagerでHTML5 ベースのビデオプレーヤーを入手することはできます。 標準搭載のHTML5 ビデオプレーヤーの埋め込みコードをコピーし、Experience Managerページに配置します。

## Experience Managerビデオコンポーネント {#aem-video-component}

Scene7ビデオの閲覧にScene7ビデオコンポーネントの使用をお勧めしますが、完全性を保つために、Scene7ビデオコンポーネントと基盤ビデオコンポーネントを使用してください。

### Experience ManagerビデオとScene7ビデオの比較 {#aem-video-and-scene-video-comparison}

次の表に、Experience Managerの基盤ビデオコンポーネントとScene7ビデオコンポーネントの間でサポートされる機能の概要を示します。

|  | Experience ManagerFoundation ビデオ | Scene7 ビデオ |
|---|---|---|
| アプローチ | HTML5 における最優先のアプローチです。Flash は HTML5 以外のフォールバックでのみ使用されます。 | ほとんどのデスクトップでは Flash です。HTML5 はモバイルとタブレットで使用されます。 |
| 配信 | プログレッシブ | アダプティブストリーミング |
| 追跡 | はい | はい |
| 拡張性 | 対応 | はい ( [HTML5 Viewer SDK API ドキュメント](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)) |
| モバイルビデオ | はい | はい |

### 設定 {#setting-up}

#### ビデオプロファイルの作成 {#creating-video-profiles}

様々なビデオエンコーディングは、Scene7クラウド設定で選択したScene7エンコーディングプリセットに従って作成されます。 基盤ビデオコンポーネントで使用するには、選択したScene7のエンコーディングプリセットごとにビデオプロファイルを作成する必要があります。 この方法を使用すると、ビデオコンポーネントは、それに応じて DAM レンディションを選択できます。

>[!NOTE]
>
>新しいビデオプロファイルおよびビデオプロファイルに対する変更をアクティベートして公開する必要があります。

1. Experience Managerで、 **[!UICONTROL ツール] > [!UICONTROL 設定コンソール]**.
1. 次の **[!UICONTROL 設定コンソール]** に移動します。 **[!UICONTROL ツール/DAM/ビデオプロファイル]** をクリックします。
1. Scene7ビデオプロファイルを作成します。 内 **[!UICONTROL 新規…]** ドロップダウンリストで、「 **[!UICONTROL ページを作成]** 次に、「 Scene7ビデオプロファイル」テンプレートを選択します。 新しいビデオプロファイルページに名前を付け、「 **[!UICONTROL 作成]**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 新しいビデオプロファイルを編集します。最初にクラウド設定を選択します。次に、クラウド設定で選択したものと同じエンコーディングプリセットを選択します。

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | プロパティ | 説明 |
   |---|---|
   | Scene7 クラウド設定 | エンコーディングプリセットで使用するクラウド設定です。 |
   | Scene7 エンコーディングプリセット | このビデオプロファイルをマップするために使用するエンコーディングプリセットです。 |
   | HTML5 ビデオタイプ | このプロパティを使用すると、HTML5 ビデオソース要素の type プロパティの値を設定できます。 この情報は、S7 エンコーディングプリセットでは提供されませんが、HTML5 ビデオ要素を使用してビデオを適切にレンダリングするために必要です。共通の形式用のリストが提供されますが、他の形式用に上書きできます。 |

   ビデオコンポーネントで使用する、クラウド設定で選択したすべてのエンコーディングプリセットについて、この手順を繰り返します。

#### デザインの設定 {#configuring-design}

この **[!UICONTROL Foundation ビデオ]** コンポーネントは、ビデオソースリストの作成に使用するビデオプロファイルについて把握しておく必要があります。 ビデオコンポーネントデザインダイアログボックスを開き、新しいビデオプロファイルを使用するためのコンポーネントデザインを設定します。

>[!NOTE]
>
>次の **[!UICONTROL Foundation ビデオ]** モバイルページのコンポーネントで、モバイルページのデザインでこれらの手順を繰り返します。

>[!NOTE]
>
>デザインを変更するには、デザインをアクティベートして、パブリッシュ時にデザインを有効にする必要があります。

1. を開きます。 **[!UICONTROL Foundation ビデオ]** コンポーネントのデザインダイアログボックスを開き、次の設定に変更します。 **[!UICONTROL プロファイル]** タブをクリックします。 次に、標準のプロファイルを削除し、新しい S7 ビデオプロファイルを追加します。 デザインダイアログボックスのプロファイルリストの順序によって、レンダリング時のビデオソース要素の順序が決まります。
1. HTML5 をサポートしていないブラウザーの場合、ビデオコンポーネントを使用すると、Flashフォールバックを設定できます。 ビデオコンポーネントデザインダイアログボックスを開き、 **[!UICONTROL Flash]** タブをクリックします。 Flash Player設定を指定し、フォールバックプロファイルをFlash Playerに割り当てます。

#### チェックリスト {#checklist}

1. S7 クラウド設定を作成します。 ビデオエンコーディングプリセットが設定され、インポーターが実行中であることを確認します。
1. クラウド設定で選択した各ビデオエンコーディングプリセット用の S7 ビデオプロファイルを作成します。
1. ビデオプロファイルをアクティベートする必要があります。
1. デザインの設定 **[!UICONTROL Foundation ビデオ]** コンポーネントをページ上に配置します。
1. デザインの変更が完了したら、デザインをアクティベートします。
