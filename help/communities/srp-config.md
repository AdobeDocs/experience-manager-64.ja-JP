---
title: ストレージ設定
seo-title: ストレージ設定
description: ストレージ設定コンソールへのアクセス方法
seo-description: ストレージ設定コンソールへのアクセス方法
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Administrator
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 67%

---


# ストレージ設定 {#storage-configuration}

ストレージ設定では、コミュニティコンテンツ用に選択されているストレージを確認できます。コミュニティコンテンツはユーザー生成コンテンツ（UGC）とも呼ばれます。

この設定では、UGC アクセス時に使用されるストレージリソースプロバイダー（SRP）の実装に関する AEM Communities のコード情報が提供されます。設定は、AEM のデプロイ時に確立したトポロジを反映している必要があります。

ストレージオプションとデプロイメントトポロジの説明については、以下を参照してください。

* [コミュニティコンテンツストア](working-with-srp.md)
* [推奨されるトポロジ](topologies.md)

## ストレージ設定コンソール  {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

オーサー環境でストレージ設定コンソールに移動するには、

* グローバルナビゲーションから：**[!UICONTROL ツール/コミュニティ/ストレージ設定]**

デフォルトの JCR 以外のストレージオプションを選択するには、

* オプションを選択します。
* 適切な設定

   * [MSRP](msrp.md#select-msrp)の選択の詳細を参照
   * [DSRP](dsrp.md#select-dsrp)の選択の詳細を参照
   * [ASRP](asrp.md#select-asrp)の選択の詳細を参照

* **[!UICONTROL 送信]**&#x200B;を選択

### JCR ストレージについて {#about-jcr-storage}

選択しなかった場合は、AEM リポジトリである JCR がデフォルトで使用されることに注意してください。

JCRは、作成者と発行環境が共有する共通のストアではありません。*a1/>*&#x200B;コミュニティコンテンツは、そのコンテンツが作成された作成者または発行環境からのみ表示されます。

詳しくは、[JCR ストア](jsrp.md)を参照してください。

>[!NOTE]
>
>`/etc/socialconfig`の下にノード`srpc`がない場合は、デフォルトの[JCRストア](jsrp.md)を示します。

