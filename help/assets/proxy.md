---
title: Assets のプロキシ開発
description: 'プロキシは、プロキシワーカーを使用してジョブを処理する  [!DNL Experience Manager]  インスタンスです。 [!DNL Experience Manager] プロキシ、サポートされている操作、プロキシコンポーネントを設定する方法、カスタムプロキシワーカーを開発する方法について説明します。 '
contentOwner: AG
feature: Asset Processing
role: Admin, Architect
exl-id: c7511326-697e-4749-ab46-513cdbaa00d8
source-git-commit: a778c3bbd0e15bb7b6de2d673b4553a7bd146143
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 75%

---

# Assets のプロキシ開発 {#assets-proxy-development}

Adobe Experience Manager Assets では、プロキシを使用して、特定のタスクの処理を配布します。

プロキシは、特定の（場合によっては別の）ものです [!DNL Experience Manager] ジョブの処理と結果の作成を担当するプロセッサーとしてプロキシワーカーを使用するインスタンス。 プロキシワーカーは、幅広いタスクに使用できます。の場合、 [!DNL Experience Manager] アセットプロキシ — 内でレンダリングするアセットの読み込みに使用できます。 [!DNL Experience Manager] アセット。 例えば、[IDS プロキシワーカー](indesign.md)は、InDesign Server を使用して、 Assets 内で使用できるようにファイルを処理します。[!DNL Experience Manager]

プロキシが個別の [!DNL Experience Manager] インスタンスである場合は、[!DNL Experience Manager] オーサリングインスタンスの負荷の軽減に役立ちます。デフォルトでは、 [!DNL Experience Manager] Assets は、同じ JVM（プロキシ経由で外部化）でアセット処理タスクを実行し、 [!DNL Experience Manager] オーサリングインスタンス。

## プロキシ（HTTP アクセス） {#proxy-http-access}

プロキシは、次の場所でのジョブの処理を受け入れるよう設定されている場合に、HTTP Servlet を介して使用できます。 `/libs/dam/cloud/proxy`. このサーブレットは、POST されたパラメーターから Sling ジョブを作成します。作成されたジョブはプロキシのジョブキューに追加され、適切なプロキシワーカーに接続されます。

### サポートされている操作 {#supported-operations}

* `job`

   **要件**：パラメーター `jobevent` をシリアル化されたバリューマップとして設定する必要があります。ジョブプロセッサー用の `Event` の作成に使用します。

   **結果**：新しいジョブが追加されます。成功した場合、一意のジョブ ID が返されます。

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **要件**：パラメーター `jobid` を設定する必要があります。

   **結果**：ジョブプロセッサーによって作成されたノードの JSON 表現が返されます。

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **要件**：パラメーター jobid を設定する必要があります。

   **結果**：指定されたジョブに関連付けられているリソースが返されます。

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **要件**：パラメーター jobid を設定する必要があります。

   **結果**：見つかった場合にジョブが削除されます。

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### プロキシワーカー {#proxy-worker}

プロキシワーカーは、ジョブの処理および結果の作成を担当するプロセッサーです。ワーカーはプロキシインスタンスにあり、プロキシワーカーとして認識されるには、[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) を実装する必要があります。

>[!NOTE]
>
>ワーカーがプロキシワーカーとして認識されるには、[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) を実装する必要があります。

### クライアント API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/index.html) は、ジョブを作成および削除し、ジョブの結果を取得するためのメソッドを提供する OSGi サービスとして使用できます。このサービスのデフォルトの実装（`JobServiceImpl`）は、HTTP クライアントを使用して、リモートプロキシサーブレットと通信します。

API の使用例を以下に示します。

```java
@Reference
 JobService proxyJobService;

 // to create a new job
 final Hashtable props = new Hashtable();
 props.put("someproperty", "some value");
 props.put(JobUtil.PROPERTY_JOB_TOPIC, "myworker/job"); // this is an identifier of the worker
 final String jobId = proxyJobService.addJob(props, new Asset[]{asset});

 // to check status (returns JobService.STATUS_FINISHED or JobService.STATUS_INPROGRESS)
 int status = proxyJobService.getStatus(jobId)

 // to get the result
 final String jsonString = proxyJobService.getResult(jobId);

 // to remove job and cleanup
 proxyJobService.removeJob(jobId);
```

### クラウドサービスの設定 {#cloud-service-configurations}

>[!NOTE]
>
>プロキシ API の参考ドキュメントは、[`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/commons/proxy/package-summary.html) にあります。

プロキシとプロキシワーカーの両方の設定は、クラウドサービスの設定を通じて使用できます。クラウドサービスの設定は、 [!DNL Experience Manager] Assets **ツール** コンソールまたは `/etc/cloudservices/proxy`. 各プロキシワーカーは、 ワーカーに固有の設定の詳細 （例： `/etc/cloudservices/proxy/workername`）で、`/etc/cloudservices/proxy` にノードを追加するように想定されています。

>[!NOTE]
>
>詳しくは、[InDesign Server プロキシワーカーの設定](indesign.md#configuring-the-proxy-worker-for-indesign-server)および[クラウドサービスの設定](../sites-developing/extending-cloud-config.md)を参照してください。

API の使用例を以下に示します。

```java
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;
 
 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### カスタマイズしたプロキシワーカーの開発 {#developing-a-customized-proxy-worker}

この [IDS プロキシワーカー](indesign.md) は、 [!DNL Experience Manager] InDesign アセットの処理をアウトソースするために既に標準で提供されている Assets プロキシワーカー。

独自のを開発および設定することもできます [!DNL Experience Manager] Assets プロキシワーカー：お客様の派遣およびアウトソーシングを行う専門的なワーカーを作成します。 [!DNL Experience Manager] アセット処理タスク。

独自のカスタムプロキシワーカーを設定するには、以下を実行する必要があります。

* 以下を設定および実装します（Sling イベントを使用）。

   * カスタムジョブトピック
   * カスタムジョブイベントハンドラー

* 次に、JobService API を使用して以下を実行します。

   * プロキシへのカスタムジョブのディスパッチ
   * ジョブの管理

* ワークフローからプロキシを使用する場合は、WorkflowExternalProcess API および JobService API を使用して、カスタム外部手順を実装する必要があります。

以下の図および手順に、実行方法の詳細を示します。

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>以下の手順では、参照例として InDesign での該当項目を示しています。

1. [Sling ジョブ](https://sling.apache.org/site/eventing-and-jobs.html)が使用されるので、ユーザーの使用例向けにジョブトピックを定義する必要があります。

   例として、IDS プロキシワーカーの `IDSJob.IDS_EXTENDSCRIPT_JOB` を参照してください。

1. 外部手順を使用してイベントを呼び出し、それが終了するまで待機します。これは、ID をポーリングすることによって実行されます。新機能を実装する独自の手順を開発する必要があります。

   `WorkflowExternalProcess` を実装してから、JobService API およびジョブトピックを使用してジョブイベントを準備し、JobService（OSGi サービス）にディスパッチします。

   例として、IDS プロキシワーカーの `INDDMediaExtractProcess`.java を参照してください。

1. トピックのジョブハンドラーを実装します。特定のアクションを実行し、ワーカー実装と見なされるように、このハンドラーを開発する必要があります。

   例として、IDS プロキシワーカーの `IDSJobProcessor.java` を参照してください。

1. dam-commons の `ProxyUtil.java` を使用します。これにより、DAM プロキシを使用してジョブをワーカーにディスパッチできます。

>[!NOTE]
>
>What [!DNL Experience Manager] Assets プロキシフレームワークには、プールメカニズムが標準で用意されていません。
>
>InDesign 統合によって、InDesign Server のプール（IDSPool）にアクセスできるようになります。このプールは InDesign の統合に固有で、 [!DNL Experience Manager] Assets プロキシフレームワーク。

>[!NOTE]
>
>結果の同期：
>
>同じプロキシを使用するインスタンスが n 個ある場合、処理結果はプロキシに保持されます。これはクライアントのジョブです ([!DNL Experience Manager] オーサー ) を使用して、ジョブの作成時にクライアントに提供されるのと同じ一意のジョブ ID を使用して、結果をリクエストします。 プロキシでは、単にジョブを実行し、リクエストに備えて結果を準備しておくだけです。
