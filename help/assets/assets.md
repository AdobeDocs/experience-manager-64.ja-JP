---
title: ' [!DNL Adobe Experience Manager Assets] の概要'
description: デジタルアセット管理とは何か、そのユースケース、および  [!DNL Adobe Experience Manager Asset]  の機能について説明します。
contentOwner: AG
feature: Asset Management
role: Leader,Architect,User
exl-id: 9292871d-3b10-49f8-ac1a-4770b4e44048
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 79%

---

# DAM ソリューションとしての [!DNL Adobe Experience Manager Assets] について {#about-assets}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[!DNL Assets] は、[!DNL Experience Manager] プラットフォームの重要な要素となるデジタルアセット管理（DAM）ツールの 1 つです。企業はこのツールを使用することで、デジタルアセットの管理や配布を行うことができます。組織全体を通じてユーザーは、画像、ビデオ、ドキュメント、オーディオクリップ、3D ファイル、リッチメディアなど多様なデジタルアセットを対象に、Web での使用、印刷、デジタル配布を目的として管理、保存、およびアクセスを行うことができます。

## Digital Asset Management とは {#what-is-digital-asset-management}

[!DNL Assets]AEM は、組織の主要なデジタルアセットを、企業全体で共有および配布する機能を提供します。組織のユーザーは、画像、グラフィック、オーディオ、ビデオおよびドキュメントなどのデジタルアセットを、Web インターフェイス（または CIFS や WebDAV フォルダー）を使用して格納、管理したり、これらのデジタルアセットにアクセスしたりできます。

[!DNL Experience Manager] の [!DNL Assets] 機能では、次のことを行うことができます。

* 様々なファイル形式の画像、ドキュメント、オーディオファイルおよびビデオファイルを追加および共有する。
* タグ、Lightbox、または星マーク（お気に入り）で分類して、アセットを管理する。アセットに注釈を追加する。
* ファイル名、ドキュメントの全文、日付、ドキュメントタイプ、タグを検索してアセットを検索します。
* アセットのメタデータ情報を追加または編集する。メタデータは、関連するアセットと共に、自動的にバージョン管理されます。アセットのメタデータの読み込みまたは書き出しができます。
* 画像編集機能（拡大・縮小、画像フィルタの追加など）を実行する。 WebDAV または CIFS フォルダーを使用した複数のデジタルアセットの読み込みと書き出しを同時におこないます。
* ワークフローおよび通知を使用して、アセットのセットに関する結合処理とダウンロードを許可し、アセットへのアクセス権を管理する。

### [!DNL Experience Manager Assets] と [!DNL Experience Manager Sites] の統合 {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] は [!DNL Sites] と完全統合され、あらゆるユースケースでシームレスに動作します。例えば、web ページを作成する場合、[!DNL Sites] の作成者は、コンテンツファインダーを通じてデジタルアセットを検索したり、使用したりできます。[!DNL Assets] と [!DNL Sites] のユーザーインターフェイスは同じです。詳細については、[サイトの概要](/help/sites-authoring/qg-page-authoring.md)を参照してください。

<!-- TBD: Update image for branding 

![screen_shot_2012-04-17at15946pm](assets/screen_shot_2012-04-17at15946pm.png) ![screen_shot_2012-04-17at20100pm](assets/screen_shot_2012-04-17at20100pm.png)

Assets managed within [!DNL Experience Manager] DAM can then be accessed via the content finder of WCM:

![screen_shot_2012-04-17at20214pm](assets/screen_shot_2012-04-17at20214pm.png) -->

### デジタルアセット管理と画像コンポーネントの比較 {#digital-asset-management-versus-image-component}

画像を DAM リポジトリに格納するか、画像コンポーネントを使用するかを決める場合は、画像のライフサイクルを考慮します。

* 画像のライフサイクルがページと同じ場合は、画像コンポーネントを使用します。
* 画像にライフサイクルが個別に設定されている場合（例えば同じ画像を 2 回使用する場合や WCM の外部で使用する場合）は、[!DNL Assets] を使用します。

## デジタルアセットとは何か {#what-are-digital-assets}

アセットとは、デジタルドキュメント、画像、ビデオまたはオーディオ（あるいはその一部）のことで、この中には複数のレンディションや、サブアセット（例えば、Photoshop ファイルのレイヤー、PowerPoint ファイルのスライド、PDF のページ、ZIP 中のファイルなど）を含めることができます。

アセットは、基本的に、バイナリ、メタデータ、レンディション、サブアセットの 3 種類です。 詳しくは、 [DAM パフォーマンスガイド](https://experienceleague.adobe.com/docs/?lang=jaexperience-manager-64/assets/administer/performance-tuning-guidelines.html) を参照してください。

>[!CAUTION]
>
>大容量のアセット（特に画像）をアップロードしたり、編集したりすると、[!DNL Experience Manager] デプロイメントのパフォーマンスに影響を与えることがあります。

### [!DNL Experience Manager Assets] 用語 {#aem-assets-terminology}

[!DNL Experience Manager] でデジタルアセットを使用する場合、以下の用語を理解している必要があります。

* **コレクション**：物理的な場所（フォルダー）、共通のプロパティ（保存された検索フォルダー）、またはユーザーの選択（Lightbox のフォルダー）のいずれかに基づいて収集したアセットの集合です。

* **メタデータ**：[!DNL Assets] にはメタデータがあります。例：作成者、有効期限、DRM（デジタル著作権管理）情報など。メタデータは、アクセスが制御されます。[!DNL Assets] では、追加設定なしに、次の共通の各種メタデータスキーマがサポートされます。

   * Dublin Core:作成者、説明、日付、件名などを含めます。
   * IPTC:イベント、モデル、場所などが含まれます。
   * WCM：ページプロパティ、[!UICONTROL オンタイム]、[!UICONTROL オフタイム]などが含まれます。

* **タグ付け**：[!DNL Assets]タグ付けや分類を行うことができます。[アセットの整理](/help/assets/organize-assets.md)を参照してください。

* **レンディション**：特定のアセットをバイナリで表現したものです。[!DNL Assets] には必ず、アップロードされたファイルの一次表現が含まれます。カスタマイズされたワークフローステップやアセットのアップロード時などに、作成された追加の表現を任意の数個持つことができます。 レンディションのサイズや解像度、透かしの追加、その他の変更された特性が異なる場合があります。

* **バージョン**：バージョン管理では、特定の時点でのデジタルアセットのスナップショットが作成されます。これにより、以前のバージョンにアセットを復元できます。[ [!DNL Assets]](managing-assets-touch-ui.md#asset-versioning) のバージョン管理を参照してください。

* **サブアセット**：サブアセットは、例えば、[!DNL Adobe Photoshop] ファイルのレイヤーや PDF ファイルのページなど、アセットを構成するアセットです。[!DNL Assets] では、サブアセットをアセットと同じように管理できます。

### デジタルアセットの使用方法 {#how-to-work-with-assets}

アセットまたはコレクションに対してアクションを実行します。 アクションは、アセット、コレクションおよびレンディションを作成または変更できます。 アセットに対して実行できる多くの基本アクション（アップロード、削除、更新、サブアセットの保存）によって、事前設定されたワークフローが実行されます。これらのアクションは、[!DNL Assets] で自動的にオンになり、[!DNL Assets] メディアハンドラーで詳細が記述されます。

これらの事前設定されたワークフローで実行されるタスクを以下に示します。

* リポジトリへのアセットの保存またはリポジトリからのアセットの削除。
* アセットのメタデータの抽出および保存。個々のメタデータ項目は XMP として保存されます。
* アセットのレンダリングとサムネールの生成。必要に応じた自動リサイズおよびトリミングも含まれます。
* 必要に応じたアセットのトランスコード。例えば、モバイルや web で使用するビデオは 24 fps、ダウンロード用ビデオは 30 fps にトランスコードされます。モバイルや web で使用するオーディオは 128 Kbps、ダウンロード用オーディオは 192 Kbps にトランスコードされます。

また、ワークフローを手動で適用することもできます。デフォルトワークフローのリストについては、[ Assets メディアハンドラー](media-handlers.md)を参照してください。

## [!DNL Experience Manager Assets] および [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

違いについて詳しくは、[Assets とMedia Library](medialibrary.md) を参照してください。

>[!MORELIKETHIS]
>
>* [ビデオの紹介 - Experience Manager Assets as a modern DAM](https://www.youtube.com/watch?v=PBwQqZgC-yo)

