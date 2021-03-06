---
title: AEM 6.4 における Forms リポジトリの再構築
seo-title: Forms Repository Restructuring in AEM 6.4
description: AEM 6.4 for Forms の新しいリポジトリ構造に移行するために必要な変更を加える方法について説明します。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.4 for Forms.
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
feature: Upgrading
exl-id: a2d6524e-3f5b-4d1e-af64-61ff95889657
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 87%

---

# AEM 6.4 における Forms リポジトリの再構築{#forms-repository-restructuring-in-aem}

親の説明に従って [AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md) このページでは、AEM 6.4 にアップグレードするお客様は、このページを使用して、AEM Formsソリューションに影響を与えるリポジトリの変更に関連する作業量を評価する必要があります。 一部の変更は AEM 6.4 アップグレードプロセス中に作業が必要ですが、それ以外は 6.5 アップグレードまで延期できます。

**6.4 へのアップグレード時におこなう変更**

* [その他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md#misc)

**6.5 へのアップグレードまでにおこなう変更**

* [EchoSign クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md#echosign-cloud-service-configuration)
* [reCAPTCHA クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md#recaptcha-cloud-service-configurations)
* [Typekit クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md#typekit-cloud-service-configurations)
* [その他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md#misc)

## 6.4 へのアップグレード時におこなう変更 {#with-upgrade}

### その他 {#misc}

| **以前の場所** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新しい場所** | `/libs/fd/fp/components` |
| **再構築の手引き** | カスタムコード内で従来の場所への明示的な参照は、新しい場所に更新する必要があります。 |
| **備考** | これらのクライアントライブラリは、変更したり拡張したりしないでください。 |

| **以前の場所** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新しい場所** | `/libs/fd/rte` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/authoring/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新しい場所** | `/libs/fd/xfaforms/clientlibs/` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/runtime/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/runtime/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新しい場所** | `/libs/fd/expeditor/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットでは新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新しい場所** | `/libs/fd/fmaddon` |
| **再構築の手引き** | これらのクライアントライブラリを変更することは推奨されず、サポートもされていません。変更された場合は、AEM 提供のコードを使用するようにクライアントライブラリをロールバックしてください。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/aep` |
|---|---|
| **新しい場所** | `/var/fd/content/annotations` |
| **再構築の手引き** | これらのクライアントライブラリを変更することは推奨されず、サポートもされていません。変更された場合は、AEM 提供のコードを使用するようにクライアントライブラリをロールバックしてください。 |
| **備考** | 該当なし |

## 6.5 へのアップグレードまでにおこなう変更 {#prior-to-upgrade}

### EchoSign クラウドサービス設定 {#echosign-cloud-service-configuration}

| **以前の場所** | `/etc/cloudservices/echosign` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **再構築の手引き** | [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md)ユーティリティを Forms 移行 UI からトリガーします。 |
| **備考** | 該当なし |

### reCAPTCHA クラウドサービス設定 {#recaptcha-cloud-service-configurations}

| **以前の場所** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **再構築の手引き** | [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md)ユーティリティを Forms 移行 UI からトリガーします。 |
| **備考** | 該当なし |

### Typekit クラウドサービス設定 {#typekit-cloud-service-configurations}

| **以前の場所** | `/etc/cloudservices/typekit` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **再構築の手引き** | [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md)ユーティリティを Forms 移行 UI からトリガーします。 |
| **備考** | 該当なし |

### その他 {#misc-1}

| **以前の場所** | `/etc/cloudservices/fdm` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **再構築の手引き** | [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md)ユーティリティを Forms 移行 UI からトリガーします。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/designs/fd/fp` |
|---|---|
| **新しい場所** | `/libs/fd/fp` |
| **再構築の手引き** | /etc テンプレートへの参照は、最終的に、それらのテンプレートを指すように更新されます。 `/libs` 対応する |
| **備考** | 該当なし |
