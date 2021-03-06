---
title: 'Workspace に表示されるカテゴリの管理 '
seo-title: Managing the categories displayed in Workspace
description: Workspace で、ユーザーが開始できるプロセスは、左側にあるナビゲーションウィンドウのカテゴリに表示されます。Workspace に表示されるこれらのカテゴリの管理方法について説明します。
seo-description: In Workspace, the processes that a user can start are displayed in categories in the left navigation pane. Learn how you can manage these categories displayed in Workspace.
uuid: c2a275f5-872e-467f-9f07-4b130631e8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 0d1536a2-10ac-4031-bd7f-264b02d0d75f
exl-id: 5a2bd0ea-2c5e-4e0c-aff1-dba06be6a5b7
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 96%

---

# Workspace に表示されるカテゴリの管理 {#managing-the-categories-displayed-in-workspace}

Workspace で、ユーザーが開始できるプロセスは、左側にあるナビゲーションウィンドウのカテゴリに表示されます。カテゴリは管理コンソールで設定できます。プロセスデザイナーのカテゴリは Workbench で設定できます。プロセスデザイナーがプロセスを作成する場合は、それらをカテゴリに割り当てます。

カテゴリ名を指定する際には、Workspace のナビゲーションウィンドウに適切に表示されるように名前を作成します。デフォルトでは、左側のナビゲーションウィンドウの幅は、210 ピクセル（約 24 文字）に固定されています。指定したカテゴリ名が長すぎて左側のナビゲーションウィンドウの固定幅に収まらない場合、名前の後ろの部分が切り捨てられます。完全な名前は、その上にマウスポインターを置いた場合にのみ表示されます。切り捨てられるカテゴリ名は作成しないようにしてください。以下に、適切な長さのカテゴリ名と切り捨てられるカテゴリ名の例を示します。

**適合するカテゴリ名：** 出席と休暇

**切り捨てられたカテゴリ名：** 出欠（米国）

Workspace では、通常、カテゴリ内のプロセスは、カードとして開始プロセスページに表示されます。通常、カテゴリの画面には 1 度に 6 つのカードを表示できます。他のカードを表示するには、スクロールする必要があります。スクロールするとプロセスを見つけにくくなるので、各カテゴリのプロセスの数を 6 つ、または解像度に応じて、スクロールせずに画面に表示できるプロセス数に制限してください。

AEM Forms データベースとして MySQL を使用している場合、管理コンソールでは拡張文字だけが異なる 2 つのカテゴリ名を区別することはできません。例えば、「abcde」という名前のカテゴリと「âbcdè」という名前のカテゴリを作成した場合、これら 2 つは同じと見なされます。

## カテゴリの追加 {#add-a-category}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／カテゴリの管理をクリックします。
1. 「追加」をクリックします。サブカテゴリを追加する場合は、カテゴリを選択し「追加」をクリックします。
1. 「名前」ボックスにカテゴリの名前を入力し、「説明」ボックスにカテゴリの説明を入力します。
1. 「追加」をクリックします。カテゴリがカテゴリの管理ページに表示されます。

   ***注意&#x200B;**：カテゴリを作成するときは、最大 5 階層まで追加できます。*

## カテゴリの編集 {#edit-a-category}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／カテゴリの管理をクリックします。
1. 編集するカテゴリを選択し、「編集」をクリックします。または、カテゴリをダブルクリックして編集することもできます。
1. 「名前」ボックスでカテゴリの名前を編集します。

## カテゴリの削除 {#remove-a-category}

削除できるのは、使用されていないカテゴリのみです。

1. 管理コンソールで、サービス／アプリケーションおよびサービス／カテゴリの管理をクリックします。
1. カテゴリの管理ページで、削除するカテゴリのチェックボックスを選択して、「削除」をクリックします。カテゴリが表示されなくなります。
