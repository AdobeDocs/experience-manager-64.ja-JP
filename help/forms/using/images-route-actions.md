---
title: ルートアクションで使用されるイメージのカスタマイズ
seo-title: Customize images used in route actions
description: LiveCycle AEM Forms Workspace のルートアクションで使用されるイメージをカスタマイズする方法。
seo-description: How-to customize the images used in route actions in LiveCycle AEM Forms workspace.
uuid: 42608376-587e-4b57-a9d5-8f9ebd981426
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 10158c13-47b4-43e3-ac47-690f3cbab158
exl-id: 7b1f60e7-c8fa-43b6-bef4-88b42e7bbc36
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 45%

---

# ルートアクションで使用されるイメージのカスタマイズ {#customize-images-used-in-route-actions}

ルートアクションで使用されるイメージをカスタマイズするには、「[カスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」で説明されている手順を実行し、次にこの記事で説明する手順を実行します。

## ルートアクションのイメージ {#images-for-route-actions}

1. 次の場所の CSS に新しいルートアクションのイメージを定義するスタイルを追加します。

   `/apps/ws/css/newStyle.css`

   例：という名前の新しいスタイルを追加します。 `myStyle1`次に示すように、画像ファイルをアップロードします。 `myStyleIcon1.png` から `/apps/ws/image`WebDAV クライアントを使用してフォルダーを作成します。

   >[!NOTE]
   >
   >WebDAV アクセスの詳細については、 [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   >[!NOTE]
   >
   >ルートアクション名と同じスタイル名を使用することをお勧めします。

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## タスクリストタスクアクションポップアップ {#task-list-task-action-popup}

1. タスクリストアクションポップアップを作成します ( [AEM Forms Workspace コードの構築](introduction-customizing-html-workspace.md#building-html-workspace-code). これには、Dev パッケージを使用する必要があります。

1. `/libs/ws/js/runtime/templates/task.html` を `/apps/ws/js/runtime/templates/task.html` にコピーします。

1. CSS スタイルの名前がサーバーからのルートアクション名と同じ場合は、 `/apps/ws/js/runtime/templates/task.html`:

   ```
   <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   
   To
   
   <%if(routeList == null){%>
               <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li class="<%= availableCommands.directCommands[i]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   ```

1. CSS スタイルの名前が、サーバーから取得したルートアクション名と異なる場合は、 `/apps/ws/js/runtime/templates/task.html`. これにより、`if-else` サーブレット条件のスタックを追加してルートアクション名でスタイルをマップします。

```
<%if(routeList == null){%>
            <li>
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
            <li>
                <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
            </li>
            <%}%>
            <%}%>
 
To
 
<%if(routeList == null){%>
            <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
                <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                     <li class="myStyle1" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                     <li class="myStyle2" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}%>
            <%}%>
            <%}%>
```

## タスクの詳細タスクアクションポップアップ {#task-details-task-action-popup}

1. `/libs/ws/js/runtime/templates/taskdetails.html` を `/apps/ws/js/runtime/templates/taskdetails.html` にコピーします。

1. CSS スタイルの名前がサーバーからのルートアクション名と同じ場合は、 `/apps/ws/js/runtime/templates/taskdetails.html`:

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                       <%}%>
   ```

1. CSS スタイルの名前が、サーバーから取得したルートアクション名と異なる場合は、 `/apps/ws/js/runtime/templates/taskdetails.html`. これにより、`if-else` サーブレット条件のスタックを追加してルートアクション名でスタイルをマップします。

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                   <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle1" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle2" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}%>
               <%}%>
   ```

1. 開く `/apps/ws/js/registry.js` 編集の際に、以下のテキストを探します。\
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. テキストを次のように置き換えます。\
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`
