---
title: ジェスチャーのカスタマイズ
seo-title: Gesture customization
description: AEM Forms アプリケーションでジェスチャーをカスタマイズ
seo-description: Customize the gestures on your AEM Forms app
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 238410e0-1623-49dc-b2fc-b5b2d5fb362b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 37%

---

# ジェスチャーのカスタマイズ {#gesture-customization}

AEM Formsアプリのジェスチャーをカスタマイズして、アプリを個別に操作する方法を提供できます。 例えば、新しいジェスチャーを追加して、タスクや Startpoint を開いたり閉じたりできます。

## AEM Forms アプリケーションのジェスチャーをカスタマイズするには {#to-customize-gestures-in-aem-forms-app}

AEM Forms アプリケーションで、左スワイプは新しいタスクまたは Startpoint を開き、右スワイプは何もしません。次の例は、AEM Formsアプリで右スワイプジェスチャーを実行したときに新しいタスクまたは Startpoint を開く手順を示しています。

1. プロジェクトを開きます。

   * iOSの場合は、を開きます。 `Capture.xcodeproj` Xcode 内
   * Android の場合、Eclipse で Android プロジェクトを開きます。
   * Windows の場合は、を開きます。 `MWSWindows.sln` Visual Studio 内。

1. views フォルダーに移動し、 `task.js` ファイルを編集します。

   * Xcode で、 **Capture > www > wsmobile > js > runtime > views** フォルダー。
   * Eclipse で、 **assets > www > wsmobile > js > runtime > views** フォルダー。
   * Visual Studio で、 **MWSWindows > www > wsmobile > js > runtime > views** フォルダー。

   >[!NOTE]
   >
   >task.js ファイルには、タスクリストまたは Startpoint リストに表示されている各タスクまたは Startpoint に関連付けられた Backbone ビューが含まれています。

1. 内 `task.js` ファイルで、ビューの events プロパティを検索します。

   events プロパティは、次の形式の各エントリとマップされます。

   `"EventName Selector": "Function"`

   JavaScript イベントをトリガーする際の名前： `EventName`次で指定されたHTML要素に対して： `Selector`、 `Function`が呼び出されます。

1. 検索

   * &quot;tap .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;tap .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;tap .task-content&quot; :&quot;onTaskClick&quot;,

      &quot;tap .last_empty_div&quot; :&quot;onTaskClick&quot;,
   これを

   * &quot;swipe .taskContentArea&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .taskOpenArea&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .task-content&quot; :&quot;onTaskClick&quot;,

      &quot;swipe .last_empty_div&quot; :&quot;onTaskClick&quot;,


1. `task.js` ファイルを保存して閉じます。
1. AEM Forms アプリケーションをビルドし実行します。これで、左スワイプと右スワイプを使用してタスクを開くことができます。

同様に、さまざまな組み合わせのジェスチャー、HTML 要素、および関数に対して、他のビューで変更を行うことができます。
