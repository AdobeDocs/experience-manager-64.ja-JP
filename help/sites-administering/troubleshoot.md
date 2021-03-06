---
title: AEM のトラブルシューティング
seo-title: Troubleshooting AEM
description: AEM に関する問題のトラブルシューティングについて説明します。
seo-description: Learn about troubleshooting issues with AEM.
uuid: d68e9ead-8aa6-4108-9f1e-85d7cd7a370f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: 1bc19f9a-fa3f-43e3-813e-23ab0b708d43
exl-id: 34b509d5-4e80-4229-b155-40004856e87e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 84%

---

# AEM のトラブルシューティング{#troubleshooting-aem}

ここでは、AEM の使用時に発生する可能性のあるいくつかの問題を取り上げます。また、それらのトラブルシューティング方法に関する推奨事項についても説明します。

>[!NOTE]
>
>AEM のオーサリングの問題をトラブルシューティングする場合は、[オーサリング時の AEM のトラブルシューティング](/help/sites-authoring/troubleshooting.md)を参照してください。

>[!NOTE]
>
>問題が発生した場合は、そのインスタンス（リリースおよびサービスパック）の[既知の問題](/help/release-notes/known-issues.md)の一覧を確認すると役に立ちます。

## 管理者が実行するトラブルシューティングのシナリオ {#troubleshooting-scenarios-for-administrators}

次の表は、管理者がトラブルシューティングをおこなう必要のある問題の概要を示しています。

<table> 
 <tbody> 
  <tr> 
   <td><strong>役割</strong></td> 
   <td><strong>問題 </strong></td> 
  </tr> 
  <tr> 
   <td>システム管理者</td> 
   <td><p>Quickstart jar をダブルクリックしても何も起きないか、jar ファイルが別のプログラム（アーカイブマネージャーなど）で開かれる</p> </td> 
  </tr> 
  <tr> 
   <td><p>システム管理者</p> </td> 
   <td><p>CRX で動作しているアプリケーションでメモリ不足のエラーが発生する</p> </td> 
  </tr> 
  <tr> 
   <td><p>システム管理者</p> </td> 
   <td><p>AEM CM Quickstart をダブルクリックした後に、ブラウザーで AEM ようこそ画面が表示されない</p> </td> 
  </tr> 
  <tr> 
   <td><p>システム管理者</p> <p>admin ユーザー</p> </td> 
   <td><p>スレッドダンプの作成</p> </td> 
  </tr> 
  <tr> 
   <td><p>システム管理者</p> <p>admin ユーザー</p> </td> 
   <td><p>閉じられていない JCR セッションの確認</p> </td> 
  </tr> 
 </tbody> 
</table>

## インストールの問題 {#installation-issues}

以下のトラブルシューティングのシナリオについては、[一般的なインストールの問題](/help/sites-deploying/troubleshooting.md#common-installation-issues)を参照してください。

* Quickstart jar をダブルクリックしても何も起きないか、JAR ファイルが別のプログラム（アーカイブマネージャーなど）で開かれる。
* CRX で動作しているアプリケーションでメモリ不足のエラーが発生する。
* AEM Quickstart をダブルクリックした後に、ブラウザーで AEM ようこそ画面が表示されない。

## トラブルシューティング分析の方法 {#methods-for-troubleshooting-analysis}

### スレッドダンプの作成 {#making-a-thread-dump}

スレッドダンプは、現在アクティブなすべての Java スレッドのリストです。AEM が適切に応答しない場合は、デッドロックまたはその他の問題をスレッドダンプで特定できます。

### Sling Thread Dumper の使用 {#using-sling-thread-dumper}

1. を開きます。 **AEM Web コンソール**;例： `http://localhost:4502/system/console/`.

1. を選択します。 **スレッド** under **ステータス** タブをクリックします。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### jstack の使用（コマンドライン） {#using-jstack-command-line}

1. AEM Java インスタンスの PID（プロセス ID）を確認します。

   例えば、 `ps -ef` または `jps`.

1. 実行:

   `jstack <pid>`

1. スレッドダンプが表示されます。

>[!NOTE]
>
>スレッドダンプをログファイルに追加するには、 `>>` 出力リダイレクト：
>
>`jstack <pid> >> /path/to/logfile.log`

詳しくは、[JVM からのスレッドダンプの取得方法](https://helpx.adobe.com/cq/kb/TakeThreadDump.html)を参照してください。

### 閉じられていない JCR セッションの確認 {#checking-for-unclosed-jcr-sessions}

AEM WCM 用の機能を開発する場合は、JCR セッションが開かれる可能性があります（データベース接続を開く処理に相当します）。開かれたセッションが閉じられないと、システムで以下の症状が発生する可能性があります。

* システムの速度が低下する。
* CacheManager の多くを確認できます。resize ログファイル内のすべてのエントリ；次の数値 (size=&lt;x>) はキャッシュの数を示し、各セッションは複数のキャッシュを開きます。
* システムのメモリが不足することがある（重大度に応じて数時間後、数日後、数週間後に発生）。

閉じられていないセッションを分析して、セッションを閉じていないコードを特定するには、ナレッジベースの記事[閉じられていないセッションの分析](https://helpx.adobe.com/crx/kb/AnalyzeUnclosedSessions.html)を参照してください。

### Adobe Experience Manager Web コンソールの使用 {#using-the-adobe-experience-manager-web-console}

発生する可能性のある問題の初期の兆候を OSGi バンドルのステータスで確認することもできます。

1. を開きます。 **AEM Web コンソール**;例： `http://localhost:4502/system/console/`.

1. 選択 **バンドル** under **OSGI** タブをクリックします。

1. 次の項目を確認します。

   * バンドルのステータス。「Inactive」または「Unsatisfied」と表示されているバンドルがある場合は、そのバンドルを停止してから再起動してください。問題が解決しない場合は、他の方法を使用した詳細な調査が必要になる可能性があります。
   * いずれかのバンドルで依存関係が失われていないかどうか。個々のバンドル名（リンク）をクリックすると、詳細を確認できます（問題が発生していない場合の例を次に示します）。

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
