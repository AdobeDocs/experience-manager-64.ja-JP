---
title: Adobe Sign との統合| ユーザーデータの処理
seo-title: Integration with Adobe Sign | Handling user data
description: AEM Forms を Adobe Sign と統合すると、アダプティブフォームで電子署名ワークフローが有効になり、法務、販売、給与、人事管理のワークフローのフォームまたは契約書を処理することができます。ユーザーデータ、データストア、ユーザーデータへのアクセスと削除について詳しく説明します。
seo-description: AEM Forms integrates with Adobe Sign to enable e-signature workflows in adaptive forms to process forms or agreements for legal, sales, payroll, human resource management workflows. Dig deeper on user data, data stores, and access and delete user data.
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Adobe Sign
role: Admin
exl-id: c2061de7-8627-4595-b96c-aa2d6abffddd
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 86%

---

# Adobe Sign との統合| ユーザーデータの処理 {#integration-with-adobe-sign-handling-user-data}

AEM Forms を Adobe Sign と統合すると、アダプティブフォームで電子署名ワークフローが有効になり、法務、販売、給与、人事管理のワークフローのフォームまたは契約書を処理することができます。これにより、1 人のユーザーおよび複数ユーザーの署名、連続署名および並列署名のワークフロー、匿名ユーザーまたはログインしたユーザーでの署名フォームなど、様々なユーザー認証方法が可能になります。

1 人の署名者または複数の署名者がアダプティブフォームに署名をして送信するときに、署名者に関する情報を含む Adobe Sign の契約書が生成されます。

AEM FormsとAdobe Signの統合について詳しくは、 [アダプティブフォームでのAdobe Signの使用](/help/forms/using/working-with-adobe-sign.md).

## ユーザーデータとデータストア {#data}

Adobe Sign 対応のアダプティブフォームには署名者に関する情報が含まれています。これにはアダプティブフォームで収集された他のユーザーのデータが含まれている場合があります。Adobe Sign サービスは、契約書内の署名を使用してユーザーデータを格納します。この契約書は、AEM Forms のクラウドサービスに設定された Adobe Sign サーバーに保存されます。さらに、Forms Portal の送信アクションを使用するようにアダプティブフォームが構成されている場合、契約書のデータはフォームデータとともに Forms Portal のデータストアに格納されます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

ユーザーデータは契約書内で収集されますが、いずれのサービステーブルにも保存されません。Adobe Sign を使用すると、管理者はサービスで管理する管理データを自身で選択できます。Adobe Sign サービスのプライバシー管理者は、依頼者の電子メールアドレスに基づいて契約書のリストの作成または削除を行うことができます。

Adobe Sign は、参加者による契約書の検索、および必要に応じて契約書の削除を実行できる Web アプリケーションを提供しています。詳しくは、 [Adobe Sign — 機能：ユーザー情報の削除](https://helpx.adobe.com/sign/help/adobesign_gdpr_user_deletion.html).

Forms Portal の送信アクションを使用するように構成されているアダプティブフォームの契約書データも、Forms Portal のデータストアに格納されます。Forms Portal のデータストアにアクセスしてデータを削除する方法については、「[Forms Portal | ユーザーデータの処理](/help/forms/using/forms-portal-handling-user-data.md)」を参照してください。
