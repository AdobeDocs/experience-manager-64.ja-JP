---
title: アダプティブフォームフィールドのカスタム外観の作成
seo-title: Create custom appearances for adaptive form fields
description: 'Adaptive Forms の追加設定不要コンポーネントの外観をカスタマイズします。 '
seo-description: Customize appearance of out-of-the-box components in Adaptive Forms.
uuid: 1f2d2ac4-44e1-45f9-a6a0-eb95931b0633
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
discoiquuid: 1115697c-cb7d-441a-876f-3c01761568c0
exl-id: 91d9a31d-a0af-45f6-9a20-4b52e2848979
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 72%

---

# アダプティブフォームフィールドのカスタム外観の作成 {#create-custom-appearances-for-adaptive-form-fields}

## はじめに {#introduction}

アダプティブフォームは[外観フレームワーク](/help/forms/using/introduction-widgets.md)を強化することで、アダプティブフォームフィールドの外観をカスタマイズして独自のユーザーエクスペリエンスの提供を実現します。たとえば、ラジオボタンとチェックボックスをトグルボタンで置き換える、またはカスタムの jQuery プラグインを使用して、電話番号や電子メール ID といったフィールドにおけるユーザーの入力を制限するなどです。

このドキュメントでは、アダプティブフォームフィールドで jQuery プラグインを使用して、これらの代替エクスペリエンスを作成する方法を説明します。加えて、外観をカスタマイズして数値フィールドのコンポーネントを数値ステッパーまたはスライダーとして表示する例も紹介します。

まずは、この記事で使用される重要な用語と概念について見てみましょう。

**外観** アダプティブフォームフィールドの様々な要素のスタイル、ルックアンドフィール、および構成を指します。 通常、ラベル、入力用のインタラクティブ領域、ヘルプアイコン、ならびにフィールドについての短い説明や長い説明などが含まれます。この記事で扱われる外観のカスタマイズは、フィールドの入力領域の外観に適用できます。

**jQuery プラグイン** jQuery ウィジェットフレームワークに基づいて、別の外観を実装するための標準的なメカニズムを提供します。

**ClientLib** 複雑な JavaScript と CSS コードによって駆動される、AEMのクライアント側処理のクライアント側ライブラリシステム。 詳しくは、「クライアント側ライブラリの使用」を参照してください。

**アーキタイプ** Maven プロジェクトの元のパターンまたはモデルとして定義される Maven プロジェクトテンプレートツールキットです。 詳しくは、「アーキタイプの概要」を参照してください。

**ユーザーコントロール** フィールドの値を含むウィジェットのメイン要素を参照し、カスタムウィジェット UI をアダプティブフォームモデルとバインドするための外観フレームワークで使用されます。

## カスタム外観の作成手順 {#steps-to-create-a-custom-appearance}

カスタム外観を作成する手順は、高レベルでは次のようになります。

1. **プロジェクトの作成**:AEMにデプロイするコンテンツパッケージを生成する Maven プロジェクトを作成します。
1. **既存のウィジェットクラスの拡張**:既存のウィジェットクラスを拡張し、必要なクラスを上書きします。
1. **クライアントライブラリを作成する**：`clientLib: af.customwidget` ライブラリを作成して、必要な JavaScript と CSS ファイルを追加します。

1. **プロジェクトのビルドとインストール**:Maven プロジェクトをビルドし、生成されたコンテンツパッケージをAEMにインストールします。
1. **アダプティブフォームの更新**:カスタム外観を使用するためにアダプティブフォームフィールドのプロパティを更新します。

### プロジェクトの作成 {#create-a-project}

Maven アーキタイプは、カスタム外観作成の開始点です。使用するアーキタイプの詳細は、次のとおりです。

* **リポジトリ**:https://repo.adobe.com/nexus/content/groups/public/
* **アーティファクト ID**:custom-appearance-archetype
* **グループ ID**:com.adobe.aemforms
* **バージョン**:1.0.4

次のコマンドを実行して、アーキタイプに基づいたローカルプロジェクトを作成します。

`mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

このコマンドにより Maven プラグインおよびリポジトリからのアーキタイプ情報がダウンロードされ、次の情報に基づいたプロジェクトが生成されます。

* **groupId**：生成された Maven プロジェクトにより使用されるグループ ID です。
* **artifactId**：生成された Maven プロジェクトで使用されるアーティファクト ID です。
* **version**：生成した Maven プロジェクトのバージョンです。
* **package**：ファイル構造に使用されるパッケージです。
* **artifactName**：生成された AEM パッケージのアーティファクトの名前です。
* **packageGroup**：生成された AEM パッケージのパッケージグループです。
* **widgetName**：参照に使用される外観の名前です。

生成されたプロジェクトの構造は次のようになります。

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### 既存のウィジェットのクラスの拡張 {#extend-an-existing-widget-class}

プロジェクトのテンプレートを作成したら、必要に応じて以下の変更を行います。

1. プロジェクトにサードパーティのプラグインを含めます。

   1. サードパーティまたはカスタム jQuery プラグインを `jqueryplugin/javascript` フォルダーおよび関連する CSS ファイルを `jqueryplugin/css` フォルダー。 詳しくは、 `jqueryplugin/javascript and jqueryplugin/css` フォルダー。
   1. `js.txt` および `css.txt` ファイルを変更して、jQuery プラグインの JavaScript ファイルと CSS ファイルが含まれるようにします。

1. フレームワーク内でサードパーティのプラグインを統合して、カスタム外観のフレームワークと jQuery プラグインとのインタラクションを有効にします。新しいウィジェットは、次の関数を拡張または上書きした後でのみ機能します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>Function</strong></td> 
   <td><strong>説明</strong></td> 
  </tr> 
  <tr> 
   <td><code>render</code></td> 
   <td>レンダリング関数は、ウィジェットのデフォルト HTML 要素のための jQuery オブジェクトを返します。デフォルトの HTML 要素は、フォーカス可能タイプとします。例： <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code>、および <code>&lt;li&gt;</code>. 返された要素は <code>$userControl</code>. この <code>$userControl</code> 上記の制約、 <code>AbstractWidget</code> クラスが期待どおりに動作する場合や、一般的な API（フォーカス、クリック）の一部に変更が必要な場合などは、 </td> 
  </tr> 
  <tr> 
   <td><code>getEventMap</code></td> 
   <td>HTML イベントを XFA イベントに変換するマップを返します。<br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> この例は、を示しています。 <code>blur</code> はHTMLイベントで、 <code>XFA_EXIT_EVENT</code> は対応する XFA イベントです。 </td> 
  </tr> 
  <tr> 
   <td><code>getOptionsMap</code></td> 
   <td>オプションの変更時に、実行すべきアクションの詳細を提供するマップを返します。キーはウィジェットに提供されるオプションで、値はオプションの変更が検出されるたびに呼び出される関数です。 ウィジェットには、すべての一般的なオプション（<code>value</code> と <code>displayValue</code> を除く）のハンドラーが用意されています。</td> 
  </tr> 
  <tr> 
   <td><code>getCommitValue</code></td> 
   <td>jQuery ウィジェットフレームワークは、jQuery ウィジェットの値が XFA モデルに保存されたときに（例えばテキストフィールドの exit イベント時に）毎回この関数を読み込みます。実装は、ウィジェットに保存された値を返す必要があります。ハンドラーには、オプションの新しい値が提供されます。</td> 
  </tr> 
  <tr> 
   <td><code>showValue</code></td> 
   <td>デフォルトでは、XFA での enter イベント時に、フィールドの <code>rawValue</code> が表示されます。この関数は、 <code>rawValue</code> を設定します。 </td> 
  </tr> 
  <tr> 
   <td><code>showDisplayValue</code></td> 
   <td>デフォルトでは、XFA での exit イベント時に、フィールドの <code>formattedValue</code> が表示されます。この関数は、 <code>formattedValue</code> を設定します。 </td> 
  </tr> 
 </tbody> 
</table>

1. 必要に応じて `integration/javascript` フォルダーの JavaScript ファイルを更新します。

   * テキストを置換 `__widgetName__` を実際のウィジェット名に置き換えます。
   * 適切なデフォルトのウィジェットクラスからウィジェットを拡張します。多くの場合は、置き換えられる既存のウィジェットに対応したウィジェットクラスになります。親クラス名は複数の場所で使用されるため、ファイル内すべての文字列 `xfaWidget.textField` のインスタンスを検索して、実際使用する親クラスで置き換えることを推奨します。
   * `render` メソッドを拡張して代替の UI を設定します。その場所から jQuery プラグインが起動し、UI またはインタラクション動作を更新します。`render` メソッドは、ユーザーコントロール要素を返します。
   * `getOptionsMap` メソッドを拡張して、ウィジェット内の変更により影響を受けるオプション設定をオーバーライドします。この関数は、オプションの変更時に実行するアクションの詳細を提供するマッピングを返します。 キーはウィジェットに提供されるオプションで、値はオプションの変更が検出されたたびに呼び出される関数です。
   * `getEventMap` メソッドは、そのウィジェットによりトリガーされるイベントを、アダプティブフォームモデルが必要とするイベントとあわせてマッピングします。デフォルト値ではデフォルトのウィジェットの標準 HTML イベントがマッピングされ、代替のイベントがトリガーされた場合は更新の必要があります。
   * `showDisplayValue` および `showValue` は、表示値を適用し、パターン形式文字列を編集します。また、別の動作にオーバーライドすることができます。
   * `getCommitValue` メソッドは `commit` イベント発生時にアダプティブフォームのフレームワークにより呼び出されます。通常これは exit イベントですが、変更により生じるドロップダウン、ラジオボタン、チェックボックス要素は例外とします。詳しくは、「[アダプティブフォームの数式](/help/forms/using/adaptive-form-expressions.md#p-value-commit-script-p)」を参照してください。
   * テンプレートファイルでは、さまざまなメソッドでの導入例が紹介されています。拡張しないメソッドは削除してください。

### クライアントライブラリの作成 {#create-a-client-library}

Maven アーキタイプで生成されたサンプルプロジェクトは、必要なクライアントライブラリを自動で作成し、`af.customwidgets` カテゴリでそれらをクライアントライブラリに含めます。`af.customwidgets` で使用できる JavaScript および CSS ファイルはランタイム時に自動で含まれます。

### 構築とインストール {#build-and-install}

プロジェクトを構築するには、シェルで以下のコマンドを実行して AEM サーバーにインストールする必要のある CRX パッケージを生成します。

`mvn clean install`

>[!NOTE]
>
>Maven プロジェクトは、POM ファイル内のリモートリポジトリを参照します。これは単に参照目的であり、Maven 標準では、リポジトリ情報は `settings.xml` ファイルで取得されます。

### アダプティブフォームの更新 {#update-the-adaptive-form}

カスタム外観をアダプティブフォームフィールドに適用する方法は、次のとおりです。

1. アダプティブフォームを編集モードで開きます。
1. カスタム外観を適用するフィールドの **Property** ダイアログを開きます。
1. 内 **スタイル設定** タブ、更新 `CSS class` プロパティを使用して、 `widget_<widgetName>` 形式 例えば、**widget_numericstepper** です。

## サンプル：カスタム外観の作成 {#sample-create-a-custom-appearance-nbsp}

それでは、数値のフィールドを数値ステッパーまたはスライダーとして表示されるようにカスタム外観を作成する例をみてみましょう。以下の手順を実行します。

1. 以下のコマンドを実行して、Maven アーキタイプをベースとするローカルプロジェクトを作成します。

   `mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   ここでは、次のパラメーターの値の指定が求められます。

   *このサンプルで使用される値は、太字でハイライト表示されています*。

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. `customWidgets` （`artifactID` プロパティで指定された値）ディレクトリに移動して、次のコマンドを実行し Eclipse プロジェクトを生成します。

   `mvn eclipse:eclipse`

1. Eclipse ツールを開き、以下の手順を実行して Eclipse プロジェクトをインポートします。

   1. **[!UICONTROL ファイル／取り込み／既存プロジェクトをワークスペースへ]**&#x200B;を選択します。

   1. 参照して、`archetype:generate` コマンドを実行したフォルダを選択します。

   1. 「**[!UICONTROL Finish]**」をクリックします。

      ![eclipse-screenshot](assets/eclipse-screenshot.png)

1. カスタム外観で使用するウィジェットを選択します。このサンプルでは、次の数値ステッパーウィジェットを使用します。

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   Eclipse プロジェクトでは、`plugin.js` ファイルのプラグインコードを見直して、外観の要件を満たすようにします。このサンプルでは、外観は以下の要件を満たしています。

   * 数値ステッパーは、 `- $.xfaWidget.numericInput`.
   * フィールドにフォーカスすると、ウィジェットの `set value` メソッドが値を設定します。これは、アダプティブフォームウィジェットでは必須要件です。
   * `render` メソッドを起動するには、`bootstrapNumber` メソッドをオーバーライドする必要があります。
   * プラグインのメインソースコード以外でプラグインに依存しません。
   * サンプルではステッパーのスタイル設定を実行しないため、CSS の追加を必要としません。
   * この `$userControl` オブジェクトを `render` メソッド。 これは、`text` タイプのフィールドであり、プラグインコードで複製されます。
   * フィールドが無効の場合に「**+**」および「**-**」ボタンが無効になります。

1. `bootstrap-number-input.js`（jQuery プラグイン）のコンテンツを `numericStepper-plugin.js` ファイルのコンテンツと置き換えます。
1. 内 `numericStepper-widget.js` ファイルを開き、次のコードを追加して、プラグインを呼び出して `$userControl` オブジェクト：

   ```java
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. 内 `numericStepper-widget.js` ファイル、上書き `getOptionsMap` プロパティを使用してアクセスオプションを上書きし、無効モードで+ボタンと — ボタンを非表示にします。

   ```java
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. 変更を保存し、 `pom.xml` ファイルを作成し、次の Maven コマンドを実行してプロジェクトを構築します。

   `mvn clean install`

1. AEM パッケージマネージャーを使ってパッケージをインストールします。

1. カスタム外観を適用するアダプティブフォームを編集モードで開き、次の手順を実行します。

   1. カスタム外観を適用するフィールドを右クリックしてから、「**[!UICONTROL 編集]**」をクリックしてコンポーネントを編集ダイアログを開きます。

   1. 「スタイル設定」タブで、**[!UICONTROL CSS クラス]** プロパティを更新して `widget_numericStepper` を追加します。

これで、新しく作成した外観を使用できるようになりました。
