---
title: AEM Forms アプリケーションの環境設定
seo-title: AEM Forms アプリケーションの環境設定
description: AEM Forms アプリケーションを構築しデプロイするためのハードウェア、ソフトウェア、ライセンス。
seo-description: AEM Forms アプリケーションを構築しデプロイするためのハードウェア、ソフトウェア、ライセンス。
uuid: 0c8f5259-8e9f-45ce-ade4-e14f1a41c0de
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 72c3a451-fa57-4b12-8d25-fc2e6fa98adb
translation-type: tm+mt
source-git-commit: db4d19e3af11f04369fc7f6a7c13377962f0650a

---


# AEM Forms アプリケーションの環境設定 {#set-up-environment-for-aem-forms-app}

AEM Forms アプリケーションを構築しデプロイするためには、次のハードウェア、ソフトウェア、ライセンスが必要です。

## Windows デバイスの場合 {#for-windows-devices}

* Microsoft Windows 8.1 または Windows 10
* Microsoft Visual Studio 2015
* Apache Cordova 向け Microsoft Visual Studio Tools

## iOS デバイス用 {#for-ios-devices}

* Mac OS X 10.9.5 以上搭載の Intel ベース Apple Mac
* iOS SDK 8.4以降
* Xcode バージョン: Xcode 6.4 for OS X 以上
* iOS Developer Enterprise プログラムのメンバーシップ
* 社内の iOS アプリケーション配布のためのエンタープライズ証明書
* Apple iPad（iOS 8.4 以降搭載）

## Android デバイスの場合 {#for-android-devices}

* Android Development Toolkit (ADT bundle) that can be downloaded from [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)
* MAC システム上に環境が設定される場合は、Applications フォルダーに ADT をインストールする必要があります。
* If the ADT is installed in any other location on MAC, or if the environment is set up on a Windows system, the ADT SDK path needs to be updated in `local.properties` file that is available in `src\android` folder in the extracted the source archive `mobileworkspace-src.zip`. このファイルで、`sdk.dir` 変数をデスクトップ上の ADT SDK の場所にポイントしてください。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zipには、PhoneGap SDK 5.0が含まれています。PhoneGap SDKが事前にインストールされていないことを確認します。

**[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)**
