---
title: AEM Forms アプリの配布
seo-title: Distribute AEM Forms app
description: モバイルデバイスでのアプリの大規模なデプロイメントには、モバイルデバイス管理 (MDM) を使用します。
seo-description: Use Mobile Device Management (MDM) for the large-scale deployment of apps on mobile devices.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
exl-id: c1bf0a0e-70f7-41dd-8b1a-c114d89a265b
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 35%

---

# AEM Forms アプリの配布 {#distribute-aem-forms-app}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

モバイルデバイス管理 (MDM) を使用すると、モバイルデバイスでのアプリの大規模なデプロイメントを可能にします。

>[!NOTE]
>
>この配布は、iOSおよび Android デバイスにのみ適用されます。

## MDM ソリューションで一般に提供される主な機能： {#main-features-generally-provided-by-mdm-solutions}

* エンタープライズ環境でのデバイス登録の有効化
* デバイス設定の設定と更新の許可
* セキュリティコンプライアンスの執行
* 企業リソースへのモバイルアクセスの保護

MDM ソリューションとモバイルアプリケーション管理を組み合わせることで、企業内のモバイルデバイス全体で、社内、公開、および購入したアプリを管理できます。

MDM 管理者は、ipa ファイルと apk ファイルの両方を MDM サーバーにアップロードし、ipa ファイルまたは apk ファイルにアクセスできるユーザーを制御できます。 管理者は、各アプリケーションに対応するプロファイル設定を制御することもできます。

## AEM Forms アプリケーションに影響するプロファイル設定 {#profile-settings-affecting-the-aem-forms-app-br}

デバイスにおける次のプロファイル設定は、お使いのデバイスの AEM Forms アプリケーションの機能に影響を与えます。

* **カメラの使用を許可** 内 **デバイス機能** セクション

「**Allow use of camera**」を無効にすると、[写真注釈](/help/forms/using/add-attachments.md)のカメラ機能は使えません。アプリでカメラを使用するには、このオプションを有効にする必要があります。

* **デバイスでのパスコードの要求** 「Passcode policies」セクションの

**アプリケーションデータの暗号化** を有効にするには、デバイスの **パスコード** を有効にすることをお勧めします。デバイスにパスコードが設定されていない場合、デバイスに保存されているアプリケーションデータは暗号化されません。
