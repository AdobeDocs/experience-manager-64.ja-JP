---
title: モバイルアプリケーションのオーサリング
seo-title: Authoring Mobile Applications
description: AEM Mobile ダッシュボードでは、モバイルアプリケーションの作成、ビルド、デプロイや、アプリケーションのメタデータの作成、削除、編集をおこなえます。このページでは、この機能について詳しく見ていきます。
seo-description: he AEM Mobile Dashboard allows you to create, build and deploy your mobile application, create, delete and edit application metadata. Follow this page to learn more.
uuid: 293b5d29-df7e-42dd-ae64-8c677317e7a5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: authoring-adobe-phonegap-enterprise
discoiquuid: abfeea65-102d-4800-abeb-304d61afcc13
exl-id: dbaa5221-4011-49cf-8123-5f8daa7fae76
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 67%

---

# モバイルアプリケーションのオーサリング{#authoring-mobile-applications}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

AEM Mobile ダッシュボードでは、モバイルアプリケーションの作成、ビルド、デプロイや、アプリケーションのメタデータの作成、削除、編集をおこなえます。アプリケーションが稼働したら、ライフサイクル指標や使用指標を含むアプリケーション分析を実行して、顧客コンバージョンとブランドロイヤルティを向上させることができます。

AEM Mobileアプリケーションを構築するには、 [モバイルアプリケーションの構築](/help/mobile/building-app-mobile-phonegap.md) ページ。

環境を設定して作業を始めるには、[AEM PhoneGap Enterprise を使用するための AEM の管理](/help/mobile/administer-phonegap.md)を参照してください。

## AEM Mobile アプリカタログ {#the-aem-mobile-apps-catalog}

この [AEM Mobile Apps カタログ](http://localhost:4502/aem/apps.html/content/phonegap) は、AEMで管理されているすべてのモバイルアプリを表示します。

このカタログは AEM Mobile の「ランディングページ」と考えられ、管理者はここで新しい AEM Mobile アプリケーションを開始できます。テンプレートに基づいて作成することも、モバイル開発者が既に開始している既存アプリケーションをアップロードすることもできます。

アプリカタログのランディングページに移動するには、以下の手順に従います。

1. **ナビゲーション**&#x200B;に移動し、「**モバイル**」を選択します。

1. 「**アプリ**」を選択して、アプリカタログを開きます。

![AEM Mobile アプリカタログ](assets/chlimage_1-135.png)

## AEM Mobile アプリダッシュボード {#the-aem-mobile-app-dashboard}

カタログから AEM Mobile アプリケーションを選択すると、そのアプリケーションのダッシュボードが表示されます。ここでは、アプリの管理、統計の表示、モバイルアプリコンテンツの構築、デプロイ、管理をおこなうことができます。

AEM Mobile ダッシュボードの各タイルの右下隅にある「...」をクリックして、詳細を表示または編集できます。

![AEM Mobile アプリケーションのコマンドセンター](assets/chlimage_1-136.png)

### アプリを管理タイル {#the-manage-app-tile}

アプリを管理タイルには、アプリケーションのアイコン、名前、説明、サポートされているプラットフォーム、更新用コールホーム URL およびバージョン情報が表示されます。このタイルをドリルダウンして、PhoneGap アプリケーション設定 (config.xml) を編集および管理し、配布用に様々なアプリケーションストアに送信するためのアプリケーションを準備できます。

詳しくは[こちら](/help/mobile/phonegap-app-details-tile.md)を参照してください。

![chlimage_1-137](assets/chlimage_1-137.png)

### ページコンテンツを管理タイル {#the-manage-page-content-tile}

AEM Sites とほぼ同様に、AEM Mobile でコンテンツを作成、更新および削除できます。**ページコンテンツを管理タイル**&#x200B;には、管理されているコンテンツのページ数と最終更新日が表示されます。タイルの各レコードをクリックすることによって、コンテンツにドリルダウンしてページを作成、コピー、移動、削除および更新できます。コンテンツが更新されたら、 **コンテンツパッケージを管理タイル。**

![コンテンツタイル](assets/chlimage_1-138.png)

### コンテンツパッケージを管理タイル {#the-manage-content-packages-tile}

ページコンテンツを管理タイルでコンテンツを追加または変更したら、コンテンツリリースの更新を使用して、変更を利用者に公開できます。

AEM アプリケーション作成者は、コンテンツパッケージを使用して AEM でページコンテンツを管理し、開発チームに PhoneGap シェルアプリケーション（アプリケーションのフレームワークまたはインフラストラクチャ）を変更してもらい、その変更を利用者に迅速に公開することができます。配信のために様々なストアに再提出するよう、開発者に協力を求める必要はありません。

コンテンツパッケージは、更新ごとにコンテンツリリースパッケージと見なされる ZIP ファイルを作成します。これらのパッケージには、アプリのレンダリング時に生成される html リソースと html ページが含まれ、最後の更新以降に変更されたファイルのみをパッケージ化するのに十分なインテリジェントです。

コンテンツパッケージを管理タイルの **タイプ** 列には、アプリケーションシェルコンテンツ（開発者が管理するアプリのフレームワークやインフラストラクチャなど）を示す「アプリ」、コンテンツ作成者が管理するページコンテンツを表す「コンテンツ」が表示されます。

コンテンツは言語として、または複数のコンテンツリリースパッケージを使用するアプリケーションの特定の部分として表すことができます。コンテンツのバンドル方法の選択肢は柔軟で、アプリケーションのコンテンツの管理方法に完全に合致するようにデザインされています。

「**変更済み**」列には、ページの最終変更日が示されます。

「**ステージング済み**」列には、最新のコンテンツ更新がいつ作成されたかが示されます。新しいコンテンツ更新を作成して変更をステージングするには、タイル内の任意のレコードを開いて、新しい更新を作成します。

「**発行済み**」列には、いつ最新のコンテンツ更新が公開され、利用者が使用できるようになったかが示されます。コンテンツを公開するには、まずそのコンテンツをステージングしてから、このタイルにドリルダウンしてコンテンツリリースの詳細コンソールから公開することで、更新を公開する必要があります。

![コンテンツリリースタイル](assets/chlimage_1-139.png) ![アプリシェルのコンテンツ同期パッケージ](do-not-localize/chlimage_1-5.png)

このアイコンは、アプリケーションシェルのコンテンツリリースパッケージを表します。

![](do-not-localize/chlimage_1-6.png)

このアイコンは、アプリケーションコンテンツのコンテンツリリースパッケージを表します。

### PhoneGap Build タイル {#the-phonegap-build-tile}

この **PhoneGap Buildタイル** 接続先 [https://build.phonegap.com](https://build.phonegap.com) リモートビルドを作成し、ホストします。 ビルドが完了すると、ビルドはダウンロードとして、または QR コードを介して直接デバイスで利用できるようになります。

または、デバイスソースをダウンロードし、[PhoneGap CLI](https://docs.phonegap.com/en/3.5.0/guide_cli_index.md.html) を使用してローカルにビルドできます。

![PhoneGap Build タイル](assets/chlimage_1-140.png)

### 指標タイル {#the-metrics-tile}

>[!CAUTION]
>
>指標タイルは、クラウドサービスを設定した後にのみ表示されます。
>
>詳しくは、 [AdobeMobile ServicesCloud Service](/help/mobile/configure-adobe-mobile-cloud-service.md) 」を参照してください。

AEM Mobileは、 [AdobeMobile Services SDK](https://www.adobe.com/ca/solutions/digital-marketing/mobile-services/app-sdk.html) (AMS) を使用します。

コントロールセンターの&#x200B;**指標タイル**&#x200B;には、AMS から取得したアプリケーションの分析概要が表示されます。右下にある「...」をクリックして、分析ダッシュボードの詳細を表示できます。

![指標タイル](assets/chlimage_1-141.png)

### エンティティコンテンツを管理タイル {#the-manage-entity-content-tile}

エンティティコンテンツを管理タイルでは、アプリの定義を追加および管理できます。アプリの定義は、アプリに適したスペース（およびその他の設定）を特定する方法です。 これにより、アプリを再コンパイルする必要なく、新しいスペースを追加できます。 アプリの定義が更新され、新しいスペースの情報が含まれます。

アプリの定義の作成および管理については、[こちら](/help/mobile/phonegap-app-definitions.md)を参照してください。

右下にある「...」をクリックして、エンティティコンテンツを管理ダッシュボードの詳細を表示できます。

![chlimage_1-142](assets/chlimage_1-142.png)

#### その他のリソース {#additional-resources}

管理者および開発者の役割と責任について詳しくは、以下のリソースを参照してください。

* [AEM と Adobe PhoneGap Enterprise での開発](/help/mobile/developing-in-phonegap.md)
* [AEM を使用した Adobe PhoneGap Enterprise のコンテンツの管理](/help/mobile/administer-phonegap.md)
