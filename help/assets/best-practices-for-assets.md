---
title: AEMを使用してアセットを管理するためのベストプラクティス
description: AEM Assetsのデプロイメントと、アセットの取り込みと処理に使用する機能に応じて、読み込み中のシステムの安定性とパフォーマンスを向上させるベストプラクティスを特定し、それに従います。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0e0e2aa693c30c8e1ef1033b936b82d83e5b348e

---


# Best practices for AEM Assets {#best-practices-for-assets}

Adobe Experience Manager（AEM）Assets は、コンテンツベロシティを通じてビジネス目標の達成に貢献する、高品質のデジタルマーケティングエクスペリエンスを実現する上できわめて重要な役割を果たします。AEM Assets でビデオや Dynamic Media などの多数のアセットを操作する、または定期的に大量のアセットをアップロードする場合、システムの効率化を実現する上でデジタルアセットの管理エクスペリエンスの最適化は重要な位置を占めます。

組織における AEM Assets のデプロイ方法や、アセットの取り込み、レンディションの生成およびメタデータの抽出に使用した機能に応じて、様々な領域でベストプラクティスを特定して順守することで、システムの安定性と高負荷下のパフォーマンスを大幅に改善できます。

以下のガイドを見ると、ニーズに合ったエンタープライズアセット管理システムを構築し管理するための知識とツールが得られます。

* [アセットパフォーマンス](performance-tuning-guidelines.md)調整ガイド導入の任意の時点で実行できるベストプラクティスのセットが含まれており、運用開始後でも、システムを最大限に活用できます。
* [アセットサイズガイ](assets-sizing-guide.md)ドアセット実装の見積もりを作成する場合は、アセットストレージ、CPU、メモリ、IO、およびネットワークスループットの点で十分なリソースを確保することが重要です。 これらのアイテムのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。このガイドには、AEM Assetsのデプロイに必要なインフラストラクチャとリソースを見積もるための効率的な指標を決定するのに役立つ、サイジングツールに関するベストプラクティスが含まれています。
* [アセット移行ガイ](assets-migration-guide.md)ド既存のシステムからAEM Assetsにアセットを移行する場合は、移行プロセスを合理化するためのいくつかの手順を検討してください。 移行ガイドには、アセットを段階的にAEMに取り込むために実行するタスクに関するベストプラクティスが含まれています。 これには、メタデータの適用、レンディションの生成、公開デプロイメント用のアセットのアクティブ化が含まれます。
* [アセットネットワークに関する考慮事項](assets-network-considerations.md)AEMデプロイメントを処理する場合、ネットワークのパフォーマンスを理解し、チョークポイントを特定し、期待されるユーザーエクスペリエンスを記述するには、ネットワークトポロジを理解することが重要です。 Assets のネットワークに関する考慮事項のドキュメントでは、AEM Assets のデプロイメントを設計する際のネットワークの考慮事項について説明します。
* [アセット監視ガイ](assets-monitoring-best-practices.md)ドAEMのデプロイ後は、システムの整合性と運用の効率を確保するために、特定のタスクとシステム全般を監視する必要があります。 この監視ガイドには、システムの様々な側面を監視するためのベストプラクティスが記載されています。
* (Deprecated) [Assets offloading guide](assets-offloading-best-practices.md)
Handling large files and running workflows in AEM Assets can consume considerable CPU, memory, and I/O resources. これらのタスクの負荷を軽減すると、CPU、メモリ、およびIOのオーバーヘッドが減少する可能性があります。 Assets オフロードガイドには、Assets オフロードの推奨される使用例およびベストプラクティスが記載されています。
* [AEMデスクトップアプリのベストプラクティス](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app-best-practices.html)AEMデスクトップアプリは、デジタルアセット管理(DAM)ソリューションをデスクトップにリンクし、AEM Web UIで使用できるファイルをデスクトップ上で直接開くことができます。 AEM デスクトップアプリケーションの使いやすいワークフローは、デスクトップのオペレーティングシステムによって提供されるネットワーク共有テクノロジにより有効化されます。このガイドには、AEM デスクトップアプリケーションの主要な機能と推奨される使用例が記載されています。
* [AEMとCreative cloudの統合のベストプラクティス](aem-cc-integration-best-practices.md)AEMの展開をCreative cloudと様々な方法で統合できます。 ベストプラクティスに従って統合ワークフローおよびアセット転送ワークフローを効率化すると、効率を最大化することができます。このガイドには、AEM AssetsとAdobe Creative cloudの統合に関するベストプラクティスが含まれています。
* (Deprecated) [AEM to Creative Cloud folder sharing best practices](aem-cc-folder-sharing-best-practices.md)
You can configure AEM to allow users in DAM to share folders with Creative Cloud (CC) users, so they are available as shared folders in the Creative Cloud Assets service. この機能を使用すると、クリエイティブチームと DAM ユーザーの間でファイルを交換することができます。このガイドでは、AEMからCreative cloudへのフォルダー共有機能を活用するためのベストプラクティスを説明します。
