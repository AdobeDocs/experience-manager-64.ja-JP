---
title: AEM アプリケーション用の設定
seo-title: Configuring for AEM Apps
description: AEM Apps の設定方法を説明します。
seo-description: Learn how to configure AEM Apps.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: 593a588c-02f1-4b48-ac57-9348d6652bcc
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 78%

---

# AEM アプリケーション用の設定{#configuring-for-aem-apps}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager アプリケーションには、アプリケーションのコンテンツを OTA（Over The Air）で更新する機能が提供されています。更新されたコンテンツはパブリッシュインスタンスに格納されます。デバイス上のアプリケーションがパブリッシュインスタンスに接続して更新を確認できるようにするには、空のリファラーヘッダーを使用できるようにパブリッシュインスタンスを設定する必要があります。

## 空のリファラーヘッダーの設定 {#configuring-empty-referrer-header}

リファラーフィルターサービスを設定するには：

* Apache Felix コンソール（**設定**）を次の場所で開きます。
* https://&lt;server>:&lt;port>/system/console/configMgr
* admin としてログインします。
* **Configurations** メニューで *Apache Sling Referrer Filter* を選択します。
* 「Allow Empty」フィールドにチェックマークを入れて、空のリファラーヘッダーを使用できるようにします。
* 「**保存**」をクリックして変更を保存します。

![chlimage_1-58](assets/chlimage_1-58.png)

詳しくは、[OSGI 設定](/help/sites-deploying/osgi-configuration-settings.md)および [セキュリティチェックリスト - クロスサイトリクエストフォージェリに関する問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)を参照してください。
