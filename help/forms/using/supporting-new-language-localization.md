---
title: アダプティブフォームのローカリゼーション用に新しいロケールをサポート
seo-title: Supporting new locales for adaptive forms localization
description: AEM Forms は、アダプティブフォームのローカライズ用に新しくロケールを追加できます。デフォルトでサポートされているロケールは、英語、フランス語、ドイツ語、日本語です。
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. The supported locales by default are English, French, German, and Japanese.
uuid: d4cee51b-c555-4544-9ae9-4aa8d38b2b17
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: Configuration
discoiquuid: e78f539a-109c-444c-8e52-be2260c3509f
feature: Adaptive Forms
role: Admin
exl-id: 9f0e7284-ac11-406d-8d8c-7682f1d66fff
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 87%

---

# アダプティブフォームのローカリゼーション用に新しいロケールをサポート {#supporting-new-locales-for-adaptive-forms-localization}

## ロケールの辞書について {#about-locale-dictionaries}

アダプティブフォームのローカリゼーションは、次の 2 種類のロケールの辞書に基づいています。

**フォーム固有の辞書** アダプティブフォームで使用される文字列が含まれます。 例えば、ラベル、フィールド名、エラーメッセージ、ヘルプの説明文などです。各ロケールに対して XLIFF ファイルのセットとして管理され、https://でアクセスできます`<host>`:`<port>`/libs/cq/i18n/translator.html.

**グローバル辞書** 2 つのグローバル辞書があり、AEM クライアントライブラリで JSON オブジェクトの形で管理されています。これらの辞書にはデフォルトのエラーメッセージ、12 か月の名前、通貨シンボル、日付と時間のパターンなどが含まれます。これらの辞書は CRXDe Lite の /libs/fd/xfaforms/clientlibs/I18N にあります。これらの場所では、各ロケールごと別々のフォルダーが用意されています。グローバルの辞書は頻繁に更新されることはありません。各ロケールごとに別の JavaScript ファイルを保持することで、ブラウザーによりそれらがキャッシュされるため、同一サーバー上で異なるアダプティブフォームにアクセスする際に、ネットワーク帯域幅の使用量を減らすことができます。

### アダプティブフォームのローカリゼーションの仕組み {#how-localization-of-adaptive-form-works}

アダプティブフォームがレンダリングされるときは、指定された順序で以下のパラメーターが参照され、リクエストされたロケールが識別されます。

* リクエストパラメーター `afAcceptLang`

   ユーザーのブラウザーロケールを上書きするには、 `afAcceptLang` リクエストパラメーターを使用して、ロケールを強制的に指定します。 例えば、次の URL は日本語ロケールでのフォームのレンダリングを強制します。

   `https://[*server*]:[*port*]/<*contextPath*>/<*formFolder*>/<*formName*>.html?wcmmode=disabled&afAcceptLang=ja`

* ユーザー向けに設定されるブラウザーのロケールです。これは、`Accept-Language` ヘッダーを使用したリクエストで指定されます。

* AEM のユーザー指定の言語設定です。

ロケールが識別されると、アダプティブフォームはフォームに固有の辞書を参照します。リクエストされたロケールでフォームに固有の辞書が見つからない場合、代わりに英語辞書（en）が使用されます。

リクエストされたロケールでクライアントライブラリが存在しない場合、ロケールに含まれる言語コードがクライアントライブラリに存在しないかチェックします。例えば、リクエストされたロケールが `en_ZA`（南アフリカ英語）で`en_ZA`用のクライアントライブラリが存在しない場合、アダプティブフォームは、`en`（英語）言語が存在する場合、このクライアントライブラリを使用します。ただし、どちらも存在しない場合、アダプティブフォームでは`en`ロケールの辞書が使用されます。

## サポートされていないロケールにローカリゼーションのサポートを追加する {#add-localization-support-for-non-supported-locales}

AEM Formsでは現在、英語 (en)、スペイン語 (es)、フランス語 (fr)、イタリア語 (it)、ドイツ語 (de)、日本語 (ja)、ポルトガル語 — ブラジル語 (pt-BR、中国語 —(zh-CN)、中国語 — 台湾 (zh-TW)、韓国語 (ko-KR) ロケールのアダプティブフォームコンテンツのローカライゼーションをサポートしています。

アダプティブフォーム実行時に新しいロケールのサポートを追加するには、次を参照してください。

1. [GuideLocalizationService にロケールを追加する](/help/forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [XFA クライアントライブラリをロケール用に追加する](/help/forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [アダプティブフォームのクライアントライブラリをロケール用に追加する](/help/forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [辞書のロケールサポートの追加](/help/forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [サーバーの再起動](/help/forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### Guide Localization Service へのロケールの追加 {#add-a-locale-to-the-guide-localization-service-br}

1. `https://[server]:[port]/system/console/configMgr` にアクセスします。
1. **Guide Localization Service** をクリックしてコンポーネントを編集します。
1. 追加するロケールを、サポート対象のロケールの一覧に追加します。

![GuideLocalizationService](assets/configservice.png)

### XFA クライアントライブラリをロケール用に追加 {#add-xfa-client-library-for-a-locale-br}

`etc/<folderHierarchy>` の下にカテゴリ `xfaforms.I18N.<locale>` のタイプ `cq:ClientLibraryFolder` のノードを作成し、次のファイルをクライアントライブラリに追加します。

* `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N` で定義されている `<locale>` の `xfalib.locale.Strings` を定義している **I18N.js**。

* 以下を含む **js.txt** ファイル。

```
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### アダプティブフォームのクライアントライブラリをロケール用に追加する {#add-adaptive-form-client-library-for-a-locale-br}

`etc/<folderHierarchy>` の下にタイプ `cq:ClientLibraryFolder` のノードを作成します。カテゴリは `guides.I18N.<locale>`、依存関係は `xfaforms.3rdparty`、`xfaforms.I18N.<locale>`、`guide.common` です。

クライアントライブラリに次のファイルを追加します。

* **i18n.js** は `guidelib.i18n` を定義し、`<locale>` の「calendarSymbols」、`datePatterns`、`timePatterns`、`dateTimeSymbols`、`numberPatterns`、`numberSymbols`、`currencySymbols`、`typefaces` のパターンを持つファイルです。これらは[ロケールセットの仕様](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)に記載されている XFA 仕様に従います。また、サポート対象の他のロケールがどのように定義されているか、`/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js` で確認することができます。

* **LogMessages.js** は、`/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js` で定義された `<locale>` の `guidelib.i18n.strings` と `guidelib.i18n.LogMessages` を定義します。

* 以下を含む **js.txt** ファイル。

```
i18n.js
LogMessages.js
```

### 辞書のロケールサポートの追加 {#add-locale-support-for-the-dictionary-br}

追加する `<locale>` が、`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` 以外の場合にのみ、この手順を実行してください。

1. 既に存在しない場合は、`nt:unstructured` の下に、`languages` ノード `etc` を作成します。

1. 既に存在しない場合は、複数の値を持つ文字列プロパティ `languages` をノードに追加します。
1. 既に存在しない場合は、`<locale>`デフォルトのロケール値`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr` を追加します。

1. `<locale>` を `/etc/languages` の `languages` プロパティの値に追加します。

`<locale>` は `https://[server]:[port]/libs/cq/i18n/translator.html` に表示されます。

### サーバーの再起動 {#restart-the-server}

追加したロケールを有効にするために AEM サーバーを再起動します。

## スペイン語サポートを追加する場合のサンプルライブラリ {#sample-libraries-for-adding-support-for-spanish}

スペイン語サポートを追加する場合のサンプルクライアントライブラリ

[ファイルを入手](assets/sample.zip)
