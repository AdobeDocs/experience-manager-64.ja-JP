---
title: アダプティブフォームのカスタムレイアウトコンポーネントの作成
seo-title: Creating custom layout components for adaptive forms
description: アダプティブフォームのカスタムレイアウトコンポーネントを作成する手順です。
seo-description: Procedure to create custom layout components for adaptive forms.
uuid: 09a0cacc-d693-46dc-90a3-254d1878a68a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
discoiquuid: 102718cb-592a-4a5c-89a6-ad4d56f3d547
exl-id: ea21b47f-25fc-48cb-a5dc-d0433146b40d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 64%

---

# アダプティブフォームのカスタムレイアウトコンポーネントの作成 {#creating-custom-layout-components-for-adaptive-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 前提条件 {#prerequisite}

カスタムレイアウトの作成/使用を可能にするレイアウトに関する知識 詳しくは、 [パネルレイアウトの変更](/help/forms/using/layout-capabilities-adaptive-forms.md).

## アダプティブフォームパネルレイアウトコンポーネント {#adaptive-form-panel-layout-component}

アダプティブフォームのパネルレイアウトコンポーネントは、ユーザーインターフェイスに対する、パネル内のアダプティブフォームのコンポーネントのレイアウト方法を制御します。

## カスタムパネルレイアウトの作成 {#creating-a-custom-panel-layout}

1. 場所 `/crx/de` に移動します。
1. パネルレイアウトを場所 `/libs/fd/af/layouts/panel` （例えば、`tabbedPanelLayout` ）から `/apps` （例えば、`/apps/af-custom-layout`）にコピーします。
1. コピーしたレイアウトの名前を `customPanelLayout` に変更します。ノード `qtip` および `jcr:description` のプロパティを変更します。例えば、それらを `Custom layout - Toggle tabs` に変更します。

![カスタムパネルレイアウトの CRX DE スナップショット](assets/custom.png)

>[!NOTE]
>
>プロパティ `guideComponentType` の値を `fd/af/layouts/panel` に設定すると、レイアウトがパネルレイアウトになります。

1. 新しいレイアウトにあるファイル `tabbedPanelLayout.jsp` の名前を customPanelLayout.jsp に変更します。
1. 新しいスタイルおよび動作を追加するには、`etc` ノードでクライアントライブラリを作成します。例えば、/etc/af-custom-layout-clientlib でノードクライアントライブラリを作成します。このノードにカテゴリのプロパティ af.panel.custom を設定します。このプロパティには次の .css ファイルと .js ファイルがあります。

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

1. アピアランスと動作を強化するには、`client library` を追加します。

   さらに、.jps ファイルに含まれるスクリプトのパスを更新します。例えば、`customPanelLayout.jsp` ファイルを次のように更新します。

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

   `/apps/af-custom-layout/customPanelLayout/defaultNavigatorLayout.jsp` ファイル：

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

1. アダプティブフォームをオーサリングモードで開きます。 定義したパネルレイアウトが、パネルレイアウトを設定するためのリストに追加されます。

   ![パネルレイアウトリストに表示されたカスタムパネルレイアウト](assets/auth-layt.png) ![カスタムパネルレイアウトを使用したアダプティブフォームのスクリーンショット](assets/s1.png) ![カスタムレイアウトの切り替え機能を示したスクリーンショット](assets/s2.png)

カスタムパネルレイアウトとカスタムパネルレイアウトを使用したアダプティブフォームのサンプル ZIP ファイル。

[ファイルを入手](assets/af-custom-layout.zip)
