---
title: 不在設定の指定
seo-title: Configuring Out of Office Settings
description: 「不在」機能を使用すると、ユーザーが不在となり、AEM forms によって割り当てられたタスクを完了できないタイミングを指定できます。
seo-description: The Out of Office feature enables you to specify when a user will be out of the office and unable to complete tasks assigned by AEM forms.
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
exl-id: 8787ffa9-9ddc-439d-9934-8913d1ed459e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 7%

---

# 不在設定の指定 {#configuring-out-of-office-settings}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

「不在」機能を使用すると、ユーザーまたは管理者は、ユーザーが不在になるタイミングを指定し、AEM forms によって割り当てられたタスクを完了できません。 ユーザーが「不在」に設定されている間、そのユーザーのタスクは 1 人以上の指定されたユーザーに割り当てられます。 ユーザーは Workspace で「不在」設定を変更できます。ユーザーの代わりに、管理者が Forms ワークフローで設定を変更することもできます。

Workbench ユーザーは、プロセスの作成時に、「不在」の設定によってタスクをリダイレクトできるかどうかを指定できます。

## ユーザーの不在情報の表示 {#view-a-user-s-out-of-office-information}

1. 管理コンソールで、サービス/Forms ワークフロー/不在をクリックします。
1. 不在ページの上部にあるボックスで、次のいずれかの操作を実行できます。

   **名前で検索**

   「名前で検索」オプションを選択します。 ユーザー名の全部または一部を入力し、「検索」をクリックします。 このフィールドを空白のままにすると、Formsワークフローはすべてのユーザーのリストを返します

   **日付範囲で検索**

   「日付範囲で検索」オプションを選択します。 検索結果を絞り込むために、開始日と終了日および目的のタイムスタンプを指定します。 「検索」をクリックします。

1. ユーザー名をクリックすると、ユーザーのリストの下にユーザーの不在情報が表示されます。

## ユーザーの不在ステータスの変更 {#change-a-user-s-out-of-office-status}

1. ユーザーを検索します。詳しくは、 [ユーザーの不在情報の表示](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. 変更するユーザーの名前をクリックします。
1. 次の *ユーザー名* 現在リストにある場合は、「不在」または「不在」を選択します。
1. 「保存」をクリックします。

## ユーザーの不在日付範囲の追加 {#add-an-out-of-office-date-range-for-a-user}

1. ユーザーを検索します。詳しくは、 [ユーザーの不在情報の表示](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. 変更するユーザーの名前をクリックします。
1. 「日付範囲を追加」をクリックします。
1. 「開始時間」と「終了時間」を入力します。 カレンダーアイコンをクリックして日付を選択できます。 終了時間を指定しない場合、ユーザーは無期限に不在と設定されます。
1. 「保存」をクリックします。

## 不在タスクにユーザーを割り当てる {#assign-a-user-for-out-of-office-tasks}

ユーザーが不在の間、1 人以上のユーザーを割り当てて、ユーザーに新しいタスクを実行できます。 次の設定を行うことができます。

* すべての新しいタスクを指定されたデフォルトユーザーに割り当てます。
* タスクを再割り当てしない。 新しいタスクは、不在のユーザーに割り当てられたままになります。
* ユーザーのタスクのほとんどを受け取るデフォルトのユーザーを割り当てますが、特定のプロセスのタスクを他のユーザーに再割り当てするか、不在のユーザーに割り当てたままにするように指定します。
* デフォルトユーザーを割り当てずに、特定のプロセスの特定のタスクを特定のユーザーに割り当てます。

   1. ユーザーを検索します。詳しくは、 [ユーザーの不在情報の表示](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. 変更するユーザーの名前をクリックします。
   1. [ 不在時のタスクの既定のユーザー ] の一覧からユーザーを選択します。 既定のユーザーが再割り当てされた項目を受け取るように指定しない場合は、「割り当てなし」を選択します。

      適切なユーザー名がリストに表示されない場合は、「ユーザーを検索」をクリックし、「ユーザーを検索」ダイアログ・ボックスを使用してユーザーを検索します。 リストから適切なユーザーを選択し、「ユーザーを選択」をクリックします。 [ ユーザの検索 ] ダイアログボックスの [ ユーザのスケジュールの表示 ] をクリックして、選択したユーザの不在スケジュールを表示することもできます。

   1. デフォルトのユーザーに送信するべきでないプロセスがある場合は、「例外の追加」をクリックし、プロセスを選択し、リストから別のユーザーを選択します。 「割り当てなし」を選択して、不在のユーザーにタスクを割り当てたままにすることもできます。
   1. 「保存」をクリックします。
