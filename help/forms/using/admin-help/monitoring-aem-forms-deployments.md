---
title: AEM Forms のデプロイメントの監視
seo-title: Monitoring AEM forms deployments
description: AEM forms のデプロイメントは、システムレベルと内部レベルの両方で監視できます。 このドキュメントでは、AEM forms のデプロイメントの監視について説明します。
seo-description: You can monitor AEM forms deployments from both a system level and an internal level. Learn more about monitoring AEM forms deployments from this document.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
exl-id: d2cd532b-4086-4553-ac26-f311da6d5ca9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 32%

---

# AEM Forms のデプロイメントの監視 {#monitoring-aem-forms-deployments}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM forms のデプロイメントは、システムレベルと内部レベルの両方で監視できます。 HP OpenView、IBM Tivoli、CA UniCenter、および JMX と呼ばれるサード・パーティ製モニタなど、スペシャリスト管理ツールを使用できます。 *JConsole* を使用して、Java アクティビティを特別に監視します。 監視戦略を実装すると、AEM Forms デプロイメントの可用性、信頼性、パフォーマンスが向上します。

AEM forms のデプロイメントの監視について詳しくは、 [AEM forms デプロイメントの監視に関するテクニカルガイド](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf).

## MBean を使用した監視 {#monitoring-using-mbeans}

AEM forms には、ナビゲーションと統計の情報を提供する 2 つの登録済み MBean が用意されています。 統合および検査でサポートされる MBean は次のみです。

* **ServiceStatistic：**&#x200B;この MBean はサービス名とそのバージョンに関する情報を提供します。
* **OperationStatistic：**&#x200B;この MBean は Forms サーバーのすべてのサービスに関する統計情報を提供します。ここでは、管理者が呼び出し時間やエラー数など、特定のサービスに関する情報を取得できます。

### ServiceStatisticMbean パブリックインターフェイス {#servicestatisticmbean-public-interfaces}

ServiceStatistic MBean の次のパブリックインターフェイスには、テスト目的でアクセスできます。

```as3
 public String getServiceId();  
 public int getMajorVersion();  
 public int getMinorVersion();
```

### OperationStatisticMbean パブリックインターフェイス {#operationstatisticmbean-public-interfaces}

OperationStatistic MBean の次のパブリックインターフェイスには、テスト目的でアクセスできます。

```as3
 // InvocationCount: The number of times the method is invoked.  
 public long getInvocationCount();  
 // InvocationStartTime: The time at which the method started to execute.  
 public long getInvocationStartTime();  
 // InvocationEndTime: The time at which the method finished execution.  
 public long getInvocationEndTime();  
 // InvocationTime: The time taken for the execution of the method.  
 public long getInvocationTime();  
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string  
 public String getLastSamplingDateTime();  
 // MaxInvocationTime: The maximum time taken for the execution of the method.  
 public long getMaxInvocationTime();  
 // MinInvocationTime: The minimum time taken for the execution of the method.  
 public long getMinInvocationTime();  
 // AverageInvocationTime: the averege execution time taken for the execution of the method.  
 public double getAverageInvocationTime();  
 // ExceptionCount: The number of times the method has thrown an Exception.  
 public long getExceptionCount();  
 // ExceptionMessage: The message of the last exception occurred.  
 public String getExeptionMessage();  
 public void setExceptionMessage(String errorMessage);
```

### MBean ツリーおよび操作の統計 {#mbean-tree-operation-statistics}

JMX コンソール (JConsole) を使用すると、OperationStatistic MBean の統計を使用できます。 これらの統計は MBean の属性で、次の階層ツリーの下で移動できます。

**MBean ツリー**

**アドビ ドメイン名：** アプリケーションサーバーに依存します。アプリケーションサーバーがドメインを定義していない場合、デフォルトは adobe.com です。

**ServiceType：** AdobeService は全サービスを表示するために使用される名前です。

**AdobeServiceName：**&#x200B;サービス名またはサービス ID。

**バージョン：**&#x200B;サービスのバージョン。

**運用の統計情報**

**呼び出し時間：**&#x200B;メソッドの実行にかかる時間。要求のシリアライズ、クライアントからサーバーへの転送、およびデシリアライズにかかる時間は含まれません。

**呼び出し数：**&#x200B;サービスを呼び出した回数。

**平均呼び出し時間：**&#x200B;サーバーを起動した後に実行したすべての呼び出しにかかる平均時間。

**最大呼び出し時間：**&#x200B;サーバーを起動した後に実行した呼び出しのうち、最も長い呼び出し時間。

**最小呼び出し時間：**&#x200B;サーバーを起動した後に実行した呼び出しのうち、最も短い呼び出し時間。

**例外数：**&#x200B;エラーが発生した呼び出しの数。

**例外メッセージ：**&#x200B;発生した最後の例外のエラーメッセージ。

**最終サンプリング日時：**&#x200B;最後の呼び出しの日付。

**時間単位：** デフォルトはミリ秒です。

JMX 監視を有効にするには、通常、アプリケーションサーバーにいくつかの設定が必要です。 詳しくは、アプリケーションサーバーのドキュメントを参照してください。

### オープン JMX アクセスの設定方法の例 {#examples-of-how-to-set-up-open-jmx-access}

**JBoss 4.0.3/4.2.0 - JVM スタートアップの設定**

JConsole から MBean を表示するには、JBoss アプリケーションサーバーの JVM 起動パラメーターを設定します。 JBoss が run.bat/sh ファイルから起動されていることを確認します。

1. InstallJBoss/bin にある run.bat ファイルを編集します。
1. JAVA_OPTS 行を検索し、次の行を追加します。

   ```as3
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 - JVM スタートアップの設定**

1. *の下にある startWebLogic.bat ファイルを編集します。 [WebLogic ホーム]*/user_projects/domains/domains_Live_Cycle/bin にAdobeします。
1. JAVA_OPTS 行を検索し、次の行を追加します。

   ```as3
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. WebLogic を再起動します。

>[!NOTE]
>
>WebLogic の場合は、リモートまたは IIOP を使用して MBean にアクセスできます。

**MBean へのリモートアクセス**

1. 新しい接続用に JConsole を起動し、リモートタブをクリックします。
1. ホスト名とポート（JVM の起動時に指定する番号 9088）を入力します。

**Websphere 6.1 - JVM スタートアップの設定**

1. Admin Console（アプリケーションサーバー/server1/プロセス定義/JVM）で、Generic JVM Argument のフィールドに次の行を追加します。

   ```as3
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.propertiesファイルに次の 3 行を追加するか、コメントを解除します ( または &lt;your websphere=&quot;&quot; jre=&quot;&quot;>/ lib/management/management.properties):

   ```as3
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect  
    com.sun.management.jmxremote.authenticate=false  
    com.sun.management.jmxremote.ssl=false
   ```

1. WebSphere を再起動します。
