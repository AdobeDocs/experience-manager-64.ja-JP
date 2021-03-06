---
title: カスタムツールバーレイアウトの作成
seo-title: Creating custom toolbar layout
description: フォームのツールバーレイアウトを指定できます。ツールバーレイアウトは、フォーム上のツールバーのコマンドとレイアウトを定義します。
seo-description: You can specify a toolbar layout for the form. The toolbar layout defines the commands and the layout of the toolbar on the form.
uuid: da60342c-f802-4264-9da4-c333df9359c2
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
discoiquuid: c69bb229-d680-4a55-9b2d-cd5ad0f83a9e
exl-id: 1b273437-8d71-4224-bdcd-0ae522ae8913
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 79%

---

# カスタムツールバーレイアウトの作成 {#creating-custom-toolbar-layout}

## ツールバーレイアウト {#layout}

アダプティブフォームの作成時に、フォームのツールバーレイアウトを指定できます。ツールバーレイアウトは、フォーム上のツールバーのコマンドとレイアウトを定義します。

ツールバーレイアウトは、複雑な JavaScript と CSS コードによるクライアントサイドのプロセッシングに大きく依存しています。このコードの提供を編成および最適化することが厄介な問題となることがあります。この問題への対処に役立つように、AEM では、クライアント側ライブラリフォルダーが提供されています。これにより、クライアント側コードをリポジトリに格納し、カテゴリ別に整理して、それぞれのコードカテゴリをクライアントに保存するタイミングと方法を定義することができます。その後、クライアント側ライブラリシステムにより、最終的な Web ページで、正しいコードを読み込むための正しいリンクが作成されます。詳細については、「[AEM におけるクライアントサイドライブラリの機能](/help/sites-developing/clientlibs.md)」を参照してください。

![ツールバーのサンプルレイアウト](assets/default_toolbar_layout.png)
**図：** *ツールバーのサンプルレイアウト*

アダプティブフォームには、購入してすぐに使える一連のレイアウトが含まれています。

![すぐに使用できるツールバーレイアウト ](assets/toolbar1.png)
**図：** *すぐに使用できるツールバーレイアウト*

カスタムのツールバーレイアウトを作成することもできます。

次の手順では、カスタムツールバーを作成する手順を示します。ここでは、3 つのアクションがツールバーに表示され、その他のアクションはツールバーのドロップダウンリストに表示されます。

付属のコンテンツパッケージには、以下に示すコード全体が含まれています。コンテンツパッケージをインストールしたら、を開きます。 `/content/forms/af/CustomLayoutDemo.html` をクリックして、カスタムツールバーレイアウトのデモを表示します。

CustomToolbarLayoutDemo.zip

[ダウンロード](assets/customtoolbarlayoutdemo.zip)
デモカスタムツールバーレイアウト

## カスタムツールバーレイアウトを作成するには {#layout-1}

1. カスタムツールバーレイアウトを入れておくフォルダーを作成します。例：

   `/apps/customlayout/toolbar`

   カスタムレイアウトを作成するには、次のフォルダーに用意されている既成のツールバーレイアウトの 1 つを使用（およびカスタマイズ）できます。

   `/libs/fd/af/layouts/toolbar`

   例えば、 `mobileFixedToolbarLayout` ノードを `/libs/fd/af/layouts/toolbar` フォルダーを `/apps/customlayout/toolbar` フォルダー。

   また、toolbarCommon.jsp を `/apps/customlayout/toolbar` フォルダー。

   >[!NOTE]
   >
   >カスタムレイアウトを維持するために作成したフォルダーは、 `apps` フォルダー。

1. コピーしたノードの名前を変更します。 `mobileFixedToolbarLayout`、 `customToolbarLayout.`

   また、ノードのための適切な説明も与えます。例えば、ノードの jcr:description を&#x200B;**ツールバーのカスタムレイアウト** に変更します。

   ノードの `guideComponentType` プロパティによりレイアウトタイプが決まります。この場合、レイアウトタイプはツールバーなので、ツールバーレイアウト選択ドロップダウンに表示されます。

   ![適切な説明を付けたノード](assets/toolbar3.png)

   適切な説明を付けたノード

   新しいカスタムツールバーレイアウトは、**アダプティブフォームツールバー**&#x200B;ダイアログ設定に表示されます。

   ![使用可能なツールバーレイアウトのリスト](assets/toolbar4.png)

   使用可能なツールバーレイアウトのリスト

   >[!NOTE]
   >
   >前のステップで更新された説明は、レイアウトドロップダウンリストに表示されます。

1. このカスタムツールバーレイアウトを選択し、「OK」をクリックします。

   clientlib（javascript と css）を `/etc/customlayout` ノードに追加し、clientlib の参照を `customToolbarLayout.jsp`.

   ![customToolbarLayout.css ファイルのパス](assets/toolbar_3.png)

   customToolbarLayout.css ファイルのパス

   サンプル `customToolbarLayout.jsp`:

   ```php
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <cq:includeClientLib categories="customtoolbarlayout" />
   <c:if test="${isEditMode}">
           <cq:includeClientLib categories="customtoolbarlayoutauthor" />
   </c:if>
   <div class="guidetoolbar mobileToolbar mobilecustomToolbar" data-guide-position-class="guide-element-hide">
       <div data-guide-scroll-indicator="true"></div>            
       <%@include file="../toolbarCommon.jsp" %>
   </div>
   ```

   >[!NOTE]
   >
   >レイアウトの guidetoolbar クラスを追加します。ツールバー用の直ちに使用可能なスタイリングは、guidetoolbar クラスに関して定義されます。

   サンプル `toolBarCommon.jsp`:

   ```php
   <%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions"%>
   <%--------------------  
   This code iterates over all the tool bar items using the guideToolbar bean.
   If the number of toolbar items are more than 3, then we create a dropdown menu using bootstrap for other actions present in the toolbar.
   In both desktop and mobile devices, the layout is different.    
   ---------------------------------%>
   
   <c:forEach items="${guideToolbar.items}" var="toolbarItem" varStatus="loop">
       <c:choose>
         <c:when test="${loop.index gt 2}">
      <c:choose>
       <c:when test="${loop.index eq 3}">
                     <div class="btn-group dropdown">   
                       <button type="button" class="btn btn-primary dropdown-toggle label" data-toggle="dropdown">Actions <span class="caret"></span></button>
                       <button type="button" class="btn btn-primary dropdown-toggle icon" data-toggle="dropdown"><span class="glyphicon glyphicon-th-list"></span></button>
             <ul class="dropdown-menu" role="menu">
                           <li>
                               <div id="${toolbarItem.id}_guide-item">
                                 <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                              </div>
                           </li>
                           <c:if test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                                </ul>
                                </div>
                           </c:if>
       </c:when>
       <c:when test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                          <li>
                                     <div id="${toolbarItem.id}_guide-item">
                                         <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                                     </div>
                           </li>
                       </ul>
                     </div>
   
       </c:when>
       <c:otherwise>
         <li>
          <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
          </div>
         </li>
       </c:otherwise>
      </c:choose>
         </c:when>
         <c:otherwise>         
     <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
        </div>
         </c:otherwise>
    </c:choose>   
   </c:forEach>
   ```

   CSS は clientlib ノード内に存在します:

   ```css
   .mobilecustomToolbar .dropdown {
       display: inline-block;    
   }
   
   .mobilecustomToolbar .dropdown {
       float: right;   
   }
   
   .mobilecustomToolbar .dropdown > button {
      padding: 6px 12px;  
   }         
   
   .mobilecustomToolbar .dropdown .guideFieldWidget, .mobilecustomToolbar .dropdown .guideFieldWidget button {
       width: 100%;   
   }         
   
   .mobilecustomToolbar .dropdown .caret{
       border-bottom: 6px solid;
       border-right: 6px solid transparent;
       border-left: 6px solid transparent;
    border-top: transparent;                                     
   }
   
   .mobilecustomToolbar .dropdown-menu{
    top: auto;
    bottom: 100%;                            
   }
   
   .mobilecustomToolbar .btn-group {            
    vertical-align: super;            
   }
   
   .mobilecustomToolbar .glyphicon {
    font-size: 24px;
   }
   
   @media (max-width: 767px){                                       
   
    .mobilecustomToolbar .dropdown .guideButton .iconButton-icon {
      display: none;
       }  
   
       .mobilecustomToolbar .dropdown .guideButton .iconButton-label {
      display: inline-block;
       } 
   
       .mobilecustomToolbar .dropdown .guideButton button {
      background-color: #013853;
       }
   
    .mobilecustomToolbar .btn-group {            
     vertical-align: top;            
    }    
   
   }
   ```

>[!NOTE]
>
>前のステップで更新された説明は、レイアウトドロップダウンリストに表示されます。

![カスタムレイアウトツールバーのデスクトップ表示](assets/toolbar_1.png)
**図：** *カスタムレイアウトツールバーのデスクトップ表示*
