---
title: コンテンツのプロパティとノード
seo-title: Content Properties and Nodes
description: 'このページでは、コンテンツのプロパティとノードについて説明します。  '
seo-description: Follow this page to learn about content properties and nodes.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
exl-id: 85a367fe-a124-42af-ae3e-fe4d10425ea1
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 49%

---

# コンテンツのプロパティとノード {#content-properties-and-nodes}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

記事、バナーおよびコレクションは、AEM では cq:Pages として表されます。

これらは、すべての cq:Pages に共通するプロパティを共有するとともに、以下に示す Adobe Experience Manager（AEM）Mobile On-Demand Services のメタデータおよび統合をサポートする他のプロパティも備えています。

以下の表では、コンテンツのプロパティとノードについて説明します。

## 共通統合プロパティ {#common-integration-properties}

| **プロパティ名** | **タイプ** | **デフォルト値または期待値** | **説明** |
|---|---|---|---|
| dps-id | 文字列 |  | AEM Mobileに割り当てられ、AEMによって保存され、AEM MobileにアップロードまたはAEM Mobileから読み込まれた後にによって割り当てられ、 |
| dps-resourceType | 文字列 | dps:Article | dps:Banner | dps:Collection | エンティティタイププロパティ |
| dps-version | 文字列 |  | AEM Mobileエンティティのバージョン（aem-id の完全な内部にも含まれる） |
| dps-lastSynced | 日付 |  | AEM MobileからAEMへの最後の同期/インポート日 |
| dps-lastUploaded | 日付 |  | AEMからAEM Mobileへの最後のアップロード日 |
| dps-lastUploadedBy | String:userid |  | AEMからAEM Mobileへの最後のアップロード要求を実行した id ユーザー |

## コアメタデータプロパティ {#core-metadata-properties}

| プロパティ名 | タイプ | デフォルト値または期待値 |
|--- |--- |--- |
| dps-title | 文字列 |  |
| dps-shortTitle | 文字列 |  |
| dps-abstract | 文字列 |  |
| dps-shortAbstract | 文字列 |  |
| dps-department | 文字列 |  |
| dps-category | 文字列 |  |
| dps-keywords | 文字列[] |  |
| dps-internalKeywords | 文字列[] |  |
| dps-importance | 文字列[] | {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;} からの重要度 |

### 記事 {#articles}

| **プロパティ名** | **タイプ** | **デフォルト値または期待値** |
|---|---|---|
| dps-author | 文字列 |  |
| dps-authorURL | 文字列 |  |
| dps-hideFromBrowsePage | ブール演算式 |  |
| dps-access | 文字列 | {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} からの ProtectedAccess |
| **Social** |  |  |
| dps-socialShareURL | 文字列 |  |
| dps-articleText | 文字列 |  |
| dps-url | 文字列 |  |

### バナー {#banners}

| **プロパティ名** | **タイプ** | **デフォルト値または期待値** |
|---|---|---|
| dps-tapAction |  | {webLink} の TapAction |
| dps-tapActionUrl |  |  |

### コレクション {#collections}

| プロパティ名 | タイプ | デフォルト値または期待値 |
|--- |--- |--- |
| dps-productId | 文字列 |  |
| dps-readingPosition | 文字列 | {&quot;reset&quot;,&quot;retain&quot;} から |
| dps-horizontalSwipe | ブール演算式 |  |
| dps-allowDownload | ブール演算式 |  |
| dps-openDefault | 文字列 | {&quot;browsePage&quot;,&quot;contentView&quot;} から |
| dps-layout | 文字列 |  |

## コンテンツノード {#content-nodes}

### 共通ノード {#common-nodes}

| ノード名 | タイプ | デフォルト値または期待値 | 説明 |
|--- |--- |--- |--- |
| image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### エンティティ {#entities}

#### 記事 {#articles-1}

| ノード名 | タイプ | 期待値のデフォルト | 説明 |
|--- |--- |--- |--- |
| social-share-image |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### バナー {#banners-1}

| ノード名 | タイプ | 期待値のデフォルト | 説明 |
|---|---|---|---|
| 該当なし |  |  |  |

#### コレクション {#collections-1}

| ノード名 | タイプ | 期待値のデフォルト | 説明 |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
