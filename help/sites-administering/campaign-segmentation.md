---
title: セグメント化の設定
seo-title: Configuring Segmentation
description: AEM Campaign でセグメント化を設定する方法を説明します。
seo-description: Learn how to configure segmentation for AEM Campaign.
uuid: f22e41b6-d9d9-4f18-9925-2d4aebc167b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 49c9c9ab-632a-40f7-8c30-d6a8c0f1b420
exl-id: 92302067-3500-41ca-9855-87f36148bfbc
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 45%

---

# セグメント化の設定{#configuring-segmentation}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>このドキュメントでは、ClientContext で使用するセグメント化の設定について説明します。 タッチ UI を使用して ContextHub でセグメントを設定するには、 [ContextHub でのセグメント化の設定](/help/sites-administering/segmentation.md).

キャンペーンを作成する場合には、セグメント化を考えることが重要になります。詳しくは、 [セグメント化の用語集](/help/sites-authoring/segmentation-overview.md) を参照してください。

サイト訪問者についてこれまでに収集した情報と、達成する目標に応じて、ターゲットコンテンツに必要なセグメントと戦略を定義する必要があります。

このようなセグメントを使用して、訪問者に特定のターゲットコンテンツを提供します。このコンテンツは、web サイトの[キャンペーン](/help/sites-authoring/personalization.md)セクションで管理されます。ここで定義したティーザーページは、任意のページのティーザー段落として含めることができ、専用のコンテンツを適用できる訪問者セグメントを定義できます。

AEMでは、セグメント、ティーザー、キャンペーンを簡単に作成および更新できます。 また、定義の結果を検証することもできます。

**セグメントエディター**&#x200B;を使用すると、セグメントを簡単に定義できます。

![segmenteditor-1](assets/segmenteditor-1.png)

以下が可能です。 **編集** 各セグメントで **タイトル**, **説明** および **ブースト** 係数 サイドキックを使用して、 **および** および **または** 定義するコンテナ **セグメントロジック**&#x200B;をクリックし、必要な **セグメント特性** をクリックして、選択基準を定義します。

## ブースト係数 {#boost-factor}

各セグメントには、重み付け係数として使用される&#x200B;**ブースト**&#x200B;パラメーターがあります。この数値が高いセグメントは、低い数値のセグメントよりも優先して選択されます。

* 最小値：`0`
* 最大値：`1000000`

## セグメントロジック {#segment-logic}

次の論理コンテナが標準で使用でき、セグメント選択のロジックを構築できます。 サイドキックからエディターにドラッグできます。

<table> 
 <tbody> 
  <tr> 
   <td> AND コンテナ<br /> </td> 
   <td> AND ブール演算。<br /> </td> 
  </tr> 
  <tr> 
   <td> OR コンテナ<br /> </td> 
   <td> OR ブール演算値。</td> 
  </tr> 
 </tbody> 
</table>

## セグメント特性 {#segment-traits}

次のセグメント特性を標準で使用できます。サイドキックからエディターにドラッグできます。

<table> 
 <tbody> 
  <tr> 
   <td> IP 範囲<br /> </td> 
   <td>訪問者に割り当てられる IP アドレスの範囲を定義します。<br /> </td> 
  </tr> 
  <tr> 
   <td> ページヒット<br /> </td> 
   <td>ページがリクエストされた頻度。<br /> </td> 
  </tr> 
  <tr> 
   <td> ページプロパティ<br /> </td> 
   <td>訪問したページのすべてのプロパティ。<br /> </td> 
  </tr> 
  <tr> 
   <td> リファラルキーワード<br /> </td> 
   <td>参照先の web サイトの情報と照合するキーワード。<br /> </td> 
  </tr> 
  <tr> 
   <td> スクリプト</td> 
   <td>評価される Javascript 式。<br /> </td> 
  </tr> 
  <tr> 
   <td> セグメントの参照 <br /> </td> 
   <td>もう一方のセグメントへの参照。<br /> </td> 
  </tr> 
  <tr> 
   <td> タグクラウド<br /> </td> 
   <td>訪問したページのタグと照合されるタグ。<br /> </td> 
  </tr> 
  <tr> 
   <td> ユーザーの年齢<br /> </td> 
   <td>ユーザープロファイルから取得される年齢。<br /> </td> 
  </tr> 
  <tr> 
   <td> ユーザープロパティ<br /> </td> 
   <td>ユーザープロファイルで確認できるその他すべての情報。 </td> 
  </tr> 
 </tbody> 
</table>

OR および AND のブール演算子を使用してこれらの特徴を組み合わせ（[新しいセグメントの作成](#creating-a-new-segment)を参照）、このセグメントを選択できる確実なシナリオを定義します。

文全体が true と評価されると、このセグメントは解決されます。複数のセグメントを適用可能な場合、**[ブースト](/help/sites-administering/campaign-segmentation.md#boost-factor)**&#x200B;係数も使用されます。

>[!CAUTION]
>
>セグメントエディターは、循環参照をチェックしません。例えば、セグメント A が別のセグメント B を参照し、そのセグメント B がセグメント A を参照しているとします。セグメントに循環参照が含まれていないことを確認する必要があります。

>[!NOTE]
>
>**_i18n** サフィックス付きのプロパティは、パーソナライズ機能の UI clientlib の一部であるスクリプトによって設定されます。UI は公開時には必要ないので、UI 関連の clientlib はすべて作成時に読み込まれます。
>
>したがって、これらのプロパティを使用してセグメントを作成するときは、通常はインスタンスで **browserFamily_i18n** ではなく、**browserFamily** を使用する必要があります。

## 新しいセグメントの作成 {#creating-a-new-segment}

新しいセグメントを定義するには、次の手順に従います。

1. パネルで、**ツール／運営／設定**&#x200B;を選択します。
1. をクリックします。 **セグメント化** ページを開き、必要な場所に移動します。
1. の作成 [新しいページ](/help/sites-authoring/managing-pages.md) の使用 **セグメント** テンプレート。
1. 新しいページを開き、セグメントエディターを表示します。

   ![screen_shot_2012-02-02at101726am](assets/screen_shot_2012-02-02at101726am.png)

1. サイドキックまたはコンテキストメニュー ( 通常はマウスの右ボタンをクリックし、 **新規…** をクリックして、Insert New Component ウィンドウを開く ) 必要なセグメント特性を見つけます。 次に、 **セグメントエディター** デフォルトの **および** コンテナ。
1. 新しい特性をダブルクリックして、特定のパラメーターを編集します。例えば、マウスの位置は次のようになります。

   ![screen_shot_2012-02-02at103135am-1](assets/screen_shot_2012-02-02at103135am-1.png)

1. クリック **OK** 定義を保存するには、次の手順に従います。
1. 以下が可能です。 **編集** セグメント定義を使用して、 **タイトル**, **説明** および **[ブースト](/help/sites-administering/campaign-segmentation.md#boost-factor)** 係数：

   ![screen_shot_2012-02-02at103547am](assets/screen_shot_2012-02-02at103547am.png)

1. 必要に応じて、さらに特性を追加します。 ブール式は、 **AND コンテナ** および **OR コンテナ** 次の下にあるコンポーネント **セグメントロジック**. セグメントエディターを使用して、不要になった特性やコンテナを削除したり、文内の新しい位置にドラッグしたりできます。

## AND コンテナと OR コンテナの使用 {#using-and-and-or-containers}

AEMで複雑なセグメントを作成できます。 これは、次の基本的な点に注意するのに役立ちます。

* 定義の最上位レベルは必ず、最初に作成された AND コンテナになります。これは変更できませんが、他のセグメント定義には影響しません。
* コンテナのネストが意味をなすようにします。 コンテナは、ブール式の括弧として表示できます。

次の例は、次のいずれかの訪問者を選択するために使用します。

16～65 歳の男性

または

16～62 歳の女性

メイン演算子は OR なので、最初に **OR コンテナ**. この中に 2 つの AND 文があり、それぞれに対して、 **AND コンテナ**：に個々の特性を追加できます。

![screen_shot_2012-02-02at105145am-1](assets/screen_shot_2012-02-02at105145am-1.png)

## セグメントの適用のテスト {#testing-the-application-of-a-segment}

セグメントを定義したら、 **[ClientContext](/help/sites-administering/client-context.md)**:

1. テストするセグメントを選択します。
1. **[Ctrl+Alt+C](/help/sites-authoring/keyboard-shortcuts.md)** キーを押して、**[クライアントコンテキスト](/help/sites-administering/client-context.md)**&#x200B;を開くと、収集されたデータが表示されます。テストを行う場合は、特定の値を&#x200B;**編集**&#x200B;するか別のプロファイルを&#x200B;**読み込んで**、その場で結果を確認できます。

1. 定義した特性に応じて、現在のページで利用可能なデータはセグメント定義と一致する場合も一致しない場合もあります。一致のステータスは定義の下に表示されます。

例えば、単純なセグメントはユーザーの年齢と性別に基づいて定義できます。特定のプロファイルを読み込むと、セグメントが正常に解決された場合は次のように表示されます。

![screen_shot_2012-02-02at105926am-1](assets/screen_shot_2012-02-02at105926am-1.png)

失敗した場合は次のように表示されます。

![screen_shot_2012-02-02at110019am-1](assets/screen_shot_2012-02-02at110019am-1.png)

>[!NOTE]
>
>すべての特性は即座に解決されますが、ほとんどの場合はページの再読み込み時にのみ変更されます。 マウス位置の変更は直ちに表示されるので、テストに役立ちます。

このようなテストは、**ティーザー**&#x200B;コンポーネントと組み合わせて、コンテンツページでも実行できます。

ティーザー段落にマウスオーバーすると、適用されたセグメントが、現在解決されているかどうか、その結果、現在のティーザーインスタンスが選択された理由で表示されます。

![chlimage_1-408](assets/chlimage_1-408.png)

## セグメントの使用 {#using-your-segment}

セグメントは現在、 [キャンペーン](/help/sites-authoring/personalization.md). セグメントを活用することで、特定のターゲットオーディエンスに表示する実際のコンテンツを制御できます。 詳しくは、 [セグメントについて](/help/sites-authoring/segmentation-overview.md) を参照してください。
