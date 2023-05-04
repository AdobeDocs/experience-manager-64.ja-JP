---
title: 多言語アセット
description: バイナリ、メタデータ、タグなどのアセットを複数の言語に翻訳するワークフローを自動化する方法を学習します。
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: 8e065137-3599-48af-a040-6923b7b5e1d9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 45%

---

# 多言語アセット {#multilingual-assets}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Adobe Experience Manager（AEM）Assets を使用して、アセット（バイナリ、メタデータ、タグを含む）に対する翻訳ワークフローを自動化し、多言語プロジェクトで使用するために他の言語のアセットを生成できます。

翻訳ワークフローを自動化するには、翻訳サービスプロバイダーと [!DNL Experience Manager] とを統合して、アセットを複数の言語に翻訳するためのプロジェクトを作成してください。[!DNL Experience Manager] では人間による翻訳と機械翻訳のワークフローがサポートされます。

人間による翻訳：翻訳されたアセットが返され、AEMに読み込まれます。 翻訳プロバイダーがAEMと統合されると、アセットは [!DNL Experience Manager] 翻訳プロバイダー

機械翻訳：機械翻訳サービスでは、アセットのメタデータとタグがすぐに翻訳されます。

アセットの翻訳には、以下が含まれます。

1. [接続中 [!DNL Experience Manager] 翻訳サービスプロバイダーと共に使用](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [翻訳統合フレームワーク設定の作成](/help/sites-administering/tc-tic.md)
1. [翻訳するアセットの準備](preparing-assets-for-translation.md)
1. [フォルダーへの翻訳クラウドサービスの適用](transition-cloud-services.md)
1. [翻訳プロジェクトの作成](translation-projects.md)

翻訳サービスプロバイダーがAEMと統合するコネクタを提供しない場合は、 [代替手法](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

また、 [コンテンツフラグメントの翻訳プロジェクトの作成](creating-translation-projects-for-content-fragments.md).
