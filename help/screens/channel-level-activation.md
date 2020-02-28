---
title: チャネルレベルのアクティブ化 - 単一イベント再生
seo-title: チャネルレベルのアクティブ化 - 単一イベント再生
description: ここでは、単一イベント再生を使用したチャネルレベルのアクティブ化について説明します。
seo-description: ここでは、単一イベント再生を使用したチャネルレベルのアクティブ化について説明します。
uuid: 87230344-5f9a-42a4-a7a8-ae4203303612
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/6.4/SCREENS
topic-tags: authoring
content-type: reference
discoiquuid: c28fd669-f23e-4d53-bec1-a2911274567d
noindex: true
translation-type: tm+mt
source-git-commit: 3addef2141ebb831f8677d011d68faf88e648dc2

---


# チャネルレベルのアクティブ化 - 単一イベント再生{#channel-level-activation-single-event-playback}

ここでは、以下のトピックについて説明します。

* **[概要](/help/screens/channel-level-activation.md#overview)**
* **[チャネルレベルのアクティブ化を単一イベント再生として使用する方法](/help/screens/channel-level-activation.md#using-channel-level-activation)**

   * **[前提条件](/help/screens/channel-level-activation.md#prerequisites)**
   * **[実装](/help/screens/channel-level-activation.md#implementation)**

* **[結果の表示](/help/screens/channel-level-activation.md#viewing-the-results)**

## 概要 {#overview}

***チャネルレベルのアクティブ化***&#x200B;を使用すると、設定された特定のスケジュールに従ってチャネルを切り替えることができます。設定されたスケジュールに従って単一イベントチャネルがメインチャネルの代わりに再生され、メインチャネルが再びコンテンツを再生するようになるまで、特定の時間だけ再生されます。

以下の例では、次のキーワードに的を絞ったソリューションを示しています。

* グローバルシーケンス用の&#x200B;***メインシーケンスチャネル***
* 設定された時刻に 1 回だけ動作する&#x200B;***単一イベントチャネル***
* メインシーケンスチャネル内で発生する単一再生イベントに&#x200B;***設定されるスケジュールと優先度***

## チャネルレベルのアクティブ化の使用 {#using-channel-level-activation}

次の節では、AEM Screens プロジェクトのチャネルに含まれる単一イベント再生の作成について説明します。

### 前提条件 {#prerequisites}

この機能の実装を開始する前に、次の前提条件を満たしていることを確認してください。

* Create an AEM Screens project (in this example, **Channel Level Activation**)

* **チャネル**&#x200B;フォルダーの下に **MainAdChannel** というチャネルを作成する

* **チャネル** フォルダーの下に **TargetedSinglePlay** という別のチャネルを作成する

* 両方のチャネルに関連アセットを追加する

次の画像は、**チャネル**&#x200B;フォルダーに **MainAdChannel** チャネルと **TargetedSinglePlay** チャネルを含む **チャネルレベルのアクティブ化** プロジェクトを示しています。

![screen_shot_2018-11-27at104500am](assets/screen_shot_2018-11-27at104500am.png)

>[!NOTE]
>
>プロジェクトの作成方法とシーケンスチャネルの作成方法について詳しくは、以下のリソースを参照してください。
>
>* [プロジェクトの作成と管理](/help/screens/creating-a-screens-project.md)
   >
   >
* [チャネルの管理](/help/screens/managing-channels.md)
>



### 実装 {#implementation}

AEM Screens プロジェクトにチャネルレベルのアクティブ化を実装するには、主に次の 3 つのタスクが必要になります。

1. **チャネル、ロケーション、ディスプレイなどのプロジェクト分類のセットアップ**
1. **ディスプレイへのチャネルの割り当て**
1. **スケジュールと優先度のセットアップ**

この機能を実装するには、以下の手順に従います。

1. **ロケーションを作成する**

   AEM Screens プロジェクトの「**ロケーション**」フォルダーに移動し、「**地域**」としてロケーションを作成します。

   ![screen_shot_2018-11-27at112112am](assets/screen_shot_2018-11-27at112112am.png)

   >[!NOTE]
   >
   >ロケーションの作成方法については、**[ロケーションの作成と管理](/help/screens/managing-locations.md)**を参照してください。

1. **ロケーションにディスプレイを作成する**

   1. **チャネルレベルのアクティブ化**／**ロケーション**／**地域**&#x200B;に移動します。
   1. 「**地域**」を選択し、アクションバーの「**+ 作成**」をクリックします。
   1. ウィザードで「**ディスプレイ**」を選択し、「**RegionDisplay**」というタイトルのディスプレイを作成します。
   ![screen_shot_2018-11-27at112216am](assets/screen_shot_2018-11-27at112216am.png)

1. **ディスプレイにチャネルを割り当てる**

   **MainAdChannel** の場合は次の手順に従います。

   1. **チャネルレベルのアクティブ化**／**ロケーション**／**地域**／**RegionDisplay** に移動し、アクションバーの「**チャネルを割り当て**」をクリックします。
   1. **チャネル割り当て**&#x200B;ダイアログボックスが開きます。
   1. 「**チャネルを参照...**」で「パス別」を選択します。
   1. Select the **Channel Path** as **Channel Level Activation** --> ***Channels*** --> ***MainAdChannel***.
   1. 「**チャネルロール**」は **mainadchannel** に設定します。
   1. 「**優先度**」で「**1**」を選択します。
   1. 「**サポートされているイベント**」で「**最初の読み込み**」および「**待機中画面**」を選択します。
   1. 「**保存**」をクリックします。
   ![screen_shot_2018-11-27at124626pm](assets/screen_shot_2018-11-27at124626pm.png)

   >[!NOTE]
   >
   >ディスプレイダッシュボードからチャネルを割り当てることもできます。それには、**チャネルレベルのアクティブ化**／**ロケーション**／**地域**／**RegionDisplay** に移動し、アクションバーの「**ダッシュボード**」をクリックします。**割り当てられたチャネルとスケジュール**&#x200B;パネルで「**+ チャネルを割り当て**」をクリックします。

   同様に、**TargetedSinglePlay** チャネルを次の手順でディスプレイに割り当てます。

   1. **チャネルレベルのアクティブ化**／**ロケーション**／**地域**／**RegionDisplay** に移動し、アクションバーの「**チャネルを割り当て**」をクリックします。
   1. **チャネル割り当て**&#x200B;ダイアログボックスが開きます。
   1. 「**チャネルを参照...**」で「パス別」を選択します。
   1. Select the **Channel Path** as **Channel Level Activation*** --> ***Channels*** --> ***TargetedSinglePlay***.*
   1. 「**チャネルロール**」は **targetedsingleplay** に設定します。
   1. 「**優先度**」を「**2**」に設定します。
   1. Select the **Supported Events** as **Initial Load**, **Idle Screen** and **Timer***, *as shown in the figure below.
   1. Choose the date in **active from** as November 27, 2018 11:59 pm and in **active until** as November 28, 2018 12:05 am.*
*
   1. Click **Save**.*
*
   >[!CAUTION]
   **TargetedSinglePlay** チャネルの優先度を **MainAdSegment** チャネルよりも高く設定する必要があります。

   ![screen_shot_2018-11-27at31206pm](assets/screen_shot_2018-11-27at31206pm.png)

   >[!NOTE]
   同じ日を選択するには、翌日を選択し、手動で同じ日付に編集する必要があります。ただし、時刻は後になるようにします。これにより、ユーザーが過去の日付を選択できないようになります。以下の例を参照してください。

   ![new1](assets/new1.gif)

## 結果の表示 {#viewing-the-results}

チャネルとディスプレイのセットアップが完了したら、AEM Screens Player を起動してコンテンツを表示してください。

プレイヤーに **MainAdChannel** チャネルのコンテンツが表示され、（スケジュールで設定したとおりに）午後 11 時 59 分になると **TargetedSinglePlay** チャネルのコンテンツが 午前 12 時 5 分まで表示されます。その後は、**MainAdChannel** のコンテンツの再生が再開されます。

>[!NOTE]
AEM Screens Player については、次のリソースを参照してください。
* [**AEM Screens Player のダウンロード&#x200B;**](https://download.macromedia.com/screens/)
* [**AEM Screens Player での作業&#x200B;**](/help/screens/working-with-screens-player.md)



