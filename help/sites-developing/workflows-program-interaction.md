---
title: プログラムによるワークフローとのやり取り
description: ワークフローを管理する方法、および API とスクリプトを使用したプログラムによるワークフローの操作方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: extending-aem
content-type: reference
exl-id: da06850a-c4d5-44dd-b572-771e3b2a66c5
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2015'
ht-degree: 56%

---

# プログラムによるワークフローとのやり取り{#interacting-with-workflows-programmatically}

[ワークフローをカスタマイズおよび拡張する](/help/sites-developing/workflows-customizing-extending.md)際は、以下の方法でワークフローオブジェクトにアクセスできます。

* [ワークフロー Java API の使用](#using-the-workflow-java-api)
* [ECMA スクリプトでのワークフローオブジェクトの取得](#obtaining-workflow-objects-in-ecma-scripts)
* [ワークフロー REST API の使用](#using-the-workflow-rest-api)

## ワークフロー Java API の使用 {#using-the-workflow-java-api}

ワークフロー Java API は、[`com.adobe.granite.workflow`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/package-summary.html) パッケージといくつかのサブパッケージで構成されます。この API の最も重要な構成要素は、`com.adobe.granite.workflow.WorkflowSession` クラスです。`WorkflowSession` クラスは、デザイン時と実行時に、次のワークフローオブジェクトへのアクセスを可能にします。

* ワークフローモデル
* 作業項目
* ワークフローインスタンス
* ワークフローデータ
* インボックス項目

このクラスは、ワークフローのライフサイクルに介入するためのメソッドもいくつか提供します。

以下の表に、プログラムによってワークフローとやり取りする際に使用するいくつかの重要な Java オブジェクトの参照ドキュメントへのリンクを示します。以降の例では、コード内でクラスオブジェクトを取得および使用する方法を示します。

| 機能 | オブジェクト |
|---|---|
| ワークフローへのアクセス | [`WorkflowSession`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html) |
| ワークフローインスタンスの実行とクエリー | [`Workflow`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)</br>[`WorkItem`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkItem.html)</br>[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) |
| ワークフローモデルの管理 | [`WorkflowModel`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html)</br>[`WorkflowNode`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html)</br>[`WorkflowTransition`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html) |
| ワークフロー内（またはそれ以外）のノードに関する情報 | [`WorkflowStatus`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) |

## ECMA スクリプトでのワークフローオブジェクトの取得 {#obtaining-workflow-objects-in-ecma-scripts}

[スクリプトの設置](/help/sites-developing/the-basics.md#locating-the-script)で説明したように、AEM は、サーバー側 ECMA スクリプトを実行する ECMA スクリプトエンジンを（Apache Sling を通じて）提供します。[`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html) クラスは、`sling` 変数としてスクリプトで直ちに使用できます。

`ScriptHelper` クラスは、`SlingHttpServletRequest` へのアクセスを可能にします。これを使用することによって、最終的に `WorkflowSession` オブジェクトを取得できます。以下に例を示します。

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## ワークフロー REST API の使用 {#using-the-workflow-rest-api}

ワークフローコンソールでは、REST API を大量に利用します。このページでは、ワークフローの REST API について説明します。

>[!NOTE]
>
>curl コマンドラインツールを使用すると、Workflow REST API を使用して、ワークフローオブジェクトにアクセスし、インスタンスのライフサイクルを管理できます。 このページの例では、curl コマンドラインツールから REST API を使用する方法を示します。

REST API では、次のアクションがサポートされています。

* ワークフローサービスを開始または停止
* ワークフローモデルの作成、更新、削除
* [ワークフローインスタンスの起動、休止、再開、終了](/help/sites-administering/workflows.md#workflow-status-and-actions)
* 作業項目の完了、委任

>[!NOTE]
>
>Web 開発用の Firefox の拡張機能である Firebug を使用すると、コンソールの操作時に HTTP トラフィックを追跡できます。例えば、`POST` リクエストにより AEM サーバーに送信されたパラメーターと値を確認できます。

このページでは、AEMが localhost のポートで実行されていると想定しています。 `4502` インストールコンテキストが `/`&quot; （ルート）と呼ばれます。 実際のインストール状況が異なる場合は、HTTP リクエストが適用される URI を実際の状況に合わせて変更してください。

`GET` リクエストに対応するレンダリングは JSON レンダリングです。の URL `GET` が `.json` 拡張子。例：

`http://localhost:4502/etc/workflow.json`

### ワークフローインスタンスの管理 {#managing-workflow-instances}

以下の HTTP リクエストメソッドが、次の URL に適用されます。

`http://localhost:4502/etc/workflow/instances`

<table> 
 <tbody> 
  <tr> 
   <td>HTTP リクエストメソッド</td> 
   <td>アクション</td> 
  </tr> 
  <tr> 
   <td><code>GET</code></td> 
   <td>使用可能なワークフローインスタンスをリストします。</td> 
  </tr> 
  <tr> 
   <td><code>POST</code></td> 
   <td><p>新しいワークフローインスタンスを作成します。パラメーターを以下に示します。<br /> - <code>model</code>:各ワークフローモデルの ID (URI)<br /> - <code>payloadType</code>:ペイロードのタイプを含む ( 例： <code>JCR_PATH</code> または URL)。<br /> ペイロードはパラメーターとして送信されます <code>payload</code>. A <code>201</code> (<code>CREATED</code>) 応答が返され、新しいワークフローインスタンスリソースの URL が格納された場所ヘッダーが返されます。</p> </td> 
  </tr> 
 </tbody> 
</table>

#### 状態によるワークフローインスタンスの管理 {#managing-a-workflow-instance-by-its-state}

以下の HTTP リクエストメソッドが、次の URL に適用されます。

`http://localhost:4502/etc/workflow/instances.{state}`

| HTTP リクエストメソッド | アクション |
|---|---|
| `GET` | 使用可能なワークフローインスタンスとその状態 ( `RUNNING`, `SUSPENDED`, `ABORTED` または `COMPLETED`) |

#### ID によるワークフローインスタンスの管理 {#managing-a-workflow-instance-by-its-id}

以下の HTTP リクエストメソッドが、次の URL に適用されます。

`http://localhost:4502/etc/workflow/instances/{id}`

<table> 
 <tbody> 
  <tr> 
   <td>HTTP リクエストメソッド</td> 
   <td>アクション</td> 
  </tr> 
  <tr> 
   <td><code>GET</code></td> 
   <td>それぞれのワークフローモデルへのリンクを含むインスタンスデータ（定義とメタデータ）を取得します。</td> 
  </tr> 
  <tr> 
   <td><code>POST</code></td> 
   <td>インスタンスの状態を変更します。新しい状態がパラメーターとして送信されます <code>state</code> とは、次のいずれかの値を持つ必要があります。 <code>RUNNING</code>, <code>SUSPENDED</code>または <code>ABORTED</code>.<br /> 新しい状態にアクセスできない場合（終了したインスタンスを休止する場合など）、 <code>409</code> (<code>CONFLICT</code>) 応答がクライアントに送り返されます。</td> 
  </tr> 
 </tbody> 
</table>

### ワークフローモデルの管理 {#managing-workflow-models}

以下の HTTP リクエストメソッドが、次の URL に適用されます。

`http://localhost:4502/etc/workflow/models`

<table> 
 <tbody> 
  <tr> 
   <td>HTTP リクエストメソッド</td> 
   <td>アクション</td> 
  </tr> 
  <tr> 
   <td><code>GET</code></td> 
   <td>使用可能なワークフローモデルを一覧表示します。</td> 
  </tr> 
  <tr> 
   <td><code>POST</code></td> 
   <td>新しいワークフローモデルを作成します. パラメーター <code>title</code> が送信されると、指定されたタイトルで新しいモデルが作成されます。 JSON モデル定義をパラメーターとして添付する <code>model</code> 指定された定義に従って、新しいワークフローモデルを作成します。<br /> A <code>201</code> 応答 (<code>CREATED</code>) は、新しいワークフローモデルリソースの URL を含む場所ヘッダーと共に返されます。<br /> 同じことが、モデル定義が <code>modelfile</code>.<br /> どちらの場合も <code>model</code> および <code>modelfile</code> パラメータ、名前を付けた追加パラメータ <code>type</code> シリアル化形式を定義するには、が必要です。 新しいシリアル化フォーマットは、OSGI API を使用して統合できます。標準の JSON シリアライザーは、ワークフローエンジンに付属しています。そのタイプは JSON です。フォーマットの例は、以下を参照してください。</td> 
  </tr> 
 </tbody> 
</table>

例：ブラウザーで、 `http://localhost:4502/etc/workflow/models.json` は、次のような json 応答を生成します。

```
[
    {"uri":"/var/workflow/models/activationmodel"}
    ,{"uri":"/var/workflow/models/dam/adddamsize"}
    ,{"uri":"/var/workflow/models/cloudconfigs/dtm-reactor/library-download"}
    ,{"uri":"/var/workflow/models/ac-newsletter-workflow-simple"}
    ,{"uri":"/var/workflow/models/dam/dam-create-language-copy"}
    ,{"uri":"/var/workflow/models/dam/dam-create-and-translate-language-copy"}
    ,{"uri":"/var/workflow/models/dam-indesign-proxy"}
    ,{"uri":"/var/workflow/models/dam-xmp-writeback"}
    ,{"uri":"/var/workflow/models/dam-parse-word-documents"}
    ,{"uri":"/var/workflow/models/dam/process_subasset"}
    ,{"uri":"/var/workflow/models/dam/dam_set_last_modified"}
    ,{"uri":"/var/workflow/models/dam/dam-autotag-assets"}
    ,{"uri":"/var/workflow/models/dam/update_asset"}
    ,{"uri":"/var/workflow/models/dam/update_asset_offloading"}
    ,{"uri":"/var/workflow/models/dam/dam-update-language-copy"}
    ,{"uri":"/var/workflow/models/dam/update_from_lightbox"}
    ,{"uri":"/var/workflow/models/cloudservices/DTM_bundle_download"}
    ,{"uri":"/var/workflow/models/dam/dam_download_asset"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-encode-video"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-thumbnail-replacement"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-user-uploaded-thumbnail"}
    ,{"uri":"/var/workflow/models/newsletter_bounce_check"}
    ,{"uri":"/var/workflow/models/projects/photo_shoot_submission"}
    ,{"uri":"/var/workflow/models/projects/product_photo_shoot"}
    ,{"uri":"/var/workflow/models/projects/approval_workflow"}
    ,{"uri":"/var/workflow/models/prototype-01"}
    ,{"uri":"/var/workflow/models/publish_example"}
    ,{"uri":"/var/workflow/models/publish_to_campaign"}
    ,{"uri":"/var/workflow/models/screens/publish_to_author_bin"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_publish_to_youtube"}
    ,{"uri":"/var/workflow/models/projects/request_copy"}
    ,{"uri":"/var/workflow/models/projects/request_email"}
    ,{"uri":"/var/workflow/models/projects/request_landing_page"}
    ,{"uri":"/var/workflow/models/projects/request_launch"}
    ,{"uri":"/var/workflow/models/request_for_activation"}
    ,{"uri":"/var/workflow/models/request_for_deactivation"}
    ,{"uri":"/var/workflow/models/request_for_deletion"}
    ,{"uri":"/var/workflow/models/request_for_deletion_without_deactivation"}
    ,{"uri":"/var/workflow/models/request_to_complete_move_operation"}
    ,{"uri":"/var/workflow/models/reverse_replication"}
    ,{"uri":"/var/workflow/models/salesforce-com-export"}
    ,{"uri":"/var/workflow/models/scene7"}
    ,{"uri":"/var/workflow/models/scheduled_activation"}
    ,{"uri":"/var/workflow/models/scheduled_deactivation"}
    ,{"uri":"/var/workflow/models/screens/screens-update-asset"}
    ,{"uri":"/var/workflow/models/translation"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_remove_from_youtube"}
    ,{"uri":"/var/workflow/models/wcm-translation/create_language_copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/prepare_translation_project"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-i18n-dictionary"}
    ,{"uri":"/var/workflow/models/wcm-translation/sync_translation_job"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-language-copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/update_language_copy"}
]
```

#### 特定のワークフローモデルの管理 {#managing-a-specific-workflow-model}

以下の HTTP リクエストメソッドが、次の URL に適用されます。

`http://localhost:4502*{uri}*`

ここで、 `*{uri}*` は、リポジトリ内のモデルノードへのパスです。

<table> 
 <tbody> 
  <tr> 
   <td>HTTP リクエストメソッド</td> 
   <td>アクション</td> 
  </tr> 
  <tr> 
   <td><code>GET</code></td> 
   <td>を取得します <code>HEAD</code> モデルのバージョン（定義とメタデータ）。</td> 
  </tr> 
  <tr> 
   <td><code>PUT</code></td> 
   <td>を更新します。 <code>HEAD</code> モデルのバージョン（新しいバージョンを作成します）。<br /> モデルの新しいバージョンの完全なモデル定義は、という名前のパラメーターとして追加する必要があります。 <code>model</code>. さらに、 <code>type</code> 新しいモデルを作成する際にはパラメーターが必要で、値を持つ必要があります。 <code>JSON</code>.<br /> </td> 
  </tr> 
  <tr> 
   <td><code>POST</code></td> 
   <td>PUT の場合と同じ動作です。AEMウィジェットがサポートされていないので、必要です <code>PUT</code> 操作。</td> 
  </tr> 
  <tr> 
   <td><code>DELETE</code></td> 
   <td>モデルを削除します。ファイアウォール/プロキシの問題を解決するには、 <code>POST</code> を含む <code>X-HTTP-Method-Override</code> 値を持つヘッダーエントリ <code>DELETE</code> は、 <code>DELETE</code> リクエスト。</td> 
  </tr> 
 </tbody> 
</table>

例：ブラウザーで、 `http://localhost:4502/var/workflow/models/publish_example.json` は `json` 次のコードに似た応答を返します。

```shell
{
  "id":"/var/workflow/models/publish_example",
  "title":"Publish Example",
  "version":"1.0",
  "description":"This example shows a simple review and publish process.",
  "metaData": 
  {
    "multiResourceSupport":"true",
    "tags":"wcm,publish"
  },
  "nodes":
  [{
    "id":"node0",
    "type":"START",
    "title":"Start",
    "description":"The start node of the workflow.",
    "metaData":
    {
    }
  },
  {
    "id":"node1",
    "type":"PARTICIPANT",
    "title":"Validate Content",
    "description":"Validate the modified content.",
    "metaData":
    {
      "PARTICIPANT":"admin"
    }
  },
  {
    "id":"node2",
    "type":"PROCESS",
    "title":"Publish Content",
    "description":"Publish the modified content.",
    "metaData":
    {
      "PROCESS_AUTO_ADVANCE":"true",
      "PROCESS":"com.day.cq.wcm.workflow.process.ActivatePageProcess"
    }
  },
  {
    "id":"node3",
    "type":"END",
    "title":"End",
    "description":"The end node of the workflow.",
    "metaData":
    {
    }
  }],
  "transitions":
  [{
    "from":"node0",
    "to":"node1",
    "metaData":
    {
    }
  },
  {
    "from":"node1",
    "to":"node2",
    "metaData":
    {
    }
  },
  {
    "from":"node2",
    "to":"node3",
    "metaData":
    {
    }
  }
]}
```

#### バージョンによるワークフローモデルの管理 {#managing-a-workflow-model-by-its-version}

以下の HTTP リクエストメソッドが、次の URL に適用されます。

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| HTTP リクエストメソッド | アクション |
|---|---|
| `GET` | 指定されたバージョンのモデルのデータを取得します（存在する場合）。 |

### （ユーザーの）インボックスの管理 {#managing-user-inboxes}

以下の HTTP リクエストメソッドが、次の URL に適用されます。

`http://localhost:4502/bin/workflow/inbox`

<table> 
 <tbody> 
  <tr> 
   <td>HTTP リクエストメソッド</td> 
   <td>アクション</td> 
  </tr> 
  <tr> 
   <td><code>GET</code></td> 
   <td>ユーザーのインボックスにある作業項目を一覧表示します。ユーザーは、HTTP 認証ヘッダーによって識別されます。</td> 
  </tr> 
  <tr> 
   <td><code>POST</code></td> 
   <td>URI がパラメーターとして送信される作業項目を完了します <code>item</code> に従って、ワークフローインスタンスを、パラメーターで定義された次のノードに進めます。 <code>route</code> または <code>backroute</code> 一歩下がる時に<br /> パラメーター <code>delegatee</code> が送信されると、パラメーターで識別される作業項目が送信されます。 <code>item</code> は指定した参加者に委任されます。</td> 
  </tr> 
 </tbody> 
</table>

#### WorkItem ID による（ユーザーの）インボックスの管理 {#managing-a-user-inbox-by-the-workitem-id}

以下の HTTP リクエストメソッドが、次の URL に適用されます。

`http://localhost:4502/bin/workflow/inbox/{id}`

| HTTP リクエストメソッド | アクション |
|---|---|
| `GET` | インボックスのデータ（定義とメタデータ）を取得します `WorkItem` は、ID で識別されます。 |

## 例 {#examples}

### 実行中のすべてのワークフローとその ID のリストを取得する方法 {#how-to-get-a-list-of-all-running-workflows-with-their-ids}

実行中のすべてのワークフローのリストを取得するには、次の URL に対して GET を実行します。

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### 実行中のすべてのワークフローとその ID のリストを取得する方法 - curl を使用した REST {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}

curl を使用した例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

この `uri` 結果に表示されるは、インスタンスとして使用できます `id` 他のコマンドで例：

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>この `curl` コマンドは、任意の [ワークフローのステータス](/help/sites-administering/workflows.md#workflow-status-and-actions) 代わりに `RUNNING`.

### ワークフローのタイトルを変更する方法 {#how-to-change-the-workflow-title}

ワークフローコンソールの「**インスタンス**」タブに表示されている&#x200B;**ワークフローのタイトル**&#x200B;を変更するには、次のように `POST` コマンドを送信します。

* を: `http://localhost:4502/etc/workflow/instances/{id}`

* 使用するパラメーター：

   * `action`:値は次のとおりです。 `UPDATE`
   * `workflowTitle`:ワークフローのタイトル

#### ワークフローのタイトルを変更する方法 - curl を使用した REST {#how-to-change-the-workflow-title-rest-using-curl}

curl を使用した例：

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### すべてのワークフローモデルを一覧表示する方法 {#how-to-list-all-workflow-models}

使用可能なすべてのワークフローモデルのリストを取得するには、次の URL に対して GET を実行します。

`http://localhost:4502/etc/workflow/models.json`

#### すべてのワークフローモデルを一覧表示する方法 - curl を使用した REST {#how-to-list-all-workflow-models-rest-using-curl}

curl を使用した例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>関連トピック [ワークフローモデルの管理](#managing-workflow-models).

### WorkflowSession オブジェクトの取得 {#obtaining-a-workflowsession-object}

この `com.adobe.granite.workflow.WorkflowSession` クラスはから適応可能です `javax.jcr.Session` オブジェクトまたは `org.apache.sling.api.resource.ResourceResolver` オブジェクト。

#### WorkflowSession オブジェクトの取得 - Java {#obtaining-a-workflowsession-object-java}

JSP スクリプト（またはサーブレットクラスの Java コード）で、HTTP リクエストオブジェクトを使用して `SlingHttpServletRequest` オブジェクトを取得します。これにより、`ResourceResolver` オブジェクトへのアクセスが可能になります。を適応させる `ResourceResolver` 対して `WorkflowSession`.

```java
<%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" 
    import="com.adobe.granite.workflow.WorkflowSession,
  org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
%>
```

#### WorkflowSession オブジェクトの取得 - ECMA スクリプト {#obtaining-a-workflowsession-object-ecma-script}

`sling``SlingHttpServletRequest` 変数を使用して、 オブジェクトの取得に使用する オブジェクトを取得します。`ResourceResolver`を適応させる `ResourceResolver` オブジェクトを `WorkflowSession` オブジェクト。

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### ワークフローモデルの作成、読み取り、削除 {#creating-reading-or-deleting-workflow-models}

以下の例では、ワークフローモデルにアクセスする方法を説明しています。

* Java および ECMA スクリプトコードは、`WorkflowSession.createNewModel` メソッドを使用します。
* curl コマンドは、モデルの URL を使用してモデルに直接アクセスします。

例では以下を実行します。

1. ID を持つモデルの作成 `/var/workflow/models/mymodel/jcr:content/model`) をクリックします。
1. モデルを削除します。

>[!NOTE]
>
>モデルを削除すると、 `deleted` モデルの `metaData` 子ノードから `true`.
>
>モデルを削除しても、モデルノードは削除されません。

新しいモデルを作成する場合：

* ワークフローモデルエディターでは、モデルが以下の特定のノード構造を使用する必要があります `/var/workflow/models`. モデルの親ノードはタイプである必要があります `cq:Page` 持つ `jcr:content` 次のプロパティ値を持つノード。

   * `sling:resourceType`: `cq/workflow/components/pages/model`
   * `cq:template`: `/libs/cq/workflow/templates/model`

   モデルを作成する際は、まずこの `cq:Page` ノードを作成し、その `jcr:content` ノードを model ノードの親として使用する必要があります。

* この `id` 一部のメソッドでモデルを識別するために必要な引数は、リポジトリ内の model ノードの絶対パスです。

   `/var/workflow/models/<*model_name>*/jcr:content/model`

   >[!NOTE]
   >
   >詳しくは、 [すべてのワークフローモデルのリストを作成する方法](#how-to-list-all-workflow-models).

#### ワークフローモデルの作成、読み取り、削除 - Java {#creating-reading-or-deleting-workflow-models-java}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" import="com.adobe.granite.workflow.WorkflowSession,
                 com.adobe.granite.workflow.model.WorkflowModel,
             org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
/* Create the parent page */
String modelRepo = new String("/var/workflow/models");
String modelTemplate = new String ("/libs/cq/workflow/templates/model");
String modelName = new String("mymodel");
Page modelParent = pageManager.create(modelRepo, modelName, modelTemplate, "My workflow model");

/* create the model */
String modelId = new String(modelParent.getPath()+"/jcr:content/model")
WorkflowModel model = wfSession.createNewModel("Made using Java",modelId);

/* delete the model */
wfSession.deleteModel(modelId);
%>
```

#### ワークフローモデルの作成、読み取り、削除 - ECMA スクリプト {#creating-reading-or-deleting-workflow-models-ecma-script}

```
var resolver = sling.getRequest().getResource().getResourceResolver();
var wfSession = resolver.adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
var pageManager = resolver.adaptTo(Packages.com.day.cq.wcm.api.PageManager);

//create the parent page node
var workflowPage = pageManager.create("/var/workflow/models", "mymodel", "/libs/cq/workflow/templates/model", "Created via ECMA Script");
var modelId = workflowPage.getPath()+ "/jcr:content/model";
//create the model
var model = wfSession.createNewModel("My Model", modelId);
//delete the model
var model = wfSession.deleteModel(modelId);
```

#### ワークフローモデルの削除 - curl を使用した REST {#deleting-a-workflow-model-rest-using-curl}

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>必要な詳細のレベルを考慮した結果、curl はモデルの作成や読み取りに使用できないと見なされています。

### ワークフローの状態の確認時のシステムワークフローの除外 {#filtering-out-system-workflows-when-checking-workflow-status}

以下を使用して、 [WorkflowStatus API](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) ：ノードのワークフローステータスに関する情報を取得します。

各種メソッドには次のパラメーターがあります。

`excludeSystemWorkflows`

このパラメーターは、 `true` をクリックして、関連する結果からシステムワークフローを除外する必要があることを示します。

あなた [OSGi 設定を更新できます。](/help/sites-deploying/configuring-osgi.md) **AdobeGranite ワークフロー PayloadMapCache** ワークフローを指定する `Models` をシステムワークフローと見なします。 デフォルト（実行時）のワークフローモデルを以下に示します。

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### タイムアウト後に参加者ステップを自動的に進める {#auto-advance-participant-step-after-a-timeout}

事前定義した時間内に終了しなかった&#x200B;**参加者**&#x200B;ステップを自動的に進める必要がある場合は、以下の手順を実行します。

1. OSGI イベントリスナーを実装して、タスクの作成と変更をリスンします。
1. タイムアウト（期限）を指定し、その時点で実行されるようにスケジュールされた sling ジョブを作成します。
1. タイムアウトになり、ジョブが実行されるときに通知されるジョブハンドラーを作成します。

   このハンドラーは、タスクがまだ完了していない場合に、タスクに対して必要なアクションを実行します。

>[!NOTE]
>
>実行するアクションは、この手法を使用できるよう明確に定義されている必要があります。

### ワークフローインスタンスとのやり取り {#interacting-with-workflow-instances}

（プログラムによって）ワークフローインスタンスとやり取りする方法について、以下に基本的な例を示します。

#### ワークフローインスタンスとのやり取り - Java {#interacting-with-workflow-instances-java}

```java
// starting a workflow
WorkflowModel model = wfSession.getModel(workflowId);
WorkflowData wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
Workflow[] workflows workflows = wfSession.getAllWorkflows();
Workflow workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### ワークフローインスタンスとのやり取り - ECMA スクリプト {#interacting-with-workflow-instances-ecma-script}

```
// starting a workflow
var model = wfSession.getModel(workflowId);
var wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
var workflows = wfSession.getWorkflows(“RUNNING“);
var workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### ワークフローインスタンスとのやり取り - curl を使用した REST {#interacting-with-workflow-instances-rest-using-curl}

* **ワークフローの開始**

   ```shell
   # starting a workflow
   curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
   
   # for example:
   curl -u admin:admin -d "model=/var/workflow/models/request_for_activation&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
   ```

* **インスタンスの一覧表示**

   ```shell
   # listing the instances
   curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
   ```

   これにより、すべてのインスタンスが一覧表示されます。以下に例を示します。

   ```shell
   [
       {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
       ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
   ]
   ```

   >[!NOTE]
   >
   >詳しくは、 [実行中のすべてのワークフローのリストを取得する方法](#how-to-get-a-list-of-all-running-workflows-with-their-ids) を使用して、特定のステータスのインスタンスを一覧表示するためのもの。

* **ワークフローの休止**

   ```shell
   # suspending a workflow
   curl -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

* **ワークフローの再開**

   ```shell
   # resuming a workflow
   curl -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

* **ワークフローインスタンスの終了**

   ```shell
   # terminating a workflow
   curl -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

### 作業項目とのやり取り {#interacting-with-work-items}

（プログラムによって）作業項目とやり取りする方法について、以下に基本的な例を示します。

#### 作業項目とのやり取り - Java {#interacting-with-work-items-java}

```java
// querying work items
WorkItem[] workItems = wfSession.getActiveWorkItems();
WorkItem workItem = wfSession.getWorkItem(id);

// getting routes
List<Route> routes = wfSession.getRoutes(workItem);

// delegating
Iterator<Participant> delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### 作業項目とのやり取り - ECMA スクリプト {#interacting-with-work-items-ecma-script}

```
// querying work items
var workItems = wfSession.getActiveWorkItems();
var workItem = wfSession.getWorkItem(id);

// getting routes
var routes = wfSession.getRoutes(workItem);

// delegating
var delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### 作業項目とのやり取り - curl を使用した REST {#interacting-with-work-items-rest-using-curl}

* **インボックスの作業項目の一覧表示**

   ```shell
   # listing the work items
   curl -u admin:admin http://localhost:4502/bin/workflow/inbox
   ```

   現在インボックス内にある作業項目の詳細が一覧表示されます。以下に例を示します。

   ```shell
   [{
       "uri_xss": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
       "uri": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
       "currentAssignee_xss": "workflow-administrators",
       "currentAssignee": "workflow-administrators",
       "startTime": 1519656289274,
       "payloadType_xss": "JCR_PATH",
       "payloadType": "JCR_PATH",
       "payload_xss": "/content/we-retail/es/es",
       "payload": "/content/we-retail/es/es",
       "comment_xss": "Process resource is null",
       "comment": "Process resource is null",
       "type_xss": "WorkItem",
       "type": "WorkItem"
     },{
       "uri_xss": "configuration/configure_analyticstargeting",
       "uri": "configuration/configure_analyticstargeting",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/securitychecklist",
       "uri": "configuration/securitychecklist",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/enable_collectionofanonymoususagedata",
       "uri": "configuration/enable_collectionofanonymoususagedata",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/configuressl",
       "uri": "configuration/configuressl",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     }
   ```

* **作業項目の委任**

   ```xml
   # delegating
   curl -d "item={item}&delegatee={delegatee}" http://localhost:4502/bin/workflow/inbox
   
   # for example: 
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_act_1&delegatee=administrators" http://localhost:4502/bin/workflow/inbox
   ```

   >[!NOTE]
   >
   >`delegatee` は、ワークフローステップに有効なオプションである必要があります。

* **作業項目を完了する、または次のステップに進める**

   ```xml
   # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
   http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
   
   # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
   curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
   ```

### ワークフローイベントのリスン {#listening-for-workflow-events}

OSGi イベントフレームワークを使用して、[`com.adobe.granite.workflow.event.WorkflowEvent` クラスが定義するイベントをリスンします。](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html)このクラスは、イベントの対象に関する情報を取得するのに役立ついくつかのメソッドも提供します。例えば、`getWorkItem` メソッドは、イベントに関与する作業項目の `WorkItem` オブジェクトを返します。

次のサンプルコードでは、ワークフローイベントをリスンし、イベントのタイプに応じてタスクを実行するサービスを定義しています。

```java
package com.adobe.example.workflow.listeners;

import org.apache.sling.event.jobs.JobProcessor;
import org.apache.sling.event.jobs.JobUtil;

import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import com.adobe.granite.workflow.event.WorkflowEvent;
import com.adobe.granite.workflow.exec.WorkItem;

/**
 * The <code>WorkflowEventCatcher</code> class listens to workflow events. 
 */
@Component(metatype=false, immediate=true)
@Service(value=org.osgi.service.event.EventHandler.class)
public class WorkflowEventCatcher implements EventHandler, JobProcessor {

 @Property(value=com.adobe.granite.workflow.event.WorkflowEvent.EVENT_TOPIC)
 static final String EVENT_TOPICS = "event.topics";

 private static final Logger logger = LoggerFactory.getLogger(WorkflowEventCatcher.class);

 public void handleEvent(Event event) {
  JobUtil.processJob(event, this);
 }

 public boolean process(Event event) {
  logger.info("Received event of topic: " + event.getTopic());
  String topic = event.getTopic();

  try {
   if (topic.equals(WorkflowEvent.EVENT_TOPIC)) {
    WorkflowEvent wfevent = (WorkflowEvent)event;
    String eventType = wfevent.getEventType();
    String instanceId = wfevent.getWorkflowInstanceId();

    if (instanceId != null) {
     //workflow instance events
     if (eventType.equals(WorkflowEvent.WORKFLOW_STARTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_RESUMED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_SUSPENDED_EVENT)) {
      // your code comes here...
     } else if (
       eventType.equals(WorkflowEvent.WORKFLOW_ABORTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_COMPLETED_EVENT)) {
      // your code comes here...
     }
     // workflow node event
     if (eventType.equals(WorkflowEvent.NODE_TRANSITION_EVENT)) {
      WorkItem currentItem = (WorkItem) event.getProperty(WorkflowEvent.WORK_ITEM);
      // your code comes here...
     }
    }
   }
  } catch(Exception e){
   logger.debug(e.getMessage());
   e.printStackTrace();
  }
  return true;
 }
}
```
