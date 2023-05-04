---
title: AEM 6.4 における e コマースリポジトリの再構築
seo-title: E-Commerce Repository Restructuring in AEM 6.4
description: AEM 6.4 e コマースの新しいリポジトリ構造に移行するために必要な変更方法について説明します。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for E-Commerce.
uuid: 1fff1a4b-c8d0-4016-92fb-e2ea26e3a302
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 28c92e7d-2106-4333-afa6-c5528a00d7b4
feature: Upgrading
exl-id: 6adcc1a4-eb0f-4410-8219-dbd7e6bbe469
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 42%

---

# AEM 6.4 における e コマースリポジトリの再構築{#e-commerce-repository-restructuring-in-aem}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md)の親ページで説明しているように、AEM 6.4 にアップグレードする場合は、このページを参考に、AEM の e コマースソリューションに影響を及ぼすリポジトリ変更に伴う作業量を評価する必要があります。一部の変更ではAEM 6.4 のアップグレードプロセス中に作業が必要ですが、6.5 のアップグレードまで延期することもできます。

## 6.4 へのアップグレード時におこなう変更 {#with-upgrade}

### 製品、注文、コレクション、分類、発送方法、支払い方法のデータ {#product-order-collections-classifications-shipping-methods-and-payment-methods-data}

<table> 
 <tbody>
  <tr>
   <td><strong>以前の場所</strong></td> 
   <td><p><code>/etc/commerce/products</code></p> <p><code>/etc/commerce/orders</code></p> <p><code>/etc/commerce/collections</code></p> <p><code>/etc/commerce/classifications</code></p> <p><code>/etc/commerce/shipping-methods</code></p> <p><code>/etc/commerce/payment-methods</code></p> </td> 
  </tr>
  <tr>
   <td><strong>新しい場所</strong></td> 
   <td><p><code>/var/commerce/products</code></p> <p><code>/var/commerce/orders</code></p> <p><code>/var/commerce/collections</code></p> <p><code>/var/commerce/classifications</code></p> <p><code>/var/commerce/shipping-methods</code></p> <p><code>/var/commerce/payment-methods</code></p> </td> 
  </tr>
  <tr>
   <td><strong>再構築の手引き</strong></td> 
   <td><p>以下の <a href="/help/sites-deploying/lazy-content-migration.md" target="_blank">遅延移行</a> e コマースデータを移行するタスクです。</p> <p>次の手順を実行します。</p> 
    <ul> 
     <li>新しい場所を指すように古い場所の参照を調整します</li> 
     <li>古い場所から新しい場所にコンテンツを移動</li> 
     <li>古い場所を削除して、システム全体で新しい場所の使用を有効にします。</li> 
    </ul> <p>タスクの対象となる場所は次のとおりです。</p> 
    <ul> 
     <li>/etc/commerce/products</li> 
     <li>/etc/commerce/collections<br /> </li> 
     <li>/etc/commerce/orders<br /> </li> 
     <li>/etc/commerce/payment-methods<br /> </li> 
     <li>/etc/commerce/shipping-methods<br /> </li> 
    </ul> <p>大規模なカタログの場合は、次の Java システムプロパティをAEMに渡して、コマース移行タスクを個別に実行することをお勧めします。</p> <p><code>propertyname: com.adobe.upgrade.forcemigration</code></p> <p><code>property value: com.day.cq.compat.codeupgrade.impl.cq64.CQ64CommerceMigrationTask</code></p> <p>移行後、AEM の再起動が必要です。</p> </td> 
  </tr>
  <tr>
   <td><strong>備考</strong></td> 
   <td>該当なし<br /> </td> 
  </tr>
 </tbody>
</table>
