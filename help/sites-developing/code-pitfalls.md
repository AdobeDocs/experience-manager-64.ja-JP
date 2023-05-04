---
title: コードの落とし穴
seo-title: Code pitfalls
description: AEM向け開発時に避ける必要がある一般的なコーディングの落とし穴
seo-description: Common coding pitfalls to avoid when developing for AEM
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
exl-id: f39910cf-1875-43fc-bfb5-259b9d8f135d
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 13%

---

# コードの落とし穴{#code-pitfalls}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## Java コードでの Sling バインディングの回避 {#avoid-sling-bindings-in-java-code}

Sling バインディングは、90%のケースでサービスにアクセスするのに適していません。 代わりに、 *@Reference* または *@Inject* 注釈。

## Java コードで Thread.interrupt を使用しない {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* は、呼び出しが間違った時点で Lucene ファイルや永続キャッシュファイルを含むファイルを閉じる可能性があるので、危険です。

## Java 同期と ReadWriteLocks を混在させない {#avoid-mixing-java-synchronization-with-readwritelocks}

競合状態に陥り、コードが最終的にデッドロックに陥る可能性があります。
