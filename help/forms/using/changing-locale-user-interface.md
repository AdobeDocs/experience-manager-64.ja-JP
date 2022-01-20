---
title: AEM Forms Workspace ユーザーインターフェイスのロケールの変更
seo-title: Changing the locale of AEM Forms workspace user interface
description: インターフェイス上で AEM Forms Workspace を変更してテキスト、折りたたまれているカテゴリ、キュー、プロセス、および日付選択をローカライズする方法。
seo-description: How to modify the AEM Forms workspace to localize text, collapsed categories, queues, and processes, and the date picker on the interface.
uuid: f8e7d399-98d9-4655-b51f-0346a5713f06
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: e4ca8188-fb9a-44bf-8437-a98abaa7521a
exl-id: 9968f399-454b-4cb2-b6af-2c16428ca7b4
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 55%

---

# AEM Forms Workspace ユーザーインターフェイスのロケールの変更 {#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Forms workspace は、英語、フランス語、ドイツ語、日本語の各言語を標準でサポートしています。 また、AEM Forms Workspace のユーザーインターフェイスを他の言語にローカライズする機能も提供しています。

AEM Forms Workspace ユーザーインターフェイスを選択した言語にローカライズするには：

* AEM Forms Workspace のテキストをローカライズします。
* 折りたたまれているカテゴリ、キュー、およびプロセスをローカライズする。
* 日付選択をローカライズする。

上記の手順を実行する前に、次の手順に従ってください： [AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md).

>[!NOTE]
>
>AEM Forms Workspace のログイン画面の言語を変更するには、「[新しいログイン画面の作成](/help/forms/using/creating-new-login-screen.md)」を参照してください。

## テキストのローカライズ {#localizing-text}

言語のサポートを追加するには、次の手順を実行します。 *新規* ブラウザのロケールコード *nw*.

1. CRXDE Lite にログインします。

   デフォルトのCRXDE LiteURL は `https://[server]:[port]/lc/crx/de/index.jsp`.

1. 場所に移動します。 `apps/ws/locales` 新しいフォルダーを作成します。 `nw.`
1. ファイルをコピーします。 `translation.json`場所から `/apps/ws/locales/en-US` 場所 `/apps/ws/locales/nw`.
1. に移動します。 `/apps/ws/locales/nw` を開きます。 `translation.json` （編集用） translation.json ファイルにロケール固有の変更を行います。

   次の例では、AEM Forms Workspace の英語およびフランス語のロケールの translation.json ファイルを示します。

   ![translation_json_in_en](assets/translation_json_in_en.png) ![translation_json_in_fr](assets/translation_json_in_fr.png)

## 折りたたまれているカテゴリ、キュー、およびプロセスのローカライズ {#localizing-collapsed-categories-queues-and-processes}

AEM Forms workspace は、カテゴリ、キュー、プロセスのヘッダーを表示するために画像を使用します。 これらのヘッダをローカライズするには、開発パッケージが必要です。開発パッケージの作成について詳しくは、 [AEM Forms Workspace コードを構築しています。](introduction-customizing-html-workspace.md#building-html-workspace-code)

次の手順では、新しくローカライズされた画像ファイルは&#x200B;*Categories_nw.png*、*Queue_nw.png*、および *Processes_nw.png* であると想定しています。画像の推奨幅は 19px です。

>[!NOTE]
>
>お使いのブラウザのブラウザ言語ロケールコードを検索するには、次のようにします。次を開きます： `https://[server]:[port]/lc/libs/ws/Locale.html`.

![collapsing_panels_image](assets/collapsing_panels_image.png)

次の手順を実行して画像をローカライズします。

1. WebDAV クライアントを使用して、画像ファイルを */apps/ws/images* フォルダーに配置します。
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

1. 次に示すセマンティックの変更をすべて実行します： [Workspace のカスタマイズ](/help/forms/using/introduction-customizing-html-workspace.md) 記事。
1. 次に移動： *js/runtime/utility* フォルダーに移動し、編集用に*usersession.js*ファイルを開きます。
1. 元のコードブロックに一覧表示されているコードを探して、if ステートメントに条件 *lang !== &#39;nw&#39;* を if 文に追加します。

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

API をローカライズするには、開発パッケージが必要です。 開発パッケージの作成について詳しくは、 [AEM Forms Workspace コードの構築](introduction-customizing-html-workspace.md#building-html-workspace-code).

1. [jQuery UI パッケージ](https://jqueryui.com/download/all/)をダウンロードして抽出し、*&lt;抽出された jquery UI パッケージ>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n に移動します。
1. ロケールコード nw の jquery.ui.datepicker-nw.js ファイルを apps/ws/js/libs/jqueryui にコピーして、ファイルにロケール固有の変更を行います。
1. に移動します。 `apps/ws/js` をクリックし、 `jquery.ui.datepicker-nw.js` ファイルを編集します。
1. main.js ファイルで、 `jquery.ui.datepicker-nw.js.` のエイリアスを作成するコード `jquery.ui.datepicker-nw.js` ファイル：

   ```
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. エイリアスを使用 `jqueryuidatepickernw` を含めるには `jquery.ui.datepicker-nw.js` ファイルを含める必要があります。 日付選択は次のファイルで使用されます。

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   以下のサンプルコードは、jquery.ui.datepicker-nw.js のエントリを追加する方法を示します。

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

1. 日付選択 API を使用するすべてのファイルで、デフォルトの日付選択 API の設定を変更します。日付選択 API は次のファイルで使用されます。

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
