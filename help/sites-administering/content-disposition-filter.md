---
title: Content Disposition フィルター
seo-title: Content Disposition フィルター
description: XSS攻撃を防ぐためのコンテンツ廃棄フィルターの使用方法を説明します。
seo-description: XSS攻撃を防ぐためのコンテンツ廃棄フィルターの使用方法を説明します。
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: bb022f6b-938b-4421-8860-4c22aecf5b85
translation-type: tm+mt
source-git-commit: 8cc85728be93d58e3aaee69c96f59ee98d5484a1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 30%

---

# Content Disposition フィルター {#content-disposition-filter}

Content Disposition フィルターは、SVG ファイルへの XSS 攻撃に対するセキュリティ機能です。

インストールが完了すると、フィルターはすべてのアセットへのアクセスをブロックします。例えば、PDFをオンラインで表示できなかった。 このセクションでは、必要に応じてフィルターを設定する方法について説明します。

## Content Disposition フィルターの設定  {#configure-content-disposition-filter}

GitHubで[Apache Sling Content Disposition Filterを表示できます。](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)

コンテンツ廃棄フィルターのオプションには、次の機能があります。

* **コンテンツ廃棄パス：フィルタ** ーが適用されるパスのリスト。次に、そのパスで除外するMIMEタイプのリストを指定します。このパスは絶対パスであり、最後にワイルドカード(`*`)を含めて、すべてのリソースパスを指定したパスプレフィックスと一致させます。次に例を示します。`/content/*:image/jpeg,image/svg+xml`は、jpgとsvg画像を除くすべてのノード（`/content`内）にフィルターを適用します

* **除外されたリソースパス：除外さ** れたリソースのリスト。各リソースパスは、絶対パスおよび完全修飾パスとして指定する必要があります。プレフィックスマッチング／ワイルドカードはサポートされていません。

* **Enable For All Resource Paths:** このフラグは、除外されたリソースパスで定義された除外されたパスを除き、すべてのパスに対してこのフィルタを有効にするかどうかを制御します。これを「true」に設定すると、Content Disposition パスが無視されます。構成とは無関係に、`jcr:data`という名前のプロパティを含むリソースパスのみが対象となります。
   `jcr:content jcr:data`
