---
title: ブランディングのカスタマイズ
seo-title: Branding Customization
description: アプリケーションアイコン、アプリケーション名、起動画像およびログインページをカスタマイズして、AEM Formsアプリに対して組織固有の明確なルックアンドフィールを提供します。
seo-description: Customize the application icon, application name, launch images, and login page to provide a distinct organization-specific look and feel to AEM Forms app.
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
exl-id: 5c5cdfe6-37f2-45c7-b679-23e3592842b2
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 46%

---

# ブランディングのカスタマイズ {#branding-customization}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

アプリケーションアイコン、アプリケーション名、起動画像およびログインページをカスタマイズして、AEM Formsアプリに組織固有の明確な外観を提供することができます。 例えば、画像を変更して、組織のロゴを使用できます。 AEM Forms アプリケーションは次のカスタマイズをサポートしています。

* アプリケーションアイコンと起動画像のカスタマイズ
* アプリ名のカスタマイズ
* ログインページの画像のカスタマイズ
* アプリメニューのロゴのカスタマイズ

## アイコンと起動画像のカスタマイズ {#customizing-icon-and-launch-images}

次の手順を実行して、AEM Formsアプリのデフォルトのアプリアイコンと起動画像をカスタマイズします。

>[!NOTE]
>
>すべてのアイコンと画像に対して、ノンインターレースの PNG 形式を使用します。

### アイコンと起動画像をカスタマイズするには {#to-customize-icon-and-launch-images}

#### iOS {#for-ios}

1. Xcode で `Capture.xcodeproj` プロジェクトを開きます。
1. （***アイコンのカスタマイズの場合***）キャプチャのナビゲータービューで、**[!UICONTROL キャプチャ／キャプチャ／サポートするファイル／Capture-info.plist]** に移動します。アイコンファイルの隣にあるドロップダウンをクリックします。アイコンファイル（.png）の名前を指定し、**[!UICONTROL キャプチャ／キャプチャ／リソース／アイコン]**&#x200B;でファイルをアップロードします。現在サポートされているサイズは、29 x 29、50 x 50、58 x 58、72 x 72、100 x 100、144 x 144 です。
1. （***起動画像のカスタマイズの場合***）画像のファイル名が次のいずれかであることを確認します。

   * 縦長の場合：`Default-Portrait~ipad.png` および `Default-Portrait@2x~ipad.png`
   * 横長の場合：`Default-Landscape~ipad.png` および `Default-Landscape@2x~ipad.png`

   これらをキャプチャプロジェクトにアップロードして、プロジェクト内の既存のファイルを置き換えます。

   >[!NOTE]
   >
   >画像の名前と解像度が、プロジェクトで置き換える画像と一致するようにしてください。

1. iOS デバイスまたは iOS シミュレーター上で AEM Forms アプリケーションを構築して実行します。

#### Android の場合 {#for-android}

1. アプリケーションのアイコンファイルに次のような名前を付けます。

   `ic_launcher.png`

1. 対応するアイコンファイルを次のディレクトリに配置します。

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >画像の名前と解像度が、プロジェクトで置き換える画像と一致するようにしてください。

1. AEM Formsアプリをリビルドします。

### Windows の場合 {#for-windows}

1. 次のパスのアイコンを置き換えます。

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. 次のパスにある起動画像を置き換えます。

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >画像の名前と解像度が、プロジェクトで置き換える画像と一致するようにしてください。

1. AEM Formsアプリをリビルドします。

## アプリ名のカスタマイズ {#customize-the-app-name}

### iOS {#for-ios-1}

1. Xcode で `Capture.xcodeproj` プロジェクトを開きます。
1. Capture のナビゲータービューで、**[!UICONTROL Capture／Capture／Supporting Files／InfoPlist.strings]** に移動します。

   `CFBundleDisplayName` 属性の値を、アプリに表示する名前に更新します。

1. iOS デバイスまたは iOS シミュレーター上で AEM Forms アプリケーションを構築して実行します。

   iOS 向けアプリケーションの構築について詳しくは、[Xcode プロジェクトの設定と iOS アプリケーションの構築](/help/forms/using/setup-xcode-project-build-installer.md)を参照してください。

### Android の場合 {#for-android-1}

1. 任意のテキストエディターまたは XML エディターで次の XML を開きます。

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. `app_name` キーの値を更新します。
1. AEM Formsアプリをリビルドします。

   Android 向けアプリの構築について詳しくは、 [Eclipse プロジェクトの設定と Android アプリの構築](/help/forms/using/setup-eclipse-project-build-installer.md).

### Windows の場合 {#for-windows-1}

1. 任意のテキストエディターで次の Xml を開きます。

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. `<name>...</name>` タグ内の値を更新します。
1. AEM Formsアプリをリビルドします。

   Windows 用アプリの構築について詳しくは、 [Visual Studio プロジェクトを設定し、Windows アプリを構築する](/help/forms/using/setup-visual-studio-project-build-installer.md).

## ログインページの画像のカスタマイズ {#customizing-images-on-the-login-page}

AEM Forms アプリケーションのログインページには、ロゴと背景画像があります。ロゴはログインダイアログボックスの上に配置され、背景画像はログインダイアログボックスの下に配置されます。 次の手順を実行して、ログインページのデフォルト画像をカスタマイズします。

**事前準備**

次の画像があることを確認します。

<table> 
 <tbody> 
  <tr> 
   <th><p>説明</p> </th> 
   <th><p>サイズ</p> </th> 
   <th><p>Filename</p> </th> 
  </tr> 
  <tr> 
   <td><p>Logo（ロゴ）</p> </td> 
   <td><p>72 x 72 ピクセル</p> </td> 
   <td><p>LC-logo.png</p> </td> 
  </tr> 
  <tr> 
   <td><p>背景画像（縦長）</p> </td> 
   <td><p>1280 x 989 ピクセル</p> </td> 
   <td><p>Landing_bg.jpeg</p> </td> 
  </tr> 
 </tbody> 
</table>

**Xcode を使用してログインページの画像をカスタマイズするには**

1. Xcode で `Capture.xcodeproj` プロジェクトを開きます。

1. `www/wsmobile/images` フォルダーに移動し、
1. ロゴを変更するには、デフォルトの `LC-logo.png` ファイルをカスタムの `LC-logo.png` ファイルに置き換えます。
1. 背景を変更するには、デフォルトの `Landing_bg.jpeg` ファイルをカスタムの `Landing_bg.jpeg` ファイルに置き換えます。
1. iOS デバイスまたは iOS シミュレーター上で AEM Forms アプリケーションを構築して実行します。

### Eclipse を使用してログインページの画像をカスタマイズするには {#to-customize-images-on-the-login-pages-using-eclipse}

1. Eclipse で Android プロジェクトを開きます。

1. `assets/www/wsmobile/images` フォルダーに移動し、
1. ロゴを変更するには、デフォルトの `LC-logo.png` ファイルをカスタムの `LC-logo.png` ファイルに置き換えます。
1. 背景を変更するには、デフォルトの `Landing_bg.jpeg` ファイルをカスタムの `Landing_bg.jpeg` ファイルに置き換えます。
1. Android デバイスでAEM Formsアプリをビルドして実行します。

### Visual Studio を使用してログインページの画像をカスタマイズするには {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Visual Studio で `MWSWindows.sln` プロジェクトを開きます。

1. `MWSWindows\www\wsmobile\images` フォルダーに移動し、
1. ロゴを変更するには、デフォルトの `LC-logo.png` ファイルをカスタムの `LC-logo.png` ファイルに置き換えます。
1. 背景を変更するには、デフォルトの `Landing_bg.jpeg` ファイルをカスタムの `Landing_bg.jpeg` ファイルに置き換えます。
1. Windows デバイス上で AEM Forms アプリケーションを構築して実行します。

## アプリメニューのロゴのカスタマイズ {#customizing_images_on_the_login_page-1}

AEM Formsアプリにログインしてメニューボタンをタップすると、メニューの上にロゴが表示されます。 次の手順を実行して、デフォルトのロゴをカスタマイズします。

**事前準備**

次の画像があることを確認します。

<table> 
 <tbody> 
  <tr> 
   <th><p>説明</p> </th> 
   <th><p>サイズ</p> </th> 
   <th><p>Filename</p> </th> 
  </tr> 
  <tr> 
   <td><p>Logo（ロゴ）</p> </td> 
   <td><p>72 x 72 ピクセル</p> </td> 
   <td><p>aem_icon.png</p> </td> 
  </tr> 
 </tbody> 
</table>

**Xcode を使用してログインページの画像をカスタマイズするには**

1. Xcode で `Capture.xcodeproj` プロジェクトを開きます。

1. `www/wsmobile/images` フォルダーに移動し、
1. ロゴを変更するには、デフォルトの `aem_icon.png` ファイルをカスタムの `aem_icon.png` ファイルに置き換えます。
1. iOS デバイスまたは iOS シミュレーター上で AEM Forms アプリケーションを構築して実行します。

### Eclipse を使用してログインページの画像をカスタマイズするには {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Eclipse で Android プロジェクトを開きます。

1. `assets/www/wsmobile/images` フォルダーに移動し、
1. ロゴを変更するには、デフォルトの `aem_icon.png` ファイルをカスタムの `aem_icon.png` ファイルに置き換えます。
1. Android デバイスでAEM Formsアプリをビルドして実行します。

### Visual Studio を使用してログインページの画像をカスタマイズするには {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Visual Studio で `MWSWindows.sln` プロジェクトを開きます。

1. `MWSWindows\www\wsmobile\images` フォルダーに移動し、
1. ロゴを変更するには、デフォルトの `aem_icon.png` ファイルをカスタムの `aem_icon.png` ファイルに置き換えます。
1. Windows デバイス上で AEM Forms アプリケーションを構築して実行します。
