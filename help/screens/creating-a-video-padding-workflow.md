---
title: ビデオパディングワークフローの作成
seo-title: ビデオパディングワークフローの作成
description: ここでは、アセットのワークフローにおけるビデオパディングの作成について説明します。
seo-description: ここでは、アセットのワークフローにおけるビデオパディングの作成について説明します。
uuid: 23f06905-c149-4df1-a8d9-26f38c7c67bb
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
topic-tags: authoring
content-type: reference
discoiquuid: 11962188-3767-4d62-b94b-6853ae749836
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340

---


# ビデオパディングワークフローの作成{#creating-a-video-padding-workflow}

ここでは、以下のトピックについて説明します。

* **概要**
* **前提条件**
* **ビデオパディングワークフローの作成**
* **AEM Screens プロジェクトでのワークフローの使用**
* **ワークフローの出力の検証**

## 概要 {#overview}

次の使用例では、チャネルへのビデオ（例：1280 x 720）の配置が必要になります。このチャネルのディスプレイは 1920 x 1080 で、0x0（左上）にビデオが配置されます。ビデオは、引き伸ばしや変更を一切おこなわないでください。また、ビデオコンポーネントで「**カバー**」は使用しません。

ビデオは横がピクセル 1～1280、縦がピクセル 1～720 のオブジェクトとして表示され、チャンネルの残りの部分はデフォルトの色になります。

## 前提条件 {#prerequisites}

ビデオのワークフローを作成する前に、次の前提条件を満たしてください。

1. AEM インスタンスの&#x200B;**アセット**&#x200B;フォルダーにビデオをアップロードする
1. AEM Screens プロジェクト（例：**TestVideoRendition**）と、**VideoRendering** という名前のチャネルを作成します（下図を参照）。

![screen_shot_2018-10-17at85307pm](assets/screen_shot_2018-10-17at85307pm.png)

## ビデオパディングワークフローの作成 {#creating-a-video-padding-workflow2}

ビデオパディングワークフローを作成するには、ビデオのワークフローを作成したあと、同じワークフローを AEM Screens プロジェクトのチャネルでも使用する必要があります。

以下の手順に従って、ワークフローを作成して使用します。

1. ワークフローの作成
1. AEM Screens プロジェクトでのワークフローの使用

### ワークフローの作成 {#creating-a-workflow}

以下の手順に従って、ビデオのワークフローを作成します。

1. AEM インスタンスに移動し、サイドレールのハンマーアイコンをクリックします。**ワークフロー**／**モデル**&#x200B;を選択して、新しいモデルを作成します。

   ![screen_shot_2018-10-17at90025pm](assets/screen_shot_2018-10-17at90025pm.png)

1. **モデル**／**作成**／**モデルを作成**&#x200B;をクリックします。**ワークフローモデルを追加**&#x200B;で、「**タイトル**」（**VideoRendition**）と「**名前**」を入力します。「**完了**」をクリックして、ワークフローモデルを追加します。

   ![screen_shot_2018-10-17at90747pm](assets/screen_shot_2018-10-17at90747pm.png)

1. ワークフローモデルを作成したら、モデル（**VideoRendition**）を選択し、アクションバーの「**編集**」をクリックします。

   ![screen_shot_2018-10-17at91256pm](assets/screen_shot_2018-10-17at91256pm.png)

1. コマンドラインコンポーネントをワークフローにドラッグ＆ドロップします。

   ![screen_shot_2018-10-22at14846pm](assets/screen_shot_2018-10-22at14846pm.png)

1. **コマンドライン**&#x200B;コンポーネントを選択し、プロパティダイアログボックスを開きます。

   ![screen_shot_2018-10-17at95752pm](assets/screen_shot_2018-10-17at95752pm.png)

1. **コマンドライン - 手順のプロパティ**&#x200B;ダイアログボックスで、「**引数**」タブを選択してフィールドに入力します。

   「**MIME タイプ**」フィールドに形式（***video/mp4***）を入力し、ワークフローを開始するコマンド（/usr/local/Cellar/ffmpeg -i ${filename} -vf &quot;pad=1920:height=1080:x=0:y=0:color=black&quot; cq5dam.video.fullhd-hp.mp4）を「**コマンド**」フィールドに入力します。

   「**MIME タイプ**」と「**コマンド**」について詳しくは、以下の注記を参照してください。

   ![screen_shot_2018-10-18at105300am](assets/screen_shot_2018-10-18at105300am.png)

1. ワークフロー（**VideoRenditions**）を選択し、アクションバーの「**ワークフローを開始**」をクリックして、**ワークフローを実行**&#x200B;ダイアログボックスを開きます。

   ![screen_shot_2018-10-18at105335am](assets/screen_shot_2018-10-18at105335am.png)

1. 「**ペイロード**」でアセットのパス（***/content/dam/huseinpeyda-crossroads01_512kb 2.mp4***）を選択し、「タイトル」に「***RunVideo***」と入力して、「**実行**」をクリックします。

   ![screen_shot_2018-10-18at112043am](assets/screen_shot_2018-10-18at112043am.png)

### AEM Screens プロジェクトでのワークフローの使用 {#using-the-workflow-in-an-aem-screens-project}

以下の手順に従って、AEM Screens プロジェクトでワークフローを使用します。

1. AEM Screens プロジェクト（**TestVideoRendition**／**チャネル**／**VideoRendition**）に移動します。

   ![screen_shot_2018-10-17at100715pm](assets/screen_shot_2018-10-17at100715pm.png)

1. アクションバーの「**編集**」をクリックします。最初に&#x200B;**アセット**&#x200B;フォルダーにアップロードしたビデオをドラッグ＆ドロップします。

   ![screen_shot_2018-10-17at102806pm](assets/screen_shot_2018-10-17at102806pm.png)

1. ビデオをアップロードしたら、「**プレビュー**」をクリックして出力を表示します。

   ![screen_shot_2018-10-22at15151pm](assets/screen_shot_2018-10-22at15151pm.png)

## ワークフローの出力の検証 {#validating-the-output-for-the-workflow}

出力は、次のいずれかの方法で検証できます。

* チャネル内のビデオのプレビューを確認する
* CRXDE Lite で ***/content/dam/testvideo.mp4/jcr:content/renditions/cq5dam.video.fullhd-hp.mp4*** に移動する（下図を参照）

![screen_shot_2018-10-22at14326pm](assets/screen_shot_2018-10-22at14326pm.png)

