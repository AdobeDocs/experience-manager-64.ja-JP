---
title: タスクアクションのカスタマイズ
seo-title: Customizing Task Actions
description: タスクアクションの外観をカスタマイズし、アクションにはイメージのみを使用し、ルートアクションに使用されるイメージをカスタマイズできます。
seo-description: You can customize appearance of the task actions, use only images for actions, and customize the images used in route actions.
uuid: f6aebcd5-beac-41bf-95bf-2c07d36afa8b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: ca3f6025-7e17-4173-8267-e24a338ea4a1
exl-id: 3534864b-3d1c-42ca-96a0-5becbfbc8ce6
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 52%

---

# タスクアクションのカスタマイズ {#customizing-task-actions}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms Workspace で、ユーザーはタスクアクションをカスタマイズすることができます。タスクアクションをカスタマイズする前に、「[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」に一覧表示されている手順に従っていることを確認してください。

## テキストスタイルのカスタマイズ {#customizing-text-style}

テキストスタイルをカスタマイズするには、`/apps/ws/css/newStyle.css` ファイルに次のコードスニペットを追加します。

```css
/*-------- For Task Actions visible in task list task action popup ----------------------------------------------------*/
#taskarea .taskActionsPopUp{
    position:absolute;
    right: 78px;
    top: 16px;
    display: none;
}
 
#taskarea .taskActionsPopUp ul{
    list-style-type: none;
    padding: 0px;
    margin: 0px;
    border: 1px solid #B2B2B2;
    background: #1D1D1D;
    box-shadow: inset 0px 0px 11px 2px #1C1C1C;
    height:34px;
}
 
#taskarea .taskActionsPopUp li{
    width: auto;
    height: 34px;
    float: left;
    border-right: 1px solid #B2B2B2;
}
 
#taskarea .taskActionsPopUp li i{
    height: 34px;
    width: 20px;
    float: left;
    cursor: pointer;
}
 
#taskarea .taskActionsPopUp li a{
    color: white;
    text-decoration: none;
    display: inline-block;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    text-align: left;
    max-width: 150px;
    margin: 8px 10px 0px 4px;
}
 
/*-------- For Task Actions visible in task Details task action popup ----------------------------------------------------*/
.task .taskActionsPopUp {
    position: absolute;
    border: 1px solid #1D1D1D;
    z-index: 110;
    right: 5px;
    top : 35px;
    background: #2f2f2f;
    display:none;
}
 
.task .taskActionsPopUp ul{
    list-style: none outside none;
    font-size: 13px;
    width: 160px;
}
 
.task .taskActionsPopUp li{
    height: 33px;
    border-bottom: 1px solid #474747;
    width: 20px
}
 
.task .taskActionsPopUp ul a{
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    color: white;
    text-decoration: none;
    height: 26px;
    width: 133px;
    padding: 7px 0px 0px 27px;
    display: block;
    text-align: left;
    cursor: pointer;
    border-bottom: 1px solid #474747;
}
```

## 画像のカスタマイズ {#customizing-images}

画像をカスタマイズするには、次のコードスニペットを `/apps/ws/css/newStyle.css` ファイルに追加します。次のコードスニペットは、 *ロック* アクション：

```css
#taskarea .taskActionsPopUp .lock, .task .taskActionsPopUp .lock{
    background: url(../images/icons.png) no-repeat -265px -6px;
}
```

>[!NOTE]
>
>「タスクリスト」および「タスクの詳細」アクションで、異なる画像や異なる解像度の画像を表示するための別々のスタイルを追加します。 例えば、「lock」アクションを変更するには、次のようにします。

```css
#taskarea .taskActionsPopUp .lock{
    background: url(../images/icons1.png) no-repeat -265px -6px;
}
.task .taskActionsPopUp .lock{
    background: url(../images/icons2.png) no-repeat -265px -6px;
}
```

## アクション用の画像のみの表示 {#showing-only-images-for-actions}

アクションのイメージのみを表示するには、ルートアクションで使用されるイメージをカスタマイズします。 詳しくは、「[ルートアクションのイメージ](/help/forms/using/images-route-actions.md)」を参照してください。

### タスクリストタスクアクションポップアップメニュー {#task-list-task-action-nbsp-pop-up-menu}

1. AEM Forms Workspace のタスクリストタスクアクションポップアップメニューの項目をカスタマイズするには、開発パッケージが必要です。 開発パッケージを作成する方法については、[AEM Forms Workspace コードの構築](/help/forms/using/introduction-customizing-html-workspace.md#building-html-workspace-code)を参照してください。

1. /libs/ws/js/runtime/templates/task.html を `/apps/ws/js/runtime/templates/task.html` にコピーして次のコードスニペットに置き換えます。

   ```
   // Orignal code
   <div class="taskActionsPopUp">
           <!--START_TASKACTIONS-->
           <ul>
               <li class="arrow"></li>
               <%if(!isMustOpenToComplete && window.lcWorkspace != undefined && window.lcWorkspace.currentUser != undefined && window.lcWorkspace.currentUser.properties != undefined && window.lcWorkspace.currentUser.properties['/client/routes/formViewOnly'] == 'false'){%>
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
               <%}%>
               <%for(var i = 0; i<availableCommands.taskACLCommands.length; i++){%>
               <li class="<%= availableCommands.taskACLCommands[i]%>" alt="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"><%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%></a>
               </li>
               <%}%>
               <%for(var i = 0; i<availableCommands.otherCommands.length; i++){%>
               <li class="<%= availableCommands.otherCommands[i]%>" alt="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"><%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%></a>
               </li>
               <%}%>
           </ul>
           <!--END_TASKACTIONS-->
           <%}%>
       </div>
   ```

   ```
   //New code
   
   <div class="taskActionsPopUp">
           <!--START_TASKACTIONS-->
           <ul>
               <li class="arrow"></li>
               <%if(!isMustOpenToComplete && window.lcWorkspace != undefined && window.lcWorkspace.currentUser != undefined && window.lcWorkspace.currentUser.properties != undefined && window.lcWorkspace.currentUser.properties['/client/routes/formViewOnly'] == 'false'){%>
               <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"></a>
               </li>
               <%}%>
               <%}%>
               <%}%>
               <%for(var i = 0; i<availableCommands.taskACLCommands.length; i++){%>
               <li class="<%= availableCommands.taskACLCommands[i]%>" alt="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"></a>
               </li>
               <%}%>
               <%for(var i = 0; i<availableCommands.otherCommands.length; i++){%>
               <li class="<%= availableCommands.otherCommands[i]%>" alt="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"></a>
               </li>
               <%}%>
           </ul>
           <!--END_TASKACTIONS-->
           <%}%>
       </div>
   ```

1. `/apps/ws/css/newStyle.css` ファイルからアンカータグに割り当てられている固定幅を削除します。

   ```css
   .task .taskActionsPopUp ul{
       list-style: none outside none;
       font-size: 13px;
       width: 160px;
   }
   
   To
   .task .taskActionsPopUp ul{
       list-style: none outside none;
       font-size: 13px;
   }
   
   AND
   
   .task .taskActionsPopUp ul a{
       white-space: nowrap;
       overflow: hidden;
       text-overflow: ellipsis;
       color: white;
       text-decoration: none;
       height: 26px;
       width: 133px;
       padding: 7px 0px 0px 27px;
       display: block;
       text-align: left;
       cursor: pointer;
       border-bottom: 1px solid #474747;
   }
   
   To
   
   .task .taskActionsPopUp ul a{
       white-space: nowrap;
       overflow: hidden;
       text-overflow: ellipsis;
       color: white;
       text-decoration: none;
       height: 26px;
       width: 0px;
       padding: 7px 0px 0px 27px;
       display: block;
       text-align: left;
       cursor: pointer;
       border-bottom: 1px solid #474747;
   }
   ```

### タスクの詳細タスクアクションポップアップメニュー {#task-details-task-action-pop-up-menu}

次の手順を実行して詳細タスクアクションポップアップメニューをカスタマイズします。

* /libs/ws/js/runtime/templates/taskdetails.html ファイルを `/apps/ws/js/runtime/templates/` フォルダーにコピーします。
* テキストの代わりにアンカータグの内部にアイコンタグをカプセル化します。例えば、以下に示す新しいコードは、アンカータグ内にアイコンタグをカプセル化します。

```
// Original code
<div class="taskActionsPopUp">
        <!--START_ACTIONBUTTONGROUP-->
        <ul>
            <li class="leftArrow"><a href="javascript:void(0);"><</a></li>
             
            <% if (isOwner && showDirectActions) { %>
                <% if (routeList === null) {%>
                    <li class="routeAction">
                        <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
                    </li>
                <% } else { %>
                    <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                        <li class="routeAction">
                            <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                        </li>
                    <%}%>
                <%}%>
             <%}%>
              
            <% if (isOwner || (showACLActions && availableCommands.taskACLCommands !== null && availableCommands.taskACLCommands !== undefined && availableCommands.taskACLCommands.length > 0) ||  availableCommands.otherCommands.length > 2) { %>
                <%for (var i = 0; showACLActions && i < availableCommands.taskACLCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>">
                        <i class="<%= availableCommands.taskACLCommands[i]%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"/>
                        <a href="javascript:void(0);" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"><%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.value')%></a>
                    </li>
                <%}%>
                 
                <%for (var i = 0; i < availableCommands.otherCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>">
                        <i class="<%= availableCommands.otherCommands[i]%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"/>
                        <a href="javascript:void(0);" value="<%= availableCommands.otherCommands[i]%>" data-action="other"><%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.value')%></a>
                    </li>
                <%}%>
            <%}%>
             
            <li class="rightArrow"><a href="javascript:void(0);">></a></li>
        </ul>
        <!--END_ACTIONBUTTONGROUP-->
    </div>
```

```
//New code
 
<div class="taskActionsPopUp">
        <!--START_ACTIONBUTTONGROUP-->
        <ul>
            <li class="leftArrow"><a href="javascript:void(0);"><</a></li>
             
            <% if (isOwner && showDirectActions) { %>
                <% if (routeList === null) {%>
                    <li class="routeAction">
                        <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
                    </li>
                <% } else { %>
                    <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                        <li class="routeAction">
                            <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                        </li>
                    <%}%>
                <%}%>
             <%}%>
              
            <% if (isOwner || (showACLActions && availableCommands.taskACLCommands !== null && availableCommands.taskACLCommands !== undefined && availableCommands.taskACLCommands.length > 0) ||  availableCommands.otherCommands.length > 2) { %>
                <%for (var i = 0; showACLActions && i < availableCommands.taskACLCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.taskaclcommand.'+availableCommands.taskACLCommands[i]+'.tooltip')%>">
                        <a href="javascript:void(0);" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL">
                            <i class="<%= availableCommands.taskACLCommands[i]%>" value="<%= availableCommands.taskACLCommands[i]%>" data-action="taskACL"/>
                        </a>
                    </li>
                <%}%>
                 
                <%for (var i = 0; i < availableCommands.otherCommands.length; i++) {%>
                    <li title="<%= $.t('taskaction.othercommand.'+availableCommands.otherCommands[i]+'.tooltip')%>">
                        <a href="javascript:void(0);" value="<%= availableCommands.otherCommands[i]%>" data-action="other">
                            <i class="<%= availableCommands.otherCommands[i]%>" value="<%= availableCommands.otherCommands[i]%>" data-action="other"/>
                        </a>
                    </li>
                <%}%>
            <%}%>
             
            <li class="rightArrow"><a href="javascript:void(0);">></a></li>
        </ul>
        <!--END_ACTIONBUTTONGROUP-->
    </div>
```

* /apps/ws/js/registry.jsファイルを編集用に開きます。
* 次のテキストを探します。 `text!/lc/libs/ws/js/runtime/templates/taskdetails.html`
* そのテキストを次のテキストに置き換えます。`text!/lc/apps/ws/js/runtime/templates/taskdetails.html`

[**サポートへのお問い合わせ**](https://www.adobe.com/jp/account/sign-in.supportportal.html)
