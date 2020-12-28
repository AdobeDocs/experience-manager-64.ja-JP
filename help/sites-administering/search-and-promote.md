---
title: Adobe Search&Promote との統合
seo-title: Adobe Search&Promote との統合
description: Adobe Search&Promote と統合する方法について説明します。
seo-description: Adobe Search&Promote と統合する方法について説明します。
uuid: ddc4510a-9bd1-4238-a8a8-5f4f563edd8d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: 87e62346-98d5-40ec-a3ef-904adf667425
translation-type: tm+mt
source-git-commit: cdec5b3c57ce1c80c0ed6b5cb7650b52cf9bc340
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 53%

---


# Adobe Search&amp;Promote との統合{#integrating-with-adobe-search-promote}

Web サイトから Adobe Search&amp;Promote サービスを呼び出すには、次のタスクを実行します。

1. クラウドの URL を指定します。
1. Search&amp;Promote サービスへの接続を設定します。
1. &lt;a0追加/>サイドキック]へのSearch&amp;Promoteコンポーネント。[!UICONTROL 
1. コンポーネントを使用して、コンテンツを作成します（[Web ページへの Search&amp;Promote 機能の追加](/help/sites-authoring/search-and-promote.md)を参照）。
1. バナーをページに追加します。バナー画像は、Search&amp;Promote データの影響を受けます。
1. Search&amp;Promote サービスが使用するサイトマップを生成します。

>[!NOTE]
>
>カスタムプロキシ設定で Search&amp;Promote を使用している場合、AEM には 3.x API を使用する機能と 4.x API を使用する機能があるので、両方の HTTP クライアントプロキシを設定する必要があります。
>
>* 3.x は [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) のように設定します。
>* 4.x は [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) のように設定します。

>



## Search&amp;Promote サービス URL の変更 {#changing-the-search-promote-service-url}

Search&amp;Promoteサービスに設定されるデフォルトのURLは`https://searchandpromote.omniture.com/px/`です。 別のサービスを使用するには、OSGi コンソールを使用して別の URL を指定します。

**Search&amp;PromoteサービスのURLを変更するには**:

1. [!UICONTROL OSGi]コンソールを開き、**[!UICONTROL 「Configuration]**」タブをタップします。 （[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)）。

1. 「**[!UICONTROL Day CQSearch&amp;Promote設定]**」項目をクリックします。
1. 「**[!UICONTROL リモートサーバーURI]**」テキストフィールドにURLを入力し、「**[!UICONTROL 保存]**」をタップします。

## Search&amp;Promote への接続の設定 {#configuring-the-connection-to-search-promote}

Search&amp;Promote への 1 つ以上の接続を設定して、Web ページがサービスとやり取りできるようにします。接続するには、Search&amp;Promote アカウントのメンバー ID とアカウント番号が必要です。

**Search&amp;Promoteへの接続を設定するには**:

1. **[!UICONTROL ツール]**&#x200B;アイコン/**[!UICONTROL デプロイメント]**&#x200B;から、**[!UICONTROL Cloud Services]**&#x200B;を選択します。

   これにより、クラウドサービスダッシュボードが表示されます。ローカルマシンの場合、ダッシュボードの URI は、次のようになります。

   [http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html)

1. [!UICONTROL Cloud Services]ページで、**[!UICONTROL AdobeSearch&amp;Promote]**&#x200B;リンクまたは&#x200B;**[!UICONTROL Search&amp;Promote]**&#x200B;アイコンをタップします。

1. 初めてAdobeSearch&amp;Promoteを設定する場合は、「**[!UICONTROL 今すぐ設定]**」をタップして[!UICONTROL 設定を作成]パネルを開きます。

   Search&amp;Promoteの詳細を表示するには、[**[!UICONTROL 詳細情報]**]をクリックしてください。

   ![chlimage_1-409](assets/chlimage_1-409.png)

1. ページ作成者が認識できる&#x200B;**[!UICONTROL タイトル]**&#x200B;を入力し、一意の&#x200B;**[!UICONTROL 名前]**&#x200B;を入力してから、**[!UICONTROL 作成]**&#x200B;をタップします。

   また、新しく作成した設定が、**[!UICONTROL クラウドサービスダッシュボード]**&#x200B;の Adobe Search&amp;Promote リスト項目の「**[!UICONTROL 利用可能な設定]**」の下に表示されます。

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. [!UICONTROL コンポーネントを編集]ダイアログボックスで、以下をフィールドに追加します。

   * **[!UICONTROL メンバー ID]**
   * **[!UICONTROL アカウント番号]**

   >[!NOTE]
   >
   >この情報を自分で取得するには、次にログインします。
   >
   >[https://searchandpromote.omniture.com/center/](https://searchandpromote.omniture.com/center/)
   >
   >有効な Seach&amp;Promote 資格情報（電子メール／パスワード）を使用します。
   >
   >ブラウザのアドレスバーにURLが表示されていることに注意してください。 次のようになります。
   >
   >[](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >[https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY](https://searchandpromote.omniture.com/px/home/?sp_id=XXXXXXXX-spYYYYYYYY)
   >
   >ここで&#x200B;**XXXXXXXX**&#x200B;は&#x200B;**[!UICONTROL メンバーid]**&#x200B;に対応し、**[!UICONTROL spYYYYYYY]**&#x200B;はアカウント番号に対応します。

1. 「**[!UICONTROL Search&amp;Promoteに接続]**」をタップします。

   接続の成功メッセージが表示されたら、「**[!UICONTROL OK]**」をタップします。

   （接続後、ボタンのテキストが「**[!UICONTROL Search&amp;Promote に再接続]**」に変更されます。）

1. 「**[!UICONTROL OK]**」をタップします。今作成した設定の Search&amp;Promote 設定ページが表示されます。

## データセンターの設定 {#configuring-the-data-center}

Search&amp;Promoteアカウントがアジアまたはヨーロッパにある場合は、デフォルトのデータセンターを変更して、適切なデータセンターを指すようにする必要があります（デフォルトのデータセンターは北米のアカウント用です）。

**データセンターを設定するには**:

1. `http://localhost:4502/system/console/configMgr/com.day.cq.searchpromote.impl.SearchPromoteServiceImpl`のWebコンソールに移動します。

   ![chlimage_1-411](assets/chlimage_1-411.png)

1. サーバーの場所に応じて、URI を次のいずれかに変更します。

   * 北米：[https://center.atomz.com/px/](https://center.atomz.com/px/)
   * EMEA:[https://center.lon5.atomz.com/px/](https://center.lon5.atomz.com/px/)
   * APAC:[https://center.sin2.atomz.com/px/](https://center.sin2.atomz.com/px/)

1. 「**[!UICONTROL 保存]**」をタップします。

## Search&amp;Promote コンポーネントのサイドキックへの追加 {#adding-search-promote-components-to-sidekick}

[!UICONTROL デザイン]モードで、**[!UICONTROL par]**&#x200B;コンポーネントを編集し、[!UICONTROL サイドキック]のSearch&amp;Promoteコンポーネントを許可します。 （詳しくは、[コンポーネント](/help/sites-developing/components.md)のドキュメントを参照）。

コンポーネントの使用について詳しくは、[WebページへのSearch&amp;Promote機能の追加](/help/sites-authoring/search-and-promote.md)を参照してください。

## ページで使用する Search&amp;Promote サービスの指定 {#specifying-the-search-promote-service-that-your-pages-use}

特定の Search&amp;Promote サービスを使用できるように、Web ページを設定します。Search&amp;Promote コンポーネントは、自動的にホストページのサービスを使用します。

ページの Search&amp;Promote プロパティを設定すると、すべての子ページが設定を継承します。必要に応じて、継承された設定を上書きするように子ページを設定できます。

>[!NOTE]
>
>サービス接続は、既に設定されている必要があります[Search&amp;Promoteへの接続の設定](#configuring-the-connection-to-search-promote)を参照してください。

1. **[!UICONTROL ページプロパティ]**&#x200B;ダイアログボックスを開きます。例えば、**[!UICONTROL Web サイト]**&#x200B;ページで、ページを右クリックし、「**[!UICONTROL プロパティ]**」をクリックします。

1. 「**[!UICONTROL クラウドサービス]**」タブをクリックします。

1. 親ページからのクラウドサービス設定の継承を無効にするには、継承パスの横にある南京錠アイコンをクリックします。

   ![sandinheritpadlock](assets/sandpinheritpadlock.png)

1. 「**[!UICONTROL 追加サービス]**」をクリックし、「**[!UICONTROL AdobeSearch&amp;Promote]**」を選択して、「**[!UICONTROL OK]**」をクリックします。

1. Search&amp;Promoteアカウントの接続設定を選択し、「**[!UICONTROL OK]**」をクリックします。

## 製品フィード {#product-feed}

Search&amp;Promote統合により、次のことが可能になります。

* [!UICONTROL eCommerce] APIを使用します。基盤となるリポジトリ構造とコマースプラットフォームとは別に使用します。
* Search&amp;Promoteの[!UICONTROL インデックスコネクタ]機能を利用して、XML形式の製品フィードを提供します。
* Search&amp;Promoteの[!UICONTROL リモートコントロール]機能を利用して、製品フィードに対するオンデマンドまたはスケジュール済みの要求を実行します。
* 様々なSearch&amp;Promoteアカウントに対するフィードの生成（クラウドサービスの設定として設定）

詳しくは、[製品フィード](/help/sites-administering/product-feed.md)を参照してください。
