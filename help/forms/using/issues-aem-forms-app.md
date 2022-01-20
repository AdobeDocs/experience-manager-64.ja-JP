---
title: AEM Forms アプリケーションのトラブルシューティング
seo-title: Troubleshoot AEM Forms app
description: 'AEM Forms アプリケーションの一般的な問題と、そのトラブルシューティングについて説明します。 '
seo-description: Learn about common issues with AEM Forms app and how to troubleshoot them.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
exl-id: 1e772376-d25a-4471-bf7c-5a8a8cdeb543
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 55%

---

# AEM Forms アプリケーションのトラブルシューティング {#troubleshoot-aem-forms-app}

この記事では、AEM Forms アプリケーションの構築中に表示される可能性のあるエラーメッセージとその解決方法について説明します。

この記事のセクションは次のとおりです。

* [iOS ユーザーの添付ファイルが失われる](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Workspace ユーザーによって送信された HTML5 フォームドラフトがポータルに表示されない](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [キャッシュされていない HTML5 フォームを AEM Forms アプリケーションに読み込むことができない](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms が Windows で同期されない](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Gradle のサポートされていないバージョン](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle と Android Gradle プラグインの互換性の問題](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS ユーザーの添付ファイルが失われる {#attachment-loss-for-ios-users}

OSGi 上の AEM Forms と同期するように設定された iOS 用の AEM Forms アプリケーションは、フィールドレベルの添付ファイルのみをサポートします。すべての添付ファイルには一意の名前が付いている必要があります。複数の添付ファイルに同じ名前が付いている場合、1 つの添付ファイルのみが保持され、同じ名前が付いている他のすべての添付ファイルは失われます。iOS デバイスのユーザーがデータを損失するのを回避するには、次の手順を実行します。

1. 接続されているサーバーで、に移動します。 **Adobe Experience Manager /ツール/操作/ Web コンソール**.
1. 検索とクリック **[!UICONTROL アダプティブフォームとインタラクティブ通信の Web チャネル設定]**.
1. 内 [!UICONTROL アダプティブフォームとインタラクティブ通信の Web チャネル設定] ダイアログ、有効 **ファイル名を一意にする**.

   If **ファイル名を一意にする** を無効にすると、複数の添付ファイルを持つアダプティブフォームを送信しようとすると、ユーザーはデータを失います。

1. 「**保存**」をクリックします。

## Workspace ユーザーによって送信された HTML5 フォームドラフトがポータルに表示されない {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

AEM Formsアプリで有効なHTML5 フォームの場合： **ドラフトとして保存** HTMLレンダリングプロファイル：保存されたドラフトは、Workspace ユーザーには表示されません。 Workspace ユーザーがポータル上で送信したHTML5 フォームの保存済みドラフトを表示するには、次の手順を実行します。

1. CRXDE を開いて管理者の資格情報でログインします。

   URL：`https://<server>:<port>/lc/crx/de/index.jsp`

1. CRXDE のルートパスにある「アクセス制御」の「アクセス制御リスト」で、**+** をクリックします。
1. **新しいエントリを追加**&#x200B;ダイアログで、「プリンシパル」フィールドのグループ検索ボタンをクリックします。
1. プリンシパルを選択ダイアログの「名前」フィールドに、「 `PERM_WORKSPACE_USER` をクリックし、 **検索**.
1. 選択 `PERM_WORKSPACE_USER` 「プリンシパルを選択」ダイアログでグループ化し、 **OK**.
1. 新しいエントリを追加ダイアログの「プリンシパル」フィールドで、`PERM_WORKSPACE_USER` グループが選択された状態になります。

   有効にする `jcr:read` ユーザーグループの権限。

1. 「**OK**」をクリックします。

## キャッシュされていない HTML5 フォームを AEM Forms アプリケーションに読み込むことができない {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

AEM Forms アプリケーションが古いバージョンの AEM Forms サーバーに接続している場合、キャッシュされていない HTML5 フォームを AEM Forms アプリケーションに読み込むことができません。

問題を解決するには、以下の手順を実行します。

1. オーサーインスタンスで、に移動します。 **Adobe Experience Manager /ツール/ Workspace アプリオフラインサービスを設定/今すぐ設定**.
1. In **Workspace アプリオフラインサービス** ページ、クリック **手動のリソースキャッシュ**.

   URL：https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. 内 **手動のリソースキャッシュ** タブで、 **+** ボタンを使用して CRX パスを追加します。
1. 内 **新しいリソースを追加** フィールド、タイプ：/etc.clientlibs/fd/xfaforms/I18N/en_US.jsをクリックし、 **追加**.
1. 「**保存**」をクリックします。

## AEM Forms が Windows で同期されない {#aem-forms-do-not-sync-on-windows}

Windows の AEM Forms アプリケーションでは、フォームまたはそのリソースのいずれかへのパスが 256 文字以上の場合、フォームは接続されたサーバーと同期されません。

フォームとそのリソースへのパスを変更して、文字数を 256 文字よりも少なくしてください。

## Gradle のサポートされていないバージョン {#unsupported-version-of-gradle}

**エラーメッセージ：** このプロジェクトは Gradle のサポートされていないバージョンを使用しています。

Android Studio で AEM Forms アプリケーションを構築すると、エラーメッセージが表示されます。この問題は、システムでサポートされる Gradle のサポート対象でないバージョンにより発生します。

**解像度：** クリック **Gradle ラッパーを修正し、プロジェクトを再インポート** をクリックして問題を解決します。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle と Android Gradle プラグインの互換性の問題 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**エラーメッセージ：** Android Gradle プラグインと Gradle のバージョンに互換性がありません。

「 **APK の構築** オプションを **ビルド** Android Studio ユーザーインターフェイスのメニュー

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**解像度：** 開く **Gradle スクリプト** > **gradle-wrapper.properties** ファイルと編集 **distributionUrl** プロパティ。

例えば、Android Studio コンソールでは、Gradle のバージョンを 3.5 にダウングレードすることをお勧めします。 **distributionUrl**/**gradle-wrapper.properties** ファイル。

選択 **ビルド** > **APK の構築** エラーを解決し、 .apk ファイルを生成する場合にもう一度使用します。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
