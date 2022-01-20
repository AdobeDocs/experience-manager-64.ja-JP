---
title: AEM アプリケーション用の設定
seo-title: Configuring for AEM Apps
description: AEM アプリケーションの設定方法について説明します。
seo-description: Learn how to configure AEM Apps.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: 593a588c-02f1-4b48-ac57-9348d6652bcc
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 24%

---

# AEM アプリケーション用の設定{#configuring-for-aem-apps}

Adobe Experience Manager Apps を使用すると、アプリケーションのコンテンツを大気中 (OTA) で更新できます。 更新されたコンテンツは、パブリッシュインスタンスに保存されます。デバイス上のアプリがパブリッシュインスタンスに接続して更新を確認できるようにするには、パブリッシュインスタンスが空のリファラーヘッダーを許可するように設定されている必要があります。

## 空のリファラーヘッダーの設定 {#configuring-empty-referrer-header}

リファラーフィルターサービスを設定するには：

* Apache Felix コンソール (**設定**):
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* admin としてログインします。
* 内 **設定** メニュー： *Apache Sling Referrer Filter*
* 「空の値を許可」フィールドをチェックして、リファラーヘッダーを空にするか、見つからないヘッダーを許可します。
* 「**保存**」をクリックして変更を保存します。

![chlimage_1-58](assets/chlimage_1-58.png)

詳しくは、 [OSGi 設定](/help/sites-deploying/osgi-configuration-settings.md) および [セキュリティチェックリスト — クロスサイトリクエストフォージェリに関する問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) 詳しくは、を参照してください。
