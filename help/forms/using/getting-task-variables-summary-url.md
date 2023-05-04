---
title: サマリー URLでのタスク変数の取得
seo-title: Getting Task Variables in Summary URL
description: タスクに関する情報を再利用し、タスクを要約または説明するサマリ URL を生成する方法。
seo-description: How-to reuse the information about a task and generate a Summary URL to summarize or describe a task.
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
exl-id: f80d006b-6970-4448-aa38-3ffec8b08c18
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 16%

---

# サマリー URLでのタスク変数の取得 {#getting-task-variables-in-summary-url}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

概要ページには、タスクに関する情報が表示されます。 この記事では、サマリーページでタスクに関する情報を再利用する方法について説明します。

このサンプルオーケストレーションでは、従業員は休暇申請フォームを送信します。 申込フォームは、従業員のマネージャーに承認を求めます。

1. resourceType のサンプルHTMLレンダラー (html.esp) を作成します。 **従業員/PtoApplication**.

   レンダラーは、次のプロパティがノードに設定されると仮定します。

   * 名前
   * empid
   * 理由
   * duration

   >[!NOTE]
   >
   >このレンダラーはサマリーページのテンプレートです。

   このレンダラーの以下のサンプルコードは、

   `apps/Employees/PtoApplication/html.esp`

   ```
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. オーケストレーションを変更して、送信されたフォームデータから 4 つのプロパティを抽出します。 その後、CRX にタイプのノードを作成します。 **従業員/PtoApplication**&#x200B;に設定され、プロパティが設定されます。

   1. プロセスの作成 **PTO 概要を作成** を呼び出し、これをサブプロセスとして使用してから **タスクを割り当て** 操作をオーケストレーションで実行します。
   1. **employeeName**、**employeeID**、**ptoReason**、**totalDays** および **nodeName** を新しいプロセスで入力変数として定義します。これらの変数は送信されたフォームデータとして渡されます。

      また、概要 URL の設定時に使用される出力変数**ptoNodePath **も定義します。

   1. 内 **PTO 概要を作成** プロセス、 **値を設定** 入力の詳細を**nodeProperty **(**nodeProps**) マップを使用します。

      このマップのキーは、前の手順でHTMLレンダラーで定義したキーと同じである必要があります。

      また、 **sling:resourceType** 値付きキー **従業員/PtoApplication** をマップに追加します。

   1. サブプロセスの使用 **storeContent** から **ContentRepositoryConnector** サービス **PTO 概要を作成** プロセス。 このサブプロセスは CRX ノードを作成します。

      次の 3 つの入力変数が必要です。

      * **フォルダーパス**:新しい CRX ノードが作成されるパス。 パスを次のように設定します。 **/content**.
      * **ノード名**:入力変数 nodeName をこのフィールドに割り当てます。 これは固有のノード名文字列です。
      * **ノードタイプ**：タイプを **nt:unstructured** として定義します。このプロセスの出力は nodePath です。 nodePath は、新しく作成されたノードの CRX パスです。 ndoePath は、 **PTO を作成** 要約プロセス。
   1. 送信されたフォームデータ (**employeeName**, **employeeID**, **ptoReason**、および **totalDays**) を新しいプロセスへの入力として使用する **PTO 概要を作成**. 出力を次のように取得します。 **ptoSummaryNodePath**.


1. 概要 URL を、サーバーの詳細と共に含まれる XPath 式として定義します **ptoSummaryNodePath**.

   XPath：`concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`。

AEM Forms Workspace で、タスクを開くと、概要 URL が CRX ノードにアクセスし、HTMLレンダラーに概要が表示されます。

概要レイアウトは、プロセスを変更せずに変更できます。 HTMLレンダラーはサマリを適切に表示します。
