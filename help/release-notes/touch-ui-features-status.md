---
title: タッチ操作対応 UI 機能のステータス
seo-title: Touch UI Feature Status
description: Adobe Experience Manager 6.3 タッチ操作対応 UI に固有のリリースノート
seo-description: Release notes specific to Adobe Experience Manager 6.3 Touch UI.
uuid: dc335334-6c50-4cee-8a2e-183958742686
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: 482b5eb0-1b15-4f10-a9d8-3b72dd74acf8
exl-id: e1422581-143b-4fce-976e-e5aa3360e2d0
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 56%

---

# タッチ操作対応 UI 機能のステータス {#touch-ui-feature-status}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!CAUTION]
>
>AEMバージョン 6.4 では、 [クラシック UI は非推奨です](/help/release-notes/deprecated-removed-features.md). Adobeはクラシック UI をさらに強化する予定はありません。ユーザーは、タッチ操作対応 UI で利用できる強力な新機能を活用することをお勧めします。

バージョン 6.0 以降、AEMでは、Adobe Marketing CloudとAdobeのユーザーインターフェイスの全体的なガイドラインに合わせて、「タッチ操作対応 UI」（別名「タッチ UI」）と呼ばれる新しいユーザーインターフェイスが導入されました。 ほぼ機能的な特性に到達したことで、これは、従来のデスクトップ向けインターフェイス（「クラシック UI」と呼ばれる）を備えたAEMの標準 UI になりました。

ほとんどの機能はタッチ操作対応 UI に搭載されていますが、まだ完成せず、今後のリリースで追加される機能もあります。

次のリストは、AEM 6.4 で実装されている機能の現在のステータスです。

AEM 6.4 にアップグレードするお客様の推奨事項については、 [お客様向けのユーザーインターフェイスRecommendations](/help/sites-deploying/ui-recommendations.md) 」を参照してください。

>[!NOTE]
>
>このページで扱うのは、クラシック UI と同等の機能のみです。
>
>クラシック UI に存在しない、タッチ操作対応 UI に追加された独自の機能は一覧に表示されません。

>[!NOTE]
>
>このリストは完成を目指していますが、すべてを網羅したものとは考えないでください。

## 凡例 {#legend}

* **完了**:この機能は、タッチ操作対応 UI で完全に使用できます
* **ほぼ完全**：この機能はタッチ操作対応 UI でほぼ完全に利用できます。
* **見つかりません**:この機能はタッチ操作対応 UI には存在しません。この操作をおこなうには、クラシック UI を使用する必要があります。
* **置換済み**:この機能は、動作が異なる新しい実装に置き換えられました。
* **削除**：この機能は、現在タッチ操作対応 UI に存在せず、置換もされません。

## 機能ステータス：サイト管理 {#feature-status-sites-admin}

これは、クラシック UI のサイト管理（`/siteadmin`）に用意されている機能とタッチ操作対応 UI（`/sites.html`） のステータスの一覧です。

<table> 
 <tbody>
  <tr>
   <td><strong>機能<br /> </strong></td> 
   <td><strong>ステータス<br /> </strong></td> 
   <td><strong>コメント</strong></td> 
  </tr>
  <tr>
   <td>サイト階層を移動</td> 
   <td>完全<br /> </td> 
   <td>AEM 6.4 では、<a href="/help/sites-authoring/basic-handling.md#content-tree">コンテンツツリー表示</a>が導入されました。</td> 
  </tr>
  <tr>
   <td>ワークフローを開始</td> 
   <td>完全<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ページを新規作成</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>新しいサイトを作成</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>新しいローンチを作成</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ライブコピーを新規作成 <br /> </td> 
   <td>完了<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>フォルダーを作成</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>公開ステータスを表示</td> 
   <td>ほぼ完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>検索</td> 
   <td>完全<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ページをコピー/貼り付け（複製）</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ページを移動</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ページを公開</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>レプリケーション権限を持たないページを公開</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>後で公開する</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ツリーを公開</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ページを非公開にする</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>レプリケーション権限のないページを非公開にする</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>後で非公開</td> 
   <td>完全<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>削除</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ロック/ロック解除</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>プロパティを表示/編集</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ページに対する権限の設定</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>バージョン履歴</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>バージョンを復元</td> 
   <td>完全<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ツリーを復元し、削除されたページを復元します</td> 
   <td>見つかりません</td> 
   <td>クラシック UI を使用します。</td> 
  </tr>
  <tr>
   <td>古いバージョンと現在のバージョンの違いを表示<br />。 </td> 
   <td>完了<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ライブコピーアクション（ロールアウト）</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>言語コピーを参照</td> 
   <td>完全</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>検索と置換</td> 
   <td>見つかりません<br /> </td> 
   <td>クラシック UI を使用します。</td> 
  </tr>
  <tr>
   <td>通知インボックス（JCR イベント）</td> 
   <td>見つかりません</td> 
   <td>クラシック UI を使用します。 別の実装に置き換えられます。</td> 
  </tr>
  <tr>
   <td>参照</td> 
   <td>ほぼ完全</td> 
   <td>受信ページのリンクの表示は、AEMの 2019 リリースで追加されます。</td> 
  </tr>
 </tbody>
</table>

## 機能ステータス：ページエディター {#feature-status-page-editor}

これは、クラシック UI ページエディター（`/cf#`/#）が持つ機能およびタッチ操作対応 UI（`/editor.html`/）のステータスの一覧です。

<table> 
 <tbody>
  <tr>
   <td><strong>機能</strong></td> 
   <td><strong>ステータス</strong></td> 
   <td><strong>コメント</strong></td> 
  </tr>
  <tr>
   <td>Web ページを編集</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>モバイル Web ページを編集<br />。 </td> 
   <td>完了<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>デザインインポーターを介して読み込んだコンテンツを編集<br /> </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>電子メールを編集</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>モバイルアプリを編集</td> 
   <td>完了<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>フォームを編集</td> 
   <td>完了<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>オファーを編集</td> 
   <td>完了<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ワークフローモデルを編集<br /> </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>コード：編集とプレビュー</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>レスポンシブプレビュー<br />。 </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>モード：デザインを編集</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>モード：基礎モード</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>モード：ライブコピーステータス<br />。 </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>注釈の追加</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>プロパティの編集<br />。 </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ページをロールアウト</td> 
   <td>完了<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ワークフローを開始および表示</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ワークフローパッケージ処理</td> 
   <td>ほぼ完全</td> 
   <td>タッチ操作対応 UI から完全にアクセス可能。クラシック UI では、複数のワークフローペイロードが引き続き表示されます。<br />。 </td> 
  </tr>
  <tr>
   <td>ページのロック/ロック解除</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ページを公開 <br /> </td> 
   <td>完了<br /> </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ページを非公開</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ページをコピー</td> 
   <td>削除<br />。 </td> 
   <td>サイト管理を使用して<a href="/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page">ページをコピー</a>します。<br /> </td> 
  </tr>
  <tr>
   <td>ページを移動</td> 
   <td>削除済み</td> 
   <td>サイト管理を使用して<a href="/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page">ページを移動</a>します。<br />。 </td> 
  </tr>
  <tr>
   <td>ページを削除</td> 
   <td>削除済み</td> 
   <td>サイト管理を使用して<a href="/help/sites-authoring/managing-pages.md#deleting-a-page">ページを削除</a>します。<br />。 </td> 
  </tr>
  <tr>
   <td>参照を表示</td> 
   <td>削除済み</td> 
   <td>サイト管理者を使用して <a href="/help/sites-authoring/author-environment-tools.md#references">詳細なリファレンスリストを参照</a>.<br /> </td> 
  </tr>
  <tr>
   <td>監査ログ</td> 
   <td>削除済み</td> 
   <td>サイト管理を使用して<a href="/help/sites-authoring/author-environment-tools.md#events-timeline">アクティビティレールを開きます</a>。<br />。 </td> 
  </tr>
  <tr>
   <td>バージョンを作成</td> 
   <td>削除済み</td> 
   <td>サイト管理を使用して<a href="/help/sites-authoring/working-with-page-versions.md#creating-a-new-version">バージョンを新規作成</a>します。<br />。 </td> 
  </tr>
  <tr>
   <td>バージョンの復元</td> 
   <td>削除済み</td> 
   <td>サイト管理者を使用して <a href="/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version">バージョンを復元</a>.</td> 
  </tr>
  <tr>
   <td>起動を切り替え</td> 
   <td>削除済み</td> 
   <td>サイト管理を使用して<a href="/help/sites-authoring/launches-promoting.md">ローンチを切り替え</a>ます。<br />。 </td> 
  </tr>
  <tr>
   <td>ページを翻訳</td> 
   <td>削除済み</td> 
   <td>サイト管理を使用して<a href="/help/sites-administering/tc-manage.md">翻訳プロジェクトにページを追加</a>します。<br />。 </td> 
  </tr>
  <tr>
   <td>タイムワープ（日付／時刻を選択してその指定日時の時点のサイトを表示）<br /> </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>権限の設定</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>クライアントコンテキスト UI<br />。 </td> 
   <td>置換</td> 
   <td>以下を使用： <a href="/help/sites-authoring/ch-previewing.md">ContextHub</a> UI を今後も開始します。</td> 
  </tr>
  <tr>
   <td>各種メディアタイプのコンテンツファインダー<br />。 </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>コンポーネントリスト</td> 
   <td>完了<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>コンポーネントのコピーと貼り付け<br /> </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>クリップボード内のコンポーネントのリスト</td> 
   <td>見つかりません</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>取り消し／やり直し</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>コンテンツをコンポーネントプレースホルダーにドラッグ&amp;ドロップ</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>コンテンツを parsys プレースホルダーに直接ドラッグ&amp;ドロップし、コンポーネントを自動作成<br /> </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

## 機能ステータス：テキスト、テーブルおよび画像エディター {#feature-status-text-table-and-image-editors}

これは、クラシック UI のテキスト、テーブルおよび画像エディターが持つ機能およびタッチ操作向け UI でのステータスの一覧です。

<table> 
 <tbody>
  <tr>
   <td><strong>機能</strong></td> 
   <td><strong>ステータス </strong></td> 
   <td><strong>コメント<br /> </strong></td> 
  </tr>
  <tr>
   <td>リッチテキストエディター</td> 
   <td>完了</td> 
   <td>インプレース、ダイアログおよびフルスクリーンで使用できます。</td> 
  </tr>
  <tr>
   <td>RTE プラグインの有効化／無効化</td> 
   <td>完了<br />。 </td> 
   <td><a href="/help/sites-authoring/templates.md">テンプレートエディター</a>を使用して実行できます。</td> 
  </tr>
  <tr>
   <td>プレーンテキストに RTE を使用</td> 
   <td>完了<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：リンクとアンカー</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：文字マップ</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：コピー／貼り付け</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：Microsoft Word から貼り付け<br />。 </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：検索と置換</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：テキストフォーマット（太字、...）</td> 
   <td>完了<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：下付き文字と上付き文字</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：均等揃え</td> 
   <td>完了<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：リスト（箇条書き／番号付き）</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：段落書式</td> 
   <td>完了<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：テキストスタイル</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：ソースエディター（HTML の編集）<br />。 </td> 
   <td>完了<br /> </td> 
   <td>ダイアログとフルスクリーンでのみ使用できます。<br /> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：スペルチェッカー</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：テーブル（埋め込みテーブルエディター）</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：取り消し／やり直し<br />。 </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>RTE プラグイン：インライン画像を許可</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>テーブルエディター</td> 
   <td>完了</td> 
   <td>インプレース、ダイアログおよびフルスクリーンで使用できます。<br />。 </td> 
  </tr>
  <tr>
   <td>表のセルに画像をドラッグ&amp;ドロップ<br /> </td> 
   <td>完了</td> 
   <td>インラインで使用可能</td> 
  </tr>
  <tr>
   <td>画像エディター<br />。 </td> 
   <td>完了</td> 
   <td>インプレース、ダイアログおよびフルスクリーンで使用できます。<br />。 </td> 
  </tr>
  <tr>
   <td>IPE プラグインの有効化／無効化</td> 
   <td>完了</td> 
   <td>現在、 <a href="/help/sites-authoring/templates.md">テンプレートエディター</a>.</td> 
  </tr>
  <tr>
   <td>IPE プラグイン：切り抜き</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>IPE プラグイン：反転</td> 
   <td>完了<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>IPE プラグイン：取り消し／やり直し</td> 
   <td>完了<br />。 </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>IPE プラグイン：画像マップ</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>IPE プラグイン：回転</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>IPE プラグイン：ズーム</td> 
   <td>完了<br />。 </td> 
   <td> </td> 
  </tr>
 </tbody>
</table>

## 機能ステータス：ツール {#feature-status-tools}

これは、クラシック UI の様々なツールと、タッチ操作対応 UI のステータスのリストです。

<table> 
 <tbody>
  <tr>
   <td><strong>機能<br /> </strong></td> 
   <td><strong>ステータス<br /> </strong></td> 
   <td><strong>コメント</strong></td> 
  </tr>
  <tr>
   <td>タスク管理</td> 
   <td>置換</td> 
   <td>6.0 を導入 <a href="/help/sites-authoring/projects.md">プロジェクトとタスク</a>.<br /> </td> 
  </tr>
  <tr>
   <td>ワークフローインボックス<br /> </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ワークフローからページテンプレートの設定（<code>/etc/workflow/wcm/templates.html</code>）</td> 
   <td>見つかりません<br /> </td> 
   <td>クラシック UI を使用します。</td> 
  </tr>
  <tr>
   <td>管理 UI のタグ付け<br />。 </td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>MSM／ブループリントコントロールセンター</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ブループリントマネージャー UI</td> 
   <td>完了</td> 
   <td> </td> 
  </tr>
  <tr>
   <td>ロールアウト設定 UI</td> 
   <td>見つかりません</td> 
   <td>クラシック UI を使用します。</td> 
  </tr>
  <tr>
   <td>ユーザー、グループ、権限 UI<br /> </td> 
   <td>ほぼ完了<br /> </td> 
   <td>詳細な権限編集の場合は、クラシック UI を使用します。<br /> </td> 
  </tr>
  <tr>
   <td>バージョンをパージ（<code>/etc/versioning/purge.html</code>）</td> 
   <td>見つかりません</td> 
   <td>クラシック UI を使用します。</td> 
  </tr>
  <tr>
   <td>外部リンクチェッカー（<code>/etc/linkchecker.html</code>）</td> 
   <td>見つかりません</td> 
   <td>クラシック UI を使用します。<br /> </td> 
  </tr>
  <tr>
   <td>バルクエディター（<code>/etc/importers/bulkeditor.html</code>）</td> 
   <td>見つかりません<br /> </td> 
   <td>クラシック UI を使用します。</td> 
  </tr>
 </tbody>
</table>
