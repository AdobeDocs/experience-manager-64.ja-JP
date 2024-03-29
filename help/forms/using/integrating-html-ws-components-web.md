---
title: Web アプリケーションでの AEM Forms ワークスペースコンポーネントの統合
seo-title: Integrating AEM Forms workspace components in web applications
description: 機能を活用し、緊密な統合を提供するために、独自の Web アプリでAEM Forms Workspace コンポーネントを再利用する方法。
seo-description: How to reuse AEM Forms workspace components in your own webapps to leverage functionality and provide tight integration.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
exl-id: 4e3ed3c8-ef77-432e-ad4d-7d341787cc5c
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 45%

---

# Web アプリケーションでの AEM Forms ワークスペースコンポーネントの統合 {#integrating-aem-forms-workspace-components-in-web-applications}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM Forms Workspace を使用できます [コンポーネント](/help/forms/using/description-reusable-components.md) を設定します。 以下のサンプル実装では、CRX™インスタンスにインストールされたAEM Forms workspace 開発パッケージのコンポーネントを使用して、Web アプリケーションを作成します。 特定のニーズに合わせて以下のソリューションをカスタマイズします。 サンプルの実装は、Web ポータル内部の `UserInfo`、`FilterList`、`TaskList` コンポーネントを再利用します。

1. `https://[server]:[port]/lc/crx/de/` で CRXDE Lite 環境にログインします。AEM Forms Workspace Dev パッケージがインストールされていることを確認します。
1. パス `/apps/sampleApplication/wscomponents` を作成します。
1. css、images、js/libs、js/runtime、および js/registry.js をコピーします

   * コピー元：`/libs/ws`
   * コピー先：`/apps/sampleApplication/wscomponents`。

1. /apps/sampleApplication/wscomponents/js フォルダー内に demomain.js ファイルを作成します。 /libs/ws/js/main.jsから demomain.js にコードをコピーします。
1. demomain.js で、コードを削除して Router を初期化し、次のコードを追加します。

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

1. /content の下に名前 `sampleApplication` およびタイプ `nt:unstructured` のノードを作成します。このノードのプロパティで、タイプ文字列の `sling:resourceType` と値 `sampleApplication` を追加します。このノードのアクセス制御リストで、jcr:read 権限を許可する `PERM_WORKSPACE_USER` にエントリを追加します。また、`/apps/sampleApplication` のアクセス制御リストで、jcr:read privileges 権限を許可する `PERM_WORKSPACE_USER` のエントリを追加します。
1. `/apps/sampleApplication/wscomponents/js/registry.js` でテンプレート値のパスを `/lc/libs/ws/` から `/lc/apps/sampleApplication/wscomponents/` にアップデートします。
1. `/apps/sampleApplication/GET.jsp`/ にあるポータルホームページの JSP ファイルで、次のコードを追加してポータル内部の必要なコンポーネントを含めます。

   ```as3
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div> 
   <div class="filterListView gcomponent" data-name="filterlist"></div> 
   <div class="taskListView gcomponent" data-name="tasklist"></div> 
   ```

   また、AEM Forms Workspace コンポーネントに必要な CSS ファイルも含めます。

   >[!NOTE]
   >
   >各コンポーネントは、レンダリング時に（クラス gcomponent を持つ）コンポーネントタグに追加されます。 ホームページにこれらのタグが含まれていることを確認します。 これらの基本制御タグの詳細については、AEM Forms Workspace の `html.jsp` ファイルを参照してください。

1. コンポーネントをカスタマイズするには、次のように、必要なコンポーネントの既存のビューを拡張します。

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

1. ポータル CSS を変更して、ポータル上の必要なコンポーネントのレイアウト、位置、スタイルを設定します。 例えば、このポータルの背景色を黒のままにして、userInfo コンポーネントも表示したいとします。 それには、以下のようにして `/apps/sampleApplication/wscomponents/css/style.css` の背景色を変更します。

   ```as3
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC    
       position: relative;
       margin: 0 auto;
   }
   ```
