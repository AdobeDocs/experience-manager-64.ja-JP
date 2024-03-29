---
title: 「チュートリアル：インタラクティブ通信の計画」
seo-title: Plan your Interactive Communication
description: インタラクティブ通信用の分析の計画
seo-description: Plan the anatomy for your Interactive Communication
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
feature: Interactive Communication
exl-id: 40f6297d-7238-4e56-9fd1-6df3a6362724
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 23%

---

# チュートリアル：インタラクティブ通信の計画 {#tutorial-plan-the-interactive-communication}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

インタラクティブ通信用の分析の計画

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

これは、「[最初のインタラクティブ通信の作成](/help/forms/using/create-your-first-interactive-communication.md)」シリーズを構成するチュートリアルです。チュートリアルの使用例を理解、実行、デモするために、時系列に従うことをお勧めします。

インタラクティブ通信を計画する際の最初の手順は、インタラクティブ通信のコンテンツを最終化することです。 法務、金融、サポート、マーケティングなどの部門の専門家が、コンテンツの最終処理に役立ちます。 コンテンツが確定したら、そのコンテンツを分析して、インタラクティブ通信の作成に必要な様々なアセットタイプを特定する必要があります。

## 計画に関する考慮事項 {#planning-considerations}

インタラクティブ通信には、次の要素が含まれます。

* **静的テキスト** 多くの場合、インタラクティブ通信の一部が含まれます。この部分は、本質的に汎用で、すべての顧客との通信に含まれます。 例えば、ヘッダー、フッター、敬称、免責事項などです。
* **バックエンドシステム（フォームデータモデル）からのデータ** は顧客固有で、インタラクティブ通信と動的に結合されます。 例えば、ポリシー番号や住所をフォームデータモデルを使用してソースにすることができます。
* **レイアウトまたはテンプレート** インタラクティブ通信の印刷版と Web 版の場合
* **注文** インタラクティブ通信内に様々な段落が表示されます。
* 送信する前に通信をカスタマイズする&#x200B;**現場の社員が入力したデータ（エージェント UI）**。例えば、支払い期限です。

* **条件付きデータ** の値は、事前定義された条件に基づいて設定されます。 例えば、インタラクティブ通信が生成された際の日付です。
* **リポジトリに保存された画像**：ロゴや署名画像など。 企業ロゴなどの画像は、ほとんどまたはすべてのインタラクティブ通信に表示されます。
* **グラフと表** インタラクティブ通信で複雑なデータを簡単に表示するために必要

## インタラクティブ通信の分析 {#anatomy-of-the-interactive-communication}

インタラクティブ通信の作成に使用するコンテンツと要素を確定したら、インタラクティブ通信の分析を作成できます。 解剖学には、 [計画に関する考慮事項](/help/forms/using/planning-interactive-communications.md#planning-considerations) 」セクションに入力します。 このユースケースでは、通信事業者が顧客に送る月次請求の分析例を次に示します。

解剖学には、次の入力モードを持つデータが含まれます。

* 静的テキスト
* フォームデータモデル
* エージェント UI
* 条件付きデータ
* 画像

各セクションの太字のテキストは静的テキストを表します。データベースには、顧客、請求書、通話テーブルが含まれます。フォームデータモデルは、これらのテーブルのいずれかのデータを受信することができます。詳しくは、[フォームデータモデルの作成](create-form-data-model-tutorial.md)を参照してください。

次の表に、インタラクティブ通信の分析における各フィールドのデータソースを示します。

<table> 
 <tbody>
  <tr>
   <td>セクション</td> 
   <td>静的テキスト</td> 
   <td>FDM </td> 
   <td>エージェント UI</td> 
   <td>画像</td> 
  </tr>
  <tr>
   <td>請求明細</td> 
   <td><p>請求書番号</p> <p>請求日</p> <p>請求期間</p> <p>プラン</p> </td> 
   <td><p>の値 <strong>プラン </strong>フィールド</p> <p>表 — 顧客</p> </td> 
   <td><p>次のフィールドの値：</p> 
    <ul> 
     <li>請求書番号</li> 
     <li>請求日</li> 
     <li>請求期間</li> 
    </ul> <p> </p> </td> 
   <td>--</td> 
  </tr>
  <tr>
   <td>顧客の詳細</td> 
   <td><p>供給場所</p> <p>都道府県コード</p> <p>モバイル番号</p> <p>代替連絡先番号</p> <p>関係番号</p> <p>接続数</p> </td> 
   <td><p>次のフィールドの値：</p> 
    <ul> 
     <li>名前</li> 
     <li>アドレス</li> 
     <li>モバイル番号</li> 
     <li>代替連絡先番号</li> 
     <li>関係番号</li> 
    </ul> <p>表 — 顧客</p> </td> 
   <td><p>次のフィールドの値：</p> 
    <ul> 
     <li>供給場所</li> 
     <li>都道府県コード</li> 
     <li>接続数</li> 
    </ul> </td> 
   <td>--</td> 
  </tr>
  <tr>
   <td>請求の要約</td> 
   <td><p>前の残高</p> <p>支払い</p> <p>調整</p> <p>現在の請求期間の請求</p> <p>支払額</p> <p>期限</p> </td> 
   <td><p>「<strong>現在の請求期間の料金</strong>」フィールドの値</p> <p>表 — 請求</p> </td> 
   <td><p>次のフィールドの値：</p> 
    <ul> 
     <li>前の残高</li> 
     <li>支払い</li> 
     <li>調整</li> 
     <li>支払額</li> 
     <li>期限</li> 
    </ul> </td> 
   <td>--</td> 
  </tr>
  <tr>
   <td>請求概要</td> 
   <td><p>通話料</p> <p>会議通話料</p> <p>SMS 料金 </p> <p>モバイルインターネット料金</p> <p>全国ローミング料金</p> <p>国際ローミング料金</p> <p>付加価値サービス料</p> <p>合計請求額</p> <p>買掛金合計</p> <p>付加価値サービス料金フィールドの条件</p> </td> 
   <td><p>次のフィールドの値：</p> 
    <ul> 
     <li>通話料</li> 
     <li>会議通話料</li> 
     <li>SMS 料金 </li> 
     <li>モバイルインターネット料金</li> 
     <li>全国ローミング料金</li> 
     <li>国際ローミング料金</li> 
     <li>付加価値サービス料</li> 
     <li>合計請求額（usagecharges 計算済みフィールド）</li> 
     <li>合計支払金額（usagecharges 計算フィールド）</li> 
    </ul> <p>表 — 請求</p> </td> 
   <td>フィールドがありません</td> 
   <td>--</td> 
  </tr>
  <tr>
   <td>通話項目別 — 発信</td> 
   <td><p>列名：</p> 
    <ul> 
     <li>日付</li> 
     <li>時刻</li> 
     <li>番号</li> 
     <li>期間</li> 
     <li>料金</li> 
    </ul> </td> 
   <td><p>すべての値</p> <p>表 — 呼び出し</p> </td> 
   <td>フィールドがありません</td> 
   <td>--</td> 
  </tr>
  <tr>
   <td>今すぐ支払う</td> 
   <td>--</td> 
   <td>--</td> 
   <td>--</td> 
   <td>PayNow</td> 
  </tr>
  <tr>
   <td>付加価値サービス</td> 
   <td>--</td> 
   <td>--</td> 
   <td>--</td> 
   <td>ValueAddedServices</td> 
  </tr>
 </tbody>
</table>
