---
title: Content Disposition フィルター
seo-title: Content Disposition Filter
description: XSS 攻撃を防ぐためのコンテンツ廃棄フィルターの使用方法を説明します。
seo-description: Learn how to use the Content Disposition Filter to prevent XSS attacks.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: bb022f6b-938b-4421-8860-4c22aecf5b85
source-git-commit: 8cc85728be93d58e3aaee69c96f59ee98d5484a1
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 30%

---

# Content Disposition フィルター {#content-disposition-filter}

Content Disposition フィルターは、SVG ファイルへの XSS 攻撃に対するセキュリティ機能です。

インストールが完了すると、フィルターはすべてのアセットへのアクセスをブロックします。例えば、オンラインでPDFを表示できなかった。 このセクションでは、必要に応じてフィルターを設定する方法について説明します。

## Content Disposition フィルターの設定 {#configure-content-disposition-filter}

次の項目を表示すると、 [GitHub の Apache Sling Content Disposition Filter。](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)

「Content Disposition Filter」のオプションには次の機能があります。

* **コンテンツ配置パス：** フィルターが適用されるパスのリストの後に、そのパスで除外する mime タイプのリストが続きます。このパスは絶対パスで、ワイルドカード (`*`) の末尾に置き換え、すべてのリソースパスを、指定されたパスプレフィックスと照合します。 例： `/content/*:image/jpeg,image/svg+xml` が `/content` jpg および svg 画像を除く

* **除外されたリソースのパス：** 除外されたリソースのリストでは、各リソースパスを絶対パスと完全修飾パスとして指定する必要があります。 プレフィックスマッチング／ワイルドカードはサポートされていません。

* **すべてのリソースパスに対して有効にする：** このフラグは、除外されたリソースパスで定義された除外されたパスを除き、すべてのパスに対してこのフィルタを有効にするかどうかを制御します。 これを「true」に設定すると、Content Disposition パスが無視されます。設定とは無関係に、という名前のプロパティを含むリソースパスのみが対象となります。 `jcr:data` または
   `jcr:content jcr:data`
