---
title: ヘルスモニターのパフォーマンスに関する微調整
seo-title: Fine-tuning Health Monitor performance
description: ヘルスモニターのパフォーマンスを微調整する方法を説明します
seo-description: Learn how to fine-tune Health Monitor performance
uuid: 770b10cb-065f-41b5-9594-a291e4311151
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: b8f8bddc-0d38-4d5e-b33f-978f04bc16c6
exl-id: b2814b0d-e843-4aba-8c74-a3be0a96f726
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 18%

---

# ヘルスモニターのパフォーマンスに関する微調整{#fine-tuning-health-monitor-performance}

ヘルスモニターに設定されるシステム統計を収集すると、AEM forms 環境のパフォーマンスに多少の影響があります。 この影響は、アプリケーションサーバーで以下に示す Java オプションを設定することで制御できます。

<table> 
 <thead> 
  <tr> 
   <th><p>プロパティ</p></th> 
   <th><p>目的</p></th> 
   <th><p>デフォルト値</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>adobe.healthmonitor.enabled</p></td> 
   <td><p>ヘルスモニタースレッドのオン/オフを切り替える</p></td> 
   <td><p>true</p></td> 
  </tr> 
  <tr> 
   <td><p>adobe.cache.statistics-enabled</p></td> 
   <td><p>Gemfire キャッシュのオン/オフを切り替えます</p></td> 
   <td><p>true</p></td> 
  </tr> 
  <tr> 
   <td><p>adobe.healthmonitor.refresh-interval</p></td> 
   <td><p>ヘルスモニタースレッドが統計を収集するまでの間隔（ミリ秒）</p></td> 
   <td><p>10 分（600,000 ミリ秒）</p></td> 
  </tr> 
  <tr> 
   <td><p>adobe.cache.multicast-port</p></td> 
   <td><p>分散システムの他のメンバーとの通信に使用されるマルチキャストポート。 0 に設定した場合、メンバの検出と配布の両方に対してマルチキャストが無効になります。 </p><p>注意：異なる分散システム用に異なるマルチキャストアドレスとポートを選択します。 別のアドレスのみを使用しないでください。</p></td> 
   <td><p>デフォルト値はありません。有効な値の範囲は 0 ～ 65535です。</p></td> 
  </tr> 
  <tr> 
   <td><p>statistic-sample-rate</p></td> 
   <td><p>統計がサンプリングされる時間（ミリ秒）。 オペレーティングシステムの統計は、サンプルを取得した場合にのみ更新されます。</p></td> 
   <td><p>600000</p></td> 
  </tr> 
  <tr> 
   <td><p>adobe.workmanager.healthmonitor.enabled</p></td> 
   <td><p>このプロパティは、ジョブや作業項目の数など、Work Manager の統計情報の収集を有効または無効にします。</p></td> 
   <td><p>true</p></td> 
  </tr> 
 </tbody> 
</table>

## JBoss への Java オプションの追加 {#add-java-options-to-jboss}

1. JBoss アプリケーションサーバーを停止します。
1. *[appserver root]*/bin/run.bat（Windows）または run.sh（Linux または UNIX）をエディターで開き、必要に応じて Java オプションを追加します。
1. サーバーを再起動します。

## WebLogic への Java オプションの追加 {#add-java-options-to-weblogic}

1. 「 https:// 」と入力して WebLogic 管理コンソールを起動します。[ホスト名]:[ポート]/console （Web ブラウザーの URL 行）
1. WebLogic Server ドメイン用に作成したユーザー名とパスワードを入力し、「Log Under Change Center」で「Lock &amp; Edit」をクリックします。
1. 「Domain Structure」で、 Environment / Servers をクリックし、右側のウィンドウで、管理対象サーバー名をクリックします。
1. 次の画面で、「設定タブ」、「サーバー起動」タブをクリックします。
1. 「引数」ボックスで、現在の内容の末尾に必要な引数を追加します。 例えば、‑ `Dadobe.healthmonitor.enabled=false` を追加すると、ヘルスモニターが無効になります。
1. 「保存」をクリックし、「変更をアクティベート」をクリックします。
1. WebLogic 管理対象サーバーを再起動します。

## WebSphere への Java オプションの追加 {#add-java-options-to-websphere}

1. WebSphere Administrative Console のナビゲーションツリーで、使用するアプリケーションサーバーに対して次の操作を実行します。

   (WebSphere 6.x) Servers / Application servers をクリックします。

   (WebSphere 7.x) Servers / Server Types / WebSphere application servers をクリックします。

1. 右側のウィンドウで、サーバー名をクリックします。
1. 「Server Infrastructure」で、Java と forms のワークフロー/Process Definition をクリックします。
1. 「その他のプロパティ」で「Java 仮想マシン」をクリックします。
1. 「 Generic JVM arguments 」ボックスに、必要な引数を入力します。
1. 「 OK 」または「 Apply 」をクリックし、「 Save directly to master configuration 」をクリックします。
