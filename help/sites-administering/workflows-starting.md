---
title: ワークフローの開始
seo-title: Starting Workflows
description: AEMでワークフローを開始する方法を説明します。
seo-description: Learn how to start Workflows in AEM.
uuid: 0648d335-ecce-459d-95fd-3d4d76181b32
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: e9ab4796-a050-40de-b073-af7d33cff009
exl-id: 39419e0e-ad37-4ca5-8205-c29fc2cd1474
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 56%

---

# ワークフローの開始{#starting-workflows}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ワークフローを管理する場合、次の様々な方法でワークフローを開始できます。

* 手動:

   * から [ワークフローモデル](#workflow-models).
   * 次のワークフローパッケージの使用 [バッチ処理](#workflow-packages-for-batch-processing).

* 自動：

   * ノードの変更に応じて、 [ランチャーの使用](#workflows-launchers).

>[!NOTE]
>
>作成者は、他の方法も使用できます。詳しくは、以下を参照してください。
>
>* [ページへのワークフローの適用](/help/sites-authoring/workflows-applying.md)
>* [DAM アセットにワークフローを適用する方法](/help/assets/assets-workflow.md)
>* [AEM Forms](https://helpx.adobe.com/jp/aem-forms/6-2/aem-workflows-submit-process-form.html)
>* [翻訳プロジェクト](/help/sites-administering/tc-manage.md)
>


## ワークフローモデル {#workflow-models}

ワークフローを開始できます [モデルの 1 つに基づいて](/help/sites-administering/workflows.md#workflow-models-and-instances) ワークフローモデルコンソールに表示されます。 唯一の必須情報はペイロードですが、タイトルやコメントも追加できます。

## ワークフローランチャー {#workflows-launchers}

ワークフローランチャーは、変更されたノードの場所とリソースタイプに応じて、コンテンツリポジトリの変更を監視し、ワークフローを起動します。

**ランチャー**&#x200B;を使用すると、次の操作を実行できます。

* 特定のノードに対して既に起動されているワークフローを確認する。
* 特定のノード/ノードタイプが作成、変更、削除されたときに起動するワークフローを選択します。
* 既存のワークフローとノード間の関係を削除します。

ランチャーは任意のノードに対して作成できます。 ただし、特定のノードに対する変更では、ワークフローは開始されません。 次のパスの下のノードに対する変更は、ワークフローの起動には影響しません。

* `/var/workflow/instances`
* `/home/users` ブランチのいずれかにあるワークフローインボックスノード
* `/tmp`
* `/var/audit`
* `/var/classes`
* `/var/eventing`
* `/var/linkchecker`
* `/var/mobile`
* `/var/statistics`

   * 例外：`/var/statistics/tracking` 以下のノードに変更を加えると、ワークフローが起動&#x200B;*します*。

標準のインストールには、様々な定義が含まれています。 これらは、デジタルアセット管理およびソーシャルコラボレーションタスクに使用されます。

![wf-100](assets/wf-100.png)

## バッチ処理用のワークフローパッケージ {#workflow-packages-for-batch-processing}

ワークフローパッケージは、処理のペイロードとしてワークフローに渡すことができるパッケージで、複数のリソースを処理できます。

ワークフローパッケージ：

* には、一連のリソース（ページ、アセットなど）へのリンクが含まれています。
* には、作成日、パッケージを作成したユーザー、簡単な説明などのパッケージ情報が格納されます。
* は、専用のページテンプレートを使用して定義されます。このようなページを使用すると、ユーザーはパッケージ内のリソースを指定できます。
* は複数回使用できます。
* は、ワークフローインスタンスが実際に実行されている間に、ユーザーが変更（リソースの追加または削除）できます。

## モデルコンソールからのワークフローの開始 {#starting-a-workflow-from-the-models-console}

1. **ツール**／**ワークフロー**／**モデル**&#x200B;の順に移動して&#x200B;**モデル** コンソールにアクセスします。
1. （コンソールの表示に従って）ワークフローを選択します。必要に応じて、「検索」（左上）を使用することもできます。

   ![wf-103](assets/wf-103.png)

   >[!NOTE]
   >
   >**[一時的な](/help/sites-developing/workflows.md#transient-workflows)**&#x200B;インジケーターは、ワークフローの履歴が保持されないワークフローを示します。

1. ツールバーの「**ワークフローを開始**」を選択します。
1. ワークフローを実行ダイアログが開き、次の内容を指定できます。

   * **ペイロード**

      ページ、ノード、アセットなどのリソースを指定できます。

   * **タイトル**

      このインスタンスを特定するためのオプションのタイトル。

   * **コメント**

      このインスタンスの詳細を特定するために役立つオプションのコメント。
   ![wf-104](assets/wf-104.png)

## ランチャー設定の作成 {#creating-a-launcher-configuration}

1. **ツール**／**ワークフロー**／**ランチャー**&#x200B;の順に移動して&#x200B;**ワークフローランチャー**&#x200B;コンソールにアクセスします。
1. 「**作成**」を選択してから「**ランチャーを追加**」を選択し、ダイアログを開きます。

   ![wf-105](assets/wf-105.png)

   * **イベントタイプ**

      ワークフローを起動するイベントタイプ。

      * 作成日
      * 変更
      * 削除済み
   * **Notetype**

      ワークフローランチャーが適用されるノードの種類。

   * **パス**

      ワークフローランチャーが適用されるパス。

   * **実行モード**

      ワークフローランチャーが適用されるサーバーの種類。**オーサー**、**パブリッシュ**&#x200B;または&#x200B;**オーサーとパブリッシュ**&#x200B;を選択します。

   * **条件**

      評価時にワークフローを起動するかどうかを決定するノード値の条件のリスト。例えば、次の条件では、ノードの 1 つのプロパティ名に「User」の値が含まれる場合、ワークフローが起動されます。

      name==User

   * **機能**

      有効にする機能のリスト。ドロップダウンセレクターを使用して、必要な機能を選択します。

   * **無効にされた機能**

   無効にする機能のリスト。ドロップダウンセレクターを使用して、必要な機能を選択します。

   * **ワークフローモデル**

      「イベントタイプ」が、「ノードタイプ」または「パス」（あるいはその両方）において、定義された「条件」の下で発生した場合に起動されるワークフロー。

   * **説明**

      ランチャー設定について説明し、識別するための自身で入力するテキスト。

   * **アクティベート**

      ワークフローランチャーをアクティベートするかどうかを制御します。

      * 選択 **有効にする** 設定プロパティが満たされたときにワークフローを起動する。
      * 選択 **無効にする** の場合（設定プロパティが満たされた場合でも）、ワークフローを実行しない場合。
   * **リストを除外**

      ワークフローを実行するかどうかを決定する際に除外（無視）するすべての JCR イベントを指定します。

      このランチャープロパティは、次のような項目のコンマ区切りリストです。

      * `property-name` は、指定したプロパティ名に対して実行されたすべての `jcr` イベントを無視します。
      * `event-user-data:<*someValue*>` は、`*<someValue*`  API で設定した `user-data`> [`ObservationManager` を含むすべてのイベントを無視します。](https://www.adobe.io/experience-manager/reference-materials/spec/jsr170/javadocs/jcr-2.0/javax/jcr/observation/ObservationManager.html#setUserData(java.lang.String

      次に例を示します。

      `jcr:lastModified,dc:modified,dc:format,jcr:lastModifiedBy,imageMap,event-user-data:changedByWorkflowProcess`

      この機能を使用して、除外項目を追加することで、別のワークフロープロセスによってトリガーされた変更を無視することができます。

      `event-user-data:changedByWorkflowProcess`





1. 「**作成**」を選択し、ランチャーを作成してコンソールに戻ります。

   適切なイベントが発生すると、ランチャーがトリガーされ、ワークフローが開始します。

## ランチャー設定の管理 {#managing-a-launcher-configuration}

ランチャー設定を作成したら、同じコンソールを使用してインスタンスを選択し、「**プロパティを表示**」を選択（および編集）するか、「**削除**」を選択します。
