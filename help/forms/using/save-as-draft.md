---
title: タスクまたはフォームをドラフトとして保存する
seo-title: Saving a task or form as a draft
description: AEM Forms アプリケーションでタスクまたはフォームのドラフトコピーを保存する手順
seo-description: Steps to save a draft copy of a task or a form in the AEM Forms app
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
exl-id: c21cddb3-d12d-4e1b-bd62-cf75946569be
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 79%

---

# タスクまたはフォームをドラフトとして保存する {#saving-a-task-or-form-as-a-draft}

「ドラフトとして保存」オプションでは、関連フォームに記入済みのデータとともに、タスクまたはフォームのスナップショットが保存されます。テンプレートからドラフトを作成することもできます。ドラフトはモバイルデバイスに保存され、今後取得できるように Adobe Experience Manager Forms サーバーと同期されます。

以下が可能です。 [フォームを更新](/help/forms/using/working-with-form.md), [注釈を付ける](/help/forms/using/add-attachments.md) 写真と手書きメモと フォームの更新を続ける際は、ドラフトとして保存することをお勧めします。記入したフォームを後で送信する場合は、ドラフトとして保存しておくと便利です。

フォームポータルに保存されたフォームの「ドラフトとして保存」機能を有効にするには、 [HTML5 フォームのドラフトとしての保存](/help/forms/using/saving-html5-form-draft.md).\
アダプティブフォームの送信を設定するには、 [ドラフトと送信コンポーネント](/help/forms/using/draft-submission-component.md). (AEM Forms JEE サーバーと同期されたフォームに対しては無効です )。

ドラフトを作成するには、フォームを開き、 **ドラフトとして保存** ![下書きとして保存](assets/save-as-draft.png). ドラフトの名前を入力して、「**保存**」をタップします。ドラフトは Drafts フォルダーに保存され、サーバーと同期されます。アプリケーションがオフラインの場合は、Outbox フォルダーに保存されます。

対応するフォームを後で更新した場合、変更内容はすぐに反映されます。AEM Forms アプリケーションを AEM Forms サーバーと同期すると、ドラフトが AEM Forms サーバーにアップロードされます。さらに、ドラフトは Outbox フォルダーから Tasks フォルダーか Drafts フォルダーに移動されます。その横には編集アイコンが表示されます。

複数のタスクやスタートポイントを使用しているときにタスクやスタートポイントを保存すると、ドラフトが保存されます。アプリケーションが AEM Forms サーバーと同期されるたびに、ドラフトがサーバー上に保存されます。これにより、最後に保存した日付と時刻のドラフトをいつでも回復できます。例えば、アプリケーションを再インストールするか、モバイルデバイスを変更する場合は、サーバーからドラフトをダウンロードできます。

## ドラフトの削除 {#delete-a-draft}

Drafts フォルダーにはすべてのドラフトが一覧表示されます。「ドラフトを削除」オプションを使用すると、ドラフトをモバイルデバイスとサーバーから完全に削除できます。

タスクから作成されたドラフトを削除するオプションは使用できません。タスクから作成されたドラフトを削除すると、タスクは中断されます。

ドラフトの破棄はオフラインモードとオンラインモードのいずれにおいても実行できます。オフラインモードでドラフトを破棄すると、サーバーとの接続が復元された後、ドラフトがサーバーから削除されます。

以下の手順を実行し、ドラフトを削除します。

1. AEM Formsアプリで、に移動します。 **Forms。**
1. 選択 **ドラフト** を選択します。
1. 編集アイコン付きのフォーム ![edit-draft-app](assets/edit-draft-app.png) 下書きを示します。 下書きの横にある横の省略記号をタップします。
1. 水平省略記号をタップして表示されたオプションの一覧から、「**ドラフトを削除**」をタップします。
