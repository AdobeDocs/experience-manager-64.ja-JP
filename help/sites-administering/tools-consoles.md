---
title: ツールコンソール
description: Adobe Experience Manager全体の様々なツールコンソールについて説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
exl-id: 7566e1bc-8571-4b3c-b420-4324026bd4dd
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 23%

---

# ツールコンソール{#tools-consoles}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

**ツール** コンソールを使用して、web サイト、デジタルアセット、およびコンテンツリポジトリのその他の要素の管理に役立つ、数多くの専用ツールにアクセスできます。現在、には 2 種類のフレーバーがあります **ツール** コンソールは、使用している UI に応じて異なります。

* [ツール - クラシック UI](#tools-classic-ui)
* [ツール - タッチ操作向け UI](#tools-touch-optimized-ui)

## ツール - クラシック UI {#tools-classic-ui}

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
   <td>複数のサイトを一元管理する。</td> 
  </tr> 
  <tr> 
   <td>ClientContext 設定<br /> </td> 
   <td> </td> 
   <td>この <a href="/help/sites-developing/client-context.md">ClientContext</a> は、ユーザーデータを動的に組み立てたコレクションを表します。 デフォルトの Marketing Cloud 設定はここに保持されます。<br /> </td> 
  </tr> 
  <tr> 
   <td>クラウドサービス設定<br /> </td> 
   <td> </td> 
   <td>関連する設定を保持 <a href="/help/sites-administering/marketing-cloud.md">Adobe Marketing Cloudとの統合</a>.</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/ecommerce.md">Commerce</a></td> 
   <td> </td> 
   <td>インポーターや様々な製品データへのアクセスを提供します。</td> 
  </tr> 
  <tr> 
   <td>DAM -Digital Rights Management<br /> </td> 
   <td> </td> 
   <td>デジタル著作権情報とライセンスへのアクセスを提供します。</td> 
  </tr> 
  <tr> 
   <td>DAM - Health Checker<br /> </td> 
   <td> </td> 
   <td>比較 <code>/var/dam</code> および <code>/content/dam</code> およびが<br /> 不整合がある場合は、 リストに表示されたファイルやフォルダーは、同期または削除できます。 フォルダー比較のノードタイプは Web コンソールで設定できます。</td> 
  </tr> 
  <tr> 
   <td>DAM -AdobeIndesign<br /> </td> 
   <td> </td> 
   <td>AdobeIndesign と組み合わせて使用するスクリプト。</td> 
  </tr> 
  <tr> 
   <td>DAM — ビデオプロファイル<br /> </td> 
   <td> </td> 
   <td>ffmpeg トランスコーディング用に設定可能なプロファイル。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/dashboards.md">ダッシュボード</a></td> 
   <td> </td> 
   <td>レポートダッシュボードを作成できます。統合データを表示するページを定義するためのカスタマイズ可能な方法を提供します。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-developing/designer.md">デザイン</a></td> 
   <td> </td> 
   <td>使用するグラフィックや CSS ファイルなど、定義されたデザインのリストを保持します。</td> 
  </tr> 
  <tr> 
   <td>カスタムドキュメント</td> 
   <td> </td> 
   <td>ドキュメントおよびオンラインヘルプを拡張する際に使用します。</td> 
  </tr> 
  <tr> 
   <td>フォーム送信</td> 
   <td> </td> 
   <td>受信したフォーム送信のリストを保持します。</td> 
  </tr> 
  <tr> 
   <td>インポーター — <a href="/help/sites-administering/bulk-editor.md">バルクエディター</a></td> 
   <td> </td> 
   <td>項目を検索して一括編集できます。 また、リポジトリに（一括で）コンテンツを書き出したり読み込んだりすることもできます。</td> 
  </tr>
  <tr> 
   <td>インポーター — フィードインポーター</td> 
   <td> </td> 
   <td><p>フィードインポーターは、外部ソースからリポジトリにコンテンツを繰り返し読み込むためのフレームワークです。 フィードインポーターの考え方は、指定した間隔でリモートリソースをポーリングして解析し、リモートリソースのコンテンツを表すノードをコンテンツリポジトリ内に作成することです。</p> </td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/external-link-checker.md">外部リンクチェック</a></td> 
   <td> </td> 
   <td>AEMインスタンス内のすべてのコンテンツページをスキャンし、外部リンクを確認します。 有効なリンクと無効なリンクのリストが表示されます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-authoring/mobile.md">モバイル</a></td> 
   <td> </td> 
   <td>モバイルデバイス向けに設計された Web サイトを作成できます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/msm.md">MSM</a></td> 
   <td> </td> 
   <td>多言語および多国籍のコンテンツを処理し、一元化されたブランディングとローカライズされたコンテンツのバランスを取るのに役立ちます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/notification.md">通知</a></td> 
   <td> </td> 
   <td>通知テンプレート。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/package-manager.md">パッケージ</a></td> 
   <td> </td> 
   <td>AEM WCM 用に読み込まれたパッケージを表示する、パッケージマネージャーへの代替リンク。 CRX のパッケージマネージャーに表示される情報と同様です。</td> 
  </tr> 
  <tr> 
   <td>レプリケーション — <a href="/help/sites-deploying/configuring.md#replication-reverse-replication-and-replication-agents">レプリケーションエージェント</a></td> 
   <td> </td> 
   <td>ページの公開時にオーサーからパブリッシュにデータをレプリケートするため、またはリバースレプリケーションを使用して、パブリッシュ環境からオーサーにユーザーのコメントを返すために使用します。</td> 
  </tr> 
  <tr> 
   <td>インポーター — <a href="/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree">ツリーをアクティベート</a></td> 
   <td> </td> 
   <td>「 Web サイト」タブから、個々のページをアクティベートできます。 大量のコンテンツページを入力または更新した場合（すべて同じルートページの下に配置されている）、ツリー全体を 1 回の操作で簡単にアクティブ化できます。 また、ドライランを実行してアクティベートをエミュレートし、アクティベートするページをハイライトすることもできます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/reporting.md">レポート</a></td> 
   <td> </td> 
   <td>AEMには、様々なカスタマイズされたレポートが用意されており、カスタマイズされたレポートを作成したり、独自のレポートを作成したりできます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-authoring/scaffolding.md">デフォルトページ基礎モード</a></td> 
   <td> </td> 
   <td>基礎モードを使用すると、ページに必要な構造を反映したフィールドを持つフォーム（スキャフォールド）を作成し、このフォームを使用して、この構造に基づくページを簡単に作成できます。</td> 
  </tr> 
  <tr> 
   <td>セキュリティ — <a href="/help/sites-administering/notification.md">セルフサービス設定 </a> </td> 
   <td> </td> 
   <td>アカウントの作成時やパスワードのリセット時にユーザーが自動的に受け取る電子メールを設定したり、リセットされたパスワードを確認したりできます。</td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/campaign-segmentation.md">セグメント化</a></td> 
   <td> </td> 
   <td>サイト訪問者がサイトに来訪したときの興味や目標は異なります。 これらの目標を理解し、期待を満たすことは、オンラインマーケティングの重要な成功要因です。 セグメント化によって訪問者の詳細を分析し、特徴付けることが成功の実現に役立ちます。<br /> </td> 
  </tr> 
  <tr> 
   <td><a href="/help/communities/working-with-srp.md">socialconfig</a></td> 
   <td> </td> 
   <td>デフォルトの SRP 設定。 詳しくは、 <a href="/help/communities/srp-config.md">ストレージ設定</a> コンソール。</td> 
  </tr> 
  <tr> 
   <td>taskmanagement</td> 
   <td> </td> 
   <td>このエントリに関連するアクティブな機能はありません。</td> 
  </tr> 
  <tr> 
   <td>テナント</td> 
   <td> </td> 
   <td>このエントリに関連するアクティブな機能はありません。</td> 
  </tr> 
  <tr> 
   <td>バージョン管理 — <a href="/help/sites-deploying/version-purging.md">バージョンをパージ</a></td> 
   <td> </td> 
   <td>必要に応じてページのバージョンをパージできます。</td> 
  </tr> 
  <tr> 
   <td>仮想リポジトリ</td> 
   <td> </td> 
   <td>ワークスペースマウント機能を使用して仮想リポジトリを設定し、CRX および JCR コネクタに基づく JCR コンテンツインフラストラクチャへのアクセスをシンプルにする JCR 対応コンテンツアプリケーションを提供できます。</td> 
  </tr> 
  <tr> 
   <td>監視ワード</td> 
   <td> </td> 
   <td>非推奨. 詳しくは、 <a href="/help/communities/moderate-ugc.md#watchwords">コミュニティコンテンツのモデレート</a></td> 
  </tr> 
  <tr> 
   <td><a href="/help/sites-administering/workflows.md">ワークフロー</a></td> 
   <td> </td> 
   <td>ワークフローは、任意の編集プロセスをサポートするページやデジタルアセットに対する一連のアクションを制御します。</td> 
  </tr> 
 </tbody> 
</table>

## ツール - タッチ操作向け UI {#tools-touch-optimized-ui}

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
   <td>マーケティングローンチを管理</td> 
  </tr> 
  <tr> 
   <td>タスク</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-authoring/task-content.md">インボックス </a></td> 
   <td>インボックスの項目を管理します。</td> 
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
   <td><a href="/help/sites-authoring/tags.md">Tag Management</a></td> 
   <td>タグとその名前空間を整理します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="https://helpx.adobe.com/cloud-manager/using/using-cloud-manager.html">Cloud Services</a></td> 
   <td>Adobe Marketing Cloud に接続.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-administering/workflows.md">workflows</a></td> 
   <td>モデルと管理のワークフロー.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-deploying/replication.md">レプリケーション</a></td> 
   <td>複数の Web サイトを作成および管理します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-administering/reporting.md">レポート</a></td> 
   <td>カスタムレポートを作成および監視.<br /> </td> 
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
   <td>Web ベースの IDE を使用してアプリケーションを開発.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-administering/package-manager.md">パッケージ</a></td> 
   <td>アプリケーションをパッケージ化および共有.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-administering/package-manager.md#package-share">パッケージ共有</a></td> 
   <td>アドビおよびコミュニティからアプリケーションをダウンロード.<br /> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-deploying/offloading.md#administering-topologies">トポロジブラウザー</a></td> 
   <td>インスタンストポロジを表示.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-deploying/offloading.md">オフロードするブラウザー</a></td> 
   <td>オフロードを管理します。</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td><a href="/help/sites-deploying/monitoring-and-maintaining.md#backups">バックアップ</a></td> 
   <td>バックアップタスクを実行.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Web コンソール<br /> </td> 
   <td>アプリケーションプラットフォームを設定および管理.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Web コンソール設定のダンプ<br /> </td> 
   <td>Web コンソールから設定ステータスをダウンロードします。<br /> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>ユーザー</td> 
   <td>ユーザーを管理.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>グループ</td> 
   <td>グループを管理.</td> 
  </tr> 
  <tr> 
   <td>外部リソース<br /> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>ドキュメント化</td> 
   <td>Web Experience Management のマニュアルを表示.<br /> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>開発者リソース</td> 
   <td>開発者向けリソースおよびダウンロード.</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>上記のオプションの一部は、実際にはクラシック UI にリンクします。
