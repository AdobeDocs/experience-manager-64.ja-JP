---
title: JSRP - JCR ストレージリソースプロバイダー
seo-title: JSRP - JCR Storage Resource Provider
description: JSRP は、通常、1 つのパブリッシュインスタンスと 1 つのオーサーインスタンスのデモ環境または開発環境に最適です
seo-description: JSRP is generally best suited for demonstration or development environments of one publish instance and one author instance
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Admin
exl-id: 73c59497-43fe-4e15-afda-e3cf5264696e
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 6%

---

# JSRP - JCR ストレージリソースプロバイダー {#jsrp-jcr-storage-resource-provider}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## JSRP について {#about-jsrp}

AEM Communitiesが JSRP をストレージオプションとして使用する場合（デフォルト）、コミュニティコンテンツは JCR に保存され、ユーザー生成コンテンツ (UGC) は、JSRP の投稿先のオーサーインスタンスまたはパブリッシュインスタンスからのみアクセスできます。

デプロイメントはシンプルなので、JSRP は、通常、1 つのパブリッシュインスタンスと 1 つのオーサーインスタンスのデモ環境または開発環境に最適です。

関連トピック [SRP オプションの特性](working-with-srp.md#characteristics-of-srp-options) および [推奨されるトポロジ](topologies.md).

## 設定 {#configuration}

### JSRP を選択 {#select-jsrp}

デフォルトでは、JSRP が UGC のストレージオプションです。

この [ストレージ設定コンソール](srp-config.md) では、使用する SRP の実装を指定するデフォルトのストレージ設定を選択できます。

オーサー環境で、ストレージ設定コンソールに移動します。

* グローバルナビゲーションから： **[!UICONTROL ツール/コミュニティ/ストレージ設定]**

![chlimage_1-234](assets/chlimage_1-234.png)

* 選択 **[!UICONTROL JCR ストレージリソースプロバイダー (JSRP)]**
* 「**[!UICONTROL 送信]**」を選択します。

### 設定の公開 {#publishing-the-configuration}

JSRP がデフォルト設定ですが、パブリッシュ環境で同じ設定がおこなわれるようにするには、次の手順を実行します。

* 作成者：

   * グローバルナビゲーションから： **[!UICONTROL ツール/導入/レプリケーション]**
   * 選択 **[!UICONTROL ツリーをアクティベート]**
   * **[!UICONTROL 開始パス]**:

      * 参照先 `/conf/global/settings/community/srpc/`
   * 選択 **[!UICONTROL 有効化]**


## ユーザーデータの管理 {#managing-user-data}

以下に関する情報： *ユーザー*, *ユーザープロファイル* および *ユーザーグループ*&#x200B;パブリッシュ環境に入力されることが多い場合は、次にアクセスします。

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## トラブルシューティング {#troubleshooting}

### UGC が JCR で表示されない {#ugc-not-visible-in-jcr}

ストレージオプションの設定を確認して、JSRP がデフォルトのプロバイダーに設定されていることを確認します。 デフォルトでは、ストレージリソースプロバイダーは JSRP です。

すべてのオーサーインスタンスとパブリッシュAEMインスタンスで、ストレージ設定コンソールに再度アクセスするか、AEMリポジトリを確認します。

* JCR で、 [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * 次を含まない [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) ノードの場合、ストレージプロバイダーが JSRP であることを意味します。
   * srpc ノードが存在し、ノードが含まれる場合 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration)の場合、デフォルト設定のプロパティでは JSRP をデフォルトのプロバイダーとして定義する必要があります

### UGC がオーサーインスタンスに表示されない {#ugc-not-visible-on-author-instance}

これはバグではありません。 JSRP の特徴は、パブリッシュ環境に入力されたコミュニティコンテンツがパブリッシュ環境でのみ表示されることです。

### UGC がパブリッシュインスタンスに表示されない {#ugc-not-visible-on-publish-instance}

単一のパブリッシュインスタンス、またはパブリッシュクラスターがデプロイされている場合は、次の手順に従います。 [UGC が JCR で表示されない](#ugc-not-visible-in-jcr).

パブリッシュファームがデプロイされている場合、JSRP の特徴は、コミュニティコンテンツが投稿先のパブリッシュインスタンスでのみ表示されることです。

UGC を任意のパブリッシュインスタンスから表示するには、パブリッシュクラスターが必要です。
