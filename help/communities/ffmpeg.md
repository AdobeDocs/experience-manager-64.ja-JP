---
title: コミュニティのための FFmpeg
seo-title: FFmpeg for Communities
description: コミュニティ用の FFmpeg のインストールと設定の方法
seo-description: How to install and configure FFmpeg for Communities
uuid: ef2f821c-70e9-4889-a8d7-a93b10a1d428
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 739ec991-552b-42cd-85cd-984d1c9fe8fd
role: Admin
exl-id: 9ed54ee3-3509-4a43-a710-90f4543ccaf3
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 5%

---

# コミュニティのための FFmpeg {#ffmpeg-for-communities}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

FFmpeg は、オーディオとビデオの変換とストリーミングを行うソリューションで、インストール時に、 [ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video) と AEM Communities のイネーブルメント機能を使用します。

FFmpeg は、オーサー環境でアップロードされたイネーブルメントリソースのメタデータを取得し、イネーブルメントリソースのリストに表示するサムネールを生成するために使用されます。

## FFmpeg のインストール {#installing-ffmpeg}

AEMをホストするサーバーに FFmpeg をインストールする必要があります *作成者* インスタンス。

1. に移動します。 [https://www.ffmpeg.org](https://www.ffmpeg.org/)
1. お使いの環境（Macintosh、Windows または Linux）向けの最新バージョンの FFmpeg をダウンロードします。

   * FFmpeg を最新の状態に保つことが重要です。古いバージョンのセキュリティの脆弱性が原因です。

1. OS の手順に従って FFmpeg をインストールします。

1. FFmpeg 実行可能ファイルがシステムパスに設定されていることを確認します。

   システム内の任意のディレクトリから FFmpeg を実行できるはずです。

   * 例：`ffmpeg -version`

## FFmpeg トランスコーディングサービスを設定 {#configure-ffmpeg-transcoding-service}

デフォルトでは、FFmpeg がインストールされている場合、DAM アセットの更新ワークフロー定義に従って、複数のレンディションが設定（トランスコーディング）されます。

トランスコーディングは CPU を大量に消費するので、ターゲットレンディションのリストを変更することをお勧めします。 ほとんどの場合、トランスコードは必要ありません。

DAM アセットの更新ワークフローを変更し、この例でトランスコードをオフにするには、次の手順を実行します。

* 管理者権限でオーサーインスタンスにサインイン
* グローバルナビゲーションから： **[!UICONTROL ツール/ワークフロー/モデル]**
* 場所 **[!UICONTROL DAM アセットの更新]**
* ダブルクリックして、編集用のワークフローをクラシック UI で開きます

   結果の場所： [http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html](http://localhost:4502/cf#/etc/workflow/models/dam/update_asset.html)

* 次をダブルクリックします。 **[!UICONTROL FFmpeg トランスコード]** ステップのプロパティダイアログにアクセスする手順
* 以下 **[!UICONTROL プロセス]** タブ：

   * **[!UICONTROL アルグメント]**:すべてのエントリをクリアしてトランスコードを無効にします。デフォルト値： `profile:firefoxhq,profile:hq,profile:flv,profile:iehq`

![chlimage_1-372](assets/chlimage_1-372.png)

* 選択 **[!UICONTROL OK]** 閉じる `Step Properties` ダイアログ

* 選択 **[!UICONTROL 保存]** 保存する `DAM Update Asset` ワークフロー

   （左上隅）
