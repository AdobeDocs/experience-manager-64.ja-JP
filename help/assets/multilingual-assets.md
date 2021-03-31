---
title: 多言語のアセット
description: バイナリ、メタデータ、タグなどのアセットを複数の言語に翻訳するワークフローを自動化する方法を学習します。
contentOwner: AG
feature: アセット管理
role: Administrator
translation-type: tm+mt
source-git-commit: 4acf159ae1b9923a9c93fa15faa38c7f4bc9f759
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 84%

---


# 多言語のアセット {#multilingual-assets}

Adobe Experience Manager（AEM）Assets を使用して、アセット（バイナリ、メタデータ、タグを含む）に対する翻訳ワークフローを自動化し、多言語プロジェクトで使用するために他の言語のアセットを生成できます。

翻訳ワークフローを自動化するには、翻訳サービスプロバイダーと AEM とを統合して、アセットを複数の言語に翻訳するためのプロジェクトを作成します。AEM では人間による翻訳と機械翻訳のワークフローがサポートされます。

人間による翻訳：翻訳済みアセットが返され、AEM に読み込まれます。翻訳プロバイダーと AEM を連携すると、AEM と翻訳プロバイダーとの間でアセットが自動的に送信されます。

機械翻訳：機械翻訳サービスでは、アセットのメタデータとタグがすぐに翻訳されます。

アセットの翻訳には次の手順が含まれます。

1. [AEM と翻訳サービスプロバイダーの接続](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [翻訳統合フレームワーク設定の作成](/help/sites-administering/tc-tic.md)
1. [翻訳するアセットの準備](preparing-assets-for-translation.md)
1. [フォルダーへの翻訳クラウドサービスの適用](transition-cloud-services.md)
1. [翻訳プロジェクトの作成](translation-projects.md)

翻訳サービスプロバイダーがAEMと統合するコネクタを提供していない場合は、[代替プロセス](/help/sites-administering/tc-manage.md#exporting-a-translation-job)を使用します。

[コンテンツフラグメント用の翻訳プロジェクトの作成](creating-translation-projects-for-content-fragments.md)も参照してください。
