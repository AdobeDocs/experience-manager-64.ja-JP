---
title: Creative CloudとAEM Assetsフォルダを共有する
description: Adobe Experience ManagerアセットユーザがAdobe Creative Cloudユーザとアセットフォルダを交換できるようにするための設定とベストプラクティスです。
contentOwner: AG
feature: コラボレーション
role: 業務担当者、管理者
translation-type: tm+mt
source-git-commit: 29e3cd92d6c7a4917d7ee2aa8d9963aa16581633
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 44%

---


# AEM／CC フォルダー共有のベストプラクティス {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>AEM／Creative Cloud フォルダー共有機能は廃止されました。Adobeでは、[Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)や[AEMデスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)など、新しい機能を使用することを強くお勧めします。 詳細については、[AEMとCreative Cloud統合のベストプラクティス](/help/assets/aem-cc-integration-best-practices.md)を参照してください。

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

* **エンタープライズネットワークに導入されたAEM Assets** サーバー（マネージドサービスまたはオンプレミス）:ここでフォルダの共有を開始します。
* **Adobe Marketing Cloud Assets コアサービス**：AEM と CC ストレージサービスの中間のサービスです。この統合を使用する企業の管理者は、Marketing Cloud 組織と AEM Assets インスタンスの間に信頼関係を確立する必要があります。また、管理者は、AEM Assets ユーザーがフォルダーも共有してセキュリティを強化できるように、[承認済みの Creative Cloud 共同作業者のリストを定義](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html?lang=en#assets)します。
* **Creative CloudアセットWebサービス** (ストレージファイルとCreative CloudファイルWeb UI):ここでは、AEM AssetsCreative Cloudーが共有された特定のCreative Cloudユーザーが招待を受諾し、そのユーザーのフォルダーアカウントストレージー内のフォルダーを確認できます。
* **Creative Cloudデスクトップアプリケーション**:（オプション）クリエイティブCreative Cloudのデスクトップから、フォルダーアセットストレージと同期して、共有フォルダーや共有ファイルに直接アクセスできます。

## 特徴と制限事項 {#characteristics-and-limitations}

* **変更の一方向の伝達：** ファイルの変更は、アセットが最初に作成（アップロード）された（最初に作成された）システム(AEMまたはCreative Cloudアセット)から、1方向にのみ伝達されます。この統合では、2 つのシステム間で完全に自動化された双方向の同期はおこなわれません。

* **バージョン管理:**

   * AEM では、AEM で作成および更新されたファイルについて、更新があった場合のみ、アセットのバージョンを作成します。
   * Creative Cloud Assets には、作業中（WIP）のファイルが更新された場合に実行される独自の[バージョン管理機能](https://helpx.adobe.com/jp/creative-cloud/help/versioning-faq.html)が用意されています（原則として最大 10 日間更新が保存されます）。

* **スペースの制限：交換するファイルの** サイズと量は、クリエイティブユーザー向けの [Creative Cloudアセットの](https://helpx.adobe.com/jp/creative-cloud/kb/file-storage-quota.html) クォータ(購読レベルによる)と最大5 GBの制限によって制限されます。また、容量は、Adobe Marketing Cloud Assets コアサービスで組織が保有しているアセット割り当てによっても制限されます。

* **容量の要件：共有フォルダ** ー内のファイルも、物理的にAEMに格納し、次にCreative Cloudアカウントに格納し、キャッシュされたコピーをMarketing Cloudアセットコアサービスに格納する必要があります。
* **ネットワークと帯域幅：共有フォルダ** ー内のファイルとすべての更新を、システム間でネットワーク経由で転送する必要があります。共有する対象は、関連するファイルおよび更新のみに限るようにしてください。
* **フォルダーの種類**：`sling:OrderedFolder` タイプの Assets フォルダーの共有はサポートされていません。フォルダーを共有したい場合は、AEM Assets でフォルダーを作成するときに「並べ替え」オプションを選択しないでください。

## ベストプラクティス {#best-practices}

AEM／CC フォルダー共有を活用するベストプラクティスには、以下のものが含まれます。

* **ボリュームに関する考慮事項：** AEM/Creative Cloudフォルダー共有は、特定のキャンペーンやアクティビティに関連するなど、少数のファイルを共有する場合に使用します。組織で承認されたアセットすべてなど、多数のアセットのセットを共有するには、他の配信方法（例えば AEM Assets Brand Portal）や AEM デスクトップアプリを使用してください。
* **深い階層の共有を避ける：共有** は再帰的に機能し、選択的な非共有は許可されません。通常、共有するフォルダーは、サブフォルダーを持たないか、1 つ下のレベルのサブフォルダーなど非常に浅い階層しか持たないものに限るようにしてください。
* **一方向の共有用に別々のフォルダー：最終アセットをAEM AssetsからCreative Cloudファイルに共有したり、クリエイティブに対応したアセットをCreative CloudファイルからAEM Assetsに共有したりするには、** 別々のフォルダーを使用します。これらのフォルダーに適した命名規則を組み合わせると、AEM AssetsユーザーとCreative Cloudユーザーの両方にとって、より分かりやすい作業環境が作成されます。
* **共有フォルダーでのWIPの回避：** 共有フォルダーは作業中には使用しないでください。ファイルに頻繁に変更を加える必要がある作業を実行するには、Creative Cloudファイルで別のフォルダーを使用します。
* **共有フォルダー以外での開始の新しい作業：** 新しいデザイン（クリエイティブファイル）は、Creative Cloudファイル内の別のWIPフォルダーで開始する必要があります。AEM Assetsユーザーと共有する場合は、移動するか共有フォルダーに保存します。
* **構造の共有の簡素化：より管理しや** すいオペレーティングの設定を行うため、構造の共有を簡素化することを検討してください。すべてのクリエイティブユーザーと共有する代わりに、AEM Assetsのフォルダーは、クリエイティブディレクターやチームマネージャーなど、チームの担当者とのみ共有する必要があります。 クリエイティブサイドのマネージャーが最終アセットを受け取って作業割り当てを決定し、デザイナーは自身の Creative Cloud アカウントで WIP アセットの作業をするようにします。Creative Cloudのコラボレーション機能を使用して作業を調整し、最後に、AEM Assetsに共有するアセットを選択して、クリエイティブに対応した共有フォルダーに戻すことができます。

以下の図に、AEM Assets の既存の最終アセットに基づいて新しいデザインを作成するための設定例を示します。

![chlimage_1-407](assets/chlimage_1-407.png)
