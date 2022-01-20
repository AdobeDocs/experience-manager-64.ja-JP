---
title: Form Bridge と HTML5 フォームのカスタムポータルの統合
seo-title: Integrating Form Bridge with custom portal for HTML5 forms
description: FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定できます。
seo-description: You can use the FormBridge API to get or set the values of form fields from the HTML page and submit the form.
uuid: 09f2189f-d584-4b84-895e-22833b6b17e3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: e0608649-bd49-4f40-bc1b-821c9b208883
feature: Mobile Forms
exl-id: bf4ae163-5d89-48fb-9bc4-182281b28f35
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 79%

---

# Form Bridge と HTML5 フォームのカスタムポータルの統合 {#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge はフォームとのやりとりを可能にする HTML5 フォームのブリッジ API です。FormBridge API リファレンスについては、 [FormBridge API リファレンス](/help/forms/using/form-bridge-apis.md).

FormBridge API を使用して、HTML ページからフォームフィールドの値を取得または設定できます。たとえば、API を使用してウィザードのような経験を築くことができます。

既存の HTML アプリケーションは FormBridge API を利用してフォームとやりとりし、それを HTML ページに埋め込むことができます。次の手順を使用して、Form Bridge API を使用してフィールドの値を設定できます。

## HTML5 フォームと Web ページの統合 {#integrating-html-forms-to-a-web-page}

1. **プロファイルの選択またはプロファイルの作成**

   1. CRX DE インターフェイスで、次の場所に移動します。 `https://[server]:[port]/crx/de`.
   1. 管理者の資格情報を使用してログインします。
   1. プロファイルを作成するか、既存のプロファイルを選択します。

      プロファイルの作成方法について詳しくは、 [新しいプロファイルの作成](/help/forms/using/custom-profile.md).

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
   >この **行 9**&#x200B;には、ページをデザインするための CSS スタイルおよび JavaScript ファイル用の追加の JSP 参照が含まれます。
   >
   >**18 行目**&#x200B;の &lt;div id=&quot;rightdiv&quot;> タグには XFA フォームの HTML スニペットが含まれています。
   ページは 2 つのコンテナ、**left** と **right** にスタイル設定されています。right コンテナにはフォームがあります。left コンテナには 2 つの入力フィールドと外部 HTML ページの一部があります。
   次のスクリーンショットは、フォームがどのようにブラウザーで表示されるかを示しています。

   ![ポータル](assets/portal.jpg)

   左側は **HTML ページ**&#x200B;の一部です。右側でフィールドを含んでいるのは **xfa フォーム**&#x200B;です。

1. **ページからのフォームフィールドへのアクセス**

   次にあるのは、フォームフィールドの値を設定するために追加できるサンプルのスクリプトです。

   例えば、 **EmployeeName** フィールドの値の使用 **名** および **姓**、 **window.formBridge.setFieldValue** 関数に置き換えます。

   同様に、 **window.formBridge.getFieldValue **API を呼び出すことで、値を読み取ることができます。

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
