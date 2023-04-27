---
title: AEM Forms アプリケーションの環境設定
seo-title: Set up environment for AEM Forms app
description: AEM Formsアプリを構築しデプロイするためのハードウェア、ソフトウェア、ライセンス。
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
ht-degree: 58%

---

# AEM Forms アプリケーションの環境設定 {#set-up-environment-for-aem-forms-app}

AEM Formsアプリを構築してデプロイするには、次のハードウェア、ソフトウェア、ライセンスが必要です。

## Windows デバイスの場合 {#for-windows-devices}

* Microsoft Windows 8.1 または Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools for Apache Cordova

## iOSデバイスの場合 {#for-ios-devices}

* Mac OS X 10.9.5 以降を実行するインテルベースのApple Mac
* iOS SDK 8.4 以降
* Xcode バージョン：OS X 以降の Xcode 6.4
* iOS Developer Enterprise プログラムのメンバーシップ
* 社内iOSアプリを配布するためのエンタープライズ証明書
* Apple iPadとiOS 8.4 以降

## Android デバイスの場合 {#for-android-devices}

* [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html) からダウンロードできる Android 開発ツールキット（ADT バンドル）
* MAC システム上に環境を設定する場合は、Applications フォルダーに ADT をインストールする必要があります。
* ADT が MAC 上のそれ以外の場所にインストールされている場合、あるいは環境が Window システム上に設定される場合、ADT SDK パスは、展開されたソースアーカイブ `mobileworkspace-src.zip` の `src\android` フォルダーにある `local.properties` ファイルでアップデートする必要があります。このファイルで、`sdk.dir` 変数をデスクトップ上の ADT SDK の場所を指すようにします。

>[!NOTE]
>
>adobe-lc-mobileworkspace-src.zip には PhoneGap SDK 5.0 が含まれています。PhoneGap SDK が事前にインストールされていないことを確認してください。
