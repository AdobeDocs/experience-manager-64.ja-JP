---
title: ワークフローステップのリファレンス
seo-title: Workflow Step Reference
description: ワークフローステップのリファレンス
seo-description: null
uuid: 72a64495-d1b1-49e7-8257-d6b2ed36961c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 25f0e0f7-9570-4748-81cb-ccec6492c0b4
exl-id: dfa39c6c-7a1a-4aa4-a72d-caa5e3ebf4a8
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2829'
ht-degree: 44%

---

# ワークフローステップのリファレンス{#workflow-step-reference}

ワークフローモデルは、様々なタイプの一連のステップで構成されます。 これらの手順は、タイプに応じて、必要な機能と制御を提供するパラメーターとスクリプトを使用して設定および拡張できます。

>[!NOTE]
>
>ここでは、標準的なワークフロー手順について説明します。
>
>モジュール固有の手順については、次の項も参照してください。
>
>* [AEM Forms Workflow Step Reference](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [メディアハンドラーとワークフローを使用したアセットの処理](/help/assets/media-handlers.md)
>


## ステップのプロパティ {#step-properties}

各ステップコンポーネントには、 **[!UICONTROL ステップのプロパティ]** 必要なプロパティを定義および編集できるダイアログ。

### ステップのプロパティ — 「共通」タブ {#step-properties-common-tab}

ほとんどのワークフローステップコンポーネントでは、次のプロパティの組み合わせを使用できます。 **[!UICONTROL 共通]** プロパティダイアログの「 」タブ

* **[!UICONTROL タイトル]**

   ステップのタイトル。

* **[!UICONTROL 説明]**

   ステップの説明。

* **[!UICONTROL ワークフローステージ]**

   適用するドロップダウンセレクター [ステージ](/help/sites-developing/workflows.md#workflow-stages) をステップに追加します。

* **[!UICONTROL タイムアウト]**

   ステップが「タイムアウト」するまでの期間です。


   **[!UICONTROL オフ]**、**[!UICONTROL 即時]**、**[!UICONTROL 1 時間]**、**[!UICONTROL 6 時間]**、**[!UICONTROL 12 時間]**、**[!UICONTROL 24 時間]**&#x200B;から選択できます。

* **[!UICONTROL タイムアウトハンドラー]**

   ステップがタイムアウトしたときにワークフローを制御するハンドラーです。例：

   `Auto Advancer`

* **[!UICONTROL ハンドラー処理の設定]**

   実行後にワークフローを次のステップに自動的に進めるには、このオプションを選択します。選択しなかった場合、実装スクリプトでワークフローの進行を処理する必要があります。

#### ステップのプロパティ — 「ユーザー/グループ」タブ {#step-properties-user-group-tab}

次のプロパティは、多くのワークフローステップコンポーネントで、 **[!UICONTROL ユーザー/グループ]** プロパティダイアログの「 」タブ

* **[!UICONTROL 電子メールでユーザーに通知]**

   * ワークフローがステップに到達したら電子メールを送信して、参加者に通知できます。
   * 有効にすると、プロパティで定義されたユーザーに電子メールが送信されます **[!UICONTROL ユーザー/グループ]** またはグループが定義されている場合は、グループの各メンバーに割り当てます。

* **[!UICONTROL ユーザー / グループ]**

   * ドロップダウン選択ボックスを使用して、ユーザーやグループ間を移動し、選択することができます
   * 特定のユーザーにステップを割り当てた場合は、そのユーザーだけがステップのアクションを実行できます。
   * グループ全体にステップを割り当てた場合、ワークフローがこのステップに到達すると、グループのユーザーすべての&#x200B;**[!UICONTROL ワークフローの受信ボックス]**&#x200B;にアクションが保持されます。
   * 詳しくは、 [ワークフローへの参加](/help/sites-authoring/workflows-participating.md) を参照してください。

## AND 分割 {#and-split}

**[!UICONTROL AND 分割]**&#x200B;は、ワークフロー内に分割を作成し、両方のブランチをアクティブにします。必要に応じて、各分岐にワークフローステップを追加できます。この手順では、複数の処理パスをワークフローに組み込むことができます。 例えば、特定のレビュー手順を並行して実行できるので、時間を節約できます。

![wf-26](assets/wf-26.png)

### AND 分割 — 設定 {#and-split-configuration}

* を編集します。 **[!UICONTROL AND 分割]** プロパティ：

   * **[!UICONTROL 名前を分割]**:名前を割り当てて説明します。
   * 必要なブランチの数を選択します。2、3、4 または 5。

* 必要に応じて、各ブランチにワークフローステップを追加します。

   ![wf-27](assets/wf-27.png)

## コンテナのステップ {#container-step}

A **[!UICONTROL コンテナ]** ステップは、子ワークフローとして実行される別のワークフローモデルを開始します。

この **[!UICONTROL コンテナ]** では、ワークフローモデルを再利用して、一般的な一連のステップを実装できます。 例えば、翻訳ワークフローモデルを複数の編集ワークフローで使用できます。

![wf-28](assets/wf-28.png)

### コンテナステップ — 設定 {#container-step-configuration}

このステップを設定するには、次のタブを編集および使用します。

* [**[!UICONTROL 共通]**](#step-properties-common-tab)
* **[!UICONTROL コンテナ]**

   * **[!UICONTROL サブワークフロー]**:開始するワークフローを選択します。

## ステップに移動 {#goto-step}

この **[!UICONTROL ステップに移動]** では、ECMAScript の結果に応じて、実行するワークフローモデル内の次のステップを指定できます。

* `true`:この **[!UICONTROL ステップに移動]** が完了し、ワークフローエンジンは指定されたステップを実行します。

* `false`:この **[!UICONTROL ステップに移動]** が完了し、通常のルーティングロジックが実行する次のステップを決定します。

**[!UICONTROL 移動ステップ]**&#x200B;を使用すると、ワークフローモデル内に詳細なルーティング構造を実装できます。例えば、ループを実装するには、 **[!UICONTROL ステップに移動]** を定義し、ループ条件を評価するスクリプトを使用して、ワークフロー内の前のステップを実行できます。

### ステップに移動 — 設定 {#goto-step-configuration}

このステップを設定するには、次のタブを編集および使用します。

* [**[!UICONTROL 共通]**](#step-properties-common-tab)
* **[!UICONTROL プロセス]**

   * **[!UICONTROL 移動先のステップ]**:実行するステップを選択します。
   * **[!UICONTROL スクリプトパス]**:を実行するかどうかを決定する ECMAScript へのパス **[!UICONTROL ステップに移動]**.
   * **[!UICONTROL スクリプト]**:を実行するかどうかを決定する ECMAScript **[!UICONTROL ステップに移動]**.

>[!CAUTION]
>
>次のいずれかを指定します。 **[!UICONTROL スクリプトパス]** または **[!UICONTROL スクリプト]**. 両方のオプションを同時に使用することはできません。 両方のプロパティの値を指定した場合、この手順では **[!UICONTROL スクリプトパス]**.

#### for ループのシミュレーション {#simulating-a-for-loop}

for ループをシミュレートするには、発生したループ反復回数を維持する必要があります。

* 通常、カウントは、ワークフローで処理される項目のインデックスを表します。
* ループの終了条件としてカウントが評価されます。

例えば、複数の JCR ノードに対してアクションを実行するワークフローを実装する場合は、ループカウンターをノードのインデックスとして使用できます。 回数を保持するには、ワークフローインスタンスのデータマップに `integer` 値を保存します。回数を増分したり、回数を終了基準と比較するには、**[!UICONTROL 移動ステップ]**&#x200B;のスクリプトを使用します。

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){ 
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      } 
 
     workflowData.getMetaDataMap().put(keyname,count);
 
     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

## OR 分割 {#or-split}

**[!UICONTROL OR 分割]**&#x200B;は、ワークフロー内に分割を作成し、どちらか 1 つのブランチだけをアクティブにします。これを使用すると、ワークフローに条件付き処理パスを導入できます。必要に応じて、各分岐にワークフローステップを追加できます。

>[!NOTE]
>
>OR 分割の作成について詳しくは、[https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html](https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html) を参照してください。

![wf-29](assets/wf-29.png)

### OR 分割 — 設定 {#or-split-configuration}

* を編集します。 **[!UICONTROL OR 分割]** プロパティ：

   * **[!UICONTROL 共通]**

      * 必要なブランチの数を選択します。2、3、4 または 5。
   * **[!UICONTROL ブランチ： *x*>]**

      * **[!UICONTROL スクリプトパス]**:スクリプトを含むファイルへのパス。
      * **[!UICONTROL スクリプト]**:ボックスにスクリプトを追加します。
      * **[!UICONTROL デフォルトルート]**:複数の分岐が true と評価される場合は、デフォルトの分岐に従います。 デフォルトとして指定できるブランチは 1 つだけです。

   >[!NOTE]
   >
   >ブランチごとに個別のタブがあります。
   >
   >* 各ブランチのスクリプトは、一度に 1 つずつ評価されます。
   >* 分岐は左から右に評価されます。
   >* true に評価された最初のスクリプトが実行されます。
   >* true に評価される分岐がない場合は、ワークフローが進行しません。


   >[!CAUTION]
   >
   >次のいずれかを指定します。 **[!UICONTROL スクリプトパス]** または **[!UICONTROL スクリプト]**. 両方のオプションを同時に使用することはできません。 両方のプロパティの値を指定した場合、この手順では **[!UICONTROL スクリプトパス]**.

   >[!NOTE]
   >
   >詳しくは、 [OR 分割のルールの定義](/help/sites-developing/workflows-models.md#example-defining-a-rule-for-an-or-split).

* 必要に応じて、各ブランチにワークフローステップを追加します。

## 参加者ステップと選択 {#participant-steps-and-choosers}

### 参加者ステップ {#participant-step}

A **[!UICONTROL 参加者ステップ]** を使用すると、特定のアクションに所有権を割り当てることができます。 ワークフローは、ユーザーがそのステップを手動で了承した場合にのみ進行します。ワークフロー上で誰かにアクションを起こさせたい場合、例えばレビューの手順などで使用します。

直接は関連していませんが、アクションを割り当てる際には、ユーザー認証を考慮する必要があります。ユーザーは、ワークフローペイロードであるページにアクセスできる必要があります。

#### 参加者ステップ — 設定 {#participant-step-configuration}

このステップを設定するには、次のタブを編集および使用します。

* [**[!UICONTROL 共通]**](#step-properties-common-tab)
* [**[!UICONTROL ユーザー / グループ]**](#step-properties-user-group-tab)

>[!NOTE]
>
>次の場合、ワークフロー開始者には常に通知が送信されます。
>
>* ワークフローが完了（終了）しました。
>* ワークフローが中止（終了）されました。
>


>[!NOTE]
>
>一部のプロパティは、電子メール通知を有効にするように設定する必要があります。 また、電子メールテンプレートをカスタマイズしたり、新しい言語用の電子メールテンプレートを追加したりすることもできます。 AEM でメール通知を設定するには、[メール通知の設定](/help/sites-administering/notification.md)を参照してください。

### ダイアログ参加者ステップ {#dialog-participant-step}

の使用 **[!UICONTROL ダイアログ参加者ステップ]** ：作業項目を割り当てられたユーザーから情報を収集します。 この手順は、後でワークフローで使用される少量のデータを収集する場合に役立ちます。

ステップを完了すると、 **[!UICONTROL 作業項目を完了]** ダイアログには、ダイアログで定義するフィールドが含まれます。 フィールドで収集されたデータは、ワークフローペイロードのノードに保存されます。 その後のワークフローステップでは、リポジトリから値を読み取ることができます。

ステップを設定するには、作業項目を割り当てるグループまたはユーザーと、ダイアログへのパスを指定します。

#### ダイアログ参加者ステップ — 設定 {#dialog-participant-step-configuration}

このステップを設定するには、次のタブを編集および使用します。

* [**[!UICONTROL 共通]**](#step-properties-common-tab)
* [**[!UICONTROL ユーザー / グループ]**](#step-properties-user-group-tab)
* **[!UICONTROL ダイアログ]**

   * **[!UICONTROL ダイアログパス**]:次の [作成するダイアログ](#dialog-participant-step-creating-a-dialog).

#### ダイアログ参加者ステップ — ダイアログの作成{#dialog-participant-step-creating-a-dialog}

ダイアログを作成するには：

* 結果データをどこに配置するかを決定します [ペイロードに保存される](#dialog-participant-step-storing-data-in-the-payload).
* [ダイアログを定義します。これには、データの収集（および保存）に使用するフィールドの定義が含まれます](#dialog-participant-step-dialog-definition)。

#### ダイアログ参加者ステップ — ペイロードへのデータの格納 {#dialog-participant-step-storing-data-in-the-payload}

ウィジェットデータは、ワークフローペイロードまたは作業項目メタデータに保存できます。 widget ノードの `name` プロパティの形式によって、データの保存場所が決定されます。

* **[!UICONTROL データをペイロードと共に保存]**

   * ウィジェットデータをワークフローペイロードのプロパティとして保存するには、ウィジェットノードの name プロパティの値に次の形式を使用します。

      `./jcr:content/nodename`

   * データは、ペイロードのノードの `nodename` プロパティに保存されます。ノードにそのプロパティが含まれていない場合は、プロパティが作成されます。
   * ペイロードと共に保存された場合、後続で同じペイロードでダイアログを使用すると、プロパティの値が上書きされます。

* **[!UICONTROL データを作業項目と共に保存]**

   * ウィジェットデータを作業項目のメタデータのプロパティとして保存するには、name プロパティの値に次の形式を使用します。

      `nodename`

   * データは、作業項目 `metadata` の `nodename` プロパティに保存されます。この場合は、同じペイロードを持つダイアログを使用しても、データは保存されます。

#### ダイアログ参加者ステップ — ダイアログ定義 {#dialog-participant-step-dialog-definition}

1. **[!UICONTROL ダイアログ構造]**

   ダイアログ参加者ステップのダイアログは、コンポーネントをオーサリングするために作成するダイアログに似ています。 これらは次の場所に保存されます。

   `/apps/myapp/workflow/dialogs`

   標準のタッチ操作対応 UI 用のダイアログは、次のノード構造を持ちます。

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content 
         |- layout 
           |- items 
             |- column 
               |- items 
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   >
   >詳しくは、 [ダイアログの作成と設定](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog).

1. **[!UICONTROL ダイアログパスプロパティ]**

   **[!UICONTROL ダイアログ参加者手順]**&#x200B;には、**[!UICONTROL ダイアログパス]**&#x200B;のプロパティ（および[参加者手順](#participant-step)のプロパティ）があります。**[!UICONTROL ダイアログパス]**&#x200B;のプロパティの値は、ダイアログの `dialog` ノードへのパスです。

   例えば、ダイアログが、ノードに保存されている `EmailWatch` というコンポーネントに含まれているとします。

   `/apps/myapp/workflows/dialogs`

   タッチ操作対応 UI の場合、**[!UICONTROL ダイアログパス]**&#x200B;のプロパティには次の値を使用します。

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **ダイアログ定義の例**

   次の XML コードスニペットは、ペイロードコンテンツの `String` ノードに `watchEmail` 値を保存するダイアログを表しています。title ノードは、[TextField](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) コンポーネントを表します。

   ```xml
   jcr:primaryType="nt:unstructured" 
       jcr:title="Watcher Email Address Dialog" 
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured" 
               margin="false" 
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured" 
                           fieldLabel="Notification Email Address" 
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   この例では、タッチ操作対応 UI の場合、次のようなダイアログが表示されます。

   ![chlimage_1-177](assets/chlimage_1-177.png)

### 動的参加者ステップ {#dynamic-participant-step}

この **[!UICONTROL 動的参加者ステップ]** コンポーネントは、 **[!UICONTROL 参加者ステップ]** 実行時に参加者が自動的に選択される差異を設定できます。

ステップを設定するには、 **[!UICONTROL 参加者選択]** 作業項目を割り当てる参加者を、ダイアログと共に識別する。

#### 動的参加者ステップ — 設定 {#dynamic-participant-step-configuration}

このステップを設定するには、次のタブを編集および使用します。

* [**[!UICONTROL 共通]**](#step-properties-common-tab)
* **[!UICONTROL 参加者選択]**

   * **[!UICONTROL 参加者選択]**:の名前 [作成する参加者選択](#dynamic-participant-step-developing-the-participant-chooser).
   * **[!UICONTROL 引数]**:必要な引数。
   * **[!UICONTROL 電子メール]**:電子メール通知をユーザーに送信するかどうかを指定します。

* **[!UICONTROL ダイアログ]**

   * **[!UICONTROL ダイアログパス]**:次の [作成するダイアログ ( **ダイアログ参加者ステップ**)](#dialog-participant-step-creating-a-dialog).

#### 動的参加者ステップ — 参加者選択の開発 {#dynamic-participant-step-developing-the-participant-chooser}

参加者選択を作成します。 したがって、任意の選択ロジックまたは条件を使用できます。 例えば、参加者選択では、最も作業項目の少ないユーザー（グループ内）を選択できます。 任意の数の参加者選択を作成して、 **動的参加者ステップ** コンポーネントをワークフローモデルに追加します。

作業項目を割り当てるユーザーを選択する OSGi サービスまたは ECMAScript を作成します。

* **[!UICONTROL ECMAscript]**

   スクリプトには、ユーザー ID を `String` 値として返す、getParticipant という関数を含める必要があります。カスタムスクリプトは、例えば `/apps/myapp/workflow/scripts` フォルダーまたはサブフォルダーに格納します。

   標準 AEM インスタンスには、次のサンプルスクリプトが付属しています。

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >`/libs` パス内の設定は&#x200B;*一切*&#x200B;変更しないでください。
   >
   >
   >`/libs` のコンテンツは、インスタンスを次回アップグレードするとき（場合によってはホットフィックスまたは機能パックを適用したとき）に上書きされるからです。

   このスクリプトは、ワークフロー開始者を参加者として選択します。

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >**[!UICONTROL ワークフローイニシエーター参加者選択]**&#x200B;コンポーネントは、**[!UICONTROL 動的参加者手順]**&#x200B;を拡張し、このスクリプトを手順の実装として使用します。

* **[!UICONTROL OSGi サービス]**

   サービスは、[com.day.cq.workflow.exec.ParticipantStepChooser](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) インターフェイスを実装する必要があります。このインターフェイスは、次の構成要素を定義します。

   * `SERVICE_PROPERTY_LABEL` フィールド：このフィールドを使用して、参加者選択の名前を指定します。この名前が、**[!UICONTROL 動的参加者ステップ]**&#x200B;のプロパティで使用可能な参加者選択のリストに表示されます。
   * `getParticipant` メソッド：動的に解決されるプリンシパル ID を `String` 値として返します。

   >[!CAUTION]
   >
   >`getParticipant` メソッドは、動的に解決されるプリンシパル ID を返します。グループ ID またはユーザー ID を指定できます。
   >
   >
   >ただし、グループ ID は **[!UICONTROL 参加者ステップ]**（参加者のリストが返された場合） **[!UICONTROL 動的参加者手順]**&#x200B;の場合は、空のリストが返されるので、委任のために使用することはできません。

   **[!UICONTROL 動的参加者ステップ]**&#x200B;コンポーネントに対して実装を使用可能にするには、サービスを書き出す OSGi バンドルに Java クラスを追加し、バンドルを AEM サーバーにデプロイします。

   >[!NOTE]
   >
   >**[!UICONTROL ランダム参加者選択]**&#x200B;は、ランダムにユーザーを選択するサンプルサービスです（`com.day.cq.workflow.impl.process.RandomParticipantChooser`）。この **[!UICONTROL ランダム参加者選択]** ステップコンポーネントサンプルは、 **[!UICONTROL 動的参加者ステップ]** では、このサービスをステップの実装として使用します。

#### 動的参加者ステップ - 参加者選択サービスの例 {#dynamic-participant-step-example-participant-chooser-service}

次の Java クラスは、`ParticipantStepChooser` インターフェイスを実装します。このクラスは、ワークフローを開始した参加者の名前を返します。このコードでは、サンプルスクリプト（`initator-participant-chooser.ecma`）と同じロジックを使用しています。

`@Property` 注釈では、`SERVICE_PROPERTY_LABEL` フィールドの値を `Workflow Initiator Participant Chooser` に設定します。

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

**[!UICONTROL 動的参加者手順]**&#x200B;プロパティダイアログの&#x200B;**[!UICONTROL 参加者選択]**&#x200B;リストには、このサービスを表す `Workflow Initiator Participant Chooser (script)` という項目が含まれています。

「ワークフローモデルが開始されると、ログには、ワークフローを開始し、作業項目を割り当てられたユーザーの ID が示されます。 この例では、`admin` ユーザーがワークフローを開始しています。

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### フォーム参加者ステップ {#form-participant-step}

この **[!UICONTROL フォーム参加者ステップ]** 作業項目が開かれたときにフォームを表示します。 ユーザーがフォームに入力して送信すると、フィールドデータはワークフローペイロードのノードに保存されます。

ステップを設定するには、作業項目を割り当てるグループまたはユーザーと、フォームへのパスを指定します。

>[!CAUTION]
>
>この節では、[ページオーサリングの基盤コンポーネントのフォームセクション](/help/sites-authoring/default-components-foundation.md#form)について説明します。

#### フォーム参加者ステップ — 設定 {#form-participant-step-configuration}

このステップを設定するには、次のタブを編集および使用します。

* [**[!UICONTROL 共通]**](#step-properties-common-tab)
* [**[!UICONTROL ユーザー / グループ]**](#step-properties-user-group-tab)
* **[!UICONTROL フォーム]**

   * **[!UICONTROL フォームパス]**：[作成するフォーム](#form-participant-step-creating-the-form)へのパス。

#### フォーム参加者ステップ — フォームの作成 {#form-participant-step-creating-the-form}

と共に使用するフォームの作成 **[!UICONTROL フォーム参加者ステップ]** 通常どおり。 ただし、フォーム参加者ステップのフォームには、次の設定が必要です。

* **[!UICONTROL フォームの開始]**&#x200B;コンポーネントでは、**[!UICONTROL アクションタイプ]**&#x200B;プロパティが `Edit Workflow Controlled Resource(s)` に設定されている必要があります。

* **[!UICONTROL フォームの開始]**&#x200B;コンポーネントには、`Form Identifier` プロパティの値が必要です。

* フォームコンポーネントでは、**エレメント名**&#x200B;プロパティを、フィールドデータを保存するノードのパスに設定する必要があります。パスは、ワークフローペイロードのコンテンツ内のノードを指す必要があります。値には次の形式を使用します。

   `./jcr:content/path_to_node`

* フォームには、**[!UICONTROL ワークフロー送信ボタン]**&#x200B;コンポーネントを含める必要があります。コンポーネントのプロパティは設定しません。

ワークフローの要件によって、フィールドデータを格納する場所が決まります。 例えば、フィールドデータを使用して、ページコンテンツのプロパティを設定できます。 **[!UICONTROL 要素名]**&#x200B;プロパティの次の値は、フィールドデータを `jcr:content` ノードの `redirectTarget` プロパティの値として保存します。

`./jcr:content/redirectTarget`

次の例では、フィールドデータはペイロードページの&#x200B;**[!UICONTROL テキスト]**&#x200B;コンポーネントのコンテンツとして使用されています。

`./jcr:content/par/text_3/text`

「最初の例は、 `cq:Page` コンポーネントのレンダリング。 2 番目の例は、ペイロードページに「**」という ID を持つ**&#x200B;テキスト`text_3`コンポーネントが含まれる場合にのみ使用できます。

フォームは、リポジトリ内のどこにでも配置できますが、ワークフローユーザーにはフォームを読み取るための権限が必要です。

### ランダム参加者選択 {#random-participant-chooser}

**[!UICONTROL ランダム参加者選択]**&#x200B;手順は、生成された作業項目をリストからランダムに選択されたユーザーに割り当てる参加者選択です。

![wf-31](assets/wf-31.png)

#### ランダム参加者選択 — 設定 {#random-participant-chooser-configuration}

このステップを設定するには、次のタブを編集および使用します。

* [**[!UICONTROL 共通]**](#step-properties-common-tab)
* **[!UICONTROL 引数]**

   * **[!UICONTROL 参加者]**:選択可能なユーザーのリストを指定します。 リストにユーザーを追加するには、 **[!UICONTROL 項目を追加]** ユーザーノードのホームパスまたはユーザー ID を入力します。 ユーザーの順序は、作業項目が割り当てられる可能性に影響を与えません。

### ワークフローイニシエーター参加者選択 {#workflow-initiator-participant-chooser}

この **[!UICONTROL ワークフローイニシエーター参加者選択]** ステップは、生成された作業項目をワークフローを開始したユーザーに割り当てる参加者選択です。 設定できるプロパティは、 **[!UICONTROL 共通]** プロパティ。

#### ワークフローイニシエーター参加者選択 — 設定 {#workflow-initiator-participant-chooser-configuration}

手順を設定するには、次のタブを使用して編集します。

* [**[!UICONTROL 共通]**](#step-properties-common-tab)

## プロセスステップ {#process-step}

A **[!UICONTROL 処理ステップ]** は、ECMAScript を実行するか、OSGi サービスを呼び出して自動処理を実行します。

![wf-32](assets/wf-32.png)

### プロセスステップ — 設定 {#process-step-configuration}

このステップを設定するには、次のタブを編集および使用します。

* [**[!UICONTROL 共通]**](#step-properties-common-tab)
* **[!UICONTROL プロセス]**

   * **[!UICONTROL プロセス]**:実行するプロセス実装。 ドロップダウンメニューを使用して、ECMAScript または OSGi サービスを選択します。参考情報：

      * 標準の ECMAScript と OSGi サービスについては、 [プロセスステップの組み込みプロセス](/help/sites-developing/workflows-process-ref.md).
      * 用の ECMAScript の作成 **[!UICONTROL プロセス]** 手順については、 [ECMAScript を使用したプロセスステップの実装](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * の OSGi サービスの作成 **[!UICONTROL プロセス]** 手順については、 [Java クラスを使用したプロセスステップの実装](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).
   * **[!UICONTROL ハンドラー処理の設定]**:実行後にワークフローを次のステップに自動的に進めるには、このオプションを選択します。 選択しなかった場合、実装スクリプトでワークフローの進行を処理する必要があります。
   * **[!UICONTROL 引数]**:プロセスに渡す引数。
