---
title: ストレージ設定
seo-title: Storage Configuration
description: ストレージ構成コンソールへのアクセス方法
seo-description: How to access the Storage Configuration Console
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Admin
exl-id: 905b6dc5-cf17-4f58-a687-27e2910a0729
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 6%

---

# ストレージ設定 {#storage-configuration}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

ストレージ設定は、コミュニティコンテンツ ( ユーザー生成コンテンツ (UGC) とも呼ばれます ) 用に選択されたストレージを識別する手段です。

この設定は、UGC へのアクセス時に使用するストレージリソースプロバイダー (SRP) の実装をAEM Communitiesコードに通知し、AEMのデプロイ時に確立されたトポロジを反映する必要があります。

ストレージオプションとデプロイメントトポロジの詳細については、

* [コミュニティコンテンツストア](working-with-srp.md)
* [推奨されるトポロジ](topologies.md)

## ストレージ設定コンソール {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

オーサー環境で、ストレージ設定コンソールに到達するには

* グローバルナビゲーションから： **[!UICONTROL ツール/コミュニティ/ストレージ設定]**

デフォルトの JCR 以外のストレージオプションを選択するには：

* オプションを選択
* 適切な設定

   * 詳細を見る [MSRP の選択](msrp.md#select-msrp)
   * 詳細を見る [DSRP の選択](dsrp.md#select-dsrp)
   * 詳細を見る [ASRP の選択](asrp.md#select-asrp)

* 「**[!UICONTROL 送信]**」を選択します。

### JCR ストレージについて {#about-jcr-storage}

何も選択しない場合、デフォルトはAEMリポジトリ (JCR) になります。

JCR は *not* オーサー環境とパブリッシュ環境で共有される共通ストア。 コミュニティコンテンツは、作成先のオーサー環境またはパブリッシュ環境からのみ表示されます。

訪問 [JCR ストア](jsrp.md) を参照してください。

>[!NOTE]
>
>ノードがない `srpc`under `/etc/socialconfig` デフォルトを示します [JCR ストア](jsrp.md).
