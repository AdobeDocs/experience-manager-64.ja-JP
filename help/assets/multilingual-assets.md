---
title: 多言語のアセット
description: バイナリ、メタデータ、タグなどのアセットを複数の言語に翻訳するワークフローを自動化する方法を学習します。
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: 8e065137-3599-48af-a040-6923b7b5e1d9
source-git-commit: 937c9425e276f67486fba1d4563799fe68d35cc7
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 60%

---

# 多言語のアセット {#multilingual-assets}

Adobe Experience Manager（AEM）Assets を使用して、アセット（バイナリ、メタデータ、タグを含む）に対する翻訳ワークフローを自動化し、多言語プロジェクトで使用するために他の言語のアセットを生成できます。

翻訳ワークフローを自動化するには、翻訳サービスプロバイダーを[!DNL Experience Manager]と統合し、アセットを複数の言語に翻訳するためのプロジェクトを作成します。 [!DNL Experience Manager] では人間による翻訳と機械翻訳のワークフローがサポートされます。

人間による翻訳：翻訳済みアセットが返され、AEM に読み込まれます。翻訳プロバイダーがAEMと統合されると、[!DNL Experience Manager]と翻訳プロバイダーの間でアセットが自動的に送信されます。

機械翻訳：機械翻訳サービスでは、アセットのメタデータとタグがすぐに翻訳されます。

アセットの翻訳には次の手順が含まれます。

1. [ [!DNL Experience Manager] と翻訳サービスプロバイダーの接続](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [翻訳統合フレームワーク設定の作成](/help/sites-administering/tc-tic.md)
1. [翻訳するアセットの準備](preparing-assets-for-translation.md)
1. [フォルダーへの翻訳クラウドサービスの適用](transition-cloud-services.md)
1. [翻訳プロジェクトの作成](translation-projects.md)

翻訳サービスプロバイダーがAEMと統合するコネクタを提供しない場合は、[代替プロセス](/help/sites-administering/tc-manage.md#exporting-a-translation-job)を使用します。

[コンテンツフラグメントの翻訳プロジェクトの作成](creating-translation-projects-for-content-fragments.md)も参照してください。
