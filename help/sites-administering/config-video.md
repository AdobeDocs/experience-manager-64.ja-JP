---
title: ビデオコンポーネントの設定
seo-title: ビデオコンポーネントの設定
description: ビデオコンポーネントの設定方法について説明します。
seo-description: ビデオコンポーネントの設定方法について説明します。
uuid: f4755a13-08ea-4096-a951-46a590f8d766
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: a1efef3c-0e4b-4a17-bcad-e3cc17adbbf7
exl-id: 46d0765d-fb77-4332-8fbb-5bd2abcd6806
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 35%

---

# ビデオコンポーネントの設定  {#configure-the-video-component}

[ビデオコンポーネント](/help/sites-authoring/default-components-foundation.md#video)を使用すると、事前定義済みのOOTB（標準搭載）ビデオ要素をページに配置できます。

適切なトランスコードを行うには、管理者が[FFmpegをインストールし、AEM](#install-ffmpeg)を個別に設定する必要があります。 HTML5 要素と共に使用するために[ビデオプロファイルを設定](#configure-video-profiles)することもできます。

>[!CAUTION]
>
>このコンポーネントは、プロジェクトレベルのカスタマイズが必要な場合は、すぐに使用できる状態では機能しなくなりました。

## ビデオプロファイルの設定 {#configure-video-profiles}

HTML5 要素に使用するビデオプロファイルの定義が必要になる場合があります。ここで選択したものは順番に使用されます。アクセスするには、[デザインモード](/help/sites-authoring/default-components-designmode.md)（クラシック UI のみ）を使用して「**[!UICONTROL プロファイル]**」タブを選択します。

![chlimage_1-317](assets/chlimage_1-317.png)

[!UICONTROL 再生]、[!UICONTROL Flash]および[!UICONTROL 詳細]のビデオコンポーネントとパラメーターのデザインも設定できます。

## FFmpegをインストールし、AEM {#install-ffmpeg}を設定します。

ビデオコンポーネントは、[https://ffmpeg.org/](https://ffmpeg.org/)からダウンロードできるビデオの適切なトランスコードを行うために、サードパーティのオープンソース製品FFmpegを利用します。 FFmpegをインストールした後、特定のオーディオコーデックと特定のランタイムオプションを使用するようにAEMを設定する必要があります。

**お使いのプラットフォーム用にFFmpegをインストールするには**:

* **Windows の場合：**

   1. `ffmpeg.zip` というコンパイル済みバイナリをダウンロードします。
   1. フォルダーに解凍します。
   1. システム環境変数`PATH`を`<*your-ffmpeg-locatio*n>\bin`に設定します。
   1. AEM を再起動します。

* **Mac OS X：**

   1. Xcode([https://developer.apple.com/technologies/tools/xcode.html](https://developer.apple.com/technologies/tools/xcode.html))をインストールします。
   1. XQuartz/X11 をインストールします。
   1. MacPorts([https://www.macports.org/](https://www.macports.org/))をインストールします。
   1. コンソールで、次のコマンドを実行し、指示に従います。

      `sudo port install ffmpeg`

      `FFmpeg` AEMがコマンドラ `PATH` インから取得できるように、に設定する必要があります。

* **OS X 10.6 用のコンパイル済みバージョンの使用：**

   1. コンパイル済みバージョンをダウンロードします。
   1. `/usr/local`ディレクトリに展開します。
   1. ターミナルから、次の操作を実行します。

      `sudo ln -s /usr/local/Cellar/ffmpeg/0.6/bin/ffmpeg /usr/bin/ffmpeg`

**AEM**&#x200B;を設定するには：

1. Web ブラウザーで [!UICONTROL CRXDE Lite] を開きます。([http://localhost:4502/crx/de](http://localhost:4502/crx/de))
1. `/libs/settings/dam/video/format_aac/jcr:content`ノードを選択し、ノードのプロパティが次のようになっていることを確認します。

   * audioCodec：

      ```
       aac
      ```

   * customArgs:

      ```
       -flags +loop -me_method umh -g 250 -qcomp 0.6 -qmin 10 -qmax 51 -qdiff 4 -bf 16 -b_strategy 1 -i_qfactor 0.71 -cmp chroma -subq 8 -me_range 16 -coder 1 -sc_threshold 40 -b-pyramid normal -wpredp 2 -mixed-refs 1 -8x8dct 1 -fast-pskip 1 -keyint_min 25 -refs 4 -trellis 1 -direct-pred 3 -partitions i8x8,i4x4,p8x8,b8x8
      ```

1. 設定をカスタマイズするには、`/apps/settings/`ノードにオーバーレイを作成し、`/conf/global/settings/`ノードの下に同じ構造を移動します。 `/libs`ノードでは編集できません。 例えば、パス`/libs/settings/dam/video/fullhd-bp`をオーバーレイするには、`/conf/global/settings/dam/video/fullhd-bp`にパスを作成します。

   >[!NOTE]
   >
   >変更が必要なプロパティだけでなく、プロファイルノード全体をオーバーレイ／編集してください。そのようなリソースは SlingResourceMerger 経由で解決されません。

1. いずれかのプロパティを変更した場合は、「**[!UICONTROL すべて保存]**」をクリックします。

>[!NOTE]
>
>AEMインスタンスをアップグレードしても、OOTBワークフローモデルは保持されません。 Adobeでは、OOTBワークフローモデルを編集する前にコピーすることをお勧めします。 例えば、「 DAMアセットの更新」モデルの「 FFmpegトランスコーディング」手順を編集する前に、「 OOTB DAMアセットの更新」モデルをコピーして、アップグレード前に存在していたビデオプロファイル名を選択します。 次に、`/apps`ノードをオーバーレイして、AEMがOOTBモデルに対するカスタムの変更を取得できるようにします。
