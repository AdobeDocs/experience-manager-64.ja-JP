---
title: Form Bridge と HTML5 フォームのカスタムポータルの統合
seo-title: Form Bridge と HTML5 フォームのカスタムポータルの統合
description: FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定できます。
seo-description: FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定できます。
uuid: 09f2189f-d584-4b84-895e-22833b6b17e3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: e0608649-bd49-4f40-bc1b-821c9b208883
feature: 'モバイルフォーム '
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 81%

---


# Form Bridge と HTML5 フォームのカスタムポータルの統合 {#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge はフォームとのやりとりを可能にする HTML5 フォームのブリッジ API です。FormBridge APIリファレンスについては、[FormBridge APIリファレンス](/help/forms/using/form-bridge-apis.md)を参照してください。

FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定できます。たとえば、API を使用してウィザードのような経験を築くことができます。

既存の HTML アプリケーションは FormBridge API を利用してフォームとやりとりし、それを HTML ページに埋め込むことができます。次の手順を使用して、Form Bridge API を使用してフィールドの値を設定できます。

## HTML5 フォームと Web ページの統合  {#integrating-html-forms-to-a-web-page}

1. **プロファイルの選択またはプロファイルの作成**

   1. CRX DEインターフェイスで、次の場所に移動します。`https://[server]:[port]/crx/de`.
   1. 管理者の資格情報を使用してログインします。
   1. プロファイルを作成するか、既存のプロファイルを選択します。

      プロファイルの作成方法について詳しくは、[新しいプロファイルの作成](/help/forms/using/custom-profile.md)を参照してください。

1. **HTML プロファイルの変更**

   XFA ランタイム、XFA ロケールライブラリ、および XFA フォーム HTML スニペットをプロファイルレンダラーに含めた後、Web ページをデザインして、フォームを Web ページ内に配置します。

   たとえば、次のコードスニペットを使用して、2 つの入力フィールドとフォームのあるアプリを作成し、フォームと外部アプリの間でのやり取りを示します。

   ```xml
   <%@ page session="false"
                  contentType="text/html; charset=utf-8"%><%
   %><%@ taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
   %><!DOCTYPE html>
   <html manifest="${param.offlineSpec}">
       <head>
          <cq:include script="formRuntime.jsp"/>
           <!-- Portal Scripts and Styles -->
          <cq:include script="portalheader.jsp"/> 
       </head>
       <body>
           <div id="leftdiv" >
               <div id="leftdivcontentarea">   
                   <!-- Portal Body -->
                 <cq:include script="portalbody.jsp"/>  
               </div>
           </div>
           <div id="rightdiv">
               <div id="formBody">
               <cq:include script="config.jsp"/>
               <!-- Form body -->
               <cq:include script="formBody.jsp"/>
               <!  --To assist in page transitions -- add navigation, based on scrolling -->
               <cq:include  script="../nav/scroll/nav_footer.jsp"/>
               <cq:include script="footer.jsp"/>
               </div>    
           </div>
       </body>
   </html>
   ```

   >[!NOTE]
   >
   >**9**&#x200B;行目には、ページをデザインするCSSスタイルとJavaScriptファイルの追加JSP参照が含まれます。
   >
   >**18 行目**&#x200B;の &lt;div id=&quot;rightdiv&quot;> タグには XFA フォームの HTML スニペットが含まれています。
   ページは 2 つのコンテナ、**left** と **right** にスタイル設定されています。right コンテナにはフォームがあります。left コンテナには 2 つの入力フィールドと外部 HTML ページの一部があります。
   次のスクリーンショットは、フォームがどのようにブラウザーで表示されるかを示しています。

   ![ポータル](assets/portal.jpg)

   左側は **HTML ページ**&#x200B;の一部です。右側でフィールドを含んでいるのは **xfa フォーム**&#x200B;です。

1. **ページからのフォームフィールドへのアクセス**

   次にあるのは、フォームフィールドの値を設定するために追加できるサンプルのスクリプトです。

   例えば、**名**&#x200B;フィールドと&#x200B;**姓**&#x200B;フィールドの値を使用して&#x200B;**EmployeeName**&#x200B;を設定する場合は、**window.formBridge.setFieldValue**&#x200B;関数を呼び出します。

   同様に、**window.formBridge.getFieldValue **APIを呼び出すことで値を読み取ることができます。

   ```
   $(function() {
               $(".input").blur(function() {
                   window.formBridge.setFieldValue(
                               'xfa.form.form1.#subform[0].EmployeeName',
                                $("#lname").val()+' '+$("#fname").val()
                              )
                   });
           });
   ```

