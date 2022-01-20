---
title: Android Studio プロジェクトのセットアップと Android アプリの作成
seo-title: Set up the Android studio project and build the Android app
description: Android Studio プロジェクトのセットアップ手順と AEM Forms アプリケーションのインストーラーの作成手順
seo-description: Steps to set up the Android Studio project and build the installer for the AEM Forms app
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
exl-id: a797ec42-e6bf-457e-91d7-0430b4671a68
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 62%

---

# Android Studio プロジェクトのセットアップと Android アプリの作成 {#set-up-the-android-studio-project-and-build-the-android-app}

ここでは、バージョン 6.3.1.1 移行の AEM Forms アプリケーションを作成する手順について説明します。AEM Forms App 6.3 のソースコードからアプリを構築する場合は、 [Eclipse プロジェクトの設定と Android™アプリの構築](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。このソースには、カスタムの AEM Forms アプリケーションを構築するためのすべてのコンポーネントが含まれています。ソースコードアーカイブ `adobe-lc-mobileworkspace-src-<version>.zip` は、 `adobe-aemfd-forms-app-src-pkg-<version>.zip` ソフトウェア配布のパッケージ。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 また、 **[!UICONTROL ダウンロードを検索]** 」オプションを使用して結果をフィルターします。
1. 使用するオペレーティングシステムに適したパッケージ名をタップし、「 」を選択します。 **[!UICONTROL 使用許諾契約書に同意する]**&#x200B;をタップし、 **[!UICONTROL ダウンロード]**.
1. [パッケージマネージャー](https://docs.adobe.com/content/help/ja/experience-manager-65/administering/contentmanagement/package-manager.html)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択し、 **[!UICONTROL インストール]**.

次の画像は、 `adobe-lc-mobileworkspace-src-<version>.zip`.

![Zip 形式に圧縮された Android™ ソースの抽出されたコンテンツ](assets/mws-content-1.png)

次の画像は、 `android`フォルダーを `src`フォルダー。

![src 内の android フォルダーのディレクトリ構造](assets/android-folder.png)

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

1. Android™ Studio でプロジェクトを設定し、署名 ID を指定するには、以下の手順を実行します。

   設定済みの Android™ Studio がインストールされているマシンにログインします。

1. ダウンロードした `adobe-lc-mobileworkspace-src-<version>.zip` アーカイブ先：

   **MACユーザー向け**: `[User_Home]/Projects`

   **Windows®ユーザーの場合**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Windows® の場合は、Android プロジェクトをシステムドライブに保存することをお勧めします。

1. アーカイブを次のディレクトリに展開します。

   **MACユーザー向け**: `[User_Home]/Projects/[your-project]`

   **Windows®ユーザーの場合**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >抽出した Android プロジェクトを Android Studio に読み込む前に、そのプロジェクトをシステムドライブに保存することをお勧めします。

1. Android™ Studio を起動します。

   **MACユーザー向け**:を更新します。 `local.properties` ファイルが `[User_Home]/Projects/[your-project]/android` フォルダーとポイント `sdk.dir` 変数を `SDK` デスクトップ上の場所

   **Windows®ユーザーの場合**:を更新します。 `local.properties` ファイルが `%HOMEPATH%\Projects\[your-project]\android` フォルダーとポイント `sdk.dir` 変数を `SDK` デスクトップ上の場所

1. クリック**[!UICONTROL 完了]**プロジェクトを構築します。

    プロジェクトが ADT Project Explorer で使用できるようになります。 

   ![アプリケーション構築後の eclipse プロジェクト](assets/eclipsebuildmws.png)

1. Android™ Studio で、「**[!UICONTROL Import Project (Eclipse ADT, Gradle, Etc.)]**」を選択します。
1. プロジェクトエクスプローラーで、でビルドするプロジェクトのルートディレクトリを選択します。 **ルートディレクトリ** テキストボックス：

   **Macユーザーの場合：** [User_Home]/Projects/MobileWorkspace/src/android

   **Windows®ユーザーの場合：** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. プロジェクトの読み込みが完了すると、ポップアップが表示されます。このポップアップには、Android™ プラグインの Gradle を更新するためのオプションが表示されます。要件に応じて、適切なボタンをクリックします。

   ![このプロジェクトに対する dontreemindame](assets/dontremindmeagainforthisproject.png)

1. Gradle が正しく作成されると、以下の画面が表示されます。適切なデバイスまたはエミュレーターをシステムに接続し、 **[!UICONTROL Android™を実行します。]**.

   ![小骨底](assets/gradleconsole.png)

1. Android™ Studio に、接続デバイスと使用可能なエミュレーターが表示されます。アプリケーションを実行するデバイスを選択して「**OK**」をクリックします。

   ![connecteddevice](assets/connecteddevice.png)

プロジェクトの作成が完了したら、Android™ Debug Bridge または Android™ Studio を使用して、アプリケーションをインストールすることができます。

### Android™ Debug Bridge を使用する {#andriod-debug-bridge}

[Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) で以下のコマンドを使用して、アプリケーションを Android™ デバイスにインストールすることができます。

**MACユーザー向け**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Windows®ユーザーの場合**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
