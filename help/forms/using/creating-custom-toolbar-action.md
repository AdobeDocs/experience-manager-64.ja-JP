---
title: カスタムツールバーアクションの作成
seo-title: Creating a custom toolbar action
description: フォーム開発者は、AEM Formsでアダプティブフォーム用のカスタムツールバーアクションを作成できます。 カスタムアクションフォームを使用すると、作成者はエンドユーザーに多くのワークフローやオプションを提供できます。
seo-description: Form developers can create custom toolbar actions for adaptive forms in AEM Forms. Using custom actions form authors can provide more workflows and options to their end users.
uuid: 6761f389-1baa-4a59-a6e0-0f86f70fc692
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
discoiquuid: b80a2bfe-6f57-4229-a9ee-1ec87f3c3306
exl-id: bb0abe28-843a-4195-afd5-5ee7f0a279be
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 60%

---

# カスタムツールバーアクションの作成 {#creating-a-custom-toolbar-action}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 前提条件 {#prerequisite}

カスタムツールバーアクションを作成する前に、 [クライアント側ライブラリの使用](/help/sites-developing/clientlibs.md) および [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## アクションとは {#what-is-an-action-br}

アダプティブフォームには、フォーム作成者が一連のオプションを設定できるツールバーが用意されています。 これらのオプションは、アダプティブフォームのアクションとして定義されます。 パネルのツールバーの「編集」ボタンをクリックして、アダプティブフォームがサポートするアクションを設定します。

![デフォルトのツールバーアクション](assets/default_toolbar_actions.png)

デフォルトで提供される一連のアクションに加えて、ツールバーでカスタムアクションを作成できます。 例えば、フォームを送信する前に、ユーザーがすべてのアダプティブフォームフィールドを確認できるようにするアクションを追加することができます。

## アダプティブフォームでカスタムアクションを作成する手順 {#steps}

カスタムのツールバーアクションを作成するには、次の手順を実行して、記入の済んだフォームを送信する前にアダプティブフォームのすべてのフィールドをエンドユーザーがレビューするためのボタンを作成します。

1. アダプティブフォームでサポートされているデフォルトのアクションは、すべて `/libs/fd/af/components/actions` フォルダーにあります。CRXDE で、`fileattachmentlisting` ノードを `/libs/fd/af/components/actions/fileattachmentlisting` から `/apps/customaction` にコピーします。

1. `apps/customaction` フォルダーにノードをコピーしたら、ノードの名前を `reviewbeforesubmit` に変更します。このノードの `jcr:title` と `jcr:description` のプロパティも変更します。

   `jcr:title` プロパティには、ツールバーダイアログに表示されるアクションの名前が含まれています。`jcr:description` プロパティには、アクションにマウスオーバーしたときに表示される詳細情報が含まれます。

   ![ツールバーのカスタマイズに使用するノードの階層](assets/action3.png)

1. `reviewbeforesubmit` ノード内の `cq:template` ノードを選択します。`guideNodeClass` プロパティの値が `guideButton` となっていることを確認し、それに合わせて `jcr:title` プロパティを変更します。
1. `cq:Template` ノードの type プロパティを変更します。現在の例では、type プロパティを button に変更します。

   type の値が、コンポーネント用に生成されたHTMLに CSS クラスとして追加されます。 ユーザーは、その CSS クラスを使用して、アクションのスタイルを設定できます。 ボタン、送信、リセット、保存の各 type 値には、モバイルデバイスとデスクトップデバイスの両方に対応するデフォルトのスタイルが用意されています。

1. アダプティブフォームを編集するツールバーのダイアログから、カスタムアクションを選択します。パネルのツールバーに「レビュー」ボタンが表示されます。

   ![カスタムアクションはツールバーで使用できます](assets/custom_action_available_in_toolbar.png) ![カスタムで作成したツールバーアクションの表示](assets/action7.png)

1. 「レビュー」ボタンに機能を持たせるには、`reviewbeforesubmit` ノードにある init.jsp ファイルに JavaScript、CSS コード、およびサーバーサイドのコードを追加します。

   `init.jsp` に次のコードを追加します。

   ```
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <guide:initializeBean name="guideField" className="com.adobe.aemds.guide.common.GuideButton"/>
   
   <c:if test="${not isEditMode}">
           <cq:includeClientLib categories="reviewsubmitclientlibruntime" />
   </c:if>
   
   <%--- BootStrap Modal Dialog  --------------%>
   <div class="modal fade" id="reviewSubmit" tabindex="-1">
       <div class="modal-dialog">
           <div class="modal-content">
               <div class="modal-header">
                   <h3>Review the Form Fields</h3>
               </div>
               <div class="modal-body">
                   <div class="modal-list">
                       <table>
                           <tr>
                               <td>
                                   <label>Your Name is: </label>
                               </td>
                           </tr>
                           <tr>
                               <td>
                                   <label>Your Pan Number is: </label>
                               </td>
                           </tr>
                           <tr>
                               <td>
                                   <label>Your Date Of Birth is: </label>
                               </td>
                           </tr>
                           <tr>
                               <td>
                                   <label>Your Total 80C Declaration Amount is: </label>
                               </td>
                           </tr>
                           <tr>
                               <td>
                                   <label>Your Total HRA Amount is: </label>
                               </td>
                           </tr>
                       </table>
                   </div>
               </div><!-- /.modal-body -->
               <div class="modal-footer">
                   <div class="fileAttachmentListingCloseButton col-md-2 col-xs-2 col-sm-2">
                       <button data-dismiss="modal">Close</button>
                   </div>
               </div>
           </div><!-- /.modal-content -->
       </div><!-- /.modal-dialog -->
   </div><!-- /.modal -->
   ```

   `ReviewBeforeSubmit.js` ファイルに次のコードを追加します。

   ```
   /*anonymous function to handle show of review before submit view */
   $(function () {
       if($("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").length > 0) {
           $("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").click(function(){
               // Create the options object to be passed to the getElementProperty API
               var options = {},
                   result = [];
               options.somExpressions = [];
               options.propertyName = "value";
               guideBridge.visit(function(model){
                   if(model.name === "name" || model.name === "pan" || model.name === "dateofbirth" || model.name === "total" || model.name === "totalmonthlyrent"){
                           options.somExpressions.push(model.somExpression);
                   }
               }, this);
               result = guideBridge.getElementProperty(options);
   
               $('#reviewSubmit .reviewlabel').each(function(index, item){
                   var data = ((result.data[index] == null) ? "No Data Filled" : result.data[index]);
                   if($(this).next().hasClass("reviewlabelvalue")){
                       $(this).next().html(data);
                   } else {
                       $(this).after($("<td></td>").addClass("reviewlabelvalue col-md-6 active").html(data));
                   }
               });
               // added because in mobile devices it was causing problem of backdrop
               $("#reviewSubmit").appendTo('body');
               $("#reviewSubmit").modal("show");
           });
       }
   });
   ```

   `ReviewBeforeSubmit.css` ファイルに次のコードを追加します。

   ```css
   .modal-list .reviewlabel {
       white-space: normal;
       text-align: right;
       padding:2px;
   }
   
   .modal-list .reviewlabelvalue {
       border: #cde0ec 1px solid;
       padding:2px;
   }
   
   /* Adding icon for this action in mobile devices */
   /* This is the glyphicon provided by bootstrap eye-open */
   /* .<type> .iconButton-icon */
   .reviewbeforesubmit .iconButton-icon {
       position: relative;
       top: -8px;
       font-family: 'Glyphicons Halflings';
       font-style: normal;
   }
   
   .reviewbeforesubmit .iconButton-icon:before {
       content: "\e105"
   }
   ```

1. カスタムアクションの機能を検証するには、プレビューモードでアダプティブフォームを開いて、ツールバーの「レビュー」ボタンをクリックします。

   >[!NOTE]
   >
   >オーサリングモードでは `GuideBridge` ライブラリは読み込まれません。そのため、オーサリングモードではこのカスタムアクションは動作しません。

   ![カスタムレビューボタンのアクションのデモ](assets/action9.png)

## サンプル {#samples}

次のアーカイブには、コンテンツパッケージが含まれています。 このパッケージには、上記のカスタムツールバーアクションのデモに関連するアダプティブフォームが含まれています。

[ファイルを取得](assets/customtoolbaractiondemo.zip)
