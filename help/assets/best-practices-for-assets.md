---
title: AEMを使用してアセットを管理するためのベストプラクティス
description: 負荷時のシステムの安定性とパフォーマンスを向上させるベストプラクティスを特定し、それに従う。 [!DNL Experience Manager] アセットの取り込みと処理に使用される Assets のデプロイメントと機能。
contentOwner: AG
feature: Asset Management
role: Architect,Admin
exl-id: e2ab924b-53cb-4011-8c0a-9e8e59dd2f16
source-git-commit: d750c852b6367d753d18be57c8910bf5671fd5e8
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 19%

---

# のベストプラクティス [!DNL Experience Manager] Assets {#best-practices-for-assets}

Adobe Experience Manager Assets は、コンテンツベロシティを通じてビジネス目標の達成に貢献する、高品質のデジタルマーケティングエクスペリエンスを実現する上で重要な役割を果たします。 内で多数のアセットを操作する場合 [!DNL Assets] また、ビデオや dynamic media を含む多数のアセットを定期的/定期的にアップロードし、デジタルアセット管理エクスペリエンスを最適化することが、システムの効率性のために重要です。

位置に応じて [!DNL Assets] アセットの取り込み、レンディションの生成、メタデータの取り込みに使用する組織や機能に応じて、様々な領域でのベストプラクティスを識別して準拠することで、負荷時のシステムの安定性とパフォーマンスを大幅に高めます。

以下のガイドを確認した後、ニーズに合ったエンタープライズアセット管理システムを構築および管理するための知識とツールを入手できます。

* [Assets パフォーマンスチューニングガイド](performance-tuning-guidelines.md)
実稼動環境に移行した後でも、実装内の任意の時点で実行できる一連のベストプラクティスを含め、システムを最大限に活用することができます。
* [Assets サイズ設定ガイド](assets-sizing-guide.md)
Assets 実装の予測を描く場合は、アセットのストレージ、CPU、メモリ、IO、ネットワークスループットに関して十分なリソースが確保されていることを確認することが重要です。 これらのアイテムのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。このガイドには、導入に必要なインフラストラクチャとリソースの見積もりに効率的な指標を決定するのに役立つベストプラクティスが含まれています [!DNL Experience Manager] アセットとサイズ調整ツール。
* [アセット移行ガイド](assets-migration-guide.md)
既存のシステムからにアセットを移行する場合 [!DNL Experience Manager] Assets では、移行プロセスを合理化するためにいくつかの手順を検討する必要があります。 この移行ガイドには、アセットを [!DNL Experience Manager] に段階的に移行するタスクのベストプラクティスが記載されています。これには、メタデータの適用、レンディションの生成、公開へのアセットのアクティベートが含まれます。
* [Assets のネットワークに関する考慮事項](assets-network-considerations.md)
処理時 [!DNL Experience Manager] デプロイメント、ネットワークトポロジの理解は、ネットワークのパフォーマンスを理解し、渋滞地点を特定し、期待されるユーザーエクスペリエンスを説明するうえで重要です。 Assets ネットワークに関する考慮事項ドキュメントでは、 [!DNL Experience Manager] アセットのデプロイメント。
* [Assets 監視ガイド](assets-monitoring-best-practices.md)
次に [!DNL Experience Manager] デプロイメントを実行する場合は、システムの整合性と運用の効率性を確保するために、特定のタスクとシステム全般を監視する必要があります。 この監視ガイドには、システムの様々な側面を監視するためのベストプラクティスが記載されています。
* （廃止） [Assets オフロードガイド](assets-offloading-best-practices.md)
での大きなファイルの処理と実行中のワークフローの処理 [!DNL Experience Manager] アセットは、CPU、メモリ、I/O リソースを大量に消費する可能性があります。 これらのタスクをオフロードすると、CPU、メモリ、および IO のオーバーヘッドを削減できます。 Assets オフロードガイドには、Assets オフロードの推奨される使用例およびベストプラクティスが記載されています。
* [[!DNL Experience Manager] デスクトップアプリケーションのベストプラクティス](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app-best-practices.html)
   [!DNL Experience Manager] デスクトップアプリケーションは、デジタルアセット管理 (DAM) ソリューションとデスクトップをつなぎ、 [!DNL Experience Manager] Web UI をデスクトップに直接配置できます。 [!DNL Experience Manager]デスクトップアプリケーションの使いやすいワークフローは、デスクトップのオペレーティングシステムから提供されるネットワーク共有テクノロジにより有効化されます。このガイドには、[!DNL Experience Manager] デスクトップアプリケーションの主要な機能と推奨される使用例が記載されています。
* [[!DNL Experience Manager] とCreative Cloud統合のベストプラクティス](aem-cc-integration-best-practices.md)
以下を [!DNL Experience Manager] Creative Cloudを使用したデプロイメントを複数の方法で実行できます。 ベストプラクティスに従って統合ワークフローおよびアセット転送ワークフローを効率化すると、効率を最大化することができます。このガイドには、の統合に関するベストプラクティスが含まれています [!DNL Experience Manager] Adobe Creative Cloudの Assets
* （廃止） [[!DNL Experience Manager] Creative Cloudフォルダー共有のベストプラクティス](aem-cc-folder-sharing-best-practices.md)
次の項目を設定できます。 [!DNL Experience Manager] DAM のユーザーがCreative Cloudーをフォルダーユーザーと共有できるようにして、フォルダーをCreative Cloudアセットサービスで共有フォルダーとして使用できるようにする。 この機能を使用すると、クリエイティブチームと DAM ユーザーの間でファイルを交換することができます。このガイドでは、 [!DNL Experience Manager] をCreative Cloudフォルダー共有機能に追加しました。
