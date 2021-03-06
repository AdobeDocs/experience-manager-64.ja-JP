---
title: セキュアな AEM Forms アプリケーション（iOS 用）の構築
seo-title: Building a secure AEM Forms app for iOS
description: セキュアな AEM Forms アプリケーションを構築する手順
seo-description: Steps to build a secure AEM Forms app.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 7efc657e-b662-47db-8e70-62a37f3a3051
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 81%

---

# セキュアな AEM Forms アプリケーション（iOS 用）の構築 {#building-a-secure-aem-forms-app-for-ios}

AEM Forms アプリケーション用 Xcode プロジェクトをアーカイブして、インストーラー（.ipa ファイル）とプロパティリストファイル（.plist ファイル）を構築する必要があります。プロパティリストファイルには、アプリケーションの名前やホストしているロケーションなど、ホストされているインハウスアプリケーションの設定情報が含まれます。 プロパティリストファイルについての詳細は、[About Information Property List Files](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)を参照してください。

1. 次の Web サイトにログインします。

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. アプリケーション ID を作成します。アプリケーション ID を作成する詳細な手順については、[アプリケーション ID の作成と設定](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)を参照してください。
1. アプリケーションのご使用の iOS アプリケーションのためのバンドル識別子を設定するには、**[!UICONTROL アプリケーション ID の設定]**&#x200B;をクリックします。
1. Web ページの下部にある、**[!UICONTROL Enable for Data Protection]** を選択します。 data protection オプションを指定します。

   「**[!UICONTROL 完了]**」をクリックします。

1. プロビジョニング／配布に行き、手順 3 で設定したアプリケーション ID を使って新しいプロファイルを作成します。
1. プロビジョニングプロファイルをダウンロードして Xcode および iPad に追加します。 
1. Xcode、iOS SDK がインストールおよび設定済みの Mac マシンにログインします。
1. Xcode で `AEM Forms.xcodeproj` プロジェクトを開きます。
1. 「**[!UICONTROL TARGETS]**」の「**[!UICONTROL AEM Forms]**」をクリックし、**[!UICONTROL AEM Forms]**」を選択します。を選択します。 **[!UICONTROL ビルド設定]** タブで、 **[!UICONTROL コード署名の権限]** セクションに移動し、権限ドロップダウンで、 **[!UICONTROL LC Enterprise]** オプション。
1. Xcode 内にある `LC Enterprise.entitlements` ファイルを探して、編集するために開きます。**XCode entitlements の下で、**プロビジョニングプロファイルに存在するのと同じキー値ペアを追加します。
1. 「**[!UICONTROL Build Settings]**」タブで、「**[!UICONTROL All]**」をクリックし、「**[!UICONTROL Combined]**」をクリックします。
1. 「**[!UICONTROL Settings]**」リストで、「**[!UICONTROL Code Signing]**」を展開します。
1. 「**[!UICONTROL Code Signing Identity]**」から、適切な署名を選択します。「**[!UICONTROL Debug]**」、「**[!UICONTROL Release]**」、「**[!UICONTROL Any iOS SDK]**」に同じ署名が選択されていることを確認します。
1. の下 **[!UICONTROL プロジェクト]**&#x200B;を選択します。 **[!UICONTROL AEM Forms]** をクリックし、適切な署名が **[!UICONTROL コード署名 ID]**, **[!UICONTROL デバッグ]**, **[!UICONTROL リリース]** および **[!UICONTROL 任意のiOS SDK]**.
1. AEM Forms アプリケーションを構築し、配布します。AEM Forms Workspace アプリケーションを構築・配信する詳細な手順については、[AEM Forms アプリケーション用のインストーラーの構築](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)を参照してください。
