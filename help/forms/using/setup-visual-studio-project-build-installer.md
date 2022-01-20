---
title: Visual Studio プロジェクトの設定と Windows アプリケーションの構築
seo-title: Set up the Visual Studio project and build the Windows app
description: Visual Studio プロジェクトを設定し、AEM Forms Windows モバイルデバイスアプリを構築する方法について学びます。
seo-description: Learn how to set up a Visual Studio project to build the AEM Forms Windows mobile device app.
uuid: 0a72387a-d920-4f66-8983-d500ef0ecd90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 85048fe4-ca1b-41fa-8e19-6eeb8dd09962
exl-id: ae0463de-271f-47c0-b947-f6d149ded8ab
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 68%

---

# Visual Studio プロジェクトの設定と Windows アプリケーションの構築 {#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。このソースには、カスタムワークスペースアプリケーションを構築するためのすべてのコンポーネントが含まれています。ソースコードアーカイブ `adobe-lc-mobileworkspace-src-<version>.zip`は、 `adobe-aemfd-forms-app-src-pkg-<version>.zip` ソフトウェア配布のパッケージ。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行します。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 また、 **[!UICONTROL ダウンロードを検索]** 」オプションを使用して結果をフィルターします。
1. 使用するオペレーティングシステムに適したパッケージ名をタップし、「 」を選択します。 **[!UICONTROL 使用許諾契約書に同意する]**&#x200B;をタップし、 **[!UICONTROL ダウンロード]**.
1. [パッケージマネージャー](https://docs.adobe.com/content/help/ja/experience-manager-65/administering/contentmanagement/package-manager.html)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択し、 **[!UICONTROL インストール]**.

1. ソースコードアーカイブをダウンロードするには、を開きます。 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` ブラウザーに表示されます。

   ソースパッケージがお使いのデバイスにダウンロードされます。

次の画像は、 `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content-2](assets/mws-content-2.png)

次の画像は、 `windows` フォルダーを `src` フォルダー。

![win-dir](assets/win-dir.png)

## 環境の設定 {#setting-up-the-environment}

Windows デバイスの場合、以下の環境が必要です。

* Microsoft Windows 8.1 または Windows 10
* Microsoft Visual Studio 2015
* Apache Cordova 向け Microsoft Visual Studio Tools

## AEM Forms アプリケーション向けの Visual Studio プロジェクトの設定 {#setting-up-visual-studio-project-for-aem-forms-app}

Visual Studio で AEM Forms アプリケーションのプロジェクトを設定するには、以下の手順を実行します。

1. を `adobe-lc-mobileworkspace-src-<version>.zip` アーカイブ先 `%HOMEPATH%\Projects` Visual Studio 2015 がインストールおよび構成された Windows 8.1 または Windows 10 デバイスのフォルダ。
1. アーカイブを `%HOMEPATH%\Projects\MobileWorkspace` ディレクトリ。
1. 次に移動： `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` ディレクトリ。
1. を開きます。 `CordovaApp.sln` Visual Studio 2015 を使用してファイルを作成し、AEM Formsアプリケーションの作成に進みます。

## AEM Forms アプリケーションの構築 {#build-aem-forms-app}

AEM Forms アプリケーションを構築しデプロイするには、次の手順を実行します。

>[!NOTE]
>
>AEM Forms アプリケーション向けに Windows ファイルシステムに保存されるデータは、暗号化されていません。Windows BitLocker Drive Encryption などのサードパーティ製ツールを使用して、ディスクデータを暗号化することをお勧めします。

1. Visual Studio Standard ツールバーで、 **リリース** を選択します。

1. 使用しているプラットフォームに応じて Windows-AnyCPU、Windows-x64、または Windows-x86 を選択します。Windows-AnyCPU を選択することをお勧めします。
1. Visual Studio ソリューションエクスプローラで、プロジェクトを右クリックします。 **CordovaApp.Windows** を選択し、 **ストア/アプリパッケージを作成**.

   ![createapppackages](assets/createapppackages.png)

   アプリパッケージの作成ウィザードが表示されます。

   CordovaApp.Windows_3.0.2.0_anycpu.appx インストーラーファイルが platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test ディレクトリに作成されます。

   エラーが発生した場合 `Retarget to windows 8.1 required`をクリックし、エラーを右クリックし、ポップアップメニューで「 」を選択します。 **Windows 8.1 にリターゲット**.

   ![retarget-solution](assets/retarget-solution.png)

1. アプリパッケージの作成ウィザードで、アプリを Windows ストアにアップロードするかどうか選択し、「**次へ**」をクリックします。

   ![createapppackagewizard1](assets/createapppackageswizard1.png)

1. 必要に応じて、バージョンやアプリのビルドの出力場所などのパラメーターを変更します。

   ![createapppackagewizard2](assets/createapppackageswizard2.png)

1. プロジェクトのビルド後に、以下のプログラムを使用してアプリをインストールすることができます。

   * Windows PowerShell
   * Visual Studio

   この `.appx` パッケージを正常にインストールするには、次の項目が必要です。

   1. WinJS ライブラリ
   1. WinJS のパッケージに、自己署名証明書または VeriSign などの信頼できる機関によって署名された公開証明書が付帯していることを確認してください。
   1. 開発者用のライセンス

   Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test ディレクトリには、4 つの主要なコンポーネントが含まれています。

   1. `.appx` file
   1. 証明書（現在、Apache Cordova による自己署名証明書です）
   1. Dependency フォルダー
   1. PowerShell ファイル（.ps1 の拡張子）



## Windows PowerShell によるアプリのデプロイ {#deploying-an-app-using-windows-powershell}

Windows デバイスにアプリケーションをインストールするには、以下の 2 つの方法があります。

### 開発者用のライセンスを取得する方法 {#by-acquiring-the-developer-license}

1. PowerShell ファイル ( `Add-AppDevPackage.ps1)`を選択します。 **PowerShell で実行**.

1. 開発者用のライセンスを取得するように求めるセットアップ画面が表示されます。Microsoft アカウントの資格情報を使用して、開発者用のライセンスを取得します。

   このライセンスは 30 日間有効です。無料で更新することができます。

1. 開発者用のライセンスを取得すると、セットアップでシステムに自己署名証明書がインストールされ、アプリケーションが正常にインストールされます。

### 企業の所有するデバイスを使用する方法 {#by-using-enterprise-owned-devices}

企業のエンタープライズドメインに加入している企業の所有するデバイスの場合は、開発者用のライセンスを取得する必要はありません。

企業の所有するデバイスでは、Professional Edition または Enterprise Edition の Windows が使用されています。

Microsoft では VeriSign などの信頼できる機関が発行した公開証明書をインストールすることを推奨しています。

アプリをデプロイするには：

* デバイスが企業のドメインに参加していることを確認します。
* グループポリシー設定を有効にします。

**グループポリシー設定を有効にするには：**

1. デバイスで、を実行します。 `gpedit.msc`.
1. **コンピューターの構成／管理用テンプレート／Windows コンポーネント／アプリケーションパッケージの展開**&#x200B;に移動します。
1. 「**信頼できるすべてのアプリケーションのインストールを許可する**」を右クリックします。
1. 「**編集**」をクリックし、「**有効**」を選択します。

1. 「**OK**」をクリックします。

次の手順で Visual Studio によって生成された PowerShell スクリプトを編集し、開発者用のライセンスを取得しないように設定します。

PowerShell スクリプトで、変数を設定します。 `$NeedDeveloperLicense = $false`.

ドメインに加入していないデバイスの場合は、製品のアクティベーションキーのサイドローディングが必要です。アクティベーションキーは Windows 販売店で購入することができます。

グループポリシーが存在せず、エンタープライズのサイドローディングが許可されていない Windows 8.1 Home Edition の場合は、エンタープライズドメインに加入することはできません。Windows 8.1 Home Edition にアプリケーションリをデプロイするには、開発者用のライセンスを使用してください。

詳しくは、[こちら](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx)をクリックしてください。

## Visual Studio によるアプリのデプロイ {#deploying-an-app-using-visual-studio}

Visual Studio を使用して Windows にアプリをインストールするには：

1. リモートデバッガーを使用してデバイスに接続します。

   詳しくは、 [リモートコンピュータで Windows ストアアプリを実行する](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine).

1. Visual Studio でアプリケーションを開き、ソリューションプラットフォームリストで Windows-x64、Windows-x86、または Windows-AnyCPU を選択して「**リモートマシン**」を選択します。
1. リモートマシンにアプリケーションがデプロイされます。
