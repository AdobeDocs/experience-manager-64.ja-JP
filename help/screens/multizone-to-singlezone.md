---
title: マルチゾーンからシングルゾーンテイクオーバーループ
seo-title: マルチゾーンからシングルゾーンテイクオーバーループ
description: 'このページでは、AEM Screensプロジェクトのマルチゾーンからシングルゾーンへのテイクオーバーループについて説明します。  '
seo-description: 'AEM Screensプロジェクトでのマルチゾーンからシングルゾーンテイクオーバーループ。  '
translation-type: tm+mt
source-git-commit: 4b2c0f3a1ef8759eb3182b93cffa09c4afc23b6a

---


# マルチゾーンからシングルゾーンテイクオーバーループ{#single-zoneto-multizone}

## 使用例の説明 {#use-case-description}

ここでは、単一のゾーンレイアウトチャネルと切り替わるマルチゾーンレイアウトチャネルの設定方法を強調する使用例について説明します。 各チャネルは、画像/ビデオアセットを順に持つ。

### 前提条件 {#preconditions}

この使用例を開始する前に、以下をおこなう方法を理解しておく必要があります。

* **[チャネルの作成と管理](/help/screens/managing-channels.md)**
* **[ロケーションの作成と管理](/help/screens/managing-locations.md)**
* **[スケジュールの作成と管理](/help/screens/managing-schedules.md)**
* **[デバイスの登録](/help/screens/device-registration.md)**

### 主要なアクター {#primary-actors}

コンテンツ作成者

## プロジェクトのセットアップ {#setting-up-the-project}

次の手順に従って、プロジェクトをセットアップします。

1. **TakeoverLoop** という名前の AEM Screens プロジェクトを作成します（下図を参照）。

   >[!NOTE]
   >
   >To learn more about creating and managing projects in AEM Screens, refer to [Creating a Project](/help/screens/creating-a-screens-project.md).

   ![](assets/takeover-loop1.png)

1. **分割画面チャネルの作成**

   1. **チャネル**&#x200B;フォルダーを選択し、アクションバーの「**作成**」をクリックしてチャネル作成用ウィザードを開きます。
   1. ウィザードで「**左 L バー型分割画面チャネル**」を選択し、**MultiZoneLayout** というタイトルのチャネルを作成します。

      ![](assets/takeover-loop2.png)

   1. Select the **MultiZoneLayout** channel and click **Edit** from the action bar to open the editor. 各ゾーンにアセットをドラッグ＆ドロップします。次の例は、以下に示すように、チャネル内のビデオ、画像、およびテキストバナーを示しています。
      ![screen_shot_2019-02-21at35932pm](assets/SZtoMZ3.png)

1. **4つの画像を使用した2 X 2チャネルの作成**

   1. **チャネル**&#x200B;フォルダーを選択し、アクションバーの「**作成**」をクリックしてチャネル作成用ウィザードを開きます。

   1. Select **2X2 Split Screen Channel** template from the wizard and create the channel titled as **TwobyTwoChannel**.

      ![screen_shot_2019-02-21at35932pm](assets/SZtoMZ4.png)
   1. チャンネルを選択し、アクシ **ョンバーで** 「編集」をクリックしてエディターを開き、次に示すように4つの画像（4つの異なるゾーン）をそのチャンネルにドラッグ&amp;ドロップします。
      ![screen_shot_2019-02-21at35932pm](assets/SZtoMZ5.png)

1. **2つの画像を使用した1 X 2分割画面チャネルの作成**

   1. **チャネル**&#x200B;フォルダーを選択し、アクションバーの「**作成**」をクリックしてチャネル作成用ウィザードを開きます。

   1. Select **1X2 Split Screen Channel** template from the wizard and create the channel titled as **OnebyTwoChannel**.

      ![screen_shot_2019-02-21at35932pm](assets/SZtoMZ6.png)
   1. チャンネルを選択し、アクシ **ョンバーで** 「編集」をクリックしてエディターを開き、次に示すように、2つの画像（2つの異なるゾーン）をそのチャンネルにドラッグ&amp;ドロップします。
      ![screen_shot_2019-02-21at35932pm](assets/SZtoMZ7.png)

1. **1つのフルスクリーンビデオでのチャネルの作成**

   1. **チャネル**&#x200B;フォルダーを選択し、アクションバーの「**作成**」をクリックしてチャネル作成用ウィザードを開きます。

   1. Select **Sequence Channel** template from the wizard and create the channel titled as **FullScreensVideo**.

      ![screen_shot_2019-02-21at35932pm](assets/SZtoMZ8.png)
   1. チャンネルを選択し、アクショ **ンバーで** 「編集」をクリックしてエディターを開き、ビデオコンポーネントをそのチャンネルにドラッグ&amp;ドロップし、次に示すように目的のビデオを追加します。
      ![screen_shot_2019-02-21at35932pm](assets/SZtoMZ9.png)