---
title: コミュニティのための FFmpeg
seo-title: コミュニティのための FFmpeg
description: コミュニティのための FFmpeg をインストールおよび設定する方法
seo-description: コミュニティのための FFmpeg をインストールおよび設定する方法
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Administrator
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 62%

---


# コミュニティのための FFmpeg {#ffmpeg-for-communities}

## 概要 {#overview}

FFmpeg は、オーディオとビデオの変換およびストリーミングのためのソリューションです。インストールすると、[ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video)の適切なトランスコーディングと AEM Communities のイネーブルメント 能に使用できます。

FFmpeg は、オーサー環境で、アップロードしたイネーブルメントリソースのメタデータを取得したり、イネーブルメントリソースの一覧に表示するサムネイルを生成するときに使用します。

## FFmpeg のインストール  {#installing-ffmpeg}

FFmpeg は AEM *オーサー*&#x200B;インスタンスをホストしているサーバーにインストールする必要があります。

1. [https://www.ffmpeg.org](https://www.ffmpeg.org/)に移動します。
1. 特定の環境用（Macintosh、Windows または Linux）の FFmpeg の最新バージョンをダウンロードします。

   * 古いバージョンにはセキュリティ脆弱性があるので、FFmpeg を最新の状態に保つことが重要です。

1. OS の手順に従って FFmpeg をインストールします。

1. システムパスにFmpeg実行可能ファイルが設定されていることを確認してください。

   システム内の任意のディレクトリからFFmpegを実行できるはずです。

   * 例：`ffmpeg -version`

## FFmpeg トランスコーディングサービスの設定 {#configure-ffmpeg-transcoding-service}

デフォルトでは、FFmpeg をインストールすると、DAM アセットの更新のワークフロー定義どおりに複数のレンディションが設定されます（トランスコーディング）。

トランスコーディングは CPU を集中的に使用するので、対象レンディションのリストを変更することを推奨します。ほとんどの場合、トランスコードは必要ありません。

DAM アセットの更新のワークフローを変更するには（この例ではトランスコーディングをオフにするには）、次のようにします。

* 管理者権限を持つ作成者インスタンスにサインインします
* グローバルナビゲーションから：**[!UICONTROL ツール/ワークフロー/モデル]**
* **[!UICONTROL DAM更新アセット]**&#x200B;を検索
* 重複を押しながらクリックすると、編集用のワークフローがクラシックUIで開きます

   結果の場所：[http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* **[!UICONTROL Fmpegトランスコード]**&#x200B;の手順を重複クリックして、手順のプロパティダイアログにアクセスします
* 「**[!UICONTROL プロセス]**」タブの下：

   * **[!UICONTROL 軍備]**:すべてのエントリを消去してトランスコードのデフォルト値を無効にします。  `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

![chlimage_1-372](assets/chlimage_1-372.png)

* 「**[!UICONTROL OK]**」を選択して`Step Properties`ダイアログを閉じます

* 「**[!UICONTROL 保存]**」を選択して`DAM Update Asset`ワークフローを保存します

   （左上隅）

