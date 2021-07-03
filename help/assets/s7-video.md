---
title: ビデオ
description: Dynamic Media Classicに自動エンコーディング用のビデオをアップロードしてExperience Managerアセット用にビデオをアップロードできる、一元化されたビデオアセット管理について説明します。 Dynamic Media Classicビデオには、Experience ManagerAssetsから直接アクセスすることもできます。 Dynamic Media Classicビデオの統合により、自動デバイスと自動帯域幅検出を使用して、最適化されたビデオの範囲をすべての画面に広げることができます。
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: managing-assets
content-type: reference
exl-id: 081e7db0-95cc-4260-8f08-318cd7d9d5b4
feature: ビデオ
role: User
source-git-commit: 5d96c09ef764b02e08dcdf480da1ee18f4d9a30c
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 30%

---

# ビデオ {#video}

Assetsでは、ビデオをAssetsに直接アップロードして、Dynamic Media Classicに自動エンコーディングできる、一元化されたビデオアセット管理を実現します。 Assetsから直接Dynamic Media Classicビデオにアクセスして、ページをオーサリングすることもできます。

Dynamic Media Classicビデオの統合により、最適化されたビデオの範囲がすべての画面に広がります（自動デバイスと帯域幅の検出）。

**[!UICONTROL Scene7ビデオ]**&#x200B;コンポーネントは、デスクトップ、タブレット、モバイルで適切な形式と画質のビデオを再生するために、デバイスと帯域幅の検出を自動的に実行します。

単一のビデオアセットだけでなく、アダプティブビデオセットを含めることができます。 アダプティブビデオセットは、複数の画面をシームレスに再生するために必要なすべてのビデオレンディション用のコンテナです。 アダプティブビデオセットは、同じビデオの異なるビットレートおよび形式でエンコードされたバージョンをグループ化します。 （例：400 kbps、800 kbps、1000 kbps）。 複数の画面タイプにわたるアダプティブビデオのストリーミングには、S7ビデオコンポーネントと共にアダプティブビデオセットを使用します。 例えば、デスクトップ、iOS、Android、BlackBerry、Windowsのモバイルデバイスなどです。

詳しくは、[Dynamic Media Classicのアダプティブビデオセットに関するドキュメントを参照してください。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/video-profiles.html#dynamicmedia)

## FFMPEGとDynamic Media Classicについて {#about-ffmpeg-and-scene}

デフォルトのビデオエンコーディングプロセスは、ビデオプロファイルとの FFMPEG ベースの統合の使用に基づいています。そのため、組み込みの DAM 収集ワークフローには、ffmpeg ベースの次の 2 つのワークフローのステップが含まれています。

* FFMPEG のサムネール
* FFMPEG エンコーディング

Dynamic Media Classic統合を有効にして設定しても、標準のDAM取り込みワークフローからこれら2つのワークフロー手順が自動的に削除または非アクティブ化されることはありません。 Experience Managerで既にFFMPEGベースのビデオエンコーディングを使用している場合は、FFMPEGがオーサリング環境にインストールされている可能性があります。 この場合、DAMを使用して取り込まれた新しいビデオは2回エンコードされます。FFMPEGエンコーダーから、またはDynamic Media Classic統合から1回。

AEMとFFMPEGで設定されたFFMPEGベースのビデオエンコーディングがインストールされている場合は、DAM取り込みワークフローから2つのFFMPEGワークフローを削除できます。

## サポートされるファイル形式 {#supported-formats}

Scene7 ビデオコンポーネントでは次の形式がサポートされます。

* F4V H.264
* MP4 H.264

## ビデオのアップロード先の指定 {#deciding-where-to-upload-your-video}

ビデオアセットのアップロード先の指定は、次の条件によって決まります。

* ビデオアセットのワークフローが必要かどうか
* ビデオアセットのバージョン管理が必要かどうか

これらの質問のいずれかまたは両方に対する回答が「はい」の場合は、ビデオをAdobeDAMに直接アップロードします。 両方の質問に対する回答が「いいえ」の場合は、ビデオをDynamic Media Classicに直接アップロードします。 各シナリオのワークフローについては、次の節で説明します。

### ビデオを直接 Adobe DAM にアップロードする場合 {#if-you-are-uploading-your-video-directly-to-adobe-dam}

アセットのワークフローまたはバージョン管理が必要な場合は、まずAdobeDAMにアップロードします。 推奨されるワークフローは次のとおりです。

1. ビデオアセットをAdobeDAMにアップロードし、Dynamic Media Classicに自動的にエンコードして公開します。
1. Experience Managerで、WCMのビデオアセットにアクセスするには、コンテンツファインダーの「**[!UICONTROL Movies]**」タブを使用します。
1. **[!UICONTROL Scene7ビデオ]**&#x200B;または&#x200B;**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントを使用するオーサー。

### ビデオを Scene7 にアップロードする場合 {#if-you-are-uploading-your-video-to-scene}

アセットのワークフローやバージョン管理が必要ない場合は、Scene7にアセットをアップロードします。 推奨されるワークフローは次のとおりです。

1. Dynamic Media Classicでは、[Scene7（システム自動）に対するFTPアップロードおよびエンコーディングのスケジュールを設定します](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#preparing-your-assets-and-folders-for-uploading)。
1. Experience Managerで、WCMのコンテンツファインダーの「**[!UICONTROL Scene7]**」タブでビデオアセットにアクセスします。
1. **[!UICONTROL Scene7ビデオ]**&#x200B;コンポーネントを使用してオーサーします。

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
   >ビデオプリセットの意味について詳しくは、[Dynamic Media Classicのドキュメント](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files)を参照してください。
   >
   >ユニバーサルプリセットを設定する際に両方のアダプティブビデオセットを選択するか、「**[!UICONTROL アダプティブビデオエンコーディング]**」オプションを選択することをお勧めします。

1. 選択したエンコーディングプロファイルは、この Scene7 クラウド設定用に指定した CQ DAM のターゲットフォルダーにアップロードされたすべてのビデオに自動的に適用されます。必要に応じて、別のターゲットフォルダーに別のエンコーディングプロファイルを適用することで、複数の Scene7 クラウド設定を指定できます。

## ビューアとエンコーディングプリセットの更新 {#updating-viewer-and-encoding-presets}

Scene7でプリセットを更新した場合は、Experience Managerでビデオのビューアプリセットとエンコーディングプリセットを更新する必要があります。 その場合は、クラウド設定のScene7設定に移動し、「**[!UICONTROL ビューアとエンコーディングプリセットを更新]**」をクリックします。

![chlimage_1-364](assets/chlimage_1-364.png)

## AdobeDAMからScene7にマスタービデオをアップロード {#uploading-your-master-video}

1. Scene7 のエンコーディングプロファイルと共にクラウド設定を指定した CQ DAM のターゲットフォルダーに移動します。
1. 「**[!UICONTROL アップロード]**」をクリックして、マスタービデオをアップロードします。ビデオのアップロードとエンコーディングは、DAMアセットの更新ワークフローが完了し、**[!UICONTROL Scene7に公開]**&#x200B;にチェックマークが付いた後に完了します。

   >[!NOTE]
   >
   >ビデオサムネールの生成には、しばらく時間がかかります。

   DAMマスタービデオをビデオコンポーネントにドラッグすると、Scene7でエンコードされた配信用のプロキシレンディションがすべて&#x200B;**&#x200B;にアクセスします。

## 基盤ビデオコンポーネントと Scene7 ビデオコンポーネントの比較 {#foundation-video-component-versus-scene-video-component}

Experience Managerを使用する場合、Sitesで使用できるビデオコンポーネントとScene7ビデオコンポーネントの両方にアクセスできます。 これらのコンポーネントに互換性はありません。

Scene7 ビデオコンポーネントは、Scene7 ビデオでのみ使用できます。基盤コンポーネントは、Experience Manager（ffmpegを使用）とScene7ビデオから保存されたビデオで使用します。

次の表に、どのコンポーネントを使用するかを示します。

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>S7ビデオコンポーネントは、標準で、ユニバーサルビデオプロファイルを使用します。 ただし、HTML5ベースのビデオプレーヤーをExperience Managerで入手することはできます。 標準搭載のHTML5ビデオプレーヤーの埋め込みコードをコピーし、Experience Managerページに配置します。

## Experience Managerビデオコンポーネント {#aem-video-component}

Scene7のビデオの視聴にScene7ビデオコンポーネントの使用をお勧めします。完全性を考慮して、基盤ビデオコンポーネントでScene7ビデオを使用してください。

### Experience ManagerビデオとScene7ビデオの比較 {#aem-video-and-scene-video-comparison}

次の表に、Experience Manager基盤ビデオコンポーネントとScene7ビデオコンポーネントの間でサポートされている機能の大まかな比較を示します。

|  | Experience Manager基盤ビデオ | Scene7 ビデオ |
|---|---|---|
| アプローチ | HTML5 における最優先のアプローチです。Flash は HTML5 以外のフォールバックでのみ使用されます。 | ほとんどのデスクトップでは Flash です。HTML5 はモバイルとタブレットで使用されます。 |
| 配信 | プログレッシブ | アダプティブストリーミング |
| 追跡 | はい | はい |
| 拡張性 | ○ | はい（[HTML5ビューアSDK APIドキュメント](https://s7d1.scene7.com/s7sdk/3.10/docs/jsdoc/index.html)を使用） |
| モバイルビデオ | はい | はい |

### 設定 {#setting-up}

#### ビデオプロファイルの作成 {#creating-video-profiles}

様々なビデオエンコーディングは、Scene7クラウド設定で選択したScene7エンコーディングプリセットに従って作成されます。 基盤ビデオコンポーネントで使用するには、選択したScene7エンコーディングプリセットごとにビデオプロファイルを作成する必要があります。 この方法を使用すると、ビデオコンポーネントがそれに応じてDAMレンディションを選択できます。

>[!NOTE]
>
>新しいビデオプロファイルおよびビデオプロファイルに対する変更をアクティベートして公開する必要があります。

1. Experience Managerで、**[!UICONTROL ツール] /[!UICONTROL 設定コンソール]**&#x200B;をタップします。
1. **[!UICONTROL 設定コンソール]**&#x200B;から、ナビゲーションツリーの&#x200B;**[!UICONTROL ツール/DAM/ビデオプロファイル]**&#x200B;に移動します。
1. Scene7ビデオプロファイルを作成します。 **[!UICONTROL 新規…]**&#x200B;ドロップダウンリストから「**[!UICONTROL ページを作成]**」を選択し、「Scene7ビデオプロファイル」テンプレートを選択します。 新しいビデオプロファイルページに名前を付け、「**[!UICONTROL 作成]**」をクリックします。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 新しいビデオプロファイルを編集します。最初にクラウド設定を選択します。次に、クラウド設定で選択したものと同じエンコーディングプリセットを選択します。

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | プロパティ | 説明 |
   |---|---|
   | Scene7 クラウド設定 | エンコーディングプリセットで使用するクラウド設定です。 |
   | Scene7 エンコーディングプリセット | このビデオプロファイルをマップするために使用するエンコーディングプリセットです。 |
   | HTML5 ビデオタイプ | このプロパティを使用すると、HTML5ビデオソース要素のtypeプロパティの値を設定できます。 この情報は、S7 エンコーディングプリセットでは提供されませんが、HTML5 ビデオ要素を使用してビデオを適切にレンダリングするために必要です。共通の形式用のリストが提供されますが、他の形式用に上書きできます。 |

   ビデオコンポーネントで使用する、クラウド設定で選択したすべてのエンコーディングプリセットについて、この手順を繰り返します。

#### デザインの設定 {#configuring-design}

**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントは、ビデオソースリストの作成に使用するビデオプロファイルについて把握している必要があります。 ビデオコンポーネントデザインダイアログボックスを開き、新しいビデオプロファイルを使用するためのコンポーネントデザインを設定します。

>[!NOTE]
>
>モバイルページで&#x200B;**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントを使用する場合は、モバイルページのデザインでこれらの手順を繰り返します。

>[!NOTE]
>
>デザインに加えた変更は、デザインをアクティベートして、パブリッシュ時に有効にする必要があります。

1. **[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントのデザインダイアログボックスを開き、「**[!UICONTROL プロファイル]**」タブに変更します。 次に、標準のプロファイルを削除し、新しいS7ビデオプロファイルを追加します。 デザインダイアログボックスでのプロファイルリストの順序によって、レンダリング時のビデオソース要素の順序が決まります。
1. HTML5をサポートしていないブラウザーの場合、ビデオコンポーネントを使用すると、Flashフォールバックを設定できます。 ビデオコンポーネントデザインダイアログボックスを開き、「**[!UICONTROL Flash]**」タブに変更します。 Flash Playerの設定を行い、Flash Playerにフォールバックプロファイルを割り当てます。

#### チェックリスト {#checklist}

1. S7クラウド設定を作成します。 ビデオエンコーディングプリセットが設定され、インポーターが実行中であることを確認します。
1. クラウド設定で選択した各ビデオエンコーディングプリセット用の S7 ビデオプロファイルを作成します。
1. ビデオプロファイルをアクティベートする必要があります。
1. ページ上の&#x200B;**[!UICONTROL 基盤ビデオ]**&#x200B;コンポーネントのデザインを設定します。
1. デザインの変更が完了したら、デザインをアクティベートします。
