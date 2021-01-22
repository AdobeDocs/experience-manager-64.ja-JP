---
title: ツールコンソール
description: Adobe Experience Manager中の様々なツールコンソールについて説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
translation-type: tm+mt
source-git-commit: 425f1e6288cfafc3053877a43fa0a20fd5d2f3ac
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 97%

---


# ツールコンソール{#tools-consoles}

**ツール**&#x200B;コンソールを使用して、Web サイト、デジタルアセット、およびコンテンツリポジトリのその他の要素の管理に役立つ、数多くの専用ツールにアクセスできます。現時点では、お使いの UI に応じて 2 種類の&#x200B;**ツール**&#x200B;コンソールを選択できます。

* [ツール - クラシック UI](#tools-classic-ui)
* [ツール - タッチ操作向け UI](#tools-touch-optimized-ui)

## ツール - クラシック UI  {#tools-classic-ui}

<table> 
 <tbody> 
  <tr> 
   <th>ページまたはフォルダー</th> 
   <th> </th> 
   <th>目的</th> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/msm.md">MSM コントロールセンター</a></td> 
   <td> </td> 
   <td>複数のサイトを統合管理するための場所です。</td> 
  </tr> 
  <tr> 
   <td>ClientContext 設定<br /> </td> 
   <td> </td> 
   <td><a href="/help/sites-developing/client-context.md">ClientContext</a> はユーザーデータを動的にまとめたコレクションを表します。デフォルトの Marketing Cloud 設定はここに保持されます。<br /> </td> 
  </tr> 
  <tr> 
   <td>クラウドサービスの設定<br /> </td> 
   <td> </td> 
   <td><a href="/help/sites-administering/marketing-cloud.md">Adobe Marketing Cloud との統合</a>に関連する設定を保持します。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/ecommerce.md">Commerce</a></td> 
   <td> </td> 
   <td>インポーターと様々な製品データにアクセスできます。</td> 
  </tr> 
  <tr> 
   <td>DAM - デジタル著作権管理<br /> </td> 
   <td> </td> 
   <td>デジタル著作権情報とライセンスにアクセスできます。</td> 
  </tr> 
  <tr> 
   <td>DAM - ヘルスチェック<br /> </td> 
   <td> </td> 
   <td><code>/var/dam</code>と<code>/content/dam</code>を比較し、<br />に矛盾がないかチェックします。 その後で、リスト内のファイルとフォルダーを同期または削除できます。フォルダー比較用のノードタイプを Web コンソールで設定できます。</td> 
  </tr> 
  <tr> 
   <td>DAM - Adobe Indesign<br /> </td> 
   <td> </td> 
   <td>Adobe Indesign と共に使用するスクリプトです。</td> 
  </tr> 
  <tr> 
   <td>DAM - ビデオプロファイル<br /> </td> 
   <td> </td> 
   <td>ffmpeg のトランスコーディング用に設定可能なプロファイルです。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/dashboards.md">ダッシュボード</a></td> 
   <td> </td> 
   <td>レポートダッシュボードを作成できます。これらのダッシュボードのカスタマイズ可能な方法を使用して、統合されたデータを表示するページを定義できます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-developing/designer.md">デザイン</a></td> 
   <td> </td> 
   <td>定義済みのデザイン（使用するグラフィックと css ファイルを含む）のリストを保持します。</td> 
  </tr> 
  <tr> 
   <td>カスタムドキュメント</td> 
   <td> </td> 
   <td>ドキュメントとオンラインヘルプを拡張する場合に使用します。</td> 
  </tr> 
  <tr> 
   <td>フォームの送信</td> 
   <td> </td> 
   <td>受信済みのフォームの送信のリストを保持します。</td> 
  </tr> 
  <tr> 
   <td>インポーター - <a href="/help/sites-administering/bulk-editor.md">バルクエディター</a></td> 
   <td> </td> 
   <td>項目を検索して一括編集できます。また、リポジトリに対するコンテンツの（一括）書き出し／読み込みをおこなうこともできます。</td> 
  </tr>
  <tr> 
   <td>インポーター - フィードインポーター</td> 
   <td> </td> 
   <td><p>フィードインポーターは、外部ソースからリポジトリにコンテンツを繰り返し読み込むためのフレームワークです。フィードインポーターという概念は、指定の間隔でリモートリソースをポーリングして解析し、リモートリソースのコンテンツを表すノードをコンテンツリポジトリに作成するためのものです。</p> </td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/external-link-checker.md">外部リンクチェック</a></td> 
   <td> </td> 
   <td>AEM インスタンス内のコンテンツページをすべてスキャンして、外部リンクをチェックします。有効なリンクと無効なリンクのリストが表示されます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-authoring/mobile.md">モバイル</a></td> 
   <td> </td> 
   <td>モバイルデバイス用にデザインされた Web サイトの作成を支援します。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/msm.md">MSM</a></td> 
   <td> </td> 
   <td>多言語および多国籍のコンテンツを処理し、統一したブランドの確立とコンテンツのローカライズの間のバランスを取るのに役立ちます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/notification.md">通知</a></td> 
   <td> </td> 
   <td>通知テンプレートです。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/package-manager.md">パッケージ</a></td> 
   <td> </td> 
   <td>AEM WCM 用に読み込まれたパッケージを表示するパッケージマネージャーへの代替リンクです。CRX のパッケージマネージャーに表示される情報に類似しています。</td> 
  </tr> 
  <tr> 
   <td>レプリケーション - <a href="/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents">レプリケーションエージェント</a></td> 
   <td> </td> 
   <td>ページを公開する際に、オーサー環境からパブリッシュ環境にデータをレプリケーションするために使用します。または、ユーザーのコメントをパブリッシュ環境からオーサー環境に戻すリバースレプリケーションで使用します。</td> 
  </tr> 
  <tr> 
   <td>インポーター - <a href="/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree">ツリーをアクティベート</a></td> 
   <td> </td> 
   <td>「Web サイト」タブから、個々のページをアクティベートできます。多数のコンテンツページを入力または更新した場合、これらのページがすべて同じルートページの下にあれば、ツリー全体を 1 回の操作で簡単にアクティベートできます。また、ドライランを実行してアクティベートをエミュレートし、アクティベートされたページをハイライト表示することもできます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/reporting.md">レポート</a></td> 
   <td> </td> 
   <td>AEM にはカスタマイズ用の様々なレポートが用意されています。レポートをカスタマイズしたり、独自のレポートを作成したりできます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-authoring/scaffolding.md">デフォルトページの基礎モード</a></td> 
   <td> </td> 
   <td>基礎モードを使用すると、ページに必要な構造を反映したフィールドを使用してフォーム（基礎）を作成し、このフォームを使用して必要な構造に基づいたページを簡単に作成できます。</td> 
  </tr> 
  <tr> 
   <td>セキュリティ - <a href="/help/sites-administering/notification.md">セルフサービス設定</a> </td> 
   <td> </td> 
   <td>アカウントの作成やパスワードのリセットをおこなったときにユーザーが自動的に受信する電子メールを設定したり、リセットされたパスワードを確認したりできます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/campaign-segmentation.md">セグメント化</a></td> 
   <td> </td> 
   <td>サイトにアクセスする訪問者は、様々な関心と目的を持っています。その目的を理解し、期待に応えることが、オンラインマーケティングを成功させるための重要な要因となります。セグメント化によって訪問者の詳細を分析し、特徴付けることが成功の実現に役立ちます。<br /> </td> 
  </tr> 
  <tr> 
   <td><a href="/help/communities/working-with-srp.md">socialconfig</a></td> 
   <td> </td> 
   <td>デフォルトの SRP 設定。<a href="/help/communities/srp-config.md">ストレージ設定</a>コンソールを参照してください。</td> 
  </tr> 
  <tr> 
   <td>taskmanagement</td> 
   <td> </td> 
   <td>このエントリに関連するアクティブな機能はありません。</td> 
  </tr> 
  <tr> 
   <td>tenants</td> 
   <td> </td> 
   <td>このエントリに関連するアクティブな機能はありません。</td> 
  </tr> 
  <tr> 
   <td>バージョン管理 - <a href="/help/sites-deploying/version-purging.md">バージョンのパージ</a></td> 
   <td> </td> 
   <td>必要に応じてページのバージョンをパージできます。</td> 
  </tr> 
  <tr> 
   <td>仮想リポジトリ</td> 
   <td> </td> 
   <td>ワークスペースのマウント機能を使用して仮想リポジトリを設定できます。これにより、JCR に対応したコンテンツアプリケーションにおいて、CRX と JCR コネクターに基づく JCR コンテンツインフラストラクチャに簡単にアクセスできるようになります。</td> 
  </tr> 
  <tr> 
   <td>監視ワード</td> 
   <td> </td> 
   <td>使用されなくなりました。<a href="/help/communities/moderate-ugc.md#watchwords">コミュニティのコンテンツのモデレート</a>を参照してください。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/workflows.md">ワークフロー</a></td> 
   <td> </td> 
   <td>ワークフローは、編集プロセスをサポートするページまたはデジタルアセットに対する一連のアクションを制御します。</td> 
  </tr> 
 </tbody> 
</table>

## ツール - タッチ操作向け UI  {#tools-touch-optimized-ui}

<table> 
 <tbody> 
  <tr> 
   <th>セクション</th> 
   <th>オプション</th> 
   <th>目的</th> 
  </tr> 
  <tr> 
   <td>オーサリング</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-classic-ui-authoring/classic-personalization-campaigns.md">キャンペーン</a></td> 
   <td>マーケティングキャンペーンを管理します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-authoring/launches.md">ローンチ</a></td> 
   <td>マーケティングローンチを管理します。</td> 
  </tr> 
  <tr> 
   <td>タスク</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-authoring/task-content.md">インボックス</a></td> 
   <td>インボックス項目を管理します。</td> 
  </tr> 
  <tr> 
   <td>運用</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-administering/security.md">ユーザーとグループ </a></td> 
   <td>ユーザーとグループを管理します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-authoring/tags.md">タグ管理</a></td> 
   <td>タグとその名前空間を整理します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="https://helpx.adobe.com/cloud-manager/using/using-cloud-manager.html">Cloud Services </a></td> 
   <td>Adobe Marketing Cloud に接続します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-administering/workflows.md">ワークフロー</a></td> 
   <td>ワークフローをモデル化および管理します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-deploying/replication.md">レプリケーション</a></td> 
   <td>複数の Web サイトを作成および管理します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-administering/reporting.md">レポート</a></td> 
   <td>カスタムレポートを作成および監視します。<br /> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-developing/hobbes.md">テスト</a></td> 
   <td>アプリケーション用に定義されたテストを実行.</td> 
  </tr> 
  <tr> 
   <td>Granite の操作</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-developing/developing-with-crxde-lite.md">CRXDE Lite</a></td> 
   <td>Web ベースの IDE を使用してアプリケーションを開発します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-administering/package-manager.md">パッケージ</a></td> 
   <td>アプリケーションをパッケージ化および共有します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-administering/package-manager.md#package-share">パッケージ共有</a></td> 
   <td>アドビおよびコミュニティからアプリケーションをダウンロードします。<br /> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-deploying/offloading.md#administering-topologies">トポロジブラウザー</a></td> 
   <td>インスタンストポロジを表示します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-deploying/offloading.md">オフロードするブラウザー</a></td> 
   <td>オフロードを管理します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#backups">バックアップ</a></td> 
   <td>バックアップタスクを実行します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Web コンソール<br /> </td> 
   <td>アプリケーションプラットフォームを設定および管理します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Web コンソール設定のダンプ<br /> </td> 
   <td>Web コンソールから設定ステータスをダウンロードします。<br /> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>ユーザー</td> 
   <td>ユーザーを管理します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>グループ</td> 
   <td>グループを管理します。</td> 
  </tr> 
  <tr> 
   <td>外部リソース<br /> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>ドキュメント</td> 
   <td>Web Experience Management のドキュメントを表示します。<br /> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>開発者リソース</td> 
   <td>開発者向けリソースおよびダウンロードです。</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>上述のオプションのいくつかは実際にはクラシック UI にリンクしています。

