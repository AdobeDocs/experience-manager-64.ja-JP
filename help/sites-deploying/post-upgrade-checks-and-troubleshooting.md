---
title: アップグレード後のチェックおよびトラブルシューティング
seo-title: Post Upgrade Checks and Troubleshooting
description: アップグレード後に発生する可能性のある問題のトラブルシューティング方法を説明します。
seo-description: Learn how to troubleshoot issues that might appear after an upgrade.
uuid: 3f83e8fc-1c45-4ef0-b8da-d29ff483d3d5
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: bc8c9aa2-f669-41f3-a526-6146ff5cf0cd
feature: Upgrading
exl-id: edd6e933-59ed-4d7e-8934-7e2ec485cfb9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1907'
ht-degree: 24%

---

# アップグレード後のチェックおよびトラブルシューティング{#post-upgrade-checks-and-troubleshooting}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## アップグレード後のチェック {#post-upgrade-checks}

次の [インプレースアップグレード](/help/sites-deploying/in-place-upgrade.md) 次のアクティビティを実行して、アップグレードを完了する必要があります。 6.4 jar でAEMが起動され、アップグレードされたコードベースがデプロイされていると想定されます。

* [ログでアップグレードの成功を確認](#verify-logs-for-upgrade-success)

* [OSGi バンドルの確認](#verify-osgi-bundles)

* [Oak バージョンの確認](#verify-oak-version)

* [PreUpgradeBackup フォルダーの検査](#inspect-preupgradebackup-folder)

* [ページの初期検証](#initial-validation-of-pages)
* [AEM サービスパックの適用](#apply-aem-service-packs)

* [AEM 機能の移行](#migrate-aem-features)

* [スケジュールされたメンテナンス設定の確認](#verify-scheduled-maintenance-configurations)

* [レプリケーションエージェントの有効化](#enable-replication-agents)

* [スケジュール済みカスタムジョブの有効化](#enable-custom-scheduled-jobs)

* [テスト計画の実行](#execute-test-plan)

### ログのアップグレード成功の確認 {#verify-logs-for-upgrade-success}

**upgrade.log**

以前は、インスタンスのアップグレード後の状態を調べるには、様々なログファイル、リポジトリの一部、Launchpad を慎重に検査する必要がありました。 アップグレード後のレポートを生成すると、アップグレードの不良を検出してから運用を開始するのに役立ちます。

この機能の主な目的は、アップグレードの成功を検証するために必要な、複数のエンドポイントをまたいで、手動での解釈や複雑な解析ロジックの必要性を減らすことです。 このソリューションは、更新の成功または特定された失敗に対応する外部自動化システムに対して、あいまいでない情報を提供することを目的としています。

具体的には、次のことが確実におこなわれます。

* アップグレードフレームワークで検出されたアップグレードエラーは、単一のアップグレードレポートに一元化できます。
* アップグレードレポートには、手動での必要な介入に関する指標が含まれています。

これに対応するために、`upgrade.log` ファイルにログを生成する方法が変更されました。

アップグレード中にエラーが発生しなかったことを示すサンプルレポートを次に示します。

![1487887443006](assets/1487887443006.png)

アップグレードプロセスでインストールされなかったバンドルを示すサンプルレポートを次に示します。

![1487887532730](assets/1487887532730.png)

**error.log**

ターゲットバージョン jar を使用したAEMの起動時および起動後は、error.log を慎重に確認する必要があります。 警告やエラーは確認する必要があります。 一般に、ログの先頭で問題を探すのが最適です。 ログの後半で発生するエラーは、実際には、ファイル内の早い段階で呼び出される根本原因の副作用である可能性があります。 エラーと警告が繰り返し発生した場合は、以下を参照してください。 [アップグレードに伴う問題の分析](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md#analyzing-issues-with-upgrade).

### OSGi バンドルの確認 {#verify-osgi-bundles}

OSGi コンソール `/system/console/bundles` に移動し、開始されていないバンドルがあるかどうかを確認します。いずれかのバンドルがインストール済み状態の場合は、`error.log` を調べて根本的な問題を特定します。

### Oak バージョンの確認 {#verify-oak-version}

アップグレード後に、Oak のバージョンがに更新されていることを確認する必要があります。 **1.8.2**. Oak バージョンを確認するには、OSGi コンソールに移動し、Oak バンドル（Oak Core、Oak Commons、Oak Segment Tar）に関連付けられたバージョンを調べます。

### PreUpgradeBackup フォルダーの検査 {#inspect-preupgradebackup-folder}

アップグレード中、AEM はカスタマイズのバックアップを作成して、`/var/upgrade/PreUpgradeBackup/<time-stamp-of-upgrade>` の下に格納することを試みます。このフォルダーを CRXDE Lite で表示するには、[CRXDE Lite を一時的に有効にする](/help/sites-administering/enabling-crxde-lite.md)ことが必要となります。

タイムスタンプがあるフォルダーには、`mergeStatus` という名前のプロパティがあり、`COMPLETED` という値である必要があります。この **処理する** フォルダーは空で、 **上書き** ノードは、アップグレード中に上書きされたノードを示します。 の下のコンテンツ **残り物** ノードは、アップグレード中に安全に結合できなかったコンテンツを示します。 実装が子ノードのいずれかに依存する場合（アップグレードされたコードパッケージにまだインストールされていない場合）は、手動で結合する必要があります。

ステージング環境または実稼動環境では、この演習の後のCRXDE Liteを無効にします。

### ページの初期検証 {#initial-validation-of-pages}

AEMの複数のページに対して初期検証を実行します。 オーサー環境をアップグレードする場合は、開始ページとようこそページ（`/aem/start.html`、`/libs/cq/core/content/welcome.html`）を開きます。オーサー環境とパブリッシュ環境の両方で、アプリケーションページをいくつか開き、正しくレンダリングされるかどうかスモークテストをおこないます。問題が発生した場合は、`error.log` を調べてトラブルシューティングをおこないます。

### AEM サービスパックの適用 {#apply-aem-service-packs}

関連するAEM 6.4 Service Pack がリリースされている場合は、適用します。

### AEM機能の移行 {#migrate-aem-features}

AEMの一部の機能では、アップグレード後に追加の手順が必要になります。 これらの機能の完全なリストと、AEM 6.4 で移行する手順については、 [コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md) ページ。

### スケジュールされたメンテナンス設定の確認 {#verify-scheduled-maintenance-configurations}

#### データストアのガベージコレクションを有効にする {#enable-data-store-garbage-collection}

ファイルデータストアを使用する場合は、データストアのガベージコレクションタスクが有効になっていて、週別メンテナンスリストに追加されていることを確認します。 説明は [こちら](/help/sites-administering/data-store-garbage-collection.md) を参照してください。

>[!NOTE]
>
>S3 のカスタムデータストアのインストールや、共有データストアを使用する場合は、この操作はお勧めしません。

#### オンラインでのリビジョンクリーンアップの有効化 {#enable-online-revision-cleanup}

MongoMK または新しい TarMK セグメント形式を使用する場合は、リビジョンのクリーンアップタスクが有効になっていて、日別メンテナンスリストに追加されていることを確認してください。 説明 [ここ](/help/sites-deploying/revision-cleanup.md).

### テスト計画の実行 {#execute-test-plan}

定義済みのに対して詳細なテスト計画を実行します [コードのアップグレードとカスタマイズ](/help/sites-deploying/upgrading-code-and-customizations.md) の下に **テスト手順** 」セクションに入力します。

### レプリケーションエージェントの有効化 {#enable-replication-agents}

パブリッシュ環境が完全にアップグレードおよび検証されたら、オーサー環境でレプリケーションエージェントを有効にします。 エージェントが各パブリッシュインスタンスに接続できることを確認します。 詳しくは、 [アップグレード手順](/help/sites-deploying/upgrade-procedure.md) イベントの順序の詳細を参照してください。

### スケジュール済みカスタムジョブの有効化 {#enable-custom-scheduled-jobs}

この時点で、コードベースの一部としてスケジュール済みのジョブを有効にすることができます。

## アップグレードの問題の分析 {#analyzing-issues-with-upgrade}

この節では、AEM 6.4 へのアップグレード手順で発生する可能性のある問題のシナリオをいくつか説明します。

これらのシナリオは、アップグレードに関連する問題の根本原因を追跡するのに役立ち、プロジェクト固有または製品固有の問題を特定するのに役立ちます。

### アップグレード後のDynamic Media Cloud Configuration の再作成 {#dynamic-media-cloud-configuration}

以前のバージョンからAEM 6.4 にアップグレードした後、以前の設定からDynamic Mediaクラウド設定にAEM 6.4 TouchUI からアクセスできなくなる場合があります。 この問題を解決するには、CRXDE Liteを使用して以前の設定を削除し、新しいDynamic Mediaクラウド設定を作成します。 関連トピック [AEM 6.4 でのDynamic Mediaリポジトリの再構築](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-4.md).

### リポジトリの移行に失敗  {#repository-migration-failing-}

CRX2 から Oak へのデータ移行は、CQ 5.4 ベースのソースインスタンスから開始されるすべてのシナリオで実現可能です。`repository.xml` の準備を含むこのドキュメントのアップグレード手順に正確に従っていること、JAAS 経由でカスタム認証を起動していないこと、および移行を始める前にインスタンスに不整合がないかをチェックしていることを確認してください。

それでも移行が失敗する場合は、`upgrade.log` を調査して根本原因を解明することができます。未知の問題の場合は、カスタマーサポートに報告してください。

### アップグレードが実行されませんでした {#the-upgrade-did-not-run}

準備手順を開始する前に、必ず **ソース** まず、java -jar aem-quickstart.jar コマンドを使用して実行します。 これは、quickstart.properties ファイルが正しく生成されるようにするために必要です。 見つからない場合、アップグレードは機能しません。 あるいは、ソースインスタンスのインストールフォルダーの `crx-quickstart/conf` の下を探して、このファイルが存在するかどうかを確認します。さらに、AEMを起動してアップグレードを開始する際には、java -jar aem-quickstart.jar コマンドを使用して実行する必要があります。 起動スクリプトから起動しても、アップグレードモードでAEMが起動しません。

### パッケージとバンドルの更新に失敗  {#packages-and-bundles-fail-to-update-}

アップグレード中にパッケージをインストールできなかった場合、パッケージに含まれるバンドルも更新されません。 このカテゴリの問題は、通常、データストアの設定ミスが原因で発生します。 また、 **エラー** および **警告** error.log 内のメッセージ。 ほとんどの場合、デフォルトのログインが機能しない可能性があるので、CRXDE を直接使用して、設定の問題を調べ、見つけることができます。

### 一部のAEMバンドルがアクティブ状態に切り替わらない {#some-aem-bundles-are-not-switching-to-the-active-state}

バンドルが起動しない場合は、未満の依存関係を確認する必要があります。

この問題が発生したが、失敗したパッケージのインストールに基づいている場合、バンドルがアップグレードされず、新しいバージョンに対して互換性がないと見なされます。 この問題のトラブルシューティング方法について詳しくは、 **パッケージとバンドルの更新に失敗** 上

また、新しいAEM 6.4 インスタンスのバンドルリストとアップグレードされたインスタンスを比較して、アップグレードされていないバンドルを検出することをお勧めします。 この比較によって、`error.log` で検索すべき問題を絞り込むことができます。

### カスタムバンドルがアクティブ状態に切り替わらない {#custom-bundles-not-switching-to-the-active-state}

カスタムバンドルがアクティブ状態に切り替わらない場合は、変更 API を読み込んでいないコードが存在する可能性が高くなります。 これは、多くの場合、満たされていない依存関係につながります。

削除された API は、以前のリリースの 1 つで廃止済みとマークする必要があります。 コードの直接移行に関する手順については、この廃止のお知らせを参照してください。 Adobeは、可能な限りセマンティックバージョン管理を目的としており、バージョンで重大な変更を示すことができます。

また、問題を引き起こした変更が絶対に必要かどうかを確認し、必要がない場合は元に戻すことをお勧めします。 また、厳密なセマンティックバージョン管理に従って、パッケージ書き出しのバージョンが必要以上に増加したかどうかを確認します。

### Platform UI の不具合 {#malfunctioning-platform-ui}

アップグレード後に特定の UI 機能が正しく動作しない場合は、まずインターフェイスのカスタムオーバーレイを確認する必要があります。 一部の構造が変更され、オーバーレイに更新が必要な場合や古い場合があります。

次に、クライアントライブラリに接続されたカスタム追加の拡張機能まで追跡できる JavaScript エラーがないかを確認します。 同じことが、AEMレイアウトに問題を引き起こす可能性のあるカスタム CSS にも当てはまります。

最後に、JavaScript で処理できない設定の誤りを確認します。 このような場合は、通常、拡張機能が不適切に非アクティブ化されています。

### カスタムコンポーネント、テンプレートまたは UI 拡張の誤動作 {#malfunctioning-custom-components-templates-or-ui-extensions}

ほとんどの場合、これらの問題の根本原因は、開始されていないバンドルやパッケージがインストールされていないバンドルと同じですが、違いは、最初にコンポーネントを使用したときに発生する問題だけです。

誤ったカスタムコードを処理する方法は、まず原因を特定するためにスモークテストを実行することです。 問題を特定したら、記事のこの[リンク]の節にある推奨事項を参照して、問題の修正方法を確認します。

### 以下のカスタマイズが見つかりません {#missing-customizations-under-etc}

`/apps` と `/libs` はアップグレードで適切に処理されますが、`/etc` の下の変更はアップグレード後に `/var/upgrade/PreUpgradeBackup` から手動で復元する必要がある場合があります。手動で統合する必要があるコンテンツについては、この場所を確認してください。

### error.log と upgrade.log の分析 {#analyzing-the-error-log-and-upgrade-log}

ほとんどの状況では、問題の原因を見つけるために、ログでエラーを確認する必要があります。 ただし、アップグレードの場合は、古いバンドルが正しくアップグレードされない可能性があるので、依存関係の問題を監視する必要もあります。

これをおこなう最善の方法は、発生している問題とは無関係と思われるすべてのメッセージを削除して、error.log を削除することです。 これは、次のコマンドを使用して、grep のようなツールで実行できます。

```shell
grep -v UnrelatedErrorString
```

一部のエラーメッセージは、すぐには説明できない場合があります。 この場合、発生したコンテキストを調べると、エラーが作成された場所を把握するのに役立ちます。 次の方法でエラーを区切ることができます。

* `grep -B`（エラーの前の行を追加）

または

* `grep -A`（エラーの後の行を追加）

一部のケースでは、この状態につながる有効なケースが存在し、アプリケーションがこれが実際のエラーであるかどうかを常に判断できないので、エラーが WARN メッセージに出ることがあります。 これらのメッセージも必ずご覧ください。

### アドビサポートのご案内 {#contacting-adobe-support}

このページのアドバイスを受けてもまだ問題が発生している場合は、Adobeサポートにお問い合わせください。 お使いの事例に関するサポートエンジニアにできる限り多くの情報を提供するには、アップグレード時の upgrade.log ファイルを必ず含めてください。
