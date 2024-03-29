---
title: AEM Forms Android アプリケーションの構築
seo-title: Build the AEM Forms Android app
description: Android Studio プロジェクトを設定し、Android 用AEM Formsアプリ用の.apk ファイルを構築する手順です
seo-description: Steps to set up the Android Studio project and build the .apk file for the AEM Forms app for Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
exl-id: dbeed62e-eff1-47bc-b6da-cad543295170
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 75%

---

# AEM Forms Android アプリケーションの構築 {#build-the-aem-forms-android-app}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms Android アプリケーションを構築するには、以下の手順を、記載されている順序で実行します。

1. [AEM Forms アプリケーションのソースコードパッケージのダウンロード](#download-android-zip)
1. [環境変数の設定](#set-environment-variable-android)
1. [標準的な AEM Forms アプリケーションの構築](#set-up-the-xcode-project)

## AEM Forms アプリケーションのソースコードパッケージのダウンロード {#download-android-zip}

AEM Forms アプリケーションのソースコードパッケージは `adobe-lc-mobileworkspace-src-<version>.zip` アーカイブを参照します。このアーカイブにはカスタムの AEM Forms アプリケーションを構築するために必要なソースコードが含まれています。アーカイブは、「ソフトウェア配布」で入手できる `adobe-aemfd-forms-app-src-pkg-<version>.zip` パッケージに含まれています。

`adobe-aemfd-forms-app-src-pkg-<version>.zip` ファイルをダウンロードするには、次の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 内 **[!UICONTROL フィルター]** セクション：
   1. 選択 **[!UICONTROL Forms]** から **[!UICONTROL 解決策]** 」ドロップダウンリストから選択できます。
   2. パッケージのバージョンとタイプを選択します。「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージの名前をタップし、「**[!UICONTROL EULA 利用規約に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。
1. ソースコードアーカイブをダウンロードするには、ブラウザーで **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zipp** を開きます。Android アプリケーションの .zip ファイルがお使いのデバイスにダウンロードされます。
1. ローカルファイルシステム上のフォルダーに .zip ファイルの内容を解凍します。例： *C:\Folder Structure\adobe-lc-mobileworkspace-src-2.4.20*

次の画像は、`adobe-lc-mobileworkspace-src-<version>.zip\android` フォルダーの構造を示しています。

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 環境変数の設定 {#set-environment-variable-android}

AEM Formsアプリのビルドプロセスを開始する前に、次の環境変数を設定します。

* JAVA_HOME 環境変数を、ローカル・ファイル・システム上の JDK ソフトウェアの場所に設定します。 例： C:\Program Files\Java\jdk1.8.0_181
* `ANDROID_SDK_ROOT` システム環境変数を、Android の SDK の場所に設定します。例： C:\Users\username\AppData\Local\Android\Sdk
* `Path` システム環境変数を、Android の platform-tools フォルダーおよび tools フォルダーに含めるように設定します。例：C:\Users\username\AppData\Local\Android\Sdk\platform-tools and C:\Users\username\AppData\Local\Android\Sdk\tools

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

adobe-lc-mobileworkspace-src-&lt;version>.zip ファイルをローカルファイルシステムに保存して環境変数を設定したら、次のいずれかのオプションを使用して、標準的な AEM Forms Android アプリケーションを構築します。

* [Android Studio を使用した AEM Forms アプリケーションの構築](#using-android-studio)
* [Android Studio を使用した .apk ファイルの生成](#generate-apk-android-studio)

### Android Studio を使用した AEM Forms アプリケーションの構築 {#using-android-studio}

Android Studio を使用してAEM Formsアプリを構築するには、次の手順を実行します。

1. 自分のマシンで Android Studio アプリケーションを起動します。
1. 「**Open an existing Android Studio project**」をクリックします。既存のプロジェクトを開くダイアログボックスが自動的に表示されない場合は、**File**／**Open** を選択します。
1. ローカルファイルシステム上の *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* に移動し、「**OK**」をクリックします。

    「**android**」オプションが左側のペインに表示されます。

   ![android_folder_studio](assets/android_folder_studio.png)

1. 左側のペインで「**android**」を選択し、**Run**／**Run &#39;android&#39;** をクリックします。
1. Select Deployment Target ダイアログボックスの「Connected Devices」セクションで Android デバイスを選択し、「OK」をクリックします。

   開発環境を正しく構築すると、アプリケーションをカスタマイズできるようになります。アプリケーションをカスタマイズする場合は、次の記事を参照してください。

   * [ブランディングのカスタマイズ](/help/forms/using/branding-customization.md)
   * [テーマのカスタマイズ](/help/forms/using/theme-customization.md)
   * [ジェスチャのカスタマイズ](/help/forms/using/gesture-customization.md)

   アプリに適切なカスタマイズを適用したら、配布用に.apk ファイルを生成できます。

### Android Studio を使用した .apk ファイルの生成 {#generate-apk-android-studio}

Android Studio を使用して.apk ファイルを生成するには、次の手順を実行します。

1. 自分のマシンで Android Studio アプリケーションを起動します。
1. 「**Open an existing Android Studio project**」を選択します。既存のプロジェクトを開くダイアログボックスが自動的に表示されない場合は、**File**／**Open** を選択します。
1. ローカルファイルシステム上の *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* に移動し、「**OK**」をクリックします。

    「android」オプションが左側のペインに表示されます。

1. **Build**／**Build APK** を選択し、.apk ファイルを生成します。

   オプションで、**Build**／**Generate Signed APK** を選択し、.apk ファイルの[署名バージョン](https://developer.android.com/studio/publish/app-signing)を生成することもできます。

## Android Debug Bridge の使用 {#build-android-debug-bridge}

.apk ファイルの生成後、次のコマンドを実行して、[Android Debug Bridge](https://developer.android.com/tools/help/adb.html) を使用して Android デバイスにアプリケーションをインストールします。

**Windows ユーザー：** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Mac ユーザー：** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
