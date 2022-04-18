---
title: AEM Sites リリースノート
seo-title: AEM Sites
description: Adobe Experience Manager 6.4 Sites 固有のリリースノート
seo-description: Release notes specific to Adobe Experience Manager 6.4 Sites.
uuid: 593928ec-5d1a-4a88-bd73-897421c5984a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: 40225441-7cfe-4395-ac71-60504b42e764
exl-id: 19ec5c00-eae5-4e7f-9dc5-c7a88b06fd2a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 80%

---

# AEM Sites リリースノート {#aem-sites-release-notes}

## Sites {#sites}

AEM Sites 6.4 の機能強化について詳しくは、以下を参照してください。

### サイト管理 {#site-administration}

* 新しいコンテンツツリーレールでサイト階層内をすばやく移動できます。これをリスト表示と組み合わせれば、クラシック UI インタラクションモデルに戻してサイト内を閲覧することができます。
* 大きいフォルダーのカード表示とリスト表示でスクロール操作が向上しました。
* 検索結果の操作性が向上しました - 「戻る」ボタンをクリックすると、前の検索結果に戻ります。
* 特定のレールを開く、ページを編集、移動、削除する、プロパティを開くなどの最もよく使用されるアクションのキーボードショートカットが追加で定義されました。
* キーボードショートカットを無効にできます（環境設定で有効／無効を切り替えます）。
* すべての UI で 7 日後にタイムスタンプが非表示になります（環境設定でデフォルトを設定します）。

### ページエディター {#page-editor}

* レスポンシブサイトのプレビューに対応するデバイスのリストが更新され、Apple iPhone 8、8 Plus、X と Samsung S7 が含まれるようになりました。
* テンプレートデザイン情報のデフォルトの保存場所が /etc/design から /conf にあるサポートサイト固有の設定に移動しました。.以前の AEM リリースからアップグレードするお客様は、引き続き /etc/design を使用できます。

### コンポーネントとテンプレートの開発 {#component-amp-template-development}

* プロジェクトアーキタイプ 13 以上（[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases) を参照）。
* HTL バージョン 1.3.1 については、[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/htl-spec/releases/tag/1.3.1) を参照してください。
* コアコンポーネント 2.0.4 以上については、[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases) を参照してください。
* スタイルシステム

   * CSS クラスをコンポーネントに割り当て、ページエディターでユーザーが UI からスタイルのサブセットから選択できるようにするまったく新しい概念が追加されました。
   * コンポーネントの周辺に表示される HTML 要素名（&lt;main> や &lt;aside> など）を定義できるようになりました。

* レイアウトコンテナのグリッドシステムについては、[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid) を参照してください。
* テンプレートエディターとポリシー

   * ポリシーでは、コンポーネントごと、コンテナごと、テンプレートごとのスタイルシステム設定をサポートするようになりました。
   * 編集可能なコンポーネントでのテンプレートレイアウト定義のサポートが改善されました。

* 参照サイト We.Retail 3.0 については、[リリースノートの GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) を参照してください。

>[!CAUTION]
>
>AEM には、既存のカスタムコードとの互換性を最大限に高めるために、jQuery ライブラリのバージョン 1.12.4 が含まれています。セキュリティに関する既知の問題に対処するため、アドビによる修正がおこなわれました。

### コンテンツフラグメントとエディター {#content-fragments-amp-editor}

* コンテンツフラグメントの基盤として、構造化コンテンツモデルが導入されました。

   * モデル エディター UI
   * コンテンツフラグメントモデルの事前設定済みデータ要素（単一行テキスト、複数行テキスト、数値、ブール値、日時、列挙、コンテンツ参照、タグ）

* AEMコンテンツフラグメントエディターの使いやすさを改善しました

   * すべての要素を表示する概要画面
   * 単一要素のフルスクリーン編集
   * リッチテキスト編集機能の強化（箇条書きリスト、番号付きリスト、インデント、ハイパーリンク、テーブル、検索と置換、スペルチェック）

* AEM コンテンツフラグメントの出力オプションの機能強化

   * 新しいコンテンツフラグメントコンポーネントをコアコンポーネントの一部として追加。[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/tree/master/extension/contentfragment/content/src/content/jcr_root/apps/core/wcm/extension/components/contentfragment/v1/contentfragment) でコードを参照してください。
   * Sling Model Exporter を介した JSON 出力でのコンテンツサービスのサポート

### エクスペリエンスフラグメント {#experience-fragments}

* エクスペリエンスフラグメント構築ブロックが導入され、コンポーネントのグループ化とバリエーション内での容易な参照により、エクスペリエンスフラグメントバリエーション間のコンテンツの再利用が促進されます。
* 参照レールを通じて、翻訳プロジェクトにエクスペリエンスフラグメントを追加できるようになりました。
* タイムラインパネルを使用してエクスペリエンスフラグメントでワークフローを開始する機能を追加しました
* 参照レールに、エクスペリエンスフラグメントがAEMのどこで使用されているかが表示されるようになりました
* テンプレートの場所を設定すると、作成者は、エクスペリエンスフラグメントテンプレートで使用できるものをグローバルレベルまたはフォルダーレベルで定義できるようになりました
* 公開／非公開などの高度なフィルター処理がファセット検索でサポートされ、結果をソーシャルメディアや Adobe Target に書き出せるようになりました。
* エクスペリエンスフラグメントを Pinterest や Facebook に書き出す際に、ソーシャルメディアへのシングルログインが可能になりました。
* AEM エクスペリエンスフラグメントが Adobe Target と統合されました。エクスペリエンスフラグメントを Adobe Target に同期させると、Target の Visual Experience Composer で使用できるオファーが Target に作成され、それを任意の Target 対応エクスペリエンスに埋め込むことができるようになります。

### 翻訳 {#translation}

* AEM 翻訳プロジェクトのユーザビリティが強化されました。

   * 1 つのプロジェクトでの複数ターゲット言語のサポート
   * 翻訳ローンチを自動的に昇格または削除するオプション
   * 翻訳プロジェクトの反復実行（毎日、毎週、毎月、毎年）をスケジュールするオプション
   * より詳細なステータス情報による翻訳プロジェクトタイルの強化

* 翻訳メモリの逆更新が導入され、AEM でコンテンツをローカルに編集した後でサードパーティ翻訳管理システム内の翻訳メモリを更新できるようになりました。
* グループ化された言語ルートを翻訳ワークフローでサポートするようになりました。
* 言語ルートに任意の名前を割り当て、ISO コードにマッピングするための JCR プロパティを使用できるようになりました。
* スマート翻訳の更新で、言語マスターブランチに追加された新しいページが認識されるようになりました
* サイト管理リスト表示での翻訳ステータスレポートが導入されました。

### マルチサイト管理（MSM） {#multi-site-management-msm}

* インメモリインデックス（LiveCopyIndex）ではなく Oak ベースのインデックスを使用することで、MSM の拡張性が向上しました。

### ローンチ {#launches}

* 大規模なサイトツリーが含まれているローンチや多数のローンチがアクティブになっている場合のパフォーマンスが向上しました。
* 複数のルートページを持つローンチの自動昇格と公開が改善されました。
* レスポンシブデバイスのプレビューが、ローンチのコンテキストで編集されたページで機能しない問題を修正しました。

### コンテンツのターゲット設定とシミュレーション {#content-targeting-simulation}

* サイト/コンテキストに基づいてセグメントを整理するためのサポートフォルダー (CQ-94620)
* サイト／コンテキスト固有のセグメントリストに対応できるように、セグメントのデフォルトの保存場所が /conf に移動しました。

### AEM と Adobe Target  {#aem-amp-adobe-target-nbsp}

* AEM エクスペリエンスフラグメントが Adobe Target と統合されました。エクスペリエンスフラグメントを Adobe Target に同期させると、Target の Visual Experience Composer で使用できるオファーが Target に作成され、それを任意の Target 対応エクスペリエンスに埋め込むことができるようになります。
* Adobe Target mbox.js バージョン 63 が含まれるようになりました。 Adobeでは、実装を at.js に切り替えることをお勧めします。
* at.js バージョン 1.2.2 が含まれるようになりました。Adobeでは、Dynamic Tag Management(DTM) または [Adobe Experience Platform Launch](https://www.adobe.com/jp/enterprise/cloud-platform/launch.html) at.js をサイトにプロビジョニングするために使用します。

### AEM と Adobe Analytics {#aem-amp-adobe-analytics}

* s_code.js H.27.5 が含まれるようになりました。 Adobeでは、実装を AppMeasurement.js に切り替えることをお勧めします
* AppMeasurement.js 1.8.0 が含まれるようになりました。 Adobeでは、Dynamic Tag Management(DTM) または [Adobe Experience Platform Launch](https://www.adobe.com/enterprise/cloud-platform/launch.html) を使用して、AppMeasurement.js をサイトにプロビジョニングします。

## Communities アドオン {#communities-add-on}

[Communities のリリースノートページ](/help/release-notes/communities-release-notes.md)を参照してください。

## Screens アドオン {#screens-add-on}

* （AEM オーサーに直接接続するのではなく）AEM パブリッシュサーバーに接続して操作や制御、およびチャネルのダウンロードを実行するために、Screens Player をサポートするようになりました。
* スケジュール内のチャネル割り当てをグループ化できるようになりました。
* チャネル割り当てには開始日と終了日が設定されるようになりました。
* デバイスダッシュボードにプレーヤーシェルとファームウェアのバージョンが表示されるようになりました。
* デバイスダッシュボードリストにプレーヤーの接続ステータスが表示されます。
* AEM Screens Player にGoogle Chrome OS サポートを追加しました。
* AEM Screens Player 用のMicrosoft Windows 10 を追加しました。
