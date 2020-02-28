---
title: アセットレベルのスケジュール設定
seo-title: アセットレベルのスケジュール設定
description: 'ここでは、プレーヤーのローカルタイムゾーンで予定時間枠にチャネル内の特定のアセットをアクティブにする方法について説明します。 '
seo-description: 'ここでは、プレーヤーのローカルタイムゾーンで予定時間枠にチャネル内の特定のアセットをアクティブにする方法について説明します。 '
uuid: b79d521b-19d4-47c8-a41a-148d7bbf6ac9
contentOwner: jsyal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
topic-tags: authoring
discoiquuid: da25cdc7-c814-493e-8d8e-b6191fee2831
noindex: true
translation-type: tm+mt
source-git-commit: 4b2c0f3a1ef8759eb3182b93cffa09c4afc23b6a

---


# アセットレベルのスケジュール設定 {#asset-level-scheduling}

ここでは、チャネルで使用されるアセットのアセットレベルのスケジュール設定について説明します。

この節では、以下のトピックについて説明します。

* 概要
* アセットレベルのスケジュール設定の使用
* アセット内の繰り返しの処理
* 複数アセットスケジュール設定

>[!CAUTION]
>
>この AEM Screens 機能は、AEM 6.3 機能パック 3 または AEM 6.4 Screens 機能パック 1 がインストールされている場合にのみ使用できます。
>
>この機能パックにアクセスするには、アドビサポートに連絡してアクセス権をリクエストする必要があります。アクセス権が付与されると、パッケージ共有から機能パックをダウンロードできるようになります。

## 概要 {#overview}

***アセットレベルのスケジュール設定***&#x200B;を使用すると、プレーヤーのローカルタイムゾーンで予定時間枠にチャネル内の特定のアセットをアクティブにすることができます。この機能は、画像、ビデオ、トランジション、ページ、埋め込みチャネル（動的または静的）に対して使用できます。

*例えば*、月曜日と水曜日のサービスタイム（午後 2 時～午後 5 時）にのみ特別なプロモーションを表示するとします。

この機能を使用すると、開始日時と終了日時だけでなく、繰り返しパターンも指定できます。

## アセットレベルのスケジュール設定の使用 {#using-asset-level-scheduling}

アセットレベルのスケジュール設定は、アセットのプロパティへのアクセス時に「**アクティブ化**」タブを設定しておこないます。

アセットレベルのスケジュール設定をおこなうには、以下の手順に従います。

1. 任意のチャネルを選択し、アクションバーの「**編集**」をクリックして、チャネル内のコンテンツを追加または編集します。

   ![screen_shot_2018-04-23at111422am](assets/screen_shot_2018-04-23at111422am.png)

   >[!NOTE]
   >
   >以下をおこなう方法について詳しくは、
   >
   >* プロジェクトを作成する方法：[新しいプロジェクトの作成](creating-a-screens-project.md)を参照してください。
   >* チャネルにコンテンツを作成して追加する方法：[チャネルの管理](managing-channels.md)を参照してください。


1. 「**編集**」をクリックしてチャネルエディターを開き、スケジュールを設定するアセットを選択します。

   ![screen_shot_2018-04-24at90434pm](assets/screen_shot_2018-04-24at90434pm.png)

1. アセットを選択し、左上の&#x200B;**設定**&#x200B;アイコンをクリックして、画像のプロパティを開きます。

   「**アクティブ化**」タブをクリックします。

   ![screen_shot_2018-04-23at112348am](assets/screen_shot_2018-04-23at112348am.png)

1. You can specify the date from the date picker from the **Active from** and **Active until** fields.

   If you select the** Active from** and **Active until** date and time, the asset will display and loop only between that start date/time and end date/time respectively.

   ![screen_shot_2018-04-23at113545am](assets/screen_shot_2018-04-23at113545am.png)

## アセット内の繰り返しの処理 {#handling-recurrence-in-assets}

必要に応じて、毎日、毎週または毎月、特定の間隔でアセットが繰り返されるようにスケジュールを設定することもできます。

例えば、金曜日の午後 1 時から午後 10 時までの間のみ、画像を表示するとします。「アクティブ化」タブを使用して、アセットの繰り返し間隔を希望どおり設定できます。

### アセットの繰り返しイベントの追加 {#adding-a-recurring-event-for-your-asset}

1. アセットを選択し、**設定**&#x200B;アイコンをクリックして、プロパティダイアログボックスを開きます。
1. 開始日時と終了日時を入力した後、Cron 形式または自然言語テキスト形式を使用して、繰り返しスケジュールを指定できます。

   Web で無料の Cron 形式生成ツールを検索し、それを使用して生成した Cron 形式を「**スケジュール**」にコピーして貼り付けることができます。特定の日時間隔でアセットが表示されるようになります。

   *または*、Cron 形式ではなく、自然言語テキスト形式（金曜日の「** 6:00 より後、18:00 より前」など）を使用して、タスクを実行することもできます。アセットを表示する「**スケジュール**」を、いずれかの形式のテキストで入力します。

## 複数アセットスケジュール設定 {#multi-asset-scheduling}

>[!CAUTION]
>
>**複数アセットスケジュール設定**&#x200B;機能は、AEM 6.3 機能パック 5 または AEM 6.4 機能パック 3 がインストールされている場合にのみ使用できます。

***複数アセットスケジュール設定***&#x200B;を使用すると、複数のアセットを選択し、選択したすべてのアセットに再生スケジュールを適用することができます。

### 前提条件 {#prerequisites}

複数アセットレベルのスケジュール設定をアセットに使用するには、シーケンスチャネルを含んだ AEM Screens プロジェクトを作成します。この機能の実装を次の使用例で示します。

* 「**MultiAssetDemo**」というタイトルの AEM Screens プロジェクトを作成する
* **MultiAssetChannel** というタイトルのチャネルを作成し、そのチャネルにコンテンツを追加します（下図を参照）。

![screen_shot_2018-12-21at70128am](assets/screen_shot_2018-12-21at70128am.png)

複数のアセットを選択し、それらの表示スケジュールを AEM Screens プロジェクトに設定するには、以下の手順に従います。

1. **MultiAssetChannel** を選択し、アクションバーの「**編集**」をクリックして、エディターを開きます。

   ![screen_shot_2018-12-21at70313am](assets/screen_shot_2018-12-21at70313am.png)

1. エディターで複数のアセットを選択し、「**アクティベーションを編集**」（左上のアイコン）をクリックします。

   ![screen_shot_2018-12-21at70550am](assets/screen_shot_2018-12-21at70550am.png)

1. Select the date and time in **Active from** and **Active until **from the **Component Activation** dialog box. スケジュールの選択が完了したら、チェックマークアイコンをクリックします。

   ![screen_shot_2018-12-17at20337pm](assets/screen_shot_2018-12-17at20337pm.png)

1. 「更新」をクリックして、複数アセットスケジュールが適用されるアセットを確認します。

   >[!NOTE]
   >
   >複数アセットスケジュールが設定されているアセットの右上隅にスケジュールアイコンが表示されます。

   ![screen_shot_2018-12-21at70722am](assets/screen_shot_2018-12-21at70722am.png)

