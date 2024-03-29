---
title: アップグレード後にアンインストールされる廃止されたバンドルの一覧
seo-title: List of Obsolete Bundles Uninstalled After the Upgrade
description: AEM 6.3 へのアップグレード時に自動的にアンインストールされるバンドルの詳細を示すリストです。
seo-description: A list detailing the bundles that are automatically uninstalled when upgrading to AEM 6.3.
uuid: b015e857-31c1-4982-b71c-f3201b49ec8e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 797a6f3b-d2a8-4835-81ab-a1602677417f
feature: Upgrading
exl-id: 0f075a01-f286-4e16-9061-4e902c553eb9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 34%

---

# アップグレード後にアンインストールされる廃止されたバンドルの一覧{#list-of-obsolete-bundles-uninstalled-after-the-upgrade}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

>[!NOTE]
>
>コードでこれらのバンドルを利用している場合は、アドビサポートに連絡し、影響を受ける領域の互換性パッケージを要求してください。

AEM 6.3 にアップグレードすると、アップグレードされた AEM バージョンに応じて、以下のバンドルが自動的にアンインストールされます。

**AEM 6.1：**

* org.eclipse.equinox.region, version 1.1.0.v20120522-1841, Active
* org.apache.sling.installer.factory.subsystems, version 1.0.0, Active
* org.apache.aries.subsystem.core, version 1.2.0, Active
* org.apache.aries.subsystem.api, version 1.1.0, Active
* org.apache.felix.resolver, version 1.0.0, Active
* org.osgi.service.subsystem.region.context.0、バージョン 1.0.0、Active
* com.adobe.cq.cq-creativecloud-cloudims、バージョン 0.0.10、アクティブ
* com.adobe.cq.cq-creativecloud-commons、バージョン 0.0.8、アクティブ
* com.adobe.cq.cq-creativecloud-filesync, version 0.0.12，インストール済み
* com.adobe.cq.cq-creativecloud-storage, version 0.0.8，インストール済み
* biz.Qute.bndlib，バージョン1.43.0，アクティブ
* com.day.cq.dam.commons.nekohtml, version 0.9.5, Active
* com.day.cq.mcm.cq-mcm-silverpop-integration, version 1.2.2, Active

**AEM 6.0：**

* org.apache.sling.discovery.impl、バージョン 1.1.6、アクティブ
* com.adobe.granite.installer.patch, version 0.4.0, Active
* biz.Qute.bndlib，バージョン1.43.0，アクティブ
* com.day.cq.cq-jobs-core, version 5.4.0, Active
* com.day.cq.cq-opensocial, version 5.7.2, Active
* com.day.cq.cq-pinauthhandler, version 1.1.2, Active
* com.day.cq.dam.commons.nekohtml, version 0.9.5, Active
* com.day.cq.mcm.cq-mcm-silverpop-integration, version 1.1.6, Active
* com.day.cq.wcm.cq-wcm-mobile-phonegap-build-integration, version 5.7.18, Active

**CQ5.6.1：**

* biz.Qute.bndlib，バージョン1.43.0，アクティブ
* com.day.cq.cq-pinauthhandler, version 1.0.0, Active
* com.day.cq.dam.commons.nekohtml, version 0.9.5, Active
* com.day.crx.crxde-support, version 2.3.14, Installed
* com.day.cq.mcm.cq-mcm-silverpop-integration, version 1.0.2, Active

**CQ5.6.0：**

* com.day.cq.cq-pinauthhandler, version 1.0.0, Active
* com.day.cq.dam.commons.nekohtml, version 0.9.5, Active
* com.day.crx.crxde-support, version 2.3.14, Installed
