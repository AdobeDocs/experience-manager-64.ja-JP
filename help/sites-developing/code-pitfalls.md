---
title: コードの落とし穴
seo-title: コードの落とし穴
description: AEM の開発時に避けるべき一般的なコードの落とし穴
seo-description: AEM の開発時に避けるべき一般的なコードの落とし穴
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
exl-id: f39910cf-1875-43fc-bfb5-259b9d8f135d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 94%

---

# コードの落とし穴{#code-pitfalls}

## Java コードで Sling Binding を使用しない {#avoid-sling-bindings-in-java-code}

Sling Binding はほとんどの場合、サービスにアクセスする方法として適切ではありません。代わりに、*@Reference* または *@Inject* 注釈を使用してください。

## Javaコード{#avoid-thread-interrupt-in-java-code}でのThread.interruptの回避

*Thread.interrupt* を不適切なタイミングで呼び出すと、Lucene ファイルや永続キャッシュファイルを含め、ファイルが閉じられることがあるので、危険です。

## Java 同期を ReadWriteLock とともに使用しない  {#avoid-mixing-java-synchronization-with-readwritelocks}

競合状態が発生し、最終的にコードがデッドロックに陥ることがあります。
