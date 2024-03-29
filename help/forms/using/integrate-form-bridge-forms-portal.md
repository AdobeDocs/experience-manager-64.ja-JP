---
title: Form Bridge と HTML5 フォームのカスタムポータルの統合
seo-title: Integrating Form Bridge with custom portal for HTML5 forms
description: FormBridge API を使用して、HTMLページからフォームフィールドの値を取得または設定し、フォームを送信することができます。
seo-description: You can use the FormBridge API to get or set the values of form fields from the HTML page and submit the form.
uuid: 09f2189f-d584-4b84-895e-22833b6b17e3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: e0608649-bd49-4f40-bc1b-821c9b208883
feature: Mobile Forms
exl-id: bf4ae163-5d89-48fb-9bc4-182281b28f35
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 24%

---

# Form Bridge と HTML5 フォームのカスタムポータルの統合 {#integrating-form-bridge-with-custom-portal-for-html-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

FormBridge は、フォームを操作するHTML5 forms ブリッジ API です。 FormBridge API リファレンスについては、[FormBridge API リファレンス](/help/forms/using/form-bridge-apis.md)を参照してください。

FormBridge API を使用して、HTMLページからフォームフィールドの値を取得または設定し、フォームを送信することができます。 例えば、API を使用してウィザードのようなエクスペリエンスを作成できます。

既存のHTMLアプリケーションは、FormBridge API を利用してフォームを操作し、HTMLページに埋め込むことができます。 次の手順を使用して、Form Bridge API を使用してフィールドの値を設定できます。

## Web ページへのHTML5 フォームの統合 {#integrating-html-forms-to-a-web-page}

1. **プロファイルの選択またはプロファイルの作成**

   1. CRX DE インターフェイスで、`https://[server]:[port]/crx/de` に移動します。
   1. 管理者の資格情報を使用してログインします。
   1. プロファイルを作成するか、既存のプロファイルを選択します。

      プロファイルの作成方法について詳しくは、[新しいプロファイルの作成](/help/forms/using/custom-profile.md)を参照してください。

1. **HTMLプロファイルの変更**

   XFA ランタイム、XFA ロケールライブラリ、および XFA フォームHTMLスニペットをプロファイルレンダラーに含め、Web ページをデザインし、フォームを Web ページ内に配置します。

   例えば、次のコードスニペットを使用して、2 つの入力フィールドとフォームを含むアプリを作成し、フォームと外部アプリの間のやり取りを示します。

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
   >**9 行目**&#x200B;には、このページをデザインするための、CSS スタイルと JavaScript ファイルの追加 JSP 参照が含まれています。
   >
   >この &lt;div id=&quot;rightdiv&quot;> ～に追い付く **18 行目** には、XFA フォームのHTMLスニペットが含まれています。
   ページは、次の 2 つのコンテナにスタイル設定されます。 **left** および **右**. 右側のコンテナにはフォームがあります。 左側のコンテナには、2 つの入力フィールドと、外部HTMLページの一部があります。
   次のスクリーンショットは、フォームがブラウザーでどのように表示されるかを示しています。

   ![ポータル](assets/portal.jpg)

   左側は **HTMLページ**. フィールドを含む右側は、 **xfa フォーム**.

1. **ページからのフォームフィールドへのアクセス**

   次に、フォームフィールドに値を設定するために追加できるサンプルスクリプトを示します。

   たとえば、「**名前 (名)**」と「**名前 (姓)**」のフィールドにある値を使用して **EmployeeName**&#x200B;を設定する場合、**window.formBridge.setFieldValue** 関数を呼び出します。

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
