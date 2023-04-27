---
title: Analytics と外部プロバイダー
seo-title: Analytics with External Providers
description: 外部プロバイダーとの Analytics について説明します。
seo-description: Learn about Analytics with External Providers.
uuid: bea8ec38-a190-46f9-a5fa-8d65321fdf20
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: bf8fd156-4be9-43f8-8948-cf7f91c25f1b
exl-id: 6d906c2b-c8bc-4d54-9887-8aaeb6cc83d3
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 70%

---

# Analytics と外部プロバイダー{#analytics-with-external-providers}

Analytics は、Web サイトがどのように使用されているかに関する、重要で興味深い情報を提供できます。

様々な標準提供の設定が、次のような適切なサービスとの統合で利用できます。

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

また、 **汎用 Analytics スニペット** をクリックして、新しいサービス設定を定義します。

その後、情報は、Web ページに追加されるコードの小さなスニペットを使用して収集されます。 次に例を示します。

>[!CAUTION]
>
>スクリプトは、`script` タグで囲まないようにしてください。

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

このようなスニペットを使用すると、データを収集してレポートを生成できます。 収集される実際のデータは、プロバイダーと、使用する実際のコードスニペットによって異なります。 統計の例を次に示します。

* 長期間の訪問者数
* 訪問したページ数
* 使用する検索語句
* ランディングページ

>[!CAUTION]
>
>Geometrixx-Outdoors デモサイトは、ページプロパティで提供した属性が、対応する `js` スクリプトの HTML ソースコード（`</html>` 終了タグのすぐ上）に追加されます。
>
>
>独自の `/apps` がデフォルトページコンポーネント（`/libs/foundation/components/page`）から継承しない場合、ユーザー（またはその開発者）が対応する `js` スクリプトが含まれていること（例えば、`cq/cloudserviceconfigs/components/servicescomponents` が含まれているか、同様のメカニズムが使用されているか）を確認する必要があります。
>
>
>これをしないと、どのサービス（汎用、Analytics、Target など）も機能しません。

## 汎用スニペットを使用した新しいサービスの作成 {#creating-a-new-service-with-a-generic-snippet}

基本設定の場合：

1. **ツール**&#x200B;コンソールを開きます。

1. 左側のパネルから、**クラウドサービス設定**&#x200B;を展開します。

1. 「**汎用分析スニペット**」をダブルクリックしてページを開きます。

   ![analytics_genericoverview](assets/analytics_genericoverview.png)

1. + をクリックし、ダイアログを使用して新しい設定を追加します。最小限の割り当てでは、名前（例：google analytics）を試用します。

   ![analytics_addconfig](assets/analytics_addconfig.png)

1. 「**作成**」をクリックすると、スニペットダイアログがすぐに開くので、適切な JavaScript スニペットをフィールドに貼り付けます。

   ![analytics_snippet](assets/analytics_snippet.png)

1. 「**OK**」をクリックして保存します。

## ページでの新しいサービスの使用 {#using-your-new-service-on-pages}

今作成したサービス設定は、必要なページで使用するように設定する必要があります。

1. ページに移動します。

1. サイドキックから&#x200B;**ページプロパティ**&#x200B;を開き、「**クラウドサービス**」タブを選択します。

1. 「**サービスを追加**」をクリックし、必要なサービス（例：**汎用分析スニペット**）を選択します。

   ![analytics_selectservice](assets/analytics_selectservice.png)

1. 「**OK**」をクリックして保存します。

1. 「**クラウドサービス**」タブに戻されます。**汎用分析スニペット**&#x200B;が、`Configuration reference missing` のメッセージと共に表示されます。ドロップダウンリストを使用して、具体的なサービスインスタンス（例：google-analytics）を選択します。

   ![analytics_selectspecificservice](assets/analytics_selectspecificservice.png)

1. 「**OK**」をクリックして保存します。

   これで、ページのページソースを表示した場合に、スニペットを表示できます。

   適切な期間が経過すると、収集された統計を表示できます。

   >[!NOTE]
   >
   >設定が子ページを持つページに添付されている場合、サービスはそれらにも継承されます。
