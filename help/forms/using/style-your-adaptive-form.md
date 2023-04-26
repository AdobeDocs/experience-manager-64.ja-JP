---
title: アダプティブフォームのスタイル設定
seo-title: Style your adaptive form
description: カスタムテーマの作成、個々のコンポーネントのスタイル設定、テーマでの Web フォントの使用について説明します
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
ht-degree: 56%

---

# アダプティブフォームのスタイル設定 {#do-not-publish-style-your-adaptive-form}

カスタムテーマの作成、個々のコンポーネントのスタイル設定、テーマでの Web フォントの使用について説明します

![](do-not-localize/08-style_your_adaptiveformmain.png)

このチュートリアルは、 [最初のアダプティブフォームを作成する](create-your-first-adaptive-form.md) 系列。 チュートリアルの使用例を理解、実行、デモするために、時系列に従うことをお勧めします。

## チュートリアルについて  {#about-the-tutorial}

テーマを使用して、アダプティブフォームに独自の外観とスタイルを設定することができます。 アダプティブフォームエディターに付属している標準のテーマを適用することも、独自のカスタムテーマを作成することもできます。 AEM Forms [テーマエディター](themes.md) をクリックしてカスタムテーマを作成します。 1 つのテーマで、モバイル、タブレット、デスクトップで開いた同じアダプティブフォームに異なる外観を提供できます。 CSS または LESS に関する事前の知識は、テーマエディターを使用する必要はありませんが、これは必須です。

このチュートリアルを最後まで学習すると、次の内容を習得できます。

* 標準搭載のテーマをアダプティブフォームに適用する
* テーマエディターを使用してアダプティブフォームのテーマを作成する
* 個々のコンポーネントのスタイル設定
* ボーナスセクション：カスタムテーマでの Web フォントの使用

このチュートリアルを完了すると、フォームは次のようになります。

![カスタムテーマが使用されているフォーム](assets/styled-adaptive-form.png)

## 事前準備 {#before-you-start}

以下に示すヘッダースタイルとロゴの画像をローカルマシンにダウンロードします。 `shipping-address-add-update-form` アダプティブフォームのヘッダーは、ヘッダースタイルとロゴの画像を使用します。ヘッダースタイルの画像はヘッダーの右側に表示されます。

[ファイルを入手](assets/header-style.png)

[ファイルを入手](assets/logo-1.png)

## 手順 1:アダプティブフォームにテーマを適用する {#step-apply-a-theme-to-your-adaptive-form}

アダプティブフォームエディターには、すぐに使用できる複数のテーマが用意されています。 アダプティブフォームでカスタムスタイルを使用しない場合は、標準のテーマを持つアダプティブフォームを発行することもできます。 テーマはアダプティブフォームとは独立しています。 同じテーマを複数のアダプティブフォームに適用することができます。 テーマをアダプティブフォームに適用するには：

1. アダプティブフォームを編集用に開きます。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. のプロパティを開く **アダプティブフォームコンテナ**. プロパティブラウザーで、に移動します。 **基本** > **アダプティブフォームのテーマ**. すべての初期設定済みテーマとカスタムテーマが、「**アダプティブフォームのテーマ**」フィールドに表示されます。デフォルトではキャンバステーマが適用されます。
1. テーマを **アダプティブフォームのテーマ** フィールドに入力します。 例： **調査テーマ**. ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) をタップして、選択したテーマを適用します。

![デフォルトのテーマを使用したアダプティブフォーム](assets/default-adaptive-form.png)

**図：** *デフォルトのテーマを使用したアダプティブフォーム*

![調査テーマを使用したアダプティブフォーム](assets/adaptive-form-with-survey-theme.png)

**図：** *調査テーマを使用したアダプティブフォーム*

## 手順 2:アダプティブフォームの更新 {#step-update-your-adaptive-form}

上記のデザインでは、既存のアダプティブフォームのプレースホルダーテキストとロゴを変更する必要があります。 必要な変更を行うには、次の手順を実行します。

1. ヘッダーの既存のロゴおよびテキストを変更します。 ロゴを削除するには：

   1. フォームをフォームエディターで開きます。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. ヘッダーコンポーネントでロゴの画像をタップし、![cmppr](assets/cmppr.png) 「プロパティ」をタップします。画像のプロパティで X をタップし、既存のロゴの画像を削除します。
   1. 「アップロード」をタップして、logo.png を選択し、 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) をタップして変更を保存します。この画像は「[事前準備](/help/forms/using/style-your-adaptive-form.md#before-you-start)」セクションでダウンロードした画像です。
   1. ヘッダーテキスト `We.Retail` をタップしてから、 ![aem_6_3_edit](assets/aem_6_3_edit.png) 「**編集**」をタップします。ヘッダーテキストを `we retail` に変更します。太字書式を `we retail` の `we` にのみ適用します。

   ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. タイトルを削除してプレースホルダーテキストを追加します。

   1. 「顧客 ID」フィールドをタップし、![cmppr](assets/cmppr.png)「プロパティ」をタップします。
   1. 「**タイトル**」フィールドの内容を「**プレースホルダーテキスト**」フィールドにコピーします。
   1. 「**タイトル**」 フィールドのコンテンツを削除して、![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) をタップします。
   1. フォーム内のすべてのテキストボックス、数値ボックス、メールフィールドで、上記の 3 つの手順を繰り返します。

   ![updated-adaptive-form](assets/updated-adaptive-form.png)

## 手順 3:アダプティブフォームのカスタムテーマの作成 {#step-create-a-custom-theme-for-your-adaptive-form}

以下を使用できます。 [テーマエディター](/help/forms/using/themes.md) をクリックしてカスタムテーマを作成します。 テーマエディターは、WYSIWYG の全機能を備えたエディターです。 これは、アダプティブフォームの様々なコンポーネントに CSS を適用する視覚的な方法です。 アダプティブフォームのコンポーネントやパネルのスタイルをより細かく制御できます。

テーマは、アダプティブフォームと同様、個別のエンティティです。 アダプティブフォームのコンポーネントやパネルのスタイル (CSS) が含まれています。 スタイルには、背景色、状態色、透明度、整列、サイズなどの CSS プロパティが含まれます。 テーマを適用すると、指定したスタイルがアダプティブフォームの対応するコンポーネントに適用されます。

このチュートリアルでは、ヘッダーとフッター、テキストと数値のコンポーネント、添付ファイルコンポーネント、ボタンのスタイルを設定します。 まずテーマを作成することから始めましょう。

### テーマの作成 {#create-a-theme}

1. AEM オーサーインスタンスにログインして、**Adobe Experience Manager**／**Forms**／**テーマ**&#x200B;に移動します。デフォルトの URL は [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes) です。 
1. 「**[!UICONTROL 作成]**」をタップし、「**[!UICONTROL テーマ]**」を選択します。テーマの作成が必要なフィールドを含む「テーマを作成」ページが表示されます。「タイトル」フィールドと「ドキュメント名」フィールドは必須です。

   * **タイトル：**&#x200B;テーマのタイトルを指定します。例： **グローバルテーマ。** タイトルを指定すると、テーマのリストからテーマを特定しやすくなります。
   * **名前：**&#x200B;テーマの名前を指定します。例： **グローバルテーマ**&#x200B;指定された名前のノードがリポジトリーに作成されます。タイトルを入力し始めると、名前フィールドの値が自動的に生成されます。候補として入力された値は変更可能です。「ドキュメント名」フィールドには、英数字、ハイフン、アンダースコアのみを使用できます。無効な入力は、すべてハイフンに置き換えられます。

1. 「**作成**」をタップします。テーマが作成され、フォームを編集用に開くためのダイアログが表示されます。「**開く**」をタップし、新規作成されたテーマを新しいタブで開きます。テーマがテーマエディターで開きます。スタイル設定の場合、テーマエディターは、AEM Formsに付属の標準のアダプティブフォームを使用します。

   テーマエディター UI の使用について詳しくは、「[テーマエディターについて](/help/forms/using/themes.md#aboutthethemeeditor)」を参照してください。

1. **テーマオプション** ![theme-options](assets/theme-options.png)／**設定**&#x200B;をタップします。「**フォームのプレビュー**」フィールドで **shipping-address-add-update-form** アダプティブフォームを選択し、 「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」、「 **保存**」の順にタップします。テーマエディターで、デフォルトのアダプティブフォームではなく独自のアダプティブフォームを使用できるようになります。テーマエディターに戻るには、「**キャンセル**」をタップします。

   ![カスタムテーマ](assets/custom-theme.png)

   **図：** *shipping-address-add-update-form アダプティブフォームを使用したテーマエディター*

   ![テーマの作成](assets/create-a-theme.png)

   **図：** *デフォルトのフォームを使用したアダプティブフォーム*

### ヘッダーとフッターのスタイル設定 {#style-header-and-footer}

ヘッダーとフッターを使用すると、アダプティブフォームの外観が一貫して独特になります。 通常、ヘッダーには組織のロゴと名前が含まれ、フッターには著作権情報が含まれます。また、これらは組織の複数の形式で同じままです。 shipping-address-add-update-form アダプティブフォームのヘッダーとフッターのスタイルを設定するには、次の手順を実行します。

1. 次に移動： **ヘッダー** > **テキスト** 」オプションが表示されます。 セレクターパネルは、テーマエディターの左側に表示されます。 パネルが表示されない場合は、をタップします。 ![サイドパネルを切り替え](assets/toggle-side-panel.png) サイドパネルを切り替えます。

1. 「**テキスト**」アコーディオンで以下のプロパティを設定し、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

   | プロパティ | 値 |
   |---|---|
   | フォントファミリー | Arial |
   | フォントカラー | FFFFFF |
   | フォントサイズ | 54px |

1. ヘッダーウィジェットをタップし、「**ヘッダー**」をタップします。ヘッダーウィジェットのスタイルを設定するオプションが左側に表示されます。「**寸法と位置**」アコーディオンを展開し、「**高さ** 」を `120px`に設定して、 「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。
1. ヘッダーウィジェットの「背景」アコーディオンを展開し、「**背景色**」を「`F6921E.`」に設定します。

   **画像とグラデーション**／**+ 追加**&#x200B;にポインターを合わせ、 「**画像**」をタップします。以下のプロパティを設定し、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

   | プロパティ | 値 |
   |---|---|
   | 画像 | header-style.png をアップロードします。 この画像は「[事前準備](/help/forms/using/style-your-adaptive-form.md#before-you-start)」セクションでダウンロードした画像です。 |
   | 位置 | 右下 |
   | タイル | 繰り返しなし |

1. テーマエディターで、ヘッダーのロゴをタップし、「**ヘッダーロゴ**」をタップします。「寸法と位置」アコーディオンを展開し、次のプロパティを設定して、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

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
     <li>下：-35px</li> 
     <li>左：1rem<strong><br /> </strong></li> 
    </ul> <p><strong>ヒント：</strong> フィールドごとに異なる値を設定するには、<img src="assets/link.png"> リンクアイコンをタップします。<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>高さ</td> 
   <td>4.75rem</td> 
  </tr> 
 </tbody> 
</table>

1. フッターウィジェットをタップし、「**フッター**」をタップします。「**背景**」アコーディオンを展開し、「**背景色**」を「`F6921E` 」に設定して、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

### データ取得コンポーネントのスタイルを設定し、アダプティブフォームに背景を適用する {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

アダプティブフォーム内の複数のコンポーネントを使用して、データを取り込むことができます。 例えば、テキストボックスや数値ボックスなどです。 すべてのデータ取得コンポーネントに同じスタイルを設定することも、コンポーネントごとに異なるスタイルを設定することもできます。このチュートリアルでは、数値ボックス（顧客 ID、郵便番号）とテキストボックス（顧客 ID、名前、発送先住所、状態、メール）に同じスタイルを適用します。データ取得コンポーネントのスタイルを設定するには、次の手順を実行します。

1. 「顧客 ID」フィールドをタップし、「**フィールドウィジェット**」オプションをタップします。次のプロパティを設定し、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

<table> 
 <tbody> 
  <tr> 
   <td>アコーディオン</td> 
   <td>プロパティ</td> 
   <td>値</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>枠色</td> 
   <td>A7A9AC</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線の半径 </td> 
   <td> 
    <ul> 
     <li>上：7px<br /> </li> 
     <li>右：7px<br /> </li> 
     <li>下：7px<br /> </li> 
     <li>左：7px<br /> </li> 
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
   <td>18px</td> 
  </tr> 
  <tr> 
   <td>Dimensionと位置</td> 
   <td>幅</td> 
   <td>60%</td> 
  </tr> 
  <tr> 
   <td>Dimensionと位置</td> 
   <td>余白</td> 
   <td> 
    <ul> 
     <li>左：10rem</li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

1. 「顧客 ID」フィールドの上部で空白領域をタップし、「**レスポンシブパネルコンテナ**」をタップします。**背景**／**背景色**&#x200B;を F1F2F2 に設定します。「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

   ![](do-not-localize/responsive-panel-container.png)

### ボタンのスタイル設定 {#style-the-buttons}

カスタムテーマを使用すると、アダプティブフォームのすべてのボタンに同じスタイルを適用することも、特定のボタンに[インラインスタイル設定](/help/forms/using/inline-style-adaptive-forms.md)を適用することもできます。ボタンのスタイルを設定するには、次の手順を実行します。

1. 「**送信**」ボタンをタップし、「**ボタン**」オプションをタップします。次のプロパティを設定し、「![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)」をタップします。

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
   <td>枠色</td> 
   <td>F6921E</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線の半径 </td> 
   <td> 
    <ul> 
     <li>上：7px<br /> </li> 
     <li>右：7px<br /> </li> 
     <li>下：7px<br /> </li> 
     <li>左：7px</li> 
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
   <td>18px</td> 
  </tr> 
 </tbody> 
</table>

1. [カスタムテーマの適用](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)、グローバルテーマをアダプティブフォームに適用します。 スタイルがアダプティブフォームに反映されない場合は、ブラウザーのキャッシュを削除した後、もう一度実行してください。

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 手順 4:個々のコンポーネントのスタイル設定 {#step-style-individual-components}

一部のスタイルは、特定のコンポーネントにのみ適用されます。 このようなコンポーネントは、アダプティブフォームエディターでスタイル設定されます。

1. アダプティブフォームを編集用に開きます。[http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 上部バーで「**スタイル**」オプションを選択します。

   ![style-option](assets/style-option.png)

1. 「**添付**」ボタンをタップし、![aem_6_3_edit](assets/aem_6_3_edit.png) アイコンをタップします。「**寸法と位置**」アコーディオンで以下のプロパティを設定します。

   | プロパティ | 値 |
   |---|---|
   | 浮動小数 | 左 |
   | 幅 | 10% |

1. 「**Government approved address proof**」オプションをタップし、![aem_6_3_edit](assets/aem_6_3_edit.png) アイコンをタップします。次のプロパティを設定します。

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
     <li>左：10px</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>寸法と位置</td> 
   <td>高さ</td> 
   <td>40px</td> 
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
   <td>1px</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線のスタイル</td> 
   <td>実線</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>枠色</td> 
   <td>A7A9AC</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>境界線の半径</td> 
   <td>7px</td> 
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
   <td>18px</td> 
  </tr> 
  <tr> 
   <td>テキスト</td> 
   <td>行の高さ</td> 
   <td>2</td> 
  </tr> 
 </tbody> 
</table>

1. 「**送信**」ボタンをタップし、![aem_6_3_edit](assets/aem_6_3_edit.png) アイコンをタップします。次のプロパティを設定します。

<table> 
 <tbody> 
  <tr> 
   <td>アコーディオン</td> 
   <td>プロパティ</td> 
   <td>値</td> 
  </tr> 
  <tr> 
   <td>Dimensionと位置</td> 
   <td>浮動小数</td> 
   <td>右</td> 
  </tr> 
  <tr> 
   <td>Dimensionと位置</td> 
   <td>余白</td> 
   <td> 
    <ul> 
     <li>上：5rem</li> 
     <li>右：14rem</li> 
     <li>下：20px</li> 
     <li>左：20px<br /> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>背景</td> 
   <td>背景色</td> 
   <td>F6921E</td> 
  </tr> 
  <tr> 
   <td>境界線</td> 
   <td>枠色</td> 
   <td>F6921E</td> 
  </tr> 
 </tbody> 
</table>

![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## 手順 5:ボーナスセクション：カスタムテーマでの Web フォントの使用 {#step-bonus-section-using-web-fonts-in-a-custom-theme}

様々なフォントを使用して、アダプティブフォームをデザインすることができます。 アダプティブフォームが表示されるすべてのデバイスに、アダプティブフォームのデザインに使用されるフォントがない場合があります。 Web フォントサービスを使用すると、必要なフォントを目的のデバイスで使用できます。

Adobe Typekitは Web フォントサービスです。 アダプティブフォームでこのサービスを設定、使用できます。アダプティブフォームでAdobe Typekitを使用するには：

>[!NOTE]
>
>![typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) Typekit は現在はAdobe Fontsと呼ばれ、Creative Cloudや他の購読に含まれています。 [詳細情報](https://fonts.adobe.com/)。

1. の作成 [Adobe Typekit](https://typekit.com/) アカウント、キットの作成、キットへのフォントMyriad Pro の追加、キットの公開、キット ID の取得を行います。 アダプティブフォームでAdobe Typekitフォント（Web フォント）を使用する必要があります。
1. AEM Formsサーバーで、に移動します。 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **Adobe Experience Manager** > **ツール** ![ハンマー](assets/hammer.png) > **導入** > **Cloud Services**. Cloud Servicesページで、に移動します。 **サードパーティのサービス** > **Typekit**&#x200B;をクリックし、 **設定** Typekit の下に表示されます。 設定が既に使用可能な場合は、「+」ボタンをクリックして新しいインスタンスを作成します。

   設定を作成ダイアログで、新しい設定の「**タイトル**」を指定し、「**作成**」をクリックします。設定ページにリダイレクトされます。コンポーネントを編集ダイアログが表示されるので、**キット ID** を入力して「**OK**」をクリックします。

1. TypeKit 設定を使用するようにテーマを設定します。 オーサーインスタンスで、テーマエディターを使用して「**グローバルテーマ**」を開きます。テーマエディターで、テーマオプション![ theme-options](assets/theme-options.png)／設定に移動します。In **Typekit 設定** 「 」フィールドでキットを選択し、 **保存**.

   Typekit に追加されたフォントは、 **テキスト** アコーディオンを使用します。
