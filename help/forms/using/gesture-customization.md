---
title: ジェスチャーのカスタマイズ
seo-title: Gesture customization
description: AEM Formsアプリでジェスチャーをカスタマイズする
seo-description: Customize the gestures on your AEM Forms app
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 238410e0-1623-49dc-b2fc-b5b2d5fb362b
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 75%

---

# ジェスチャーのカスタマイズ {#gesture-customization}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms アプリケーションのジェスチャーをカスタマイズして、アプリケーションを操作するための独自の方法を提供できます。例えば、タスクまたはスタートポイントを開いたり閉じたりするジェスチャーを新たに追加できます。

## AEM Formsアプリでジェスチャーをカスタマイズするには {#to-customize-gestures-in-aem-forms-app}

AEM Formsアプリでは、左スワイプは新しいタスクまたは Startpoint を開き、右スワイプは何もしません。 次の例では、AEM Forms アプリケーションで右スワイプジェスチャーを実行したときに新しいタスクまたはスタートポイントを開くための手順を示しています。

1. プロジェクトを開きます。

   * iOS の場合、Xcode で `Capture.xcodeproj` を開きます。
   * Android の場合、Eclipse で Android プロジェクトを開きます。
   * Windows の場合、Visual Studio で `MWSWindows.sln` を開きます。

1. views フォルダーに移動し、`task.js` ファイルを編集用に開きます。

   * Xcode では、**Capture／www／wsmobile／js／runtime／views** フォルダーに移動します。
   * Eclipse では、**assets／www／wsmobile／js／runtime／views** フォルダーに移動します。
   * Visual Studio では、**MWSWindows／www／wsmobile／js／runtime／views** フォルダーに移動します。

   >[!NOTE]
   >
   >task.js ファイルには、タスクリストまたは Startpoint リストに表示されている各タスクまたは Startpoint に関連付けられた Backbone ビューが含まれています。

1. `task.js` ファイルで、ビューのイベントプロパティを検索します。

   イベントプロパティは、各エントリが次の形式で指定されたマップです。

   `"EventName Selector": "Function"`

   `Selector` で指定された HTML 要素で `EventName` という名前の Javascript イベントをトリガーすると、`Function` が呼び出されます。

1. 検索

   * &quot;tap .taskContentArea&quot; : &quot;onTaskClick&quot;、

      &quot;tap .taskOpenArea&quot; : &quot;onTaskClick&quot;、

      &quot;tap .task-content&quot; : &quot;onTaskClick&quot;、

      &quot;tap .last_empty_div&quot; : &quot;onTaskClick&quot;、
   これを

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;、

      &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;、

      &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;、

      &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;、


1. `task.js` ファイルを保存して閉じます。
1. AEM Formsアプリをビルドして実行します。 これで、左スワイプと右スワイプを使用してを開くことができます。

同様に、さまざまな組み合わせのジェスチャー、HTML 要素、および関数に対して、他のビューで変更を行うことができます。
