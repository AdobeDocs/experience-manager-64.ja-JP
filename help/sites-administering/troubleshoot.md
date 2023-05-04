---
title: AEM のトラブルシューティング
seo-title: Troubleshooting AEM
description: AEMの問題のトラブルシューティングについて説明します。
seo-description: Learn about troubleshooting issues with AEM.
uuid: d68e9ead-8aa6-4108-9f1e-85d7cd7a370f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: 1bc19f9a-fa3f-43e3-813e-23ab0b708d43
exl-id: 34b509d5-4e80-4229-b155-40004856e87e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 31%

---

# AEM のトラブルシューティング{#troubleshooting-aem}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

次の節では、AEMの使用時に発生する可能性のあるいくつかの問題と、そのトラブルシューティング方法に関する推奨事項について説明します。

>[!NOTE]
>
>AEMでオーサリングの問題をトラブルシューティングする場合は、 [作成者向けのトラブルシューティング。](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>問題が発生した場合は、リストを確認することも重要です [既知の問題](/help/release-notes/known-issues.md) インスタンス（リリースおよびサービスパック）の

## 管理者向けのトラブルシューティングシナリオ {#troubleshooting-scenarios-for-administrators}

管理者がトラブルシューティングに必要とする可能性のある問題の概要を次の表に示します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>役割</strong></td> 
   <td><strong>問題 </strong></td> 
  </tr> 
  <tr> 
   <td>システム管理者</td> 
   <td><p>クイックスタート JAR をダブルクリックしても何の影響もなく、jar ファイルを別のプログラム（アーカイブマネージャーなど）で開く</p> </td> 
  </tr> 
  <tr> 
   <td><p>システム管理者</p> </td> 
   <td><p>CRX で実行中のアプリケーションでメモリ不足エラーが発生する</p> </td> 
  </tr> 
  <tr> 
   <td><p>システム管理者</p> </td> 
   <td><p>AEM CM Quickstart をダブルクリックした後、ブラウザーにAEMのようこそ画面が表示されない</p> </td> 
  </tr> 
  <tr> 
   <td><p>システム管理者</p> <p>管理者ユーザー</p> </td> 
   <td><p>スレッドダンプの作成</p> </td> 
  </tr> 
  <tr> 
   <td><p>システム管理者</p> <p>管理者ユーザー</p> </td> 
   <td><p>閉じられていない JCR セッションの確認</p> </td> 
  </tr> 
 </tbody> 
</table>

## インストールの問題 {#installation-issues}

詳しくは、 [一般的なインストールの問題](/help/sites-deploying/troubleshooting.md#common-installation-issues) 次のトラブルシューティングシナリオについては、を参照してください。

* クイックスタート JAR をダブルクリックしても効果がないか、別のプログラム（アーカイブマネージャーなど）が含まれた JAR ファイル。
* CRX で実行中のアプリケーションはメモリ不足エラーをスローします。
* AEM Quickstart をダブルクリックした後、ブラウザーにAEMのようこそ画面が表示されない。

## 分析のトラブルシューティング方法 {#methods-for-troubleshooting-analysis}

### スレッドダンプの作成 {#making-a-thread-dump}

スレッドダンプは、現在アクティブなすべての Java スレッドのリストです。 AEMが正しく応答しない場合、スレッドダンプは、デッドロックやその他の問題を識別するのに役立ちます。

### Sling Thread Dumper の使用 {#using-sling-thread-dumper}

1. **AEM web コンソール**&#x200B;を開きます（例：`http://localhost:4502/system/console/`）。

1. **ステータス**&#x200B;タブの下の&#x200B;**スレッド**&#x200B;を選択します。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### jstack の使用（コマンドライン） {#using-jstack-command-line}

1. AEM Java インスタンスの PID（プロセス ID）を確認します。

   例えば、`ps -ef` や `jps` を使用できます。

1. 実行:

   `jstack <pid>`

1. スレッドダンプが表示されます。

>[!NOTE]
>
>`>>` 出力リダイレクトを使用すると、ログファイルにスレッドダンプを追加できます。
>
>`jstack <pid> >> /path/to/logfile.log`

詳しくは、[JVM からのスレッドダンプの取得方法](https://helpx.adobe.com/cq/kb/TakeThreadDump.html)を参照してください。

### 閉じられていない JCR セッションの確認 {#checking-for-unclosed-jcr-sessions}

AEM WCM 用の機能が開発されている場合、JCR セッションを開くことができます（データベース接続を開く場合と同等）。 開いたセッションが閉じられない場合は、システムに次の現象が発生する可能性があります。

* システムの速度が低下します。
* 多数の CacheManager を確認できます（ログファイル内の resizeAll エントリ）。次の数値（size=&lt;x>）はキャッシュ数を示しており、各セッションが複数のキャッシュを開きます。
* システムのメモリが不足することがある（重大度に応じて数時間後、数日後、数週間後に発生）。

閉じられていないセッションを分析し、セッションを閉じていないコードを調べるには、ナレッジベースの記事を参照してください [閉じられていないセッションの分析](https://helpx.adobe.com/jp/crx/kb/AnalyzeUnclosedSessions.html).

### Adobe Experience Manager Web コンソールの使用 {#using-the-adobe-experience-manager-web-console}

OSGi バンドルのステータスによって、考えられる問題が早期に示される場合もあります。

1. **AEM web コンソール**&#x200B;を開きます（例：`http://localhost:4502/system/console/`）。

1. **OSGI** タブの下の&#x200B;**バンドル**&#x200B;を選択します。

1. チェック項目:

   * バンドルのステータス。 Inactive または Unsatisfied の場合は、バンドルを停止して再起動してみます。 問題が解決しない場合は、他の方法を使用してさらに調査する必要がある場合があります。
   * いずれかのバンドルに依存関係がないかどうか。 このような詳細は、個々のバンドル名（リンク）をクリックすると確認できます（次の例では問題はありません）。

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
