---
title: AEM Forms の AEM デスクトップアプリケーション
seo-title: AEM desktop app for AEM Forms
description: AEM デスクトップアプリケーションにより、Adobe Experience Manager（AEM）のアセットリポジトリと AEM Forms のバイナリファイルを、システム上のネットワークディレクトリにマップすることができます。AEMデスクトップアプリケーションでサポートされるアセットと、AEM Forms for AEMデスクトップアプリケーションを有効にする方法について詳しく説明します。
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
ht-degree: 52%

---

# AEM Forms の AEM デスクトップアプリケーション {#aem-desktop-app-for-aem-forms}

AEM デスクトップアプリケーションにより、Adobe Experience Manager（AEM）のアセットリポジトリと AEM Forms のバイナリファイルを、システム上のネットワークディレクトリにマップすることができます。同期されたアセットとバイナリファイルをエクスプローラーで表示し、様々なアプリを使用して必要に応じてファイルを編集できます。 ファイルの表示に加えて、バイナリファイルの作成、アップロード、削除をおこなうこともできます。 また、ソフトウェアから直接ファイルを開いたり、編集したり、保存したりすることもできます。 例えば、Designer から直接 XDP ファイルを開いて編集することができます。 アセットに対してローカルで加えた変更は、AEM AssetsリポジトリとAEM Forms UI に反映されます。

AEMインスタンスからアプリをダウンロードできます。 AEM デスクトップアプリケーションの詳しいダウンロード方法については、[AEM デスクトップアプリケーションのリリースノート](https://helpx.adobe.com/jp/experience-manager/desktop-app/release-notes.html)を参照してください。

## AEM デスクトップアプリケーションでサポートされる AEM Forms のアセット {#aem-forms-assets-supported-in-aem-desktop-app}

このアプリケーションを使用して、フォームテンプレート (.xdp)、PDFフォーム (.pdf)、ドキュメント (.pdf)、画像、XML スキーマ (.xsd)、スタイルシート (.xfs) のAEM Formsバイナリファイルを同期できます。 その他のすべてのファイル（サポートされていないファイル）が 0 バイトファイルとしてデスクトップアプリケーションに表示されます。 サポートされていないファイルを 0 バイトファイルとして表示すると、AEM Formsサーバー上で使用可能なその他のアセットの存在をユーザーが認識できます。

>[!NOTE]
>
>ファイル名には、英数字、ハイフン、アンダースコアのみを含めることができます。

## AEM デスクトップアプリケーションに対して AEM Forms を有効にする {#enable-aem-forms-for-aem-desktop-app}

AEMデスクトップアプリケーションは、Microsoft Windows では WebDAV プロトコルを使用し、Mac OS X では SMB1 を使用してAEM Formsサーバーに接続します。 初期状態の AEM Forms サーバーは、バイナリファイルと他のアセットを WebDAV クライアントまたは SMB クライアントと同期するようには設定されていません。AEM Forms for AEMデスクトップアプリケーションを有効にするには、次の手順を実行します。

1. 管理者として AEM Forms にログインします。
1. オーサーインスタンスで、「![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager／Tools]** ![ハンマー](assets/hammer.png) **[!UICONTROL ／Deployment／Operations／Web Console]**」をクリックしてください。新しいウィンドウに web コンソールが表示されます。
1. Web コンソールウィンドウで、**[!UICONTROL FormsManager アドオン設定]**&#x200B;オプションを探して選択してください。
1. FormsManager アドオン設定ダイアログで&#x200B;**[!UICONTROL 非同期リソース]**&#x200B;チェックボックスの選択を解除して、**[!UICONTROL 保存]**&#x200B;をクリックしてください。
1. AEM Forms サーバーを再起動します。再起動が完了すると、AEM Forms サーバーでコンテンツを取得し、そのコンテンツを AEM デスクトップアプリケーションと共有できるようになります。
1. AEM デスクトップアプリケーションを開き、AEM Forms サーバーに接続してください。

   接続に成功すると、アプリケーションは `content/dam` と `content/dam/formsanddocuments` のフォルダーを作成します。上記のフォルダーとローカルフォルダーとの間でファイルを移動するだけでなく、AEM デスクトップアプリケーションを使用して、自動的に作成されたフォルダー間でコンテンツを移動することができます。
