---
title: ビデオ
description: アセットでは、ビデオアセットを統合管理できます。ビデオを直接アセットにアップロードして、Scene7 に対する自動エンコーディングをおこなったり、アセットから直接 Scene7 ビデオにアクセスしてページオーサリングをおこなったりできます。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: authoring
content-type: reference
exl-id: 7cb3d58c-0d78-4414-9b66-0a10e52d0906
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1683'
ht-degree: 40%

---

# ビデオ{#video}

Assets では、ビデオアセット管理を一元化し、Assets に直接ビデオをアップロードしてDynamic Media Classicに自動エンコーディングし、Assets から直接Dynamic Media Classicビデオにアクセスしてページをオーサリングできます。

Dynamic Media Classicビデオの統合により、最適化されたビデオがすべての画面に広がります（自動デバイスと帯域幅の検出）。

* Dynamic Media Classic(Scene7) ビデオコンポーネントは、デスクトップ、タブレット、モバイルで適切な形式と品質のビデオを再生するために、デバイスと帯域幅の検出を自動的に実行します。
* Assets — 単一のビデオアセットだけでなく、アダプティブビデオセットを含めることができます。アダプティブビデオセットは、複数の画面でビデオをシームレスに再生するのに必要なすべてのビデオレンディションのコンテナです。アダプティブビデオセットは、同じビデオの、異なるビットレート（400 kbps、800 kbps、1000 kbps など）でエンコードされたバージョンをグループ化します。デスクトップ、iOS、Android、Blackberry および Windows モバイルデバイスを含む複数の画面にアダプティブビデオをストリーミングする場合、S7 ビデオコンポーネントと共にアダプティブビデオセットを使用します。詳しくは、 [Scene7のアダプティブビデオセットに関するドキュメントを参照してください](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).

## FFMPEG とDynamic Media Classicについて {#about-ffmpeg-and-scene}

デフォルトのビデオエンコーディングプロセスは、ビデオプロファイルとの FFMPEG ベースの統合の使用に基づいています。そのため、組み込みの DAM アセットの更新ワークフローには、ffmpeg ベースの次の 2 つのワークフローのステップが含まれています。

* FFMPEG のサムネイル
* FFMPEG エンコーディング

Dynamic Media Classic統合を有効にして設定しても、標準の DAM アセットの更新取り込みワークフローからこれら 2 つのワークフローステップが自動的に削除または非アクティブ化されることはありません。 FFMPEG ベースのビデオエンコーディングを既に AEM で使用している場合は、オーサリング環境に FFMPEG がインストールされている可能性があります。この場合、Assets を使用して取り込まれた新しいビデオは 2 回エンコードされます。FFMPEG エンコーダーから、Dynamic Media Classic統合から 1 回。

AEM で FFMPEG ベースのビデオエンコーディングが設定済みで、FFMPEG がインストールされている場合は、2 つの FFMPEG ワークフローを DAM アセットの更新ワークフローから削除することをお勧めします。

### サポートされるファイル形式 {#supported-formats}

Dynamic Media Classicビデオコンポーネントでは、次の形式がサポートされています。

* F4V H.264
* MP4 H.264

### ビデオのアップロード先の指定 {#deciding-where-to-upload-your-video}

ビデオアセットのアップロード先の指定は、次の条件によって決まります。

* ビデオアセットのワークフローが必要かどうか
* ビデオアセットのバージョン管理が必要かどうか

これらの質問のいずれかまたは両方に対する回答が「はい」の場合は、ビデオをAdobeDAM に直接アップロードします。 両方の質問に対する回答が「いいえ」の場合は、ビデオをDynamic Media Classicに直接アップロードします。 次の節では、各シナリオのワークフローについて説明します。

#### ビデオを直接 Adobe Assets にアップロードする場合 {#if-you-are-uploading-your-video-directly-to-adobe-assets}

アセットのワークフローまたはバージョン管理が必要な場合は、まず Adobe Assets にアップロードする必要があります。推奨されるワークフローは次のとおりです。

1. ビデオアセットをAdobeAssets にアップロードし、自動的にエンコードしてDynamic Media Classicに公開します。
1. AEM の WCM（コンテンツファインダーの「**[!UICONTROL ムービー]**」タブ）で、ビデオアセットにアクセスします。
1. Dynamic Media Classicビデオまたは基盤ビデオコンポーネントを使用したオーサー。

#### ビデオをDynamic Media Classicにアップロードする場合 {#if-you-are-uploading-your-video-to-scene}

アセットのワークフローやバージョン管理が必要ない場合は、アセットをDynamic Media Classicにアップロードする必要があります。 推奨されるワークフローは次のとおりです。

1. Dynamic Media Classicでは、 [Dynamic Media Classicへの FTP アップロードおよびエンコーディングのスケジュール設定（システムが自動化）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#uploading-your-files).
1. AEMで、WCM のビデオアセット ( **[!UICONTROL Dynamic Media Classic]** 」タブをクリックします。
1. Dynamic Media Classicビデオコンポーネントを使用したオーサリング。

### Dynamic Media Classicとの統合の設定ビデオ {#configuring-integration-with-scene-video}

**ユニバーサルプリセットを設定するには：**:

1. In **[!UICONTROL Cloud Services]**&#x200B;を選択し、 **[!UICONTROL Dynamic Media Classic]** 設定およびクリック **[!UICONTROL 編集]**.
1. 「**[!UICONTROL ビデオ]**」タブを選択します。

   >[!NOTE]
   >
   >クラウド設定がページにない場合は、「**[!UICONTROL ビデオ]**」タブが表示されません。詳しくは、 [WCM でのDynamic Media Classicの有効化](#enablingscene7forwcm).

1. アダプティブビデオエンコーディングプロファイル、組み込みの単一のビデオエンコーディングプロファイルまたはカスタムビデオエンコーディングプロファイルを選択します。

   >[!NOTE]
   >
   >ビデオプリセットの意味について詳しくは、 [Dynamic Media Classicドキュメント](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >ユニバーサルプリセットを設定する際に両方のアダプティブビデオセットを選択するか、「**[!UICONTROL アダプティブビデオエンコーディング]**」オプションを選択することをお勧めします。

1. 選択したエンコーディングプロファイルは、このDynamic Media Classicクラウド設定用に設定した CQ DAM ターゲットフォルダーにアップロードされたすべてのビデオに自動的に適用されます。 必要に応じて、様々なターゲットフォルダーを持つ複数のDynamic Media Classicクラウド設定を設定し、様々なエンコーディングプロファイルを適用できます。

### ビューアとエンコーディングプリセットの更新 {#updating-viewer-and-encoding-presets}

AEMでプリセットが更新されたので、ビデオのビューアとエンコーディングプリセットを更新する必要がある場合は、クラウド設定のDynamic Media Classic設定に移動して、「 **ビューアとエンコーディングプリセットを更新します**.

![chlimage_1-131](assets/chlimage_1-131.png)

### マスタービデオのアップロード {#uploading-your-master-video}

AdobeDAM からDynamic Media Classicにマスタービデオをアップロードするには：

1. Dynamic Media Classicのエンコーディングプロファイルを使用してクラウド設定を行った CQ DAM ターゲットフォルダーに移動します。
1. 「**[!UICONTROL アップロード]**」をクリックして、マスタービデオをアップロードします。ビデオのアップロードとエンコーディングは、 [!UICONTROL DAM アセットの更新] ワークフローが完了し、 **[!UICONTROL Dynamic Media Classicに公開]** にはチェックマークが付いています。

   >[!NOTE]
   >
   >ビデオのサムネイルの生成にはある程度の時間がかかることがあります。

   DAM マスタービデオをビデオコンポーネントにドラッグすると、ビデオコンポーネントにアクセスできます *すべて* Dynamic Media Classicがエンコードした配信用のプロキシレンディションの数を格納します。

### 基盤ビデオコンポーネントとDynamic Media Classicビデオコンポーネントの比較 {#foundation-video-component-versus-scene-video-component}

AEMを使用する場合、Sites で使用できるビデオコンポーネントと、Dynamic Media Classic(Scene7) ビデオコンポーネントの両方にアクセスできます。 これらのコンポーネントに互換性はありません。

Dynamic Media Classicビデオコンポーネントは、Dynamic Media Classicビデオでのみ機能します。 基盤コンポーネントは、AEM （ffmpeg を使用）およびDynamic Media Classicビデオから保存されたビデオに対して機能します。

次の表は、どのコンポーネントをどのようなシナリオで使用すべきかを示しています。

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>標準では、Dynamic Media Classicビデオコンポーネントはユニバーサルビデオプロファイルを使用します。 ただし、AEMで使用するHTML5 ベースのビデオプレーヤーを入手することはできます。 Dynamic Media Classicで、標準のHTML5 ビデオプレーヤーの埋め込みコードをコピーし、AEMページに配置します。

## AEM ビデオコンポーネント {#aem-video-component}

Dynamic Media Classicビデオの閲覧にDynamic Media Classicビデオコンポーネントの使用をお勧めしますが、ここでは、 [!UICONTROL 基盤ビデオコンポーネント] AEMでは、完全性を保つために使用されます。

### AEMビデオとDynamic Media Classicビデオの比較 {#aem-video-and-scene-video-comparison}

次の表は、AEM 基盤ビデオコンポーネントと Scene7 ビデオコンポーネントでサポートされている機能の簡単な比較です。

|  | AEM 基盤ビデオ | Dynamic Media Classic Video |
|---|---|---|
| アプローチ | HTML5 における最優先のアプローチです。Flash は HTML5 以外のフォールバックでのみ使用されます。 | ほとんどのデスクトップでは Flash です。HTML5 はモバイルとタブレットで使用されます。 |
| 配信 | プログレッシブ | アダプティブストリーミング |
| 追跡 | はい | はい |
| 拡張性 | 対応 | はい (Dynamic Media Classic Viewer SDK を使用 ) |
| モバイルビデオ | はい | はい |

### 設定 {#setting-up}

#### ビデオプロファイルの作成 {#creating-video-profiles}

様々なビデオエンコーディングは、Dynamic Media Classicクラウド設定で選択したDynamic Media Classicのエンコーディングプリセットに従って作成されます。 基盤ビデオコンポーネントでビデオコンポーネントを使用するには、選択したDynamic Media Classicのエンコーディングプリセットごとにビデオプロファイルを作成する必要があります。 これにより、対応する DAM レンディションをビデオコンポーネントで選択できます。

>[!NOTE]
>
>新しいビデオプロファイルおよびビデオプロファイルに対する変更をアクティベートして公開する必要があります。

1. AEM で、**[!UICONTROL ツール]**&#x200B;に移動し、「**[!UICONTROL 設定コンソール]**」を選択します。設定コンソールで、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Assets]** > **[!UICONTROL ビデオプロファイル]** をクリックします。
1. 新しいDynamic Media Classicビデオプロファイルを作成します。 内 **[!UICONTROL 新規…]** メニュー、選択 **[!UICONTROL ページを作成]** 次に、「 Dynamic Media Classicビデオプロファイル」テンプレートを選択します。 新しいビデオプロファイルページに名前を付け、「 **[!UICONTROL 作成]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. 新しいビデオプロファイルを編集します。最初にクラウド設定を選択します。次に、クラウド設定で選択したものと同じエンコーディングプリセットを選択します。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | プロパティ | 説明 |
   |---|---|
   | Dynamic Media Classic(Scene7) クラウド設定 | エンコーディングプリセットで使用するクラウド設定です。 |
   | Dynamic Media Classic(Scene7) エンコーディングプリセット | このビデオプロファイルをマップするために使用するエンコーディングプリセットです。 |
   | HTML5 ビデオタイプ | このプロパティを使用すると、HTML5 ビデオのソース要素の type プロパティの値を設定できます。この情報は、Dynamic Media Classicのエンコーディングプリセットでは提供されませんが、HTML5 ビデオ要素を使用してビデオを適切にレンダリングするために必要です。 共通の形式用のリストが提供されますが、他の形式用に上書きできます。 |

   ビデオコンポーネントで使用する、クラウド設定で選択したすべてのエンコーディングプリセットについて、この手順を繰り返します。

#### デザインの設定 {#configuring-design}

ビデオソースリストを作成するには、基盤ビデオコンポーネントが、使用するビデオプロファイルについて認識しておく必要があります。ビデオコンポーネントのデザインダイアログを開いて、新しいビデオプロファイルを使用するためのコンポーネントのデザインを設定してください。

>[!NOTE]
>
>基盤ビデオコンポーネントをモバイルページで使用する場合は、ここに示す手順をモバイルページのデザインで繰り返す必要がある可能性があります。

>[!NOTE]
>
>デザインを変更するには、デザインのアクティベーションをおこなって、公開時に変更を有効にする必要があります。

1. 基盤ビデオコンポーネントのデザインダイアログを開き、「**[!UICONTROL プロファイル]**」タブに変更します。その後、標準のプロファイルを削除し、新しいDynamic Media Classicビデオプロファイルを追加します。 デザインダイアログでのプロファイルリストの順序は、レンダリング時のビデオソース要素の順序も定義します。
1. HTML5 をサポートしていないブラウザーの場合は、ビデオコンポーネントで Flash フォールバックを設定できます。ビデオコンポーネントのデザインダイアログを開き、「**[!UICONTROL Flash]**」タブに変更します。Flash Player 設定を指定して、Flash Player のフォールバックプロファイルを割り当てます。

#### チェックリスト {#checklist}

1. Dynamic Media Classic(Scene7) クラウド設定を作成します。 ビデオエンコーディングプリセットが設定され、インポーターが実行中であることを確認します。
1. クラウド設定で選択した各ビデオエンコーディングプリセットに対して、Dynamic Media Classicビデオプロファイルを作成します。
1. ビデオプロファイルをアクティベートする必要があります。
1. 目的のページで基盤ビデオコンポーネントの設計を設定します。
1. デザインの変更が完了したら、デザインをアクティベートします。
