---
title: AEM Forms Workspace ユーザーインターフェイスのロケールの変更
seo-title: Changing the locale of AEM Forms workspace user interface
description: AEM Forms Workspace を変更して、テキスト、折りたたまれたカテゴリ、キュー、プロセス、およびインターフェイス上の日付選択をローカライズする方法です。
seo-description: How to modify the AEM Forms workspace to localize text, collapsed categories, queues, and processes, and the date picker on the interface.
uuid: f8e7d399-98d9-4655-b51f-0346a5713f06
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: e4ca8188-fb9a-44bf-8437-a98abaa7521a
exl-id: 9968f399-454b-4cb2-b6af-2c16428ca7b4
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 59%

---

# AEM Forms Workspace ユーザーインターフェイスのロケールの変更 {#changing-the-locale-of-aem-forms-workspace-user-interface}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms Workspace では、英語、フランス語、ドイツ語、日本語によるサポートを提供しています。また、AEM Forms Workspace ユーザーインターフェイスをその他の言語にローカライズする機能も提供しています。

AEM Forms Workspace ユーザーインターフェイスを任意の言語にローカライズするには、次のようにします。

* AEM Formsワークスペースのテキストをローカライズする。
* 折りたたまれたカテゴリ、キュー、およびプロセスをローカライズする。
* 日付選択をローカライズする

前述した手順を実行する前に、「[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」に一覧表示されている手順に従っていることを確認してください。 

>[!NOTE]
>
>AEM Forms Workspace のログイン画面の言語を変更するには、 [新しいログイン画面の作成](/help/forms/using/creating-new-login-screen.md).

## テキストのローカライズ {#localizing-text}

次の手順を実行して&#x200B;*新規*&#x200B;言語のサポートおよびブラウザのロケールコード「*nw*」を追加します。

1. CRXDE Lite にログインします。


   CRXDE Lite のデフォルトの URL は、 `https://[server]:[port]/lc/crx/de/index.jsp` です。

1. `apps/ws/locales` の場所に移動して、新しいフォルダー「`nw.`」を作成します。
1.  `translation.json`の場所から`/apps/ws/locales/en-US`の場所に、`/apps/ws/locales/nw`ファイルをコピーします。
1. `/apps/ws/locales/nw`に移動して `translation.json`を開いて編集します。translation.json ファイルにロケール固有の変更を加えます。

   次の例には、AEM Forms Workspace の英語とフランス語のロケールの translation.json ファイルが含まれています。

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## 折りたたまれているカテゴリ、キューおよびプロセスのローカライズ {#localizing-collapsed-categories-queues-and-processes}

AEM Forms Workspace では画像を使用してカテゴリ、キュー、およびプロセスのヘッダを表示します。これらのヘッダをローカライズするには、開発パッケージが必要です。開発パッケージを作成する方法については、「[AEM Forms Workspace コードの構築](introduction-customizing-html-workspace.md#building-html-workspace-code)」を参照してください。

次の手順では、新しくローカライズされた画像ファイルは&#x200B;*Categories_nw.png*、*Queue_nw.png*、および *Processes_nw.png* であると想定しています。画像の推奨される幅は 19px です。

>[!NOTE]
>
>お使いのブラウザのブラウザ言語ロケールコードを検索するには、次のようにします。`https://[server]:[port]/lc/libs/ws/Locale.html`を開きます。

![collapsing_panels_image](assets/collapsing_panels_image.png)

画像をローカライズするには、次の手順を実行します。

1. WebDAV クライアントを使用して、 */apps/ws/images* フォルダー。
1. */apps/ws/css* に移動します。*newStyle.css* を開いて編集し、次のエントリを追加します。

   ```
   #categoryListBar .content.nw {
        background: #3e3e3e url(../images/Categories_nw.png) no-repeat 10px 10px;
    }
   
   #filterListBar .content.nw {
       background: #3e3e3e url(../images/Queues_nw.png) no-repeat 10px 10px;
   }
   
   #processNameListBar .content.nw {
       background: #3e3e3e url(../images/Processes_nw.png) no-repeat 10px 10px;
   }
   ```

1. 「[Workspace のカスタマイズ](/help/forms/using/introduction-customizing-html-workspace.md)」の記事に一覧表示されているすべてのセマンティック変更を実行します。
1. 次に移動： *js/runtime/utility* フォルダーに移動し、編集用に*usersession.js*ファイルを開きます。
1. 元のコードブロックに一覧表示されているコードを探して、ステートメントに条件 *lang ! == &#39;nw&#39;* を追加します。 

   ```
   // Orignal code
   setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

   ```
   //new code
    setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP' && lang !== 'nw')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

## 日付選択のローカライズ {#localizing-date-picker}

API をローカライズするには、開発パッケージが必要です。 開発パッケージを作成する方法については、「[AEM Forms Workspace コードの構築](introduction-customizing-html-workspace.md#building-html-workspace-code)」を参照してください。

1. をダウンロードして抽出します。 [jQuery UI パッケージ](https://jqueryui.com/download/all/)に移動します。 *&lt;extracted jquery=&quot;&quot; ui=&quot;&quot; package=&quot;&quot;>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n
1. ロケールコード nw のjquery.ui.datepicker-nw.js ファイルを apps/ws/js/libs/jqueryui にコピーし、ファイルにロケール固有の変更を行います。
1. `apps/ws/js` に移動し、 `jquery.ui.datepicker-nw.js` ファイルを開いて編集します。 
1. main.js ファイルで、 `jquery.ui.datepicker-nw.js.` にエイリアスを作成します。 `jquery.ui.datepicker-nw.js` ファイルにエイリアスを作成するためのコードは、次のとおりです。

   ```
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. エイリアス `jqueryuidatepickernw` を使用して日付選択を使用するすべてのファイルに `jquery.ui.datepicker-nw.js` ファイルを含めます。日付選択は次のファイルで使用されます。

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   以下のサンプルコードは、jquery.ui.datepicker-nw.js のエントリを追加する方法を示しています。

   ```
   //Original Code
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, slimScroll, UserSearch, LogManager, Logger) {
   ```

   ```
   // Code with Date Picker alias for new language
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'jqueryuidatepickernw', // Date Picker alias
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, jQueryUIDatePickerNW, slimScroll, UserSearch, LogManager, Logger) {
   ```

1. 日付選択 API を使用するすべてのファイルで、デフォルトの日付選択 API 設定を変更します。 日付選択 API は、次のファイルで使用されます。

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   次のコードを変更して新しいロケールを追加します。

   ```
   if (locale === 'ja-JP') {
      $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
      $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
      $.datepicker.setDefaults($.datepicker.regional.fr);
   } else {
      $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```

コピー先：

```
if (locale === 'ja-JP') {
    $.datepicker.setDefaults($.datepicker.regional.ja);
} else if (locale === 'de-DE') {
    $.datepicker.setDefaults($.datepicker.regional.de);
} else if (locale === 'fr-FR') {
    $.datepicker.setDefaults($.datepicker.regional.fr);
} else if (locale === 'nw') {
    $.datepicker.setDefaults($.datepicker.regional.nw);
} else {
    $.datepicker.setDefaults($.datepicker.regional['']);
}
```
