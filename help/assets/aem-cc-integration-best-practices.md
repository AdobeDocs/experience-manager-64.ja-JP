---
title: Experience Manager と Creative Cloud の統合のベストプラクティス
description: Adobe Creative Cloudと [!DNL Experience Manager] デプロイメントを統合し、アセット転送ワークフローを効率化し、効率を最大化するためのベストプラクティス
contentOwner: AG
feature: Collaboration,Adobe Asset Link,Desktop App
role: User,Admin
exl-id: cb9bea05-3359-4fb4-b935-59e522a5f387
source-git-commit: 1679bbab6390808a1988cb6fe9b7692c3db31ae4
workflow-type: tm+mt
source-wordcount: '3488'
ht-degree: 64%

---

# [!DNL Experience Manager] と統合の [!DNL Creative Cloud] ベストプラクティス {#aem-and-creative-cloud-integration-best-practices}

<!-- TBD: Reconcile with 6.5 article that's ahead of this article now in terms of content streamlining and structuring.
-->

Adobe Experience Manager Assetsは、Adobe Creative Cloudと統合して、DAMユーザーがクリエイティブチームと連携し、コンテンツ作成プロセスでのコラボレーションを合理化する、デジタルアセット管理(DAM)ソリューションです。

Adobe Creative Cloud は、デジタルアセットの作成を支援するソリューションとサービスのエコシステムをクリエイティブチームに提供します。これには、デスクトップおよびモバイルアプリケーション、デスクトップ同期や Web エクスペリエンスを備えたストレージなどのクラウドサービス、および Adobe Stock などのマーケットプレイスが含まれます。

使用例に基づいてデスクトップとエンタープライズクラスの DAM の間で選択すべき統合や、つながるワークフローに関連するベストプラクティスについては、このドキュメントで説明します。

>[!NOTE]
>
>[!DNL Experience Manager]からCreative Cloudへのフォルダー共有は廃止され、このガイドでは扱われなくなりました。 Adobeでは、[!DNL Experience Manager]で管理されたAdobeにアクセスできるよう、[アセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html)や[[!DNL Experience Manager] デスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=ja)などの新しい機能を使用することをお勧めします。

## クリエイティブ、マーケター、DAMユーザーのコラボレーションニーズ {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要件 | 使用例 | 関係するサーフェス |
|---|---|---|
| デスクトップ上でクリエイティブプロフェッショナル向けのエクスペリエンスを簡素化する | クリエイティブプロフェッショナル、またはネイティブのアセット作成アプリケーションで作業するデスクトップユーザー向けに、DAM([!DNL Assets])からのアセットへのアクセスを合理化します。 [!DNL Experience Manager]を簡単かつ簡単に検出し、（開く）、編集し、変更をに保存し、新しいファイルをアップロードする方法が必要です。 | Windows または Mac デスクトップ、Creative Cloud アプリ |
| すぐに使用できる高品質なアセットを Adobe Stock から提供する | マーケティング担当者は、アセットの調達と検出を支援することでコンテンツ作成プロセスの促進に貢献します。クリエイティブプロフェッショナルは、承認されたアセットをクリエイティブツール内から直接使用します。 | [!DNL Assets];Adobe Stock marketplace;メタデータフィールド |
| 組織でアセットを配布および共有する | 社内部門／支店および外部のパートナー、ディストリビューター、代理店は、親組織で共有されている承認済みアセットを使用します。組織では、作成したアセットを安全かつシームレスに共有して幅広く再利用したいと考えています。 | Brand Portal、Asset Share Commons |

## コラボレーションニーズをサポートするアドビ製品／サービス {#adobe-offerings-to-support-the-collaboration-need}

| 関係するユーザーに対する価値提案 | アドビ製品／サービス | 関係するサーフェス |
|---|---|---|
| クリエイティブユーザーは、[!DNL Experience Manager]からCreative Cloudを検出し、開いて使用し、変更を編集して[!DNL Experience Manager]にアップロードし、新しいファイルを[!DNL Experience Manager]にアップロードします。また、アセットアプリを残す必要はありません。 | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator、InDesign |
| ビジネスユーザーは、アセットの開封と使用、編集と[!DNL Experience Manager]への変更のアップロード、デスクトップ環境から[!DNL Experience Manager]への新しいファイルのアップロードを簡単におこなえます。 汎用の統合を使用して、アドビ以外のアセットも含め、あらゆるアセットタイプをネイティブデスクトップアプリケーションで開きます。 | [[!DNL Experience Manager] デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja) | [!DNL Experience Manager]Windows および Mac デスクトップ上の デスクトップアプリケーション |
| マーケターとビジネスユーザーは、[!DNL Experience Manager]内からAdobe Stockアセットを検出、プレビュー、ライセンス、保存および管理します。 ライセンスを取得し保存したアセットは、限定された Adobe Stock メタデータを提供してガバナンスの強化に役立ちます。 | [Adobe Experience Manager と Adobe Stock との連携](aem-assets-adobe-stock.md) | [!DNL Experience Manager] webインターフェイス |

ここでは、主に、コラボレーションニーズの最初の 2 つの側面に焦点を当てます。アセットの大規模な配布と調達については、使用例として簡単に説明します。そのようなニーズに対するソリューションとしては、Adobe Brand Portal または Asset Share Commons を検討してください。代替ソリューション([Brand Portal](https://helpx.adobe.com/jp/experience-manager/brand-portal/user-guide.html)、[Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)コンポーネントに基づいて構築できるソリューション、[Link Share](/help/assets/link-sharing.md)、[Experience Managerアセット](/help/assets/managing-assets-touch-ui.md)の使用など)については、特定の要件に基づいて検討する必要があります。

![Creative Cloud接 [!DNL Experience Manager]続：使用する機能の決定](assets/creative-connections-aem.png)

<!-- 
## Terms and definitions {#terms-and-definitions}

The terms used in this document may have a different meaning in other contexts. In particular, the following terms pertaining to the digital asset lifecycle are used when referring to workflows between a creative professional's desktop and DAM:

* **Work-in-progress or creative work-in-progress (WIP):** A phase in asset lifecycle where an asset undergoes multiple changes and is typically not yet ready to be shared with broader teams.
* **Creative-ready assets:** Assets that are ready to be shared with a broader team, or have been  selected / approved  by the creative team for sharing with marketing or LOB teams.
* **Asset approvals:** The approval process that runs for assets already uploaded to DAM, which typically includes brand approvals, legal approvals, and so on.
* **Final asset:** An asset that has gone through all  approvals/metadata  tagging and is ready to be used by the broader team. Such an asset is stored in DAM and made available to all (or all interested) users. It can be used in marketing channels or by creative teams to create designs.
* **Minor asset  update/change:** A quick and small change to a digital asset. It is often made in response to a retouching or minor editing request, asset review, or approval (for example, reposition, change text size, adjust saturation/brightness, color, and so on).
* **Major asset  update/change:** A change to a digital asset that requires considerable work, and sometimes must be done over a longer period of time. It typically includes multiple changes. The asset must be saved multiple times while being updated. Major asset updates typically cause the asset to enter a WIP stage.
* **DAM:** Digital asset management. In this document, it is synonymous with Experience Manager Assets, unless specifically mentioned otherwise.
* **Creative user:** A creative professional, who creates digital assets using Creative Cloud apps and services. In some cases, a creative user may be a member of a creative team who may use Creative Cloud, but does not create digital assets (like a creative director or creative team manager).
* **DAM user:** A typical user of a DAM system. Depending on the organization, a DAM user can be a marketing or a non-marketing user, for example a Line-of-Business (LOB) user, librarian, sales person, and so on.
-->

### 使用例のマッピング

| 使用例 | [!DNL Experience Manager] デスクトップアプリケーション | フォルダーの共有 | その他のソリューション |
|---|---|---|---|
| 少数のDAMアセットをクリエイティブユーザーと共有する | ✔✔ | ✔ |  |
| DAMアセットの数(2)をクリエイティブユーザーと共有する | ✔✔ | ✘ | [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) <br> [アセット共有](assets-finder-editor.md) |
| DAM へのアクセス権を持っているユーザーと DAM アセットを共有する | ✔✔ | ✔ | [リンク共有](link-sharing.md) |
| DAM へのアクセス権を持っていないユーザーと DAM アセットを共有する | ✘ | ✔✔ | [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) <br> [アセット共有](assets-finder-editor.md) |
| 少数／小さいボリュームのアセットを DAM に保存する | ✔✔ | ✔ | [Web UI によるアップロード](managing-assets-touch-ui.md) |
| DAMに多数のアセットを保存する(3) | ✔✔ | ✘ | [Web UI によるアップロード](managing-assets-touch-ui.md)  <br> カスタムスクリプト/ツール |
| DAM へ膨大な量のアセットを移行する | ✘ | ✘ | [移行ガイド](assets-migration-guide.md) |
| デスクトップですばやくアセットを開く | ✔✔ | ✘ |  |
| デスクトップですばやくアセットを開いて変更する | ✔✔ | ✘ |  |

シンボルの凡例：

* ✔✔：推奨されるソリューション
* ✔：許容されるソリューション
* ✘：この例に使用してはならない

補足：

* (1)少ない資産数：例えば、プロジェクトまたはキャンペーンに関連するアセットの小さなセットなどです
* (2)資産数の増加：例えば、組織内のすべての承認済みアセットなどです
* (3)[!DNL Experience Manager]デスクトップアプリケーションのアップロードフォルダー機能を使用する

アセット配布使用例をサポートするには、他のソリューションを考慮に入れる必要があります。

* [Brand Portalを使用す](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) ると、Assetsに設定可能なSaaSアドオンを使用し [!DNL Experience Manager] て、アセットを公開できます。
* カスタムソリューションは [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) のコードベースに基づいて作成される。
* [!DNL Experience Manager][ リンク共有](/help/assets/link-sharing.md)：リンクを使用してアドホックでアセットを共有する。
* [[!DNL Experience Manager] Assets Webインタ](/help/assets/managing-assets-touch-ui.md) ーフェイスは、アクセス制御の設定で保護される外部の関係者向けの領域と、必要なIT/ネットワーク設定の調整をおこな [!DNL Experience Manager] い、外部ユーザーがにアクセスできるようにしま [!DNL Experience Manager]す。

## 主な概念と使用例 {#key-concepts-and-use-cases}

### よく使用される用語 {#glossary-of-common-terms}

* **作業中（WIP）またはクリエイティブ WIP：**&#x200B;アセットライフサイクルのフェーズ。アセットに対してまだ複数の変更がおこなわれている最中であり、通常は、より広範なチームと共有するための準備がまだできていない状態。
* **クリエイティブレディアセット：**&#x200B;より広範なチームと共有するための準備ができているアセット。または、マーケティングチームもしくは LOB チームと共有するためにクリエイティブチームによって選択／承認されているアセット。
* **アセット承認：** 既に DAM にアップロードされているアセットに対して実行される承認プロセス。通常、ブランド承認および法的承認などが含まれます。
* **最終アセット：**&#x200B;すべての承認／メタデータタグ付けが完了し、より広範なチームに使用される準備ができているアセット。このようなアセットは DAM に保存され、すべてのユーザー（またはすべての関係者）が使用できるようになっています。マーケティングチャネルで使用したり、クリエイティブチームがデザインの作成に使用したりできます。
* **アセットの小規模な更新／変更：**&#x200B;デジタルアセットに対する迅速で小規模な変更。多くの場合、リタッチ作業や小規模な編集の要求、アセットレビューまたは承認に対応するためにおこなわれます（例えば、再配置、テキストサイズの変更、彩度／明るさ、色などの調整）。
* **アセットの大規模な更新／変更：**&#x200B;デジタルアセットに加えられる、大規模な作業が必要な変更。その変更作業は比較的長期にわたる場合もあります。通常は複数の変更が含まれます。アセットは、更新中、複数回保存する必要があります。アセットの大規模な更新により、ほとんどの場合、アセットのステージは WIP になります。
* **DAM：**&#x200B;デジタルアセット管理。このドキュメントでは、特に断りのない限り、[!DNL Experience Manager Assets]と同義です。
* **クリエイティブユーザー：** Creative Cloud のアプリケーションとサービスを使用してデジタルアセットを作成するクリエイティブプロフェッショナル。クリエイティブチームに所属し、Creative Cloud を使用するが、デジタルアセットの作成はおこなわないメンバー（クリエイティブディレクターやクリエイティブチームマネージャーなど）を含む場合もあります。
* **DAM ユーザー：** DAM システムの一般的な利用者。組織によっては、マーケティング分野のユーザーもマーケティング以外の分野のユーザーも含まれます（例えば、事業部門（LOB）ユーザー、ライブラリアン、販売担当者など）。

### [!DNL Experience Manager]とCreative Cloud統合を使用する際の考慮事項 {#considerations-when-using-aem-and-creative-cloud-integration}

* [デスクトップアプリケーションのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)を参照してください。
* [Adobe Stock統合](aem-assets-adobe-stock.md)を参照
* [Adobeアセットリンク](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)を参照

Experience ManagerとCreative Cloudの統合に関するベストプラクティスの概要です。 以下のそれぞれの項目の詳細は、このドキュメントで後述されています。

* **Photoshop、InDesign、Illustrator のいずれかで作業しているクリエイティブユーザーの場合：** Adobe Asset Link は、 からチェックアウトされたアセットの更新の適切な処理など、最適なユーザーエクスペリエンスを提供します。[!DNL Experience Manager]
* **任意の汎用ファイル形式またはアプリケーションについてデスクトップからアセットへのアクセスを簡素化する場合：**[!DNL Experience Manager] デスクトップアプリケーションを使用します。
* **アセットを DAM に保存する理由とタイミングを理解する：**&#x200B;更新を組織内の広範なチームで利用できるようにする必要があります。
* **共有するアセットの量に注意を払う：**&#x200B;アセットを配布する場合、ガバナンスとセキュリティが最も重要な要素になる可能性があります。Brand Portal のように、大規模なアセット配布を想定したツールの使用を検討してください。
* **アセットのライフサイクルを理解する：**&#x200B;組織内のそれぞれのチームでアセットがどのように処理されるかを理解します。
* **アセットへの頻繁な保存を慎重に処理する：** Adobe Asset Link では、PS、AI、ID を使用して自動的に処理します。他のアプリケーションの場合は、すべての変更が DAM で必要な場合を除き、マップされたフォルダーや共有フォルダーでは WIP 状態のタスクを実行しないでください。

### [!DNL Assets]からAdobe Stockアセットにアクセス {#access-to-adobe-stock-assets-from-aem-assets}

[[!DNL Experience Manager] およびAdobe Stock](/help/assets/aem-assets-adobe-stock.md) 統合を使 [!DNL Experience Manager] 用すると、Adobe Stockからにアセットを検索、プレビュー、ライセンス取得し、保存でき [!DNL Experience Manager]ます。ライセンス取得され保存された Adobe Stock アセットには、限定された Stock メタデータが付いており、このメタデータを使用してアセットをさらに絞り込むことができます。

この統合に関するいくつかの重要な点を以下に示します。

* Adobeストックのアセットが[!DNL Experience Manager]に保存されると、アセットは通常の[!DNL Experience Manager]アセットになり、バイナリは[!DNL Experience Manager]リポジトリに保存されます。 Adobe Stockに関連する一部のメタデータは、そのアセット用に[!DNL Experience Manager]に保存されます。保存しないと、取り込みプロセスは他のファイルの場合と同じように見えます。 例えば、スマートタグがアクティブな場合、保存時にこれらのアセットにタグが追加されます。
* [!DNL Experience Manager]に保存されたアセットはコピーであり、Adobe Stockへのリンクではありません。

**[!DNL Experience Manager]Adobe Stock から Creative Cloud 内の に保存されたアセットの操作**。この統合は Adobe Asset Link とは無関係ですが、Adobe Asset Link では Stock から保存されたこれらのアセットをそのように認識し、Photoshop、Illustrator、InDesign の Adobe Asset Link 拡張 UI でこれらのアセットに追加のメタデータと Stock アイコンを表示します。ファイルは[!DNL Experience Manager]に保存すると通常の[!DNL Experience Manager]アセットになるので、参照や開くなどの操作が可能です。
AdobeのAsset Link拡張機能が存在するCreative Cloudアプリで作業するクリエイティブユーザーは、Adobe Stockから[!DNL Experience Manager]にライセンスが必要なアセットにアクセスできるほか、Creative Cloudライブラリパネルを使用して、Adobe Stockアセットの検索、プレビュー、ライセンス取得をおこなうこともできます。
Adobe Stockのアセットは、ライセンスが供与され[!DNL Experience Manager]に保存され、[!DNL Experience Manager] Assetsデプロイメントにアクセスする広範なチームが利用できます。一方、Creative Cloudライブラリパネルを介してAdobe Stockのクリエイティブライセンスを取得すると、Creative Cloudアカウントでのみ利用できます。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM article.
-->

## DAM へのアセットの保存について {#about-storing-assets-in-a-dam}

クリエイティブチームとマーケティング／事業部門（LOB）チームの間の効率的なワークフローをデザインし、最適なサポート機能を選択するには、アセットを DAM に保存するタイミングと理由を理解することが重要です。

### アセットを DAM に保存する理由 {#why-assets-are-stored-in-dam}

アセットを DAM に保存すると、アクセスおよび検索がしやすくなります。これにより、組織またはエコシステムの多数のユーザー（パートナー、顧客などを含む）が、アセットを活用できるようになります。

ほとんどの組織は、ダウンストリームのマーケティング/LOBプロセスに関連するアセット([!DNL Experience Manager] SitesやAdobe Experience Cloud、Advertising Cloudが提供する他のチャネル、Analytics Cloudが測定した他のチャネルに公開し、ユーザーやパートナーに提供するなど)のみを保存します。 また、レビュー／承認プロセスを受ける可能性のあるアセットも DAM に保存します。このように、DAM に保存されるアセットのほとんどは活用される可能性の高いアセットであり、活用の予定がないアセットの保存が防止されます。

また、アセットを保存する場合、技術上およびリソース使用上でも考慮すべき点があります。DAM では、保存されたアセット関連の追加サービスが用意されています（メタデータの抽出、バージョン管理、プレビュー／トランスコーディングの生成、参照の管理およびアクセス制御情報の追加など）。これらのサービスを使用すると、追加の時間リソースおよびインフラストラクチャリソースが消費されます。

多くの場合、アセットおよび更新をすべて保存することは推奨されません。例えば、特定のアセットの更新の質が低く、大量のリソースを消費するような場合、そのアセットは DAM に保存しないようにします。

### アセットを DAM に保存するタイミング {#when-assets-are-stored-in-dam}

クリエイティブチーム（および組織）は、通常、アセットのライフサイクルのステージごとにアセットを保存しようとは考えません。例えば、以下のような場合、アセットは保存されません。

* アセットがまだ最終決定されていない、またはテストが予定されている場合
* アセットがクリエイティブ／内部チームのレビューサイクルで不合格になった場合
* 問題のアセットに比べ、外部チームへの作業の説明に、より適したアセットがある場合

通常、以下のクラスのアセットが DAM に保存されます。

* 一定の成熟度に到達し、共有する準備ができたと判断されたアセット
* クリエイティブチームが事前に選択したアセット
* マーケティング部門が使用できる、または特定の契約や合意に応じて同部門から要求された、特定の形式のアセット（例えば、RAW ファイルから変換した JPG ファイル、PSD ファイルから作成した TIFF／画像ファイルなど）

### アセットの更新を DAM に保存するタイミング {#when-updates-to-assets-are-stored-in-dam}

原則として、より広範な DAM ユーザーに関連するアセットの更新のみを DAM に保存するようにしてください。それにより、（マーケティングおよび類似の部門の）ユーザーの DAM アセットのタイムラインには、関連するバージョンのみが表示されます。

代表的な例としては、アセットのライフサイクルで主要なマイルストーンに関連する変更があります。例えば、最初のクリエイティブレディアセットや、クリエイティブチームからの要求／レビューに基づいた公式の更新などは、DAM に保存してバージョン管理する必要があります。

DAM の既存アセットに対する変更要求が出された後、マーケティングチームのレビューのためにクリエイティブチームがおこなった更新も、関連する更新の一例です。この更新は、今後の参考にしたり、以前のバージョンに戻したりするために、DAM に保存してバージョン管理する必要があります。

以下は、通常、関係がないと見なされる更新の例です。

* マーケティングレビューの準備ができる前に、アセットの最終ではないバージョンがアップロードされた場合
* アセットの準備ができたとクリエイティブチームが判断する前に、WIP フェーズのアセットにクリエイティブの変更が頻繁に加えられた場合

### DAM へのユーザーアクセス権 {#user-access-to-dam}

[!DNL Experience Manager] Assets では、 Assets デプロイメントに対するアクセス権に基づいて、2 つのタイプのユーザーがサポートされています。[!DNL Experience Manager]通常、エンタープライズネットワーク（ファイアウォール）の内側にいるユーザーは、DAM への直接アクセス権を持っています。エンタープライズネットワークの外側にいるその他のユーザーは、直接アクセス権を持っていません。このユーザータイプにより、技術的観点から、どの統合を使用できるかが決定されます。

#### DAM への直接アクセス権を持つクリエイティブユーザー {#creative-users-with-direct-access-to-dam}

通常、社内のクリエイティブチームや、社内ネットワークに  内部ネットワークに転送された場合、[!DNL Experience Manager]ログインを含むDAMインスタンスにアクセスできます。

このような場合、[!DNL Experience Manager]デスクトップアプリケーションを使用すると、最終/承認済みアセットに簡単にアクセスし、クリエイティブレディアセットをDAMに保存できます。

#### DAM へのアクセス権を持たないクリエイティブユーザー {#creative-users-without-access-to-dam}

DAM インスタンスへの直接アクセス権を持たない外部のエージェンシーやフリーランサーも、承認済みアセットにアクセスしたり、新しいデザインを DAM に追加したりする必要が生じることがあります。

そのような場合は、[!DNL Experience Manager]/Creative Cloud統合を活用して、ワークフローを改善できます。 クリエイティブユーザーは、Adobe ID を持ち、ストレージサービス付きの Creative Cloud アカウントを持っていることが前提条件です。

以下の方法で、最終／承認済みアセットへのアクセスを提供することができます。

* 多数のアセットへのアクセスを提供するには：[[!DNL Experience Manager] Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)を使用するか、[!DNL Experience Manager]パブリッシュインフラストラクチャで顧客の[アセット共有](assets-finder-editor.md)を実装します。

* 一部のアセットへのアクセスを提供するには：Adobe Creative Cloudとの[!DNL Experience Manager]フォルダー共有は、Assets Brand Portalやアセット共有に加えて、 [!DNL Experience Manager]で使用できます。 この統合には、いくつかの制限があります。詳しくは、この記事を参照してください。

### ユースケース {#use-cases}

以下の使用例は、DAM とデザイナーのデスクトップの間の様々なワークフローのタイプについて説明しています。

#### DAMのアセットを使用した新しいデザインの作成 {#creating-new-designs-using-assets-from-dam}

以下の図は、デジタルアセットのライフサイクルを示しています。クリエイティブユーザーおよび DAM ユーザー（マーケティング担当者、LOB ユーザー）が、既存アセットを活用する方法、既存アセットを使用して別のアセットを作成する方法、承認のために既存アセットを送信する方法についての説明です。

![chlimage_1-301](assets/chlimage_1-301.png)

アセットのライフサイクルには、以下のステージがあります。

1. 承認済みアセットをクリエイティブデスクトップで共有する：DAM にある最終アセットがクリエイティブユーザーのデスクトップで使用できるようになります。
1. 新しいデザイン（クリエイティブデジタルアセット）を作成する：新しいファイルが WIP 領域に保存されます。
1. 承認済みアセットを新しいデザインで使用（配置）:クリエイティブユーザーが、承認済みの既存のアセットを使用して新しいCreative Cloudを作成する
1. WIP の更新を頻繁に保存する：クリエイティブユーザーが、ファイルを繰り返し更新し、頻繁に保存します。このステージでは、クリエイティブユーザーが他者と共同作業をおこない、頻繁に更新を保存します。ただし、この更新は、  通常、DAMユーザーには関心がありません。
1. アセットは、クリエイティブレディの状態になり、クリエイティブレディフォルダーに保存されます。
1. アセットの  更新：アセットの更新または新しいファイルがDAMのユーザーに提供される
1. アセットは実稼動環境に配置されます。これはDAMプロセスで、組織に応じて、タグ付け、承認、アクセス制御の変更で構成される場合があります。 このステージでは、アセットは最終アセットと見なされ、DAM を使用している、より広範なチームが使用できるようになります。また、クリエイティブユーザーが、このアセットを使用して、別のアセットを作成することもできます。

このプロセスでアセットを管理する方法について、いくつか一般的な推奨事項があります。

* WIPファイル用の専用ストレージ領域/システム( Adobe Creative Cloud Assets同期フォルダーなど)を使用します。DAMユーザーに関連しない頻繁な更新は、[!DNL Experience Manager] Assets内ではなく、専用のシステムで処理するのが最適です。 WIPアセットは、Adobe Creative Cloudデスクトップアプリケーションを使用してローカルディスクに同期したり、ローカルストレージに保存したりできます。
* 最終アセットと DAM にアップロードするアセットには別々のフォルダー／共有を使用する：わかりやすいように、最終アセットには専用のマッピングされた／共有フォルダー（上記の例の「最終」）、DAM にアップロードして戻す予定のアセットにも専用のフォルダー（同「クリエイティブレディ」）を使用します。

#### DAMで管理されている既存のアセットの変更 {#changing-existing-assets-managed-in-dam}

場合によっては、DAM にあるアセットを変更する必要が生じることがあります。以下に例を示します。

* [!DNL Experience Manager]アセットで行われたレビューと承認のアセットの変更リクエスト
* 既存の最終アセットを大規模に更新する場合
* 既存のファイルを少し編集する場合（特にファイルが最終的に承認される前）

このような場合、[!DNL Experience Manager]デスクトップアプリケーションは、これらの操作を実行する最も簡単な方法を提供します。

![chlimage_1-302](assets/chlimage_1-302.png)

以下の図は、一連のイベントを示しています。

<!-- TBD for formatting. 
This article will get fixed automatically when 6.5 content is ported to it.
And 6.5 content will be ported after updating it for [!DNL Experience Manager] desktop app 2.0 best practices.
And it will be updated for DA2.0 best practices after 6.5 repo is available for writers to edit content in.
-->

* **1:** DAMからデスクトップにアセットを共有するか、選択したアプリケーション(Adobe Photoshopなど)のデスクトップで直接開きます。ファイルをチェックアウトしてロックすることをお勧めします。
* **2：**&#x200B;小規模な更新：ファイルを編集して変更を保存します。
* 手順 2 で考えられる別のフロー

   * **A：**&#x200B;大規模な更新：ファイルを大幅に変更する必要が生じた場合は、WIP フォルダー／領域にファイルをコピーして、時々保存してください。
   * **B：**&#x200B;作業は WIP フォルダーのファイルで続行します。保存された変更は、DAM のバージョンには同期されません。
   * **C：**&#x200B;更新が完了したら、マッピングされたフォルダーにファイルをコピーバック／保存します。

* **3：**&#x200B;アセットの更新が DAM で反映されます。ファイルをチェックインしてロックを解除します。
* **4：アセ** ットが実稼動環境に配置されます。

このプロセスでアセットを管理する方法について、いくつか一般的な推奨事項があります。

* [!DNL Experience Manager]デスクトップアプリケーションによってマッピングされたネットワーク共有から開いたファイルは、ファイルに加えた変更が小さい場合を除き、直接保存しないでください。
* さらに変更を加えたい場合は、分離された WIP フォルダーにファイルをコピーし、時々保存しながら、クリエイティブチームと共同作業をおこないます。

#### DAM への一括アップロード {#bulk-upload-to-dam}

同時に大量のファイルを DAM にアップロードする必要が生じることもあります。例えば、以下のような場合です。

* 撮影した大量の写真や 大きなプロジェクトを撮る
* クリエイティブエージェンシーから提供されたアセットのアップロード
* 大規模なアセットのセットから一部選択したアセットのアップロード（選択が DAM の外でおこなわれた場合）

これは、デスクトップユーザーの通常のワークフローの一部として、  写真撮影など)を、デスクトップユーザーのワークフローの通常の部分として使用します。 大規模なアセット移行については、ここでは説明しません。

以下の機能を活用すると、アセットを一括でアップロードすることができます。

* 大きなフォルダーや階層フォルダーをアップロードするには、[!DNL Experience Manager]デスクトップアプリケーションを使用します。このデスクトップアプリケーションでは、[フォルダーのアップロード](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app.html#bulkupload)機能を使用できます。 フォルダーの階層構造もアップロードできます。アセットはバックグラウンドでアップロードされます。そのため、アセットは Web ブラウザーのセッションに拘束されません。
* 1つのフォルダーから少数のファイルをアップロードする場合は、デスクトップからWeb UIに直接ドラッグするか、[!DNL Experience Manager] Assets Web UIの「作成」オプションを使用します。

>[!NOTE]
>
>ビジネス要件によっては、カスタムアップローダーを使用することもできます。

#### デスクトップから直接デジタルアセットを管理 {#managing-digital-assets-directly-from-desktop}

ネットワークファイル共有を使用してデジタルアセットを管理する場合、[!DNL Experience Manager]デスクトップアプリケーションでマッピングされたネットワーク共有を使用するだけで、便利な方法と見なされます。 ネットワークファイル共有から移行する際には、 [!DNL Experience Manager] Web UIには、ネットワーク共有（検索、コレクション、メタデータ、コラボレーション、プレビューなど）で可能な限り優れた豊富なデジタルアセット管理機能が用意されています。 [!DNL Experience Manager]デスクトップアプリは、

[!DNL Experience Manager]デスクトップアプリケーションを使用して[!DNL Experience Manager] Assetsのネットワーク共有でアセットを直接管理することは避けてください。 例えば、[!DNL Experience Manager]デスクトップアプリケーションを使用して複数のファイルを移動/コピーしないでください。 代わりに、 [!DNL Experience Manager] Assets Web UIを使用して、Finder/エクスプローラーからフォルダーをネットワーク共有にドラッグするか、 [!DNL Experience Manager] Assetsのフォルダーアップロード機能を使用します。

#### アセットの移行 {#asset-migration}

既存のシステムから新しいシステムへのアセットの移行や、サーバーに格納されている大量のアセットの移行を計画し実行するには、[移行ガイド](/help/assets/assets-migration-guide.md)を参照してください。[!DNL Experience Manager] Desktop App と ／Creative Cloud 統合では、そのような移行をサポートしていません。[!DNL Experience Manager]大量のアセットを取り込む必要があり、メタデータのマッピング、変換および取り込みに関する様々な要件が多数あることから、移行には別のツールとアプローチを採用することをお勧めします。

>[!MORELIKETHIS]
>
>* [Adobeアセットリンク](https://helpx.adobe.com/in/enterprise/admin-guide.html/in/enterprise/using/adobe-asset-link.ug.html)
>* [[!DNL Experience Manager] デスクトップアプリのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [[!DNL Experience Manager] Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=ja)
>* [[!DNL Experience Manager] とAdobe Stockの統合](aem-assets-adobe-stock.md)

