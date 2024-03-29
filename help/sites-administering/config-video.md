---
title: ビデオコンポーネントの設定
seo-title: Configure the Video component
description: ビデオコンポーネントの設定方法を説明します。
seo-description: Learn how to configure the Video Component.
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
exl-id: 46d0765d-fb77-4332-8fbb-5bd2abcd6806
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 37%

---

# ビデオコンポーネントの設定 {#configure-the-video-component}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

この [ビデオコンポーネント](/help/sites-authoring/default-components-foundation.md#video) では、事前定義済みの標準 (OOTB) ビデオ要素をページに配置できます。

適切なトランスコードをおこなうには、管理者が [FFmpeg のインストールとAEMの設定](#install-ffmpeg) 個別に。 また、 [ビデオプロファイルの設定](#configure-video-profiles) HTML5 要素で使用

>[!CAUTION]
>
>このコンポーネントは、広範なプロジェクトレベルのカスタマイズをしない限り、標準搭載の状態では使用できなくなりました。

## ビデオプロファイルの設定 {#configure-video-profiles}

HTML5 の要素に使用するビデオプロファイルを定義できます。 ここで選択したものは順番に使用されます。アクセスするには、[デザインモード](/help/sites-authoring/default-components-designmode.md)（クラシック UI のみ）を使用し、「**[!UICONTROL プロファイル]**」タブを選択します。

![chlimage_1-317](assets/chlimage_1-317.png)

また、ビデオコンポーネントのデザインと、 [!UICONTROL 再生], [!UICONTROL Flash]、および [!UICONTROL 詳細].

## FFmpeg のインストールと AEM の設定 {#install-ffmpeg}

ビデオコンポーネントは、からダウンロードできるビデオの適切なトランスコードに、サードパーティのオープンソース製品 FFmpeg を使用します。 [https://ffmpeg.org/](https://ffmpeg.org/). FFmpeg をインストールした後、特定のオーディオコーデックと特定のランタイムオプションを使用するようにAEMを設定する必要があります。

**お使いのプラットフォーム用の FFmpeg をインストールするには、以下を実行します。**:

* **Windows の場合：**

   1. コンパイル済みバイナリを次のようにダウンロードします。 `ffmpeg.zip`
   1. フォルダーに解凍します。
   1. システム環境変数の設定 `PATH` から `<*your-ffmpeg-locatio*n>\bin`
   1. AEM を再起動します。

* **Mac OS X の場合：**

   1. Xcode ([https://developer.apple.com/technologies/tools/xcode.html](https://developer.apple.com/technologies/tools/xcode.html))
   1. XQuartz/X11 をインストールします。
   1. MacPorts ([https://www.macports.org/](https://www.macports.org/))
   1. コンソールで、次のコマンドを実行し、指示に従います。

      `sudo port install ffmpeg`

      `FFmpeg` は、 `PATH` AEMはコマンドラインを使用してこれを取得できます。

* **OS X 10.6 用のプリコンパイル版を使用する場合：**

   1. コンパイル済みバージョンをダウンロードします。
   1. 次の場所に抽出します。 `/usr/local` ディレクトリ。
   1. ターミナルから、以下を実行します。

      `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`

**AEMを設定するには**:

1. Web ブラウザーで [!UICONTROL CRXDE Lite] を開きます。([http://localhost:4502/crx/de](http://localhost:4502/crx/de))
1. `/libs/settings/dam/video/format_aac/jcr:content` ノードを選択し、ノードのプロパティが次のようになっていることを確認します。

   * audioCodec:

      ```
       aac
      ```

   * customArgs:

      ```
       -flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8
      ```

1. 設定をカスタマイズするには、 `/apps/settings/` ノードにオーバーレイを作成し、同じ構造を `/conf/global/settings/` ノードの下に移動します。`/libs` ノードで編集することはできません。例えば、パス `/libs/settings/dam/video/fullhd-bp` をオーバーレイするには、`/conf/global/settings/dam/video/fullhd-bp` で作成します。

   >[!NOTE]
   >
   >変更が必要なプロパティだけでなく、プロファイルノード全体をオーバーレイして編集します。 このようなリソースは、SlingResourceMerger を介して解決されません。

1. いずれかのプロパティを変更した場合、 **[!UICONTROL すべて保存]**.

>[!NOTE]
>
>OOTB ワークフローモデルは、AEMインスタンスをアップグレードしても保持されません。 Adobeでは、OOTB ワークフローモデルを編集する前にコピーすることをお勧めします。 例えば、DAM アセットの更新モデルの FFmpeg トランスコーディング手順を修正する前に OOTB DAM アセットの更新モデルをコピーして、アップグレード前に存在していたビデオプロファイル名を選択します。その後、`/apps` ノードをオーバーレイして、AEM で OOTB モデルへのカスタム変更を取得できます。
