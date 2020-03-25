---
title: AEM Assetsについて
description: デジタルアセット管理、その使用例、アドビのAEM Assetの機能について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 077cc39c5ed47371a4e3fae1e991209c7bfe6b80

---


# AEM Assetsについて {#about-assets}

アセットは、AEMプラットフォームと完全に統合されたDigital Asset Management(DAM)ツールで、企業はデジタルアセットを共有および配信できます。 組織のユーザーは、Web、印刷およびデジタル配信に使用する画像、ビデオ、ドキュメント、オーディオクリップ、リッチメディア（Flash ファイルなど）を管理、格納したり、これらのデジタルアセットにアクセスしたりできます。

## What is Digital Asset Management (DAM)? {#what-is-digital-asset-management}

AEM Assets は、組織の主要なデジタルアセットを、企業全体で共有および配布する機能を提供します。組織のユーザーは、画像、グラフィック、オーディオ、ビデオおよびドキュメントなどのデジタルアセットを、Web インターフェイス（または CIFS や WebDAV フォルダー）を使用して格納、管理したり、これらのデジタルアセットにアクセスしたりできます。

AEM Assets は AEM に完全に統合されており、次の操作をおこなうことができます。

* 様々なファイル形式の画像、ドキュメント、オーディオファイルおよびビデオファイルを追加および共有する。
* 必要に応じて、タグ、Lightbox または星マークでグループ化することで、アセットを管理する。アセットに注釈を追加する。
* ファイル名、ドキュメントのフルテキスト、日付、ドキュメントタイプおよびタグに基づいてアセットを検索する。
* アセットのメタデータ情報を追加または編集する。メタデータは、関連するアセットと共に、自動的にバージョン管理されます。アセットのメタデータの読み込みまたは書き出しができます。
* 拡大縮小や画像フィルターの追加など、画像編集機能を実行する。WebDAV または CIFS フォルダーを使用して、複数のデジタルアセットを同時に読み込んだり、書き出したりする。
* ワークフローおよび通知を使用して、アセットのセットに関する結合処理とダウンロードを許可し、アセットへのアクセス権を管理する。

### AEM AssetsはAEMのWCM機能と完全に統合されています {#aem-assets-fully-integrated-in-cq-wcm}

AEM Assets は CQ WCM と完全に統合されており、「DAM」アイコンで機能を使用できます。

<!-- TBD: Update image for branding -->

![screen_shot_2012-04-17at15946pm](assets/screen_shot_2012-04-17at15946pm.png)![screen_shot_2012-04-17at20100pm](assets/screen_shot_2012-04-17at20100pm.png)

CQ DAM 内で管理されるアセットに、WCM のコンテンツファインダーを使用してアクセスできます。

<!-- TBD: Update image for branding -->

![screen_shot_2012-04-17at20214pm](assets/screen_shot_2012-04-17at20214pm.png)

>[!NOTE]
>
>The basic navigation of user interface is the same as the rest of AEM - see [Overview of the GUI Console](/help/sites-authoring/qg-page-authoring.md) for full details.

### Digital Asset Management versus the Image component {#digital-asset-management-versus-image-component}

画像をAEM Assetsに配置するか、画像コンポーネントを使用するかを決定する際は、画像のライフサイクルを考慮します。

* 画像がページと同じライフサイクルの場合は、画像コンポーネントを使用します。
* 画像にライフサイクルが個別に設定されている場合、例えば画像を 2 回使用する場合や WCM の外部で使用する場合は、AEM Assets を使用します。

## What are digital assets? {#what-are-digital-assets}

アセットとは、複数のレンディションを持つことができ、サブアセット（例えば、Photoshopファイルのレイヤー、PowerPointファイルのスライド、PDFのページ、ZIP内のファイル）を持つことができるデジタルドキュメント、画像、ビデオまたはオーディオ（またはその一部）です。

アセットは、基本的にバイナリ、メタデータ、レンディション、サブアセットを組み合わせたものです。詳しくは、[DAM パフォーマンスガイド](/help/sites-deploying/assets-performance-sizing.md)を参照してください。

>[!CAUTION]
>
>大容量のアセット（特に画像）のアップロードまたは編集は、CQ インスタンスのパフォーマンスに影響を与えることがあります。

### AEM Assets terminology {#aem-assets-terminology}

AEM でデジタルアセットを使用する際には、次の用語を理解しておく必要があります。

* **コレクション：** 物理的な場所（フォルダ）、共通のプロパティ（保存済みの検索フォルダ）、またはユーザ選択（ライトボックスフォルダ）に基づくアセットのコレクション。

* **メタデータ：** アセットにはメタデータが含まれます。例えば、作成者、有効期限、DRM情報(Digital Rights Management)などです。 メタデータは、アクセスが制御されます。AEM Assets では、追加設定なしに、次の共通の各種メタデータスキーマがサポートされます。

   * **Dublin Core**:作成者、説明、日付、件名などを含みます。
   * **IPTC**:イベント、モデル、場所などを含む。
   * **WCM**:ページプロパティ、オン時間、オフ時間などを含む。

* **タグ付け：** アセットは、タグ付けおよび分類できます。 タグの使用およびタグの管理を参照してください。

* **レンディション：** レンディションとは、アセットのバイナリ表現です。 アセットは、常に（アップロードされたファイルの）一次表現を持ちます。アセットは、例えば、カスタマイズされたワークフロー手順によって作成された、またはアセットがアップロードされた際に作成された、任意の数の追加の表現を持つことができます。レンディションには、様々なサイズや解像度のものがあります。また、透かしが追加されていたり、その他の変更された特徴を持つものもあります。

* **バージョン：** バージョン管理では、特定の時点でのデジタルアセットのスナップショットを作成します。 これにより、以前のバージョンにアセットを復元できます。See [versioning in AEM Assets](managing-assets-touch-ui.md#asset-versioning).

* **サブアセット：** サブアセットは、例えば、Adobe PhotoshopファイルのレイヤーやPDFファイルのページなど、アセットを構成するアセットです。 AEM Assets では、サブアセットをアセットと同じように管理できます。

### アセットの使用方法 {#how-to-work-with-assets}

アセットまたはコレクションに対してアクションを実行します。アクションでは、アセット、コレクションおよびレンディションを作成したり変更したりできます。アセットに対して実行できる多くの基本アクション（アップロード、削除、更新、サブアセットの保存）によって、事前設定されたワークフローが実行されます。これらのアクションは、AEM Assets で自動的にオンになり、AEM Assets メディアハンドラーで詳細が記述されます。

これらの事前設定されたワークフローで実行されるタスクを以下に示します。

* アセットをリポジトリに保存または削除します。
* アセットのメタデータを抽出し、保存します。個々のメタデータ項目はXMPとして保存されます。
* アセットのレンディションとサムネールを生成する必要に応じて、自動サイズ変更と切り抜きを含めます。
* 必要に応じてアセットをトランスコードします。例えば、モバイルおよびWeb用のビデオは24フレーム/秒でトランスコードされ、30フレーム/秒のビデオをダウンロードします。モバイルおよびWebでの使用に適したオーディオは128 kbpsでトランスコードされ、192 kbpsでのダウンロード用にオーディオがトランスコードされます。

また、ワークフローを手動で適用することもできます。デフォルトワークフローのリストについては、[AEM Assets メディアハンドラー](media-handlers.md)を参照してください。

## AEM DAMとAEM MediaLibrary {#cq-dam-vs-cq-medialibrary}

See [AEM DAM and AEM MediaLibrary](medialibrary.md) for information on the differences.
