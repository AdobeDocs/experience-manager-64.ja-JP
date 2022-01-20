---
title: Web アプリケーションでの AEM Forms Workspace コンポーネントの統合
seo-title: Integrating AEM Forms workspace components in web applications
description: 独自の Web アプリケーションで AEM Forms Workspace コンポーネントを再利用して、機能を強化し密接な統合を提供する方法。
seo-description: How to reuse AEM Forms workspace components in your own webapps to leverage functionality and provide tight integration.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
exl-id: 4e3ed3c8-ef77-432e-ad4d-7d341787cc5c
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 72%

---

# Web アプリケーションでの AEM Forms Workspace コンポーネントの統合 {#integrating-aem-forms-workspace-components-in-web-applications}

AEM Forms Workspace [コンポーネント](/help/forms/using/description-reusable-components.md) を固有の Web アプリケーションで使用することができます。以下のサンプルの実装は、CRX™ インスタンスにインストールされた AEM Forms Workspace Dev パッケージのコンポーネントを使用して Web アプリケーションを作成します。下記のソリューションをカスタマイズして、個々のニーズに合わせます。実装例の再利用 `UserInfo`, `FilterList`、および `TaskList`web ポータル内のコンポーネント。

1. 次の場所でCRXDE Lite環境にログイン `https://[server]:[port]/lc/crx/de/`. AEM Forms Workspace Dev パッケージがインストールされていることを確認します。
1. パスの作成 `/apps/sampleApplication/wscomponents`.
1. css、images、js/libs、js/runtime、および js/registry.js を

   * コピー元：`/libs/ws`
   * コピー先：`/apps/sampleApplication/wscomponents`。

1. /apps/sampleApplication/wscomponents/js フォルダー内部に demomain.js ファイルを作成します。コードを /libs/ws/js/main.js から demomain.js にコピーします。
1. demomain.js で、コードを削除してルーターを初期化し、以下のコードを追加します。

   ```
   require(['initializer','runtime/util/usersession'], 
       function(initializer, UserSession) { 
           UserSession.initialize( 
               function() { 
                   // Render all the global components
                   initializer.initGlobal();  
               }); 
       });
   ```

1. /content の下に、名前でノードを作成します。 `sampleApplication` と入力します。 `nt:unstructured`. このノードのプロパティで、 `sling:resourceType` の型が文字列および値 `sampleApplication`. このノードのアクセス制御リストで、jcr:read 権限を許可する `PERM_WORKSPACE_USER` にエントリを追加します。また、 `/apps/sampleApplication` エントリを追加 `PERM_WORKSPACE_USER` jcr:read 権限の許可
1. In `/apps/sampleApplication/wscomponents/js/registry.js` からパスを更新 `/lc/libs/ws/` から `/lc/apps/sampleApplication/wscomponents/` テンプレート値用。
1. ポータルホームページの JSP ファイル ( ) `/apps/sampleApplication/GET.jsp`次のコードを追加して、必要なコンポーネントをポータル内に含めます。

   ```as3
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div> 
   <div class="filterListView gcomponent" data-name="filterlist"></div> 
   <div class="taskListView gcomponent" data-name="tasklist"></div> 
   ```

   AEM Forms Workspace コンポーネントに必要な CSS ファイルも含めます。

   >[!NOTE]
   >
   >各コンポーネントはレンダリングする際にコンポーネントタグ（クラス gcomponent を所有）に追加されます。ホームページにこれらのタグが含まれていることを確認します。これらの基本制御タグの詳細については、AEM Forms Workspace の `html.jsp` ファイルを参照してください。

1. コンポーネントをカスタマイズするには、以下のように必要なコンポーネントの既存のビューを拡張します。

   ```as3
   define([ 
       ‘jquery’, 
       ‘underscore’, 
       ‘backbone’, 
       ‘runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){ 
           var demoUserInfo = UserInfo.extend({ 
               //override the functions to customize the functionality 
               render: function() { 
                   UserInfo.prototype.render.call(this); // call the render function of the super class 
                   … 
                   //other tasks 
                   … 
               } 
           }); 
           return demoUserInfo; 
   });
   ```

1. ポータルの CSS を修正し、ポータル上の必要なコンポーネントのレイアウト、配置、スタイルを設定します。たとえば、このポータルの背景色を黒色に保持して userInfo コンポーネントも同様に表示するとします。それには、 `/apps/sampleApplication/wscomponents/css/style.css` 次のように指定します。

   ```as3
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC    
       position: relative;
       margin: 0 auto;
   }
   ```
