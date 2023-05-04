---
title: カスタムアダプティブフォームテーマの作成
seo-title: Creating custom adaptive form themes
description: アダプティブフォームテーマは、アダプティブフォームのスタイル（ルックアンドフィール）を定義するAEMクライアントライブラリです。 カスタムアダプティブフォームテーマを作成する方法を説明します。
seo-description: An adaptive form theme is an AEM client library that you use to define the styles (look and feel) for an adaptive form. Learn how you can create custom adaptive form themes.
uuid: b25df10e-b07c-4e9d-a799-30f1c6fb3c44
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 437e6581-4eb1-4fbd-a6da-86b9c90cec89
exl-id: e6aa866f-3483-4db1-abaa-01ee585928dc
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 55%

---

# カスタムアダプティブフォームテーマの作成 {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!CAUTION]
>
>AEM Forms は、アダプティブフォームの[テーマ](/help/forms/using/themes.md)を作成および変更するための[テーマエディター](/help/forms/using/themes.md)機能を提供します。この記事に示す手順は、 [テーマエディター](/help/forms/using/themes.md)が存在しないバージョンからアップデートし、LESS/CSS ファイルを使用して作成されたテーマに対する投資を既におこなっている場合（テーマ前のエディター方式）のみ実行します。

## 前提条件 {#prerequisites}

* LESS（Leaner CSS）の知識
* Adobe Experience Managerでクライアントライブラリを作成する方法
* [アダプティブフォームテンプレートの作成](/help/forms/using/custom-adaptive-forms-templates.md) 作成したテーマを使用する場合

## アダプティブフォームのテーマ {#adaptive-form-theme}

An **アダプティブフォームのテーマ** は、アダプティブフォームのスタイル（ルックアンドフィール）の定義に使用するAEMクライアントライブラリです。

次を作成します。 **アダプティブテンプレート** テーマをテンプレートに適用します。 次に、このカスタムテンプレートを使用して **アダプティブフォーム**.

![アダプティブフォームとクライアントライブラリ](assets/hierarchy.png)

## アダプティブフォームテーマを作成するには {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>次の手順は、ノード、プロパティ、フォルダなどのAEMオブジェクトのサンプル名を使用して説明します。
>
>この手順にしたがって同じ名前を使用すると、結果として次のスナップショットと同じようなテンプレートが出来上がるはずです：

![フォレストテーマのアダプティブフォームのスナップショット](assets/thumbnail.png)
**図：** *フォレストテーマのサンプル*

1. `/apps`ノードの下に `cq:ClientLibraryFolder` タイプのノードを作成します。

   例として、以下のノードを作成します：

   `/apps/myAfThemes/forestTheme`

1. 複数の値を持つ文字列プロパティ `categories`をノードに追加し、適切な値に設定します。

   例えば、プロパティを `af.theme.forest` に設定します。

   ![CRX レポジトリのスナップショット](assets/3-2.png)

1. 手順 1 で作成したノードに、 `less` と `css` の 2 つのフォルダーと `css.txt` のファイルを追加します：

   * `less` フォルダー：`less` 変数と CSS スタイルの管理に使用される `less mixins` を定義する `less` 変数ファイルが含まれています。

      このフォルダーは、`less` 変数ファイル、`less` ミックスインファイル、ミックスインと変数を使用してスタイルを定義する `less` ファイルから構成されています。そして、これらすべての less ファイルは、styles.less にインポートされます。

   * `css` フォルダー：テーマで使用される静的スタイルを定義する CSS ファイルが含まれています。

   **LESS 変数ファイル**:これらはファイルで、CSS スタイルの定義で使用される変数を定義または上書きします。

   アダプティブフォームは、以下の.less ファイルで定義された OOTB 変数を提供します。

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   アダプティブフォームは、次のファイルで定義されているサードパーティ変数も提供しています：

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   アダプティブフォームで提供される LESS 変数 を使用する、これらの変数を上書きする、または 新しく LESS 変数を作成することができます。

   >[!NOTE]
   >
   >LESS プリプロセッサーのファイルをインポートする際に、import 文でファイルの相対パスを指定します。

   上書き変数の例：

   ```
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   `less` 変数を上書きするには：

   1. デフォルトのアダプティブフォーム変数を読み込む：

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. 次に、上書きされた変数を含む LESS ファイルをインポートします。

   新しい変数の定義の例：

   ```
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **LESS ミックスインファイル：**&#x200B;変数を引数として受け入れる関数を定義することができます。これらの関数の出力は、結果のスタイルです。 CSS スタイルの繰り返しを避けるために、これらの mixin を異なるスタイルで使用します。

   アダプティブフォームは、次のファイルで定義された OOTB mixin を提供します。

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   アダプティブフォームは、次のファイルで定義されているサードパーティミックスインも提供しています：

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   ミックスインの定義の例： 

   ```
   .rounded-corners (@radius) {
     -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
     -ms-border-radius: @radius;
     -o-border-radius: @radius;
     border-radius: @radius;
   }
   
   .border(@color, @type, @size) {
      border: @color @size @type;
   }
   ```

   **styles.less ファイル：**&#x200B;このファイルは、クライアントライブラリに使わなくてはならないすべての LESS ファイル（変数、ミックスイン、スタイル）を含むために使用します。

   次の `styles.less` ファイルのサンプルでは、インポートステートメントは任意の順序で配置することができます。

   次の LESS ファイルをインポートするためのステートメントは必須です：

   * `globalvariables.less`
   * `layoutvariables.less`
   * `components.less`
   * `layouts.less`

   ```
   @import "../../../clientlibs/fd/af/guidetheme/common/less/globalvariables.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layoutvariables.less";
   @import "forestTheme-variables";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/components.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layouts.less";
   
   /* custom styles */
   
   .guidetoolbar {
     input[type="button"], button, .button {
       .rounded-corners (@button-radius);
       &:hover {
         background-color: @button-hover-bg-color;
       }
       &:focus {
         background-color: @button-focus-bg-color;
       }
     }
   }
   
   form {
       background-image: url(../images/forest.png);
    background-repeat: no-repeat;
    background-size: 100%;
   }
   ```

   `css.txt` には、ライブラリにダウンロードする CSS ファイルのパスが含まれています。

   次に例を示します。

   ```
   #base=/apps/clientlibs/fd/af/third-party/css
   bootstrap.css
   
   #base=less
   styles.less
   
   #base=/apps/clientlibs/fd/xfaforms/xfalib/css
   datepicker.css
   listboxwidget.css
   scribble.css
   dialog.css
   ```

   >[!NOTE]
   >
   >styles.less ファイルは必須ではありません。 つまり、カスタムスタイル、変数、mixin を定義していない場合は、このファイルを作成する必要はありません。
   >
   >ただし、style.less ファイルを作成しない場合、css.txt ファイル内で次の行のコメントを解除する必要があります。
   >
   >**`#base=less`**
   >
   >さらに、次の行をコメントアウトします：
   >
   >**`styles.less`**

## アダプティブフォームでテーマを使用するには {#to-use-a-theme-in-an-adaptive-form}

アダプティブフォームテーマを作成した後、このテーマをアダプティブフォームで使用するには、次の手順を行ないます：

1. 「[アダプティブフォームテーマを作成するには](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p)」のセクションで作成したテーマを含めるには、`cq:Component` タイプのカスタムページを作成します。

   例：`/apps/myAfCustomizations/myAfPages/forestPage`

   1. `sling:resourceSuperType` プロパティを追加し、その値を `fd/af/components/page/base` に設定します。

      ![CRX レポジトリのスナップショット](assets/1-2.png)

   1. ページでテーマを使用するには、ノードに上書きファイル library.jsp を追加する必要があります。

      次に、この記事の「アダプティブフォームテーマを作成するには」の節で作成したテーマを読み込みます。

      以下のサンプルコードでは、`af.theme.forest` のテーマをインポートしています。

      ```
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **オプション**：カスタムページでは、header.jsp、footer.jsp、the body.jsp を必要に応じて上書きしてください。

1. jcr:content が前の手順で作成されたカスタムページ（例：`myAfCustomizations/myAfPages/forestPage)`）を指しているカスタムテンプレート（例：`/apps/myAfCustomizations/myAfTemplates/forestTemplate`）を作成します。

   ![CRX レポジトリのスナップショット](assets/2-1.png)

1. 前の手順で作成したテンプレートを使用して、アダプティブフォームを作成します。 アダプティブフォームのルックアンドフィールは、この記事の「アダプティブフォームテーマを作成するには」の節で作成したテーマによって定義されます。
