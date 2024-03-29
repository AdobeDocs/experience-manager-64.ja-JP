---
title: AEM Forms アプリケーションのトラブルシューティング
seo-title: Troubleshoot AEM Forms app
description: AEM Formsアプリの一般的な問題と、そのトラブルシューティング方法について説明します。
seo-description: Learn about common issues with AEM Forms app and how to troubleshoot them.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
exl-id: 1e772376-d25a-4471-bf7c-5a8a8cdeb543
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 70%

---

# AEM Forms アプリケーションのトラブルシューティング {#troubleshoot-aem-forms-app}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

この記事では、AEM Formsアプリの構築中に表示される可能性のあるエラーメッセージと、それらを解決する手順について説明します。

この記事のセクションは次のとおりです。

* [iOS ユーザーの添付ファイルが失われる](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Workspace ユーザーによって送信された HTML5 フォームドラフトがポータルに表示されない](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [キャッシュされていない HTML5 フォームを AEM Forms アプリケーションに読み込むことができない](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms が Windows で同期されない](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Gradle のサポートされていないバージョン](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle と Android Gradle プラグインの互換性の問題](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS ユーザーの添付ファイルが失われる {#attachment-loss-for-ios-users}

OSGi 上のAEM Formsと同期するように設定されたiOS用AEM Formsアプリは、フィールドレベルの添付ファイルのみをサポートします。 すべての添付ファイルに一意の名前を付ける必要があります。 複数の添付ファイルに同じ名前が付いている場合、1 つの添付ファイルのみが保持され、同じ名前が付いている他のすべての添付ファイルは失われます。iOS デバイスのユーザーがデータを損失するのを回避するには、次の手順を実行します。

1. 接続したサーバーで、**Adobe Experience Manager／ツール／操作／web コンソール**&#x200B;に移動します。
1. 「**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 web チャネルの設定]**」を検索してクリックします。
1. [!UICONTROL アダプティブフォームおよびインタラクティブ通信 web チャネルの設定]ダイアログで、「**ファイル名を一意にする**」を有効にします。

   「**ファイル名を一意にする**」設定が無効になっている場合、複数の添付ファイルが含まれているアダプティブフォームを送信しようとするとデータが失われます。

1. 「**保存**」をクリックします。

## Workspace ユーザーによって送信された HTML5 フォームドラフトがポータルに表示されない {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

「**ドラフトとして保存**」HTML レンダリングプロファイルを使用する AEM Forms アプリケーションで HTML5 フォームが有効になっている場合、保存されたドラフトは Workspace ユーザーには表示されません。Workspace ユーザーから送信された HTML5 フォームの保存済みドラフトをポータルに表示するには、次の手順を実行します。

1. CRXDE を開いて管理者の資格情報でログインします。

   URL：`https://<server>:<port>/lc/crx/de/index.jsp`

1. CRXDE のルートパスにある「アクセス制御」の「アクセス制御リスト」で、**+** をクリックします。
1. 内 **新しいエントリの追加** ダイアログで、「プリンシパル」フィールドのグループ検索ボタンをクリックします。
1. プリンシパルを選択ダイアログの「名前」フィールドで、`PERM_WORKSPACE_USER` と入力し、「**検索**」をクリックします。
1. プリンシパルを選択ダイアログで `PERM_WORKSPACE_USER` グループを選択し、「**OK**」をクリックします。
1. 新しいエントリを追加ダイアログの「プリンシパル」フィールドで、`PERM_WORKSPACE_USER` グループが選択された状態になります。

   ユーザーグループの `jcr:read` 権限を有効にします。

1. 「**OK**」をクリックします。

## キャッシュされていない HTML5 フォームを AEM Forms アプリケーションに読み込むことができない {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

AEM Formsアプリが古いバージョンのAEM Formsサーバーに接続されている場合、キャッシュされていないHTML5 forms をAEM Formsアプリに読み込めません。

問題を解決するには、以下の手順を実行します。

1. オーサーインスタンスで、**Adobe Experience Manager／ツール／Workspace アプリオフラインサービスを設定／今すぐ設定**&#x200B;に移動します。
1. **Workspace アプリオフラインサービス**&#x200B;のページで、「**手動のリソースキャッシュ**」をクリックします。

   URL：https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. 「**手動のリソースキャッシュ**」タブで、「**+**」ボタンをクリックして CRX パスを追加します。
1. 「**新しいリソースを追加**」フィールドで、/etc.clientlibs/fd/xfaforms/I18N/en_US.js と入力して、「**追加**」をクリックします。
1. 「**保存**」をクリックします。

## AEM Forms が Windows で同期されない {#aem-forms-do-not-sync-on-windows}

Windows 版AEM Formsアプリでは、フォームのパスまたはそのリソースのいずれかに 256 文字以上が含まれている場合、フォームは接続されたサーバーと同期されません。

文字数を 256 文字未満に減らすには、フォームとそのリソースのパスを変更します。

## Gradle のサポートされていないバージョン {#unsupported-version-of-gradle}

**エラーメッセージ：** The project is using an unsupported version of Gradle.（プロジェクトは Gradle のサポート対象でないバージョンを使用しています。）

Android Studio でAEM Formsアプリを作成すると、エラーメッセージが表示されます。 この問題は、システムでサポートされている Gradle のサポートされていないバージョンが原因で発生します。

**解決策：**「**Fix Gradle wrapper and re-import project**」（Gradle のラッパーを修正してプロジェクトを再度インポート）をクリックして問題を解決します。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle と Android Gradle プラグインの互換性の問題 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**エラーメッセージ：** The versions of the Android Gradle plugin and Gradle are not compatible.（Android Gradle プラグインと Gradle のバージョンには互換性がありません。）

Android Studio のユーザーインターフェイスで、**Build** メニューから「**Build APK**」オプションを選択すると、このエラーメッセージが表示されます。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**解決策：** **Gradle Scripts** ／ **gradle-wrapper.properties** ファイルを開き、**distributionUrl**&#x200B;プロパティを編集します。

例えば、Android Studio コンソールでは Gradle のバージョンを 3.5 にダウングレードすることをお勧めします。そのバージョンを **gradle-wrapper.properties** ファイルの **distributionUrl**&#x200B;で編集します。

**Build**／**Build APK** を再び選択し、 エラーを解決して .apk ファイルを生成します。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
