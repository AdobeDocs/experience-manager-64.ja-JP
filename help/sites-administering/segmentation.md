---
title: ContextHub でのセグメント化の設定
seo-title: Configuring Segmentation with ContextHub
description: Context Hub でセグメント化を設定する方法について説明します。
seo-description: Learn how to configure segmentation with Context Hub.
uuid: 196cfb18-317c-443d-b6f1-f559e4221baa
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 6cade87c-9ed5-47d7-9b39-c942268afdad
exl-id: 83e73a5d-c6fa-426a-8476-78769ae7a8c1
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 53%

---

# ContextHub でのセグメント化の設定 {#configuring-segmentation-with-contexthub}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>この節では、ContextHub を使用する際のセグメント化の設定について説明します。 ClientContext 機能を使用している場合は、 [ClientContext のセグメント化の設定](/help/sites-administering/campaign-segmentation.md).

キャンペーンを作成する場合、セグメント化を考えることが重要になります。詳しくは、 [オーディエンスの管理](/help/sites-authoring/managing-audiences.md) を参照してください。

サイト訪問者についてこれまでに収集した情報と、達成する目標に応じて、ターゲットコンテンツに必要なセグメントと戦略を定義する必要があります。

このようなセグメントを使用して、訪問者に特定のターゲットコンテンツを提供します。このコンテンツは、web サイトの「[パーソナライズ機能](/help/sites-authoring/personalization.md)」セクションで管理されます。ここで定義した[アクティビティ](/help/sites-authoring/activitylib.md)は、任意のページに追加でき、専用のコンテンツを適用できる訪問者セグメントを指定できます。

AEMを使用すると、ユーザーエクスペリエンスを簡単にパーソナライズできます。 また、セグメント定義の結果を検証することもできます。

## セグメントへのアクセス {#accessing-segments}

この [オーディエンス](/help/sites-authoring/managing-audiences.md) コンソールは、ContextHub または ClientContext のセグメントやAdobe Targetアカウントのオーディエンスを管理するために使用します。 このドキュメントでは、ContextHub のセグメントの管理について取り上げます。の場合 [ClientContext セグメント](/help/sites-administering/campaign-segmentation.md) およびAdobe Targetセグメントについては、関連するドキュメントを参照してください。

セグメントにアクセスするには、グローバルナビゲーションで「**ナビゲーション／パーソナライズ機能／オーディエンス**」を選択します。

![chlimage_1-310](assets/chlimage_1-310.png)

## セグメントエディター {#segment-editor}

**セグメントエディター**&#x200B;を使用すると、セグメントを簡単に変更できます。セグメントを編集するには、[セグメントリスト](/help/sites-administering/segmentation.md#accessing-segments)からセグメントを選択し、「**編集**」ボタンをクリックします。

![segmenteditor](assets/segmenteditor.png)

コンポーネントブラウザーを使用すると、**AND** および **OR** コンテナを追加してセグメントロジックを定義してから、別のコンポーネントを追加してプロパティや値を比較できます。また、スクリプトやその他のセグメントを参照して選択条件を定義する（[新しいセグメントの作成](#creating-a-new-segment)を参照）ことによって、セグメントの選択シナリオを正確に定義できます。

ステートメント全体が true と評価されると、セグメントは解決されます。複数のセグメントを適用可能な場合、**ブースト**&#x200B;係数も使用されます。[ブースト係数](/help/sites-administering/campaign-segmentation.md#boost-factor)について詳しくは、「[新しいセグメントの作成](#creating-a-new-segment)」を参照してください。

>[!CAUTION]
>
>セグメントエディターは、循環参照をチェックしません。例えば、セグメント A が別のセグメント B を参照し、そのセグメント B がセグメント A を参照しているとします。セグメントに循環参照が含まれていないことを確認する必要があります。

### コンテナ {#containers}

次のコンテナは、すぐに使用でき、比較と参照をグループ化してブール評価をおこなうことができます。 コンポーネントブラウザーからエディターにドラッグできます。 詳しくは、「[AND コンテナと OR コンテナの使用](/help/sites-administering/segmentation.md#using-and-and-or-containers)」の節を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td>コンテナ AND<br /> </td> 
   <td>AND ブール演算子<br /> </td> 
  </tr> 
  <tr> 
   <td>コンテナ OR<br /> </td> 
   <td>OR ブール演算子</td> 
  </tr> 
 </tbody> 
</table>

### 比較 {#comparisons}

次のセグメント比較を、すぐに使用してセグメントプロパティを評価できます。 コンポーネントブラウザーからエディターにドラッグできます。

<table> 
 <tbody> 
  <tr> 
   <td>プロパティ - 値<br />。 </td> 
   <td>ストアのプロパティと定義済みの値を比較<br /> </td> 
  </tr> 
  <tr> 
   <td>プロパティ - プロパティ</td> 
   <td>ストアの 1 つのプロパティと別のプロパティを比較<br />。 </td> 
  </tr> 
  <tr> 
   <td>プロパティ - セグメントの参照</td> 
   <td>ストアのプロパティを参照先の別のセグメントと比較<br />。 </td> 
  </tr> 
  <tr> 
   <td>プロパティ - スクリプトの参照</td> 
   <td>ストアのプロパティとスクリプトの結果を比較<br />。 </td> 
  </tr> 
  <tr> 
   <td>セグメントリファレンス - スクリプトリファレンス</td> 
   <td>参照先セグメントとスクリプトの結果を比較<br />。 </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>値の比較時に比較のデータタイプが設定されていない場合（つまり、自動検出に設定されている場合）、ContextHub のセグメント化エンジンでは、javascript と同じように値が比較されます。期待されたタイプに値がキャストされず、誤った結果が生じる可能性があります。 次に例を示します。
>
>`null < 30 // will return true`
>
>したがって、[セグメントの作成](/help/sites-administering/segmentation.md#creating-a-new-segment)時に比較対象の値のタイプがわかる場合は、常に&#x200B;**データタイプ**&#x200B;を選択してください。次に例を示します。
>
>`profile/age` プロパティを比較する場合は、比較対象のタイプが&#x200B;**数値**&#x200B;であることが既にわかっているので、`profile/age` が設定されていなくても、`profile/age` が 30 より小さいという比較では、想定どおりに **false** が返されます。

### 参照 {#references}

次の参照を標準で使用して、スクリプトまたは別のセグメントに直接リンクできます。 コンポーネントブラウザーからエディターにドラッグできます。

<table> 
 <tbody> 
  <tr> 
   <td>セグメントの参照<br /> </td> 
   <td>参照先セグメントを評価</td> 
  </tr> 
  <tr> 
   <td>スクリプト参照</td> 
   <td>参照先セグメントをします。詳しくは、次の「<a href="/help/sites-administering/segmentation.md#using-script-references">スクリプト参照の使用</a>」の節を参照してください。</td> 
  </tr> 
 </tbody> 
</table>

## 新しいセグメントの作成 {#creating-a-new-segment}

新しいセグメントを定義するには、次の手順に従います。

1. [セグメントへのアクセス](/help/sites-administering/segmentation.md#accessing-segments)後、「作成」ボタンをクリックまたはタップし、「**ContextHub セグメントを作成**」を選択します。

   ![chlimage_1-311](assets/chlimage_1-311.png)

1. 「**新しい ContextHub セグメント**」で、セグメントのタイトルと必要に応じてブースト値を入力し、「**作成**」をタップまたはクリックします。

   ![chlimage_1-312](assets/chlimage_1-312.png)

   各セグメントには、重み付け係数として使用されるブーストパラメーターがあります。複数のセグメントが有効である場合、数値が小さいセグメントよりも、数値が大きいセグメントのほうが優先して選択されます。

   * 最小値：`0`
   * 最大値：`1000000`

1. 比較または参照をセグメントエディターにドラッグすると、デフォルトの AND コンテナに表示されます。
1. 新しい参照またはセグメントの「設定」オプションをダブルクリックまたはタップして、特定のパラメーターを編集します。 この例では、サンノゼのユーザーをテストしています。

   ![screen_shot_2012-02-02at103135am](assets/screen_shot_2012-02-02at103135am.png)

   常に **データタイプ** できれば、比較が適切に評価されていることを確認します。 詳しくは、 [比較](/help/sites-administering/segmentation.md#comparisons) を参照してください。

1. クリック **OK** 定義を保存するには、次の手順に従います。
1. 必要に応じてその他のコンポーネントを追加します。AND と OR の比較のコンテナコンポーネントを使用して、ブール式を作成できます ( [AND および OR コンテナの使用](/help/sites-administering/segmentation.md#using-and-and-or-containers) を参照 )。 セグメントエディターを使用すると、不要になったコンポーネントを削除したり、ステートメント内の新しい位置にドラッグしたりできます。

### AND コンテナと OR コンテナの使用 {#using-and-and-or-containers}

AND および OR コンテナコンポーネントを使用すると、AEMで複雑なセグメントを作成できます。 これをおこなう場合、次の基本的なポイントに注意すると役立ちます。

* 定義の最上位レベルは必ず、最初に作成された AND コンテナになります。これは変更できませんが、他のセグメント定義には影響しません。
* コンテナのネストが意味をなすようにします。 コンテナは、ブール式の括弧として表示できます。

次の例は、アドビのプライムエイジグループに属すると見なされる訪問者を選択するために使用されます。

30～59 歳の男性

OR

30～59 歳の女性

最初に、OR コンテナコンポーネントをデフォルトの AND コンテナ内に配置します。OR コンテナ内に 2 つの AND コンテナを追加し、それらの両方にプロパティまたは参照コンポーネントを追加できます。

![screen_shot_2012-02-02at105145am](assets/screen_shot_2012-02-02at105145am.png)

### スクリプト参照の使用 {#using-script-references}

スクリプト参照コンポーネントを使用すると、セグメントプロパティの評価を外部スクリプトに委任できます。 スクリプトを適切に設定したら、セグメント条件の他のコンポーネントとして使用できます。

#### 参照するスクリプトの定義 {#defining-a-script-to-reference}

1. `contexthub.segment-engine.scripts` クライアントライブラリにファイルを追加します。
1. 値を返す関数を実装します。 次に例を示します。

   ```
   ContextHub.console.log(ContextHub.Shared.timestamp(), '[loading] contexthub.segment-engine.scripts - script.profile-info.js');
   
   (function() {
       'use strict';
   
       /**
        * Sample script returning profile information. Returns user info if data is available, false otherwise.
        *
        * @returns {Boolean}
        */
       var getProfileInfo = function() {
           /* let the SegmentEngine know when script should be re-run */
           this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
           this.dependOn(ContextHub.SegmentEngine.Property('profile/givenName'));
   
           /* variables */
           var name = ContextHub.get('profile/givenName');
           var age = ContextHub.get('profile/age');
   
           return name === 'Joe' && age === 123;
       };
   
       /* register function */
       ContextHub.SegmentEngine.ScriptManager.register('getProfileInfo', getProfileInfo);
   
   })();
   ```

1. スクリプトを `ContextHub.SegmentEngine.ScriptManager.register` に登録します。

その他のプロパティに依存するスクリプトでは、`this.dependOn()` を呼び出す必要があります。例えば、スクリプトが `profile/age` に依存する場合は次のようになります。

```
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### スクリプトの参照 {#referencing-a-script}

1. ContextHub セグメントを作成します。
1. 追加 **スクリプト参照** コンポーネントをセグメントの目的の場所に配置します。
1. の編集ダイアログを開きます。 **スクリプト参照** コンポーネント。 If [適切に設定](/help/sites-administering/segmentation.md#defining-a-script-to-reference)を使用する場合、スクリプトは **スクリプト名** 」ドロップダウンリストから選択できます。

## セグメントの適用のテスト {#testing-the-application-of-a-segment}

セグメントを定義したら、**[ContextHub](/help/sites-authoring/ch-previewing.md)** を使用して、考えられる結果についてテストすることができます。

1. ページのプレビュー
1. ContextHub アイコンをクリックして ContextHub ツールバーを表示します。
1. 作成したセグメントに一致するペルソナを選択
1. ContextHub は、選択したペルソナに適したセグメントを解決します

例えば、Prime Age Group のユーザーを識別するためのシンプルなセグメント定義は、ユーザーの年齢と性別に基づく単純なセグメント定義です。 これらの条件に一致する特定のペルソナを読み込むと、次のようにセグメントが正常に解決されたかどうかがわかります。

![screen_shot_2012-02-02at105926am](assets/screen_shot_2012-02-02at105926am.png)

解決されていない場合は次のようになります。

![screen_shot_2012-02-02at110019am](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>すべての特性は即座に解決されますが、ほとんどの場合はページの再読み込み時にのみ変更されます。

このようなテストは、コンテンツページで、ターゲットコンテンツおよび関連する **アクティビティ** および **エクスペリエンス**.

上記のプライムエイジグループセグメントの例を使用してアクティビティとエクスペリエンスを設定した場合は、「 」アクティビティを使用してセグメントを簡単にテストできます。 アクティビティの設定について詳しくは、 [ターゲットコンテンツのオーサリングに関するドキュメント](/help/sites-authoring/content-targeting-touch.md).

1. ターゲットコンテンツを設定したページの編集モードでは、コンテンツがターゲット設定されているのをコンテンツ上の矢印アイコンで確認できます。

   ![chlimage_1-313](assets/chlimage_1-313.png)

1. プレビューモードに切り替えてから、ContextHub を使用して、エクスペリエンスに設定されているセグメント化と一致しないペルソナに切り替えます。

   ![chlimage_1-314](assets/chlimage_1-314.png)

1. エクスペリエンスに設定されているセグメント化と一致するペルソナに切り替え、それに応じてエクスペリエンスが変化することを確認します。

   ![chlimage_1-315](assets/chlimage_1-315.png)

## セグメントの使用 {#using-your-segment}

セグメントを使用して、特定のターゲットオーディエンスに表示する実際のコンテンツを制御します。 オーディエンスおよびセグメントについて詳しくは、[オーディエンスの管理](/help/sites-authoring/managing-audiences.md)を参照してください。オーディエンスおよびセグメントを使用したコンテンツのターゲティングについては、[ターゲットコンテンツのオーサリング](/help/sites-authoring/content-targeting-touch.md)を参照してください。
