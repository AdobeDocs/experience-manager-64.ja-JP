---
title: AEM Forms用AEMデスクトップアプリケーション
seo-title: AEM desktop app for AEM Forms
description: AEMデスクトップアプリケーションでは、Adobe Experience Manager(AEM)Assets リポジトリーとAEM Formsバイナリファイルを、システム上のネットワークディレクトリにマッピングできます。 AEMデスクトップアプリケーションでサポートされるアセットと、AEM Forms for AEMデスクトップアプリケーションを有効にする方法について詳しく説明します。
seo-description: AEM desktop app lets you map the Adobe Experience Manager (AEM) Assets repository and AEM Forms binary files to a network directory on your system. Learn more about the assets supported in AEM desktop app and how to enable AEM Forms for AEM desktop app.
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
role: Admin
exl-id: 26cd0851-cadf-4a8f-b3bf-59f77671f584
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 53%

---

# AEM Forms用AEMデスクトップアプリケーション {#aem-desktop-app-for-aem-forms}

AEMデスクトップアプリケーションでは、Adobe Experience Manager(AEM)Assets リポジトリーとAEM Formsバイナリファイルを、システム上のネットワークディレクトリにマッピングできます。 同期されたアセットとバイナリファイルをファイルエクスプローラーで表示し、各種のアプリケーションを使用してファイルを編集することができます。ファイルを表示するだけでなく、バイナリファイルの作成、アップロード、削除を行うこともできます。また、ソフトウェアから、ファイルのオープン、編集、保存を直接実行することもできます。例えば、Designer で直接 XDP ファイルを開いて編集することができます。アセットに対してローカルで行った変更内容は、AEM アセットリポジトリと AEM Forms の UI に反映されます。

AEM デスクトップアプリケーションは、AEM インスタンスからダウンロードすることができます。アプリのダウンロードについて詳しくは、 [AEMデスクトップアプリケーションリリースノート](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## AEMデスクトップアプリケーションでサポートされるAEM Forms Assets {#aem-forms-assets-supported-in-aem-desktop-app}

AEM デスクトップアプリケーションを使用して、フォームテンプレートタイプ（.xdp）、PDF フォームタイプ（.pdf）、ドキュメントタイプ（.pdf）、画像タイプ、XML スキーマタイプ（.xsd）、スタイルシートタイプ（.xfs）の AEM Forms バイナリファイルを同期することができます。AEM デスクトップアプリケーションでは、他のすべてのファイル（サポートされていないファイル）は 0 バイトファイルとして表示されます。サポートされていないファイルを 0 バイトファイルとして表示することにより、他の使用可能なアセットが AEM Forms サーバー上に存在することをユーザーに認識させることができます。

>[!NOTE]
>
>ファイル名には、英数字、ハイフン、下線のみを含めることができます。

## AEM Forms for AEMデスクトップアプリケーションの有効化 {#enable-aem-forms-for-aem-desktop-app}

AEMデスクトップアプリケーションは、Microsoft Windows では WebDAV プロトコルを使用し、Mac OS X では SMB1 を使用してAEM Formsサーバーに接続します。 WebDAV または SMB クライアントとのバイナリファイルおよび他のアセットの同期が、AEM Formsサーバーで初期設定の状態で有効になっていません。 AEM Forms for AEMデスクトップアプリケーションを有効にするには、次の手順を実行します。

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager /ツール]** ![ハンマー](assets/hammer.png) **[!UICONTROL /導入/運営/Web コンソール]**. 新しいウィンドウに Web コンソールが表示されます。
1. Web コンソールウィンドウで、「**[!UICONTROL FormsManager アドオン設定]**」オプションを探して選択します。
1. FormsManager アドオン設定ダイアログで「**[!UICONTROL 非同期リソース]**」チェックボックスの選択を解除して「**[!UICONTROL 保存]**」をクリックします。
1. AEM Forms サーバーを再起動します。再起動後、AEM FormsサーバーはAEMデスクトップアプリケーションでコンテンツを受け入れ、共有できるようになります。
1. AEM デスクトップアプリケーションを起動し、AEM Forms サーバーに接続します。

   接続に成功すると、デスクトップアプリケーションによって `content/dam` および `content/dam/formsanddocuments` フォルダー。 上記のフォルダーとローカルフォルダーとの間でファイルを移動するだけでなく、AEM デスクトップアプリケーションを使用して、自動的にデータが取り込まれたフォルダー間でコンテンツを移動することができます。
