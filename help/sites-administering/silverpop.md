---
title: Silverpop Engage との統合
seo-title: Integrating with Silverpop Engage
description: AEM と Silverpop Engage を統合する方法について説明します。
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: dfff7aaf-5264-4763-995f-5647f565c03b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: dfff6bdc-0d5f-4338-aa8a-7d0eb04bc19a
exl-id: 3148ba52-4464-4f3e-8741-645cd7a1c970
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 78%

---

# Silverpop Engage との統合{#integrating-with-silverpop-engage}

>[!NOTE]
>
>既製の AEM は Silverpop と&#x200B;**統合できません**。[Silverpop の統合パッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content)をパッケージ共有からダウンロードしてインスタンスにインストールする必要があります。パッケージをインストールしたら、このドキュメントの説明に従って設定してください。

AEMと Silverpop Engage の統合により、AEMで作成した電子メールを Silverpop 経由で管理および送信できます。 また、AEMページ上のAEM forms を使用して、Silverpop のリード管理機能を使用することもできます。

この統合によって次の機能を使用できるようになります。

* AEM で電子メールを作成し、配信用に Silverpop に公開する機能。
* AEM フォームのアクションを設定して、Silverpop サブスクライバーを作成する機能。

Silverpop Engage が設定されると、Silverpop Engage にニュースレターまたは電子メールを発行できます。

## Silverpop 設定の作成 {#creating-a-silverpop-configuration}

Silverpop 設定は、**クラウドサービス**、**ツール**&#x200B;または **API エンドポイント**&#x200B;で追加できます。すべての方法をここで説明します。

### クラウドサービスを使用した Silverpop の設定 {#configuring-silverpop-via-cloudservices}

Silverpop 設定をクラウドサービスで設定するには：

1. AEM で、**ツール**／**デプロイメント**／**クラウドサービス**&#x200B;をタップまたはクリックします。( または、 `https://<hostname>:<port>/etc/cloudservices.html`.)
1. サードパーティのサービスで、 **Silverop Engage** その後 **設定**. Silverpop 設定ウィンドウが開きます。

   >[!NOTE]
   >
   >Silverpop Engage のパッケージをパッケージ共有からダウンロードしない限り、Silverpop Engage をサードパーティのサービスのオプションとして使用できません。

1. タイトルを入力し、オプションで名前を入力して、「**作成**」をクリックします。「**Silverpop 設定**」設定ウィンドウが開きます。
1. ユーザー名、パスワードを入力し、API エンドポイントをドロップダウンリストから選択します。
1. 「**Silverpop に接続」をクリックします。**&#x200B;接続に成功したら、成功ダイアログが表示されます。「**OK**」をクリックしてウィンドウを閉じます。Silverpop に移動するには、 **Silverpop Engage に移動**.
1. Silverpop が設定されました。「**編集**」をクリックして、この設定を編集できます。
1. また、Silverpop Engage フレームワークは、タイトルおよび名前（オプション）を提供することで、パーソナライズされたアクション用に設定できます。「作成」をクリックすると、既に設定された Silverpop 接続のフレームワークを作成します。

   読み込まれたデータ拡張列は、後で AEM コンポーネントの「**テキストおよびパーソナライゼーション**」で使用できます。

### ツールを使用した Silverpop の設定 {#configuring-silverpop-via-tools}

Silverpop 設定をツールで設定するには：

1. AEM で、**ツール**／**デプロイメント**／**クラウドサービス**&#x200B;をタップまたはクリックします。または、 `https://<hostname>:<port>/misadmin#/etc`.
1. **ツール**／**クラウドサービス設定**／**Silverpop Engage** を選択します。
1. 「**新規**」をクリックして、**ページを作成**&#x200B;ウィンドウを開きます。

   ![chlimage_1-44](assets/chlimage_1-44.jpeg)

1. **タイトル**&#x200B;を入力し、オプションで&#x200B;**名前**&#x200B;を入力して、「**作成**」をクリックします。
1. 前述の手順 4 で示した設定情報を入力します。その手順に従って、Silverpop の設定を完了します。

### 複数の設定の追加 {#adding-multiple-configurations}

複数の設定を追加するには：

1. ようこそページで、「**クラウドサービス**」をクリックし、「**Silverpop Engage**」をクリックします。クリック **設定を表示** ボタンが表示されます。 利用可能なすべての設定が一覧表示されます。
1. 「利用可能な設定」の横にある「**+**」記号をクリックします。**設定を作成**&#x200B;ウィンドウが開きます。前述の設定手順に従って新しい設定を作成します。

### Silverpop に接続するための API エンドポイントの設定 {#configuring-api-end-points-for-connecting-to-silverpop}

現在、AEM には 6 つの保護されていないエンドポイント（Engage 1～6）があります。Silverpop は、2 つの新しいエンドポイントと、既存のものを変更した接続エンドポイントを提供します。

API エンドポイントを設定するには：

1. に移動します。 `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` オン `https://<hostname>:<port>/crxde.`
1. 右クリックして、**Create**／**Create Node**&#x200B;を選択します。
1. 次を入力します。 **名前** as `sp-e0` を選択します。 **タイプ** as `cq:Widget`.
1. 新しく追加したノードに 2 つのプロパティを追加します。

   1. **名前**: `text`, **タイプ**: `String`, **値**: `Engage 0`
   1. **名前**: `value`, **タイプ**: `String`, **値**: `https://api0.silverpop.com`

   ![chlimage_1-286](assets/chlimage_1-286.png)

   「すべて保存」ボタンをクリックします。

1. を使用してもう 1 つのノードを作成します。 **名前** as `sp-e7` および **タイプ** as `cq:Widget`.

   新しく追加したノードに 2 つのプロパティを追加します。

   1. **名前**: `text`, **タイプ**: `String`, **値**: `Pilot`
   1. **名前**: `value`, **タイプ**: `String`, **値**: `https://apipilot.silverpop.com/XMLAPI`

1. 既存の API エンドポイント（Engage 1～6）を変更するには、それぞれを 1 つずつクリックして、値を次のように置き換えます。

   | **ノード名** | **既存の終点の値** | **新しいエンドポイント値** |
   |---|---|---|
   | sp-e1 | https://api.engage1.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. 「**すべて保存**」をクリックします。これで、AEM は、保護されたエンドポイントで Silverpop と接続する準備ができました。

   ![chlimage_1-45](assets/chlimage_1-45.jpeg)
