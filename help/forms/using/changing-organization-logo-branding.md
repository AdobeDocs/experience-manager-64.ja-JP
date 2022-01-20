---
title: ブランディングのための組織ロゴの変更
seo-title: Changing the organization logo for branding
description: AEM Forms Workspace をブランディングするには、デフォルトのロゴをカスタマイズして組織のロゴを指定します。
seo-description: To brand AEM Forms workspace provide the logo of your organization by customizing the default logo.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
exl-id: 890e98af-0491-4b59-9a9b-6c245db54f0f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 79%

---

# ブランディングのための組織ロゴの変更 {#changing-the-organization-logo-for-branding}

組織ロゴは AEM Forms Workspace の左上隅に表示されます。ロゴを更新するには、[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)および次の手順に従います。

1. ロゴを作成してファイルに `NewWorkspace.png` と名前を付けます。WebDAV クライアントを使用して画像ファイルを /apps/ws/images フォルダーに配置します。

   >[!NOTE]
   >
   >ロゴの画像の推奨サイズは 218 ピクセル × 20 ピクセルです。

   >[!NOTE]
   >
   >WebDAV アクセスの詳細については、 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. 次のスタイルを追加することによって、/apps/ws/css/newStyle.css にあるスタイルシートの新しいロゴ画像を参照します。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px; 
         }
   ```
