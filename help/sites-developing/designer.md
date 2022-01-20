---
title: デザインとデザイナー
seo-title: Designs and the Designer
description: Web サイト用に、また AEM で、デザインの作成が必要になります。その場合はデザイナーを使用します
seo-description: You will need to create a design for your website and in AEM, you do so by using the Designer
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
exl-id: 8a4fc7c7-03bc-44db-93f1-dbd76fc9dbd7
source-git-commit: 9ae048ca2811a56c5d6f0b2415fcfcccc4384dbf
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 43%

---

# デザインとデザイナー{#designs-and-the-designer}

>[!CAUTION]
>
>この記事では、クラシック UI に基づく Web サイトの作成方法について説明します。 アドビでは、[AEM Sites の開発の手引き](/help/sites-developing/getting-started.md)で詳しく説明しているように、Web サイトに最新の AEM テクノロジーを利用することをお勧めします。

デザイナーは、 [クラシック UI](/help/release-notes/touch-ui-features-status.md) AEMの

>[!NOTE]
>
>Web アクセシビリティについて詳しくは、[AEM と Web アクセシビリティのガイドライン](/help/managing/web-accessibility.md)を参照してください。

## デザイナーの使用 {#using-the-designer}

デザインは、 **デザイン** セクション **ツール** タブ：

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

ここで、デザインの格納に必要な構造を作成し、必要なカスケーディングスタイルシート（CSS）および画像をアップロードできます。

デザインは、以下の場所に格納されます。 `/apps/<your-project>`. Web サイトに使用するデザインへのパスは、 `cq:designPath` プロパティ `jcr:content` ノード。

![chlimage_1-74](assets/chlimage_1-74.png)

>[!NOTE]
>
>デザインモードのページ上でおこなわれたすべての変更は、サイトのデザインノードの下に保持され、同じデザインを持つすべてのページに自動的に適用されます。

## 必要なもの {#what-you-will-need}

デザインを実現するには、以下が必要です。

**CSS**  — カスケーディングスタイルシートは、ページ上の特定の領域の形式を定義します。

**画像**  — 背景、ボタンなどの機能に使用する画像。

### Web サイトをデザインする際の考慮事項 {#considerations-when-designing-your-website}

Web サイトを開発する際は、画像と CSS ファイルをの下に保存することを強くお勧めします。 `/apps/<your-project>` 次のスニペットで説明するように、現在のデザインに基づいてリソースを参照できます。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

前述の例には、次のようないくつかの利点があります。

* 別々のデザインパスを使用しているサイトごとに、コンポーネントのルックアンドフィールを変化させることができます。
* Web サイトの再設計は、サイトのルートにある別のノードにデザインパスを指すことで、 `design/v1` から `design/v2.`

* `/etc/designs` および `/content` は、ブラウザーが外部ユーザーの保護を目にする唯一の外部 URL で、ユーザーの下に何があるかを知るためのものです `/apps` ツリー。 上記の URL の利点は、アセットの公開をいくつかの異なる場所に制限するので、システム管理者がより高いセキュリティを設定するのに役立ちます。
