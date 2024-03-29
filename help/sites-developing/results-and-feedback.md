---
title: 結果の追跡とフィードバックの提供
seo-title: Tracking results and providing feedback
description: テストケースの定義方法と場所、および結果のテスト計画は、独自の判断でおこないます
seo-description: How and where you define the test cases, and the resulting test plan, is at your own discretion
uuid: b4b811d4-4ca0-4477-a866-b262f9a698f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: testing
content-type: reference
discoiquuid: 2fff5f64-d330-4b32-a861-1f5315363b69
exl-id: 976f00d0-0b7a-4d5e-bfbc-44c2504ca2f6
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 42%

---

# 結果の追跡とフィードバックの提供{#tracking-results-and-providing-feedback}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

テストケースの定義方法と場所、および結果のテスト計画は、自由に指定できます。多くのツールを使用できます。

ただし、選択する方法やツールに関係なく、保存される情報は、

* 次のようにする必要があります。

   * テストケースとその結果のトラッキングに限定する。これにより、メンテナンスが明快なままになり、テストの進行状況を明確に把握できます。
   * 1 つのコピーとして維持され、プロジェクトチームのすべての適切なメンバーが使用できます。
   * 中立で、テスト結果に限定する。テスト結果に起因するすべてのアクションを決定するのは、プロジェクトマネージャーの責任です。

* 次のようには、しないようにします。

   * トラッキング情報を含めるように拡張する（バグ、新機能、後続のアクションも同様）この情報は他の場所で管理する必要があります。再び、多くのツールが使用可能です。
