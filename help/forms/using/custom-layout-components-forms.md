---
title: アダプティブフォームのカスタムレイアウトコンポーネントの作成
seo-title: Creating custom layout components for adaptive forms
description: アダプティブフォームのカスタムレイアウトコンポーネントの作成手順
seo-description: Procedure to create custom layout components for adaptive forms.
uuid: 09a0cacc-d693-46dc-90a3-254d1878a68a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
discoiquuid: 102718cb-592a-4a5c-89a6-ad4d56f3d547
exl-id: ea21b47f-25fc-48cb-a5dc-d0433146b40d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 57%

---

# アダプティブフォームのカスタムレイアウトコンポーネントの作成 {#creating-custom-layout-components-for-adaptive-forms}

## 前提条件 {#prerequisite}

カスタムレイアウトの作成および使用を可能にするレイアウトについての知識が必要です。「[パネルレイアウトの変更](/help/forms/using/layout-capabilities-adaptive-forms.md)」を参照してください。

## アダプティブフォームのパネルレイアウトのコンポーネント {#adaptive-form-panel-layout-component}

アダプティブフォームのパネルレイアウトのコンポーネントは、ユーザーインターフェイスに考慮して、パネル内のアダプティブフォームのコンポーネントをどのようにレイアウトするかをコントロールします。

## カスタムパネルレイアウトの作成 {#creating-a-custom-panel-layout}

1. 場所に移動します。 `/crx/de`.
1. 次の場所からパネルレイアウトをコピーする `/libs/fd/af/layouts/panel` ( 例： `tabbedPanelLayout`) から `/apps` ( 例： `/apps/af-custom-layout`) をクリックします。
1. コピーしたレイアウトの名前をに変更します。 `customPanelLayout`. ノードのプロパティを変更する `qtip` および `jcr:description`. 例えば、次のように変更します。 `Custom layout - Toggle tabs`.

![カスタムパネルレイアウトの CRX DE スナップショット](assets/custom.png)

>[!NOTE]
>
>プロパティの設定 `guideComponentType`値に `fd/af/layouts/panel` は、レイアウトがパネルレイアウトであることを判別します。

1. ファイル名を変更 `tabbedPanelLayout.jsp` 新しいレイアウトの下で、customPanelLayout.jsp.
1. 新しいスタイルおよび動作を追加するには、`etc` ノードでクライアントライブラリを作成します。例えば、/etc/af-custom-layout-clientlib の場所で、ノード client-library を作成します。 このノードにカテゴリのプロパティ af.panel.custom を設定します。このプロパティには次の .css ファイルと .js ファイルがあります。

   ```css
   /** CSS defining new styles used by custom layout **/
   
   .menu-nav {
       background-color: rgb(198, 38, 76);
       height: 30px;
    width: 30px;
    font-size: 2em;
    color: white;
       -webkit-transition: -webkit-transform 1s;  /* For Safari 3.1 to 6.0 */
    transition: transform 1s;
   }
   
   .tab-content {
    border: 1px solid #08b1cf;
   }
   
   .custom-navigation {
       -webkit-transition: width 1s, height 1s, -webkit-transform 1s;  /* For Safari 3.1 to 6.0 */
    transition: width 1s, height 1s, transform 1s;
   }
   
   .panel-name {
       padding-left: 30px;
       font-size: 20px;
   }
   
   @media (min-width: 992px) {
    .nav-close {
     width: 0px;
       }
   }
   
   @media (min-width: 768px) and (max-width: 991px) {
    .nav-close {
     height: 0px;
       }
   }
   
   @media (max-width: 767px) {
    .menu-nav, .custom-navigation {
        display: none;
       }
   }
   ```

   ```
   /** function for toggling the navigators **/
   var toggleNav = function () {
   
       var nav = $('.custom-navigation');
       if (nav) {
           nav.toggleClass('nav-close');
       }
   }
   
   /** function to populate the panel title **/
   $(window).on('load', function() {
       if (window.guideBridge) {
           window.guideBridge.on("elementNavigationChanged",
           function (evntName, evnt) {
                       var activePanelSom = evnt.newText,
                           activePanel = window.guideBridge._guideView.getView(activePanelSom);
                       $('.panel-name').html(activePanel.$itemNav.find('a').html());
                   }
           );
       }
   });
   ```

1. 外観と動作を強化するには、 `client library`.

   さらに、.jps ファイルに含まれるスクリプトのパスを更新します。例えば、 `customPanelLayout.jsp` ファイルの内容は次のとおりです。

   ```
   <%-- jsp encapsulating navigator container and panel container divs --%>
   
   <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
   <cq:includeClientLib categories="af.panel.custom"/>
   <div>
       <div class="row">
           <div class="col-md-2 col-sm-2 hidden-xs menu-nav glyphicon glyphicon-align-justify" onclick="toggleNav();"></div>
           <div class="col-md-10 col-sm-10 hidden-xs panel-name"></div>
       </div>
       <div class="row">
           <div class="col-md-2 hidden-xs guide-tab-stamp-list custom-navigation">
               <cq:include script = "/apps/af-custom-layout/customPanelLayout/defaultNavigatorLayout.jsp" />
           </div>
           <div  class="col-md-10">
               <c:if test="${fn:length(guidePanel.description) > 0}">
                   <div class="<%=GuideConstants.GUIDE_PANEL_DESCRIPTION%>">
                       ${guide:encodeForHtml(guidePanel.description,xssAPI)}
                           <cq:include script="/libs/fd/af/components/panel/longDescription.jsp"/>
                   </div>
               </c:if>
               <cq:include script = "/apps/af-custom-layout/customPanelLayout/panelContainer.jsp"/>
           </div>
       </div>
   </div>
   ```

   この `/apps/af-custom-layout/customPanelLayout/defaultNavigatorLayout.jsp` ファイル：

   ```
   <%-- jsp governing the navigation part --%>
   
   <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
   <%@ page import="com.adobe.aemds.guide.utils.StyleUtils" %>
   <%-- navigation tabs --%>
   <ul id="${guidePanel.id}_guide-item-nav-container" class="tab-navigators tab-navigators-vertical in"
       data-guide-panel-edit="reorderItems" role="tablist">
       <c:forEach items="${guidePanel.items}" var="panelItem">
           <c:set var="isNestedLayout" value="${guide:hasNestablePanelLayout(guidePanel,panelItem)}"/>
           <li id="${panelItem.id}_guide-item-nav" title="${guide:encodeForHtmlAttr(panelItem.navTitle,xssAPI)}" data-path="${panelItem.path}" role="tab" aria-controls="${panelItem.id}_guide-item">
               <c:set var="panelItemCss" value="${panelItem.cssClassName}"/>
               <% String panelItemCss = (String) pageContext.getAttribute("panelItemCss");%>
               <a data-guide-toggle="tab" class="<%= StyleUtils.addPostfixToClasses(panelItemCss, "_nav") %> guideNavIcon nested_${isNestedLayout}">${guide:encodeForHtml(panelItem.navTitle,xssAPI)}</a>
               <c:if test="${isNestedLayout}">
                   <guide:initializeBean name="guidePanel" className="com.adobe.aemds.guide.common.GuidePanel"
                       resourcePath="${panelItem.path}" restoreOnExit="true">
                       <sling:include path="${panelItem.path}"
                                      resourceType="/apps/af-custom-layout/customPanelLayout/defaultNavigatorLayout.jsp"/>
                   </guide:initializeBean>
               </c:if>
               <em></em>
           </li>
       </c:forEach>
   </ul>
   ```

   更新済み `/apps/af-custom-layout/customPanelLayout/panelContainer.jsp`:

   ```
   <%-- jsp governing the panel content --%>
   
   <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
   
   <div id="${guidePanel.id}_guide-item-container" class="tab-content">
       <c:if test="${guidePanel.hasToolbar && (guidePanel.toolbarPosition == 'Top') }">
           <sling:include path="${guidePanel.toolbar.path}"/>
       </c:if>
   
   <c:forEach items="${guidePanel.items}" var="panelItem">
       <div class="tab-pane" id="${panelItem.id}_guide-item" role="tabpanel">
           <c:set var="isNestedLayout" value="${guide:hasNestablePanelLayout(guidePanel,panelItem)}"/>
           <c:if test="${isNestedLayout}">
               <c:set var="guidePanelResourceType" value="/apps/af-custom-layout/customPanelLayout/panelContainer.jsp" scope="request"/>
           </c:if>
           <sling:include path="${panelItem.path}" resourceType="${panelItem.resourceType}"/>
       </div>
   </c:forEach>
   <c:if test="${guidePanel.hasToolbar && (guidePanel.toolbarPosition == 'Bottom')}">
       <sling:include path="${guidePanel.toolbar.path}"/>
   </c:if>
   </div>
   ```

1. オーサリングモードでアダプティブフォームを開きます。定義したパネルレイアウトがパネルレイアウト設定用のリストに追加されます。

   ![カスタムパネルレイアウトがパネルレイアウトリストに表示される](assets/auth-layt.png) ![カスタムパネルレイアウトを使用したアダプティブフォームのスクリーンショット](assets/s1.png) ![カスタムレイアウトの切り替え機能を示すスクリーンショット](assets/s2.png)

カスタムパネルレイアウトとカスタムパネルレイアウトを使用したアダプティブフォームのサンプル ZIP ファイル。

[ファイルを入手](assets/af-custom-layout.zip)
