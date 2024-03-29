---
title: Silverpop Engage との統合
seo-title: Integrating with Silverpop Engage
description: AEMを Silverpop Engage と統合する方法を説明します
seo-description: Learn how to integrate AEM with Silverpop Engage
uuid: dfff7aaf-5264-4763-995f-5647f565c03b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: integration
content-type: reference
discoiquuid: dfff6bdc-0d5f-4338-aa8a-7d0eb04bc19a
exl-id: 3148ba52-4464-4f3e-8741-645cd7a1c970
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 47%

---

# Silverpop Engage との統合{#integrating-with-silverpop-engage}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>Silverpop 統合は、 **not** すぐに使用できます。 次をダウンロードする必要があります： [Silverpop 統合パッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content) パッケージ共有からインスタンスにインストールします。 パッケージをインストールしたら、このドキュメントの説明に従って設定できます。

AEM を Silverpop Engage と統合すると、AEM で作成したメールを Silverpop を使用して管理および送信できます。また、AEM ページ上の AEM フォームを使用して、Silverpop のリード管理機能を使用できます。

統合により、次の機能を利用できます。

* 電子メールをAEMで作成し、配布用に Silverpop に公開する機能。
* AEMフォームのアクションを設定して Silverpop 購読者を作成する機能。

Silverpop Engage が設定されると、Silverpop Engage にニュースレターまたはメールを発行できます。

## Silverpop 設定の作成 {#creating-a-silverpop-configuration}

Silverpop 設定は、**クラウドサービス**、**ツール**&#x200B;または **API エンドポイント**&#x200B;で追加できます。この節では、すべてのメソッドについて説明します。

### クラウドサービスを使用した Silverpop の設定 {#configuring-silverpop-via-cloudservices}

Cloud Servicesで Silverpop 設定を作成するには：

1. AEM で、**ツール**／**デプロイメント**／**クラウドサービス**&#x200B;をタップまたはクリックします。（または `https://<hostname>:<port>/etc/cloudservices.html` に直接アクセスします。）
1. サードパーティのサービスで、「**Silverpop Engage**」、「**設定**」の順にクリックします。Silverpop 設定ウィンドウが開きます。

   >[!NOTE]
   >
   >Silverpop Engage は、パッケージ共有からパッケージをダウンロードしない限り、サードパーティのサービスのオプションとして使用できません。

1. タイトルを入力し、オプションで名前を入力して、「**作成**」をクリックします。Silverpop 設定ウィンドウが開きます。
1. ユーザー名とパスワードを入力し、ドロップダウンリストから API エンドポイントを選択します。
1. クリック **Silverpop に接続します。** 接続に成功すると、成功ダイアログが表示されます。 「**OK**」をクリックしてウィンドウを閉じます。「**Silverpop Engage に移動**」をクリックすることで、Silverpop に移動できます。
1. Silverpop が設定されました。「**編集**」をクリックして、この設定を編集できます。
1. さらに、Silverpop Engage フレームワークは、タイトルと名前（オプション）を指定することで、パーソナライズされたアクション用に設定できます。 「作成」をクリックすると、既に設定済みの Silverpop 接続用のフレームワークが正常に作成されます。

   読み込まれたデータ拡張列は、後でAEMコンポーネントで使用できます。 **テキストとパーソナライゼーション**.

### ツールを使用した Silverpop の設定 {#configuring-silverpop-via-tools}

ツールで Silverpop 設定を作成するには：

1. AEM で、**ツール**／**デプロイメント**／**クラウドサービス**&#x200B;をタップまたはクリックします。または、`https://<hostname>:<port>/misadmin#/etc` にアクセスして直接移動します。
1. **ツール**／**クラウドサービス設定**／**Silverpop Engage** を選択します。
1. 「**新規**」をクリックして、**ページを作成**&#x200B;ウィンドウを開きます。

   ![chlimage_1-44](assets/chlimage_1-44.jpeg)

1. 次を入力します。 **タイトル** オプションで **名前**&#x200B;をクリックし、 **作成**.
1. 前の手順 4 で説明した設定情報を入力します。 この手順に従って、Silverpop の設定を完了します。

### 複数の設定の追加 {#adding-multiple-configurations}

複数の設定を追加するには：

1. ようこそページで、 **Cloud Services** をクリックし、 **Silverpop Engage**. 「**設定を表示**」ボタンをクリックします（1 つ以上の Silverpop 設定が利用可能な場合に表示されます）。使用可能なすべての設定が表示されます。
1. 次をクリック： **+** [ 利用可能な設定 ] の横に記号を付けます。 これにより、 **設定を作成** ウィンドウ 前の設定手順に従って、新しい設定を作成します。

### Silverpop に接続するための API エンドポイントの設定 {#configuring-api-end-points-for-connecting-to-silverpop}

現在、AEMには、セキュリティで保護されていないエンドポイントが 6 つあります（エンゲージ 1 ～ 6）。 Silverpop で、既存のエンドポイントに対して、2 つの新しいエンドポイントと変更された接続エンドポイントを提供するようになりました。

API エンドポイントを設定するには：

1. `https://<hostname>:<port>/crxde.` で `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` に移動します。
1. 右クリックして、**Create**／**Create Node**&#x200B;を選択します。
1. 「**名前**」に「`sp-e0`」と入力して、「**タイプ**」で「`cq:Widget`」を選択します。
1. 新しく追加したノードに 2 つのプロパティを追加します。

   1. **名前**：`text`、**タイプ**：`String`、**値**：`Engage 0`
   1. **名前**：`value`、**タイプ**：`String`、**値**：`https://api0.silverpop.com`

   ![chlimage_1-286](assets/chlimage_1-286.png)

   「すべて保存」ボタンをクリックします。

1. 「**名前**」に「`sp-e7`」と入力し、「**タイプ**」で「`cq:Widget` 」を選択して、もう 1 つのノードを作成します。

   新しく追加したノードに 2 つのプロパティを追加します。

   1. **名前**：`text`、**タイプ**：`String`、**値**：`Pilot`
   1. **名前**：`value`、**タイプ**：`String`、**値**：`https://apipilot.silverpop.com/XMLAPI`

1. 既存の API エンドポイント（Engage 1～6）を変更するには、それぞれを 1 つずつクリックして、値を次のように置き換えます。

   | **ノード名** | **既存のエンドポイント値** | **新しいエンドポイント値** |
   |---|---|---|
   | sp-e1 | https://api.engage1.silverpop.com/XMLAPI | https://api1.silverpop.com |
   | sp-e2 | https://api.engage2.silverpop.com/XMLAPI | https://api2.silverpop.com |
   | sp-e3 | https://api.engage3.silverpop.com/XMLAPI | https://api3.silverpop.com |
   | sp-e4 | https://api.engage4.silverpop.com/XMLAPI | https://api4.silverpop.com |
   | sp-e5 | https://api.engage5.silverpop.com/XMLAPI | https://api5.silverpop.com |
   | sp-e6 | https://api.pilot.silverpop.com/XMLAPI | https://api6.silverpop.com |

1. 「**すべて保存**」をクリックします。AEMは、セキュアなエンドポイントで Silverpop に接続する準備が整いました。

   ![chlimage_1-45](assets/chlimage_1-45.jpeg)
