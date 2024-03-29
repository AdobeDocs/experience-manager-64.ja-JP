---
title: 大量の保護された情報の配布
seo-title: High-volume secure information delivery
description: Document Security は、大量実稼動環境のドキュメントに対してではなく、ユーザーに対するライセンスの関連付けをサポートします。
seo-description: Document security supports the association of licenses to users, rather than to the documents in mass production environments.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
feature: Document Security
exl-id: 78fc7c4a-a634-4628-927a-c9622bdc13fc
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 8%

---

# 大量の保護された情報の配布 {#high-volume-secure-information-delivery}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

通信会社の安全な月次請求書を生成するような大量生産環境では、各ドキュメントに固有のライセンスを作成すると、リソースを大量に消費する可能性があります。 このような場合、Document Security は、ドキュメントに対するライセンスの関連付けではなく、ユーザーに対するライセンスの関連付けをサポートします。 ユーザーに対して生成されたライセンスは、そのユーザーに対して保護されているすべてのドキュメントに対して使用されます。

このアプローチの利点の 1 つは、Document Security データベースのサイズが、ユーザー数ではなく、ドキュメント数に比例して大きくなることです。 また、1 人のユーザーに対して 1 回だけライセンスを作成する必要があるので、以降、これらのポリシーを使用してドキュメントを保護する方が速くなります。 オフラインアクセス、ドキュメントの有効期限、失効などの機能は、そのようなすべてのドキュメントでサポートされます。

Document Security は抽象ポリシーもサポートしています。 抽象ポリシーは、ドキュメントセキュリティ設定や使用権限などのすべてのポリシー属性を含むポリシーテンプレートですが、プリンシパルのリストは含まれていません。 管理者は、ドキュメントへのアクセス権を持つ別のプリンシパルを持つ抽象ポリシーから任意の数のポリシーを作成できます。 抽象ポリシーに対して行った変更は、抽象ポリシーから生成された実際のポリシーには影響しません。

通信会社の月次請求書生成の場合、要約ポリシーを作成し、ユーザーを作成して、各ユーザーに対して一意のライセンスを生成します。 ライセンスは、後で各ユーザーのドキュメントに適用されます。

抽象ポリシーの作成は、Document Security Java SDK を通じてのみサポートされます。 ただし、Document Security Web ページから抽象ポリシーから作成したポリシーを管理することはできます。 この方法を使用して作成されるポリシーは、動作が Document Security Web ページから作成されるポリシーと同じです。

詳しくは、「[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp)」を参照してください。
