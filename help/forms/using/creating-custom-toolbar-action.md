---
title: カスタムツールバーアクションの作成
seo-title: Creating a custom toolbar action
description: フォーム開発者は、AEM Forms のアダプティブフォーム用にカスタムツールバーアクションを作成できます。カスタムアクションフォームを使用して、作成者はより多くのワークフローとオプションをエンドユーザーに提供できます。
seo-description: Form developers can create custom toolbar actions for adaptive forms in AEM Forms. Using custom actions form authors can provide more workflows and options to their end users.
uuid: 6761f389-1baa-4a59-a6e0-0f86f70fc692
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
discoiquuid: b80a2bfe-6f57-4229-a9ee-1ec87f3c3306
exl-id: bb0abe28-843a-4195-afd5-5ee7f0a279be
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 85%

---

# カスタムツールバーアクションの作成 {#creating-a-custom-toolbar-action}

## 前提条件 {#prerequisite}

カスタムツールバーアクションを作成する前に、「[クライアント側のライブラリを使用する方法](/help/sites-developing/clientlibs.md)」と「[CRXDE Lite を使用した開発](/help/sites-developing/developing-with-crxde-lite.md)」を参照して理解を深めてください。

## アクションとは {#what-is-an-action-br}

アダプティブフォームは、フォーム作成者がオプションの組み合わせを設定できるツールバーを提供します。これらのオプションは、アダプティブフォームのアクションとして定義されます。ツールバーの編集ボタンをクリックして、アダプティブフォームでサポートするアクションを設定するパネルを開きます。

![デフォルトのツールバーアクション](assets/default_toolbar_actions.png)

デフォルトで提供される一連のアクションに加え、カスタムアクションをツールバーに作成することができます。例えば、アクションを追加することで、フォームを送信する前にアダプティブフォームのすべてのフィールドを、ユーザーがレビューできるようにすることが可能です。

## アダプティブフォームにカスタムアクションを作成する手順 {#steps}

カスタムツールバーアクションを作成するには、次の手順を実行して、記入の済んだフォームを送信する前にアダプティブフォームのすべてのフィールドをエンドユーザーがレビューするためのボタンを作成します。

1. アダプティブフォームでサポートされるデフォルトのアクションは、すべて `/libs/fd/af/components/actions` フォルダー。 CRXDE で、 `fileattachmentlisting` ノードから `/libs/fd/af/components/actions/fileattachmentlisting` から `/apps/customaction`.

1. ノードを `apps/customaction` フォルダーの名前をに変更し、ノード名をに変更します。 `reviewbeforesubmit`. また、 `jcr:title` および `jcr:description` ノードのプロパティ。

   `jcr:title` のプロパティには、ツールバーダイアログに表示されるアクションの名前が含まれます。`jcr:description` のプロパティには、アクションにマウスオーバーしたときに表示される詳細情報が含まれます。

   ![ツールバーのカスタマイズに使用するノードの階層](assets/action3.png)

1. 選択 `cq:template` ノード内 `reviewbeforesubmit` ノード。 次の値を `guideNodeClass` プロパティは `guideButton` および `jcr:title` プロパティを適切に設定します。
1. type プロパティを `cq:Template` ノード。 この例では、タイプのプロパティをボタンに変更します。

   このコンポーネントで、生成された HTML に type の値が CSS クラスとして追加されます。ユーザーはこの CSS クラスを使用して、アクションのスタイルを設定できますボタン、送信、リセット、およびタイプの値を保存する際のスタイルが、モバイルとデスクトップデバイスの両方にデフォルトで用意されています。

1. アダプティブフォームの編集のツールバーダイアログからカスタムアクションを選択します。パネルのツールバーにレビューボタンが表示されます。

   ![カスタムアクションはツールバーで使用できます](assets/custom_action_available_in_toolbar.png) ![カスタムで作成したツールバーアクションの表示](assets/action7.png)

1. レビューボタンに機能を持たせるには、`reviewbeforesubmit` ノードにある init.jsp ファイルに JavaScript コード、CSS コード、およびサーバー側コードを追加します。

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

1. カスタムアクションの機能を検証するには、プレビューモードでアダプティブフォームを開いて、ツールバーのレビューボタンをクリックします。

   >[!NOTE]
   >
   >オーサリングモードでは `GuideBridge` ライブラリは読み込まれません。そのため、オーサリングモードではこのカスタムアクションは動作しません。

   ![カスタムレビューボタンのアクションのデモ](assets/action9.png)

## サンプル {#samples}

コンテンツパッケージは次のアーカイブにあります。このパッケージには、上記のカスタムツールバーアクションのデモに関連するアダプティブフォームが含まれています。

[ファイルを入手](assets/customtoolbaractiondemo.zip)
