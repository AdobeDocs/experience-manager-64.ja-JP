---
title: AEM
description: ' [!DNL Experience Manager]  アセットのデプロイメントと、アセットの取り込みと処理に使用する機能に応じて、負荷時のシステムの安定性とパフォーマンスを高めるベストプラクティスを特定し、順守します。'
contentOwner: AG
feature: Asset Management
role: Architect,Admin
exl-id: e2ab924b-53cb-4011-8c0a-9e8e59dd2f16
source-git-commit: d750c852b6367d753d18be57c8910bf5671fd5e8
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 14%

---

# [!DNL Experience Manager] Assets のベストプラクティス {#best-practices-for-assets}

Adobe Experience Manager Assets は、コンテンツベロシティを通じてビジネス目標の達成に貢献する、高品質のデジタルマーケティングエクスペリエンスを提供する上で重要な役割を果たします。 [!DNL Assets] 内で大量のアセットを扱う場合、またはビデオや Dynamic Media を含む多数のアセットを定期的/定期的にアップロードする場合、システムの効率を高めるには、デジタルアセット管理エクスペリエンスの最適化が重要です。

組織に対する [!DNL Assets] の配置方法と、アセットの取り込み、レンディションの生成、メタデータの抽出に使用する機能に応じて、様々な領域でのベストプラクティスを識別して準拠することで、負荷時のシステムの安定性とパフォーマンスが大幅に向上します。

次のガイドを確認した後、ニーズに合ったエンタープライズアセット管理システムを構築し、管理するための知識とツールを入手できます。

* [アセットのパフォーマンス調整ガイド実稼動環境への移行後も、実装のあらゆる時点で実行できる一連のベストプラクティスが含まれており、システムを最大限に活用することができます。](performance-tuning-guidelines.md)

* [アセットのサ](assets-sizing-guide.md)
イジングガイド Assets 実装の予測を描く際には、アセットのストレージ、CPU、メモリ、IO、およびネットワークスループットの観点から十分なリソースを確保することが重要です。これらのアイテムのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。このガイドには、[!DNL Experience Manager] Assets のデプロイに必要なインフラストラクチャとリソースの見積もりに効率的な指標を判断するのに役立つベストプラクティスとサイジングツールが含まれています。
* [アセット移行ガ](assets-migration-guide.md)
イドレガシーシステムからアセットにアセットを移行する場合 [!DNL Experience Manager] は、移行プロセスを効率化するためにいくつかの手順を考慮する必要があります。移行ガイドには、アセットを [!DNL Experience Manager] に移行するタスクに関するベストプラクティスが含まれています。 これには、メタデータの適用、レンディションの生成、公開デプロイメントへのアセットのアクティベートが含まれます。
* [Assets のネットワークに関す](assets-network-considerations.md)
る考慮事項デプロイメン [!DNL Experience Manager] トを処理する場合、ネットワークのパフォーマンスを理解し、渋滞地点を特定し、期待されるユーザーエクスペリエンスを説明するために、ネットワークトポロジを理解することが重要です。Assets のネットワークに関する考慮事項ドキュメントでは、[!DNL Experience Manager] アセットのデプロイメントを設計する際のネットワークに関する考慮事項について説明します。
* [アセット監視ガ](assets-monitoring-best-practices.md)
イドデプロイメン [!DNL Experience Manager] ト後は、システムの整合性と運用の効率を確保するために、特定のタスクとシステム全般を監視する必要があります。この監視ガイドには、システムの様々な側面を監視するためのベストプラクティスが記載されています。
* （非推奨） [Assets オフロードガイド ](assets-offloading-best-practices.md)
[!DNL Experience Manager] Assets で大きなファイルや実行中のワークフローを処理すると、CPU、メモリ、I/O リソースを大量に消費する可能性があります。 これらのタスクのオフロードは、CPU、メモリ、IO のオーバーヘッドを減らす可能性があります。 Assets オフロードガイドには、Assets オフロードの推奨される使用例およびベストプラクティスが記載されています。
* [[!DNL Experience Manager] デスクトップアプリケーションのベストプラクティス](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app-best-practices.html)
   [!DNL Experience Manager] デスクトップアプリケーションは、デジタルアセット管理 (DAM) ソリューションとデスクトップを連携させ、 [!DNL Experience Manager] web UI で使用可能なファイルをデスクトップで直接開くことができます。[!DNL Experience Manager]デスクトップアプリケーションの使いやすいワークフローは、デスクトップのオペレーティングシステムから提供されるネットワーク共有テクノロジにより有効化されます。このガイドでは、主な機能と推奨される [!DNL Experience Manager] デスクトップアプリケーションの使用例を説明します。
* [[!DNL Experience Manager] およびCreative Cloud統合のベス](aem-cc-integration-best-practices.md)
トプラクティスデプロイメントと [!DNL Experience Manager] Creative Cloudは、複数の方法で統合できます。ベストプラクティスに従って統合ワークフローおよびアセット転送ワークフローを効率化すると、効率を最大化することができます。このガイドには、[!DNL Experience Manager] Assets とAdobe Creative Cloudの統合に関するベストプラクティスが記載されています。
* （非推奨） [[!DNL Experience Manager]  フォルダー共有のベストプラクティスをCreative Cloud](aem-cc-folder-sharing-best-practices.md)
[!DNL Experience Manager] を設定して、DAM のユーザーがCreative Cloudーユーザーとフォルダーを共有できるようにし、Creative Cloudーアセットサービスで共有フォルダーとして使用できるようにすることができます。 この機能を使用すると、クリエイティブチームと DAM ユーザーの間でファイルを交換することができます。このガイドでは、[!DNL Experience Manager] をフォルダー共有機能に活用するベストプラクティスをCreative Cloudに説明します。
