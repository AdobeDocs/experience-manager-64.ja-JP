---
title: AEM
description: ' [!DNL Experience Manager] アセットのデプロイメントと、アセットの取り込みと処理に使用する機能に応じて、負荷時のシステムの安定性とパフォーマンスを向上させるベストプラクティスを特定し、順守します。'
contentOwner: AG
feature: Asset Management
role: Architect,Admin
exl-id: e2ab924b-53cb-4011-8c0a-9e8e59dd2f16
source-git-commit: de5632ff0ee87a4ded88e792b57e818baf4c01a3
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 14%

---

# [!DNL Experience Manager]アセットのベストプラクティス {#best-practices-for-assets}

Adobe Experience Manager Assetsは、コンテンツベロシティを通じてビジネス目標の達成に貢献する、高品質のデジタルマーケティングエクスペリエンスを提供する上で重要な役割を果たします。 [!DNL Assets]内で多数のアセットを扱う場合や、ビデオやダイナミックメディアを含む多数のアセットを定期的/定期的にアップロードする場合は、デジタルアセット管理エクスペリエンスの最適化がシステム効率の上に重要です。

組織に対する[!DNL Assets]の配置方法と、アセットの取り込み、レンディションの生成、メタデータの抽出に使用する機能に応じて、様々な領域でのベストプラクティスを識別して準拠することで、負荷時のシステムの安定性とパフォーマンスが大幅に向上します。

以下のガイドを確認した後、ニーズに合ったエンタープライズアセット管理システムを構築および管理するための知識とツールを入手できます。

* [アセットパフォーマン](performance-tuning-guidelines.md)
スチューニングガイド実稼動環境への移行後も含め、実装のあらゆる時点で実行できる、システムを最大限に活用するための一連のベストプラクティスが含まれています。
* [アセットのサ](assets-sizing-guide.md)
イジングガイドAssets実装の予測を描く際には、アセットのストレージ、CPU、メモリ、IO、ネットワークスループットの観点から十分なリソースが確保されていることを確認することが重要です。これらのアイテムのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。このガイドには、[!DNL Experience Manager] Assetsのデプロイに必要なインフラストラクチャとリソースの予測に効率的な指標を判断するのに役立つベストプラクティスとサイジングツールが含まれています。
* [アセット移行ガ](assets-migration-guide.md)
イド既存のシステムからアセットに移行する場合 [!DNL Experience Manager] は、移行プロセスを効率化するためにいくつかの手順を考慮する必要があります。移行ガイドには、アセットを[!DNL Experience Manager]に移行するタスクに関するベストプラクティスが含まれています。 これには、メタデータの適用、レンディションの生成、公開デプロイメントへのアセットのアクティベートが含まれます。
* [Assetsのネットワークに関す](assets-network-considerations.md)
る考慮事項デプロイメ [!DNL Experience Manager] ントを処理する場合、ネットワークのパフォーマンスを理解し、渋滞地点を特定し、期待されるユーザーエクスペリエンスを説明するには、ネットワークトポロジを理解することが重要です。Assetsのネットワークに関する考慮事項のドキュメントでは、[!DNL Experience Manager]アセットのデプロイメントを設計する際のネットワークに関する考慮事項について説明します。
* [アセット監視](assets-monitoring-best-practices.md)
ガイドデプロイメ [!DNL Experience Manager] ント後は、システムの整合性と運用の効率性を確保するために、特定のタスクとシステム全般を監視する必要があります。この監視ガイドには、システムの様々な側面を監視するためのベストプラクティスが記載されています。
* （非推奨） [Assetsオフロードガイド](assets-offloading-best-practices.md)
[!DNL Experience Manager] Assetsで大きなファイルや実行中のワークフローを処理すると、CPU、メモリ、I/Oリソースが大量に消費される可能性があります。 これらのタスクのオフロードは、CPU、メモリ、IOのオーバーヘッドを減らす可能性があります。 Assets オフロードガイドには、Assets オフロードの推奨される使用例およびベストプラクティスが記載されています。
* [[!DNL Experience Manager] デスクトップアプリのベストプラクティス](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app-best-practices.html)
   [!DNL Experience Manager] デスクトップアプリケーションは、デジタルアセット管理(DAM)ソリューションとデスクトップを連携させ、 [!DNL Experience Manager] web UIで使用可能なファイルをデスクトップで直接開けるようにします。[!DNL Experience Manager]デスクトップアプリケーションの使いやすいワークフローは、デスクトップのオペレーティングシステムから提供されるネットワーク共有テクノロジにより有効化されます。このガイドでは、[!DNL Experience Manager]デスクトップアプリケーションの主な機能と推奨される使用例を説明します。
* [[!DNL Experience Manager] Creative Cloud統合のベストプ](aem-cc-integration-best-practices.md)
ラクティスデプロイメントと [!DNL Experience Manager] Creative Cloudは、複数の方法で統合できます。ベストプラクティスに従って統合ワークフローおよびアセット転送ワークフローを効率化すると、効率を最大化することができます。このガイドには、[!DNL Experience Manager] AssetsとAdobe Creative Cloudの統合に関するベストプラクティスが含まれています。
* （非推奨） [[!DNL Experience Manager] Creative Cloudフォルダー共有のベストプラクティス](aem-cc-folder-sharing-best-practices.md)
[!DNL Experience Manager]を設定して、DAMのユーザーがCreative Cloud(CC)ユーザーとフォルダーを共有できるようにすることで、Creative Cloudアセットサービスで共有フォルダーとして使用できます。 この機能を使用すると、クリエイティブチームと DAM ユーザーの間でファイルを交換することができます。このガイドでは、[!DNL Experience Manager]をフォルダー共有機能に活用するためのベストプラクティスをCreative Cloudします。
