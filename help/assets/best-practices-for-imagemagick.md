---
title: ImageMagick をインストールして、 [!DNL Experience Manager] Assets
description: ImageMagick ソフトウェアの概要と、インストール方法、コマンドラインプロセスのステップの設定方法、ImageMagick を使用して画像の編集、組み立て、サムネール生成をおこなう方法を学習します。
contentOwner: AG
feature: Renditions,Developer Tools
role: Admin
exl-id: 9aeda88a-fd66-4fad-b496-3352a6ecab81
source-git-commit: 63a4304a1a10f868261eadce74a81148026390b6
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 47%

---

# ImageMagick をインストールして、 [!DNL Experience Manager Assets] {#install-and-configure-imagemagick-to-work-with-aem-assets}

ImageMagick は、ビットマップ画像の作成、編集、作成、変換をおこなうためのソフトウェアプラグインです。 PNG、JPEG、JPEG2000、GIF、TIFF、DPX、EXR、WebP、Postscript、PDF、SVGなど、様々な形式（200 以上）の画像の読み取りと書き込みが可能です。 ImageMagick は、画像のサイズ変更、反転、ミラー、回転、変形、剪断および変換をおこなう場合に使用します。ImageMagick を使用して、画像の色を調整したり、各種特殊効果を適用したりすることもできます。また、テキスト、直線、多角形、楕円および曲線を描画することもできます。

ImageMagick を使用して画像を処理するには、コマンドラインからAdobe Experience Managerメディアハンドラーを使用します。 ImageMagick を使用して様々なファイル形式を取り扱うには、[Assets のファイル形式に関するベストプラクティス](assets-file-format-best-practices.md)を参照してください。すべてのサポートされるファイル形式については、[Assets でサポートされるファイル形式](assets-formats.md)を参照してください。

ImageMagick を使用して大きなファイルを処理する場合は、必要なメモリが通常より多くなること、IM ポリシーの変更が必要になる可能性があること、パフォーマンスへの全体的な影響を考慮してください。メモリ要件は、解像度、ビット深度、カラープロファイル、ファイル形式などの様々な要因によって異なります。ImageMagick を使用して非常に大きなファイルを処理する場合は、 [!DNL Experience Manager] サーバー。 いくつかの有用なリソースを最後に紹介します。

>[!NOTE]
>
>次を使用する場合： [!DNL Experience Manager] 大きなPSDや PSB ファイルを大量に処理する予定がある場合は、Adobe Managed Services(AMS) でAdobeカスタマーサポートにお問い合わせください。 Experience Managerは、30000 x 23000ピクセルを超える高解像度の PSB ファイルを処理できない場合があります。

## ImageMagick のインストール {#installing-imagemagick}

各種オペレーティングシステム向けに、様々なバージョンの ImageMagick インストールファイルが用意されています。オペレーティングシステムに適したバージョンを使用してください。

1. 適切な [ImageMagick のインストールファイル](https://www.imagemagick.org/script/download.php) ご使用のオペレーティングシステム用。
1. ImageMagick をホストするディスクにインストールするには [!DNL Experience Manager] サーバーで、インストールファイルを起動します。

1. path 環境変数を ImageMagick のインストールディレクトリに設定します。
1. インストールが成功したかどうかを確認するには、`identify -version` コマンドを実行します。

## コマンドラインプロセスのステップの設定 {#set-up-the-command-line-process-step}

特定の使用例に応じてコマンドラインプロセスのステップを設定できます。次の手順を実行して、JPEGイメージファイルをに追加するたびに、反転画像とサムネール (140 x 100、48 x 48、319 x 319、1280 x 1280) を生成します。 `/content/dam` の [!DNL Experience Manager] サーバ：

1. の [!DNL Experience Manager] サーバーで、ワークフローコンソール (`https://[aem_server]:[Port]/workflow`) をクリックし、 **[!UICONTROL DAM アセットの更新]** ワークフローモデル。
1. 次の **[!UICONTROL DAM アセットの更新]** ワークフローモデル、開く **[!UICONTROL EPSサムネール (powered by ImageMagick)]** 手順
1. 内 **[!UICONTROL 「引数」タブ]**，追加 `image/jpeg` から **[!UICONTROL MIME タイプ]** リスト。

   ![mime_types_jpeg](assets/mime_types_jpeg.png)

1. 「**[!UICONTROL コマンド]**」ボックスに、次のコマンドを入力します。

   `convert ./${filename} -flip ./${basename}.flipped.jpg`

1. を選択します。 **[!UICONTROL 生成されたレンディションを削除]** および **[!UICONTROL Web レンディションを生成]** フラグ。

   ![select_flags](assets/select_flags.png)

1. 「**[!UICONTROL Web に対応した画像]**」タブで、1280 x 1280 ピクセルというサイズでレンディションの詳細を指定します。さらに、i と指定します。*image/jpeg* 内 **[!UICONTROL MIME タイプ]** ボックス

   ![web_enabled_image](assets/web_enabled_image.png)

1. 「**[!UICONTROL OK]**」をタップまたはクリックして、変更内容を保存します。

   >[!NOTE]
   >
   >この `convert` 特定の Windows バージョン（Windows SE など）では、コマンドを実行できない場合があります。これは、ネイティブの `convert` Windows インストールに含まれるユーティリティ。 このような場合は、ImageMagick ユーティリティの完全パスを指定します。例えば、以下のように指定します。
   >
   >`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ./${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. を開きます。 **[!UICONTROL サムネールを処理]** 手順を実行し、MIME タイプを追加します。 `image/jpeg` under **[!UICONTROL スキップ MIME タイプ]**.

   ![skip_mime_types](assets/skip_mime_types.png)

1. 内 **[!UICONTROL Web に対応した画像]** 」タブで、MIME タイプを追加します。 `image/jpeg` の下に **[!UICONTROL リストをスキップ]**. 「**[!UICONTROL OK]**」をタップまたはクリックして、変更内容を保存します。

   ![web_enabled](assets/web_enabled.png)

1. ワークフローを保存します。
1. ImageMagic が画像を正しく処理できるかどうかを確認するには、にJPG画像をアップロードします。 [!DNL Assets]. その画像の反転画像とレンディションが生成されるかどうかを確認します。

## セキュリティの脆弱性の緩和 {#mitigating-security-vulnerabilities}

ImageMagick を使用した画像の処理に関連して、セキュリティの脆弱性が複数存在します。例えば、ユーザーが送信した画像の処理は、リモートコード実行（RCE）のリスクを伴います。

さらに、様々な画像処理プラグインは、PHP の imagick、Ruby の rmagick と paperclip、Node.js の imagemagick など、ImageMagick ライブラリに依存します。

ImageMagick または影響を受けるライブラリを使用する場合は、以下のタスクのどちらか（できれば両方）を実行して、既知の脆弱性を緩和することをお勧めします。

1. すべての画像ファイルが期待どおりの長さで始まっていることを確認します。 [&quot;マジックバイト&quot;](https://en.wikipedia.org/wiki/List_of_file_signatures) ImageMagick に送信して処理する前にサポートする画像ファイルタイプに対応します。
1. ポリシーファイルを使用して、脆弱な ImageMagick コーダーを無効にします。 ImageMagick のグローバルポリシーは、次の場所にあります。 `/etc/ImageMagick`.

>[!MORELIKETHIS]
>
>* [を使用して様々なファイル形式を処理するためのベストプラクティス [!DNL Assets]](assets-file-format-best-practices.md)
>* [ImageMagick のコマンドラインオプション](https://www.imagemagick.org/script/command-line-options.php)
>* [ImageMagick の基本的な使用例と高度な使用例](https://www.imagemagick.org/Usage/)
>* [ImageMagick 向けの Assets パフォーマンスチューニング](performance-tuning-guidelines.md)
>* [でサポートされているファイル形式の完全なリスト [!DNL Assets]](assets-formats.md)
>* [画像のファイル形式とメモリコストの理解](https://www.scantips.com/basics1d.html)

