---
title: AEM Forms Android アプリケーションの構築
seo-title: Build the AEM Forms Android app
description: Android Studio プロジェクトを設定し、Android 向け AEM Forms アプリケーションの .apk ファイルを構築するための手順
seo-description: Steps to set up the Android Studio project and build the .apk file for the AEM Forms app for Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
exl-id: dbeed62e-eff1-47bc-b6da-cad543295170
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 62%

---

# AEM Forms Android アプリケーションの構築 {#build-the-aem-forms-android-app}

AEM Forms Android アプリケーションを構築するには、以下の手順を、記載されている順序で実行します。

1. [AEM Forms アプリケーションのソースコードパッケージのダウンロード](#download-android-zip)
1. [環境変数の設定](#set-environment-variable-android)
1. [標準的な AEM Forms アプリケーションの構築](#set-up-the-xcode-project)

## AEM Forms アプリケーションのソースコードパッケージのダウンロード {#download-android-zip}

AEM Formsアプリのソースコードパッケージは、 `adobe-lc-mobileworkspace-src-<version>.zip` アーカイブ。 このアーカイブにはカスタムの AEM Forms アプリケーションを構築するために必要なソースコードが含まれています。アーカイブは、 `adobe-aemfd-forms-app-src-pkg-<version>.zip`パッケージは、「ソフトウェア配布」で入手できます。

次の手順を実行して、 `adobe-aemfd-forms-app-src-pkg-<version>.zip` ファイル：

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 また、 **[!UICONTROL ダウンロードを検索]** 」オプションを使用して結果をフィルターします。
1. 使用するオペレーティングシステムに適したパッケージ名をタップし、「 」を選択します。 **[!UICONTROL 使用許諾契約書に同意する]**&#x200B;をタップし、 **[!UICONTROL ダウンロード]**.
1. [パッケージマネージャー](https://docs.adobe.com/content/help/ja/experience-manager-65/administering/contentmanagement/package-manager.html)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択し、 **[!UICONTROL インストール]**.
1. ソースコードアーカイブをダウンロードするには、を開きます。 **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** ブラウザーに表示されます。 Android アプリの.zip ファイルがお使いのデバイスにダウンロードされます。
1. ローカルファイルシステム上のフォルダーに .zip ファイルの内容を解凍します。例： *C:\Folder Structure\adobe-lc-mobileworkspace-src-2.4.20*

次の画像は、 `adobe-lc-mobileworkspace-src-<version>.zip\android`フォルダー。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 環境変数の設定 {#set-environment-variable-android}

AEM Forms アプリケーションの構築プロセスを開始する前に、次の環境変数を設定します。

* JAVA_HOME 環境変数を、ローカルファイルシステム上の JDK ソフトウェアの場所に設定します。例：C:\Program Files\Java\jdk1.8.0_181
* を `ANDROID_SDK_ROOT` システム環境変数を Android の SDK の場所に設定します。 例： C:\Users\username\AppData\Local\Android\Sdk
* `Path` システム環境変数を、Android の platform-tools フォルダーおよび tools フォルダーに含めるように設定します。例：C:\Users\username\AppData\Local\Android\Sdk\platform-tools and C:\Users\username\AppData\Local\Android\Sdk\tools

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

adobe-lc-mobileworkspace-src — を保存したら、&lt;version>ローカルファイルシステム上の.zip ファイルと、環境変数を設定し、次のいずれかのオプションを使用して、標準のAEM Forms Android アプリを構築します。

* [Android Studio を使用した AEM Forms アプリケーションの構築](#using-android-studio)
* [Android Studio を使用した .apk ファイルの生成](#generate-apk-android-studio)

### Android Studio を使用した AEM Forms アプリケーションの構築 {#using-android-studio}

Android Studio を使用して AEM Forms アプリケーションを構築するには、次の手順を実行します。

1. お使いのマシンで Android Studio アプリケーションを起動します。
1. 「**Open an existing Android Studio project**」をクリックします。既存のプロジェクトを開くダイアログボックスが自動的に表示されない場合は、**File**／**Open** を選択します。
1. ローカルファイルシステム上の *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* に移動し、「**OK**」をクリックします。

    「**android**」オプションが左側のペインに表示されます。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 選択 **android** 左側のウィンドウから、 **実行** > **「android」を実行します。**.
1. Select Deployment Target ダイアログボックスの「Connected Devices」セクションから Android デバイスを選択し、「OK」をクリックします。

    開発環境を正しく構築すると、アプリケーションをカスタマイズできるようになります。アプリケーションをカスタマイズする場合は、次の記事を参照してください。

   * [ブランディングのカスタマイズ](/help/forms/using/branding-customization.md)
   * [テーマのカスタマイズ](/help/forms/using/theme-customization.md)
   * [ジェスチャーのカスタマイズ](/help/forms/using/gesture-customization.md)

   アプリケーションを適切にカスタマイズした後、.apk ファイルを生成して配布できます。

### Android Studio を使用した .apk ファイルの生成 {#generate-apk-android-studio}

Android Studio を使用して .apk ファイルを生成するには、次の手順を実行します。

1. お使いのマシンで Android Studio アプリケーションを起動します。
1. 選択 **既存の Android Studio プロジェクトを開きます。**. 既存のプロジェクトを開くダイアログボックスが自動的に表示されない場合は、**File**／**Open** を選択します。
1. ローカルファイルシステム上の *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* に移動し、「**OK**」をクリックします。

    「android」オプションが左側のペインに表示されます。

1. **Build**／**Build APK**&#x200B;を選択し、.apk ファイルを生成します。

   オプションで、「選択」を選択します。 **ビルド** > **署名済み APK を生成** を生成する [署名済みバージョン](https://developer.android.com/studio/publish/app-signing) .apk ファイルの

## Android Debug Bridge の使用 {#build-android-debug-bridge}

.apk ファイルが生成されたら、次のコマンドを実行して、 [Android Debug Bridge](https://developer.android.com/tools/help/adb.html).

**Windows ユーザー：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Macユーザー：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
