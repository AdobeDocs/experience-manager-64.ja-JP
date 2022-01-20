---
title: Xcode プロジェクトの設定と iOS アプリケーションの構築
seo-title: Set up the Xcode project and build the iOS app
description: 標準的な AEM Forms アプリケーション（iOS 用）の構築方法を説明します。
seo-description: Explains how to build standard AEM Forms app for iOS.
uuid: 33ccf014-05af-43c2-abb2-e0bd9c89ce32
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 2dec23f7-6cca-4cc9-a78a-acd23ae7da5f
exl-id: e03beca1-1a95-42c7-b20b-4a2d9eab4df9
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 64%

---

# Xcode プロジェクトの設定と iOS アプリケーションの構築 {#set-up-the-xcode-project-and-build-the-ios-app}

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

1. ソースコードアーカイブをダウンロードするには、を開きます。 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` ブラウザーに表示されます。

   ソースパッケージがお使いのデバイスにダウンロードされます。

次の画像は、 `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

次の表に、 `adobe-lc-mobileworkspace-src-[version]/ios` フォルダー。

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

1. 以下の手順を実行して、Xcode でプロジェクトを設定し、署名 ID を決定します。

   Xcode およびiOS SDK がインストールおよび設定されているMacマシンにログインします。

1. を `adobe-lc-mobileworkspace-src-<version>.zip` ダウンロードフォルダーからにアーカイブする `[*User_Home*]/Projects/`.
1. アーカイブを `[*User_Home*]/Projects/[your-project]`ディレクトリ。
1. 次に移動： ` [*User_Home*]/Projects/ `[プロジェクト]`/adobe-lc-mobileworkspace-src-[version]/ios` ディレクトリ。
1. Xcode で `AEM Forms.xcodeproj` プロジェクトを開きます。
1. 「**TARGETS**」の「**AEM Forms**」をクリックし、**AEM Forms**」を選択します。を選択します。 **ビルド設定** タブで、 **コード署名の権限** 「 」セクション、「 Debug 」フィールドおよび「 Release 」フィールドで、次のいずれかの操作をおこないます。

   * 標準 Mobile Workspace アプリケーションを作成するための各フィールドを未指定のままにする。
   * の説明に従って、に対するフィールドを指定します。 [iOS用セキュアAEM Formsアプリの構築](/help/forms/using/building-secure-mobile-workspace-app.md) セキュアなAEM Formsアプリを構築するため。

1. 「**Build Settings**」タブで、「**All**」をクリックし、「**Combined**」をクリックします。
1. 「**Settings**」リストで、「**Code Signing**」を展開します。
1. 「**Code Signing Identity**」から、適切な署名を選択します。新しい署名の作成について詳しくは、 [開発プロビジョニングプロファイルの作成とダウンロード](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. 「**Debug**」、「**Release**」、「**Any iOS SDK**」に同じ署名が選択されていることを確認します。
1. 次のコードを `AEM Forms-info.plist` ファイル：

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
   >この手順は、AEM Formsアプリが App Transport Security の要件を満たさないサーバーに接続する必要がある場合にのみ必要です。

1. の下 **プロジェクト**&#x200B;を選択します。 **AEM Forms** をクリックし、適切な署名が **コード署名 ID**, **デバッグ**, **リリース** および **任意のiOS SDK**.
1. プロビジョニング済み iPad を Mac マシンに接続します。
1. 用のプロビジョニング済みデバイスを選択 **AEM Forms** プロジェクト。

   ![ipad](assets/ipad.png)

   プロビジョニング済みデバイスの iPad Air 2 が選択されます。

1. 「**Product**」／「**Clean**」を選択します。
1. 「**Product**」／「**Build**」を選択します。

## AEM Forms アプリケーション用インストーラーの構築 {#build-the-installer-for-the-mobile-workspace-app}

 Xcode プロジェクトをアーカイブして、インストーラー（.ipa ファイル）とプロパティリストファイル（.plist ファイル）を構築する必要があります。プロパティリストファイルには、アプリケーションの名前やホストしているロケーションなど、ホストされているインハウスアプリケーションの設定情報が含まれます。 プロパティリストファイルについての詳細は、「[情報プロパティリストファイルについて](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)」を参照してください。

1. プロビジョニングされた iPad の Mac マシンへの接続iPadのプロビジョニングについて詳しくは、 [開発プロビジョニングプロファイルの作成とダウンロード](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 用のプロビジョニング済みデバイスを選択 **AEM Forms** プロジェクト。

   ![ipad-1](assets/ipad-1.png)

   プロビジョニング済みデバイスの iPad Air 2 が選択されます。

1. 「**Product**」／「**Clean**」を選択します。
1. 「**Product**」／「**Build**」を選択します。
1. 「**Product**」／「**Archive**」を選択します。
1. Organizer - Archives で、プロジェクトの最新のアーカイブを選択し、「**Distribute**」をクリックします。
1. 「**Save for Enterprise or Ad-Hoc Deployment**」を配布手段として選択し、「**Next**」をクリックします。
1. 適切な「**Code Signing Identity**」を選択し、「**Next**」をクリックします。「**Allow**」をクリックして署名を適用します。
1. アプリケーションに名前をつけて、「**Save for Enterprise Distribution**」を選択します。
1. アプリケーションに&#x200B;**アプリケーション URL** を指定します。 例えば、CRX サーバーでアプリをホストするには、URL を指定します `https://[*LC_host*]:[*port*]/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. 「**タイトル**」フィールドで、AEM Forms を指定します。
1. 「**保存**」をクリックして Xcode を閉じます。

   インストーラーファイル `AEM Forms.ipa`、プロパティリストファイル `AEM Forms-info.plist` が指定された場所に作成されます。

1. を開きます。 `AEM Forms-info.plist` ファイルを編集します。
1. .ipa ファイルの URL のスペースをすべて %20 に置き換えます。
1. `AEM Forms-info.plist` ファイルを保存して閉じます。
