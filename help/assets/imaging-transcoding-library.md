---
title: 画像トランスコーディングライブラリ
description: エンコーディング、トランスコーディング、画像のリサンプリング、画像のサイズ変更などの中心的な画像処理機能を実行する画像処理ソリューションであるアドビの画像トランスコーディングライブラリを設定および使用する方法について説明します。
contentOwner: AG
feature: Renditions,Developer Tools,Asset Processing
role: Admin
exl-id: 0314626d-e846-4f10-950e-6c1ceb7f4c06
source-git-commit: cc9b6d147a93688e5f96620d50f8fc8b002e2d0d
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 36%

---

# 画像トランスコーディングライブラリ {#imaging-transcoding-library}

アドビの画像トランスコーディングライブラリは独自の画像処理ソリューションであり、以下のような中心的な画像処理機能を実行できます。

* エンコード
* トランスコーディング（サポートされる形式間での変換）
* PS およびインテル IPP アルゴリズムを使用する画像リサンプリング
* ビット深度およびカラープロファイルの保持
* JPEG品質圧縮
* 画像のサイズ変更

画像トランスコーディングライブラリは、CMYK のサポートと、CMYK -Alpha を除く完全なアルファをサポートします。

画像トランスコーディングライブラリは、様々なファイル形式とプロファイルをサポートするだけでなく、パフォーマンス、拡張性、品質に関しては、他のサードパーティソリューションよりも大きなメリットがあります。 画像トランスコーディングライブラリを使用する主なメリットを次に示します。

* **ファイルサイズまたは解像度を増やして拡大**：拡大・縮小は、主にファイルのデコード中のサイズ変更によって実現します。これは画像トランスコーディングライブラリに搭載された特許取得済みの機能です。この機能により、ランタイム中のメモリ使用状況が常に最適化され、ファイルサイズの増加やメガピクセル解像度の二次関数ではなくなります。画像トランスコーディングライブラリは、より大容量の高解像度（メガピクセル値がより高い）ファイルを処理できます。ImageMagick などのサードパーティツールの場合、大容量のファイルを処理できず、ファイルの処理中にクラッシュします。
* **Photoshop 品質の圧縮およびサイズ変更アルゴリズム**：ダウンサンプリングの品質（スムーズ、シャープ、自動バイキュービック）および圧縮品質に関する業界標準に準拠しています。画像トランスコーディングライブラリは、入力画像の品質係数をさらに評価し、出力画像に最適なテーブルと品質設定をインテリジェントに使用します。 この機能により、画質を損なうことなく最適なサイズのファイルが作成されます。
* **高スループット：** 応答時間は短く、スループットは ImageMagick よりも常に高くなります。 したがって、画像トランスコーディングライブラリを使用すると、ユーザーの待ち時間が短縮され、ホスティングのコストが削減されます。
* **同時負荷に応じた拡張性：** 画像トランスコーディングライブラリは、同時読み込み条件下で最適に動作します。 CPU パフォーマンスとメモリ使用状況を最適化し、応答時間を短縮しながら、高スループットを実現するため、ホスティングコストを抑えることができます。

## サポートされているプラットフォーム {#supported-platforms}

画像トランスコーディングライブラリは、RHEL 7 および CentOS 7 ディストリビューションでのみ使用できます。

>[!NOTE]
>
>Mac OS やその他の *nix 系ディストリビューション（Debian、Ubuntu など）はサポートされていません。

## 使用方法 {#usage}

画像トランスコーディングライブラリ用のコマンドライン引数には、以下を使用できます。

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth ‘4’ is automatically converted to ‘8’
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

次のオプションを `-resize` パラメーター：

* `X`: `Works similar to AEM. For example -resize 319.`

* `WxH`: `Aspect Ratio will not be maintained, For example -resize 319X319.`

* `Wx`: `Fixes the width and calculates the height maintaining the aspect ratio. For example -resize 319x.`

* `xH`: `Fixes the height and calculates the width maintaining the aspect ratio. For example -resize x319.`

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## 画像トランスコーディングライブラリの設定 {#configuring-imaging-transcoding-library}

ITL 処理を設定するには、設定ファイルを作成し、ワークフローを更新して実行します。

### 抽出されたバンドルの設定ファイルを作成 {#create-conf-file}

ライブラリを設定するには、次の手順で、ライブラリを示す.conf ファイルを作成します。 管理者またはルート権限が必要です。

1. をダウンロードします。 [ソフトウェア配布からの画像トランスコーディングライブラリパッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) パッケージマネージャーを使用してインストールします。 このパッケージは [!DNL Experience Manager] 6.5.

1. のバンドル ID を知るには `com.day.cq.dam.cq-dam-switchengine`をクリックし、Web コンソールにログインしてをタップします。 **[!UICONTROL OSGi/バンドル]**. または、バンドルコンソールを開くには、 `https://[aem_server:[port]/system/console/bundles/` URL。 場所 `com.day.cq.dam.cq-dam-switchengine` バンドルとその ID。

1. コマンドを使用してフォルダーを確認し、必要なライブラリがすべて抽出されていることを確認します。 `ls -la /aem64/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`：フォルダー名はバンドル ID を使用して構築されます。 例えば、コマンドは次のようになります。 `ls -la /aem64/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` バンドル id がの場合 `588`.

1. 作成 `SWitchEngineLibs.conf` ファイルを追加して、ライブラリにリンクします。

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. 追加 `/aem64/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` 次を使用して conf ファイルにパス `cat SWitchEngineLibs.conf` コマンドを使用します。

1. 実行 `ldconfig` コマンドを使用して、必要なリンクとキャッシュを作成します。

1. AEMの起動に使用するアカウントで、を編集します。 `.bash_profile` ファイル。 追加 `LD_LIBRARY_PATH` 次の行を追加します。

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. パスの値がに設定されていることを確認するには、次のようにします。 `.`，使用 `echo $LD_LIBRARY_PATH` コマンドを使用します。 出力は次のようになります `.`. 値が `.`、セッションを再起動します。

### DAM アセットの更新ワークフローを設定 {#configure-dam-asset-update-workflow}

を更新します。 [!UICONTROL DAM アセットの更新] 画像の処理にライブラリを使用するワークフロー。

1. 次をタップまたはクリックします。 [!DNL Experience Manager] ロゴをクリックし、に移動します。 **[!UICONTROL ツール/ワークフロー/モデル]**.

1. 次の **[!UICONTROL ワークフローモデル]** ページで、 **[!UICONTROL DAM アセットの更新]** ワークフローモデルが編集モードになっています。

1. を開きます。 **[!UICONTROL サムネールを処理]** ワークフロープロセスステップ。 内 **[!UICONTROL サムネール]** 」タブで、デフォルトのサムネール生成プロセスをスキップする MIME タイプを **[!UICONTROL スキップ MIME タイプ]** リスト。
例えば、画像トランスコーディングライブラリを使用してTIFF画像のサムネールを作成する場合は、次のように指定します。 `image/tiff` 内 **[!UICONTROL スキップ MIME タイプ]** フィールドに入力します。

1. 「**[!UICONTROL Web に対応した画像]**」タブで、デフォルトの Web レンディション生成プロセスをスキップする MIME タイプを「**[!UICONTROL リストをスキップ]**」に追加します。例えば、MIME タイプをスキップした場合は、 `image/tiff` 上記の手順で、 `image/tiff` をスキップリストに追加します。

1. を開きます。 **[!UICONTROL EPSサムネール (powered by ImageMagick)]** ステップ、 **[!UICONTROL 引数]** タブをクリックします。 内 **[!UICONTROL MIME タイプ]** リストに、画像トランスコーディングライブラリで処理する MIME タイプを追加します。 例えば、MIME タイプをスキップした場合は、 `image/tiff` 上記の手順で、 `image/jpeg` から **[!UICONTROL MIME タイプ]** リスト。

1. 既定のコマンドが存在する場合は、そのコマンドを削除します。

1. サイドパネルを切り替えて、ステップのリストから&#x200B;**[!UICONTROL SWitchEngine ハンドラー]**&#x200B;を追加します。

1. コマンドを [!UICONTROL SwitchEngine ハンドラ] カスタム要件に基づいて。 必要に応じて、指定したコマンドのパラメータを調整します。 例えば、JPEG 画像のカラープロファイルを保持したい場合、「**[!UICONTROL コマンド]**」リストに以下のコマンドを追加します。

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![小児](assets/chlimage_1-199.png)

1. （オプション）1 つのコマンドを使用して、中間レンディションからサムネールを生成します。 中間レンディションは静的レンディションと Web レンディションを生成するソースとなります。この方法は最初の方法より処理が高速です。ただし、この方法ではサムネールにカスタムパラメーターを適用できません。

   ![小児](assets/chlimage_1-200.png)

1. Web レンディションを生成するには、 **[!UICONTROL Web 対応画像]** タブをクリックします。

1. 更新した [!UICONTROL DAM アセットの更新] ワークフローモデル。 ワークフローを保存します。

設定を確認し、TIFFイメージをアップロードして、error.log ファイルを監視します。 君は気づくだろう `INFO` メンションのあるメッセージ `SwitchEngineHandlingProcess execute: executing command line`. ログでは、生成されたレンディションが示されます。 ワークフローが完了したら、AEMで新しいレンディションを表示できます。

>[!MORELIKETHIS]
>
>* [サポートされる MIME タイプに関する記事](assets-formats.md#supported-image-transcoding-library)

