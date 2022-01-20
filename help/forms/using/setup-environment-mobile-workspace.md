---
title: AEM Forms アプリケーションの環境設定
seo-title: Set up environment for AEM Forms app
description: AEM Forms アプリケーションを構築しデプロイするためのハードウェア、ソフトウェア、ライセンス。
seo-description: Hardware, software, and licenses to build and deploy the AEM Forms app.
uuid: 0c8f5259-8e9f-45ce-ade4-e14f1a41c0de
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 72c3a451-fa57-4b12-8d25-fc2e6fa98adb
exl-id: 5c60d1a6-a4a2-4131-81e6-e39a5ab07dcf
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 65%

---

# AEM Forms アプリケーションの環境設定 {#set-up-environment-for-aem-forms-app}

AEM Forms アプリケーションを構築しデプロイするためには、次のハードウェア、ソフトウェア、ライセンスが必要です。

## Windows デバイスの場合 {#for-windows-devices}

* Microsoft Windows 8.1 または Windows 10
* Microsoft Visual Studio 2015
* Apache Cordova 向け Microsoft Visual Studio Tools

## iOS デバイスの場合 {#for-ios-devices}

* Mac OS X 10.9.5 以上搭載の Intel ベース Apple Mac
* iOS SDK 8.4 以降
* Xcode バージョン: Xcode 6.4 for OS X 以上
* iOS Developer Enterprise プログラムのメンバーシップ
* 社内の iOS アプリケーション配布のためのエンタープライズ証明書
* Apple iPad（iOS 8.4 以降搭載）

## Android デバイスの場合 {#for-android-devices}

* Android Development Toolkit（ADT バンドル）（からダウンロード可能） [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)
* MAC システム上に環境が設定される場合は、Applications フォルダーに ADT をインストールする必要があります。
* ADT がMACの他の場所にインストールされている場合、または環境が Windows システムに設定されている場合は、ADT SDK のパスを `local.properties` ファイル `src\android` 抽出されたソースアーカイブ内のフォルダー `mobileworkspace-src.zip`. このファイルで、`sdk.dir` 変数をデスクトップ上の ADT SDK の場所にポイントしてください。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip には PhoneGap SDK 5.0 が含まれています。PhoneGap SDK が事前にインストールされていないことを確認してください。
