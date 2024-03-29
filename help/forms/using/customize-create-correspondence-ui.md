---
title: 通信作成用 UI のカスタマイズ
seo-title: Customize create correspondence UI
description: 通信の作成 UI をカスタマイズする方法を説明します。
seo-description: Learn how to customize create correspondence UI.
uuid: 5b6eb8fd-0270-4638-bdf4-cb7015919d57
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
discoiquuid: 3efd8f5a-9f38-4d9b-88d6-d8fde6c9a644
feature: Correspondence Management
exl-id: 63cd01d2-a0d5-4f85-b9d2-ec3007ce3fa9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1131'
ht-degree: 53%

---

# 通信作成 UI のカスタマイズ {#customize-create-correspondence-ui}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

Correspondence Management を使用すると、ソリューションテンプレートを再ブランディングして、より優れたブランド価値を実現し、組織のブランディング標準に準拠できます。 ユーザーインターフェイスのリブランディングには、組織のロゴの変更が含まれます。ロゴは、通信を作成 UI の左上隅に表示されます。

通信を作成 UI のロゴを組織のロゴと共に変更できます。

![通信作成 UI のカスタムアイコン](assets/0_1_introscreenshot.png)
**図：** *通信を作成 UI のカスタムアイコン*

### 通信を作成 UI でのロゴの変更 {#changing-the-logo-in-the-create-correspondence-ui}

選択したロゴイメージを設定するには、次の手順を実行します。

1. [CRX 内で適切なフォルダー構造](#creatingfolderstructure)を作成します。
1. CRX で作成したフォルダーに、[新しいロゴファイルをアップロード](#uploadlogo)します。

1. CRX 上に [CSS をセットアップ](#createcss)し、新しいロゴを参照します。
1. ブラウザーの履歴を消去し、[通信作成 UI を更新](#refreshccrui)します。

## 必要なフォルダー構造の作成 {#creatingfolderstructure}

カスタムロゴ画像とスタイルシートをホストするためのフォルダー構造を、以下で説明するように作成します。 ルートフォルダー/apps を持つ新しいフォルダー構造は、/libs フォルダーの構造に似ています。

カスタマイズの場合は、以下に説明するように、/apps ブランチに並列フォルダー構造を作成します。

/apps 分岐（フォルダー構造）により：

* システムの更新時にそれらのファイルを安全に保ちます。アップグレード、機能パック、ホットフィックスを適用すると、/libs 分岐が更新されます。/libs 分岐に変更内容をホストしていると上書きされてしまいます。
* 現在のシステムやブランチを乱さないようにします。カスタムファイルの保存にデフォルトの場所を使用すると、誤って解決できる場合があります。
* AEMでリソースを検索する際に、リソースの優先度を高めるのに役立ちます。 AEM では、リソースを検索する場合、最初に /apps 分岐を検索し、次に /libs 分岐を検索するように設定されています。このメカニズムにより、システムはオーバーレイ（および、そこに定義されたカスタマイズ内容）を使用します。

次の手順を実行して、必要なフォルダー構造を /apps 分岐に作成します。

1. `https://[server]:[port]/[ContextPath]/crx/de` にアクセスし、管理者としてログインします。
1. apps フォルダー内に、ccrui フォルダーにある css フォルダーと同様のパスと構造を持つ、`css` というフォルダーを作成します。

   css フォルダーの作成手順：

   1. 次のパスにある **css** フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。`/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      ![ノードをオーバーレイ](assets/1_overlaynode_css.png)

   1. 「ノードをオーバーレイ」ダイアログに次の値が表示されていることを確認します。

      **パス：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css

      **オーバーレイの場所：**/apps/

      **ノードタイプを一致させる：**&#x200B;オン

      ![オーバーレイノードのパス](assets/0_1_5ioverlaynodedialog.png)

      >[!NOTE]
      >
      >/libs 分岐は変更しないでください。このブランチは、次の操作を行うたびに変更される可能性が高いので、加えた変更はすべて失われる可能性があります。
      >
      >* インスタンスでのアップグレード
      >* ホットフィックスの適用
      >* 機能パックのインストール


   1. 「**OK**」をクリックします。指定されたパスに css フォルダーが作成されます。

1. apps フォルダー内に、ccrui フォルダーにある imgs フォルダーと同様のパスと構造を持つ、`imgs` というフォルダーを作成します。

   1. 次のパスにある **imgs** フォルダーを右クリックし、「**ノードをオーバーレイ**」を選択します。`/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs`
   1. 「ノードをオーバーレイ」ダイアログに次の値が表示されていることを確認します。

      **パス：**/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs

      **オーバーレイの場所：**/apps/

      **ノードタイプを一致させる**：オン

   1. 「**OK**」をクリックします。

      >[!NOTE]
      >
      >/apps フォルダーに手動でフォルダー構造を作成することもできます。

1. 「**すべて保存**」をクリックして、サーバーに変更を保存します。

## CRX に新しいロゴをアップロード {#uploadlogo}

カスタムロゴファイルを CRX にアップロードします。 ロゴの描画には、標準的な HTML 規則が適用されます。サポートしている画像ファイル形式は、AEM Forms へのアクセスに使用しているブラウザーによって異なります。すべてのブラウザーは、JPEG、GIF、PNG をサポートしています。 詳しくは、サポートされる画像形式に関するブラウザー固有のドキュメントを参照してください。

* ロゴ画像のデフォルトのサイズは 48 px &amp;ast；です48 px。 画像がこのサイズに近いか、48 px &amp;ast；より大きいことを確認します。48 px。
* ロゴ画像の高さが 50 px を超える場合、「通信を作成」のユーザーインターフェイスでは、ヘッダーの高さになるので、画像を最大高さ 50 px まで縮小表示します。 画像を縮小しながら、通信を作成ユーザーインターフェイスで画像の縦横比が維持されます。
* 画像が小さい場合、通信作成用ユーザーインターフェイスでは拡大表示されません。そのため、ロゴ画像をきれいに表示するには、高さが少なくとも 48 ピクセルあり、幅も十分にあるファイルを使用することが大切です。

以下の手順を実行して、CRX にカスタムロゴファイルをアップロードします。

1. `https://[server]:[port]/[contextpath]/crx/de` にアクセスします。必要に応じて、管理者としてログインします。
1. CRXDE から、次のパスにある **imgs** フォルダーを右クリックし、「**作成」／「ファイルを作成**」を選択します。

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs/`

   ![imgs フォルダ内に新しいノードを作成する](assets/2_contentexplorernewnode.png)

1. 「ファイルを作成」ダイアログで、ファイルの名前「CustomLogo.png」（またはロゴファイルの名前）を入力します。

   ![新規ノードとしての CustomLogo.png](assets/3_contentexplorernewnode_customlogo.png)

1. 「**すべて保存**」をクリックします。

   作成した新しいファイル（ここでは「CustomLogo.png」）の下に、jcr:content プロパティが表示されます。

1. フォルダー構造で jcr:content をクリックします。

   jcr:content のプロパティが表示されます。

   ![jcrcontentproperties](assets/jcrcontentproperties.png)

1. **jcr:data** プロパティをダブルクリックします。

   「Edit jcr:data」のダイアログが表示されます。

   次に、newlogo.png フォルダーをクリックし、jcr:content（dim オプション）をダブルクリックし、タイプを nt:resource に設定します。プロパティが表示されていない場合は、まず、名前が「jcr:content」のプロパティを作成します。

1. 「jcr:data の編集」ダイアログで「**参照**」をクリックし、ロゴとして使用する画像ファイルを選択します（ここでは、「CustomLogo.png」）。

   サポートしている画像ファイル形式は、AEM Forms へのアクセスに使用しているブラウザーによって異なります。すべてのブラウザーは、JPEG、GIF、PNG をサポートしています。 詳しくは、サポートされる画像形式に関するブラウザー固有のドキュメントを参照してください。

   ![カスタムロゴファイルのサンプル](assets/geometrixx-outdoors.png)
   **図：** *例 — カスタムロゴとして使用する CustomLogo.png*

1. 「**すべて保存**」をクリックします。

## CSS を作成してロゴを UI に統合する {#createcss}

カスタムロゴイメージを使用するには、コンテンツコンテキストに追加のスタイルシートを読み込む必要があります。

ロゴの描画用スタイルシートを設定する手順は、以下のとおりです。

1. `https://[server]:[port]/[contextpath]/crx/de` にアクセスします。必要に応じて、管理者としてログインします。
1. 次の場所に、customcss.css というファイルを作成します。異なるファイル名は使用できません。

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css/`

   customcss.css ファイルの作成手順：

   1. を右クリックします。 **css** フォルダーと選択 **作成/ファイルを作成**.
   1. 新規ファイルダイアログボックスで、CSS の名前を「`customcss.css`」として指定し、「**OK**」をクリックします。異なるファイル名は使用できません。
   1. 次のコードを、新しく作成した css ファイルに追加します。 コードの content:url で、CRXDE の imgs フォルダーにアップロードした画像名を指定します。

      ```css
      .logo, .logo:after {
      content:url("../imgs/CustomLogo.png");
      }
      ```

   1. 「**すべて保存**」をクリックします。

## 通信を作成 UI を更新してカスタムロゴを表示 {#refreshccrui}

ブラウザーのキャッシュをクリアし、ブラウザーで通信を作成 UI インスタンスを開きます。 カスタムロゴが表示されます。

![カスタムロゴを用いて、通信作成用ユーザーインターフェイスを構築する](assets/0_1_introscreenshot-1.png)
**図：** *通信を作成 UI のカスタムアイコン*
