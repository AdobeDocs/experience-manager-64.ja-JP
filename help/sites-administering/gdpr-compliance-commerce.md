---
title: AEM Commerce - GDPR 対応
seo-title: AEM Commerce - GDPR Readiness
description: '"AEM Commerce - GDPR 対応"'
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
feature: Commerce Integration Framework
exl-id: c5002812-cbc6-4b3e-85be-3446630b4e8a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 69%

---

# AEM Commerce - GDPR 対応{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>以下の節では GDPR を例として使用していますが、詳細はすべてのデータ保護およびプライバシー規制に適用できます。（GDPR、CCPA など）

データのプライバシー権に関する EU 一般データ保護規則（GDPR）が 2018 年 5 月に発効します。詳しくは、[アドビプライバシーセンターの GDPR ページ](https://www.adobe.com/jp/privacy/general-data-protection-regulation.html)を参照してください。

>[!NOTE]
>
>詳しくは、[AEM の GDPR 対応](/help/managing/data-protection-and-privacy.md)を参照してください。

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

デフォルトのコマース統合では AEM がエクスペリエンスレイヤーとなり、サービスを利用して得られたデータをヘッドレスモードで動作する顧客のコマースプラットフォームに送り返します。

一部のコマースプラットフォームでは、プロファイル情報 ( `/home/users`) およびコマーストークン（コマースプラットフォームにログインするため）をAEMで使用します。 これらのユースケースについては、[AEM プラットフォームでの GDPR 要求の処理](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)をお読みください。

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## AEM Commerce での GDPR 要求の処理 {#handling-gdpr-requests-for-aem-commerce}

Salesforces Commerce Cloud 統合の場合、AEM Commerce には GDPR 関連の情報は一切格納されません。[Salesforce Cloud](https://documentation.demandware.com/) に要求を転送してください。

hybris とIBM WebSphere の統合の場合、AEMにデータが一部存在します。 [AEM プラットフォームの GDPR 手順](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md)に従い、以下の質問について考察してください。

1. **データはどこに格納され、使用されているか？** キャッシュされたユーザープロファイル情報（名前、コマースユーザー識別子、トークン、パスワード、アドレスデータなど）がAEMから表示されます。
1. **対象となる GDPR データを誰と共有するか？** AEM Commerce 内の GDPR 関連データの更新は一切格納されず（前述の関連プロファイル情報は除く）、すべて管理元のコマースプラットフォームへと送り返されます。
1. **ユーザーデータの削除方法は？**  AEM でユーザープロファイルを削除し、コマースプラットフォームでユーザーの削除を呼び出してください。

>[!NOTE]
>
>[hybris の wiki](https://wiki.hybris.com/) または [Websphere Commerce のドキュメント](https://www-01.ibm.com/support/docview.wss?uid=swg27036450)を必要に応じて参照してください。
