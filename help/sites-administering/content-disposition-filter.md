---
title: Content Disposition フィルター
seo-title: Content Disposition Filter
description: Content Disposition フィルターを使用して XSS 攻撃を防ぐ方法について説明します。
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
ht-degree: 73%

---

# Content Disposition フィルター {#content-disposition-filter}

コンテンツの配置フィルターは、SVGファイルに対する XSS 攻撃に対するセキュリティ機能です。

インストールが完了すると、フィルターはすべてのアセットへのアクセスをブロックします。 例えば、オンラインで PDF を表示することができなくなります。この節では、必要に応じてフィルターを設定する方法について説明します。

## Content Disposition フィルタの設定 {#configure-content-disposition-filter}

次の項目を表示すると、 [GitHub の Apache Sling Content Disposition Filter。](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)

Content Disposition フィルターのオプションには、次の機能があります。

* **Content Disposition パス：**&#x200B;フィルターが適用されるパスのリストの後に、そのパスで除外する MIME タイプのリストを追加したもの。このパスは絶対パスでなければならず、すべてのリソースパスを指定されたパスプレフィックスと一致させるため、末尾にワイルドカード（`*`）を含めることができます。例：`/content/*:image/jpeg,image/svg+xml` は、jpg および svg 画像を除く、`/content` 内のすべてのノードにフィルターを適用します。

* **除外されたリソースパス：**&#x200B;除外されたリソースのリストです。各リソースパスは絶対パスおよび完全修飾パスとして指定する必要があります。プレフィックスマッチング／ワイルドカードはサポートされていません。

* **すべてのリソースパスを有効化：**&#x200B;このフラグは、除外されたリソースパスで定義されたパス以外のすべてのパスに対して、このフィルターを有効にするかどうかを制御します。これを「true」に設定すると、Content Disposition パスが無視されます。設定とは無関係に、という名前のプロパティを含むリソースパスのみが対象となります。 `jcr:data` または
   `jcr:content jcr:data`
