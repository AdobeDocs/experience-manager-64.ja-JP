---
title: ワークフローモデルの作成
seo-title: Creating Workflow Models
description: ワークフローモデルを作成して、ユーザーがワークフローを開始したときに実行される一連の手順を定義します。
seo-description: You create a workflow model to define the series of steps executed when a user starts the workflow.
uuid: 53d94176-4d5f-4ab3-9628-6b7d44f81139
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 9d2dba11-0d2d-4aed-b941-c8ade9bb7bfa
exl-id: d9c9db5f-9788-460f-ac09-88dd3c911edd
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '2483'
ht-degree: 40%

---

# ワークフローモデルの作成{#creating-workflow-models}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!CAUTION]
>
>クラシック UI の使用については、 [AEM 6.3 ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-3/sites-developing/workflows-models.html) 参照用。

次の項目を作成します。 [ワークフローモデル](/help/sites-developing/workflows.md#model) ：ユーザーがワークフローを開始したときに実行される一連の手順を定義します。 ワークフローを一時的なものにするか、複数のリソースを使用するかなど、モデルのプロパティを定義することもできます。

ユーザーがワークフローを開始すると、1 つのインスタンスが開始されます。これは、次の場合に作成される、対応するランタイムモデルです。 [同期](#sync-your-workflow-generate-a-runtime-model) 変更内容。

## 新しいワークフローの作成 {#creating-a-new-workflow}

最初に新しいワークフローモデルを作成すると、そのモデルには次の内容が含まれます。

* **[!UICONTROL フロー開始]**&#x200B;ステップと&#x200B;**[!UICONTROL フロー終了]**ステップ。


   これらのステップは、ワークフローの始まりと終わりを表します。これらの手順は必須で、編集または削除できません。

* 「**手順 1**」という名前のサンプルの&#x200B;**参加者**ステップ。


   このステップは、作業項目をワークフロー開始者に割り当てるように設定されています。このステップを編集または削除し、必要に応じてステップを追加します。

エディターを使用して新しいワークフローを作成するには：

1. を開きます。 **[!UICONTROL ワークフローモデル]** コンソール～の方法で **[!UICONTROL ツール]**, **[!UICONTROL ワークフロー]**, **[!UICONTROL モデル]** 例：

   [http://localhost:4502/aem/workflow](http://localhost:4502/aem/workflow)

1. 「**[!UICONTROL 作成]**」を選択してから、「**[!UICONTROL モデルを作成]**」を選択します。
1. この **[!UICONTROL ワークフローモデルを追加]** ダイアログボックスが表示されます。 次を入力します。 **[!UICONTROL タイトル]** および **[!UICONTROL 名前]** （オプション）を選択する前に **[!UICONTROL 完了]**.
1. 新しいモデルが&#x200B;**[!UICONTROL ワークフローモデル]**&#x200B;コンソールに表示されます。
1. 新しいワークフローを選択し、「[**[!UICONTROL 編集&#x200B;]**」をクリックすると、ワークフローが設定のために開かれます](#editing-a-workflow)。

   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>（CRX パッケージを使用して）プログラムによってモデルを作成する場合は、次の場所にサブフォルダーを作成することもできます。
>
>`/var/workflow/models`
>
>例：`/var/workflow/models/prototypes`
>
>このフォルダーは、 [そのフォルダー内のモデルへのアクセスの管理](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that).

## ワークフローの編集 {#editing-a-workflow}

既存のワークフローモデルは、次の目的で編集できます。

* [ステップの定義](#adding-a-step-to-a-model) そして [パラメーター](#configuring-a-workflow-step)

* ワークフローのプロパティを設定します。 [ステージ](#configuring-workflow-stages-that-show-workflow-progress), [ワークフローが一時的かどうか](#creating-a-transient-workflow) および/または [複数のリソースを使用](#configuring-a-workflow-for-multi-resource-support)

の編集 [**デフォルトまたはレガシー** （標準）ワークフロー](#editing-a-default-or-legacy-workflow-for-the-first-time) には、 [セーフコピー](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) は、変更がおこなわれる前に実行されます。

ワークフローの更新が完了したら、 **[!UICONTROL 同期]** から **[!UICONTROL ランタイムモデルの生成]**. 詳しくは、 [ワークフローを同期](#sync-your-workflow-generate-a-runtime-model) 」を参照してください。

### ワークフローの同期 — ランタイムモデルの生成 {#sync-your-workflow-generate-a-runtime-model}

**同期** （エディターツールバーの右側）に、 [ランタイムモデル](/help/sites-developing/workflows.md#runtime-model). ランタイムモデルは、ユーザーがワークフローを開始したときに実際に使用されるモデルです。 変更内容を&#x200B;**[!UICONTROL 同期]**&#x200B;しない場合は、その変更内容は実行時には反映されません。

ワークフローに変更を加える場合は、 **[!UICONTROL 同期]** 個々のダイアログ（ステップなど）に独自の保存オプションがある場合でも、ランタイムモデルを生成する。

変更がランタイム（保存済み）モデルと同期された場合、 **[!UICONTROL 同期済み]** が代わりに表示されます。

一部のステップには、必須のフィールドが含まれているか、組み込みの検証が含まれています。 これらの条件が満たされない場合、 **[!UICONTROL 同期]** モデル。 例えば次のように、**[!UICONTROL 参加者]**&#x200B;ステップで参加者が定義されていない場合などです。

![wf-21](assets/wf-21.png)

### 初めてのデフォルトまたはレガシーワークフローの編集 {#editing-a-default-or-legacy-workflow-for-the-first-time}

を開くと、 [デフォルトまたはレガシーモデル](/help/sites-developing/workflows.md#workflow-types) （編集用）:

* この **[!UICONTROL 手順]** ブラウザーを使用できません（左側）。
* ツールバーで「**[!UICONTROL 編集]**」操作を利用できます（右側）。
* 次の理由から、最初はモデルとそのプロパティが読み取り専用モードで開かれます。

   * デフォルトのワークフローは `/libs` にあります。
   * レガシーワークフローは、 `/etc`

選択 **[!UICONTROL 編集]** は次のようになります。

* ワークフローが `/conf` にコピーされます。
* ～を作る **[!UICONTROL 手順]** 使用可能なブラウザー
* 変更を加えられるようになります。

>[!NOTE]
>
>詳しくは、[ワークフローモデルの場所](/help/sites-developing/workflows-best-practices.md#locations-workflow-models)を参照してください。

![wf-22](assets/wf-22.png)

### モデルへのステップの追加 {#adding-a-step-to-a-model}

実行するアクティビティを表す手順をモデルに追加する必要があります。各手順は特定のアクティビティを実行します。 標準のAEMインスタンスでは、様々なステップコンポーネントを使用できます。

モデルを編集すると、使用可能なステップが **[!UICONTROL 手順]** ブラウザー。 次に例を示します。

![wf-10](assets/wf-10.png)

>[!NOTE]
>
>AEMと共にインストールされる主なステップコンポーネントについて詳しくは、 [ワークフローステップのリファレンス](/help/sites-developing/workflows-step-ref.md).

**モデルにステップを追加するには**:

1. 既存のワークフローモデルを編集用に開きます。 **[!UICONTROL ワークフローモデル]**&#x200B;コンソールで、必要なモデルを選択し、**[!UICONTROL 編集]**&#x200B;をクリックします。
1. を開きます。 **[!UICONTROL 手順]** ブラウザ；using **[!UICONTROL サイドパネルを切り替え]**（上部のツールバーの左端） ここでは、以下のことができます。

   * **[!UICONTROL フィルター]** を参照してください。
   * ドロップダウンセレクターを使用して、選択を特定のステップのグループに限定します。
   * 「説明を表示アイコン」![wf-stepinfo-icon](assets/wf-stepinfo-icon.png) を選択して、適切な手順の詳細を確認する。

   ![wf-02](assets/wf-02.png)

1. 適切なステップをモデル内の必要な場所にドラッグします。

   例： **[!UICONTROL 参加者ステップ]**.

   フローに追加された後は、次の操作を実行できます。 [ステップの設定](#configuring-a-workflow-step).

   ![wf-03](assets/wf-03.png)

1. 必要に応じて、手順やその他の更新をいくつでも追加します。

   実行時に、ステップはモデルに表示される順序で実行されます。 ステップコンポーネントを追加した後、モデル内の別の場所にドラッグできます。

   既存のステップのコピー、切り取り、貼り付け、グループ化、削除もできます。例えば [ページエディター。](/help/sites-authoring/editing-content.md)

   分割ステップは、ツールバーオプション ![wf-collapseexpand-toolbar-icon](assets/wf-collapseexpand-toolbar-icon.png) を利用して折りたたんだり展開したりできます。

1. **[!UICONTROL 同期]**（エディターツールバー）をクリックして変更内容を確認し、ランタイムモデルを生成します。

   詳しくは、 [ワークフローを同期](#sync-your-workflow-generate-a-runtime-model) 」を参照してください。

### ワークフローステップの設定 {#configuring-a-workflow-step}

以下が可能です。 **設定** をクリックし、 **[!UICONTROL ステップのプロパティ]** ダイアログボックス

1. 次の手順で **[!UICONTROL ステップのプロパティ]** ステップのダイアログボックスは、次のいずれかの方法で表示されます。

   * ワークフローモデルのステップをタップし、「 」を選択します。 **[!UICONTROL 設定]** を選択します。
   * ステップをダブルクリックします。

   >[!NOTE]
   >
   >AEMと共にインストールされる主なステップコンポーネントについて詳しくは、 [ワークフローステップのリファレンス](/help/sites-developing/workflows-step-ref.md).

1. の設定 **[!UICONTROL ステップのプロパティ]** 必要に応じて使用できるプロパティは、ステップのタイプに応じて異なります。複数のタブを使用することもできます。 例えば、新しいワークフローで `Step 1` として表示されるデフォルトの&#x200B;**[!UICONTROL 参加者ステップ]**&#x200B;では、次のようになります。

   ![wf-11](assets/wf-11.png)

1. チェックマークをクリックして、アップデート内容を確認します。
1. **[!UICONTROL 同期]**（エディターツールバー）をクリックして変更内容を確認し、ランタイムモデルを生成します。

   詳しくは、 [ワークフローを同期](#sync-your-workflow-generate-a-runtime-model) 」を参照してください。

### 一時的なワークフローの作成 {#creating-a-transient-workflow}

次の項目を作成できます。 [一時的](/help/sites-developing/workflows.md#transient-workflows) 新しいモデルを作成する場合、または既存のモデルを編集する場合のワークフローモデル：

1. 次のワークフローモデルを開く： [編集中](#editing-a-workflow).
1. 選択 **[!UICONTROL ワークフローモデルのプロパティ]** をクリックします。
1. ダイアログボックスで、をアクティブにします。 **[!UICONTROL 一時的なワークフロー]** （必要に応じて非アクティブ化）:

   ![wf-07](assets/wf-07.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックし、**[!UICONTROL 同期]**（エディターツールバー）をクリックして変更内容を確認し、ランタイムモデルを生成します。

   詳しくは、 [ワークフローを同期](#sync-your-workflow-generate-a-runtime-model) 」を参照してください。

>[!NOTE]
>
>ワークフローを[一時的](/help/sites-developing/workflows.md#transient-workflows)モードで実行した場合は、AEM にはワークフロー履歴が保存されません。したがって、そのワークフローに関連する情報は、[タイムライン](/help/sites-authoring/basic-handling.md#timeline)に表示されません。 [](/help/sites-authoring/basic-handling.md#timeline)

### タッチ UI でワークフローモデルを使用可能にする {#make-workflow-models-available-in-touchui}

クラシック UI に表示されるワークフローモデルがタッチ UI の&#x200B;**[!UICONTROL タイムライン]**&#x200B;レールの選択ポップアップメニューに表示されない場合は、設定に従ってワークフローモデルを使用可能にします。以下の手順は、**[!UICONTROL アクティベーションのリクエスト]**&#x200B;と呼ばれるワークフローモデルの使用を説明します。

1. 該当するモデルがタッチ対応 UI で使用できないことを確認します。`/assets.html/content/dam` パスを使用してアセットにアクセスします。アセットを選択します。左側のレールで&#x200B;**[!UICONTROL タイムライン]**&#x200B;を開きます。**[!UICONTROL ワークフローを開始]**&#x200B;をクリックして、**[!UICONTROL アクティベーションのリクエスト]** モデルがポップアップリストに存在しないことを確認します。

1. **[!UICONTROL ツール／一般／タグ付け]**&#x200B;と移動します。**[!UICONTROL ワークフロー]**&#x200B;を選択します。

1. 「**[!UICONTROL 作成／タグを作成]**」を選択します。**[!UICONTROL タイトル]**&#x200B;を `DAM` に、**[!UICONTROL 名前]**&#x200B;を `dam` に、それぞれ設定します。**[!UICONTROL 送信]**を選択します。
   ![ワークフローモデルでタグを作成する](assets/workflow_create_tag.png)

1. **[!UICONTROL ツール／ワークフロー／モデル]**&#x200B;に移動します。**[!UICONTROL アクティベーションのリクエスト]**&#x200B;を選択し、次に&#x200B;**[!UICONTROL 編集]**&#x200B;を選択してください。

1. 選択 **[!UICONTROL 編集]** を開き、 **[!UICONTROL ワークフローモデルのプロパティ]**. 次に移動： **[!UICONTROL 基本]** タブをクリックします。

1. `Workflow : DAM` を&#x200B;**[!UICONTROL タグ]**&#x200B;フィールドに追加します。チェック（チェックマーク）で選択を確認します。

1. **[!UICONTROL 保存して閉じる]**でタグの追加を確認します。
   ![モデルのページプロパティの編集](assets/workflow_model_edit_activation1.png)

1. **[!UICONTROL 同期]**&#x200B;でプロセスを完了します。タッチ操作対応 UI でワークフローを使用できるようになりました。

### マルチリソースサポートのためのワークフローの設定 {#configuring-a-workflow-for-multi-resource-support}

次のワークフローモデルを設定できます。 [マルチリソースのサポート](/help/sites-developing/workflows.md#multi-resource-support) 新しいモデルを作成する場合、または既存のモデルを編集する場合：

1. 次のワークフローモデルを開く： [編集中](#editing-a-workflow).
1. 選択 **[!UICONTROL ワークフローモデルのプロパティ]** をクリックします。

1. ダイアログボックスで、をアクティブにします。 **[!UICONTROL マルチリソースのサポート]** （必要に応じて非アクティブ化）:

   ![wf-08](assets/wf-08.png)

1. 変更内容を「**[!UICONTROL 保存して閉じる]**」で確認し、「**[!UICONTROL 同期]**」（エディターツールバー）でランタイムモデルを生成します。

   詳しくは、 [ワークフローを同期](#sync-your-workflow-generate-a-runtime-model) 」を参照してください。

### ワークフローステージの設定（ワークフローの進行状況を表示） {#configuring-workflow-stages-that-show-workflow-progress}

[ワークフローステージ](/help/sites-developing/workflows.md#workflow-stages) タスクを処理する際のワークフローの進行状況を視覚化します。

>[!CAUTION]
>
>ワークフローステージが **[!UICONTROL ページプロパティ]**&#x200B;が含まれていますが、どのワークフローステップにも使用されていない場合、進行状況バーには（現在のワークフローステップに関係なく）進行状況は表示されません。

使用可能なステージは、ワークフローモデルで定義されます。既存のワークフローモデルを更新して、ステージ定義を含めることができます。 ワークフローモデルに対して任意の数のステージを定義できます。

定義するには **[!UICONTROL ステージ]** ワークフローの場合：

1. 編集するワークフローモデルを開きます。
1. 選択 **[!UICONTROL ワークフローモデルのプロパティ]** をクリックします。 次に、 **[!UICONTROL ステージ]** タブをクリックします。
1. 必要な&#x200B;**[!UICONTROL ステージ]**&#x200B;を追加（および配置）します。ワークフローモデルに対して任意の数のステージを定義できます。

   次に例を示します。

   ![wf-08-1](assets/wf-08-1.png)

1. クリック **[!UICONTROL 保存して閉じる]** をクリックしてプロパティを保存します。
1. ワークフローモデル内の各ステップにステージを割り当てます。 次に例を示します。

   ![wf-09](assets/wf-09.png)

   1 つのステージを複数のステップに割り当てることができます。 次に例を示します。

   | **ステップ** | **ステージ** |
   |---|---|
   | 手順 1 | 作成 |
   | 手順 2 | 作成 |
   | 手順 3 | レビュー |
   | 手順 4 | 承認 |
   | 手順 5 | 承認 |
   | 手順 6 | 完了 |

1. 「**[!UICONTROL 同期]**」（エディターツールバー）をクリックして変更内容を確定し、ランタイムモデルを生成します。

   詳しくは、 [ワークフローを同期](#sync-your-workflow-generate-a-runtime-model) 」を参照してください。

## パッケージでのワークフローモデルの書き出し {#exporting-a-workflow-model-in-a-package}

1. を使用して新しいパッケージを作成します。 [パッケージマネージャー](/help/sites-administering/package-manager.md#package-manager):

   1. 次の方法でパッケージマネージャーに移動します。 **[!UICONTROL ツール]**, **[!UICONTROL 導入]**, **[!UICONTROL パッケージ]**.
   1. 「**[!UICONTROL パッケージを作成]**」をクリックします。
   1. 次を指定： **[!UICONTROL パッケージ名]**、および必要に応じてその他の詳細。
   1. 「**[!UICONTROL OK]**」をクリックします。

1. 新しいパッケージのツールバーの「**[!UICONTROL 編集]**」をクリックします。

1. 「**[!UICONTROL フィルター]**」タブを開きます。

1. 「**[!UICONTROL フィルターを追加]**」を選択し、ワークフローモデルの&#x200B;*設計*&#x200B;のパスを指定します。

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   「**[!UICONTROL 完了]**」をクリックします。

1. 「**[!UICONTROL フィルターを追加]**」を選択し、ランタイムワークフローモデルのパスを指定します&#x200B;*。*

   `/var/workflow/models/<*your-model-name*>`

   「**[!UICONTROL 完了]**」をクリックします。

1. モデルで使用されるカスタムスクリプトに対してフィルターを追加します。
1. クリック **[!UICONTROL 保存]** をクリックして、フィルター定義を確認します。
1. 選択 **[!UICONTROL ビルド]** をクリックします。
1. 選択 **[!UICONTROL ダウンロード]** をクリックします。

## ワークフローを使用したフォーム送信の処理 {#using-workflows-to-process-form-submissions}

選択したワークフローで処理されるフォームを設定できます。 ユーザーがフォームを送信すると、フォーム送信のデータをペイロードとして使用した新しいワークフローインスタンスが作成されます。

フォームで使用するワークフローを設定するには、次の手順を実行します。

1. 新しいページを作成し、編集用に開きます。
1. を追加します。 **[!UICONTROL フォーム]** コンポーネントをページに追加します。
1. の設定 **[!UICONTROL フォーム開始]** ページに表示されたコンポーネント
1. 「**[!UICONTROL ワークフローを開始]**」で、使用可能なワークフローの中から目的のワークフローを選択します。

   ![wf-12](assets/wf-12.png)

1. チェックマークを使用して、新しいフォーム設定を確認します。

## ワークフローのテスト {#testing-workflows}

ワークフローをテストする際には、様々なペイロードタイプを使用することをお勧めします。開発されたタイプとは異なるタイプを含む。 例えば、ワークフローで Assets を処理する場合は、ページをペイロードとして設定し、エラーがスローされないことを確認して、アセットをテストします。

例えば、次のようにして、新しいワークフローをテストします。

1. コンソールから[ワークフローモデルを開始](/help/sites-administering/workflows-starting.md)します。
1. **[!UICONTROL ペイロード]**&#x200B;を定義して確定します。

1. ワークフローが進行するように、必要に応じてアクションを実行します。
1. ワークフローの実行中にログファイルを監視します。

また、AEMを **[!UICONTROL デバッグ]** ログファイル内のメッセージ。 詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。開発が完了したら、**[!UICONTROL ログレベル]**&#x200B;を&#x200B;**[!UICONTROL 情報]**&#x200B;に戻します。

## 例 {#examples}

### 例：公開のリクエストを承認／拒否する（単純な）ワークフローの作成 {#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

ワークフロー作成の可能性をいくつか示すために、ここでは、`Publish Example` ワークフローのバリエーションを作成します。

1. [新しいワークフローモデルを作成](#creating-a-new-workflow).

   新しいワークフローには、次の情報が含まれます。

   * **[!UICONTROL フロー開始]**
   * `Step 1`
   * **[!UICONTROL フロー終了]**

1. `Step 1` を削除します（この例には不適切なステップタイプです）。

   * ステップをクリックし、コンポーネントツールバーの「**[!UICONTROL 削除]**」を選択します。アクションを確認します。

1. 次の **[!UICONTROL ワークフロー]** ステップブラウザーの選択、 **[!UICONTROL 参加者ステップ]** をワークフロー上に配置し、次の間に配置します。 **[!UICONTROL フロー開始]** および**[!UICONTROL フロー終了*]*.
1. プロパティダイアログボックスを開くには、次のいずれかを実行します。

   * 参加者ステップをクリックし、コンポーネントツールバーの「**[!UICONTROL 設定]**」を選択します。
   * 参加者ステップをダブルクリックします。

1. 「**[!UICONTROL 共通]**」タブで、「**[!UICONTROL タイトル]**」と「**[!UICONTROL 説明]**」の両方に `Validate Content` と入力します。
1. を開きます。 **[!UICONTROL ユーザー/グループ]** タブ：

   * 有効化 **[!UICONTROL 電子メールでユーザーに通知]**.
   * 「**[!UICONTROL ユーザー／グループ]**」フィールドで「`Administrator`（`admin`）」を選択します。

   >[!NOTE]
   >
   >E メールを送信する場合は、 [メールサービスとユーザーアカウントの詳細を設定する必要があります](/help/sites-administering/notification.md).

1. チェックマークを付けて更新を確認します。

   ワークフローモデルの概要に戻ります。ここで、参加者ステップが `Validate Content` という名前に変更されます。

1. **[!UICONTROL OR 分岐]**&#x200B;をワークフローにドラッグして、「`Validate Content`」と「**[!UICONTROL フロー終了]**」の間に配置します。
1. を開きます。 **[!UICONTROL OR 分割]** 設定用。
1. 設定：

   * **[!UICONTROL 共通]**:選択 **[!UICONTROL 2 ブランチ]**
   * **[!UICONTROL ブランチ 1]**:選択 **[!UICONTROL デフォルトルート]**.
   * **[!UICONTROL ブランチ 2]**:確実にする **[!UICONTROL デフォルトルート]** が選択されていません。

1. 更新内容を **[!UICONTROL OR 分割]**.
1. ドラッグ **[!UICONTROL 参加者ステップ]** 左側のブランチに対して、プロパティを開き、次の値を指定して、変更を確定します。

   * **[!UICONTROL タイトル]**：`Reject Publish Request`
   * **[!UICONTROL ユーザー／グループ]**：`projects-administrators` など
   * **[!UICONTROL メールでユーザーに通知する]**：有効にすると、ユーザーにメールで通知が届きます。

1. **[!UICONTROL プロセスステップ]**&#x200B;を右側のブランチにドラッグし、プロパティを開き、次の値を指定してから変更内容を確認します。

   * **[!UICONTROL タイトル]**：`Publish Page as Requested`
   * **[!UICONTROL プロセス]**：`Activate Page` を選択します。このプロセスは、選択されているページをパブリッシャーインスタンスに公開します。

1. クリック **[!UICONTROL 同期]** （エディターのツールバー）を使用して、ランタイムモデルを生成します。

   詳しくは、 [ワークフローを同期](#sync-your-workflow-generate-a-runtime-model) 」を参照してください。

   新しいワークフローモデルは次のようになります。

   ![wf-13](assets/wf-13.png)

1. このワークフローをページに適用します。その結果、ユーザーが「**[!UICONTROL コンテンツを検証]**」ステップの「**[!UICONTROL 完了]**」に移動すると、「**[!UICONTROL リクエストに応じてページを公開]**」と「**[!UICONTROL 公開リクエストを拒否]**」のどちらを実行するかを選択できます。

   ![chlimage_1-182](assets/chlimage_1-182.png)

### 例：OR 分割のルールの定義 {#example-defining-a-rule-for-an-or-split}

**[!UICONTROL OR 分割]** ステップを使用すると、ワークフローに条件付き処理パスを導入できます。

OR ルールを定義するには：

1. 2 つのスクリプトを作成し、リポジトリに保存します。例えば、次の場所です。

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   >
   >スクリプトには、ブール値を返す[関数 `check()`](#function-check) を含める必要があります。

1. ワークフローを編集し、 **[!UICONTROL OR 分割]** をモデルに追加します。
1. のプロパティを編集 **[!UICONTROL ブランチ 1]** の **[!UICONTROL OR 分割]**:

   * 「**[!UICONTROL 値]**」を `true` に設定して、これを「**[!UICONTROL デフォルトのルート]**」として定義します。
   * 「**[!UICONTROL ルール]**」として、そのスクリプトへのパスを設定します。次に例を示します。

      `/apps/myapp/workflow/scripts/myscript1.ecma`
   >[!NOTE]
   >
   >必要に応じて、ブランチの順序を切り替えることができます。

1. **[!UICONTROL OR 分割]**&#x200B;の&#x200B;**[!UICONTROL ブランチ 2]** のプロパティを編集します。

   * 「**[!UICONTROL ルール]**」として、もう 1 つのスクリプトへのパスを設定します。次に例を示します。

      `/apps/myapp/workflow/scripts/myscript2.ecma`

1. 各ブランチ内の個々のステップのプロパティを設定します。「**[!UICONTROL ユーザー／グループ]**」が設定されていることを確認します。
1. クリック **同期** （エディターのツールバー）を使用して、ランタイムモデルに対する変更を保持します。

   詳しくは、 [ワークフローを同期](#sync-your-workflow-generate-a-runtime-model) 」を参照してください。

#### 関数 Check() {#function-check}

>[!NOTE]
>
>詳しくは、 [ECMAScript の使用](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).

次のサンプルスクリプトは、ノードが `/content/we-retail/us/en` の下に位置する `JCR_PATH` の場合、`true` を返します。

```
function check() {
    if (workflowData.getPayloadType() == "JCR_PATH") {
      var path = workflowData.getPayload().toString();
      var node = jcrSession.getItem(path);

      if (node.getPath().indexOf("/content/we-retail/us/en") >= 0) {
       return true;
      } else {
       return false;
      } 
     } else {
      return false;
     }
}
```

### 例：アクティベーションのカスタマイズリクエスト {#example-customized-request-for-activation}

標準搭載の任意のワークフローをカスタマイズできます。 動作をカスタマイズするには、該当するワークフローの詳細をオーバーレイします。

例： **[!UICONTROL アクティベーションのリクエスト]**. このワークフローは、 **[!UICONTROL サイト]** コンテンツ作成者が適切なレプリケーション権限を持っていない場合に、自動的にトリガーされます。 詳しくは、[ページオーサリングのカスタマイズ - アクティベーションをリクエストワークフローのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow)を参照してください。
