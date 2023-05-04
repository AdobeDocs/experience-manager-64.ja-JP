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
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 48%

---

# AEM 6.4 における Forms リポジトリの再構築{#forms-repository-restructuring-in-aem}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

[AEM 6.4 におけるリポジトリの再構築](/help/sites-deploying/repository-restructuring.md)の親ページで説明しているように、AEM 6.4 にアップグレードする場合は、このページを参考に、AEM Forms ソリューションに影響を及ぼすリポジトリ変更に伴う作業量を評価する必要があります。一部の変更ではAEM 6.4 のアップグレードプロセス中に作業が必要ですが、6.5 のアップグレードまで延期することもできます。

**6.4 へのアップグレード時におこなう変更**

* [その他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md#misc)

**6.5 へのアップグレード前**

* [EchoSign クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md#echosign-cloud-service-configuration)
* [reCAPTCHA クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md#recaptcha-cloud-service-configurations)
* [Typekit クラウドサービス設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md#typekit-cloud-service-configurations)
* [その他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-4.md#misc)

## 6.4 へのアップグレード時におこなう変更 {#with-upgrade}

### その他 {#misc}

| **以前の場所** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新しい場所** | `/libs/fd/fp/components` |
| **再構築の手引き** | カスタムコード内で従来の場所を明示的に参照している場合は、新しい場所に更新する必要があります。 |
| **備考** | これらのクライアントライブラリは、変更または拡張しないでください。 |

| **以前の場所** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新しい場所** | `/libs/fd/rte` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/authoring/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新しい場所** | `/libs/fd/xfaforms/clientlibs/` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/runtime/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/af` |
|---|---|
| **新しい場所** | `/libs/fd/af/runtime/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新しい場所** | `/libs/fd/expeditor/clientlibs` |
| **再構築の手引き** | クライアントライブラリ内のリソースを絶対パスで参照できる場合、新しいアセットで新しいパスを使用する必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新しい場所** | `/libs/fd/fmaddon` |
| **再構築の手引き** | これらの clientlib の変更は、推奨もサポートもされていませんでした。 これらの clientlib に変更が加えられた場合、AEM提供のコードを使用するには、それらをロールバックする必要があります。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/aep` |
|---|---|
| **新しい場所** | `/var/fd/content/annotations` |
| **再構築の手引き** | これらの clientlib の変更は、推奨もサポートもされていませんでした。 これらの clientlib に変更が加えられた場合、AEM提供のコードを使用するには、それらをロールバックする必要があります。 |
| **備考** | 該当なし |

## 6.5 へのアップグレード前 {#prior-to-upgrade}

### EchoSign クラウドサービス設定 {#echosign-cloud-service-configuration}

| **以前の場所** | `/etc/cloudservices/echosign` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **再構築の手引き** | この [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md) Forms移行 UI からトリガーされるユーティリティ。 |
| **備考** | 該当なし |

### reCAPTCHA クラウドサービス設定 {#recaptcha-cloud-service-configurations}

| **以前の場所** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **再構築の手引き** | この [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md) Forms移行 UI からトリガーされるユーティリティ。 |
| **備考** | 該当なし |

### Typekit クラウドサービス設定 {#typekit-cloud-service-configurations}

| **以前の場所** | `/etc/cloudservices/typekit` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **再構築の手引き** | この [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md) Forms移行 UI からトリガーされるユーティリティ。 |
| **備考** | 該当なし |

### その他 {#misc-1}

| **以前の場所** | `/etc/cloudservices/fdm` |
|---|---|
| **新しい場所** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **再構築の手引き** | この [遅延コンテンツ移行](/help/sites-deploying/lazy-content-migration.md) Forms移行 UI からトリガーされるユーティリティ。 |
| **備考** | 該当なし |

| **以前の場所** | `/etc/designs/fd/fp` |
|---|---|
| **新しい場所** | `/libs/fd/fp` |
| **再構築の手引き** | /etc 内のテンプレートへの参照は、最終的には、それらに対応する `/libs` 内のテンプレートを指すように更新してください。 |
| **備考** | 該当なし |
