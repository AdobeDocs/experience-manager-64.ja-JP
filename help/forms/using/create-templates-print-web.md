---
title: '"チュートリアル：テンプレートの作成"'
seo-title: Create Print and Web templates for Interactive Communication
description: インタラクティブ通信用の印刷テンプレートと Web テンプレートの作成
seo-description: Create Print and Web templates for Interactive Communication
uuid: d7b0d9a5-f5f0-4c21-a6f8-622bf94f4491
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 40c0a17b-6894-44cc-b1f7-490913061532
feature: Interactive Communication
exl-id: 5822145f-d317-4807-a3f0-1d2aea0a779b
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1816'
ht-degree: 65%

---

# チュートリアル：テンプレートの作成 {#tutorial-create-templates}

インタラクティブ通信用の印刷テンプレートと Web テンプレートの作成

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

このチュートリアルは、 [最初のインタラクティブ通信を作成する](/help/forms/using/create-your-first-interactive-communication.md) 系列。 チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

インタラクティブ通信を作成するには、AEM サーバーに用意されている印刷チャネルと Web チャネル用のテンプレートを入手する必要があります。

印刷チャネルのテンプレートは Adobe Forms Designer で作成されて、AEM サーバーにアップロードされます。これらのテンプレートはインタラクティブ通信を作成する際に使用できるようになります。

Web チャネル用のテンプレートは AEM で作成されます。テンプレートの作成者と管理者は、Web テンプレートの作成、編集、有効化を行うことができます。作成して有効化されたテンプレートは、インタラクティブ通信を作成する際に使用できるようになります。

本チュートリアルは、印刷チャネル用および Web チャネル用のテンプレートの作成方法を順を追って説明します。これにより、作成されたテンプレートは、インタラクティブ通信を作成する際に使用できるようになります。このチュートリアルを完了すると、次の操作を実行できるようになります。

* Adobe Forms Designer を使用して印刷チャネル用の XDP テンプレートを作成する
* XDP テンプレートを AEM Forms サーバーにアップロードする
* Web チャネル用のテンプレートを作成し有効化する

## 印刷チャネル用のテンプレートの作成 {#create-template-for-print-channel}

次のタスクを使用して、インタラクティブ通信の印刷チャネル用のテンプレートの作成と管理を行います。

* [Forms Designer を使用して XDP テンプレートを作成する](/help/forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [AEM Forms サーバーに XDP テンプレートをアップロードする](/help/forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [レイアウトフラグメント用に XDP テンプレートを作成する](/help/forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Forms Designer を使用して XDP テンプレートを作成する {#create-xdp-template-using-forms-designer}

次に基づいて [使用例](/help/forms/using/create-your-first-interactive-communication.md) および [解剖学](/help/forms/using/planning-interactive-communications.md)XDP テンプレートで次のサブフォームを作成します。

* 請求明細：ドキュメントフラグメントが含まれます
* 顧客の詳細：ドキュメントフラグメントを含める
* 請求の要約：ドキュメントフラグメントを含める
* 概要：ドキュメントフラグメント（Charges サブフォーム）とグラフ（Charts サブフォーム）を含めます
* 通話明細：テーブルを含める（レイアウトフラグメント）
* 今すぐ支払う：画像を含む
* 付加価値サービス：画像を含む

![create_print_template](assets/create_print_template.gif)

XDP ファイルを Forms サーバーにアップロード後、これらのサブフォームは印刷テンプレートのターゲット領域として表示されます。インタラクティブ通信を作成する際に、ドキュメントフラグメント、グラフ、レイアウトフラグメント、画像などのすべてのエンティティがターゲット領域に追加されます。

印刷チャネル用に XDP テンプレートを作成するには、次の手順を実行します。

1. Forms Designer を開き、「 **ファイル** > **新規** > **空白のフォームを使用し、** タップ **次へ**&#x200B;次に、 **完了** をクリックして、テンプレート作成用のフォームを開きます。

   「**オブジェクトライブラリ**」および「**オブジェクト**」オプションが **Window** メニューから選択されていることを確認します。

1. **サブフォーム**&#x200B;コンポーネントを&#x200B;**オブジェクトライブラリ**&#x200B;からフォームにドラッグアンドドロップします。
1. 右側のペインの「**オブジェクト**」ウィンドウのサブフォームを表示するには、「サブフォーム」を選択します。
1. を選択します。 **サブフォーム** 「 」タブで「 」を選択します。 **フロー** から **コンテンツ** 」ドロップダウンリストから選択できます。 長さを調整するには、サブフォームの左のエンドポイントをドラッグします。
1. 「**連結**」タブで、次の手順を実行します。

   1. 指定 **BillDetails** 内 **名前** フィールドに入力します。
   1. 「**データ連結**」ドロップダウンリストから「**データ連結なし**」を選択します。

   ![forms_designer_subform](assets/forms_designer_subform.png)

1. 同様に、ルートサブフォームを選択し、 **サブフォーム** 「 」タブで「 」を選択します。 **フロー** から **コンテンツ** 」ドロップダウンリストから選択できます。 「**連結**」タブで、次の手順を実行します。

   1. 指定 **TelecaBill** 内 **名前** フィールドに入力します。
   1. 「**データ連結**」ドロップダウンリストから「**データ連結なし**」を選択します。

   ![root_subform_print_template](assets/root_subform_print_template.png)

1. 手順 2～5 を繰り返し、次のサブフォームを作成します。

   * BillDetails
   * CustomerDetails
   * BillSummary
   * 概要 — **サブフォーム** 「 」タブで「 」を選択します。 **配置済み** から **コンテンツ** このサブフォームのドロップダウンリスト。 次のサブフォームを&#x200B;**概要**&#x200B;サブフォームに挿入します。

      * 料金
      * グラフ
   * ItemisedCalls
   * PayNow
   * ValueAddedServices

   時間を節約するには、既存のサブフォームをコピー＆ペーストして新しいサブフォームを作成することもできます。

   次の手順で、 **グラフ** Charges サブフォームの右側にあるサブフォームで、 **グラフ** サブフォームを左側のウィンドウから、 **レイアウト** タブで、 **AnchorX** フィールドに入力します。 指定する値は、**料金**&#x200B;サブフォームの「**幅**」フィールドの値よりも大きい値である必要があります。を選択します。 **料金** サブフォームを開き、 **レイアウト** タブで **幅** フィールドに入力します。

1. **テキスト**&#x200B;オブジェクトを、**オブジェクトライブラリ**&#x200B;からフォームにドラッグアンドドロップし、ボックスに **Dial XXXX to subscribe** とテキストを入力します。
1. 左ペインでテキストオブジェクトを右クリックし、「 」を選択します。 **オブジェクト名を変更**&#x200B;テキストオブジェクトの名前を **購読**.

   ![print_xdp_template_subform](assets/print_xdp_template_subform.png)

1. ローカルのファイルシステムにファイルを保存するには、「**ファイル**／**名前を付けて保存**」を選択して、次の手順を実行します。

   1. ファイルを保存する場所に移動し、**create_first_ic_print_template** と名前を指定します。
   1. 「**ファイルの種類**」ドロップダウンリストから&#x200B;**.xdp** を選択します。
   1. 「**保存**」をタップします。

### AEM Forms サーバーに XDP テンプレートをアップロードする {#upload-xdp-template-to-the-aem-forms-server}

Forms Designer を使用して XDP テンプレートの作成が終わったら、AEM Forms サーバーにアップロードする必要があります。これにより、作成されたテンプレートは、インタラクティブ通信を作成する際に使用できるようになります。

1. **[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. **作成**／**ファイルのアップロード**&#x200B;をタップします。

   に移動して選択します。 **create_first_ic_print_template** template (XDP) をタップし、 **開く** をクリックして、XDP テンプレートをAEM Formsサーバーに読み込みます。

### レイアウトフラグメント用に XDP テンプレートを作成する {#create-xdp-template-for-layout-fragments}

インタラクティブ通信の印刷チャネル用のレイアウトフラグメントを作成するには、Forms Designer を使用して XDP を作成し、AEM Forms サーバーにアップロードします。

1. Forms Designer を開き、「 **ファイル** > **新規** > **空白のフォームを使用し、** タップ **次へ**&#x200B;次に、 **完了** をクリックして、テンプレート作成用のフォームを開きます。

   「**オブジェクトライブラリ**」および「**オブジェクト**」オプションが **Window** メニューから選択されていることを確認します。

1. 次をドラッグ&amp;ドロップ： **テーブル** コンポーネント **オブジェクトライブラリ** をフォームに追加します。
1. テーブルの挿入ダイアログで、次の手順を実行します。

   1. 列数を **5** と指定します。
   1. ボディ行数を **1** と指定します。
   1. 「**テーブルにヘッダー行を含む**」チェックボックスを選択します。
   1. 「**OK**」をタップします。

1. **テーブル** 1 の隣の左側のペインで「**+**」をタップし、**Cell1** を右クリックし、「**オブジェクト名の変更**」を「**日付**」に選択します。

   同様に、**Cell2**、**Cell3**、**Cell4**&#x200B;および&#x200B;**Cell5** の名前をそれぞれ&#x200B;**時刻**、**番号**、**時間**&#x200B;および&#x200B;**料金**&#x200B;に変更します。

1. 「 **デザイナービュー** を選択し、名前をに変更します。 **時間**, **数値**, **期間**、および **料金**.

   ![layout_fragment_print](assets/layout_fragment_print.png)

1. 左側のペインから&#x200B;**Row 1** を選択し、「**オブジェクト**／**連結**／**各データアイテムについて行を繰り返す**」を選択します。

   ![layout_fragment_print_repeat](assets/layout_fragment_print_repeat.png)

1. 次をドラッグ&amp;ドロップ： **テキストフィールド** コンポーネント **オブジェクトライブラリ** から **デザイナービュー**.

   ![layout_fragment_print_text_field](assets/layout_fragment_print_text_field.png)

   同様に、**テキストフィールド**&#x200B;コンポーネントを&#x200B;**時刻**、**番号**、**時間**&#x200B;および&#x200B;**料金**&#x200B;行にドラッグアンドドロップします。

1. ローカルのファイルシステムにファイルを保存するには、「**ファイル**／**名前を付けて保存**」を選択して、次の手順を実行します。

   1. ファイルを保存する場所に移動し、名前を指定します。 **table_lf**.
   1. 「**ファイルの種類**」ドロップダウンリストから&#x200B;**.xdp** を選択します。
   1. 「**保存**」をタップします。

   Forms Designer を使用してレイアウトフラグメント用 XDP テンプレートの作成が終わったら、AEM Forms サーバーに[アップロード](/help/forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)する必要があります。これにより、作成されたテンプレートは、レイアウトフラグメントを作成する際に使用できるようになります。

## Web チャネル用テンプレートの作成 {#create-template-for-web-channel}

次のタスクを使用して、インタラクティブ通信の Web チャネル用のテンプレートの作成と管理を行います。

* [テンプレート用フォルダーの作成](/help/forms/using/create-templates-print-web.md#create-folder-for-templates)
* [テンプレートの作成](/help/forms/using/create-templates-print-web.md#create-the-template)
* [テンプレートの有効化](/help/forms/using/create-templates-print-web.md#enable-the-template)
* [インタラクティブ通信でボタンの有効化](/help/forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### テンプレート用フォルダーの作成 {#create-folder-for-templates}

Web チャネルテンプレートを作成するには、作成したテンプレートを保存できるフォルダーを定義します。フォルダー内にテンプレートを作成したら、そのテンプレートを有効にする必要があります。これにより、フォームユーザーがそのテンプレートを使用して、インタラクティブ通信の Web チャネルを作成できるようになります。

編集可能なテンプレート用のフォルダーを作成するには、次の手順を実行します。

1. タップ **ツール** ![ツール](assets/tools-icon.svg) > **設定ブラウザー**.
   * 詳しくは、[](/help/sites-administering/configurations.md)設定ブラウザーのドキュメントを参照してください。
1. 設定ブラウザーページで、をタップします。 **作成**.
1. 内 **設定を作成** ダイアログ、指定 **Create_First_IC_templates** フォルダーのタイトルとして、 **編集可能なテンプレート**&#x200B;をタップし、 **作成**.

   ![create_first_ic_web_template](assets/create_first_ic_web_template.png)

   この **Create_First_IC_templates** フォルダーが作成され、 **設定ブラウザー** ページ。

### テンプレートの作成 {#create-the-template}

次に基づいて [使用例](/help/forms/using/create-your-first-interactive-communication.md) および [解剖学](/help/forms/using/planning-interactive-communications.md)で、Web テンプレートに次のパネルを作成します。

* 請求明細：ドキュメントフラグメントが含まれます
* 顧客の詳細：ドキュメントフラグメントを含める
* 請求の要約：ドキュメントフラグメントを含める
* 料金概要：ドキュメントフラグメントとグラフ（2 列レイアウト）を含めます
* 通話明細：テーブルを含む
* 今すぐ支払う：次を含む： **今すぐ支払う** ボタンと画像
* 付加価値サービス：画像と **購読** 」ボタンをクリックします。

![create_web_template](assets/create_web_template.gif)

ドキュメントフラグメント、グラフ、テーブル、画像、ボタンなどのすべてのエンティティが、インタラクティブ通信を作成する際に追加されます。

**Create_First_IC_templates** フォルダーでWeb チャネル用のテンプレートを作成するには、次の手順を実行します。

1. 次を選択して、適切なテンプレートフォルダーに移動します。 **ツール** > **テンプレート** > **Create_First_IC_templates** フォルダー。
1. 「**作成**」をタップします。
1. の **テンプレートタイプを選択** 設定ウィザード：「 **インタラクティブ通信 — Web チャネル** とタップします。 **次へ**.
1. の **テンプレートの詳細** 設定ウィザード：次を指定します。 **Create_First_IC_Web_Template** をテンプレートタイトルとして使用します。 オプション内容を指定し、「**作成**」をタップします。

   次を示す確認メッセージ： **Create_First_IC_Web_Template** が表示されます。

1. 「**開く**」をタップして、テンプレートエディターでテンプレートを開きます。
1. 「**プレビュー**」オプションの隣にあるドロップダウンリストから「**初期コンテンツ**」を選択します。

   ![template_editor_initial_content](assets/template_editor_initial_content.png)

1. タップ **ルートパネル** 次に、 **+** をクリックして、テンプレートに追加できるコンポーネントのリストを表示します。
1. コンポーネントの一覧から、**ルートパネル**&#x200B;の上に追加する「**パネル**」を選択します。
1. 左側のペインで「**コンテンツ**」タブを選択します。手順 8 で追加された新しいパネルは、コンテンツツリーの&#x200B;**ルートパネル**&#x200B;の下に表示されます。

   ![content_tree_root_panel](assets/content_tree_root_panel.png)

1. パネルを選択し、 ![configure_icon](assets/configure_icon.png) （設定）を参照してください。
1. プロパティペインで、次の手順を実行します。

   1. 「名前」フィールドに&#x200B;**billdetails** と入力します。
   1. 「タイトル」フィールドに、**請求明細**&#x200B;と入力します。
   1. 「**列数**」ドロップダウンリストから、**1** を選択します。
   1. タップ ![done_icon](assets/done_icon.png) をクリックしてプロパティを保存します。

   コンテンツツリーの&#x200B;**請求明細**&#x200B;に更新パネル名が更新されます。

1. 手順 7～11 を繰り返し、次のプロパティを含むパネルをテンプレートに追加します。

   | 名前 | タイトル | 列数 |
   |---|---|---|
   | customerdetails | 顧客情報 | 1 |
   | billsummary | 請求内容 | 1 |
   | summarycharges | 請求概要 | 2 |
   | itemisedcalls | 通話明細 | 1 |
   | paynow | Pay Now | 2 |
   | vas | 付加価値サービス | 1 |

   次の画像は、すべてのパネルがテンプレートに追加された後のコンテンツツリーを示しています。

   ![content_tee_all_panels](assets/content_tee_all_panels.png)

### テンプレートの有効化 {#enable-the-template}

Web テンプレートの作成が終わったら、インタラクティブ通信を作成する際に、そのテンプレートを有効にする必要があります。

Web テンプレートを有効にするには、次の手順を実行します。

1. タップ **ツール** ![ツール](assets/tools-icon.svg) > **テンプレート**.
1. 次に移動： **Create_First_IC_Web_Template** テンプレートを選択してをタップします。 **有効にする**.
1. 再度「**有効**」をタップして確認します。

   これでテンプレートが有効になり、テンプレートのステータスとして「有効」が表示されます。このテンプレートは、Web チャネル用のインタラクティブ通信を作成する際に使用できます。

### インタラクティブ通信でボタンの有効化 {#enabling-buttons-in-interactive-communications}

ユースケースに基づき、「**Pay Now**」および「**登録**」ボタン（アダプティブフォームコンポーネント）をインタラクティブ通信に含める必要があります。インタラクティブ通信でこれらのボタンの仕様を有効にするには、次の手順を実行します。

1. 選択 **構造** を選択します。 **プレビュー** オプション。
1. コンテンツツリーを使用して、**ドキュメントコンテナ**&#x200B;ルートパネルを選択し、「**ポリシー**」をタップして、インタラクティブ通信で使用が許可されているコンポーネントを選択します。

   ![structure_configure_policy](assets/structure_configure_policy.png)

1. 「**プロパティ**」セクションの「**許可されているコンポーネント**」タブで、**アダプティブフォーム**&#x200B;コンポーネントから「**ボタン**」を選択します。

   ![allowed_components_af](assets/allowed_components_af.png)

1. タップ ![done_icon](assets/done_icon.png) をクリックしてプロパティを保存します。
