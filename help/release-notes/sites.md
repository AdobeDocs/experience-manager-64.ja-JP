---
title: AEM Sitesリリースノート
seo-title: AEM Sites
description: リリースノート (Adobe Experience Manager 6.4 Sites 固有 )
seo-description: Release notes specific to Adobe Experience Manager 6.4 Sites.
uuid: 593928ec-5d1a-4a88-bd73-897421c5984a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: 40225441-7cfe-4395-ac71-60504b42e764
exl-id: 19ec5c00-eae5-4e7f-9dc5-c7a88b06fd2a
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 9%

---

# AEM Sitesリリースノート {#aem-sites-release-notes}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## Sites {#sites}

AEM Sites 6.4 の機能強化について詳しくは、以下を参照してください。

### サイト管理 {#site-administration}

* 新しいコンテンツツリーレールでサイト階層をすばやく移動できるようになりました。 リストビューと組み合わせて、クラシック UI のインタラクションモデルに戻し、サイトを参照します。
* 大きなフォルダーのカード表示とリスト表示でのスクロールを改善しました。
* 検索結果とのやり取りが改善されました。「戻る」ボタンをクリックすると、前の検索結果に戻ります。
* 特定のレールを開く、ページを編集、移動および削除する、プロパティを開くなど、ほとんどの一般的なアクションのキーボードショートカットが追加されました。
* キーボードショートカットを無効にする機能（環境設定での有効/無効）。
* 7 日後にすべての UI でタイムスタンプの表示を停止します（環境設定でデフォルトに設定）。

### ページエディター {#page-editor}

* レスポンシブサイトプレビュー用にデバイスリストが更新され、Apple iPhone 8、8 Plus および X、Samsung S7 が含まれるようになりました。
* /conf 内のサイト固有の設定をサポートするために、テンプレートデザイン情報のデフォルトの場所を/etc/design から移動しました。 以前のAEMリリースからアップグレードしたお客様は、引き続き/etc/design を使用できます。

### コンポーネントとテンプレートの開発 {#component-amp-template-development}

* プロジェクトアーキタイプ 13 以降 ( [リリースノート用の GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases).
* HTL バージョン 1.3.1 については、[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/htl-spec/releases/tag/1.3.1) を参照してください。
* コアコンポーネント 2.0.4 以上については、[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases) を参照してください。
* スタイルシステム

   * CSS クラスをコンポーネントに割り当て、ページエディターのユーザーが UI を使用してスタイルのサブセットから選択できるようにする、まったく新しい概念が追加されました。
   * コンポーネントの周囲にレンダリングされるHTML要素名を定義する機能を追加しました。例： &lt;main>, &lt;aside>

* レイアウトコンテナのグリッドシステムについては、[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid) を参照してください。
* テンプレートエディターとポリシー

   * ポリシーで、コンポーネントごと、コンテナごと、テンプレートごとのスタイルシステム設定がサポートされるようになりました。
   * 編集可能なコンポーネント上のテンプレートでのレイアウトの定義のサポートを改善しました。

* 参照サイト We.Retail 3.0 については、[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) を参照してください。

>[!CAUTION]
>
>AEM には、既存のカスタムコードとの互換性を最大限に高めるために、jQuery ライブラリのバージョン 1.12.4 が含まれています。セキュリティに関する既知の問題に対処するため、アドビによる修正がおこなわれました。

### コンテンツフラグメントとエディター {#content-fragments-amp-editor}

* コンテンツフラグメントの基盤として構造化コンテンツモデルを導入しました。

   * モデルエディター UI
   * コンテンツフラグメントモデル用に事前設定されたデータ要素（1 行テキスト、複数行テキスト、数値、ブール値、日時、列挙、コンテンツ参照、タグ）

* AEMコンテンツフラグメントエディターの使いやすさを改善しました

   * すべての要素を表示：概要
   * 単一要素に対するフルスクリーン編集
   * リッチテキスト編集機能の強化（箇条書きリスト、番号付きリスト、インデント、ハイパーリンク、テーブル、検索と置換、スペルチェック）

* AEMコンテンツフラグメントの出力オプションの拡張が追加されました。

   * 新しいコンテンツフラグメントコンポーネントをコアコンポーネントの一部として追加しました。 [GitHub のコードを参照してください。](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/tree/master/extension/contentfragment/content/src/content/jcr_root/apps/core/wcm/extension/components/contentfragment/v1/contentfragment)
   * Sling Model Exporter を介した JSON 出力でのコンテンツサービスのサポート

### エクスペリエンスフラグメント  {#experience-fragments}

* エクスペリエンスフラグメント構築ブロックが導入され、コンポーネントをグループ化し、バリエーション内で簡単に参照できるようにして、エクスペリエンスフラグメントバリエーション間のコンテンツの再利用を容易にしました。
* 参照レールを使用してエクスペリエンスフラグメントを翻訳プロジェクトに追加する機能を追加しました
* タイムラインパネルを使用してエクスペリエンスフラグメントでワークフローを開始する機能を追加しました
* 参照レールに、エクスペリエンスフラグメントがAEMのどこで使用されているかが表示されるようになりました
* テンプレートの場所を設定すると、作成者は、エクスペリエンスフラグメントテンプレートで使用できるものをグローバルレベルまたはフォルダーレベルで定義できるようになりました
* ファセット検索で、公開済み/未公開などの高度なフィルタリングをサポートし、ソーシャルメディアやAdobe Targetに書き出せるようになりました
* エクスペリエンスフラグメントをPinterestまたはFacebookに書き出す際の単一のソーシャルメディアログインを追加しました。
* AEM Experience Fragments をAdobe Targetと統合しました。 エクスペリエンスフラグメントを Target に同期すると、Adobe Targetでオファーが作成され、Target の Visual Experience Composer と共に使用して、Target が有効な任意のエクスペリエンスに埋め込むことができます。

### 翻訳 {#translation}

* AEM Translation プロジェクトの使いやすさの強化：

   * 1 つのプロジェクトでの複数のターゲット言語のサポート
   * 翻訳ローンチを自動的に昇格および削除するオプション
   * 翻訳プロジェクトの定期的な実行をスケジュールするオプション（日別、週別、月別、年別）
   * 翻訳プロジェクトタイルがより詳細なステータス情報で強化されました

* AEMでローカルコンテンツを編集した後にサードパーティの翻訳管理システムで翻訳メモリを更新するために、逆翻訳メモリの更新が導入されました。
* 翻訳ワークフローで、グループ化された言語ルートがサポートされるようになりました
* 言語ルートに任意の名前を割り当て、ISO コードにマッピングするために JCR プロパティを使用する機能を追加しました。
* スマート翻訳の更新で、言語マスターブランチに追加された新しいページが認識されるようになりました
* サイト管理者リスト表示での翻訳ステータスレポートの導入

### マルチサイト管理（MSM） {#multi-site-management-msm}

* Oak ベースのインデックスとインメモリ (LiveCopyIndex) を使用することで、MSM の拡張性が向上しました。

### ローンチ {#launches}

* 大きなサイトツリーを含む起動のパフォーマンスを向上し、多数の起動がアクティブな場合もパフォーマンスを向上しました。
* 複数のルートページを持つローンチの自動昇格と公開を改善しました。
* レスポンシブデバイスのプレビューが、ローンチのコンテキストで編集されたページで機能しない問題を修正しました。

### コンテンツのターゲティングとシミュレーション {#content-targeting-simulation}

* サイト/コンテキストに基づいてセグメントを整理するためのサポートフォルダー (CQ-94620)
* セグメントのデフォルトの場所を/conf に移動し、サイト/コンテキスト固有のセグメントリストを取得しました。

### AEM &amp; Adobe Target  {#aem-amp-adobe-target-nbsp}

* AEM Experience Fragments をAdobe Targetと統合しました。 エクスペリエンスフラグメントを Target に同期すると、Adobe Targetでオファーが作成され、Target の Visual Experience Composer と共に使用して、Target が有効な任意のエクスペリエンスに埋め込むことができます。
* Adobe Target mbox.js バージョン 63 が含まれるようになりました。 Adobeでは、実装を at.js に切り替えることをお勧めします。
* at.js バージョン 1.2.2 が含まれるようになりました。 Adobeでは、Dynamic Tag Management(DTM) または [Adobe Experience Platform Launch](https://www.adobe.com/enterprise/cloud-platform/launch.html) at.js をサイトにプロビジョニングするために使用します。

### AEM &amp; Adobe Analytics {#aem-amp-adobe-analytics}

* s_code.js H.27.5 が含まれるようになりました。 Adobeでは、実装を AppMeasurement.js に切り替えることをお勧めします
* AppMeasurement.js 1.8.0 が含まれるようになりました。 Adobeでは、Dynamic Tag Management(DTM) または [Adobe Experience Platform Launch](https://www.adobe.com/enterprise/cloud-platform/launch.html) を使用して、AppMeasurement.js をサイトにプロビジョニングします。

## Communities アドオン {#communities-add-on}

詳しくは、 [Communities リリースノートページ](/help/release-notes/communities-release-notes.md)

## Screens アドオン {#screens-add-on}

* (AEM作成者に直接ではなく ) コマンドと制御およびチャネルのダウンロード用に、AEM Player が Screens Player に接続できるようになりました。
* スケジュールでチャネル割り当てをグループ化する機能を追加しました。
* チャネルの割り当てに開始日と終了日が設定されました
* デバイスダッシュボードにプレーヤーシェルとファームウェアバージョンが表示されるようになりました
* デバイスダッシュボードリストにプレーヤーの接続状態が表示されます
* AEM Screens Player にGoogle Chrome OS サポートを追加しました。
* AEM Screens Player 用のMicrosoft Windows 10 を追加しました。
