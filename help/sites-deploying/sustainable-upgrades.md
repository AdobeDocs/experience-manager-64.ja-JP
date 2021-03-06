---
title: 持続可能なアップグレード
seo-title: Sustainable Upgrades
description: AEM 6.4 の持続可能なアップグレードについて説明します。
seo-description: Learn about sustainable upgrades in AEM 6.4.
uuid: 59d64af5-6ee0-40c8-b24a-c06848f70daa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 5ca8dd7a-4efd-493e-8022-d2f10903b0a2
feature: Upgrading
exl-id: 765efa8d-1548-4db3-ba87-baa02075eaf6
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 86%

---

# 持続可能なアップグレード{#sustainable-upgrades}

## カスタマイズフレームワーク {#customization-framework}

### アーキテクチャ（機能／インフラストラクチャ／コンテンツ／アプリケーション）  {#architecture-functional-infrastructure-content-application}

カスタマイズフレームワーク機能は、アップグレードしづらいコード（APIS など）またはコンテンツ（オーバーレイなど）などの拡張できない領域での違反が減少するように設計されています。

カスタマイズフレームワークには、**API サーフェス**&#x200B;と&#x200B;**コンテンツ分類**&#x200B;の 2 つのコンポーネントがあります。

#### API サーフェス {#api-surface}

AEM の以前のリリースでは、多くの API が Uber Jar を介して公開されていました。これらの API の一部は、お客様による使用を意図して公開されたものではなく、複数のバンドルにまたがって AEM 機能をサポートするために公開されたものです。今後は、アップグレードの観点からどの API が安全に使用できるかをお客様に示すために、Java API は、公開または非公開としてマークされます。その他の詳細を次に示します。

* としてマークされた Java API `Public` は、カスタム実装バンドルで使用および参照できます。

* 公開 API は、互換パッケージのインストールによる後方互換性があります。
* 互換パッケージには、後方互換性を確保するために互換 Uber JAR が含まれます。
* としてマークされた Java API `Private` は、AEMの内部バンドルでのみ使用されることを目的としており、カスタムバンドルでは使用できません。

>[!NOTE]
>
>このコンテキストでの`Private`非公開および`Public`公開の概念を、Java の クラスおよび クラスの概念と混同しないようにしてください。

![image2018-2-12_23-52-48](assets/image2018-2-12_23-52-48.png)

#### コンテンツ分類 {#content-classifications}

AEM では、以前からオーバーレイの原理と Sling Resource Merger を使用して、ユーザーが AEM の機能の拡張およびカスタマイズをおこなうことができるようになっています。AEM コンソールと UI を強化する事前定義済みの機能は、**/libs** に格納されます。ユーザーは **/libs** の下は何も変更できませんが、**/apps** の下にコンテンツを追加して、**/libs** 内で定義されている機能をオーバーレイおよび拡張できます（詳しくは、「オーバーレイを使用した開発」を参照）。この場合も、AEM のアップグレード時に多数の問題が発生します。**/libs** 内のコンテンツが変更され、オーバーレイ機能が予期しない動作で破損することがあるからです。ユーザーは、`sling:resourceSuperType` を介した継承によって、または sling:resourceType を使用して **/libs** 内のコンポーネントを直接参照することによって、AEM コンポーネントを拡張することもできます。同様のアップグレードの問題は、参照およびオーバーライドの使用例で発生する可能性があります。

安全に使用およびオーバーレイできる **/libs** の領域を容易に理解してより安全になるように、**/libs** 内のコンテンツは次の mixin によって分類されています。

* **公開（granite:PublicArea）** - オーバーレイ、継承（`sling:resourceSuperType`）または直接使用（`sling:resourceType`）できるように、ノードを公開として定義します。公開としてマークされた /libs の下のノードは、互換パッケージを追加することで、アップグレードしても安全になります。通常、顧客は公開としてマークされたノードのみを利用する必要があります。

* **抽象（granite:AbstractArea）** - ノードを抽象として定義します。ノードはオーバーレイまたは継承できます ( `sling:resourceSupertype`) ですが、直接使用しないでください ( `sling:resourceType`) をクリックします。

* **最終（granite:FinalArea）** - ノードを最終として定義します。最終として分類されたノードは、オーバーレイも継承もできません。最終ノードは、 `sling:resourceType`. 最終ノードの下のサブノードは、デフォルトで内部と見なされます。

* **内部（granite:InternalArea）** - ノードを内部として定義します。内部として分類されたノードは、オーバーレイ、継承、直接使用のいずれもできません。これらのノードは、AEM の内部機能でのみ使用されます。

* **注釈なし** - ノードはツリー階層に基づいて分類を継承します。/ root はデフォルトで公開です。**親が内部または最終として分類されているノードも、内部として扱われます。**

>[!NOTE]
>
>これらのポリシーは、Sling 検索パスに基づくメカニズムに対してのみ適用されます。その他の分野 **/libs** と同様に、クライアントサイドライブラリは `Internal`の代わりに、標準の clientlib のインクルードでも使用できます。 このような場合は、お客様が引き続き内部分類に従うことが重要です。

#### CRXDE Lite コンテンツタイプインジケーター {#crxde-lite-content-type-indicators}

CRXDE Liteで適用された Mixin は、次のようにマークされたコンテンツノードとツリーを表示します `INTERNAL` はグレー表示になっています。 の場合 `FINAL` 灰色表示になっているのはアイコンだけです。 これらのノードの子もグレー表示されます。どちらの場合も、オーバーレイノード機能は無効になります。

**公開**

![image2018-2-8_23-34-5](assets/image2018-2-8_23-34-5.png)

**最終**

![image2018-2-8_23-34-56](assets/image2018-2-8_23-34-56.png)

**内部**

![image2018-2-8_23-38-23](assets/image2018-2-8_23-38-23.png)

**コンテンツヘルスチェック**

AEM 6.4 にはヘルスチェックが付属しています。オーバーレイまたは参照されたコンテンツがコンテンツ分類と一致しない方法で使用された場合は、このヘルスチェックにより警告が表示されます。

**Sling／Granite コンテンツアクセスチェック**&#x200B;は、リポジトリを監視して、お客様のコードが AEM の保護されたノードに誤ってアクセスしていないかどうかを確認する新しいヘルスチェックです。

このヘルスチェックは **/apps** をスキャンし、通常は完了するまで数秒かかります。

この新しいヘルスチェックにアクセスするには、次の手順に従います。

1. AEM ホーム画面から、**ツール／運営／ヘルスレポート**&#x200B;に移動します。
1. 次に示すように、**Sling／Granite コンテンツアクセスチェック**&#x200B;をクリックします。

   ![screen_shot_2017-12-14at55648pm](assets/screen_shot_2017-12-14at55648pm.png)

スキャンが完了すると、警告のリストが表示され、誤って参照されている保護されたノードをエンドユーザーに通知します。

![screenshot-2018-2-5healthreports](assets/screenshot-2018-2-5healthreports.png)

違反を修正すると、緑の状態に戻ります。

![screenshot-2018-2-5healthreports-violations](assets/screenshot-2018-2-5healthreports-violations.png)

ヘルスチェックには、バックグラウンドサービスによって収集された情報が表示されます。バックグラウンドサービスでは、オーバーレイまたはリソースタイプがすべての Sling 検索パスにわたって使用される場合は常に、非同期的にチェックが実行されます。コンテンツ mixin が誤って使用された場合、違反が報告されます。
