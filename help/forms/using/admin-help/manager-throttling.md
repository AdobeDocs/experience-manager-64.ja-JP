---
title: ワークマネージャーとスロットリング
seo-title: Work Manager and throttling
description: このドキュメントでは、ワークマネージャーの背景情報と、ワークマネージャーのスロットルオプションを設定する手順を説明します。
seo-description: This document provides background information on Work Manager, and provides instructions on configuring Work Manager throttling options.
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
exl-id: 759cff3e-960a-4c38-a731-9fff21e739cf
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 13%

---

# ワークマネージャーとスロットリング{#work-manager-and-throttling}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM forms（および以前のバージョン）では、JMS キューを使用して非同期的に操作を実行していました。 AEM forms では、JMS キューが Work Manager に置き換えられました。 このドキュメントでは、ワークマネージャーの背景情報と、ワークマネージャーのスロットルオプションを設定する手順を説明します。

## 長期間有効な（非同期）操作について {#about-long-lived-asynchronous-operations}

AEM forms では、サービスによって実行される操作は、短時間のみ有効（同期）と長時間有効（非同期）のどちらかになります。 短時間のみ有効な操作は、呼び出された同じスレッドで同期して完了します。 これらの操作は、応答を待ってから続行します。

長期間有効な操作は、複数の自動タスクと人的タスクを統合する大規模なソリューションの一部として、顧客がローン申し込みフォームを完成させ、送信する必要がある場合など、システムにまたがる場合や、組織を超える場合もあります。 このような操作は、応答を待つ間も続行する必要があります。 長期間有効な操作は、基になる作業を非同期的に実行し、完了を待つ間、他の方法でリソースをエンゲージすることを許可します。 短時間のみ有効な操作とは異なり、Work Manager では、呼び出し後に長期間有効な操作が完了したとは考慮されません。 同じサービス上で別の操作を要求するシステムや、フォームを送信するユーザーなどの外部トリガーが、操作の完了時に発生する必要があります。

## ワークマネージャーについて {#about-work-manager}

AEM forms（および以前のバージョン）では、JMS キューを使用して非同期的に操作を実行していました。 AEM forms では、Work Manager を使用して、管理されたスレッドを介して非同期操作をスケジュールおよび実行します。

非同期操作は次の方法で処理されます。

1. ワークマネージャーは、実行する作業項目を受け取ります。
1. ワークマネージャは、作業項目をデータベーステーブルに格納し、作業項目に一意の識別子を割り当てます。 データベースレコードには、作業項目の実行に必要なすべての情報が含まれています。
1. Work Manager スレッドは、スレッドが空きになったときに作業項目を取り込みます。 作業項目をプルする前に、スレッドは、必要なサービスが開始されているか、次の作業項目をプルするのに十分なヒープサイズがあるか、作業項目を処理するのに十分な CPU サイクルがあるかを確認できます。 また、ワークマネージャーは、実行をスケジュールする際に、作業項目の属性（優先度など）を評価します。

AEM forms 管理者は、ヘルスモニターを使用して、キュー内の作業項目の数やステータスなど、Work Manager の統計を確認できます。 ヘルスモニターを使用して、作業項目を一時停止、再開、再試行、または削除することもできます。 ( [ワークマネージャーに関連する統計を表示](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## ワークマネージャーのスロットルオプションの設定 {#configuring-work-manager-throttling-options}

ワークマネージャーのスロットルを設定して、使用可能なメモリリソースが十分にある場合にのみ作業項目がスケジュールされるようにすることができます。 スロットルは、アプリケーションサーバーで次の JVM オプションを設定することで設定します。

<table> 
 <thead> 
  <tr> 
   <th><p>プロパティ</p></th> 
   <th><p>説明</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><code> adobe.work-manager.queue-refill-interval</code></td> 
   <td><p>ワークマネージャがキュー内の新しい項目を確認する際に使用する時間間隔をミリ秒単位で指定します。</p><p>このオプションの値は整数です。 デフォルト値は <code>1000</code> ミリ秒（1 秒）です。 </p><p>非同期呼び出しの量が少ない場合は、この値を増やすことができます。 例えば、2000 ～ 5000（2 ～ 5 秒）の間に増やすことができます。 </p><p>非同期呼び出しの量が多い場合は、デフォルト値で十分ですが、必要に応じて低い値を使用できます。 この値を大きく減らすと（例えば、50 を下回ると 1 秒に 20 回のポーリング頻度が発生します）、システムのオーバーヘッドが大幅に増加します。</p></td> 
  </tr> 
  <tr> 
   <td><code> adobe.workmanager.debug-mode-enabled</code></td> 
   <td><p>このオプションを <code>true</code> に設定するとデバッグモードが有効になり、false を設定すると無効になります。 </p><p>デバッグモードでは、ワークマネージャーのポリシー違反およびワークマネージャーの一時停止/再開アクションに関するメッセージがログに記録されます。 このオプションは、トラブルシューティングの場合にのみ true に設定します。</p></td> 
  </tr> 
  <tr> 
   <td><code> adobe.workmanager.memory-control.enabled</code></td> 
   <td><p>このオプションを <code>true</code> に設定すると、後述するメモリ制御設定に基づいてスロットリングが有効になります。<code>false</code> に設定するとスロットリングが無効になります。</p></td> 
  </tr> 
  <tr> 
   <td><code> adobe.workmanager.memory-control.high-limit</code></td> 
   <td><p>ワークマネージャーが受信ジョブをスロットリング処理する前に、使用状態にすることができるメモリの最大比率を指定します。</p><p>このオプションのデフォルト値は <code>95</code> です。この値はほとんどのシステムで適切です。 システムを最大容量までプッシュする必要がある場合にのみ増やします。 ただし、この値を増やすと、メモリ不足の問題のリスクも高くなります。</p><p>クラスター環境でAEM forms を実行している場合は、クラスターのノードごとにメモリ制御の制限設定を異なる設定にする必要が生じる場合があります。 例えば、インタラクティブな作業用にロードバランサーでプログラムされたノード A と B に低い上限を設定できます。 また、ロードバランサーでは使用せず、非同期作業用に予約されたノード C と D に高い上限を設定することもできます。</p></td> 
  </tr> 
  <tr> 
   <td><code> adobe.workmanager.memory-control.low-limit</code></td> 
   <td><p>ワークマネージャが受信ジョブのスロットリングを停止する前に、使用可能なメモリの最大割合を指定します。</p><p>このオプションのデフォルト値は <code>20</code> です。この値はほとんどのシステムで適切です。</p></td> 
  </tr> 
  <tr> 
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td> 
   <td><p>ワークマネージャーの最大バッチサイズを指定します。 デフォルトのバッチサイズは 10 です。</p><p>タスクが完了した後でもワークマネージャーのプロセスのステータスが更新されない場合は、バッチサイズを 1 に設定します。</p></td> 
  </tr> 
 </tbody> 
</table>

**JBoss への Java オプションの追加**

1. JBoss アプリケーションサーバーを停止します。
1. *[[appserver root]]*/bin/run.bat（Windows）または run.sh（Linux または UNIX）をエディターで開き、`-Dproperty=value`の形式で必要に応じて Java オプションを追加します。
1. サーバーを再起動します。

**WebLogic への Java オプションの追加**

1. 次のように入力して、WebLogic 管理コンソールを起動します。 `https://`*[ホスト名&#x200B;]*`:`*[ポート]* `/console` （Web ブラウザー）を使用して、
1. WebLogic Server ドメイン用に作成したユーザー名とパスワードを入力し、「Log Under Change Center」で「Lock &amp; Edit」をクリックします。
1. 「Domain Structure」で、 Environment / Servers をクリックし、右側のウィンドウで、管理対象サーバー名をクリックします。
1. 次の画面で、「設定タブ」、「サーバー起動」タブをクリックします。
1. 「引数」ボックスで、現在の内容の末尾に必要な引数を追加します。 例えば、ヘルスモニターを無効にするには、次を追加します。

   `-Dadobe.healthmonitor.enabled=false`はヘルスモニターを無効にします。

1. 「保存」をクリックし、「変更をアクティベート」をクリックします。
1. WebLogic 管理対象サーバーを再起動します。

**WebSphere への Java オプションの追加**

1. WebSphere Administrative Console のナビゲーションツリーで、 Servers / Server Types / WebSphere application servers をクリックします。
1. 右側のウィンドウで、サーバー名をクリックします。
1. 「Server Infrastructure」で、Java と forms のワークフロー/Process Definition をクリックします。
1. 「その他のプロパティ」で「Java 仮想マシン」をクリックします。
1. 「 Generic JVM arguments 」ボックスに、必要な引数を入力します。
1. 「 OK 」または「 Apply 」をクリックし、「 Save directly to master configuration 」をクリックします。
