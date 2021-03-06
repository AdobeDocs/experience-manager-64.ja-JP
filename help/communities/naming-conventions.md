---
title: 命名規則
seo-title: Naming Conventions
description: Java パッケージ名内のハイフン
seo-description: Hyphens in Java Package Name
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: f5a63642-9f2c-436f-bd40-4459545a0ddf
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 51%

---

# 命名規則 {#naming-conventions}

## Java パッケージ名内のハイフン {#hyphens-in-java-package-name}

Java クラスの場所を作成する際には、パッケージ名がリポジトリフォルダーの場所のパッケージ名と一致しており、パス内のハイフンが適切にエスケープされている必要がある点に注意してください。

AEM の開発では、リポジトリ項目の名前にハイフンを使用することが推奨されていますが、Java パッケージ名でハイフンを使用することはできません。

基になる CRX プラットフォームでは、実際のアンダースコア「 」を区別できる必要があります。_&#39;およびハイフン&#39;-&#39; したがって、JCR では、ハイフンをその Unicode 値 (u002d) に置き換え、アンダースコア「 」でエスケープする必要があります_&#39;.

例えば、リポジトリのパスが **/apps/my-example/component/info/Info.java**、パッケージ名は `java package apps.my_002dexample.component.info;`

アンダースコアも同様にエスケープする必要があり、次のようにします。 `_` 次に `_005f`.
