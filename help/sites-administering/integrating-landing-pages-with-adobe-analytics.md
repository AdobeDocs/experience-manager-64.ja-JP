---
title: ランディングページと Adobe Analytics の統合
seo-title: Integrating Landing Pages with Adobe Analytics
description: ランディングページと Adobe Analytics を統合する方法について説明します。
seo-description: Learn how to integrate landing pages with Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
exl-id: 2923ae94-375a-4c44-a08f-f992eb08000a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 46%

---

# ランディングページと Adobe Analytics の統合{#integrating-landing-pages-with-adobe-analytics}

AEMは、ランディングページソリューションを [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) 次のコールトゥアクション (CTA) コンポーネントを使用する。

1. クリックスルーコンポーネント
1. グラフィックリンクコンポーネント

これらのコンポーネントは、Adobe Analytics変数（トラフィック、コンバージョン変数）および成功イベントを使用してマッピングでき、Adobe Analyticsに情報を送信するための特定の属性を公開します。

## 前提条件 {#prerequisites}

Adobeでは、 [既存のAEMとAdobe Analyticsの統合](/help/sites-administering/adobeanalytics.md) を参照して、この統合の仕組みを理解してください。

## マッピングに使用できるコンポーネント {#components-available-for-mapping}

AEMで、 **コールトゥアクション** コンポーネント — **ClickThroughLink** および **GraphicalLink**  — サイドキックに表示され、Adobe Analytics変数にマッピングできます。

![chlimage_1-21](assets/chlimage_1-21.jpeg)

### Adobe Analytics へのランディングページコンポーネントのマッピング {#mapping-landing-page-components-to-adobe-analytics}

ランディングページコンポーネントを Adobe Analytics にマッピングするには：

1. Adobe Analytics設定を作成し、新しいフレームワークを作成したら、ドロップダウンメニューから適切なレポートスイートを選択します。 この結果、Adobe Analytics の変数が取得され、コンテンツファインダーに表示されます。
1. コールトゥアクション（CTA）コンポーネントを、サイドキックからページ中央のマッピング領域の適切な場所にドラッグ＆ドロップします。

<table> 
 <tbody>
  <tr>
   <td><strong>コンポーネント名</strong></td> 
   <td><strong>公開される属性</strong></td> 
   <td><strong>属性の意味</strong></td> 
  </tr>
  <tr>
   <td><strong>CTA クリックスルーリンク</strong></td> 
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td> 
   <td>リンクのラベルまたはリンクのテキスト </td> 
  </tr>
  <tr>
   <td><br type="_moz" /> </td> 
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td> 
   <td>リンクをクリックしたときの移動先 </td> 
  </tr>
  <tr>
   <td><br type="_moz" /> </td> 
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td> 
   <td>クリックイベント </td> 
  </tr>
  <tr>
   <td><strong>CTA グラフィックリンク</strong></td> 
   <td><i>eventdata.clicktroughImageLabel</i> <br /> </td> 
   <td>CTA 画像のタイトル </td> 
  </tr>
  <tr>
   <td><br type="_moz" /> </td> 
   <td><i>eventdata.clicktroughImageTarget</i> <br /> </td> 
   <td>リンクを含む画像をクリックしたときの移動先</td> 
  </tr>
  <tr>
   <td><br type="_moz" /> </td> 
   <td><i>eventdata.clicktroughImageAsset</i> <br /> </td> 
   <td>リポジトリ内の画像アセットへのパス </td> 
  </tr>
  <tr>
   <td><br type="_moz" /> </td> 
   <td><i>eventdata.events.clicktroughImageClick</i> <br /> </td> 
   <td>クリックイベント</td> 
  </tr>
 </tbody>
</table>

1. コンテンツファインダーで、これらの公開される属性と Adobe Analytics 変数をマッピングします。これで、フレームワークを使用する準備が整いました。
1. これで、新しいランディングページを作成するか、既存の CTA コンポーネントを含む既存のランディングページを開いて、 **Cloud Services** タブ **ページプロパティ** サイドキック（タッチ操作向け UI）で、 **プロパティを開く** をクリックし、 **Cloud Services**) をクリックし、ランディングページで使用するフレームワークを設定します。 ドロップダウンリストからフレームワークを選択します。

   ![chlimage_1-25](assets/chlimage_1-25.png)

1. ランディングページを含むフレームワークを設定したら、実装されたコンポーネントが使用できるようになり、CTA でのクリックがすべて Adobe Analytics に記録されます。
