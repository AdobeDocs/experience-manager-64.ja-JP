---
title: Xcode プロジェクトの設定と iOS アプリケーションの構築
seo-title: Set up the Xcode project and build the iOS app
description: iOS用の標準AEM Formsアプリケーションの作成方法を説明します。
seo-description: Explains how to build standard AEM Forms app for iOS.
uuid: 33ccf014-05af-43c2-abb2-e0bd9c89ce32
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 2dec23f7-6cca-4cc9-a78a-acd23ae7da5f
exl-id: e03beca1-1a95-42c7-b20b-4a2d9eab4df9
source-git-commit: 0f4f8c2640629f751337e8611a2c8f32f21bcb6d
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 78%

---

# Xcode プロジェクトの設定と iOS アプリケーションの構築 {#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms では、AEM Forms アプリケーションの完全なソースコードを提供しています。ソースには、カスタムAEM Formsアプリを作成するためのすべてのコンポーネントが含まれています。 ソースコードアーカイブ `adobe-lc-mobileworkspace-src-<version>.zip` は、ソフトウェアディストリビューションの `adobe-aemfd-forms-app-src-pkg-<version>.zip` パッケージの一部です。

AEM Forms アプリケーションソースを入手するには、以下の手順を実行してください。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 内 **[!UICONTROL フィルター]** セクション：
   1. 選択 **[!UICONTROL Forms]** から **[!UICONTROL 解決策]** 」ドロップダウンリストから選択できます。
   2. パッケージのバージョンとタイプを選択します。「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージの名前をタップし、「**[!UICONTROL EULA 利用規約に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。

1. ソースコードアーカイブをダウンロードするには、ブラウザーで `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` を開きます。

   ソースパッケージがデバイスにダウンロードされます。

以下の画像は、`adobe-lc-mobileworkspace-src-<version>.zip` から抽出した内容を示しています。

![mws-content](assets/mws-content.png)

以下の表は、`adobe-lc-mobileworkspace-src-[version]/ios` フォルダーのコンテンツの詳細を示しています。

<table> 
 <tbody> 
  <tr> 
   <th><p>ディレクトリ</p> </th> 
   <th><p>コンテンツ</p> </th> 
  </tr> 
  <tr> 
   <td><p><code>CordovaLib</code></p> </td> 
   <td><p>PhoneGap SDK 6.4.0</p> </td> 
  </tr> 
  <tr> 
   <td><p><code>AEM Forms</code></p> </td> 
   <td><p>リソース、PhoneGap プラグイン、およびアプリケーションのメインモジュール</p> </td> 
  </tr> 
  <tr> 
   <td><p><code>AEM Forms.xcodeproj</code></p> </td> 
   <td><p>AEM Forms アプリケーション用 Xcode プロジェクト</p> </td> 
  </tr> 
  <tr> 
   <td><p><code>www</code></p> </td> 
   <td><p>AEM Forms アプリケーション プロジェクト用 HTML、CSS、画像、および JavaScript ファイル</p> </td> 
  </tr> 
 </tbody> 
</table>

コード署名と iOS プロビジョニングポータルへのデバイスの追加について詳しくは、[iOS コード署名の設定、処理、トラブルシューティング](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)を参照してください。

## 標準的な AEM Forms アプリケーションの構築 {#set-up-the-xcode-project}

1. 以下の手順を実行して、Xcode でプロジェクトを設定し、署名 ID を決定してください。

   Xcode と iOS SDK がインストールされて設定されている Mac マシンにログインします。

1. `adobe-lc-mobileworkspace-src-<version>.zip` アーカイブを、ダウンロードフォルダーから `[*User_Home*]/Projects/` にコピーします。
1. アーカイブを `[*User_Home*]/Projects/[your-project]` ディレクトリに抽出します。
1. ` [*User_Home*]/Projects/ `[プロジェクト]`/adobe-lc-mobileworkspace-src-[version]/ios`ディレクトリに移動します。
1. Xcode で `AEM Forms.xcodeproj` プロジェクトを開きます。
1. **TARGETS** の **AEM Forms** をクリックし、**AEM Forms** を選択してください。**ビルド設定**&#x200B;タブを選択し、**コード署名の資格**&#x200B;セクションの「デバッグ」フィールドと「リリース」フィールドで、以下のいずれかの操作を実行してください。

   * 標準 Mobile Workspace アプリケーションを作成するための各フィールドを未指定のままにする。
   * [セキュアな AEM Forms アプリケーション（iOS 用）の構築](/help/forms/using/building-secure-mobile-workspace-app.md)の説明に従って各フィールドを指定し、セキュアな AEM Forms アプリケーションを作成してください

1. 内 **ビルド設定** タブ、クリック **すべて** 次に、 **結合**.
1. 次の **設定** リスト、展開 **コード署名**.
1. 「**コード署名 ID**」用に、適切な署名を選択します。新しい署名を作成する方法について詳しくは、[開発プロビジョニングプロファイルの作成とダウンロード](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)を参照してください。
1. **デバッグ**、**リリース**、**任意の iOS SDK**&#x200B;に同じ署名が選択されていることを確認してください。
1. `AEM Forms-info.plist` ファイル内の次のコードを 

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   `yourserver.com` をサーバーの適切なホスト名で置き換える際に、上記のコードを以下のコードに置き換えます。

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSExceptionDomains</key>
   <dict>
   <key>yourserver.com</key>
   <dict>
   <!-Include to allow subdomains->
   <key>NSIncludesSubdomains</key>
   <true/>
   <!-Include to allow HTTP requests->
   <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
   <true/>
   <!-Include to support forward secrecy->
   <key>NSExceptionRequiresForwardSecrecy</key>
   <false/>
   <!-Include to specify minimum TLS version->
   <key>NSTemporaryExceptionMinimumTLSVersion</key>
   <string>TLSv1.1</string>
   </dict>
   </dict>
   </dict>
   ```

   >[!NOTE]
   >
   >このステップは、AEM Forms アプリケーションがアプリケーション転送セキュリティ要件に従っていないサーバーに接続する必要がある場合にのみ必要となります。

1. **プロジェクト**&#x200B;の **AEM Forms** を選択し、**コード署名 ID**、**デバッグ**、**リリース**、**任意の iOS SDK** に対して適切な署名が選択されていることを確認してください。
1. プロビジョニング済み iPad を Mac マシンに接続します。
1. **AEM Forms** プロジェクト用のプロビジョニング済みデバイスを選択します。

   ![iPad](assets/ipad.png)

   プロビジョニングされたデバイスであるiPad Air 2 が選択されます。

1. 選択 **製品** > **クリーン**.
1. 選択 **製品** > **ビルド**.

## AEM Forms アプリケーション用インストーラーの構築 {#build-the-installer-for-the-mobile-workspace-app}

Xcode プロジェクトをアーカイブして、インストーラー（.ipa ファイル）とプロパティリスト（.plist ファイル）を構築する必要があります。 プロパティリストファイルには、アプリケーションの名前やホストしているロケーションなど、ホストされているインハウスアプリケーションの設定情報が含まれます。プロパティリストファイルについての詳細は、[About Information Property List Files](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) を参照してください。

1. プロビジョニング済み iPad を Mac マシンに接続します。iPad のプロビジョニングの詳細情報については、[開発プロビジョニングプロファイルの作成とダウンロード](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html) を参照してください。
1. **AEM Forms** プロジェクト用のプロビジョニング済みデバイスを選択します。

   ![ipad-1](assets/ipad-1.png)

   プロビジョニングされたデバイスであるiPad Air 2 が選択されます。

1. 選択 **製品** > **クリーン**.
1. 選択 **製品** > **ビルド**.
1. 選択 **製品** > **アーカイブ**.
1. Organizer - Archives で、プロジェクトの最新のアーカイブを選択し、 **分布**.
1. 選択 **エンタープライズまたはアドホックデプロイメント用に保存** 配布方法として、をクリックします。 **次へ**.
1. 適切な **コード署名 ID** をクリックし、 **次へ**. クリック **許可** 署名を適用します。
1. アプリの名前を入力し、「 」を選択します。 **エンタープライズ配布用に保存**.
1. 次を提供： **アプリケーション URL** アプリの 例えば、CRX サーバーのアプリケーションをホストするには、URL`https://[*LC_host*]:[*port*]/lc/content/distribution/mobileworkspace/APP_NAME.ipa`を指定します。
1. 内 **タイトル** 「AEM Forms」を指定します。
1. クリック **保存** Xcode を閉じます。

   インストーラーファイル、`AEM Forms.ipa`、プロパティリストファイル `AEM Forms-info.plist` が指定された場所に作成されます。

1. `AEM Forms-info.plist` ファイルをエディターで開きます。
1. .ipa ファイルの URL のスペースをすべて %20 に置き換えます。
1. `AEM Forms-info.plist` ファイルを保存して閉じます。
