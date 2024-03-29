---
title: AEM Brackets 拡張
seo-title: AEM Brackets Extension
description: AEM Brackets 拡張
seo-description: null
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
exl-id: 5924d38b-243e-4a81-85b6-9ff89ae4c811
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 61%

---

# AEM Brackets 拡張{#aem-brackets-extension}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

AEM Brackets Extension は、AEMのコンポーネントとクライアントライブラリを編集するためのスムーズなワークフローを提供し、 [Brackets](https://brackets.io/) コードエディター。コードエディター内からPhotoshopのファイルおよびレイヤーにアクセスできます。 拡張機能によって提供される簡単な同期（Maven や File Vault は不要）により、開発者の効率が向上し、AEMに関する知識が限られたフロントエンド開発者もプロジェクトに参加できます。 この拡張機能は、[HTML Template Language（HTL）](https://helpx.adobe.com/jp/experience-manager/htl/user-guide.html)のサポートも提供しており、複雑な JSP を使用しない、より手軽でセキュアなコンポーネント開発を可能にします。

![chlimage_1-53](assets/chlimage_1-53.png)

### 機能 {#features}

AEM Brackets Extension の主な機能は次のとおりです。

* 変更されたファイルの AEM 開発インスタンスへの自動同期。
* ファイルおよびフォルダーの手動双方向同期。
* プロジェクトのコンテンツパッケージ全体の同期。
* 式および `data-sly-*` ブロックステートメントの HTL コードコンプリート。

さらに、Brackets には、AEMフォントエンド開発者向けの便利な機能が多数用意されています。

* Photoshopファイルでは、レイヤー、測定値、色、フォント、テキストなど、PSDファイルから情報を抽出する機能がサポートされています。
* 抽出した情報をコード内で簡単に再利用するために、PSDからのコードヒント。
* LESS および SCSS などの CSS プリプロセッサーサポート。
* さらに具体的なニーズをカバーする数百の追加の拡張機能。

## インストール {#installation}

### Brackets {#brackets}

AEM Brackets Extension は、Brackets バージョン 1.0 以降をサポートしています。

最新バージョンの Brackets を [brackets.io](https://brackets.io/) からダウンロードしてください。

### 拡張機能 {#the-extension}

拡張機能をインストールするには、次の手順を実行します。

1. Brackets を開きます。 メニュー内 **ファイル**&#x200B;を選択します。 **Extension Manager...**
1. 入力 **AEM** 検索バーで **AEM Brackets Extension**.

   ![chlimage_1-54](assets/chlimage_1-54.png)

1. 「**インストール**」をクリックします。
1. インストールが完了したら、ダイアログとExtension Managerを閉じます。

## はじめに {#getting-started}

### Content-Package プロジェクト {#the-content-package-project}

拡張機能がインストールされたら、Brackets を使用してファイルシステムから content-package フォルダーを開き、AEMコンポーネントの開発を開始できます。

プロジェクトには、少なくとも次の要素を含める必要があります。

1. `jcr_root` フォルダー（例：`myproject/jcr_root`）

1. `filter.xml` ファイル（例：`myproject/META-INF/vault/filter.xml`）。`filter.xml` ファイルの構造について詳しくは、[ワークスペースフィルターの定義](https://jackrabbit.apache.org/filevault/filter.html)を参照してください。

Brackets の **File** メニューで「**Open Folder**」を選択し、`jcr_root` フォルダーまたは親プロジェクトフォルダーを選択します。

>[!NOTE]
>
>コンテンツパッケージを含むプロジェクトを所有していない場合は、[HTL TodoMVC Example](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc) を使用できます。GitHub で、「**Download ZIP**」をクリックし、ファイルをローカルに抽出し、上記の説明に従って Brackets で `jcr_root` フォルダーを開きます。次に、以下の手順に従って&#x200B;**プロジェクト設定**&#x200B;を行い、最後に「コンテンツパッケージ全体の同期」セクションの下部の説明に従って「**Export Content Package**」を実行して、パッケージ全体を AEM 開発インスタンスにアップロードします。
>
>これらの手順が完了したら、AEM 開発インスタンス上の URL `/content/todo.html` にアクセスし、Brackets でコード変更を開始できるようになり、web ブラウザーを更新することで変更内容がただちに AEM サーバーに同期されることを確認できます。

### プロジェクト設定 {#project-settings}

コンテンツをAEM開発インスタンスと同期するには、プロジェクト設定を定義する必要があります。 プロジェクト設定の定義は、**AEM** メニューに移動し、「**プロジェクト設定**」を選択しておこないます。

![chlimage_1-55](assets/chlimage_1-55.png)

プロジェクト設定を使用して、次を定義できます。

1. サーバー URL（例：`http://localhost:4502`）
1. 有効な HTTPS 証明書がないサーバーを許容するかどうか（必要ない場合はオフのままにしてください）
1. コンテンツの同期に使用するユーザー名（例：`admin`）
1. ユーザーのパスワード（例：`admin`）

## コンテンツの同期 {#synchronizing-content}

AEM Brackets Extension は、`filter.xml` で定義されているフィルタリングルールによって許可されているファイルおよびフォルダーに対して、次のタイプのコンテンツ同期を提供します。

### 変更されたファイルの自動同期 {#automated-synchronization-of-changed-files}

これにより、変更が Brackets からAEMインスタンスにのみ同期されますが、逆の方法は決して同期されません。

### 手動双方向同期 {#manual-bidirectional-synchronization}

Project Explorer で、任意のファイルまたはフォルダーを右クリックしてコンテキストメニューを開き、「**サーバーにエクスポート**」または「**サーバーからインポート**」オプションにアクセスできます。

![chlimage_1-56](assets/chlimage_1-56.png)

>[!NOTE]
>
>選択したエントリが `jcr_root` フォルダー外にある場合、コンテキストメニュー項目「**サーバーにエクスポート**」および「**サーバーからインポート**」は無効になります。

### コンテンツパッケージ全体の同期 {#full-content-package-synchronization}

**AEM** メニューで、「**コンテンツパッケージのエクスポート**」または「**コンテンツパッケージのインポート**」オプションを使用して、プロジェクト全体をサーバーと同期できます。

![chlimage_1-57](assets/chlimage_1-57.png)

### 同期ステータス {#synchronization-status}

AEM Brackets Extension には、Brackets ウィンドウの右側にあるツールバーに、最後の同期のステータスを示す通知アイコンが表示されます。

* 緑 — すべてのファイルが正常に同期されました
* 青 — 同期操作が進行中です
* 黄 — 一部のファイルが同期されませんでした
* 赤 — どのファイルも同期されませんでした

通知アイコンをクリックすると、同期済みの各ファイルのすべてのステータスの一覧を示す同期ステータスレポートダイアログが開きます。

![chlimage_1-58](assets/chlimage_1-58.png)

>[!NOTE]
>
>使用する同期方法にかかわらず、`filter.xml` のフィルタリングルールによって「含める」とマークされているコンテンツのみが同期されます。
>
>さらに、リポジトリーへの同期およびリポジトリーからの同期からコンテンツを除外するために、`.vltignore` ファイルがサポートされています。

## HTL コードの編集 {#editing-htl-code}

AEM Brackets Extension によって、HTL 属性および式の作成を容易にするオートコンプリートも導入されます。

### 属性のオートコンプリート {#attribute-auto-completion}

1. HTML 属性に「`sly`」と入力します。この属性は、「`data-sly-`」にオートコンプリートされます。
1. ドロップダウンリストで HTL 属性を選択します。

### 式のオートコンプリート {#expression-auto-completion}

式 `${}` 内で、一般的な変数名がオートコンプリートされます。

## 詳細情報 {#more-information}

AEM Brackets Extension はオープンソースのプロジェクトで、Apache License バージョン 2.0 に従って、[Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) チームにより GitHub にホストされています。

* コードリポジトリー：[https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache License バージョン 2.0：[https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

Brackets コードエディターもオープンソースのプロジェクトで、[Adobe Systems Inc](https://github.com/adobe)により GitHub にホストされています。

* コードリポジトリー：[https://github.com/adobe/brackets](https://github.com/adobe/brackets)

ご自由に投稿してください。
