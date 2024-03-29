---
title: OSGi 上の Forms 中心のワークフロー | ユーザーデータの処理
seo-title: Forms-centric workflows on OSGi | Handling user data
description: Forms中心のAEMワークフローを使用すると、実世界のForms中心のビジネスプロセスを自動化できます。 ユーザーデータとデータストアの詳細を掘り下げます。 ユーザーデータにアクセスして削除する方法を説明します。
seo-description: Forms-centric AEM workflows enable you to automate real-world Forms-centric business processes. Dig deeper on user data and data stores. Learn how to access and delete user data.
uuid: 6eefbe84-6496-4bf8-b065-212aa50cd074
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 9f400560-8152-4d07-a946-e514e9b9cedf
role: Admin
exl-id: 65c13bc8-da82-4c4b-b014-341ce1b59b71
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 30%

---

# OSGi 上の Forms 中心のワークフロー | ユーザーデータの処理 {#forms-centric-workflows-on-osgi-handling-user-data}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Forms中心のAEMワークフローを使用すると、実世界のForms中心のビジネスプロセスを自動化できます。 ワークフローは、関連付けられたワークフローモデルで指定された順序で実行される一連のステップで構成されます。 各手順では、ユーザーへのタスクの割り当てや電子メールメッセージの送信など、特定のアクションを実行します。 ワークフローでは、リポジトリ内のアセット、ユーザーアカウントおよびサービスとやり取りができます。このため、ワークフローでは、Experience Manager のあらゆる側面を含む複雑なアクティビティを連携させることができます。

フォーム中心のワークフローは、次のいずれかの方法でトリガーまたは起動できます。

* AEM インボックスからのアプリケーションの送信
* AEM Forms アプリケーションからのアプリケーションの送信
* アダプティブフォームの送信
* 監視フォルダーの使用
* インタラクティブ通信またはレターの送信

Forms中心のAEMワークフローと機能について詳しくは、 [OSGi 上のForms中心のワークフロー](/help/forms/using/aem-forms-workflow.md).

## ユーザーデータとデータストア {#user-data-and-data-stores}

ワークフローがトリガーされると、そのワークフローインスタンスに対してペイロードが自動生成されます。 各ワークフローインスタンスには、一意のインスタンス ID と、関連するペイロード ID が割り当てられます。 ペイロードには、ワークフローインスタンスに関連付けられたユーザーデータとフォームデータのリポジトリの場所が含まれます。 さらに、ワークフローインスタンスのドラフトと履歴データもAEMリポジトリに保存されます。

ワークフローインスタンスのペイロード、ドラフト、履歴が存在するデフォルトのリポジトリの場所は次のとおりです。

>[!NOTE]
>
>ワークフローまたはアプリケーションを作成する際に、ペイロード、ドラフトおよび履歴データを保存する様々な場所を設定できます。 ワークフローまたはアプリケーションがデータを保存する場所を特定するには、ワークフローを確認します。

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td>AEM 6.4 Forms</td> 
   <td>AEM 6.3 Forms</td> 
  </tr> 
  <tr> 
   <td><strong>ワークフロー<br />インスタンス</strong></td> 
   <td>/var/workflow/instances/[server_id]/&lt;date&gt;/[workflow-instance]/</td> 
   <td>/etc/workflow/instances/[server_id]/[date]/[workflow-instance]/</td> 
  </tr> 
  <tr> 
   <td><strong>ペイロード</strong></td> 
   <td>/var/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td> 
   <td>/etc/fd/dashboard/payload/[server_id]/[date]/<br /> [payload-id]/</td> 
  </tr> 
  <tr> 
   <td><strong>ドラフト</strong></td> 
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td> 
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow-instance]/draft/[workitem]/</td> 
  </tr> 
  <tr> 
   <td><strong>History</strong></td> 
   <td>/var/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td> 
   <td>/etc/fd/dashboard/instances/[server_id]/<br /> [date]/[workflow_instance]/history/</td> 
  </tr> 
 </tbody> 
</table>

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

リポジトリ内のワークフローインスタンスからユーザーデータにアクセスして削除できます。 これをおこなうには、ユーザーに関連付けられたワークフローインスタンスのインスタンス ID を把握しておく必要があります。 ワークフローインスタンスのインスタンス ID は、ワークフローインスタンスを開始したユーザーのユーザー名またはワークフローインスタンスの現在の担当者を使用して確認できます。

ただし、次のシナリオでは、イニシエーターに関連付けられたワークフローを識別する際に、特定できない場合や、結果があいまいになる場合があります。

* **監視フォルダーを介してトリガーされたワークフロー**:ワークフローが監視フォルダーによってトリガーされた場合、ワークフローインスタンスは、そのイニシエーターを使用して識別できません。 この場合、ユーザ情報は、格納されたデータにエンコードされます。
* **パブリッシュインスタンスから開始されたAEM**:アダプティブフォーム、インタラクティブ通信、またはレターがAEMパブリッシュインスタンスから送信されると、すべてのワークフローインスタンスがサービスユーザーを使用して作成されます。 この場合、ログインしたユーザーのユーザー名はワークフローインスタンスのデータには取り込まれません。

### ユーザーデータにアクセス {#access}

ワークフローインスタンスに格納されているユーザーデータを特定してアクセスするには、次の手順を実行します。

1. AEM オーサーインスタンスで、`https://[server]:[port]/crx/de` にアクセスして、**[!UICONTROL ツール／クエリ]**&#x200B;に移動します。

   選択 **[!UICONTROL SQL2]** から **[!UICONTROL タイプ]** 」ドロップダウンリストから選択できます。

1. 使用可能な情報に応じて、次のいずれかのクエリを実行します。

   * ワークフロー開始者が既知の場合は、次の手順を実行します。

   `SELECT &ast; FROM [cq:Workflow] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[initiator]='*initiator-ID*'`

   * 検索しているデータのユーザーが現在のワークフローの担当者である場合は、次のコマンドを実行します。

   `SELECT &ast; FROM [cq:WorkItem] AS s WHERE ISDESCENDANTNODE([path-to-workflow-instances]) and s.[assignee]='*assignee-id*'`

   クエリを実行すると、指定されたワークフロー開始者また現在のワークフロー担当者のすべてのワークフローインスタンスの場所が返されます。

   例えば、次のクエリを実行すると、ワークフロー開始者が `/var/workflow/instances` の `srose` ノードから 2 つのワークフローインスタンスのパスが返されます。

   ![workflow-instance](assets/workflow-instance.png)

1. クエリから返されたワークフローインスタンスのパスに移動します。 status プロパティは、ワークフローインスタンスの現在のステータスを表示します。

   ![status](assets/status.png)

1. ワークフローインスタンスのノードで、`data/payload/` に移動します。`path` プロパティには、ワークフローインスタンスのペイロードへのパスが格納されます。パスに移動すれば、ペイロードに格納されたデータにアクセスできます。

   ![payload-path](assets/payload-path.png)

1. ワークフローインスタンスのドラフトと履歴の場所に移動します。

   次に例を示します。

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/draft/`

   `/var/fd/dashboard/instances/server0/2018-04-09/_var_workflow_instances_server0_2018-04-09_basicmodel_54/history/`

1. 手順 2 のクエリを実行して返されたすべてのワークフローインスタンスで手順 3 から 5 を繰り返します。

>[!NOTE]
>
>また、AEM Forms App はデータをオフラインモードで保存します。 ワークフローインスタンスのデータは、個々のデバイスにローカルに保存され、アプリがサーバーと同期する際にFormsサーバーに送信される可能性があります。

### ユーザーデータの削除 {#delete-user-data}

次の手順を実行して、ワークフローインスタンスからユーザーデータを削除するには、AEM管理者である必要があります。

1. 詳しくは、 [ユーザーデータにアクセス](/help/forms/using/forms-workflow-osgi-handling-user-data.md#access) 次の点に注意してください。

   * ユーザーに関連付けられたワークフローインスタンスへのパス
   * ワークフローインスタンスのステータス
   * ワークフローインスタンスのペイロードへのパス
   * ワークフローインスタンスのドラフトと履歴へのパス

1. この手順を、**RUNNING**、**SUSPENDED**、または **STALE** ステータスにあるワークフローインスタンスに対して実行します。

   1. `https://[server]:[port]/aem/start.html` にアクセスして、管理者の資格情報を使用してログインします。
   1. に移動します。 **[!UICONTROL ツール/ワークフロー/インスタンス]**.
   1. ユーザーに関連するワークフローインスタンスを選択してをタップします **[!UICONTROL 終了]** ：実行中のインスタンスを終了します。

   ワークフローインスタンスの操作方法について詳しくは、[ワークフローインスタンスの管理](/help/sites-administering/workflows-administering.md)を参照してください。

1. CRXDE Liteコンソールに移動し、ワークフローインスタンスのペイロードパスに移動して、 `payload` ノード。
1. ワークフローインスタンスのドラフトパスに移動して、`draft` ノードを削除します。
1. ワークフローインスタンスの履歴パスに移動して、`history` ノードを削除します。
1. ワークフローインスタンスのワークフローインスタンスパスに移動して、ワークフローの `[workflow-instance-ID]` ノードを削除します。

   >[!NOTE]
   >
   >ワークフローインスタンスノードを削除すると、すべてのワークフロー参加者のワークフローインスタンスが削除されます。

1. ユーザーに対して識別されたすべてのワークフローインスタンスに対して、手順 2 ～ 6 を繰り返します。
1. ワークフロー参加者のAEM Formsアプリの送信トレイからオフラインのドラフトおよび送信データを特定して削除し、サーバーに送信されないようにします。

また、API を使用してノードやプロパティにアクセスし、削除することもできます。 詳しくは、次のドキュメントを参照してください。

* [AEM JCR へのプログラムからのアクセス方法](/help/sites-developing/access-jcr.md)
* [ノードおよびプロパティの削除](https://docs.adobe.com/docs/en/spec/jcr/2.0/10_Writing.html#10.9%20Removing%20Nodes%20and%20Properties)
* [API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)
