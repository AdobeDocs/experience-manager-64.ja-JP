---
title: Android Studio プロジェクトのセットアップと Android アプリの作成
seo-title: Set up the Android studio project and build the Android app
description: Android Studio プロジェクトを設定し、AEM Formsアプリ用のインストーラーを構築する手順です
seo-description: Steps to set up the Android Studio project and build the installer for the AEM Forms app
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
exl-id: a797ec42-e6bf-457e-91d7-0430b4671a68
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 81%

---

# Android Studio プロジェクトのセットアップと Android アプリの作成 {#set-up-the-android-studio-project-and-build-the-android-app}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ここでは、バージョン 6.3.1.1 移行の AEM Forms アプリケーションを作成する手順について説明します。AEM Forms App 6.3 のソースコードを使用してアプリケーションを作成する手順については、[Eclipse プロジェクトの設定と Android™ アプリの作成](/help/forms/using/setup-eclipse-project-build-installer.md)を参照してください。

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。このソースには、カスタムの AEM Forms アプリケーションを構築するためのすべてのコンポーネントが含まれています。ソースコードアーカイブ `adobe-lc-mobileworkspace-src-<version>.zip` は、ソフトウェア配布の `adobe-aemfd-forms-app-src-pkg-<version>.zip` パッケージの一部です。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行してください。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 内 **[!UICONTROL フィルター]** セクション：
   1. 選択 **[!UICONTROL Forms]** から **[!UICONTROL 解決策]** 」ドロップダウンリストから選択できます。
   2. パッケージのバージョンとタイプを選択します。「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージの名前をタップし、「**[!UICONTROL EULA 利用規約に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して、**[!UICONTROL インストール]**&#x200B;をクリックします。

次の画像は、`adobe-lc-mobileworkspace-src-<version>.zip` から抽出した内容を示しています。

![ZIP 形式に圧縮された Android™ ソースの抽出されたコンテンツ](assets/mws-content-1.png)

次の画像は、`src`フォルダー内の `android`フォルダーのディレクトリ構造を示しています。

![src 内の Android フォルダーのディレクトリ構造](assets/android-folder.png)

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

1. 次の手順を実行して、Android™ Studio でプロジェクトを設定し、署名 ID を指定します。

   Android™ Studio がインストールおよび設定されているマシンにログインします。

1. ダウンロードした `adobe-lc-mobileworkspace-src-<version>.zip` アーカイブを次の場所にコピーします。

   **Mac ユーザーの場合**：`[User_Home]/Projects`

   **Windows®ユーザーの場合**：`%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Windows® の場合は、Android プロジェクトをシステムドライブに保存することをお勧めします。

1. アーカイブを次のディレクトリに展開します。

   **Mac ユーザーの場合**：`[User_Home]/Projects/[your-project]`

   **Windows® ユーザーの場合**：`%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >抽出した Android プロジェクトを Android Studio にインポートする前に、そのプロジェクトをシステムドライブに保存することをお勧めします。

1. Android™ Studio を起動します。

   **Mac ユーザーの場合**：`[User_Home]/Projects/[your-project]/android` フォルダー内の `local.properties` ファイルを更新用に開き、デスクトップ上の `SDK` の場所を指すように `sdk.dir` 変数を編集します。

   **Windows® ユーザーの場合**：`%HOMEPATH%\Projects\[your-project]\android` フォルダー内の `local.properties` ファイルを更新用に開き、デスクトップ上の `SDK` の場所を指すように `sdk.dir` 変数を編集します。

1. クリック**[!UICONTROL 完了]**プロジェクトを構築します。

   プロジェクトが ADT Project Explorer で使用できるようになります。 

   ![アプリケーション構築後の Eclipse プロジェクト](assets/eclipsebuildmws.png)

1. Android™ Studio で、**[!UICONTROL Import Project (Eclipse ADT, Gradle, Etc.)]** を選択します。
1. プロジェクトエクスプローラーの「**Root Directory**」テキストボックスで、作成するプロジェクトのルートディレクトリを選択します。

   **Mac ユーザーの場合：** [User_Home]/Projects/MobileWorkspace/src/android

   **Windows® ユーザーの場合：** %HOMEPATH%¥Projects¥MobileWorkspace¥src¥android

1. プロジェクトが読み込まれると、Android™プラグイン Gradle を更新するためのオプションがポップアップ表示されます。 必要に応じて、適切なボタンをクリックします。

   ![dontremindmeagainforthisproject](assets/dontremindmeagainforthisproject.png)

1. Gradle が正しく作成されると、以下の画面が表示されます。適切なデバイスまたはエミュレーターをシステムに接続し、「**[!UICONTROL Android™ を実行]**」をクリックします。

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio に、接続デバイスと使用可能なエミュレーターが表示されます。アプリケーションを実行するデバイスを選択して **OK** をクリックします。

   ![connecteddevice](assets/connecteddevice.png)

プロジェクトの作成が完了したら、Android™ Debug Bridge または Android™ Studio を使用して、アプリケーションをインストールすることができます。

### Android™ Debug Bridge を使用する {#andriod-debug-bridge}

[Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) で以下のコマンドを使用して、アプリケーションを Android™ デバイスにインストールすることができます。

**Mac ユーザーの場合**：`adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Windows® ユーザーの場合**：`adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
