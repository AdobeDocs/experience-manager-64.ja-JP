---
title: Creative CloudとAEM Assetsフォルダを共有する
description: Adobe Experience ManagerアセットユーザがAdobe Creative Cloudユーザとアセットフォルダを交換できるようにするための設定とベストプラクティスです。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 501a6c470113d249646f4424a19ee215a82b032d
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 44%

---


# AEM／CC フォルダー共有のベストプラクティス {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>AEM／Creative Cloud フォルダー共有機能は廃止されました。Adobeでは、 [Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) 、AEMデスクトップアプリなど、新しい機能を使用することを強くお勧めします [](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app.html)。 Learn more in [AEM and Creative Cloud integration best practices](/help/assets/aem-cc-integration-best-practices.md).

Adobe Experience Manager(AEM)は、AEM AssetsのユーザーがCreative Cloudユーザーとフォルダーを共有できるように設定できるので、Creative Cloudアセットサービスで共有フォルダーとして使用できます。 この機能を使用すると、クリエイティブチームと AEM Assets ユーザーの間でファイルをやり取りすることができます。特に、クリエイティブユーザーが AEM Assets インスタンスへのアクセス権を持っていない（エンタープライズネットワーク上にいない）場合に便利です。

このタイプの統合は、以下のどちらの例でも使用できます。特に、AEM Assets への直接アクセス権を持っていないユーザーと作業する場合に有用です。

* AEM Assets の特定のアセットのセットを CC Files のユーザーと共有する（例えば、新しいマーケティングアクティビティのデザインワークのためのクリエイティブブリーフおよび承認されたアセットのセット）。
*  Creative Cloud ユーザーから新しいファイルを受け取る。

>[!NOTE]
>
>このドキュメントを読む前に、[AEM と Creative Cloud の統合のベストプラクティス](aem-cc-integration-best-practices.md)全体をよく読むと、このトピックについて概要を把握することができます。

## 概要 {#overview}

AEMからCreative Cloudへのフォルダー共有は、AEM AssetsとCreative Cloudのアカウント間でフォルダーとファイルをサーバー側で共有することに依存しています。 クリエイティブプロフェッショナルは、デスクトップでCreative Cloudデスクトップアプリケーションを使用し、Adobe CreativeSyncテクノロジを使用してディスク上で直接共有フォルダーを使用できるようにすることもできます。

以下の図は統合の概要を示しています。

![chlimage_1-406](assets/chlimage_1-406.png)

この統合の主要な要素は以下のとおりです。

* **エンタープライズネットワークに導入されたAEM Assetsサーバ** （マネージドサービスまたはオンプレミス）: ここでフォルダの共有を開始します。
* **Adobe Marketing Cloud Assets コアサービス**：AEM と CC ストレージサービスの中間のサービスです。この統合を使用する企業の管理者は、Marketing Cloud 組織と AEM Assets インスタンスの間に信頼関係を確立する必要があります。また、管理者は、AEM Assets ユーザーがフォルダーも共有してセキュリティを強化できるように、[承認済みの Creative Cloud 共同作業者のリストを定義](https://docs.adobe.com/content/help/en/core-services/interface/assets/t-admin-add-cc-user.html)します。
* **Creative CloudアセットWebサービス** (ストレージファイルとCreative CloudファイルWeb UI): ここでは、AEM AssetsCreative Cloudーが共有された特定のCreative Cloudユーザーが招待を受諾し、そのユーザーのフォルダーアカウントストレージー内のフォルダーを確認できます。
* **Creative Cloudデスクトップアプリケーション**: （オプション）クリエイティブCreative Cloudのデスクトップから、フォルダーアセットストレージと同期して、共有フォルダーや共有ファイルに直接アクセスできます。

## 特徴と制限事項 {#characteristics-and-limitations}

* **変更の一方向伝播：** ファイルの変更は、1方向(アセットが最初に作成（アップロード）されたシステム(AEMまたはCreative Cloudアセット)からのみ反映されます。 この統合では、2 つのシステム間で完全に自動化された双方向の同期はおこなわれません。

* **バージョン管理:**

   * AEM では、AEM で作成および更新されたファイルについて、更新があった場合のみ、アセットのバージョンを作成します。
   * Creative Cloud Assets には、作業中（WIP）のファイルが更新された場合に実行される独自の[バージョン管理機能](https://helpx.adobe.com/jp/creative-cloud/help/versioning-faq.html)が用意されています（原則として最大 10 日間更新が保存されます）。

* **スペースの制限：** 交換するファイルのサイズと量は、クリエイティブユーザー向けの [Creative Cloudアセットの割り当て](https://helpx.adobe.com/jp/creative-cloud/kb/file-storage-quota.html) (購読レベルに応じる)と、最大5 GBのファイルサイズ制限によって制限されます。 また、容量は、Adobe Marketing Cloud Assets コアサービスで組織が保有しているアセット割り当てによっても制限されます。

* **必要な領域：** 共有フォルダー内のファイルも、AEMに物理的に保存され、次にCreative Cloudアカウントに保存され、キャッシュされたコピーと共にMarketing Cloudアセットコアサービスに保存する必要があります。
* **ネットワークと帯域幅：** 共有フォルダー内のファイルとすべての更新を、システム間でネットワーク経由で転送する必要があります。 共有する対象は、関連するファイルおよび更新のみに限るようにしてください。
* **フォルダーの種類**：`sling:OrderedFolder` タイプの Assets フォルダーの共有はサポートされていません。フォルダーを共有したい場合は、AEM Assets でフォルダーを作成するときに「並べ替え」オプションを選択しないでください。

## ベストプラクティス {#best-practices}

AEM／CC フォルダー共有を活用するベストプラクティスには、以下のものが含まれます。

* **ボリュームの考慮事項：** 特定のキャンペーンやアクティビティなど、少数のファイルを共有する場合は、AEM/Creative Cloudのフォルダ共有を使用する必要があります。 組織で承認されたアセットすべてなど、多数のアセットのセットを共有するには、他の配信方法（例えば AEM Assets Brand Portal）や AEM デスクトップアプリを使用してください。
* **階層の深い共有を避ける：** 共有は再帰的に機能し、選択的な非共有は許可されません。 通常、共有するフォルダーは、サブフォルダーを持たないか、1 つ下のレベルのサブフォルダーなど非常に浅い階層しか持たないものに限るようにしてください。
* **一方向の共有用に別々のフォルダーを作成する：** 最終アセットをAEM AssetsからCreative Cloudファイルに共有する場合、およびクリエイティブに対応したアセットをCreative CloudファイルからAEM Assetsに共有する場合は、個別のフォルダーを使用する必要があります。 これらのフォルダーに適した命名規則を組み合わせると、AEM AssetsユーザーとCreative Cloudユーザーの両方に対して、理解しやすい作業環境が作成されます。
* **共有フォルダーでのWIPの回避：** 共有フォルダーは作業中には使用しないでください。ファイルに頻繁に変更を加える必要がある作業を行うには、Creative Cloudファイル内の別のフォルダーを使用します。
* **共有フォルダー外での開始の新しい作業：** 新しいデザイン（クリエイティブファイル）は、Creative Cloudファイル内の別のWIPフォルダーで開始する必要があります。AEM Assetsユーザーと共有する準備が整ったら、共有フォルダーに移動または保存する必要があります。
* **構造の共有の簡素化：** より管理しやすいオペレーティング設定を行うには、共有構造の簡素化を検討してください。 すべてのクリエイティブユーザーと共有する代わりに、AEM Assetsのフォルダーは、クリエイティブディレクターやチームマネージャーなど、チームの担当者とのみ共有する必要があります。 クリエイティブサイドのマネージャーが最終アセットを受け取って作業割り当てを決定し、デザイナーは自身の Creative Cloud アカウントで WIP アセットの作業をするようにします。Creative Cloudのコラボレーション機能を使用して作業を調整し、最後に、AEM Assetsに共有するアセットを選択して、クリエイティブに対応した共有フォルダーに戻すことができます。

以下の図に、AEM Assets の既存の最終アセットに基づいて新しいデザインを作成するための設定例を示します。

![chlimage_1-407](assets/chlimage_1-407.png)
