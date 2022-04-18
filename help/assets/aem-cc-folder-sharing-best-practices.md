---
title: Experience Manager AssetsフォルダーをCreative Cloudと共有
description: Adobe Experience Manager Assets ユーザーがAdobe Creative Cloudユーザーとアセットフォルダーを交換できるようにする設定とベストプラクティス。
contentOwner: AG
feature: Collaboration
role: User,Admin
exl-id: 7e2adfcc-410d-4574-8f7e-39aceecfdd4b
source-git-commit: 1679bbab6390808a1988cb6fe9b7692c3db31ae4
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 31%

---

# [!DNL Experience Manager] から [!DNL Creative Cloud] フォルダー共有のベストプラクティス {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>Experience Manager-Creative Cloudフォルダー共有機能は非推奨です。 [Adobe Asset Link](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) または [Experience Manager デスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)などの新しい機能を使用することを強くお勧めします。詳しくは、[Experience Manager と Creative Cloud の統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)を参照してください。

Adobe Experience Managerは、Experience Manager AssetsのユーザーがCreative Cloudーユーザーとフォルダーを共有できるように設定できるので、Creative Cloudアセットサービスで共有フォルダーとして使用できます。 この機能は、クリエイティブチームとExperience Manager Assetsユーザー間でファイルを交換する場合に使用できます。特に、クリエイティブユーザーがExperience Manager Assetsインスタンスにアクセスできない場合（エンタープライズネットワーク上にない場合）に使用できます。

このタイプの統合は、両方の使用例で使用できます。特に、Experience Manager Assetsへの直接アクセス権を持たないユーザーを扱う場合に便利です。

* Experience Manager Assetsの特定のアセットのセットをCreative Cloudファイルユーザーと共有する（新しいマーケティングアクティビティのデザイン作業に使用する、クリエイティブな概要や承認済みアセットのセットなど）
*  Creative Cloud ユーザーから新しいファイルを受け取る。

>[!NOTE]
>
>このドキュメントを読む前に、 [Experience ManagerとCreative Cloudの統合のベストプラクティス](aem-cc-integration-best-practices.md) を参照してください。

## 概要 {#overview}

Experience ManagerからCreative Cloudへのフォルダー共有は、Experience Manager AssetsとCreative Cloudアカウントの間で、サーバー側でフォルダーやファイルを共有する必要があります。 また、デスクトップでCreative Cloudデスクトップアプリケーションを使用するクリエイティブプロフェッショナルは、Adobe CreativeSyncテクノロジーを使用して、共有フォルダーをディスク上で直接使用できるようにします。

以下の図は統合の概要を示しています。

![chlimage_1-406](assets/chlimage_1-406.png)

この統合の主要な要素は以下のとおりです。

* **[!DNL Assets]server** エンタープライズネットワーク（マネージドサービスまたはオンプレミス）にデプロイされる場合：フォルダーの共有はここで開始されます。
* **Adobe Marketing Cloud Assets コアサービス**:Experience ManagerとCreative Cloud・ストレージ・サービスの仲介を行う。 統合を使用する会社の管理者は、Marketing Cloud組織とExperience Manager Assetsインスタンスの間に信頼関係を確立する必要があります。 また、管理者は、 Assets ユーザーがフォルダーも共有してセキュリティを強化できるように、[承認済みの Creative Cloud 共同作業者のリストを定義](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html?lang=ja#アセット)します。
* **Creative CloudAssets Web サービス** ( ストレージおよびCreative Cloudファイル Web UI):特定のCreative Cloudユーザー（アセットフォルダーの共有先）が招待を受け入れ、Creative Cloudアカウントストレージにそのフォルダーを表示できるようになります。
* **Creative Cloudデスクトップアプリケーション**:（オプション）クリエイティブユーザーのデスクトップから、Creative Cloudアセットストレージとの同期を介して、共有フォルダー/ファイルに直接アクセスできるようにします。

## 特徴と制限事項 {#characteristics-and-limitations}

* **変更の一方向の伝播：** ファイルの変更は、アセットが最初に作成（アップロード）されたシステム (Experience ManagerーまたはCreative Cloudーアセット ) から 1 方向にのみ反映されます。 この統合では、2 つのシステム間で完全に自動化された双方向の同期はおこなわれません。

* **バージョン管理:**

   * Experience Managerは、ファイルがExperience Managerで生成され、そこで更新された場合にのみ、更新時にアセットのバージョンを作成します。
   * Creative Cloud Assets には、作業中（WIP）のファイルが更新された場合に実行される独自の[バージョン管理機能](https://helpx.adobe.com/jp/creative-cloud/help/versioning-faq.html)が用意されています（原則として最大 10 日間更新が保存されます）。

* **容量制限：**&#x200B;交換するファイルのサイズおよびボリュームは、クリエイティブユーザーに適用される特定の [Creative Cloud Assets 割り当て](https://helpx.adobe.com/jp/creative-cloud/kb/file-storage-quota.html)（サブスクリプションレベルに依存します）とファイルサイズの上限（5 GB）によって制限されます。また、容量は、Adobe Marketing Cloud Assets コアサービスで組織が保有しているアセット割り当てによっても制限されます。

* **容量要件：** また、共有フォルダー内のファイルは、Experience ManagerとCreative Cloudアカウントに物理的に保存し、キャッシュされたコピーをMarketing CloudAssets コアサービスに保存する必要があります。
* **ネットワークと帯域幅：**&#x200B;共有フォルダーのファイルとその更新はすべて、システム間のネットワーク経由で転送する必要があります。共有する対象は、関連するファイルおよび更新のみに限るようにしてください。
* **フォルダーの種類**：`sling:OrderedFolder` タイプの Assets フォルダーの共有はサポートされていません。フォルダーを共有する場合は、Experience Manager Assetsでフォルダーを作成する際に、「並べ替え」オプションを選択しないでください。

## ベストプラクティス {#best-practices}

Experience Managerをフォルダー共有に活用するためのベストプラクティスは、次のとおりです。Creative Cloud

* **ボリュームに関する考慮事項：** Experience Manager、Creative Cloudフォルダーの共有は、特定のキャンペーンやアクティビティに関連した、より少ない数のファイルを共有する場合に使用します。 組織内の承認済みアセットなど多数のアセットを共有するには、他の配布方法 (Experience Manager Assets Brand Portalなど ) やExperience Managerデスクトップアプリケーションを使用します。
* **深い階層を共有しない：** 共有は再帰的に機能し、選択的な共有解除は許可されません。 通常、共有するフォルダーは、サブフォルダーを持たないか、1 つ下のレベルのサブフォルダーなど非常に浅い階層しか持たないものに限るようにしてください。
* **一方向の共有用にフォルダを分割する：** 最終的なアセットをExperience Manager AssetsからCreative Cloudファイルに共有したり、クリエイティブレディアセットをCreative Cloudファイルからに共有したりするには、個別のフォルダーを使用します。 [!DNL Assets]. これらのフォルダーに適した命名規則を使用すると、Experience Manager AssetsユーザーとCreative Cloudユーザーを同様に理解しやすい作業環境を作成できます。
* **WIP 作業のために共有フォルダーを使用しない：**&#x200B;共有フォルダーは、処理中の作業（WIP）で使用しないでください。ファイルを頻繁に変更する必要がある作業を行うには、Creative Cloud Files の別のフォルダーを使用します。
* **共有フォルダー以外で新しい作業を開始：** 新しいデザイン（クリエイティブファイル）は、Creative Cloudファイル内の別の WIP フォルダーで開始する必要があり、Experience Manager Assetsユーザーと共有する準備が整ったら、共有フォルダーに移動または保存する必要があります。
* **共有の構造を簡素化する：**&#x200B;操作の設定管理を向上させるには、共有の構造を簡素化する必要があります。すべてのクリエイティブユーザーと共有する代わりに、Experience Manager Assetsフォルダーは、クリエイティブディレクターやチームマネージャーと同様に、チーム担当者とのみ共有する必要があります。 クリエイティブサイドのマネージャーが最終アセットを受け取って作業割り当てを決定し、デザイナーは自身の Creative Cloud アカウントで WIP アセットの作業をするようにします。Creative Cloudのコラボレーション機能を使用して作業を調整し、最後に、Experience Manager Assetsで共有する準備が整ったアセットを選択して、クリエイティブレディ共有フォルダーに戻すことができます。

次の図は、Experience Manager Assetsの既存の最終アセットに基づいて新しいデザインを作成するための設定例を示しています。

![chlimage_1-407](assets/chlimage_1-407.png)
