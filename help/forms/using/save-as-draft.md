---
title: タスクまたはフォームをドラフトとして保存する
seo-title: Saving a task or form as a draft
description: AEM Formsアプリケーションでタスクまたはフォームのドラフトコピーを保存する手順
seo-description: Steps to save a draft copy of a task or a form in the AEM Forms app
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
exl-id: c21cddb3-d12d-4e1b-bd62-cf75946569be
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 26%

---

# タスクまたはフォームをドラフトとして保存する {#saving-a-task-or-form-as-a-draft}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

「ドラフトとして保存」オプションでは、タスクまたはフォームのスナップショットと、関連するフォームに入力されたデータが保存されます。 また、テンプレートからドラフトを作成することもできます。 下書きはモバイルデバイスに保存され、後で取得できるようにAdobe Experience Manager Formsサーバーと同期されます。

[フォームの更新](/help/forms/using/working-with-form.md)や、写真および手書きメモを使用した[フォームの注釈付け](/help/forms/using/add-attachments.md)を行うことができます。フォームを更新し続ける際は、フォームをドラフトとして保存することをお勧めします。 後から入力済みのフォームを送信する場合は、ドラフトとして保存すると便利です。

フォームポータルで保存したフォームの「ドラフトとして保存」機能を有効にするには、[HTML5 フォームのドラフトでの保存](/help/forms/using/saving-html5-form-draft.md)を参照してください。
\
アダプティブフォームの送信を設定するには、[ドラフトと送信コンポーネント](/help/forms/using/draft-submission-component.md)を参照してください。（AEM Forms JEE サーバーと同期しているフォームでは無効になります。）

ドラフトを作成するには、フォームを開いて「**ドラフトとして保存** ![save-as-draft](assets/save-as-draft.png)」をタップします。下書きの名前を入力し、をタップします。 **保存**. 下書きは Drafts フォルダーに保存され、サーバーと同期されます。 アプリがオフラインの場合、送信トレイは送信トレイフォルダーに保存されます。

後で対応するフォームを更新すると、変更が直ちに反映されます。 AEM FormsアプリケーションをAEM Formsサーバーと同期すると、下書きがAEM Formsサーバーにアップロードされます。 さらに、下書きは Outbox フォルダーから Tasks フォルダーまたは Drafts フォルダーに移動されます。 横に編集アイコンが表示されます。

複数のタスクやスタートポイントを操作し、それらを保存し続けると、ドラフトが保存されます。 アプリがAEM Formsサーバーと同期されるたびに、ドラフトがサーバーに保存されます。 これにより、最後に保存した日時に基づいて、いつでも下書きを復元できます。 例えば、アプリを再インストールする場合やモバイルデバイスを変更する場合は、サーバーから下書きをダウンロードできます。

## 下書きの削除 {#delete-a-draft}

drafts フォルダーには、すべての下書きが一覧表示されます。 「下書きを削除」オプションを使用すると、下書きをモバイルデバイスおよびサーバーから完全に削除できます。

タスクから作成されたドラフトを削除するオプションは使用できません。 タスクから作成されたドラフトを削除すると、タスクは中止されます。

下書きは、オフラインモードとオンラインモードの両方で破棄できます。 オフラインモードで下書きを破棄すると、サーバーとの接続が復元された場合にのみ、下書きがサーバーから削除されます。

下書きを削除するには、次の手順を実行します。

1. AEM Forms アプリケーションで、「**Forms**」に移動します。
1. 「検索」の隣にあるドロップダウンから「**ドラフト**」を選択します。
1. フォームについている編集アイコン ![edit-draft-app](assets/edit-draft-app.png) は、そのフォームがドラフトであることを意味しています。ドラフトの横にある「...」をタップします。
1. 水平省略記号をタップして表示されたオプションの一覧から、「**ドラフトを削除**」をタップします。
