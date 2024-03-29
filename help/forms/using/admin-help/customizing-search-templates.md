---
title: 検索テンプレートのカスタマイズ
seo-title: Customizing search templates
description: Workspace で使用する検索テンプレートを作成して、タスクページと追跡ページからプロセスのインスタンスを検索できます。 また、既存の検索テンプレートを編集または削除することもできます。
seo-description: You can create search templates to be used in Workspace to search for instances of processes from the To Do and Tracking pages. You can also edit or delete existing search templates.
uuid: 2043ba8a-07f0-4054-af3c-f3a14c2183ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 6e4b4dfa-3af5-4c21-a2a1-b90ef02d8514
exl-id: 5230222b-53f8-414c-aaa1-848d6e9369e8
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 16%

---

# 検索テンプレートのカスタマイズ {#customizing-search-templates}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Workspace で使用する検索テンプレートを作成して、タスクページと追跡ページからプロセスのインスタンスを検索できます。 また、既存の検索テンプレートを編集または削除することもできます。

検索テンプレートを作成または編集する際に、検索結果のレイアウトおよび並べ替え順を指定できます。 ただし、検索結果が表示された後で、ユーザーは Workspace でこれらの設定を変更できます。

検索テンプレートは必要な数だけ作成できます。

>[!NOTE]
>
>検索テンプレートを保存する際は、一意の名前を付ける必要があります。 そうしないと、警告メッセージを表示せずに既存のテンプレートを上書きできます。

## 単純な検索テンプレートの作成 {#create-a-simple-search-template}

1. 管理コンソールで、サービス/Workspace/検索テンプレートをクリックします。
1. 「ID」タブの「検索テンプレートの説明」ボックスで、テンプレートの目的を指定します。
1. （オプション）「条件」タブをクリックして、テンプレートの検索条件を指定します。
1. 「保存」タブをクリックし、テンプレートの一意の名前を入力して、「保存」をクリックします。

## 検索テンプレートの作成または編集 {#create-or-edit-a-search-template}

1. 管理コンソールで、サービス/Workspace/検索テンプレートをクリックします。
1. （オプション）既存のテンプレートを編集する場合、または既存のテンプレートを新しいテンプレートの基礎として使用する場合、「検索テンプレート名」リストからテンプレートを選択します。
1. 「検索テンプレートの説明」ボックスに、テンプレートの目的を入力します。
1. （オプション）「ユーザーの手順」ボックスに、テンプレートの使用に役立つ手順を入力します。 これらの手順は、ユーザーが検索テンプレートを選択すると Workspace に表示されます。
1. 「条件」タブをクリックします。 ここで、1 つ以上の検索条件を定義します。 検索条件を追加するには：

   * 「条件」タブの上部で、プロセス要素またはタスク要素を選択します。

      **ヒント**：*以前にプロセス名要素を選択し、プロセスを指定した場合、そのプロセスで定義したすべてのプロセス変数も選択できます。*

      **ヒント**：*表示タスク要素を選択すると、ユーザーは、検索結果から完了したタスクを削除できるようになります。*

      「条件」タブの下部に、選択した要素の検索条件フィールドが表示されます。

   * 選択した各プロセス要素、タスク要素およびプロセス変数に対して、「基準」タブの下部にある対応する検索フィールドに入力します。

      * 表示されるリストから関係演算子（「次と等しい」など）を選択し、その横のボックスでオペランドの値を指定します。
      * （オプション）Workspace でユーザーがオペランドの値を変更できるようにするには、「ユーザーに対してオペランドの変更を許可する」を選択します。
      * （オプション）ユーザーがリレーショナル演算子を変更できるようにするには、「ユーザーが別のリレーショナル演算子を選択できるようにします」を選択します。 表示されるリストで、ユーザーが使用できる演算子を選択します。

      **ヒント**：*要素としてプロセス名を選択した場合、オペランドフィールドの横にあるアイコンをクリックして、表示されるリストから Forms サーバーで実行しているプロセスを選択できます。プロセスを選択した後、「条件」タブの一番上の「プロセス変数」で、そのプロセスで定義したすべてのプロセス変数を選択できます。*

      **ヒント**：*要素の検索条件の横にある削除アイコンをクリックして、検索テンプレートから要素を削除できます。*


1. （オプション）列見出しを検索結果に表示するには、「レイアウト」タブをクリックし、次の手順を実行します。

   * プロセスまたはタスク要素を選択し、右向き矢印をクリックして、「レポート列」リストに移動します。
   * 「レポート列」リストで、プロセスまたはタスク要素を選択し、上向き矢印または下向き矢印をクリックして、列の順序内の位置に移動します。 検索結果の列見出しは、ここにリストされている順序で表示されます。
   * （オプション）列見出しの要素名を変更するには、「レポート列」リストから要素を選択し、新しい名前を指定します。

   >[!NOTE]
   >
   >検索テンプレートで指定されたレイアウトは、Workspace で列見出しに対して指定されたユーザーの環境設定よりも優先されます。

1. （オプション）検索結果を並べ替える列ごとに、「並べ替え」タブをクリックし、次の手順を実行します。

   * プロセスまたはタスクの要素を選択し、右向き矢印をクリックして、選択した要素を「ソート順序」リストに移動します。
   * 「並べ替え順」リストで、プロセスまたはタスクの要素を選択し、上向き矢印または下向き矢印をクリックして、並べ替え順での位置に移動します。 検索結果の列は、ここに表示される順序に基づいて並べ替えられます。
   * （オプション）列を降順に並べ替えるには、要素名の横にあるチェックボックスを選択します。 このチェックボックスがオフの場合、列は昇順で並べ替えられます。

1. 「保存」タブをクリックします。
1. （オプション）新しい検索テンプレートを作成する場合は、一意の名前を付けます。 一意の名前を指定しない場合、既存のテンプレートを上書きする可能性があります。
1. 「保存」ボタンをクリックします。

## 検索テンプレートの削除 {#delete-a-search-template}

1. 「ID」タブで、「検索テンプレート名」リストから名前を選択します。
1. 「このテンプレートを削除」をクリックし、「OK」をクリックします。
