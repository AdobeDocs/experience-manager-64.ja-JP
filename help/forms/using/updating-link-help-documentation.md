---
title: ドキュメントへのリンクの更新
seo-title: Updating the link to the documentation
description: AEM Forms Workspace の Workspace ヘルプリンクの宛先を更新して、カスタムドキュメントリンクを指すようにする方法。
seo-description: How-to update the destination of Workspace Help link in AEM Forms workspace to point to your custom documentation link.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
exl-id: 68fe3f97-ded8-4223-b4b9-02704077e37e
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 43%

---

# ドキュメントへのリンクの更新 {#updating-the-link-to-the-documentation}

AEM Forms Workspace のデフォルトのヘルプコンテンツにアクセスするには、 **ヘルプ/Workspace ヘルプ**. Adobeの Web サイト上のオンラインドキュメントを指しています。 ただし、他の URL を指すように更新することもできます。

デフォルトのヘルプ URL を変更する場合は、次の使用例を検討してください。

* 選択した言語でローカライズされたヘルプを提供する場合。
* カスタマイズされた Workspace にカスタマイズされたヘルプコンテンツを指定する場合。

オンラインドキュメントの URL を更新するには、「[カスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」の後に以下の手順を実行します。

1. `userinfo.html` ファイルを `/libs/ws/js/runtime/templates` から `/apps/ws/js/runtime/templates` にコピーします。
1. 変更点：

   ```
   <ul class="helpmenu">
     <li>            
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   コピー先：

   ```
   <ul class="helpmenu">
     <li>            
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. 以下の操作を実行します。

   1. /apps/ws/js/registry.js を開いて編集します。
   1. `text!/lc/libs/ws/js/runtime/templates/userinfo.html` を検索して `text!/lc/apps/ws/js/runtime/templates/userinfo.html` に置換します。
