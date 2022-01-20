---
title: AEM 6.4 Forms へのアップグレード
seo-title: Upgrade to AEM 6.4 Forms
description: 'AEM 6.1 Forms、AEM 6.2 Forms、LiveCycle ES4 SP1 を、AEM 6.3 Forms に直接アップグレードすることができます。 '
seo-description: You can perform a direct upgrade from AEM 6.1 Forms, AEM 6.2 Forms, and LiveCycle ES4 SP1 to AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: c613b54b-8768-46ef-a6f5-15bcc1642a75
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 100%

---

# AEM 6.4 Forms へのアップグレード{#upgrade-to-aem-forms}

AEM 6.4 Forms には、いくつかの新機能と機能強化が導入されています。これにより、フォームと通信の作成、管理、ユーザーエクスペリエンスが簡素化されます。AEM 6.4 Forms のすべての新機能と機能強化については、[新機能の概要についてのドキュメント](/help/forms/using/whats-new.md)を参照してください。

既存の LiveCycle または AEM Forms のインストール環境をアップグレードすると、AEM 6.4 Forms に導入された新機能と機能強化を使用できるようになります。既存のデータ、プロセス、アセットはそのまま保存されます。また、プロセスのメタデータと状態についても、そのまま保存されます。アップグレードを行うためのアップグレードパスは、選択することができます。

以下の図は、OSGi 上の AEM Forms の有効なアップグレードパスを示しています。

![](do-not-localize/osgi-upgrade.png)

以下の場合は、直接アップグレードすることができます。

* OSGi 上の AEM 6.2 Forms
* OSGi 上の AEM 6.3 Forms

以下の場合は、マルチホップアップグレードを実行することができます。

* OSGi 上の AEM 6.0 Forms
* OSGi 上の AEM 6.1 Forms

以下の図は、JEE 上の AEM Forms の有効なアップグレードパスを示しています。

![](do-not-localize/jee-upgrade-6-4.png)

以下の場合は、直接アップグレードすることができます。

* LiveCycle ES3
* LiveCycle ES4 SP1
* JEE 上の AEM 6.2 Forms
* JEE 上の AEM 6.3 Forms

以下の場合は、マルチホップアップグレードを実行することができます。

* LiveCycle ES2
* JEE 上の AEM 6.0 Forms
* JEE 上の AEM 6.1 Forms
