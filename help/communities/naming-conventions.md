---
title: 命名規則
seo-title: Naming Conventions
description: Java パッケージ名でのハイフン
seo-description: Hyphens in Java Package Name
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: f5a63642-9f2c-436f-bd40-4459545a0ddf
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 7%

---

# 命名規則 {#naming-conventions}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## Java パッケージ名でのハイフン {#hyphens-in-java-package-name}

Java クラスの場所を作成する場合、パッケージ名は、リポジトリフォルダーの場所と一致し、パス内のハイフンが適切にエスケープされる必要があります。

AEMの開発では、リポジトリ項目の名前にハイフンを使用することが推奨されますが、ハイフンは Java パッケージ名内では無効です。

基になる CRX プラットフォームでは、実際のアンダースコア「 」を区別できる必要があります。_&#39;およびハイフン&#39;-&#39; したがって、JCR では、ハイフンをその Unicode 値 (u002d) に置き換え、アンダースコア「 」でエスケープする必要があります_&#39;.

例えば、リポジトリのパスが **/apps/my-example/component/info/Info.java**、パッケージ名は `java package apps.my_002dexample.component.info;`

アンダースコアも同様にエスケープする必要があり、次のようにします。 `_` 次に `_005f`.
