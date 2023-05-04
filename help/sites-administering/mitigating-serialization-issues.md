---
title: AEM でのシリアル化の問題の軽減
seo-title: Mitigating serialization issues in AEM
description: AEMでのシリアル化の問題を軽減する方法について説明します。
seo-description: Learn how to mitigate serialization issues in AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
exl-id: 779e1e4c-9a6e-4446-9c12-5b2499afbf6a
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 46%

---

# AEM でのシリアル化の問題の軽減{#mitigating-serialization-issues-in-aem}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

アドビの AEM チームは、オープンソースプロジェクト [NotSoSerial](https://github.com/kantega/notsoserial) と緊密に連携して **CVE-2015-7501** に記載されている脆弱性の軽減に努めています。NotSoSerial は [Apache 2 ライセンス](https://www.apache.org/licenses/LICENSE-2.0)でライセンスが付与され、[BSD に似た独自のライセンス](https://asm.ow2.org/license.html)でライセンスが付与される ASM コードが含まれます。

このパッケージに含まれるエージェント JAR は、アドビが変更を加えて配布する NotSoSerial です。

NotSoSerial は Java レベルの問題を解決する Java レベルのソリューションであり、AEM に固有のものではありません。これはオブジェクトのシリアル化を解除するときに、プリフライトのチェックを追加します。このチェックを実行すると、ファイアウォールスタイルの許可リストやブロックリストに対してクラス名がテストされます。 デフォルトブロックリストのクラス数は限られているので、システムやコードに影響を与える可能性は低くなります。

デフォルトでは、エージェントは、現在の既知の脆弱なクラスに対してブロックリストチェックを実行します。 このブロックリストは、このタイプの脆弱性を使用する現在の弱点のリストからユーザーを保護することを目的としています。

ブロックリストと許可リストは、 [エージェントの設定](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) 」の節を参照してください。

このエージェントは、最新の既知の脆弱なクラスを軽減するためのものです。 プロジェクトで信頼できないデータの逆シリアル化が行われている場合でも、サービス拒否攻撃、メモリ不足攻撃、未知の逆シリアル化攻撃に対する脆弱性が生じる可能性があります。

アドビは Java 6、7 および 8 を正式にサポートしていますが、NotSoSerial は Java 5 もサポートしています。

## エージェントのインストール {#installing-the-agent}

>[!NOTE]
>
>以前に AEM 6.1 向けのシリアル化のホットフィックスをインストールした場合は、Java を実行する行からエージェントの開始コマンドを削除してください。

1. **com.adobe.cq.cq-serialization-tester** バンドルをインストールします。

1. Web コンソール（`https://server:port/system/console/bundles`）にアクセスします。
1. シリアル化バンドルを探し、起動します。 これは NotSoSerial エージェントを動的に自動読み込みする必要があります。

## アプリケーションサーバーへのエージェントのインストール {#installing-the-agent-on-application-servers}

NotSoSerial エージェントは、アプリケーションサーバー用のAEMの標準配布には含まれていません。 ただし、AEM jar 配布から抽出して、アプリケーションサーバーの設定で使用することができます。

1. まず、AEM quickstart ファイルをダウンロードして抽出します。

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. AEM クイックスタートを展開した場所に移動し、`crx-quickstart/opt/notsoserial/` フォルダーを AEM アプリケーションサーバーのインストールの `crx-quickstart` フォルダーにコピーします。

1. `/opt` の所有者を、サーバーを実行しているユーザーに変更します。

   ```shell
   chown -R opt <user running the server>
   ```

1. この記事の後の節で示すように、エージェントが正しくアクティブ化されていることを設定および確認します。

## エージェントの設定 {#configuring-the-agent}

デフォルトの設定は、ほとんどのインストールで十分です。 これには、リモート実行の既知の脆弱性があるクラスのブロックリストや、信頼できるデータのシリアル化解除が比較的安全なパッケージの許可リストが含まれます。

ファイアウォールの設定は動的であり、次の手順でいつでも変更できます。

1. Web コンソール（`https://server:port/system/console/configMgr`）にアクセスします。
1. 検索とクリック **デシリアライゼーションファイアウォールの構成。**

   >[!NOTE]
   >
   >また、次の URL にアクセスして、設定ページに直接アクセスすることもできます。
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


この設定には、許可リスト、ブロックリスト、シリアル化解除ログが含まれています。

**リストへの登録を許可**

許可リストセクションでは、シリアル化解除を許可するクラスまたはパッケージのプレフィックスがこれらに該当します。 独自のクラスを逆シリアル化する場合は、クラスまたはパッケージをこの許可リストに追加する必要があることに注意する必要があります。

**ブロックリスト**

ブロックリストセクションには、シリアル化解除が許可されないクラスが表示されます。これらのクラスの初期セットは、リモート実行の攻撃に脆弱であると見なされるクラスに限定されています。ブロックリストは、許可リストに登録されているエントリの前に適用されます。

**Diagnostinc Logging**

 診断ログのセクションでは、シリアル化解除の実行中にログに記録される内容を、複数のオプションから選択できます。これらは最初の使用時にログに記録され、後続の使用では記録されません。

デフォルトの **class-name-only** は、シリアル化が解除されるクラスを示します。

**full-stack** オプションを選択すると、最初にシリアル化の解除が試行されたときの Java スタックがログに記録され、シリアル化の解除が実行されている場所を示します。これは、自身の環境からシリアル化が解除されたクラスを探して削除するときに便利です。

## エージェントのアクティベーションの確認 {#verifying-the-agent-s-activation}

シリアル化解除エージェントの設定は、次の URL を参照して確認できます。

* `https://server:port/system/console/healthcheck?tags=deserialization`

URL にアクセスすると、エージェントに関連するヘルスチェックのリストが表示されます。 エージェントが正しくアクティブ化されているかどうかは、ヘルスチェックが合格していることを確認することで確認できます。 障害が発生した場合は、エージェントを手動で読み込む必要がある場合があります。

エージェントに関する問題のトラブルシューティングの詳細については、 [動的エージェントの読み込みでのエラーの処理](#handling-errors-with-dynamic-agent-loading) 下

>[!NOTE]
>
>`org.apache.commons.collections.functors` を許可リストに追加すると、ヘルスチェックは必ず失敗します。

## 動的エージェントの読み込みでのエラーの処理 {#handling-errors-with-dynamic-agent-loading}

ログにエラーが表示された場合、または検証手順でエージェントの読み込み中に問題が検出された場合は、エージェントを手動で読み込む必要が生じる場合があります。 また、JDK(Java Development Toolkit) の代わりに JRE(Java Runtime Environment) を使用している場合は、動的読み込み用のツールを使用できないので、この方法を使用することをお勧めします。

エージェントを手動で読み込むには、以下の手順に従います。

1. 次のオプションを追加して、CQ jar の JVM 起動パラメーターを変更します。

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >エージェントがフォークされた JVM で有効にならないので、これには —nofork CQ/AEMオプションと適切な JVM メモリ設定も使用する必要があります。

   >[!NOTE]
   >
   >Adobe 配布版の NotSoSerial エージェント JAR は、AEM インストールの `crx-quickstart/opt/notsoserial/` フォルダーにあります。

1. JVM を停止して再開します。

1. 上記の手順に従って、エージェントのアクティベーションを再度確認します。 [エージェントのアクティベーションの確認](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## その他の注意点 {#other-considerations}

IBM JVM 上で実行している場合は、[こちら](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html)の Java Attach API のサポートに関するドキュメントを参照してください。
