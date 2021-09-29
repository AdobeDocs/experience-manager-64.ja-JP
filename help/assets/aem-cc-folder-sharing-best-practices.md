---
title: Experience ManagerアセットフォルダーをCreative Cloudと共有
description: Adobe Experience Manager AssetsユーザーがAdobe Creative Cloudユーザーとアセットフォルダーを交換できるようにするための設定とベストプラクティス。
contentOwner: AG
feature: Collaboration
role: User,Admin
exl-id: 7e2adfcc-410d-4574-8f7e-39aceecfdd4b
source-git-commit: 1679bbab6390808a1988cb6fe9b7692c3db31ae4
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 18%

---

# [!DNL Experience Manager] フォルダー共 [!DNL Creative Cloud] 有のベストプラクティス {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>Experience Managerフォルダー共有機能のCreative Cloudは非推奨（廃止予定）となりました。 Adobeでは、[AdobeExperience Managerリンク](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)や[アセットデスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)など、新しい機能を使用することを強くお勧めします。 詳しくは、[Experience ManagerとCreative Cloudの統合に関するベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)を参照してください。

Adobe Experience Managerは、Experience Managerアセット内のユーザーがCreative Cloudーユーザーとフォルダーを共有できるように設定でき、Creative Cloudアセットサービス内の共有フォルダーとして使用できます。 この機能は、クリエイティブチームとExperience Managerアセットユーザー間でファイルを交換する場合に使用できます。特に、クリエイティブユーザーがExperience Managerアセットインスタンスにアクセスできない場合（エンタープライズネットワーク上にない場合）に使用できます。

このタイプの統合は、特にExperience Managerアセットへの直接アクセス権を持たないユーザーと作業する場合に、両方の使用例で使用できます。

* Experience Managerアセットの特定のアセットのセットをCreative Cloudファイルユーザーと共有する（新しいマーケティングアクティビティのデザイン作業用のクリエイティブブリーフや承認済みアセットのセットなど）
*  Creative Cloud ユーザーから新しいファイルを受け取る。

>[!NOTE]
>
>このドキュメントを読む前に、Experience ManagerとCreative Cloudの統合に関するベストプラクティス](aem-cc-integration-best-practices.md)の概要を確認してください。[

## 概要 {#overview}

Experience ManagerからCreative Cloudへのフォルダー共有は、Experience ManagerAssetsとCreative Cloudアカウントの間で、フォルダーとファイルをサーバー側で共有する必要があります。 また、デスクトップでCreative Cloudデスクトップアプリケーションを使用するクリエイティブプロフェッショナルは、Adobe CreativeSyncテクノロジーを使用して、共有フォルダーを直接ディスク上で使用できるようにします。

以下の図は統合の概要を示しています。

![chlimage_1-406](assets/chlimage_1-406.png)

この統合の主要な要素は以下のとおりです。

* **[!DNL Assets]エンタープライズネットワーク（マネージドサービスまたはオンプレミス）にデプロイされた** サーバー：フォルダーの共有はここで開始されます。
* **Adobe Marketing Cloud Assetsコアサービス**:Experience ManagerとCreative Cloud・ストレージ・サービスの仲介役統合を使用する会社の管理者は、Marketing Cloud組織とExperience ManagerAssetsインスタンスの間に信頼関係を確立する必要があります。 また、管理者は、 Assets ユーザーがフォルダーも共有してセキュリティを強化できるように、[承認済みの Creative Cloud 共同作業者のリストを定義](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html#assets)します。
* **Creative CloudアセットWebサービス** (ストレージおよびCreative CloudファイルWeb UI):ここでは、Creative Cloudフォルダーが共有された特定のCreative Cloudユーザーが招待を受け入れ、自分のアカウントストレージにフォルダーが表示されます。
* **Creative Cloudデスクトップアプリケーション**:（オプション）クリエイティブユーザーのデスクトップから、Creative Cloudアセットストレージと同期を使用して共有フォルダー/ファイルに直接アクセスできます。

## 特徴と制限事項 {#characteristics-and-limitations}

* **変更の一方向伝播：** ファイルの変更は、元々アセットが作成（アップロード）された(Experience ManagerまたはCreative Cloudアセットからの)一方向にのみ伝播されます。この統合では、2 つのシステム間で完全に自動化された双方向の同期はおこなわれません。

* **バージョン管理:**

   * Experience Managerは、ファイルがExperience Managerで作成され、そこで更新された場合にのみ、更新時にアセットのバージョンを作成します。
   * Creative Cloud Assets には、作業中（WIP）のファイルが更新された場合に実行される独自の[バージョン管理機能](https://helpx.adobe.com/jp/creative-cloud/help/versioning-faq.html)が用意されています（原則として最大 10 日間更新が保存されます）。

* **容量の制限：** 交換するファイルのサイズとボリュームは、クリエイティブユーザー向けの特定の [Creative Cloudアセットの割合(購読レベルに応じ](https://helpx.adobe.com/jp/creative-cloud/kb/file-storage-quota.html) る)と、最大5 GBのファイルサイズの制限によって制限されます。また、容量は、Adobe Marketing Cloud Assets コアサービスで組織が保有しているアセット割り当てによっても制限されます。

* **容量の要件：** 共有フォルダー内のファイルは、Experience ManagerとCreative Cloudアカウントに物理的に保存し、キャッシュされたコピーをMarketing CloudAssetsコアサービスに保存する必要もあります。
* **ネットワークと帯域幅：** 共有フォルダー内のファイルとすべての更新は、システム間のネットワークを介して転送する必要があります。共有する対象は、関連するファイルおよび更新のみに限るようにしてください。
* **フォルダーの種類**：`sling:OrderedFolder` タイプの Assets フォルダーの共有はサポートされていません。フォルダーを共有する場合は、フォルダーアセットでフォルダーを作成する際に、「順序付き」Experience Managerを選択しないでください。

## ベストプラクティス {#best-practices}

フォルダーとフォルダーの共有をExperience Managerに活用するためのベストプラクティスは次のとおりです。Creative Cloud

* **ボリュームに関する考慮事項：** Experience Manager、Creative Cloudフォルダー共有は、特定のキャンペーンやアクティビティなど、より少ない数のファイルを共有する場合に使用します。組織内の承認済みアセットなど、大量のアセットセットを共有するには、他の配布方法(例：Experience ManagerAssets Brand Portal)やExperience Managerのデスクトップアプリケーションを使用します。
* **深い階層の共有を避ける：** 共有は再帰的に機能し、選択的な共有解除はできません。通常、共有するフォルダーは、サブフォルダーを持たないか、1 つ下のレベルのサブフォルダーなど非常に浅い階層しか持たないものに限るようにしてください。
* **一方向共有用にCreative Cloudーを分離する：** 最終アセットをExperience ManagerアセットからCreative Cloudファイルに共有したり、クリエイティブレディアセットをファイルからに共有したりする場合は、個別のフォルダーを使用する必要があ [!DNL Assets]ります。これらのフォルダーに適切な命名規則を適用すると、Experience ManagerアセットとCreative Cloudユーザーを同様に理解しやすい作業環境を作成できます。
* **共有Creative Cloudー内でWIPを避ける：** 共有フォルダーは作業中には使用しないでください。ファイルに頻繁に変更を加える必要のある作業を実行するには、共有フォルダーを作業中に別のフォルダーを使用します。
* **共有Creative Cloudー以外で新しい作業を開始：** 新しいデザイン（クリエイティブファイル）は、Experience Managerファイル内の別のWIPフォルダーで開始する必要があり、Assetsユーザーと共有する準備が整ったら、共有フォルダーに移動または保存する必要があります。
* **共有構造の簡素化：** より管理しやすいオペレーティングセットアップをおこなうには、共有構造を簡素化することを検討してください。Experience Managerアセットフォルダーは、すべてのクリエイティブユーザーと共有する代わりに、クリエイティブディレクターやチームマネージャーなど、チーム担当者とのみ共有する必要があります。 クリエイティブサイドのマネージャーが最終アセットを受け取って作業割り当てを決定し、デザイナーは自身の Creative Cloud アカウントで WIP アセットの作業をするようにします。Creative Cloudのコラボレーション機能を使用して作業を調整し、最後に、Experience Managerアセットで共有する準備が整ったアセットを選択して、クリエイティブレディの共有フォルダーに戻すことができます。

次の図は、Experience ManagerAssetsの既存の最終アセットに基づいて新しいデザインを作成するための設定例を示しています。

![chlimage_1-407](assets/chlimage_1-407.png)
