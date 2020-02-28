---
title: AEM Assets リリースノート
seo-title: AEM Assets
description: Adobe Experience Manager 6.4 Assets 固有のリリースノート。
seo-description: Adobe Experience Manager 6.4 Assets 固有のリリースノート。
uuid: f5e7608d-f906-4a35-b442-899703de3587
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: release-notes
content-type: reference
discoiquuid: 397b3267-1437-4263-963c-9d68ccc928ab
translation-type: tm+mt
source-git-commit: 2411f1aa2853a161603d15917102d5cf1a8139b6

---


# AEM Assets リリースノート {#aem-assets-release-notes}

AEM 6.4 Assetsで行われた主な機能、ハイライト、および機能強化は、このリリースノートで説明します。 詳しくは、記載されているリンクを参照してください。

## Adobe Asset Link {#adobe-asset-link}

Creative Cloud エンタープライズ版の Adobe Asset Link を使用すると、コンテンツ作成プロセスでのクリエイターとマーケティング担当者の共同作業を効率化できます。Creative cloudエンタープライズ版の新しいネイティブ機能で、Adobe Photoshop、Adobe IllustratorまたはAdobe inDesignから直接AEM Assetsに接続できます。 これらのツールを残さずに

To learn more about the capability, prerequisites, and how to access it, see the [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) page.

## Enhanced Smart Tags (powered by Adobe Sensei) {#enhanced-smart-tags-powered-by-adobe-sensei}

AEM 6.4では、AEM 6.3で起動されたスマートタグに加え、人工知能ベースの拡張スマートタグ機能が導入されています。

* スマートコンテンツサービスは、顧客のビジネス分類を学習し、それを使用して、汎用タグに加えて、顧客関連のタグでデジタルアセットに自動的にタグ付けします。 これにより、アセットの検索効率が大幅に向上し、市場投入までの時間が短縮されます。
* Adobe Senseiはスマートコンテンツサービスを強化し、ビジネス分類に関する画像認識アルゴリズムをトレーニングできます。 このコンテンツインテリジェンスを利用して、類似のアセットに関連性の高いタグが付加されます。

AEM Assets拡張スマートタグを使用するには、AEM 6.4の最 [新のサービスパックをインストールします](https://helpx.adobe.com/experience-manager/aem-releases-updates.html)。

## Smart Translation Search (powered by Adobe Sensei) {#smart-translation-search-powered-by-adobe-sensei}

AEM 6.4では、多言語検索シナリオをサポートするスマート翻訳検索機能が導入されています。 お客様のチームが世界中に分散していて複数のロケールが使用されている場合に、コストと時間のかかる翻訳ワークフローを経なくても、様々な言語で検索できるようになりました。

* 検索クエリは手動の介入なしに変換されます。
* スマートタグは英語で生成され、他の言語に機械翻訳されます。
* 多言語検索は、50を超える言語をサポートするオープンソースライブラリApache Joshuaを使用して構築されています。

## ユーザーエクスペリエンス {#user-experience}

AEM 6.4では、ブラウズ、検索、複数ページのアセット、管理ツールの領域でユーザーエクスペリエンスが大幅に向上しました。 詳細は以下のとおりです。

参照の改善

* 新しいコンテンツツリーレールでアセット階層内をすばやく移動できます。これをリスト表示と組み合わせれば、クラシック UI インタラクションモデルに戻してアセット階層内を閲覧することができます。
* アセットの移動に使用するm、プロパティページを開くp、コピー操作に使用するCtrl + cなどの新しいキーボードショートカットが追加されました。
* 多数のアセットの閲覧に対応するように、カードおよびリスト表示でのスクロールが改善され、遅延読み込みがおこなわれるようになりました。
* 表示設定に基づいて様々なサイズのカードをサポートするように、カード表示が改善されました。
* アセットの詳細でのエクスペリエンスが改善され、現在のアセットの表示や「前」または「次」のアセットへの移動が可能になりました。

検索の強化

* 検索の戻るボタンが新たに追加され、検索項目に移動後、検索クエリーをもう一度実行しなくても検索結果の同じ位置に戻ることができるようになりました。
* 検索結果の数が表示されるようになりました。
* 以前の画像、ドキュメント、マルチメディアオプションに比べて、JPG、PNG、PSDなどの詳細なMIMEタイプに基づいて検索結果をフィルターできるように、ファイルタイプ検索フィルターが強化されました。
* 検索フィルターが改善され、以前の時間スライダー機能ではなく、正確なタイムスタンプで処理できるようになりました。

複数ページのアセットの改善

* 複数ページアセットの閲覧操作が改善され、クリック数が少なくなりました。
* コメントと注釈のサポートが改善され、ページレベルではなくアセットレベルですべて照合されるようになりました。

管理ツールの機能強化

* メタデータ、検索、レポートの管理ツールに用意されているプロパティピッカーが改善され、オートコンプリート機能や閲覧機能により管理操作が簡単になりました。

カタログ

* ユーザーエクスペリエンスが改善され、テンプレートユーザーインターフェイスとの連携が改善されました。 For more information, see [Catalog Producer](../sites-administering/catalog-producer.md).

## メタデータ  {#metadata}

AEM 6.4 には、複数の高度なメタデータ管理機能が組み込まれており、大量のメタデータを管理し、ルールと検証を通じてメタデータの整合性を確保できるようになっています。主な機能を以下に示します。

* 新しいメタデータ一括書き出し機能により、多数のアセットのメタデータを CSV 形式で（すべてまたは選択的に）書き出して、編集、共有、サードパーティ統合をおこなうことができます。
* 新しいメタデータ一括読み込み機能により、CSV ファイルを読み込んで、複数のアセットに対する新規メタデータの追加や既存メタデータの更新を一度におこなうことができます。この操作は非同期的で、システムのパフォーマンスに影響を与えません。 操作が完了したら、AEM の通知システムから通知されます。
* メタデータスキーマツールを使用した新しいカスケードメタデータおよびコンテキストメタデータが導入されました。依存関係のチェーンやフィールド間の値マッピングを定義できるようになりました。また、メタデータフォームフィールドが表示／非表示のコンテキストを定義することもできます。こうして、他のフィールドの値に応じて、いつでも、関係のあるフィールドのみ表示することができます。

## レポート {#reports}

AEM 6.4では、アセットレポートに関する次の重要な機能強化が行われています。

* Sling ジョブを適用した拡張性の高い（大規模なリポジトリに対応）エンタープライズレベルの新しいレポートフレームワークで、レポート要求を非同期的に処理できます。特定の日時にレポートをスケジュールすることができます。また、カスタム列をレポートに追加することもできます。
* 新しいOOTBレポートは、ディスク使用量、ファイル、リンク共有、ブランドポータルへの公開、スマートタグトレーニングなど、最も一般的なお客様からの質問です。
* 新しいレポート作成および管理 UI には、オプションがきめ細かく用意されており、アーカイブされたレポートへのアクセスやレポート実行ステータス（成功、失敗、待機中など）の表示が可能です。

## Brand Portal {#brand-portal}

* **6.3 プラットフォームへのアップグレード**： Brand Portal は AEM 6.0 から AEM 6.3 にアップグレードされ、新機能の追加やパフォーマンスの向上がおこなわれました。
* **並列公開**： AEM Assets と Brand Portal の間で発生する可能性のあるレプリケーションの数（以前は 1）まで対応しており、公開のパフォーマンスが大幅に向上しています。
* **スキーマおよび検索ファセットの公開**：メタデータスキーマとカスタム検索ファセットを Brand Portal に公開できるので、作業の重複をなくすことができます。
* **タグの一括公開**：（階層と共に）分類を Brand Portal に公開できるので、作業の重複をなくすことができます。
* **セルフサインアップまたはアクセスのリクエスト**:ブランドポータルへの未登録ユーザーのワークフロー。
* **アプリ内（画面上）のメンテナンス通知**：事前に通知が表示されるので、ビジネスの混乱を避けることができます。
* **レポート機能の向上**：ダウンロード、公開、リンク共有の 3 つの OOTB レポートが使用可能です。
* **DRM ベースの制限事項**：ライセンスされたアセットの有効期限が切れると、Brand Portal からダウンロードできなくなります。

## AEM デスクトップアプリケーション {#aem-desktop-app}

AEM desktop app is updated to version 1.8, which is compatible with AEM 6.4. The full list of changes for AEM desktop app is provided in a dedicated [AEM desktop app release notes](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html) document.\
AEM 6.3のリリース以降のAEMデスクトップアプリのハイライトを以下に示します。

* フォルダー階層をバックグラウンドでアップロードする機能。
* アセットのアップロードをバックグラウンドで監視するための UI。
* キャッシュ機能の向上（キャッシュのパラメーターを管理するための UI など）。
* AEM 認証設定（SAML／SSO）とネットワークプロキシに幅広く対応。
* サポート性：ユーザーインターフェイスからログに簡単にアクセスできます。
* 安定性の向上とお客様から報告された問題の修正。

ドキュメントとベストプラクティスについては、次のドキュメントを参照してください。

* [アプリケーションの操作](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)（エンドユーザー向け）を対象としたユーザーガイド
* [エンドユーザーおよび管理者を対象とした](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app-best-practices.html)、ベストプラクティスガイド
* [AEMとAEMデスクトップ](https://helpx.adobe.com/experience-manager/desktop-app/install-configure-aem-desktop-app.html)・アプリケーションが連携して動作するように設定する管理者向けのインストール・ガイド

## 階層ストレージ {#tiered-storage}

AEM 6.4 には、様々な階層ストレージ環境設定をサポートしライフサイクルルールを実行する一連の機能が含まれています。ストレージオプションでは、AWS や Azure などのパブリッククラウドもサポートしています（それに限定されるわけではありません）。

* ユーザーは、ストレージ・クラスを自由に選択して後から変更し、あるクラスから別のクラスへのアセットの保存に関するルールを定義したり、アセットのライフサイクルを管理したりできます。
* ユーザーが別の AWS や Azure を選択することでストレージコストを削減できます。

サポートされているプラットフォームの概要については、[技術要件に関するドキュメント](../sites-deploying/technical-requirements.md)を参照してください。

## 閉じられたユーザーグループ {#closed-user-group}

* AEM 6.4では、「閉じたユーザーグループ」または「CUG」は、発行インスタンスでのフォルダーアクセスを制限するためのタッチUIオプションで、フォルダーレベルでフォルダープロパティページを介してプリンシパルを追加し、内部のすべてのフォルダーとサブフォルダー/アセットに適用します。
* 発行モードでは、CUGが設定され、フォルダーで認証が有効になっている場合、ユーザーがフォルダーにアクセスしようとすると、ログインページにリダイレクトされます。 したがって、ログインに成功した後でのみ、権限を持つユーザーがフォルダーとその中のアセットにアクセスできます。このように、CUG は、選ばれたプリンシパルを除くすべてのユーザーに対して、コンテンツリポジトリ内の特定のツリーのみ読み取りを制限します。

## Dynamic Media add-on {#dynamic-media-add-on}

AEM 6.4 の Dynamic Media では、マスターアセットのアップロードと管理を AEM Assets Web UI でおこなえる新しいモードをサポートしており、動的レンディションなどのダイナミックメディア機能は、Dynamic Media クラウド配信サービスによりバックグラウンドで処理されます。

In this mode (introduced first with the release of [AEM 6.3 Feature Packs 14410 and 18912](https://helpx.adobe.com/experience-manager/6-3/release-notes/dynamic-media-featurepack-14410.html)), users benefit from end-to-end asset management and dynamic media features using the modern AEM Assets web UI, and still leverage the delivery services that are backwards compatible with Dynamic Media Classic (Scene7)—including delivery URLs, which are unchanged.

この他にも、AEM 6.4 で導入されているものとしては、Adobe Sensei を利用した新しい機能、VR や 3D などの新しいメディアに対応する機能強化、ダイナミックメディアビューア、インタラクティブ画像やカルーセルバナーでのエクスペリエンスフラグメントのサポートなどがあります。

### Smart Crop (powered by Adobe Sensei) {#smart-crop-powered-by-adobe-sensei}

* スマート切り抜きでは、画像の非破壊的な切り抜きを自動的におこない、重要な部分だけを残します。これにより、レスポンシブデザインに対応します。切り抜かれる部分をプレビューし、必要に応じて、切り抜く範囲を手動で調整することができます。
* この機能により、製品画像のスウォッチを自動的に生成することもできます。自動スウォッチ生成は、カラースウォッチやパターンスウォッチまたはその両方を製品画像に自動的に追加するのに役立ちます。

詳しくは、[イメージプロファイル](../assets/image-profiles.md)のドキュメントを参照してください。

また、Dynamic Media コンポーネントでのスマート切り抜きの使用について詳しくは、[ページへのダイナミックメディアアセットの追加](../assets/adding-dynamic-media-assets-to-pages.md)を参照してください。

### スマートイメージング {#smart-imaging}

* スマートイメージングでは、各ユーザーの独自の表示特性を活用して、エクスペリエンスに最適化された画像を自動的に提供し、パフォーマンスとエンゲージメントを向上させます。
* ブラウザーの機能に応じて、画像が様々な形式に自動的に変換されます。
* 画質の設定は、それぞれのブラウザーで決定され適用されます。これにより、限られた帯域幅と低速の接続でも、画像の読み込みパフォーマンスを許容できる範囲に保つことができます。

詳しくは、[スマートイメージング](../assets/imaging-faq.md)のドキュメントを参照してください。

### Emerging Media and Viewer Enhancements {#emerging-media-amp-viewer-enhancements}

* 新しいビューアがサポートされ、臨場感のあるより良いエクスペリエンスをユーザーに提供できます。
* パノラマビューアを使用すると、ユーザーの関心を引き、部屋のシーン、プロパティ、場所、風景をより快適に体験できます。 詳しくは、[パノラマ画像](../assets/panoramic-images.md)のドキュメントを参照してください。

* VRビューアは、プロパティ、場所および風景に対してイマーシブな体験を提供します。
* 製品画像に最適化された垂直画像ビューアが用意されています。
* キーボードのアクセシビリティが向上しました。

### 3D and integration with Dimension CC {#d-and-integration-with-dimension-cc}

Integration with [Adobe Dimension CC](https://www.adobe.com/products/dimension.html) for more seamless 3D workflow has been introduced. 詳しくは、3Dアセットドキュ [メントの操作を参照してください](../assets/assets-3d.md) 。