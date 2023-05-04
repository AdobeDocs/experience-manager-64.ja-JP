---
title: Acrobat Signとの統合 |ユーザーデータの処理
seo-title: Integration with Acrobat Sign | Handling user data
description: AEM FormsはAcrobat Signと統合され、アダプティブフォームの電子署名ワークフローを有効にして、法務、販売、給与、人事管理の各ワークフローに関するフォームや契約を処理できます。 ユーザーデータ、データストア、ユーザーデータへのアクセスと削除について詳しく説明します。
seo-description: AEM Forms integrates with Acrobat Sign to enable e-signature workflows in adaptive forms to process forms or agreements for legal, sales, payroll, human resource management workflows. Dig deeper on user data, data stores, and access and delete user data.
uuid: cb3a455d-2e33-44c8-8f71-3a7ecd939cd8
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: e9e0d8fb-955e-4021-9e9a-9c95c6ffe88d
feature: Acrobat Sign
role: Admin
exl-id: c2061de7-8627-4595-b96c-aa2d6abffddd
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 11%

---

# Acrobat Signとの統合 |ユーザーデータの処理 {#integration-with-adobe-sign-handling-user-data}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEM FormsはAcrobat Signと統合され、アダプティブフォームの電子署名ワークフローを有効にして、法務、販売、給与、人事管理の各ワークフローに関するフォームや契約を処理できます。 これにより、1 人のユーザーおよび複数ユーザーの署名、連続署名および並列署名のワークフロー、匿名ユーザーまたはログインしたユーザーでの署名フォームなど、様々なユーザー認証方法が可能になります。

署名者または複数の署名者がアダプティブフォームに署名して送信すると、その署名者に関する情報を含むAcrobat Sign契約が生成されます。

AEM FormsとAcrobat Signの統合について詳しくは、 [アダプティブフォームでのAcrobat Signの使用](/help/forms/using/working-with-adobe-sign.md).

## ユーザーデータとデータストア {#data}

Acrobat Sign対応のアダプティブフォームには署名者に関する情報が含まれており、アダプティブフォームによって収集された他のユーザーデータも含まれている場合があります。 Acrobat Signサービスは、契約内の署名を使用してユーザーデータを保存します。 契約は、AEM Forms Cloud Services で設定されたAcrobat Signサーバーに保存されます。 さらに、Formsポータルの送信アクションを使用するようにアダプティブフォームが設定されている場合、契約書データはフォームデータと共にフォームポータルのデータストアに保存されます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

ユーザーデータは契約内で収集されますが、どのサービステーブルにも保存されません。 Acrobat Signを使用すると、管理者は、サービスで管理するデータの管理に関して、独自の選択肢を作成できます。 Acrobat Signサービスのプライバシー管理者は、要求者の電子メールアドレスに基づいて契約のリストを作成したり、契約を削除したりできます。

Acrobat Signは、参加者による契約の検索、および必要に応じて削除を可能にする Web アプリケーションを提供します。 詳しくは、 [Acrobat Sign — 機能：ユーザー情報の削除](https://helpx.adobe.com/jp/sign/help/adobesign_gdpr_user_deletion.html).

Formsポータル送信アクションを使用するように設定されたアダプティブフォームの契約データも、フォームポータルデータストアに保存されます。 フォームポータルのデータストアにアクセスしてデータを削除するには、 [Forms portal |ユーザーデータの処理](/help/forms/using/forms-portal-handling-user-data.md).
