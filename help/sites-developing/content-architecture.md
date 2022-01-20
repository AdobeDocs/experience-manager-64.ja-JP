---
title: コンテンツのアーキテクチャ
seo-title: Content Architecture
description: コンテンツの設計に関するヒント（ヒント — すべてがコンテンツ）
seo-description: Tips for architecting your content in Adobe Experience Manager (AEM). (hint - everything is content)
uuid: fef2bf0f-70ec-4621-8479-a62b7e1fbc07
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: ca46b74c-6114-458b-98c0-2a93abffcdc3
exl-id: 9fff10fb-4b65-459a-a7a7-6ee9c0c26bf5
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 60%

---

# コンテンツのアーキテクチャ{#content-architecture}

## David&#39;s Model に準拠 {#follow-david-s-model}

David&#39;s Model は何年も前に David Nuescheler によって作成されたものですが、その考え方は今でも当てはまります。David&#39;s Model の主な定義は次のとおりです。

* データが最初に取り込まれ、構造が後になります。 多分。
* コンテンツ階層は手動で設計し、成り行き任せにしない。
* ワークスペースは `clone()`, `merge()`、および `update()`.
* 同じ名前の兄弟に注意する。
* 参照は害が多いと考えられる。
* ファイルはあくまでもファイル。
* ID は悪いです。

David&#39;s Model は、Jackrabbit Wiki の [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### すべてがコンテンツである {#everything-is-content}

あらゆるデータの格納には、データベースなど別個のサードパーティデータソースを利用するのではなく、リポジトリを使用する必要があります。このことは、作成済みコンテンツ、バイナリデータ（画像など）、コード、設定などに当てはまります。このようにすると、1 つの API セットを使用してすべてのコンテンツを管理でき、レプリケーションによってこのコンテンツのプロモーションを管理できます。また、バックアップやログの単一ソースを得ることができます。

### 「コンテンツモデルが第一」というデザインの原則の使用 {#use-the-content-model-first-design-principle}

新機能をビルドするときには、常に JCR コンテンツ構造の設計から始め、次にデフォルトの Sling サーブレットを使用したコンテンツの読み込みおよび書き込みに進みます。これにより、標準のアクセス制御メカニズムで実装が適切に動作し、不要な CRUD スタイルのサーブレットを生成するのを防ぐことができます。

### RESTful に準拠 {#be-restful}

サーブレットをパスではなく resourceType に基づいて定義する必要があります。これにより、JCR アクセス制御を使用し、REST 原則に準拠し、リクエストで提供されるリソースとリソースのリゾルバーを使用できます。 また、クライアント側から URL を変更する必要なく、サーバー側で URL をレンダリングするスクリプトを変更できます。一方、セキュリティを強化するために、クライアント側からサーバー側の実装の詳細を非表示にできます。

### 新しいノードタイプの定義を回避 {#avoid-defining-new-node-types}

ノードタイプはインフラストラクチャレイヤー内の下位レベルで機能し、ほとんどの要件は nt:unstructured、oak:Unstructured、sling:Folder または cq:Page のノードタイプに割り当てられた sling:resourceType を使用することで満たすことができます。ノードタイプはリポジトリ内のスキーマと同じで、ノードタイプの変更は最終的に非常に高価になる場合があります。

### JCR の命名規則に準拠 {#adhere-to-naming-conventions-in-the-jcr}

命名規則に準拠することにより、コードベースの一貫性が高まるので、不具合の発生率を低下させ、システムで作業する開発者の生産性を高めることができます。AEMの開発では、次の規則をAdobeが使用します。

* ノード名

   * すべて小文字
   * 単語間の区切りにハイフンを使用

* プロパティ名

   * キャメルケース、小文字で開始

* コンポーネント（JSP/HTML）

   * すべて小文字
   * 単語間の区切りにハイフンを使用
