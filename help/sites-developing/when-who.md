---
title: テスト - 実行のタイミングとテスター
seo-title: Testing - when and with whom?
description: 様々な役割をテストやプロジェクト開発の様々な段階に関与させることができます
seo-description: Various roles can be involved in testing and at various stages of project development
uuid: 431e8f06-80eb-4fb3-a4c7-2580608b0a1c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: testing
content-type: reference
discoiquuid: 6148f8e6-ab62-4eb8-8a2d-c431b8318000
exl-id: cba4a814-052b-4b9f-96f2-8c80b2766ecc
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 16%

---

# テスト - 実行のタイミングとテスター{#testing-when-and-with-whom}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

様々な役割をテストやプロジェクト開発の様々な段階に関与させることができます。

<table> 
 <tbody> 
  <tr> 
   <td>テストチーム</td> 
   <td>責任の範囲 </td> 
   <td>When...</td> 
  </tr> 
  <tr> 
   <td>開発チーム</td> 
   <td>開発チームは、単体テストと一部の統合テストを担当します。</td> 
   <td>これらのテストは、開発中に繰り返され、拡張されますが、チェーンの最初の段階です。</td> 
  </tr> 
  <tr> 
   <td>品質保証チーム</td> 
   <td><p>機能テストとパフォーマンステストをおこなうには、（適切な規模の）品質保証チームが必要です。</p> <p>これらは中立的で、専用のテスターです。ソフトウェアの黄金律は、開発者が自分の作業をテストしてはならないと常に言っています。</p> <p>このチームのメンバーは、Day プロジェクトチーム、パートナー、および/または顧客チームから取り込まれる場合があります。</p> </td> 
   <td><p>最初の関数リリースは、（現実的に可能な限り早く）テスト担当者に公開する必要があります。 初期の中間リリースは多くのバグを生み出す可能性がありますが、重要な問題に対する早期のフィードバックを提供できます。</p> </td> 
  </tr> 
  <tr> 
   <td>顧客テストチーム</td> 
   <td><p>選択したプロジェクトモデルによっては、顧客チームのメンバー、特に顧客サイトの作成者がテストに参加する予定があります。</p> <p>は次のように有利です。</p> 
    <ul> 
     <li><p>開発中のプロジェクトを顧客に体験してもらう。</p> </li> 
     <li><p>お客様からの早期のフィードバックを提供します。</p> </li> 
     <li><p>ユーザーは過去の経験に基づいて要望を述べる傾向にあり、できる限り早い段階から顧客をテストに参加させれば、新プロジェクトを実際に体験する機会が増える<i>。</i></p> </li> 
    </ul> </td> 
   <td><p>早期の関与は良いものですが、お客様が使用するリリースは安定しており、合理的な機能を備えている必要があります。</p> <p>第一印象は常に重要です。</p> </td> 
  </tr> 
 </tbody> 
</table>
