---
title: ビデオ
seo-title: ビデオ
description: Dynamic Media でビデオを使用する方法について説明します。
seo-description: Dynamic Media でビデオを使用する方法について説明します。
uuid: 15e89f88-2787-472d-bbb6-d370bbab9228
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: Dynamic-Media
content-type: reference
discoiquuid: b721dc7c-b056-47f5-9489-9f4db45b68a0
translation-type: tm+mt
source-git-commit: 978c6e5cffb557f0d42f961bdde597fabf278ddd

---


# ビデオ {#video}

ここでは、Dynamic Media でのビデオの操作方法について説明します。

## クイックスタート：ビデオ {#quick-start-videos}

次の順を追ったワークフローに従って、ダイナミックメディアのアダプティブビデオセットをすばやく習得できます。各手順の後に、詳細を参照できるトピックの見出しへの相互参照を示します。

>[!NOTE]
>
>ダイナミックメディアのビデオを操作する前に、AEM 管理者が既にダイナミックメディアクラウドサービスを有効にして設定を完了していることを確認してください。
>
>* [Dynamic Media - ハイブリッドモードの設定の Dynamic Media クラウドサービスの設定を参照してください。](/help/assets/config-dynamic.md)
>* [ダイナミックメディア - Scene7 モードの設定](config-dms7.md)および[ダイナミックメディア - Scene7 モードのトラブルシューティング](troubleshoot-dms7.md)を参照してください。
>



1. 次の手順を実行して、**Dynamic Media ビデオをアップロードします**。

   * 独自のビデオエンコーディングプロファイルを作成します。または、ダイナミックメディアに付属の定義済みの「アダプティブビデオエンコーディング」プロファイルを使用するだけでもかまいません。

      * [ビデオエンコーディングプロファイルの作成](video-profiles.md)
      * Learn more about [Best practices for video encoding](#best-practices-for-encoding-videos).
   * マスタービデオをアップロードする1つ以上のフォルダーにビデオ処理プロファイルを関連付けます。

      * [ビデオプロファイルのフォルダーへの適用](video-profiles.md#applying-a-video-profile-to-folders)
      * [処理プロファイルを使用するためのデジタルアセットの整理におけるベストプラクティス](organize-assets.md#organize-using-folders)に関する詳細
      * [デジタルアセットの整理](organize-assets.md)に関する詳細
   * フォルダーにマスタービデオをアップロードします。20 GB までのビデオファイルをアップロードできます。フォルダーにビデオを追加すると、フォルダーに割り当てたビデオ処理プロファイルに従ってエンコードされます。

      * [ビデオのアップロード](managing-video-assets.md#uploading-and-previewing-video-assets)
      * [サポートされる入力ファイル形式](assets-formats.md#supported-multimedia-formats)に関する詳細 
   * アセットまたはワークフロー表示から[ビデオ処理の進行状況](#monitoring-video-encoding-and-youtube-publishing-progress)を監視します。




1. 次のいずれかの操作をおこなって、**Dynamic Media ビデオを管理します。**

   * ビデオアセットを整理、参照および検索します。

      * [デジタルアセットの整理](organize-assets.md)

         Learn more about [Best practices for organizing your digital assets for using processing profiles](organize-assets.md#organize-using-folders)

      * [ビデオアセットの検索](search-video-assets.md) 、ア [セットの検索](managing-assets-touch-ui.md#searching-assets)
   * ビデオアセットをプレビューして公開します。

      * ソースビデオとビデオのエンコードされたレンディションを、関連するサムネールと共に表示します。

         [ビデオのプレビュー](managing-video-assets.md#uploading-and-previewing-video-assets) /アセット [のプレビュー](previewing-assets.md)

         [ビデオレンディションの表示](video-renditions.md)

         [ビデオレンディションの管理](managing-assets-touch-ui.md#managing-renditions)

      * [ビューアプリセットの管理](managing-viewer-presets.md)
      * [アセットの公開](publishing-dynamicmedia-assets.md)
   * ビデオのメタデータを操作します。

      * フレームレート、オーディオおよびビデオのビットレート、コーデックなど、エンコードされたビデオレンディションのプロパティを表示します。

         [ビデオレンディショのプロパティの表示](video-renditions.md)

      * タイトル、説明、タグ、カスタムメタデータフィールドなど、ビデオのプロパティを編集します。

         [ビデオプロパティの編集](managing-assets-touch-ui.md#editing-properties)

      * [デジタルアセット用のメタデータの管理](metadata.md)
      * [メタデータスキーマ](metadata-schemas.md)
   * ビデオのレビュー、承認、注釈の付け方

      * [ビデオの注釈の作成](managing-video-assets.md#annotating-video-assets) 、アセ [ットの注釈の作成](managing-assets-touch-ui.md#annotating)
      * [アセットへのワークフローの適用](assets-workflow.md)[、またはアセットへのワークフローの開始](managing-assets-touch-ui.md#starting-a-workflow-on-an-asset)
      * [フォルダーのアセットのレビュー](bulk-approval.md)
      * [プロジェクト](/help/sites-authoring/projects.md)




1. 次のいずれかの操作をおこなって、**Dynamic Media ビデオを公開します。**

   * Webコンテンツ管理システムとしてAdobe Experience Managerを使用している場合は、Webページにビデオを直接追加できます。

      * [Web ページへのビデオの追加](adding-dynamic-media-assets-to-pages.md)
   * サードパーティのWebコンテンツ管理システムを使用している場合は、Webページにビデオをリンクまたは埋め込むことができます。

      * URLを使用したビデオの統合：

         [Web アプリケーションへの URL のリンク](linking-urls-to-yourwebapplication.md).
      * Webページの埋め込みコードを使用したビデオの統合：

         [Webページへのビデオビューアの埋め込み](embed-code.md)。
   * [YouTube にビデオを公開します](#publishing-videos-to-youtube)。
   * [ビデオレポートを生成します](#viewing-video-reports)。
   * [ビデオにキャプションを追加します](#adding-captions-to-video)。



## Dynamic Media でのビデオの操作 {#working-with-video-in-dynamic-media}

ダイナミックメディアのビデオは、デスクトップ、iOS、Android、Blackberry、Windows携帯端末など複数の画面にストリーミング用の高品質なアダプティブビデオを簡単に公開できるエンドツーエンドのソリューションです。アダプティブビデオセットは、同じビデオを異なるビットレート（400 kbps、800 kbps、1000 kbpsなど）やフォーマットでエンコードしたバージョンをグループ化します。デスクトップコンピューターまたはモバイルデバイスは、使用可能な帯域幅を検出します。

例えば、iOS モバイルデバイスでは、3G、4G、Wi-Fi などの帯域幅が検出されます。次に、アダプティブビデオセット内の様々なビデオのビットレートの中から、適切なエンコード済みビデオが自動的に選択されます。そのビデオが、デスクトップ、モバイルデバイスまたはタブレットにストリーミングされます。

さらに、デスクトップまたはモバイルデバイスでネットワーク状況が変化した場合に、ビデオ品質が自動的に、動的に切り替えられます。また、デスクトップが全画面表示モードに切り替わった場合、アダプティブビデオセットがより高い解像度を使用するように応答するので、ユーザーの閲覧エクスペリエンスが向上します。アダプティブビデオセットを使用すると、Dynamic Media ビデオを複数の画面とデバイスで再生するユーザーにとって最適な再生方法が提供されます。

再生または再生時に選択するエンコード済みビデオの決定に、ビデオプレーヤーが使用するロジックは、次のアルゴリズムに基づきます。

1. ビデオプレーヤーは、プレーヤー自体の「初期ビットレート」に設定されている値に最も近いビットレートで、初期ビデオフラグメントを読み込みます。
1. ビデオプレーヤーは、帯域幅の速度の変化に応じて、次の条件に従って切り替わります。

   1. プレーヤーは、見積もり帯域幅を超えない範囲内で、最も高い帯域幅でのストリームを選択します。
   1. プレーヤーは、使用可能な帯域幅の 80％ほどを見積もります。ただし、使用可能な帯域幅が上昇した場合は、帯域幅を大きく見積もりすぎてすぐに元の帯域幅に戻ることを防ぐために、より控えめな 70％ほどの見積もりとなります。

For detailed technical information about the algorithm, see [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

1 つのビデオおよびアダプティブビデオセットの管理では、次の方法がサポートされています。

* サポートされる各種ビデオ形式およびオーディオ形式のビデオをアップロードして、複数の画面での再生用にビデオを MP4 H.264 形式へとエンコードすること。事前定義済みのアダプティブビデオセット、1 つのビデオのエンコーディングプリセットを使用するか、独自のエンコーディングをカスタマイズしてビデオの品質とサイズを制御することができます。

   * アダプティブビデオセットが生成される場合、そのセットには MP4 ビデオが含まれます。
   * **注意**：マスター／ソースビデオはアダプティブビデオセットには追加されません。

* すべての HTML5 ビデオビューアでのビデオキャプション。
* 効率的なビデオアセット管理のための、メタデータが完全にサポートされたビデオの整理、参照および検索。
* Web やデスクトップおよびモバイルデバイス（iPhone、iPad、Android、Blackberry および Windows Phone を含む）へのアダプティブビデオセットの配信。

アダプティブビデオのストリーミングは、各種 iOS プラットフォームでサポートされています。See the [Adobe Viewers Reference Guide](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_about.html).

ダイナミックメディアでは、MP4 H.264 ビデオのモバイルビデオ再生がサポートされています。このビデオ形式をサポートする Blackberry デバイスについては、[Blackberry でサポートされているビデオ形式](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482)のページで確認できます。

このビデオ形式をサポートする Windows デバイスについては、[Windows Phone でサポートされているビデオ形式](https://msdn.microsoft.com/library/windows/apps/ff462087%28v=vs.105%29.aspx)で確認できます。

* Dynamic Media ビデオビューアプリセットを使用してビデオを再生します。このビューアプリセットには、次のビューアが含まれます。

   * 1 つのビデオのビューア
   * ビデオコンテンツと画像コンテンツの両方を組み合わせた混在メディアビューア

* 自社ブランドのニーズに合わせてビデオプレーヤーを設定します。
* 単純な URL か埋め込みコードを使用して、ビデオを Web サイト、モバイルサイトまたはモバイルアプリケーションに統合します。

詳しくは、[動的なビデオ再生](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480)を参照してください。

『Adobe Scene7 ビューアリファレンスガイド』の[HTML5 ビューアについて](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_viewers_about.html)も参照してください。

## ベストプラクティス：HTML5 ビデオビューアの使用 {#best-practice-using-the-html-video-viewer}

ダイナミックメディアHTML5ビデオビューアは堅牢なビデオプレーヤーです。HTML5ビデオ再生に関連する多くの一般的な問題や、アダプティブストリーミング配信の不足、デスクトップブラウザーの利用範囲の制限など、モバイルデバイスに関連する問題を回避するために使用できます。

プレーヤーのデザイン側から見れば、ビデオプレーヤーの全機能を、標準の Web 開発ツールでデザインできます。例えば、HTML5 と CSS を使用して、ボタン、コントロールおよびカスタムのポスター画像背景をデザインして、カスタマイズした表示によって顧客に対応することができます。

ビューアの再生側から見れば、ビューアによってブラウザーのビデオ機能が自動的に検出されます。その後、HLS ストリーミング（アダプティブビデオストリーミング）を使用してビデオが配信されます。または、これらの配信方法が使用できない場合は、HTML5 プログレッシブが代わりに使用されます。

HTML5 と CSS を使用して再生コンポーネントをデザインできる機能、埋め込み再生の機能、ブラウザーの機能に応じてアダプティブストリーミングまたはプログレッシブストリーミングを使用できる機能を 1 つのプレーヤーにまとめることで、リッチメディアコンテンツを配信する範囲をデスクトップユーザーとモバイルユーザーの両方に拡大して、ビデオエクスペリエンスを効率化することができます。

『Adobe ビューアリファレンスガイド』の[HTML5 ビューアについて](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/c_html5_viewers_about.html)も参照してください。

### HTML5 ビデオビューアを使用した、デスクトップコンピューターおよびモバイルデバイス上でのビデオ再生 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

デスクトップおよびモバイルへのアダプティブビデオストリーミングの場合、ビットレートの切り替えに使用されるビデオは、アダプティブビデオセット内のすべての MP4 ビデオに基づいています。

ビデオの再生は、HLS（HTTP ライブストリーミング）ビデオストリーミングか、プログレッシブビデオダウンロードを使用しておこなわれます。6.0、6.1、6.2 など以前の AEM バージョンでは、ビデオは HTTP 上でストリーミングされました。

一方、AEM 6.3 以降では、DM ゲートウェイサービスの URL が常に HTTPS も使用するので、ビデオは HTTPS（つまり、HLS ビデオストリーミング）でストリーミングされます。このデフォルトの動作はユーザーに影響しません。つまり、ブラウザーでサポートされていない場合を除き、ビデオストリーミングは常に HTTPS 上でおこなわれます（以下の表を参照してください）。したがって、次のようになります。

* HTTPS Web サイトが HTTPS ビデオストリーミングに対応している場合は、ストリーミングが適しています。
* HTTP Web サイトが HTTPS ビデオストリーミングに対応している場合は、ストリーミングが適しており、Web ブラウザーから混合コンテンツに関する問題は発生しません。

HLS（HTTP ライブストリーミング）は、アダプティブビデオストリーミングの Apple 標準で、ネットワーク帯域幅のキャパシティに応じて再生を自動的に調整します。また、HLS では、ビデオの残りのダウンロードを待たずに、ビデオ内の任意のポイントを「シーク」できます（「HTTP ライブストリーミング」も参照してください）。

プログレッシブビデオは、ユーザーのデスクトップ画面やモバイルデバイスにダウンロードしてローカルに保存することで配信されます。

次の表に、デバイス、ブラウザー、およびデスクトップコンピューターやモバイルデバイスでの Scene7 ビデオビューアによるビデオの再生方法を示します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>デバイス</strong></td> 
   <td><strong>ブラウザー</strong></td> 
   <td><strong>ビデオ再生モード</strong></td> 
  </tr> 
  <tr> 
   <td>デスクトップ</td> 
   <td>Internate Explorer 9および10</td> 
   <td>プログレッシブダウンロード。</td> 
  </tr> 
  <tr> 
   <td>デスクトップ</td> 
   <td>Internate Explorer 11+</td> 
   <td>Windows 8 および Windows 10 では、HLS が要求されるたびに HTTPS を強制的に使用します。既知の制約事項：このブラウザー／オペレーティングシステムの組み合わせでは、HLS での HTTP は機能しません。<br /><br />Windows 7 - プログレッシブダウンロード。HTTP プロトコルと HTTPS プロトコルの選択には標準的なロジックが使用されます。</td> 
  </tr> 
  <tr> 
   <td>デスクトップ</td> 
   <td>Firefox 23～44</td> 
   <td>プログレッシブダウンロード。</td> 
  </tr> 
  <tr> 
   <td>デスクトップ</td> 
   <td>Firefox 45 以降</td> 
   <td>HLS ビデオストリーミング。</td> 
  </tr> 
  <tr> 
   <td>デスクトップ</td> 
   <td>Chrome</td> 
   <td>HLS ビデオストリーミング。</td> 
  </tr> 
  <tr> 
   <td>デスクトップ</td> 
   <td>Safari（Mac）</td> 
   <td>HLS ビデオストリーミング。</td> 
  </tr> 
  <tr> 
   <td>Mobile</td> 
   <td>Chrome（Android 6 以前）</td> 
   <td>プログレッシブダウンロード。</td> 
  </tr> 
  <tr> 
   <td>Mobile</td> 
   <td>Chrome（Android 7 以降）</td> 
   <td>HLS ビデオストリーミング。</td> 
  </tr> 
  <tr> 
   <td>Mobile</td> 
   <td>Android（デフォルトブラウザー）</td> 
   <td>プログレッシブダウンロード。</td> 
  </tr> 
  <tr> 
   <td>Mobile</td> 
   <td>Safari（iOS）</td> 
   <td>HLS ビデオストリーミング。</td> 
  </tr> 
  <tr> 
   <td>Mobile</td> 
   <td>Chrome（iOS）</td> 
   <td>HLS ビデオストリーミング。</td> 
  </tr> 
  <tr> 
   <td>Mobile</td> 
   <td>Blackberry</td> 
   <td>HLS ビデオストリーミング。</td> 
  </tr> 
 </tbody> 
</table>

## Dynamic Media ビデオソリューションのアーキテクチャ {#architecture-of-dynamic-media-video-solution}

次の図に、アップロード後、DMGateway によってエンコードされ、公開されるビデオのオーサリングワークフローの全体像を示します。

![chlimage_1-427](assets/chlimage_1-427.png)

## ビデオのハイブリッド公開アーキテクチャ {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## ビデオエンコーディングのベストプラクティス {#best-practices-for-encoding-videos}

Dynamic Media を有効にし、ビデオクラウドサービスを設定済みの場合、**[!UICONTROL Dynamic Media エンコードビデオ]**&#x200B;ワークフローがビデオをエンコードします。このワークフローは、ワークフローの処理履歴とエラー情報を取り込みます。詳しくは、[ビデオエンコーディングと YouTube への公開の進行状況の監視](#monitoring-video-encoding-and-youtube-publishing-progress)を参照してください。If you have enabled Dynamic Media and set up Video Cloud services, the **[!UICONTROL Dynamic Media Encode Video]** workflow automatically takes effect when you upload a video. (If you are not using Dynamic Media, the **[!UICONTROL DAM Update Asset]** workflow takes effect.)

ここでは、ソースビデオファイルのエンコードにおけるベストプラクティスのヒントを説明します。

ビデオエンコーディングに関するアドバイスについては、以下を参照してください。

* 記事：『ストリーミングの初歩：基礎 - コーデック、帯域幅、データレート、解像度』：*www.adobe.com/go/learn_s7_streaming101_jp*[ ](https://www.adobe.com/go/learn_s7_streaming101_en)
* ビデオ：『ビデオエンコーディングの基礎』：*www.adobe.com/go/learn_s7_encoding_jp*[ ](https://www.adobe.com/go/learn_s7_encoding_en)

### ソースビデオファイル {#source-video-files}

ビデオファイルをエンコードするときは、可能な限り最高品質のソースビデオファイルを使用します。以前にエンコードされたビデオファイルの使用は避けてください。そのようなファイルは既に圧縮済みで、さらにエンコードすると標準を下回る品質のビデオが作成されるからです。

次の表に、ソースビデオファイルのエンコード前の推奨サイズ、縦横比および最小ビットレートを示します。

| サイズ | 縦横比 | 最小ビットレート |
|--- |--- |--- |
| 1,024 X 768 | 4:3 | 4,500 kbps（ほとんどのビデオ） |
| 1,280 X 720 | 16:9 | 3,000～6,000 kbps（ビデオ内のモーションの量に応じて調整） |
| 1,920 X 1,080 | 16:9 | 6,000～8,000 kbps（ビデオ内のモーションの量に応じて調整） |

### ファイルのメタデータの取得 {#obtaining-a-file-s-metadata}

ビデオ編集ツールを使用してメタデータを参照するか、メタデータ取得用のアプリケーションを使用して、ファイルのメタデータを取得することができます。以下は、サードパーティアプリケーションの MediaInfo を使用してビデオファイルのメタデータを取得する手順です。

1. このWebページに移動：https://mediaarea.net/en/MediaInfo [](https://mediaarea.net/en/MediaInfo).
1. 使用しているGUIバージョンのインストーラを選択してダウンロードし、インストール手順に従います。
1. After installation, either right-click the video file (Windows only) and select **[!UICONTROL MediaInfo]**, or open **[!UICONTROL MediaInfo]** and drag your video file into the application. You see all metadata associated with your video file, including its width, height, and fps.

### 縦横比 {#aspect-ratio}

マスタービデオファイルのビデオエンコーディングプリセットを選択または作成するときには、マスタービデオファイルと同じ縦横比をプリセットに使用してください。縦横比とは、ビデオの高さに対する幅の比率のことです。

ビデオファイルの縦横比を決定するには、ファイルのメタデータを取得し、ファイルの幅と高さをメモしておきます（上記のファイルのメタデータの取得を参照）。 次の式を使用して縦横比を決定します。

*幅/高さ = 縦横比*

次の表に、この式の解を一般的な縦横比に変換した結果を示します。

| 式の解 | 縦横比 |
|--- |--- |
| 1.33 | 4:3 |
| 0.75 | 3:4 |
| 1.78 | 16:9 |
| 0.56 | 9:16 |

例えば、幅 1,440、高さ 1,080 のビデオの縦横比は 1,440/1,080、つまり 1.33 になります。このビデオファイルをエンコードするには、縦横比 4:3 のビデオエンコーディングプリセットを選択します。

### ビットレート {#bitrate}

ビットレートとは、1 秒間のビデオ再生を作成するためにエンコードされるデータの量です。ビットレートは、1 秒あたりのキロビット数（Kbps）の単位で測定します。

すべてのコーデックで非可逆圧縮が使用されるので、ビットレートは、ビデオ品質における最も重要な要素となります。非可逆圧縮では、ビデオファイルの圧縮率が高いほど、ビデオの品質は低下します。したがって、他の特性（解像度、フレームレートおよびコーデック）がすべて等しい場合は、ビットレートが低いほど、圧縮ファイルの品質は低下します。

ビットレートエンコーディングは 2 種類あり、そのどちらかを選択できます。

* **Constant Bitrate Encoding** (CBR) - CBRエンコード中、ビットレートまたは1秒あたりのビット数は、エンコードプロセス全体で同じになります。 CBR エンコーディングでは、設定されているデータレートが、ビデオ全体での設定値として使用されます。また、CBR エンコーディングでは、メディアファイルの品質は最適化されませんが、その分、空き容量の節約になります。

   ビデオ全体に同じようなモーションレベルが含まれている場合は、CBR を使用します。CBR は、ビデオコンテンツのストリーミングに最も一般的に使用されています。[カスタムで追加するビデオエンコーディングパラメーターの使用](video-profiles.md#using-custom-added-video-encoding-parameters)も参照してください。

* **Variable Bitrate Encoding** (VBR) - VBRエンコードは、圧縮機が必要とするデータに基づいて、データレートを設定した上限以下に調整します。 つまり、VBR エンコーディングプロセスでは、メディアファイルのビットレートが、そのニーズに応じて動的に増減します。

   VBR は、CBR よりエンコードに時間がかかりますが、生成されるメディアファイルは最高品質となります。VBR は、ビデオコンテンツの HTTP プログレッシブ配信に最も一般的に使用されます。

**VBR と CRB のどちらを使用するべきか** VBR と CBR のどちらを選択するべきかという話になると、ほとんどの場合、メディアファイルには VBR を使用することをお勧めします。VBR は、優位性のあるビットレートで CBR より高品質のファイルを生成します。VBR を使用するときは、2 パスエンコーディングを使用し、最大ビットレートをターゲットビデオのビットレートの 1.5 倍に設定してください。

ビデオエンコーディングプリセットを選択するときには、ターゲットのエンドユーザーの接続速度を考慮してください。その速度の 80 ％のデータレートを持つプリセットを選択してください。例えば、ターゲットのエンドユーザーの接続速度が 1,000 Kbps の場合の最適なプリセットは、ビデオデータレートが 800 Kbps のプリセットです。

次の表に、一般的な接続速度のデータレートを示します。

| 速度（Kbps） | 接続タイプ |
|--- |--- |
| 256 | ダイアルアップ接続。 |
| 800 | 一般的なモバイル接続。この接続では、3G エクスペリエンス向けに 400～800 の範囲のデータレートがターゲットとなります。 |
| 2,000 | 一般的なブロードバンドデスクトップ接続。この接続では、データレートを800 ～ 2000 Kbpsの範囲でターゲットにします。ほとんどのターゲットは平均1200 ～ 1500 Kbpsです。 |
| 5,000 | 一般的な高帯域幅接続。この高帯域幅の範囲でのエンコードは推奨されません。ほとんどのユーザーに対して、この速度でビデオを配信することはできません。 |

### 解像度 {#resolution}

**解像度**&#x200B;は、ビデオファイルの高さと幅をピクセル単位で表したものです。ほとんどのソースビデオは、1,920 x 1,080 などの高解像度で保存されます。ストリーミング用のソースビデオは、比較的低い解像度（640 x 480 以下）に圧縮されます。

解像度とデータレートは、ビデオの品質を決める、一体的な関連を持つ 2 つの要素です。同じビデオ品質を維持するには、ビデオファイル内のピクセル数が多いほど（解像度が高いほど）、データレートを高くする必要があります。例えば、320 x 240 の解像度と 640 x 480 の解像度のビデオファイルにおけるフレームあたりピクセル数を考察すると、次のようになります。

| 解像度 | フレームあたりピクセル数 |
|--- |--- |
| 320x240 | 76,800 |
| 640 x 480 | 307,200 |

640 x 480 のファイルのフレームあたりピクセル数は 4 倍あります。これら 2 つの解像度例で同じデータレートを達成するには、640 x 480 のファイルに対して 4 倍の圧縮率を適用します。その結果、ビデオの品質が低下する可能性があります。つまり、250 Kbps のビデオデータレートの場合、320 x 240 の解像度では高品質の表示が可能ですが、640 x 480 の解像度では高品質の表示は期待できません。

一般に、高いデータレートを使用するほど、ビデオの画質は良くなり、高い解像度を使用するほど、その画質を維持するために必要になるデータレートも（解像度が低い場合と比較して）増加します。

解像度とデータレートには関連があるので、ビデオをエンコードする際には次の 2 つの方法から選択できます。

* データレートを選択してから、選択したデータレートできれいに表示される最高の解像度でエンコードします。
* 解像度を選択してから、選択した解像度で高品質のビデオを配信するために必要になるデータレートでエンコードします。

マスタービデオファイルのビデオエンコーディングプリセットを選択（または作成）する場合は、次の表を使用して正しい解像度をターゲットにします。

| 解像度 | 高さ（ピクセル） | 画面サイズ |
|--- |--- |--- |
| 240p | 240 | ごく小さな画面 |
| 300p | 300 | 小型の画面（一般にモバイルデバイス用） |
| 360p | 360 | 小型の画面 |
| 480p | 480 | 中型の画面 |
| 720p | 720 | 大型の画面 |
| 1080p | 1080 | 高画質の大型の画面 |

### Fps (Frames per second) {#fps-frames-per-second}

日本および米国では、ほとんどのビデオは 1 秒あたりのフレーム数（fps）が 29.97 で撮影されます。また、ヨーロッパでは、ほとんどのビデオが 25 fps で撮影されます。映画は 24 fps で撮影されます。

マスタービデオファイルの fps レートに一致するビデオエンコーディングプリセットを選択します。例えば、マスタービデオが 25 fps の場合は、25 fps のエンコーディングプリセットを選択します。デフォルトでは、すべてのカスタムエンコーディングでマスタービデオファイルの fps が使用されます。そのため、ビデオエンコーディングプリセットを作成するときに、fps 設定を明示的に指定する必要はありません。

### ビデオエンコーディングのサイズ {#video-encoding-dimensions}

最適化の理由で、ソースビデオのサイズがエンコードされるすべてのビデオの整数倍になるようなエンコーディングのサイズを選択してください。

この比率を計算するために、ソースの幅をエンコードの幅で割って幅の比率を求めます。次に、ソースの高さをエンコードの高さで割って高さの比率を求めます。

結果の比率が整数の場合は、ビデオが最適なサイズで縮小されます。結果の比率が整数でない場合は、ディスプレイに圧縮による副作用のピクセルが残存して、ビデオの品質に影響を及ぼします。この影響は、ビデオにテキストが含まれる場合に特に目立ちます。

例として、1,920 x 1,080 のソースビデオを取り上げます。次の表の 3 つのエンコードされたビデオは、使用すべき最適なエンコーディング設定です。

<table> 
 <tbody> 
  <tr> 
   <th><p>ビデオタイプ</p> </th> 
   <th><p>幅 x 高さ</p> </th> 
   <th><p>幅の比率</p> </th> 
   <th><p>高さの比率</p> </th> 
  </tr>
  <tr> 
   <td><p>ソース</p> </td> 
   <td><p>1920 x 1080</p> </td> 
   <td><p>1</p> </td> 
   <td><p>1</p> </td> 
  </tr> 
  <tr> 
   <td><p>エンコード</p> </td> 
   <td><p>960 x 540</p> </td> 
   <td><p>2</p> </td> 
   <td><p>2</p> </td> 
  </tr> 
  <tr> 
   <td><p>エンコード</p> </td> 
   <td><p>640 x 360</p> </td> 
   <td><p>3</p> </td> 
   <td><p>3</p> </td> 
  </tr> 
  <tr> 
   <td><p>エンコード</p> </td> 
   <td><p>480 x 270</p> </td> 
   <td><p>4</p> </td> 
   <td><p>4</p> </td> 
  </tr> 
 </tbody> 
</table>

### エンコードされたビデオのファイル形式 {#encoded-video-file-format}

Dynamic Media では、MP4 H.264 ビデオエンコーディングプリセットの使用を推奨しています。MP4 ファイルでは H.264 ビデオコーデックが使用されるので、高品質のビデオを圧縮されたファイルサイズで作成することができます。

## YouTube へのビデオの公開 {#publishing-videos-to-youtube}

以前作成した YouTube チャンネルに、オンプレミス AEM ビデオアセットを直接公開できます。

ビデオアセットを YouTube に公開するには、タグを使用して AEM Assets をセットアップします。これらのタグを YouTube チャンネルに関連付けます。ビデオアセットのタグがYouTubeチャネルのタグと一致する場合、ビデオはYouTubeに公開されます。 ビデオアセットにタグがない場合、YouTubeには投稿されません。

YouTubeに公開すると、AEMの処理プロファイルシステムがバイパスされ、ビデオエンコーディングプロファイルもバイパスされます。 これは、YouTubeに独自のエンコーディングがあるので、ビデオ処理プロファイルを必要としないためです。 ただし、ほとんどの場合は、ビデオアセットにビデオ処理プロファイルを適用しておくことが予期されています。ビデオ処理プロファイルをバイパスしてYouTubeに直接公開する場合、AEM Asset内のビデオアセットには表示可能なサムネールが表示されません。 また、ダイナミックメディア実行モードで実行する場合、エンコードされていないビデオは、どのダイナミックメディアアセットタイプとも機能しません。

YouTubeサーバーにビデオアセットを公開するには、YouTubeでの安全で安全なサーバー間認証を確実に行うために、次のタスクを実行する必要があります。

1. [Google Cloud 設定](#configuring-google-cloud-settings)
1. [YouTube チャネルの作成](#creating-a-youtube-channel)
1. [公開用タグの追加](#adding-tags-for-publishing)
1. [YouTube への公開のレプリケーションエージェントの有効化](#enabling-the-youtube-publish-replication-agent)
1. [AEM での YouTube の設定](#setting-up-youtube-in-aem)
1. [（オプション）アップロードしたビデオのデフォルト YouTube プロパティ設定の自動化](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [YouTube チャンネルへのビデオの公開](#publishing-videos-to-your-youtube-channel)
1. [（オプション）YouTube での公開済みビデオの確認](video.md#optional-verifying-the-published-video-on-youtube)
1. [Web アプリケーションへの YouTube URL のリンク](#linking-youtube-urls-to-your-web-application)

また、[ビデオを非公開にして YouTube から削除する](#unpublishing-videos-to-remove-them-from-youtube)こともできます。

### Google Cloud 設定 {#configuring-google-cloud-settings}

YouTube に公開するには、Google アカウントが必要です。GMAIL のアカウントを持っている場合は、既に Google アカウントも所有しています。Google アカウントがない場合も、簡単に作成できます。YouTubeにビデオアセットを公開するには資格情報が必要なので、アカウントが必要です。 If you have an account already created, then skip this task and proceed to [Creating a YouTube channel](#creating-a-youtube-channel).

>[!NOTE]
>
>以下の手順は、このドキュメントを執筆している時点で正確なものです。Google は、Web サイトを予告なく定期的に更新します。そのため、以下の手順は、最新の手順とは少し異なる場合もあります。

**Google cloudを設定するには**:

1. 新しい Google アカウントを作成します。

   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   既に Google アカウントを持っている場合は、次のステップに進んでください。

1. Go to [https://cloud.google.com/](https://cloud.google.com/).
1. On the Google Cloud Platform page, near the top, tap **[!UICONTROL Console]**. Google アカウントの資格情報を使用して、「**ログイン**」しなければならない場合もあります。
1. On the **[!UICONTROL Dashboard]** page, tap **[!UICONTROL Create Project]**.
1. In the **[!UICONTROL New Project]** dialog box, enter in a project name.

    プロジェクト ID は、プロジェクト名に基づいて付けられます。そのため、プロジェクト名は慎重に選んでください。プロジェクト名を後で変更することはできません。また、後でAdobe Experience ManagerでYouTubeを設定する場合は、同じプロジェクトIDを再入力する必要があります。 このプロジェクト ID はメモしておいてください。
1. 「**[!UICONTROL 作成]**」をタップします。

1. On your project’s **[!UICONTROL Dashboard]**, in the **[!UICONTROL Getting Started]** card, tap **[!UICONTROL Enable APIs and get credentials like keys]**.
1. Near the top of the **[!UICONTROL Dashboard]** page, tap **[!UICONTROL Enable API]**.
1. On the **[!UICONTROL Library]** page, under YouTube APIs, tap **[!UICONTROL YouTube Data API]**.
1. Near the top of the **YouTube Data API v3]** page, tap **[!UICONTROL Enable]** to turn it on.
1. この API を使用するために資格情報が必要となる場合があります。If necessary, tap **[!UICONTROL Create Credentials]**.
1. 「**[!UICONTROL API を呼び出す場所]**」ドロップダウンリストから、「**[!UICONTROL ウェブサーバー（node.js、Tomcat など）]**」を選択します。
1. 「**[!UICONTROL アクセスするデータの種類]**」で、「**[!UICONTROL ユーザーデータ]**」を選択します。
1. 「**[!UICONTROL 必要な認証情報」をタップします。]**」ボタンをクリックします。
1. 「**[!UICONTROL OAuth 2.0 クライアント ID を作成する]**」の下で、一意の名前を入力します。
1. In the text field under the **[!UICONTROL Authorized Javascript origins]** heading, enter the following path, substituting your own domain and port number in the path, then press **[!UICONTROL Enter]** to add the path to the list:

   `https://<servername.domain>:<port_number>`

   例：`https://1a2b3c.mycompany.com:4321`

   **注意**：上記のパスは入力例です。

1. In the text field under the **[!UICONTROL Authorized redirect URIs]** heading, enter the following, substituting your own domain and port number in the path, then press Enter to add the path to the list:

   `https://<servername.domain>:<port#>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   例：`https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **注意**：上記のパスは入力例です。

1. Tap **[!UICONTROL Create client ID]**.
1. On the Credentials page, under the **[!UICONTROL Set up the OAuth 2.0 consent screen]** heading, select the Gmail address that you are currently using.
1. 「**[!UICONTROL ユーザーに表示するサービス名]**」の下にあるテキストフィールドに、同意画面に表示するサービス名を入力します。

   同意画面は、AEM 管理者が YouTube の認証をおこなう際に表示され、AEM は YouTube に権限を要求します。

1. 「続行」を **[!UICONTROL タップしま]**&#x200B;す。
1. Under the **[!UICONTROL Download credentials]** heading, tap **[!UICONTROL Download]**.
1. Save the `client_id.json` file.

   このダウンロードした JSON ファイルは、後で Adobe Experience Manager で YouTube をセットアップするときに必要になります。


1. 「**[!UICONTROL Done]**」をタップします。

   次は、YouTube チャネルを作成します。

### YouTube チャネルの作成 {#creating-a-youtube-channel}

YouTube にビデオを公開するには、1 つ以上のチャネルが必要です。既に YouTube チャンネルを作成している場合は、このタスクをスキップして、次の「**公開用タグの追加**」タスクに進んでください。

>[!CAUTION]
>
>Be sure you have already set up one or more channels in YouTube &amp;ast;before&amp;ast; you add channels under YouTube Settings in AEM (see [Setting up YouTube in AEM](#setting-up-youtube-in-aem) below). この操作に失敗した場合、既存のチャネルが存在しないという警告は表示されません。 ただし、チャネルを追加してもGoogle認証は引き続き発生しますが、ビデオを送信するチャネルを選択するオプションはありません。

**YouTubeチャネルを作成するには**:

1. [https://www.youtube.com](https://www.youtube.com/) にアクセスし、Google アカウントの資格情報を使用してログインします。
1. In the upper-right corner of the YouTube page, tap your profile picture (may also appear as a letter within a solid colored circle), then tap **[!UICONTROL YouTube settings]** (round gear icon).
1. On the **[!UICONTROL Overview]** page, under the **[!UICONTROL Additional Features]** heading, tap **[!UICONTROL See all my channels or create a new channel]**.
1. On the **[!UICONTROL Channels]** page, tap **[!UICONTROL Create a new channel]**.
1. On the **[!UICONTROL Brand Account]** page, in the **[!UICONTROL Brand Account Name]** field, enter a business name or any other channel name you choose where you want to publish your video assets, then tap **[!UICONTROL Create]**.

   この名前は、AEM で YouTube をセットアップするときに入力する必要があるので、覚えておいてください。

1. （オプション）必要に応じて、さらにチャネルを追加します。

     次は、公開用タグを追加します。

### 公開用タグの追加 {#adding-tags-for-publishing}

AEM で、YouTube にビデオを公開するには、1 つ以上の YouTube チャンネルにタグを関連付けます。公開用タグの追加については、[タグの管理](/help/sites-administering/tags.md)を参照してください。

Or, if you intend to use the default tags in AEM, you can skip this task and go to [Enabling the YouTube Publish replication agent](#enabling-the-youtube-publish-replication-agent).

### YouTube への公開のレプリケーションエージェントの有効化 {#enabling-the-youtube-publish-replication-agent}

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Tools > Deployment > Replication > Agents on Author]**.
1. On the **[!UICONTROL Agents of Author]** page, tap **[!UICONTROL YouTube Publish (youtube)]**.
1. On the toolbar, to the right of Settings, tap **[!UICONTROL Edit]**.
1. 「**[!UICONTROL 有効]**」チェックボックスをオンにして、レプリケーションエージェントをオンにします。
1. tap **[!UICONTROL OK]**.

   次は、AEM で YouTube をセットアップします。

### AEM での YouTube の設定 {#setting-up-youtube-in-aem}

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Tools > Deployment > Cloud Services]**.
1. Under the **[!UICONTROL Third Party Services]** heading, under YouTube, tap **[!UICONTROL Configure now]**.
1. In the **Create Configuration]** dialog box, enter a title (mandatory) and name (optional) in the respective fields.
1. 「**[!UICONTROL 作成]**」をタップします。
1. In the **[!UICONTROL YouTube Account Settings]** dialog box, in the **[!UICONTROL Application Name]** field, enter the Google Project ID.

   このプロジェクト ID は、先ほど Google Cloud 設定をおこなったときに指定したものです。

   Leave the **[!UICONTROL YouTube Account Setting]** dialog box open; you will return to it in a moment.

1. 任意のテキストエディターを使用して、「Google Cloud 設定」のタスクでダウンロードして保存しておいた JSON ファイルを開きます。
1. この JSON テキスト全体を選択してコピーします。
1. Return to the **[!UICONTROL YouTube Account Settings]** dialog box. In the **[!UICONTROL JSON Config]** field, paste the JSON text.
1. 「**[!UICONTROL OK]**」をタップします。

   次は、AEM で YouTube チャンネルをセットアップします。

1. 「**[!UICONTROL 利用可能なチャネル]**」の右にある「**[!UICONTROL +]**」（プラス記号のアイコン）をタップします。
1. In the **[!UICONTROL YouTube Channel Settings]** dialog box, in the **[!UICONTROL Title]** field, enter the name of the channel that you created in the task **C[!UICONTROL reating a YouTube channel ]**earlier.

   必要に応じて、説明を追加することもできます。

1. 「**[!UICONTROL OK]**」をタップします。
1. YouTube／Google 認証が表示されます。Google Cloud アカウントにまだログインしていない場合は、この手順をスキップしてください。

   * 前述の Google プロジェクト ID と JSON テキストに関連付けられた Google ユーザー名とパスワードを入力します。
   * アカウントに存在するチャネルの数によっては、2 つ以上の項目が表示されます。チャネルを選択してください。電子メールアドレスを選択しないでください。
   * 次のページで、「**[!UICONTROL 確定]**」をタップして、このチャネルへのアクセスを許可します。

1. [ **[!UICONTROL許可**]をタップ

   次は、公開用タグを設定します。

1. **投稿用のタグの設定** - **[!UICONTROL Cloud Services/YouTubeページで]****** 、鉛筆アイコンをタップして、使用するタグのリストを編集します。
1. ドロップダウンリストアイコン（上下逆のキャレット）をタップして、AEM で利用可能なタグのリストを表示します。
1. 1 つ以上のタグをタップして追加します。

   追加したタグを削除するには、そのタグを選択して、「**[!UICONTROL X]**」をタップします。

1. When you are finished adding the tags you want, tap **[!UICONTROL OK]**.

   これで、YouTubeチャンネルにビデオを投稿します。

### （オプション）アップロードしたビデオのデフォルト YouTube プロパティ設定の自動化{#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

ビデオをアップロードする際に YouTube プロパティの設定を自動化できます。これをおこなうためには、メタデータ処理プロファイルを AEM で作成します。

メタデータ処理プロファイルを作成するには、まず「**[!UICONTROL フィールドラベル]**」、「**[!UICONTROL プロパティにマッピング]**」、「**[!UICONTROL 選択肢]**」の各フィールドの値をコピーします。これらはすべてビデオのメタデータスキーマで見つかります。次に、これらの値を追加して、YouTube ビデオメタデータ処理プロファイルを作成します。

**オプションで、アップロードしたビデオのデフォルトのYouTubeプロパティの設定を自動化するには**:

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Tools > Assets > Metadata Schemas]**.
1. 「**[!UICONTROL デフォルト値]**」をタップします。（「デフォルト値」の左側にある選択ボックスにチェックマークを追加しないでください）。
1. On the **[!UICONTROL default]** page, check the box to the left of **[!UICONTROL video]**, then tap **[!UICONTROL Edit]**.
1. On the **[!UICONTROL Metadata Schema Editor]** page, tap the **[!UICONTROL Advanced]** tab.
1. Under the YouTube Publishing heading, tap **[!UICONTROL YouTube Category]**. （YouTube カテゴリドロップダウンリストはタップしないでください。）
1. ページの右側の「**[!UICONTROL 設定]**」タブで次の手順を実行します。

   * 「**[!UICONTROL フィールドラベル]**」テキストフィールドで、値を選択してコピーします。

       コピーした値を、開いているテキストエディターに貼り付けます。後でメタデータ処理プロファイルを作成するときにこの値が必要になります。テキストエディターは開いたままにしておきます。

   * 「**[!UICONTROL プロパティにマッピング]**」テキストフィールドで、値を選択してコピーします。

       コピーした値を、開いているテキストエディターに貼り付けます。後でメタデータ処理プロファイルを作成するときにこの値が必要になります。テキストエディターは開いたままにしておきます。

   * 「**[!UICONTROL 選択肢]**」の下で、使用するデフォルト値（「人とブログ」または「科学と技術」など）を選択してコピーします。

       コピーした値を、開いているテキストエディターに貼り付けます。後でメタデータ処理プロファイルを作成するときにこの値が必要になります。テキストエディターは開いたままにしておきます。

1. Under the YouTube Publishing heading, tap **[!UICONTROL YouTube Privacy]**. （YouTube のプライバシードロップダウンリストはタップしないでください。）
1. ページの右側の「**[!UICONTROL 設定]**」タブで次の手順を実行します。

   * 「**[!UICONTROL フィールドラベル]**」テキストフィールドで、値を選択してコピーします。

       コピーした値を、開いているテキストエディターに貼り付けます。後でメタデータ処理プロファイルを作成するときにこの値が必要になります。テキストエディターは開いたままにしておきます。

   * 「**[!UICONTROL プロパティにマッピング]**」テキストフィールドで、値を選択してコピーします。

       コピーした値を、開いているテキストエディターに貼り付けます。後でメタデータ処理プロファイルを作成するときにこの値が必要になります。テキストエディターは開いたままにしておきます。

   * 「**[!UICONTROL 選択肢]**」の下で、使用するデフォルト値を選択してコピーします。選択肢は 2 つが 1 組になっています。1 組の下のフィールドは、コピーするデフォルト値（公開、非公開またはプライベート）です。

       コピーした値を、開いているテキストエディターに貼り付けます。後でメタデータ処理プロファイルを作成するときにこの値が必要になります。テキストエディターは開いたままにしておきます。

1. Near the upper-right corner of the **[!UICONTROL Metadata Schema Editor]** page, tap **[!UICONTROL Cancel]**.
1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Tools > Assets > Metadata Profiles]**.

1. On the **[!UICONTROL Metadata Profiles** page, near the upper-right corner of the page, tap **[!UICONTROL Create**. In the **[!UICONTROL Add Metadata Profile** dialog box, in the **[!UICONTROL Profile title]** text field, enter the name `YouTube Video`.
1. On the **[!UICONTROL Metadata Profile Editor]** page, tap the **[!UICONTROL Advance]** tab.
1. 次の手順を実行して、コピーした「YouTube への公開」の値を、プロファイルに追加します。

   * ページの右側で、「**[!UICONTROL フォームを作成]**」タブをタップします。
   * Drag the component labeled **[!UICONTROL Section Header]** to the left and drop it in the form area.
   * Tap **[!UICONTROL Field Label]** to select the component.
   * On the right side of the page, under the **[!UICONTROL Settings]** tab, in the **[!UICONTROL Field Label]** text field, enter `YouTube Publishing`.
   * Tap the **[!UICONTROL Build Form]** tab, then drag the component labeled **[!UICONTROL Single Line Text]** and drop it below the **[!UICONTROL YouTube Publishing]** heading that you just created.
   * Tap **[!UICONTROL Field Label]** to select the component.
   * On the right side of the page, under the **[!UICONTROL Settings]** tab, paste the **[!UICONTROL YouTube Publishing]** values (**[!UICONTROL Field Label]** value and **[!UICONTROL Map to property]** value) that you copied earlier, into their respective fields on the form. Paste the **[!UICONTROL Choices]** value into the **[!UICONTROL Default Value]** field.

1. 次の手順を実行して、コピーした「YouTube のプライバシー」の値を、プロファイルに追加します。

   * ページの右側で、「**[!UICONTROL フォームを作成]**」タブをタップします。
   * Drag the component labeled **[!UICONTROL Section Header]** to the left and drop it in the form area.
   * Tap **[!UICONTROL Field Label]** to select the component.
   * On the right side of the page, under the Settings tab, in the Field Label text field, enter `YouTube Privacy`.
   * Tap the **[!UICONTROL Build Form]** tab, then drag the component labeled **[!UICONTROL Single Line Text]** and drop it below the **[!UICONTROL YouTube Privacy]** heading you just created.
   * Tap **[!UICONTROL Field Label]** to select the component.
   * On the right side of the page, under the **[!UICONTROL Settings]** tab, paste the **[!UICONTROL YouTube Publishing]** values (**[!UICONTROL Field Label]** value and **[!UICONTROL Map to property]** value) that you copied earlier, into their respective fields on the form. Paste the **[!UICONTROL Choices** value into the **[!UICONTROL Default Value]** field.

1. ページの右上隅にある「**[!UICONTROL 保存]**」をタップします。
1. YouTube への公開メタデータプロファイルを、ビデオのアップロード先フォルダーに適用します。メタデータプロファイルとビデオプロファイルを設定する必要があります。

   詳しくは、[メタデータプロファイル](metadata-profiles.md)と[ビデオプロファイル](video-profiles.md)を参照してください。

### YouTube チャンネルへのビデオの公開 {#publishing-videos-to-your-youtube-channel}

次は、前の手順で追加したタグを、ビデオアセットに関連付けます。このプロセスにより、AEMはYouTubeチャネルに投稿するアセットを知ることができます。

To publish content from YouTube, AEM uses the **[!UICONTROL Publish to YouTube]** workflow, which lets you monitor progress and view any failure information.
詳しくは、[ビデオエンコーディングと YouTube への公開の進行状況の監視](#monitoring-video-encoding-and-youtube-publishing-progress)を参照してください。

**YouTubeチャネルにビデオを投稿するには**:

1. AEM で、YouTube チャネルに公開するビデオアセットの場所に移動します。
1. ビデオアセットを選択します。

   選択したビデオアセット（オリジナルのソースビデオや、そのエンコードされたレンディションなど）に関係なく、オリジナルのソースビデオが常にアップロードされます。

1. On the toolbar, tap **[!UICONTROL Properties]**.
1. In the **[!UICONTROL Basic]** tab, under the Metadata heading, tap **[!UICONTROL Browse]** to the right of the **[!UICONTROL Tags]** field.
1. On the **[!UICONTROL Select Tags]** page, navigate to the tags you want to use, and then select one or more tags.
1. In the upper-right corner of the page, tap the **[!UICONTROL Confirm]** icon.
1. In the upper-right corner of the video&#39;s properties page, tap **[!UICONTROL Save]**.
1. ツールバーの&#x200B;**[!UICONTROL 発行／発行]**&#x200B;をタップします。

   必要に応じて、YouTubeチャネルに公開されたビデオを検証できます。

### （オプション）YouTube での公開済みビデオの確認{#optional-verifying-the-published-video-on-youtube}

YouTube への公開（または非公開）の進行状況を監視できます。

詳しくは、[ビデオエンコーディングと YouTube への公開の進行状況の監視](#monitoring-video-encoding-and-youtube-publishing-progress)を参照してください。

公開にかかる時間は、マスタービデオの形式、ファイルサイズ、アップロードトラフィックなどの多数の要因により左右されます。公開プロセスにかかる時間は、数分から数時間までの幅があります。また、高解像度の形式では、レンダリングの時間がかかることにも注意してください。例えば、720p や 1080p の場合、表示されるまでの時間が 480p よりも大幅に長くなります。

8 時間経っても「**[!UICONTROL アップロード済み（処理中、お待ちください）]**」というステータスメッセージが表示される場合は、サイトからビデオを削除して再度アップロードしてみてください。

### Web アプリケーションへの YouTube URL のリンク {#linking-youtube-urls-to-your-web-application}

ビデオの公開後にダイナミックメディアによって生成されるYouTube URL文字列を取得できます。YouTube URLをコピーすると、そのURLはクリップボードに格納されるので、Webサイトやアプリケーションのページに必要に応じて貼り付けることができます。

YouTube URL は、ビデオアセットを YouTube に公開するまではコピーできません。

**YouTube URLをWebアプリケーションにリンクするには**:

1. Navigate to the YouTube *published* video asset whose URL you want to copy, then select it.

   Remember that YouTube URLs are only available to copy *after* you have first *published* the video assets to YouTube.

1. On the toolbar, tap **[!UICONTROL Properties]**.
1. 「**[!UICONTROL 詳細]**」タブをタップします。
1. Under the **[!UICONTROL YouTube Publishing]** heading, in the **[!UICONTROL YouTube URL]** List, select and copy the URL text to your web browser to preview the asset or to add to your web content page.

### ビデオを非公開にして YouTube から削除 {#unpublishing-videos-to-remove-them-from-youtube}

AEM でビデオアセットを非公開にすると、そのビデオは YouTube から削除されます。

>[!CAUTION]
>
>YouTube 内からビデオを直接削除すると、AEM にはそのことがわかりません。そのため、AEM は、そのビデオがまだ YouTube に公開されているかのように機能を続けます。ビデオアセットを YouTube で非公開にするときは、必ず AEM からおこなってください。

AEM では、YouTube からのコンテンツの削除に **[!UICONTROL YouTube で非公開]**&#x200B;ワークフローを使用します。このワークフローでは、進行状況を監視して、エラー情報を表示できます。詳しくは、[ビデオエンコーディングと YouTube への公開の進行状況の監視](#monitoring-video-encoding-and-youtube-publishing-progress)を参照してください。

**ビデオを非公開にしてYouTubeから削除するには**:

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Tools > Assets]**.
1. YouTube チャンネルで非公開にするビデオアセットの場所に移動します。
1. アセット選択モードで、1 つ以上の公開済みビデオアセットを選択します。
1. On the toolbar, tap **[!UICONTROL Unpublish > Unpublish]**.

## ビデオエンコーディングと YouTube への公開の進行状況の監視 {#monitoring-video-encoding-and-youtube-publishing-progress}

ビデオエンコーディングが適用されたフォルダーに新しいビデオをアップロードしたり、YouTube にビデオを公開したりする場合は、ビデオエンコーディング／YouTube への公開の進行状況（エラー状況）を様々な方法で監視できます。YouTube への公開の実際の進行状況は、ログを介してのみ把握できますが、YouTube への公開が失敗したか成功したかは、別の方法で示されます（以下の手順で説明します）。また、YouTube の公開ワークフローやビデオエンコーディングが完了するか中止されると、そのことを知らせる電子メール通知を受け取ることもできます。

### 進行状況の監視 {#monitoring-progress}

進行状況を監視するには（エンコーディング／YouTube の公開の失敗を含む）：

1. アセットフォルダー内のビデオエンコーディングの進行状況を表示します。

   * In **[!UICONTROL Card View]**, video encoding progress displays on the asset by percent. エラーがある場合、エラー情報はアセットにも表示されます。

      ![chlimage_1-429](assets/chlimage_1-429.png)

   * In **[!UICONTROL List View]**, video encoding progress displays in the **[!UICONTROL Processing Status]** column. エラーがある場合は、そのメッセージも同じ列に表示されます。

      ![chlimage_1-430](assets/chlimage_1-430.png)

      この列は、デフォルトでは表示されません。To enable the column, select **[!UICONTROL View Settings]** from the **[!UICONTROL Views]** drop-down menu, and add the **[!UICONTROL Processing Status]** column and tap **[!UICONTROL Update]**.

      ![chlimage_1-431](assets/chlimage_1-431.png)

1. アセット詳細の進行状況を表示します。When you tap an asset, open the drop-down menu and select **[!UICONTROL Timeline]**. タイムラインを、エンコーディングや YouTube への公開などのワークフローアクティビティに絞り込むには、「**[!UICONTROL ワークフロー]**」を選択します。

   ![chlimage_1-432](assets/chlimage_1-432.png)

   エンコーディングなどのワークフロー情報がタイムラインに表示されます。For YouTube publish, the **[!UICONTROL Workflow]** timeline also includes the name of the YouTube channel and the YouTube video URL. In addition, you see any failure notifications in the **[!UICONTROL Workflow]** timeline.

   >[!NOTE]
   >
   >It may take a long time for failure/error messages to finally be recorded due to multiple workflow configurations on **[!UICONTROL retries]**, **[!UICONTROL retry delay]**, and **[!UICONTROL timeout]** from [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr), for example:
   >
   >* Apache Sling Job Queue Configuration
   >* Adobe Granite Workflow External Process Job Handler
   >* Granite Workflow Timeout Queue
   > 
   >これらの設定の&#x200B;**[!UICONTROL 再試行]**、**[!UICONTROL 再試行遅延]**&#x200B;および&#x200B;**[!UICONTROL タイムアウト]**&#x200B;プロパティは調整できます。

1. For workflows in progress, see **Workflow Instances** available from **[!UICONTROL Tools > Workflow > Instances]**.

   >[!NOTE]
   >
   >**[!UICONTROL ツール]**&#x200B;メニューにアクセスするには、管理者権限が必要となる場合があります。

   ![chlimage_1-433](assets/chlimage_1-433.png)

   Select the instance and tap **[!UICONTROL Open History]**.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   From the **[!UICONTROL Workflow Instances]** area, you can also suspend, terminate, or rename workflows. See [Administering workflows](/help/sites-administering/workflows-administering.md) for more information.

1. For failed jobs, see **Workflow Failures** available from **[!UICONTROL Tools > Workflow > Failures]**. **[!UICONTROL ワークフローエラー]**&#x200B;に、エラーが発生したすべてのワークフローアクティビティが表示されます。

   >[!NOTE]
   >
   >**[!UICONTROL ツール]**&#x200B;メニューにアクセスするには、管理者権限が必要となる場合があります。

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >It may take a long time for the error message to finally be recorded due to multiple workflow configurations on **[!UICONTROL retries]**, **[!UICONTROL retry delay]**, and **[!UICONTROL timeout]** from [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr), for example:
   >
   >* Apache Sling Job Queue Configuration
   >* Adobe Granite Workflow External Process Job Handler
   >* Granite Workflow Timeout Queue
   >
   >これらの設定の&#x200B;**[!UICONTROL 再試行]**、**[!UICONTROL 再試行遅延]**&#x200B;および&#x200B;**[!UICONTROL タイムアウト]**&#x200B;プロパティは調整できます。

1. For completed workflows, see **[!UICONTROL Workflow Archive]** available from **[!UICONTROL Tools > Workflow > Archive]**. **[!UICONTROL ワークフローアーカイブ]**&#x200B;に、完了したすべてのワークフローアクティビティが表示されます。

   **[!UICONTROL ツール]**&#x200B;メニューにアクセスするには、管理者権限が必要となる場合があります。

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. 中止またはエラーが発生したワークフロージョブに関する電子メール通知を受け取ることができます。これらの電子メール通知は、管理者が設定できます。詳しくは、[電子メール通知の設定](#configuring-e-mail-notifications)を参照してください。

#### 電子メール通知の設定 {#configuring-e-mail-notifications}

**[!UICONTROL ツール]**&#x200B;メニューにアクセスするには、管理者権限が必要となる場合があります。

通知の設定方法は、エンコーディングジョブに関する通知と、YouTube への公開ジョブに関する通知のどちらを希望しているかによって異なります。

* For encoding jobs, you can access the configuration page for all AEM workflow email notifications at **[!UICONTROL Tools > Operations > Web Console]** and by searching for **[!UICONTROL Day CQ Workflow Email Notification Service]**. See [Configuring Email Notification in AEM](/help/sites-administering/notification.md). You can select or clear the check boxes for **[!UICONTROL Notify on Abort]** or **[!UICONTROL Notify on Complete]** accordingly.

* YouTube への公開ジョブの場合、次の手順に従います。

1. In AEM, select **[!UICONTROL Tools > Workflow > Models]**.
1. 「YouTubeに投 **[!UICONTROL 稿」ワークフローを選択し]** 、「編集」をタッ **[!UICONTROL プします]**。
1. YouTubeのアップロードワークフ **[!UICONTROL ローステップを右クリックし]** 、「編集」をタッ **[!UICONTROL プします]**。
1. 「引数」タブを **タップします&#x200B;**。
1. 次のチェックボックスをオンまたはオフにできます。

   * **[!UICONTROL 公開開始]**
   * **[!UICONTROL 公開の失敗]**
   * **[!UICONTROL 投稿完了]**（チャネルとURLに関する情報を含む）
   チェックボックスをオフにすると、YouTube の公開ワークフローから指定された電子メール通知は届きません。

   >[!NOTE]
   >
   >これらの電子メールは YouTube に固有で、かつ一般的なワークフロー電子メール通知です。結果として、設定に応じて、**Day CQ Workflow Email Notification Service** で使用できる一般的な通知と、YouTube に固有の通知の 2 つの電子メール通知セットを受け取ることができます。

## ビデオレポートの表示 {#viewing-video-reports}

ビデオレポートは、ダイナミックメディア — ハイブリッドモードの実行時に使用できます。ダイナミックメディア — Scene7モードを実行している場合は、レポートを使用できません。

ビデオレポートには、指定した期間に複数の集計指標が表示され、*公開された*個々のビデオと集計されたビデオが期待どおりに動作しているかを監視できます。以下のトップ指標データは、Webサイト全体で公開されたすべてのビデオに関して集計されます。

* ビデオ開始
* 完了率
* ビデオの平均視聴時間
* ビデオの合計視聴時間
* 訪問別ビデオ数

すべての公開済みビデオの表も表示されるので、ビデオ開始数の合計に基づいて、Web サイトで視聴された上位のビデオを追跡できます。**

リストのビデオ名をタップすると、ビデオのオーディエンス保持（ドロップオフ）レポートが折れ線グラフの形式で表示されます。このグラフには、ビデオ再生中の特定の瞬間におけるビュー数が表示されます。ビデオを再生すると、プレーヤーの時間インジケーターと同期して縦棒が表示されていきます。この折れ線グラフのデータが急激に下るところは、オーディエンスが関心をなくして再生を終了したところです。

ビデオが Adobe Experience Manager Dynamic Media 以外でエンコードされた場合、オーディエンス保持（ドロップオフ）グラフおよび表内の再生率データは利用できません。

[Dynamic Media クラウドサービスの設定](/help/assets/config-dynamic.md)も参照してください。

>[!NOTE]
>
>トラッキングおよびレポートのデータは、Dynamic Media 独自のビデオプレーヤーと関連するビデオプレーヤープリセットの使用状況のみに基づいています。そのため、他のビデオプレーヤーによって再生されたビデオを追跡およびレポートすることはできません。

デフォルトでは、ビデオレポートを初めて入力すると、現在の月の最初から現在の月の日付で終わるビデオデータがレポートに表示されます。ただし、独自の日付範囲を指定することで、デフォルトの日付範囲を上書きできます。次にビデオレポートを開くと、指定した日付範囲が使用されます。

ビデオレポートの正常動作のために、ダイナミックメディアクラウドサービスの設定時に、レポートスイート ID が自動的に作成されます。そのときに、そのレポートスイート ID が発行サーバーにプッシュされ、アセットのプレビューの際に URL コピー機能で使用できるようになります。ただし、そのためには発行サーバーを事前にセットアップしておく必要があります。発行サーバーがセットアップされていない場合も、発行してビデオレポートを確認することはできますが、その際にはダイナミックメディアクラウド設定に戻って「**OK**」をタップする必要があります。

**ビデオレポートを表示するには**:

1. In the upper-left corner of AEM, tap the AEM logo, then in the left rail, tap **[!UICONTROL Tools > Assets > Video Reports]**.
1. ビデオレポートページで、次のいずれかの操作をおこないます。

   * 右上付近にある&#x200B;**[!UICONTROL ビデオレポートを更新]**&#x200B;アイコンをタップします。

      「更新」を使用する必要があるのは、レポートの最終日が今日の日付である場合のみです。これにより、前回レポートを実行した後に発生したビデオ追跡を確実に確認できます。

   * Near the upper-right corner, tap the **[!UICONTROL Date Picker]** icon.

      ビデオデータを表示する開始日と終了日の範囲を指定し、「**[!UICONTROL レポートを実行]**」をタップします。
   The **[!UICONTROL Top Metrics]** group box identifies various aggregate measurements for all *published* videos across your site.

1. 上位の公開済みビデオを示した表で、ビデオ名をタップしてビデオを再生し、そのビデオのオーディエンス保持（ドロップオフ）レポートを表示します。

### Scene7 HTML5 ビューア SDK を使用して作成したビデオビューアに基づくビデオレポートの表示 {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

ダイナミックメディアが提供する標準搭載のビデオビューアを使用している場合、または標準搭載のビデオビューアを基にカスタムビューアプリセットを作成した場合、ビデオレポートを表示するために追加の手順は必要ありません。ただし、Scene7 HTML5ビューアSDKに基づいて独自のビデオビューアを作成した場合は、次の手順を使用して、ビデオビューアがダイナミックメディアビデオレポートにトラッキングイベントを送信するようにします。

独自のビデオビューアを作成するには、Scene7 ビューアリファレンスと Scene7 HTML5 ビューア SDK を使用します。

詳しくは、[Scene7 ビューアリファレンスガイド](https://marketing.adobe.com/resources/help/en_US/s7/viewers_ref/index.html)を参照してください。

Scene7 HTML ビューア SDK は、Adobe Developer Connection からダウンロードできます。

詳しくは、[Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html) を参照してください。

Scene7 HTML5 ビューア SDK を使用して作成したビデオビューアに基づいてビデオレポートを表示するには：

1. 公開済みビデオアセットの場所に移動します。
1. アセットのページの左上隅付近にある、ドロップダウンリストで「**[!UICONTROL ビューア]**」を選択します。
1. 任意のビデオビューアプリセットを選択し、埋め込みコードをコピーします。
1. 埋め込みコード内の次の行を探します。

   `videoViewer.setParam("config2", "<value>");`

   このパラ `config2` メーターは、HTML5ビューアでの追跡を有効にします。 また、ビデオレポートの設定情報や、お客様固有のAdobe Analytics設定を含む、会社固有のプリセットでもあります。

   config2 パラメーターの正しい値は、**[!UICONTROL 埋め込みコード]**&#x200B;と **[!UICONTROL URL コピー]**&#x200B;機能のいずれかで検索できます。**[!UICONTROL URL]** コピーコマンドから取得した URL 内でパラメーター `&config2=<value>` を探します。この値はほぼ常に `companypreset` ですが、一部のケースでは `companypreset-1`、`companypreset-2` などとなっていることもあります。

1. カスタムのビデオビューアコードで、次の操作をおこなって、ビューアページに AppMeasurementBridge.jsp を追加します。

   * 最初に、パラメータが必要かどうかを判断 `&preset` します。

      パラメータ `config2` ーが `companypreset`である場合は、必 *要はありませ*`&preset=parameter`ん。

      その他 `config2` の場合は、プリセットパラメータをパラメータと同じに設定し `config2` ます。 例えば、AppMeasurmentBridge.jsp `config2=companypreset-2`のURL `&param2=companypreset-2` にを追加します。

   * 次に、AppMeasurementBridge.jspスクリプトを追加します。

      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. 次の操作をおこなって、TrackingManager コンポーネントを作成します。

   * After calling `s7sdk.Utils.init();` create a TrackingManager instance to track events by adding the following:

      `var trackingManager = new s7sdk.TrackingManager();`

   * 次の手順を実行して、コンポーネントをTrackingManagerに接続します。

      イベントハ `s7sdk.Event.SDK_READY` ンドラーで、追跡するコンポーネントをTrackingManagerにアタッチします。

      例えば、コンポーネントが `videoPlayer`

      `trackingManager.attach(videoPlayer);`

      
を使用して、コンポーネントをtrackingManagerにアタッチします。 ページ上の複数のビューアを追跡するには、複数のトラッキングマネージャーコンポーネントを使用します。

   * 次を追加して、AppMeasurementBridgeオブジェクトを作成します。

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

   * 次を追加して、トラッキング関数を追加します。

      ```
      trackingManager.setCallback(appMeasurementBridge.track, 
       appMeasurementBridge);
      ```
   appMeasurementBridge オブジェクトには組み込みのトラッキング関数があります。ただし、複数のトラッキングシステムやその他の機能をサポートするために、独自のトラッキング関数を作成することもできます。

   For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

## ビデオへのキャプションの追加 {#adding-captions-to-video}

キャプションを 1 つのビデオまたはアダプティブビデオセットに追加することにより、ビデオの提供先をグローバルマーケットまで広げることができます。キャプションを追加すると、言語ごとの音声の吹き替えの必要性、つまりネイティブスピーカーを使って音声を再録音する必要性がなくなります。ビデオは録画された言語で再生されます。外国語のサブタイトルが表示されるので、違う言語の視聴者も音声部分を理解できます。

聴覚障害者のためのクローズドキャプションを使用することで、キャプションによってアクセシビリティを大幅に向上させることもできます。

>[!NOTE]
>
>使用するビデオプレーヤーがキャプションの表示に対応する必要があります。

Dynamic Media には、キャプションファイルを JSON（JavaScript Object Notation）形式に変換する機能があります。このように変換できるので、JSON テキストを、ビデオの完全なトランスクリプトとして表示せずに Web ページに埋め込むことができます。この後、検索エンジンがコンテンツをクロールしてインデックスを作成できます。これにより、ビデオを検索しやすくなり、ビデオコンテンツの詳細がユーザーに提供されます。

URL で JSON 機能を使用する方法について詳しくは、Scene7 画像サービング API ヘルプの[静的コンテンツ（画像以外）の提供（英語）](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/c_serving_static_nonimage_contents.html)を参照してください。**

**ビデオにキャプションまたはサブタイトルを追加するには**:

1. サードパーティアプリケーションまたはサービスを使用して、ビデオキャプション／サブタイトルのファイルを作成します。

   WebVTT（Web Video Text Tracks）標準に従ってファイルを作成してください。キャプションファイルの拡張子は .vtt です。WebVTT キャプション標準をよく確認してください。

   [WebVTT：Web Video Text Tracks 形式（英語）](https://dev.w3.org/html5/webvtt/)を参照してください。

   Dynamic Media の外部でキャプション／サブタイトルのファイルを作成するための無料ツールや有料ツールがあります。例えば、スタイル設定なしの単純なビデオキャプションファイルを作成するには、次に示すキャプションの作成および編集用の無償オンラインツールを使用できます。

   [WebVTT Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

   よい結果を得るためには、このツールを Explorer 9 以上、Google Chrome、または Safari で使用してください。

   In the tool, in the **[!UICONTROL Enter URL of video file]** field, paste the copied URL of your video file and then tap **[!UICONTROL Load]**. [アセットの URL の取得](linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)を参照して、ビデオファイルそのものの URL を取得し、それを「**[!UICONTROL ビデオファイルの URL を入力]**」フィールドに貼り付けてください。その後、Internet Explorer、Chrome、または Safari で、ビデオを再生できます。

   ここで、サイトの画面に表示される指示に従って、WebVTT ファイルを作成して保存します。終了したら、キャプションファイルの内容をコピーし、空のテキストエディターに貼り付けて、ファイル拡張子 .vtt を付けて保存します。

   >[!NOTE]
   >
   >複数言語のビデオサブタイトルを用意してグローバル対応する場合、WebVTT 標準では、サポート対象の言語ごとに個別の .vtt ファイルを作成して呼び出す必要があります。

   通常、VTT ファイルの名前はビデオファイルと同じにして、言語ロケール（-EN、-FR、-DE など）を追加します。そうしておくと、既存の Web コンテンツ管理システムを使用してビデオの URL を自動的に生成する際に役立ちます。

1. AEMで、WebVTTキャプションファイルをDAMにアップロードします。
1. Navigate to the *published* video asset that you want to associate with the caption file that you uploaded.

   URL をコピーするには、その&#x200B;*前に*&#x200B;アセットを&#x200B;*公開*&#x200B;しておく必要があります。

   [アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

1. 次のいずれかの操作をおこないます。

   * ポップアップビデオビューアエクスペリエンスの場合、「**[!UICONTROL URL]**」をタップします。URL ダイアログボックスで、URL を選択してクリップボードにコピーし、その URL を単純なテキストエディターに貼り付けます。コピーしたビデオのURLを次の構文で追加します。

      `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

      キャプション `,1` パスの末尾にあるをメモしておきます。 Immediately following the .vtt filename extension in the path, you have the option to enable (turn on) or disable (turn off) the closed caption button on the video player bar by setting to `,1` or `,0`, respectively.

   * For an embedded video viewer experience, tap **[!UICONTROL Embed Code]**. 埋め込みコードダイアログボックスで、埋め込みコードを選択してクリップボードにコピーし、単純なテキストエディターに貼り付けます。 コピーした埋め込みコードを次の構文で追加します。

      `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

      キャプション `,1` パスの末尾にあるをメモしておきます。 Immediately following the .vtt filename extension in the path, you have the option to enable (turn on) or disable (turn off) the closed caption button on the video player bar by setting to `,1` or `,0`, respectively.

## ビデオへのチャプターマーカーの追加 {#adding-chapter-markers-to-video}

1 つのビデオまたはアダプティブビデオセットにチャプターマーカーを追加すると、長編ビデオの視聴と操作が簡単になります。ユーザがビデオを再生するとき、ビデオタイムライン（ビデオスクラバー）のチャプターマーカーをタップすると、目標地点に簡単に移動したり、新しいコンテンツ、デモ、チュートリアルなどに直ちにジャンプしたりできます。

>[!NOTE]
>
>ビデオプレーヤーが、チャプターマーカーの使用をサポートしている必要があります。Dynamic Media ビデオプレーヤーは、チャプターマーカーをサポートしていますが、サードパーティのビデオプレーヤーは、チャプターマーカーを必ずしもサポートしているとは限りません。

必要であれば、ビデオビューアプリセットを使用するのではなく、チャプター機能を備えた独自のカスタムビデオビューアを作成して、ブランディングできます。チャプターナビゲーション機能を備えた独自の HTML5 ビューアの作成方法について詳しくは、『Adobe Scene Viewer SDK for HTML5』の「Customizing Behavior Using Modifiers」で `s7sdk.video.VideoPlayer` クラスと `s7sdk.video.VideoScrubber`7 クラスの説明を参照してください。Adobe Scene7 Viewer SDK は、[Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html) からダウンロードして入手できます。

 ビデオのチャプターリストを作成する方法は、キャプションを作成する方法とほとんど同じです。つまり、WebVTT ファイルを作成します。ただし、WebVTT キャプションファイルも使用する場合は、WebVTT ファイルと分けておく必要があります。キャプションとチャプターを 1 つの WebVTT ファイルにまとめることはできません。

 チャプターナビゲーション機能を備えた WebVTT ファイルを作成する際に使用するフォーマットの例として、次のサンプルを使用できます。

### ビデオチャプターナビゲーション機能を備えた WebVTT ファイル {#webvtt-file-with-video-chapter-navigation}

```xml
WEBVTT 
Chapter 1 
00:00.000 --> 01:04.364 
The bicycle store behind it all. 
Chapter 2 
01:04.364 --> 02:00.944 
Creative Cloud. 
Chapter 3 
02:00.944 --> 03:02.937 
Ease of management for a working solution. 
Chapter 4 
03:02.937 --> 03:35.000 
Cost-efficient access to rapidly evolving technology.
```

上記の例では、`Chapter 1` はキュー識別子で、オプションです。`00:00:000 --> 01:04:364` のキュー時間は、チャプターの開始時間と終了時間を、`00:00:000` という形式で指定しています。最後の 3 桁はミリ秒で、`000` のまま残しておくこともできます。The chapter title of `The bicycle store behind it all` is the actual description of the chapter’s contents. ユーザーが、ビデオのタイムラインのビジュアルキューポイントにマウスポインターを置くと、キュー識別子、開始キュー時間およびチャプタータイトルが、ビデオプレーヤー内にポップアップ表示されます。

 HTML5 ビデオビューアを使用するので、作成するチャプターファイルが WebVTT（Web Video Text Tracks）標準に準拠していることを確認してください。チャプターファイルの拡張子は .vtt です。WebVTT キャプション標準をよく確認してください。

 詳しくは、[WebVTT: The Web Video Text Tracks Format](https://dev.w3.org/html5/webvtt/) を参照してください。

**ビデオにチャプターマーカーを追加するには：**

1. AEM 外で、単純なテキストエディターを使用して、ビデオチャプターファイルを作成します。

   英語以外の言語のビデオチャプターを用意してグローバル対応する場合、WebVTT 標準では、サポート対象の言語ごとに個別の .vtt ファイルを作成して呼び出す必要があります。

1. Save the `.vtt` file in UTF8 encoding to avoid problems with character rendition in the chapter title text.

    一般に、チャプター VTT ファイルの名前には、ビデオファイルと同じ名前を付けて、名前の末尾にチャプターを追加します。そうしておくと、既存の Web コンテンツ管理システムを使用してビデオの URL を自動的に生成する際に役立ちます。
1. AEMで、WebVTTチャプターファイルをアップロードします。

   [アセットのアップロード](managing-assets-touch-ui.md#uploading-assets)を参照してください。

1. 次のいずれかの操作をおこないます。

   <table> 
     <tbody> 
      <tr> 
       <td>ポップアップビデオビューアの操作</td> 
       <td> 
       <ol> 
       <li>Navigate to the <i>published </i>video asset that you want to associate with the chapter file that you uploaded. URL をコピーするには、その<i>前に</i>アセットを<i>公開</i>しておく必要があります。<a href="/help/assets/publishing-dynamicmedia-assets.md">アセットの公開</a>を参照してください。</li> 
       <li>ドロップダウンメニューから「ビューア」をタッ <strong>プします</strong>。</li> 
       <li>左側のレールで、ビデオビューアのプリセット名をタップします。 ビデオのプレビューが別のページで開きます。</li> 
       <li>左側のレールの下部にある「<strong>URL</strong>」をタップします。</li> 
       <li>URLダイアログボックスで、URLを選択してクリップボードにコピーし、URLを単純なテキストエディターに貼り付けます。</li> 
       <li><br /> コピーしたビデオのURLを次の構文と共に追加し、コピーしたURLとチャプターファイルに関連付けます。 <br /> <code>&amp;navigation=&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;</code><br /> </li> 
      </ol> </td> 
      </tr> 
      <tr> 
       <td>埋め込みビデオビューアの操作<br /> </td> 
       <td> 
       <ol> 
       <li>Navigate to the <i>published </i>video asset that you want to associate with the chapter file that you uploaded. URL をコピーするには、その<i>前に</i>アセットを<i>公開</i>しておく必要があります。<a href="/help/assets/publishing-dynamicmedia-assets.md">アセットの公開</a>を参照してください。</li> 
       <li>ドロップダウンメニューから「ビューア」をタッ <strong>プします</strong>。</li> 
       <li>左側のレールで、ビデオビューアのプリセット名をタップします。 ビデオのプレビューが別のページで開きます。</li> 
       <li>In the left rail, at the bottom, tap <strong>Embed</strong>.</li> 
       <li>埋め込みコードダイアログボックスで、コード全体を選択してクリップボードにコピーし、単純なテキストエディターに貼り付けます。</li> 
       <li>ビデオの埋め込みコードを次の構文と共に追加し、コピーしたチャプターファイルのURLに関連付けます。<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt&gt;"</code></li> 
      </ol> </td> 
      </tr> 
     </tbody> 
    </table>

## ビデオのサムネールについて {#about-video-thumbnails}

Dynamic Media によって自動的に生成される 10 個のサムネール画像の中から、ビデオに追加する画像を 1 つ選択できます。選択したサムネールは、ビデオアセットを AEM Sites、AEM Mobile または AEM Screens のオーサリング環境で Dynamic Media コンポーネントと使用するときに、ビデオプレーヤーに表示されます。サムネールは、ビデオ全体のコンテンツを最も正確に表す静的な画像として機能し、さらに、再生ボタンをタップすることを推奨します。

ビデオの合計時間に基づいて、Dynamic Media は、10 個（デフォルト）のサムネール画像を、1％、11％、21％、31％、41％、51％、61％、71％、81％および 91％でビデオに取り込みます。10 個のサムネールは維持されます。つまり、後で別のサムネールを選択することになっても、一連のサムネールを再生成する必要はありません。10 個のサムネール画像をプレビューした後、ビデオで使用する画像を選択します。デフォルトに変更する場合は、CRXDE Lite を使用して、サムネール画像が生成される時間間隔を設定できます。例えば、等間隔の 4 つのサムネール画像をビデオから生成するだけの場合は、間隔時間を 24％、49％、74％および 99％に設定できます。

理論上、ビデオをアップロードしてから Web サイトで公開するまでの間は、ビデオサムネールをいつでも追加できます。

必要であれば、Dynamic Media によって生成されるサムネールを使用するのではなく、カスタムサムネールをアップロードしてビデオを表すことも可能です。例えば、ビデオのタイトル、人目を引くオープニング画像、またはビデオからキャプチャした特定の画像を持つカスタムサムネール画像を作成できます。アップロードするカスタムビデオサムネール画像は、最大解像度が 1280 x 720 ピクセル（最小幅 640 ピクセル）で、2MB を超えてはなりません。

>[!NOTE]
>
>カスタムビデオサムネールを使用できるのは、ダイナミックメディア - ハイブリッドモードを実行している場合のみです。

### ビデオサムネールの追加 {#adding-a-video-thumbnail}

1. ビデオサムネールを追加する、アップロードされたビデオアセットに移動します。
1. In asset selection mode either from the **[!UICONTROL List View]** or the **[!UICONTROL Card View]**, tap the video asset.
1. ツールバーの&#x200B;**[!UICONTROL プロパティを表示]**&#x200B;アイコン（丸で囲まれた「i」）をタップします。
1. On the video&#39;s **[!UICONTROL Properties]** page, tap **[!UICONTROL Change Thumbnail]**.
1. On the **[!UICONTROL Change Thumbnail]** page, on the toolbar, tap **[!UICONTROL Select Frame]**.

   デフォルトの時間間隔またはカスタマイズした時間間隔に基づき、Dynamic Media によって一連のサムネール画像がビデオから生成されます。

1. 生成されたサムネール画像をプレビューした後、ビデオに追加する画像を選択します。
1. 「**[!UICONTROL 変更を保存]**」をタップします。

   ビデオのサムネール画像が更新され、選択したサムネールが使用されます。後で、サムネール画像を変更する場合は、**[!UICONTROL サムネールを変更]**&#x200B;ページに戻って、新しい画像を選択できます。

   新しいデフォルトの時間間隔を設定した場合、または新しいビデオをアップロードして既存のビデオを置き換えた場合、Dynamic Media によってサムネールを再生成する必要があります。

   詳しくは、[ビデオサムネールが生成されるデフォルトの時間間隔の設定](#configuring-the-default-time-interval-that-video-thumbnails-are-generated)を参照してください。

#### ビデオサムネールが生成されるデフォルトの時間間隔の設定 {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

新しいデフォルトの時間間隔を設定して保存すると、この変更は、今後アップロードするビデオに対してのみ自動的に反映されます。以前にアップロードしたビデオには、新しいデフォルトは自動的に適用されません。既存のビデオについては、サムネールを再生成する必要があります。

詳しくは、[ビデオサムネールの追加](#adding-a-video-thumbnail)を参照してください。

ビデオサムネールが生成されるデフォルトの時間間隔を設定するには：

1. AEM で、**[!UICONTROL ツール／一般／CRXDE Lite]** をタップします。

1. In the CRXDE Lite page, in the directory panel on the left, navigate t `o etc/dam/imageserver/configuration/jcr:content/settings.`

   このディレクトリパネルが表示されない場合は、「ホーム」タブの左側にある >> アイコンをタップします。

1. On the lower-right panel, in the **[!UICONTROL Properties]** tab, double-tap `thumbnailtime`.
1. thumbnailtime を編集ダイアログボックスで、テキストフィールドに間隔値を割合で入力します。

   * プラス記号（+）アイコンをタップして、1 つ以上の間隔値フィールドを追加します。このアイコンは、ダイアログボックスの下部までスクロールしないと表示されない場合があります。
   * リストから間隔値フィールドを削除するには、そのフィールドの右側にあるマイナス記号（-）アイコンをタップします。
   * 上向き矢印アイコンと下向き矢印アイコンをタップして、間隔値の順序を変更します。

1. 「**[!UICONTROL OK]**」をタップして、「プロパティ」タブに戻ります。****
1. CRXDE Lite ページの左上隅にある「**[!UICONTROL すべて保存]**」をタップした後、左上隅の「ホームに戻る」アイコンをタップして AEM に戻ります。****

   詳しくは、[ビデオサムネールの追加](#adding-a-video-thumbnail)を参照してください。

### カスタムビデオサムネールの追加 {#adding-a-custom-video-thumbnail}

>[!NOTE]
>
>この機能を使用できるのは、ダイナミックメディア - ハイブリッドモードを実行している場合のみです。

1. ビデオサムネールを追加する、アップロードされたビデオアセットに移動します。
1. In asset selection mode either from the **[!UICONTROL List View]** or the **[!UICONTROL Card View]**, tap the video asset.
1. ツールバーの&#x200B;**[!UICONTROL プロパティを表示]**&#x200B;アイコン（丸で囲まれた「i」）をタップします。
1. On the video&#39;s **[!UICONTROL Properties]** page, tap **[!UICONTROL Change Thumbnail]**.
1. On the **[!UICONTROL Change Thumbnail]** page, on the toolbar, tap **[!UICONTROL Upload New Thumbnail]**.
1. 使用するサムネール画像に移動して、その画像を選択します。次に、「**[!UICONTROL 開く]**」をタップして、AEM への画像のアップロードを開始します。
1. After the image is successfully uploaded, in the **[!UICONTROL Change Thumbnail]** page, tap **[!UICONTROL Save Changes]**.

   カスタムサムネールがビデオに追加されます。

