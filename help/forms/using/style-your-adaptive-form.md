---
title: 'アダプティブフォームのスタイル設定 '
seo-title: Style your adaptive form
description: 'カスタムテーマの作成、個別コンポーネントのスタイル設定、テーマでの Web フォントの使用について説明します。 '
seo-description: Learn to create a custom theme, style individual components, and use web fonts in a theme
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
feature: Adaptive Forms
exl-id: 0ccf43eb-f0c6-4204-8325-f891caa8f5af
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '2049'
ht-degree: 69%

---

# アダプティブフォームのスタイル設定 {#do-not-publish-style-your-adaptive-form}

カスタムテーマの作成、個別コンポーネントのスタイル設定、テーマでの Web フォントの使用について説明します。

![](do-not-localize/08-style_your_adaptiveformmain.png)

これは、「[最初のアダプティブフォームを作成する](create-your-first-adaptive-form.md)」シリーズを構成するチュートリアルです。チュートリアル内のユースケースを理解して実際に操作できるように、このシリーズのチュートリアルを最初から順に学習することをお勧めします。

## このチュートリアルについて  {#about-the-tutorial}

テーマを使用すると、アダプティブフォームに独自の外観やスタイルを設定できます。アダプティブフォームエディターの初期設定済みテーマを適用することも、独自のカスタムテーマを作成することもできます。AEM Forms はカスタムテーマを作成するための[テーマエディター](themes.md)を提供します。単一のテーマを使用すると、モバイル、タブレット、デスクトップで開いた同一のアダプティブフォームに異なる外観を設定できます。テーマエディターを使用する場合、CSS や LESS の予備知識は特に必要ありません。

このチュートリアルを終了すると、以下の操作を実行できるようになります。

* 初期設定済みテーマをアダプティブフォームに適用する
* テーマエディターを使用して、アダプティブフォームのテーマを作成する
* 個別コンポーネントのスタイルを設定する
* オプション：カスタムテーマに Web フォントを使用する

チュートリアルを完了すると、フォームの外観は以下のようになります。

![カスタムテーマが使用されているフォーム](assets/styled-adaptive-form.png)

## 事前準備 {#before-you-start}

以下に示すヘッダースタイルとロゴの画像をローカルマシンにダウンロードします。`shipping-address-add-update-form` アダプティブフォームのヘッダーは、ヘッダースタイルとロゴの画像を使用します。ヘッダースタイルの画像はヘッダーの右側に表示されます。

[ファイルを入手](assets/header-style.png)

[ファイルを入手](assets/logo-1.png)

## 手順 1：アダプティブフォームへのテーマの適用 {#step-apply-a-theme-to-your-adaptive-form}

アダプティブフォームエディターは多数の初期設定済みテーマを提供します。アダプティブフォームにカスタムスタイルを使用する場合は、初期設定済みテーマを使用してアダプティブフォームを発行することもできます。テーマはアダプティブフォームから独立しています。同一のテーマを複数のアダプティブフォームに適用できます。テーマをアダプティブフォームに適用するには、次の手順を実行します。

1. アダプティブフォームを編集用に開きます。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. **アダプティブフォームコンテナ**&#x200B;のプロパティを開きます。プロパティブラウザーで、**基本**／**アダプティブフォームのテーマ**&#x200B;に移動します。すべての初期設定済みテーマとカスタムテーマが、「**アダプティブフォームのテーマ**」フィールドに表示されます。デフォルトではキャンバステーマが適用されます。
1. 「**アダプティブフォームのテーマ**」フィールドでテーマを選択します（**調査テーマ**&#x200B;など）。タップ ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 選択したテーマを適用します。

![デフォルトのテーマを使用したアダプティブフォーム](assets/default-adaptive-form.png)

**図：** *デフォルトのテーマを持つアダプティブフォーム*

![調査テーマを使用したアダプティブフォーム](assets/adaptive-form-with-survey-theme.png)

**図：** *調査テーマを持つアダプティブフォーム*

## 手順 2：アダプティブフォームの更新 {#step-update-your-adaptive-form}

上記のデザインでは、既存のアダプティブフォームのプレースホルダーテキストとロゴを変更する必要があります。必要な変更を行うには、次の手順を実行します。

1. ヘッダーの既存のロゴとテキストを変更します。ロゴを削除するには、次の手順を実行します。

   1. フォームエディターでフォームを開きます。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. ヘッダーコンポーネントでロゴ画像をタップし、をタップします。 ![cmppr](assets/cmppr.png) プロパティ。 画像のプロパティで X をタップし、既存のロゴの画像を削除します。
   1. 「アップロード」をタップし、logo.png を選択して、 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 変更を保存します。 画像が [事前準備](/help/forms/using/style-your-adaptive-form.md#before-you-start) 」セクションに入力します。
   1. ヘッダーテキストをタップします。 `We.Retail`をタップし、 ![aem_6_3_edit](assets/aem_6_3_edit.png) **編集**. ヘッダーテキストを次に変更： `we retail`. 太字の適用先： `we`in `we retail`.

   ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. タイトルを削除してプレースホルダーテキストを追加します。

   1. 「顧客 ID 」フィールドをタップし、をタップします。 ![cmppr](assets/cmppr.png) プロパティ。
   1. 「**タイトル**」フィールドの内容を「**プレースホルダーテキスト**」フィールドにコピーします。
   1. コンテンツを削除 **タイトル** フィールドとタップ ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. フォーム内のすべてのテキストボックス、数値ボックス、電子メールフィールドで、上記の 3 つの手順を繰り返します。

   ![updated-adaptive-form](assets/updated-adaptive-form.png)

## 手順 3：アダプティブフォームのカスタムテーマの作成 {#step-create-a-custom-theme-for-your-adaptive-form}

[テーマエディター](/help/forms/using/themes.md)を使用すると、カスタムテーマを作成できます。テーマエディターは非常に強力な WYSIWYG エディターです。視覚的に確認しながら、アダプティブフォームの各種コンポーネントに CSS を適用できます。アダプティブフォームのコンポーネントやパネルのスタイルを詳細にコントロールできます。

アダプティブフォームと同様、テーマは独立したエンティティです。アダプティブフォームのコンポーネントとパネルのスタイル（CSS）が含まれています。スタイルには背景色、状態色、透明度、配置、サイズなど、CSS プロパティが含まれています。テーマを適用すると、指定したスタイルがアダプティブフォームの対応するコンポーネントに適用されます。

このチュートリアルでは、ヘッダー、フッター、テキストコンポーネント、数値コンポーネント、添付ファイルコンポーネント、ボタンのスタイルを設定します。まずテーマを作成することから始めましょう。

### テーマの作成 {#create-a-theme}

1. AEMオーサーインスタンスにログインし、に移動します。 **Adobe Experience Manager** > **Forms** > **テーマ**. デフォルトの URL は [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. 「**[!UICONTROL 作成]**」をタップし、「**[!UICONTROL テーマ]**」を選択します。テーマの作成が必要なフィールドが含まれた「テーマを作成」ページが表示されます。「タイトル」フィールドと「ドキュメント名」フィールドは必須です。

   * **タイトル：** テーマのタイトルを指定します。 （**グローバルテーマ**&#x200B;など）。タイトルはテーマのリストから目的のテーマを見つけるのに役立ちます。
   * **名前：** テーマの名前を指定します。 （**グローバルテーマ**&#x200B;指定された名前のノードがリポジトリーに作成されます。タイトルを入力し始めると、名前フィールドの値が自動的に生成されます。候補として入力された値は変更可能です。「ドキュメント名」フィールドには、英数字、ハイフン、アンダースコアのみを使用できます。無効な入力は、すべてハイフンに置き換えられます。

1. 「**作成**」をタップします。テーマが作成され、フォームを編集用に開くためのダイアログが表示されます。タップ **開く** をクリックして、新しく作成したテーマを新しいタブで開きます。 テーマがテーマエディターで開きます。スタイルを設定する際、テーマエディターは AEM Forms に付属している初期設定済みアダプティブフォームを使用します。

   テーマエディターの UI の使用について詳しくは、 [テーマエディターについて](/help/forms/using/themes.md#aboutthethemeeditor).

1. タップ **テーマオプション** ![theme-options](assets/theme-options.png) > **設定**. 内 **フォームをプレビュー** フィールドで、 **shipping-address-add-update-form** アダプティブフォーム、タップ ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)をタップします。 **保存**. テーマエディターで、デフォルトのアダプティブフォームではなく独自のアダプティブフォームを使用できるようになります。テーマエディターに戻るには、「**キャンセル**」をタップします。

   ![カスタムテーマ](assets/custom-theme.png)

   **図：** *shipping-address-add-update-form アダプティブフォームのテーマエディター*

   ![create-a-theme](assets/create-a-theme.png)

   **図：** *デフォルトフォームを持つアダプティブフォーム*

### ヘッダーとフッターのスタイル設定 {#style-header-and-footer}

ヘッダーとフッターをアダプティブフォームで使用すると、独特な外観を作成できます。通常、ヘッダーには組織のロゴと名前が含まれ、フッターには著作権情報が含まれます。これらは組織の複数のフォーム間で統一されます。shipping-address-add-update-form アダプティブフォームのヘッダーとフッターのスタイルを設定するには、次の手順を実行します。

1. セレクターパネルで&#x200B;**ヘッダー**／**テキスト**&#x200B;オプションに移動します。セレクターパネルはテーマエディターの左側にあります。パネルが表示されない場合は、をタップします。 ![サイドパネルを切り替え](assets/toggle-side-panel.png) サイドパネルを切り替えます。

1. 次のプロパティを **テキスト** アコーディオンとタップ ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | プロパティ | 値 |
   |---|---|
   | フォントファミリー | Arial |
   | フォントカラー | FFFFFF |
   | フォントサイズ | 54 px |

1. ヘッダーウィジェットをタップし、「**ヘッダー**」をタップします。ヘッダーウィジェットのスタイルを設定するオプションが左側に表示されます。を展開します。 **Dimensionと位置** アコーディオン、 **高さ** から `120px`をタップし、 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. ヘッダーウィジェットの「背景」アコーディオンを展開し、「**背景色**」を `F6921E.` に設定します。

   上にマウスポインターを置く **画像とグラデーション** > **+追加**&#x200B;をタップします。 **画像**. 次のプロパティを設定し、 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | プロパティ | 値 |
   |---|---|
   | 画像 | header-style.png をアップロードします。画像が [事前準備](/help/forms/using/style-your-adaptive-form.md#before-you-start) 」セクションに入力します。 |
   | 位置 | 右下 |
   | タイル | 繰り返しなし |

1. テーマエディターで、ヘッダーのロゴをタップし、「**ヘッダーロゴ**」をタップします。「Dimensionと位置」アコーディオンを展開し、次のプロパティを設定して、をタップします。 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

<table> 
 <tbody> 
  <tr> 
   <td>余白</td> 
   <td>値</td> 
  </tr> 
  <tr> 
   <td>余白</td> 
   <td> 
    <ul> 
     <li>上：1.5rem</li> 
     <li>下：-35 px</li> 
     <li>左：1rem<strong><br /> </strong></li> 
    </ul> <p><strong>ヒント：</strong> フィールドごとに異なる値を設定するには、<img src="assets/link.png"> リンクアイコンをタップします。<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>高さ</td> 
   <td>4.75rem</td> 
  </tr> 
 </tbody> 
</table>

1. フッターウィジェットをタップし、「**フッター**」をタップします。を展開します。 **背景** アコーディオン、 **背景色** から `F6921E`をタップし、 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### データ取得コンポーネントのスタイル設定とアダプティブフォームの背景の適用 {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

アダプティブフォームでは複数のコンポーネントを使用してデータを取得できます。例えば、テキストボックスと数値ボックスを使用できます。すべてのデータキャプチャコンポーネントと同じスタイルを指定するか、コンポーネントごとに別々のスタイルを指定することができます。 このチュートリアルでは、数値ボックス（顧客 ID、郵便番号）とテキストボックス（顧客 ID、名前、発送先住所、状態、電子メール）に同じスタイルを適用します。データ取得コンポーネントのスタイルを設定するには：

1. 「顧客 ID」フィールドをタップし、「**フィールドウィジェット**」オプションをタップします。次のプロパティを設定し、 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

<table> 
 <tbody> 
  <tr> 
   <td>アコーディオン</td> 
   <td>プロパティ</td> 
   <td>値</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線の色</td> 
   <td>A7A9AC</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線の半径 </td> 
   <td> 
    <ul> 
     <li>上：7 px<br /> </li> 
     <li>右：7 px<br /> </li> 
     <li>下：7 px<br /> </li> 
     <li>左：7 px<br /> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>テキスト</td> 
   <td>フォントファミリー</td> 
   <td>Arial</td> 
  </tr> 
  <tr> 
   <td>テキスト</td> 
   <td>フォントカラー</td> 
   <td>939598<br /> </td> 
  </tr> 
  <tr> 
   <td>テキスト</td> 
   <td>フォントサイズ</td> 
   <td>18 px</td> 
  </tr> 
  <tr> 
   <td>寸法と位置</td> 
   <td>幅</td> 
   <td>60%</td> 
  </tr> 
  <tr> 
   <td>寸法と位置</td> 
   <td>余白</td> 
   <td> 
    <ul> 
     <li>左：10rem</li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

1. 「顧客 ID」フィールドの上部で空白領域をタップし、「**レスポンシブパネルコンテナ**」をタップします。**背景**／**背景色**&#x200B;を F1F2F2 に設定します。タップ ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![](do-not-localize/responsive-panel-container.png)

### ボタンのスタイル設定 {#style-the-buttons}

カスタムテーマを使用して、アダプティブフォームのすべてのボタンに同じスタイルを適用し、 [インラインスタイル](/help/forms/using/inline-style-adaptive-forms.md) をクリックして、特定のボタンにスタイルを適用します。 ボタンのスタイルを設定するには、次の手順を実行します。

1. 「**送信**」ボタンをタップし、「**ボタン**」オプションをタップします。次のプロパティを設定し、 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

<table> 
 <tbody> 
  <tr> 
   <td>アコーディオン</td> 
   <td>プロパティ</td> 
   <td>値</td> 
  </tr> 
  <tr> 
   <td>背景</td> 
   <td>背景色</td> 
   <td>F6921E</td> 
  </tr> 
  <tr> 
   <td>境界線<br /> </td> 
   <td>境界線の色</td> 
   <td>F6921E</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線の半径 </td> 
   <td> 
    <ul> 
     <li>上：7 px<br /> </li> 
     <li>右：7 px<br /> </li> 
     <li>下：7 px<br /> </li> 
     <li>左：7 px</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>テキスト<br /> </td> 
   <td>フォントファミリー</td> 
   <td>Arial</td> 
  </tr> 
  <tr> 
   <td>テキスト</td> 
   <td>フォントカラー</td> 
   <td>FFFFFF</td> 
  </tr> 
  <tr> 
   <td>テキスト</td> 
   <td>フォントサイズ</td> 
   <td>18 px</td> 
  </tr> 
 </tbody> 
</table>

1. アダプティブフォームに[カスタムテーマを適用](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)するか、グローバルテーマを適用します。スタイルがアダプティブフォームに反映されない場合は、ブラウザーのキャッシュを消去して、もう一度試してください。

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 手順 4：個別コンポーネントのスタイル設定 {#step-style-individual-components}

一部のスタイルは特定のコンポーネントのみに適用されます。このようなコンポーネントのスタイルは、アダプティブフォームエディターで設定します。

1. アダプティブフォームを編集用に開きます。[http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 上部バーで「**スタイル**」オプションを選択します。

   ![style-option](assets/style-option.png)

1. 次をタップします。 **添付** ボタンをクリックし、 ![aem_6_3_edit](assets/aem_6_3_edit.png)アイコン 次のプロパティを **Dimensionと位置** アコーディオン：

   | プロパティ | 値 |
   |---|---|
   | 浮動小数 | Left |
   | 幅 | 10% |

1. 次をタップします。 **政府が承認した住所の配達確認** オプションを選択し、 ![aem_6_3_edit](assets/aem_6_3_edit.png)アイコン 次のプロパティを設定します。

<table> 
 <tbody> 
  <tr> 
   <td>アコーディオン</td> 
   <td>プロパティ</td> 
   <td>値</td> 
  </tr> 
  <tr> 
   <td>寸法と位置</td> 
   <td>浮動小数</td> 
   <td>左</td> 
  </tr> 
  <tr> 
   <td>寸法と位置</td> 
   <td>幅</td> 
   <td>73%</td> 
  </tr> 
  <tr> 
   <td>寸法と位置</td> 
   <td>パディング</td> 
   <td> 
    <ul> 
     <li>左：10 px</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>寸法と位置</td> 
   <td>高さ</td> 
   <td>40 px</td> 
  </tr> 
  <tr> 
   <td>寸法と位置<br /> </td> 
   <td>余白</td> 
   <td><br /> 
    <ul> 
     <li>右：2rem</li> 
     <li>左：10rem </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>背景</td> 
   <td>背景色</td> 
   <td>FFFFFF</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線の幅</td> 
   <td>1 px</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線のスタイル</td> 
   <td>実線</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線の色</td> 
   <td>A7A9AC</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線の半径</td> 
   <td>7 px</td> 
  </tr> 
  <tr> 
   <td>テキスト</td> 
   <td>フォントファミリー</td> 
   <td>Arial</td> 
  </tr> 
  <tr> 
   <td>テキスト</td> 
   <td>フォントカラー</td> 
   <td>BCBEC0</td> 
  </tr> 
  <tr> 
   <td>テキスト</td> 
   <td>フォントサイズ</td> 
   <td>18 px</td> 
  </tr> 
  <tr> 
   <td>テキスト</td> 
   <td>行の高さ</td> 
   <td>2</td> 
  </tr> 
 </tbody> 
</table>

1. 次をタップします。 **送信** ボタンをクリックし、 ![aem_6_3_edit](assets/aem_6_3_edit.png) アイコン 次のプロパティを設定します。

<table> 
 <tbody> 
  <tr> 
   <td>アコーディオン</td> 
   <td>プロパティ</td> 
   <td>値</td> 
  </tr> 
  <tr> 
   <td>寸法と位置</td> 
   <td>浮動小数</td> 
   <td>Right</td> 
  </tr> 
  <tr> 
   <td>寸法と位置</td> 
   <td>余白</td> 
   <td> 
    <ul> 
     <li>上：5rem</li> 
     <li>右：14rem</li> 
     <li>下：20 px</li> 
     <li>左：20 px<br /> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>背景</td> 
   <td>背景色</td> 
   <td>F6921E</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線の色</td> 
   <td>F6921E</td> 
  </tr> 
 </tbody> 
</table>

![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## 手順 5：オプション：カスタムテーマでの Web フォントの使用 {#step-bonus-section-using-web-fonts-in-a-custom-theme}

アダプティブフォームは各種フォントを使用してデザインできます。アダプティブフォームのデザインに使用するフォントが、アダプティブフォームを表示するデバイスに存在しない場合があります。Web フォントサービスを使用して、必要なフォントをターゲットデバイスに配信できます。

Adobe Typekit は Web フォントサービスです。アダプティブフォームでこのサービスを設定、使用できます。アダプティブフォームでAdobe Typekitを使用するには：

>[!NOTE]
>
>![typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) Typekit は現在はAdobe Fontsと呼ばれ、Creative Cloudや他の購読に含まれています。 [詳細情報](https://fonts.adobe.com/)を参照してください。

1. の作成 [Adobe Typekit](https://typekit.com/) アカウント、キットの作成、キットへのフォントMyriad Pro の追加、キットの公開、キット ID の取得を行います。 アダプティブフォームでAdobe Typekitフォント（Web フォント）を使用する必要があります。
1. AEM Formsサーバーで、に移動します。 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **Adobe Experience Manager** > **ツール** ![ハンマー](assets/hammer.png) > **導入** > **Cloud Services**. Cloud Servicesページで、に移動します。 **サードパーティのサービス** > **Typekit**&#x200B;をクリックし、 **設定** Typekit の下に表示されます。 設定が既に使用可能な場合は、「+」ボタンをクリックして新しいインスタンスを作成します。

   設定を作成ダイアログで、 **タイトル** 設定の場合は、「 」をクリックします。 **作成**. 設定ページにリダイレクトされます。表示される編集コンポーネントダイアログで、 **キット ID** をクリックし、 **OK**.

1. TypeKit 設定を使用するようにテーマを設定します。オーサーインスタンスで、を開きます。 **グローバルテーマ** （テーマエディター）を使用します。 テーマエディターで、テーマオプション![ theme-options](assets/theme-options.png)／設定に移動します。In **Typekit 設定** 「 」フィールドでキットを選択し、 **保存**.

   Typekit に追加されたフォントは、 **テキスト** アコーディオンを使用します。
