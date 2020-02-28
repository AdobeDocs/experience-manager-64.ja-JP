---
title: AEMとCreative cloudの統合のベストプラクティス
description: AEMデプロイメントをAdobe Creative cloudと統合し、アセット転送ワークフローを合理化し、最大限の効率を達成するためのベストプラクティス
contentOwner: AG
translation-type: tm+mt
source-git-commit: 1f44950e3e0653df61289e1bd435d13829051365

---


# AEM and Creative Cloud integration best practices {#aem-and-creative-cloud-integration-best-practices}

<!-- TBD: Reconcile with 6.5 article that's ahead of this article now in terms of content streamlining and structuring.
-->

Adobe Experience Manager Assetsは、Adobe Creative cloudと統合できるデジタルアセット管理(DAM)ソリューションで、DAMユーザーがクリエイティブチームと連携し、コンテンツ作成プロセスでのコラボレーションを合理化するのに役立ちます。

Adobe Creative Cloud は、デジタルアセットの作成を支援するソリューションとサービスのエコシステムをクリエイティブチームに提供します。これには、デスクトップおよびモバイルアプリケーション、デスクトップ同期や Web エクスペリエンスを備えたストレージなどのクラウドサービス、および Adobe Stock などのマーケットプレイスが含まれます。

ユースケースに基づいてデスクトップとエンタープライズクラスの DAM の間で選択すべき統合や、つながるワークフローに関連するベストプラクティスについては、このドキュメントで説明します。

>[!NOTE]
>
>AEMからCreative cloudへのフォルダー共有は廃止され、本ガイドでは説明しません。 Adobe recommends using newer capabilities such as [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) or [AEM desktop app](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html) to provide creative user with access to assets managed in AEM.

## Collaboration needs of creatives, marketers, and DAM users {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要件 | 使用事例   | 関係するサーフェス |
|---|---|---|
| デスクトップ上でクリエイティブプロフェッショナル向けのエクスペリエンスを簡素化する | クリエイティブプロフェッショナル（より広い意味では、ネイティブアセット作成アプリケーションで作業しているデスクトップユーザー）向けに、DAM（AEM Assets）で管理されるアセットへのアクセスを効率化します。変更の検出、使用（開く）、編集、AEM への保存のほか、新しいファイルのアップロードを容易にわかりやすくおこなえる方法が必要です。 | Windows または Mac デスクトップ、Creative Cloud アプリ |
| すぐに使用できる高品質なアセットを Adobe Stock から提供する | マーケティング担当者は、アセットの調達と検出を支援することでコンテンツ作成プロセスの促進に貢献します。クリエイティブプロフェッショナルは、承認されたアセットをクリエイティブツール内から直接使用します。 | AEM Assets、Adobe Stock マーケットプレイス、メタデータフィールド |
| 組織でアセットを配布および共有する | 社内部門／支店および外部のパートナー、ディストリビューター、代理店は、親組織で共有されている承認済みアセットを使用します。組織では、作成したアセットを安全かつシームレスに共有して幅広く再利用したいと考えています。 | Brand Portal、Asset Share Commons |

## コラボレーションニーズをサポートするアドビ製品／サービス {#adobe-offerings-to-support-the-collaboration-need}

| 関係するユーザーに対する価値提案 | アドビ製品／サービス | 関係するサーフェス |
|---|---|---|
| クリエイティブユーザーは、Creative Cloud アプリを使用したまま、AEM からアセットを検出し、それらを開いて使用したり、編集して変更を AEM にアップロードするほか、新しいファイルを AEM にアップロードします。 | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator、InDesign |
| ビジネスユーザーは、アセットを開いて使用する作業、AEMに対する変更の編集とアップロード、デスクトップ環境からAEMへの新しいファイルのアップロードを簡単に行うことができます。 汎用の統合を使用して、アドビ以外のアセットも含め、あらゆるアセットタイプをネイティブデスクトップアプリケーションで開きます。 | [AEM Desktop App](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | Windows および Mac デスクトップ上の AEM Desktop App |
| マーケティング担当者とビジネスユーザーは、AEM 内から Adobe Stock アセットの検出、プレビュー、ライセンス取得と保存、管理をおこなえます。ライセンスを取得し保存したアセットは、限定された Adobe Stock メタデータを提供してガバナンスの強化に役立ちます。 | [Experience ManagerとAdobe stockの統合](aem-assets-adobe-stock.md) | AEM Web インターフェイス |

ここでは、主に、コラボレーションニーズの最初の 2 つの側面に焦点を当てます。アセットの大規模な配布と調達については、ユースケースとして簡単に説明します。そのようなニーズに対するソリューションとしては、Adobe Brand Portal または Asset Share Commons を検討してください。[Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html)、 [Asset Share Commonsコンポーネントに基づいて構築できるソリューション、](https://adobe-marketing-cloud.github.io/asset-share-commons/) Link Share [、](/help/assets/link-sharing.md)Manager Assets Assetsを使用したリンク共有 [](/help/assets/managing-assets-touch-ui.md) 、特定の要件に基づいてレビューする必要があります。

![AEM 用の Creative Cloud 接続：使用する機能の決定](assets/creative-connections-aem.png)

<!-- 
## Terms and definitions {#terms-and-definitions}

The terms used in this document may have a different meaning in other contexts. In particular, the following terms pertaining to the digital asset lifecycle are used when referring to workflows between a creative professional's desktop and DAM:

* **Work-in-progress or creative work-in-progress (WIP):** A phase in asset lifecycle where an asset undergoes multiple changes and is typically not yet ready to be shared with broader teams.
* **Creative-ready assets:** Assets that are ready to be shared with a broader team, or have been  selected / approved  by the creative team for sharing with marketing or LOB teams.
* **Asset approvals:** The approval process that runs for assets already uploaded to DAM, which typically includes brand approvals, legal approvals, and so on.
* **Final asset:** An asset that has gone through all  approvals/metadata  tagging and is ready to be used by the broader team. Such an asset is stored in DAM and made available to all (or all interested) users. It can be used in marketing channels or by creative teams to create designs.
* **Minor asset  update/change:** A quick and small change to a digital asset. It is often made in response to a retouching or minor editing request, asset review, or approval (for example, reposition, change text size, adjust saturation/brightness, color, and so on).
* **Major asset  update/change:** A change to a digital asset that requires considerable work, and sometimes must be done over a longer period of time. It typically includes multiple changes. The asset must be saved multiple times while being updated. Major asset updates typically cause the asset to enter a WIP stage.
* **DAM:** Digital asset management. In this document, it is synonymous with AEM Experience Manager Assets, unless specifically mentioned otherwise.
* **Creative user:** A creative professional, who creates digital assets using Creative Cloud apps and services. In some cases, a creative user may be a member of a creative team who may use Creative Cloud, but does not create digital assets (like a creative director or creative team manager).
* **DAM user:** A typical user of a DAM system. Depending on the organization, a DAM user can be a marketing or a non-marketing user, for example a Line-of-Business (LOB) user, librarian, sales person, and so on.
-->

### 使用事例のマッピング

| 使用事例   | AEM デスクトップアプリケーション | フォルダー共有 | その他のソリューション |
|---|---|---|---|
| より少ない数のDAMアセットをクリエイティブユーザーと共有 | ✔✔ | ✔ |  |
| DAMアセットの数を増やしてクリエイティブユーザーと共有 | ✔✔ | ✘ | [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) <br> [アセット共有](assets-finder-editor.md) |
| DAM へのアクセス権を持っているユーザーと DAM アセットを共有する | ✔✔ | ✔ | [リンク共有](link-sharing.md) |
| DAM へのアクセス権を持っていないユーザーと DAM アセットを共有する | ✘ | ✔✔ | [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) <br> [アセット共有](assets-finder-editor.md) |
| 少数／小さいボリュームのアセットを DAM に保存する | ✔✔ | ✔ | [Web UI によるアップロード](managing-assets-touch-ui.md) |
| DAMへの大量のアセットの保存(3) | ✔✔ | ✘ | [Web UI によるアップロード](managing-assets-touch-ui.md) <br> Custom script / tool |
| DAM へ膨大な量のアセットを移行する | ✘ | ✘ | [移行ガイド](assets-migration-guide.md) |
| デスクトップですばやくアセットを開く | ✔✔ | ✘ |  |
| デスクトップですばやくアセットを開いて変更する | ✔✔ | ✘ |  |

記号の凡例：

* ✔✔：推奨されるソリューション
* ✔：許容されるソリューション
* ✘：この例に使用してはならない

補足：

* (1)少ない資産数：例えば、プロジェクトやキャンペーンに関連するアセットの小さなセット
* (2)資産数の増加例えば、組織内のすべての承認済みアセット
* (3)AEMデスクトップアプリのアップロードフォルダー機能の使用

アセット配布ユースケースをサポートするには、他のソリューションを考慮に入れる必要があります。

* [Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) for a configurable, saaS add-on to AEM Assets to publish assets.
* カスタムソリューションは [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) のコードベースに基づいて作成される。
* AEM [リンク共有](/help/assets/link-sharing.md)：リンクを使用してアドホックでアセットを共有する。
* [AEM Assets Web インターフェイス](/help/assets/managing-assets-touch-ui.md)：外部ユーザーが AEM にアクセスできるようにする、アクセスAEM アクセス制御の設定で保護されている外部関係者向けのエリア。必要な IT／ネットワーク設定の調整機能が備わっている。

## 主な概念とユースケース {#key-concepts-and-use-cases}

### よく使用される用語 {#glossary-of-common-terms}

* **作業中（WIP）またはクリエイティブ WIP：**&#x200B;アセットライフサイクルのフェーズ。アセットに対してまだ複数の変更がおこなわれている最中であり、通常は、より広範なチームと共有するための準備がまだできていない状態。
* **クリエイティブレディアセット：**&#x200B;様々なチームと共有する準備ができているアセット、またはクリエイティブチームがマーケティングチームや LOB チームとの共有用に選択／承認したアセット。
* **アセット承認：** 既に DAM にアップロードされているアセットに対して実行される承認プロセス。通常、ブランド承認および法的承認などが含まれます。
* **最終アセット：**&#x200B;すべての承認／メタデータのタグ付けを経て、幅広いチームが使用できる状態にあるアセット。このようなアセットは DAM に保存され、すべてのユーザー（またはすべての関係者）が使用できるようになっています。マーケティングチャネルで使用したり、クリエイティブチームがデザインの作成に使用したりできます。
* **アセットの小規模な更新／変更：**&#x200B;デジタルアセットに対する迅速で小規模な変更。多くの場合、リタッチ作業や小規模な編集の要求、アセットレビューまたは承認に対応するためにおこなわれます（例えば、再配置、テキストサイズの変更、彩度／明るさ、色などの調整）。
* **アセットの大規模な更新／変更：**&#x200B;デジタルアセットに加えられる、大規模な作業が必要な変更。その変更作業は比較的長期にわたる場合もあります。通常は複数の変更が含まれます。アセットは、更新中、複数回保存する必要があります。アセットの大規模な更新により、ほとんどの場合、アセットのステージは WIP になります。
* **DAM：**&#x200B;デジタルアセット管理。このドキュメントでは、特に断りのない限り、AEM Experience Manager Assets と同義です。
* **クリエイティブユーザー：** Creative Cloud のアプリケーションとサービスを使用してデジタルアセットを作成するクリエイティブプロフェッショナル。クリエイティブチームに所属し、Creative Cloud を使用するが、デジタルアセットの作成はおこなわないメンバー（クリエイティブディレクターやクリエイティブチームマネージャーなど）を含む場合もあります。
* **DAM ユーザー：** DAM システムの一般的な利用者。組織によっては、DAM ユーザーにマーケティング分野のユーザーもマーケティング以外の分野のユーザーも含まれます（例えば、事業部門（LOB）ユーザー、ライブラリアン、販売担当者など）。

### AEMとCreative cloudの統合を使用する場合の考慮事項 {#considerations-when-using-aem-and-creative-cloud-integration}

* See [desktop app best practices](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* 「 [Adobe stockの統合」を参照](aem-assets-adobe-stock.md)
* See [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

Experience ManagerとCreative cloudの統合に関するベストプラクティスの概要を示します。 以下のそれぞれの項目の詳細は、このドキュメントで後述されています。

* **Photoshop、InDesign、Illustrator のいずれかで作業しているクリエイティブユーザーの場合：** Adobe Asset Link は、AEM からチェックアウトされたアセットの更新の適切な処理など、最適なユーザーエクスペリエンスを提供します。
* **任意の汎用ファイル形式またはアプリケーションについてデスクトップからアセットへのアクセスを簡素化する場合：** AEM Desktop App を使用します。
* **アセットを DAM に保存する理由とタイミングを理解する：**&#x200B;更新を組織内の広範なチームで利用できるようにする必要があります。
* **共有するアセットの量に注意を払う：**&#x200B;アセットを配布する場合、ガバナンスとセキュリティが最も重要な要素になる可能性があります。Brand Portal のように、大規模なアセット配布を想定したツールの使用を検討してください。
* **アセットのライフサイクルを理解する：**&#x200B;組織内のそれぞれのチームでアセットがどのように処理されるかを理解します。
* **アセットへの頻繁な保存を慎重に処理する：** Adobe Asset Link では、PS、AI、ID を使用して自動的に処理します。他のアプリケーションの場合は、すべての変更が DAM で必要な場合を除き、マップされたフォルダーや共有フォルダーでは WIP 状態のタスクを実行しないでください。

### AEM Assets からの Adobe Stock アセットへのアクセス {#access-to-adobe-stock-assets-from-aem-assets}

[AEMとAdobe stockの統合により](/help/assets/aem-assets-adobe-stock.md) 、AEMユーザーは、Adobe stockからAEMにアセットを検索、プレビュー、ライセンス認証および保存できます。 ライセンスを取得して保存したAdobe Stockアセットでは、選択したStockメタデータが使用され、追加のフィルターでアセットを検索するために使用できます。

この統合に関するいくつかの重要な点を以下に示します。

* Adobe Stock 内のアセットが AEM に保存されると、それらは通常の AEM Assets になり、バイナリが AEM リポジトリに保存されます。Adobe Stock に関係する一部のメタデータが AEM 内のアセットに保存されます。その他の点では、取り込みプロセスは他のあらゆるファイルの場合と同様です。例えば、スマートタグがアクティブな場合、保存時にこれらのアセットにタグが追加されます。
* AEM に保存されたアセットはコピーであり、Adobe Stock へのリンクではありません。

**Adobe Stock から Creative Cloud 内の AEM に保存されたアセットの操作**。この統合は Adobe Asset Link とは無関係ですが、Adobe Asset Link では Stock から保存されたこれらのアセットをそのように認識し、Photoshop、Illustrator、InDesign の Adobe Asset Link 拡張 UI でこれらのアセットに追加のメタデータと Stock アイコンを表示します。AEM に保存すると通常の AEM アセットになるので、ファイルを閲覧したり開いたりすることができます。Adobe Asset Link 拡張機能を備えた Creative Cloud アプリで作業している クリエイティブユーザーは、Adobe Stock から AEM に保存したライセンス取得済みアセットにアクセスできるだけでなく、Creative Cloud ライブラリパネルを使用して Adobe Stock アセットを検索、プレビューし、ライセンスを取得することもできます。Adobe Stock からライセンスを取得してAEM に保存したアセットは、AEM Assets デプロイメントにアクセスする広範なチームで利用できるようになります。ただし、.クリエイティブユーザーが Creative Cloud ライブラリパネル経由で Adobe Stock からアセットのライセンスを取得した場合、デフォルトでは、それらのアセットは自分の Creative Cloud アカウント内でしか使用できません。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM article.
-->

## DAMへのアセットの保存について {#about-storing-assets-in-a-dam}

クリエイティブチームとマーケティング／事業部門（LOB）チームの間の効率的なワークフローをデザインし、最適なサポート機能を選択するには、アセットを DAM に保存するタイミングと理由を理解することが重要です。

### アセットを DAM に保存する理由 {#why-assets-are-stored-in-dam}

アセットを DAM に保存すると、アクセスおよび検索がしやすくなります。これにより、組織またはエコシステムの多数のユーザー（パートナー、顧客などを含む）が、アセットを活用できるようになります。

ほとんどの組織では、ダウンストリームマーケティング／LOB プロセスに関連するアセットのみを保存するようにしています（例えば、AEM Sites 経由での Web チャネルのようなチャネルへの公開、Adobe Experience Cloud（Marketing Cloud、Advertizing Cloud）により提供され、Analytics Cloud により測定される他のチャネルへの公開、ユーザー／パートナーへの提供などのプロセス）。また、レビュー／承認プロセスを受ける可能性のあるアセットも DAM に保存します。このように、DAM に保存されるアセットのほとんどは活用される可能性の高いアセットであり、活用の予定がないアセットの保存が防止されます。

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

AEM Assets では、AEM Assets デプロイメントに対するアクセス権に基づいて、2 つのタイプのユーザーがサポートされています。通常、エンタープライズネットワーク（ファイアウォール）の内側にいるユーザーは、DAM への直接アクセス権を持っています。エンタープライズネットワークの外側にいるその他のユーザーは、直接アクセス権を持っていません。このユーザータイプにより、技術的観点から、どの統合を使用できるかが決定されます。

#### DAM への直接アクセス権を持つクリエイティブユーザー {#creative-users-with-direct-access-to-dam}

通常、社内ネットワークに接続されている社内のクリエイティブチームまたはエージェンシー/クリエイティブプロフェッショナルは、AEMログインを含むDAMインスタンスにアクセスできます。

そのような場合、AEMデスクトップアプリケーションは、最終的な/承認済みのアセットに簡単にアクセスでき、クリエイティブなアセットをDAMに保存できます。

#### DAM へのアクセス権を持たないクリエイティブユーザー {#creative-users-without-access-to-dam}

DAM インスタンスへの直接アクセス権を持たない外部のエージェンシーおよびフリーランサーも、承認済みアセットにアクセスしたり、新しいデザインを DAM に追加したりする必要が生じることがあります。

そのような場合は、AEM／Creative Cloud 統合を活用して、ワークフローを向上させることができます。クリエイティブユーザーは、Adobe ID を持ち、ストレージサービス付きの Creative Cloud アカウントを持っていることが前提条件です。

以下の方法で、最終／承認済みアセットへのアクセスを提供することができます。

* To provide access to a large number assets: Use [AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html), or customer’s implementation of [Asset Share](assets-finder-editor.md) on AEM publish infrastructure

* いくつかのアセットへのアクセスを提供するには：AEM Assets Brand portalまたはアセット共有に加えて、Adobe Creative cloudとのAEMフォルダー共有を使用できます。 この統合に関連するいくつかの制限があり、この記事で詳しく説明します。

### ユースケース {#use-cases}

以下の使用例は、DAM とデザイナーのデスクトップの間の様々なワークフローのタイプについて説明しています。

#### Create new designs using assets from DAM {#creating-new-designs-using-assets-from-dam}

以下の図は、デジタルアセットのライフサイクルを示しています。クリエイティブユーザーおよび DAM ユーザー（マーケティング担当者、LOB ユーザー）が、既存アセットを活用する方法、既存アセットを使用して別のアセットを作成する方法、承認のために既存アセットを送信する方法についての説明です。

![chlimage_1-301](assets/chlimage_1-301.png)

アセットのライフサイクルには、以下のステージがあります。

1. 承認済みアセットをクリエイティブデスクトップで共有する：DAM にある最終アセットがクリエイティブユーザーのデスクトップで使用できるようになります。
1. 新しいデザイン（クリエイティブデジタルアセット）を作成する：新しいファイルが WIP 領域に保存されます。
1. 承認されたアセットを新しいデザインで使用（配置）:クリエイティブユーザーは、Creative cloudアプリケーションで既に承認されたアセットを使用して新しいアセットを作成します
1. WIP の更新を頻繁に保存する：クリエイティブユーザーが、ファイルを繰り返し更新し、頻繁に保存します。このステージでは、クリエイティブユーザーが他者と共同作業をおこない、頻繁に更新を保存します。ただし、この更新は、  通常、DAMユーザーには興味がありません。
1. アセットは、クリエイティブレディの状態になり、クリエイティブレディフォルダーに保存されます。
1. アセットの  更新：DAMのユーザーがアセットの更新または新しいファイルを利用できる
1. アセットを実稼働環境に配置：これはDAMプロセスで、組織によってはタグ付け、承認、アクセス制御の変更を構成する場合があります。 このステージでは、アセットは最終アセットと見なされ、DAM を使用している、より広範なチームが使用できるようになります。また、クリエイティブユーザーが、このアセットを使用して、別のアセットを作成することもできます。

このプロセスでアセットを管理する方法について、いくつか一般的な推奨事項があります。

* Adobe Creative Cloud Assets 同期フォルダーなど WIP ファイル専用のストレージ領域／システムを使用する：DAM ユーザーに関連のない頻繁な更新は、AEM Assets 内からではなく専用のシステムで処理することをお勧めします。WIPアセットは、Adobe Creative cloudデスクトップアプリケーションを使用してローカルディスクに同期したり、ローカルストレージに保存したりできます。
* 最終アセットと DAM にアップロードするアセットには別々のフォルダー／共有を使用する：わかりやすいように、最終アセットには専用のマッピングされた／共有フォルダー（上記の例の「最終」）、DAM にアップロードして戻す予定のアセットにも専用のフォルダー（同「クリエイティブレディ」）を使用します。

#### Change existing assets managed in DAM {#changing-existing-assets-managed-in-dam}

場合によっては、DAM にあるアセットを変更する必要が生じることがあります。次のような例があります。

* AEM Assets でおこなわれたレビューおよび承認の結果、アセットを変更するよう要求があった場合
* 既存の最終アセットを大規模に更新する場合
* 既存のファイルを少し編集する場合（特にファイルが最終的に承認される前）

このような場合、AEM デスクトップアプリケーションを使用すると、これらのオペレーションを簡単に実行できます。

![chlimage_1-302](assets/chlimage_1-302.png)

以下の図は、一連のイベントを示しています。

<!-- TBD for formatting. 
This article will get fixed automatically when 6.5 content is ported to it.
And 6.5 content will be ported after updating it for AEM desktop app 2.0 best practices.
And it will be updated for DA2.0 best practices after 6.5 repo is available for writers to edit content in.
-->

* **** 1:DAMからデスクトップにアセットを共有するか、任意のアプリケーション（例えば、Adobe Photoshopなど）でデスクトップ上で直接開きます。 ファイルをチェックアウトしてロックすることをお勧めします。
* **2：**&#x200B;小規模な更新：ファイルを編集して変更を保存します。
* 手順 2 で考えられる別のフロー

   * **A：**&#x200B;大規模な更新：ファイルを大幅に変更する必要が生じた場合は、WIP フォルダー／領域にファイルをコピーして、時々保存してください。
   * **B：**&#x200B;作業は WIP フォルダーのファイルで続行します。保存された変更は、DAM のバージョンには同期されません。
   * **C：**&#x200B;更新が完了したら、マッピングされたフォルダーにファイルをコピーバック／保存します。

* **3：**&#x200B;アセットの更新が DAM で反映されます。ファイルをチェックインしてロックを解除します。
* **** 4:アセットは実稼動に移されます。

このプロセスでアセットを管理する方法について、いくつか一般的な推奨事項があります。

* ファイルの変更がごく小規模なものでない限り、AEM デスクトップアプリケーションでマッピングされたネットワーク共有から開いたファイルを直接保存しないようにしてください。
* さらに変更を加えたい場合は、分離された WIP フォルダーにファイルをコピーし、時々保存しながら、クリエイティブチームと共同作業をおこないます。

#### DAM への一括アップロード {#bulk-upload-to-dam}

同時に大量のファイルを DAM にアップロードする必要が生じることもあります。例えば、以下のような場合です。

* 撮影した大量の写真や 写真や大きなプロジェクト
* クリエイティブエージェンシーから提供されたアセットのアップロード
* 大規模なアセットのセットから一部選択したアセットのアップロード（選択が DAM の外でおこなわれた場合）

これは、デスクトップユーザーの通常のワークフローの一部として、  photoshootなど)を使用し、デスクトップユーザーのワークフローの通常の部分として使用できます。 大規模なアセット移行については、ここでは説明しません。

以下の機能を活用すると、アセットを一括でアップロードすることができます。

* To upload large/hierarchical folders, use AEM desktop app, which provides a [Folder Upload](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) feature. フォルダーの階層構造もアップロードできます。アセットはバックグラウンドでアップロードされます。そのため、アセットは Web ブラウザーのセッションに拘束されません。
* 1 つのフォルダーから少数のファイルをアップロードする場合は、デスクトップから Web UI に直接ファイルをドラッグするか、AEM Assets Web UI の「作成」オプションを使用します。

>[!NOTE]
>
>ビジネス要件に応じて、カスタムアップローダーも使用できます。

#### Manage digital assets directly from desktop {#managing-digital-assets-directly-from-desktop}

ネットワークファイル共有を使用してデジタルアセットを管理している場合、AEM デスクトップアプリケーションでマップされたネットワーク共有を使用するだけで、より便利になる可能性があります。ネットワークファイル共有から切り替える場合に忘れてならないのは、AEM Web UI では豊富なデジタルアセット管理（DAM）機能を使用できることです。ネットワーク共有で可能な機能（検索、収集、メタデータ、共同作業、プレビューなど）より多くの機能が用意されています。また、AEM デスクトップアプリケーションには、サーバー側の DAM リポジトリとデスクトップの作業を連携させることができる便利なリンクもあります。

AEM Assetsのネットワーク共有でアセットを直接管理する場合は、AEMデスクトップアプリを使用しないでください。 例えば、AEMデスクトップアプリケーションを使用して複数のファイルを移動/コピーすることは避けてください。 この場合は、AEM Assets Web UI を使用して、Finder／エクスプローラーからフォルダーをネットワーク共有にドラッグします。または、AEM Assets のフォルダーアップロード機能を使用します。

#### アセットの移行 {#asset-migration}

既存のシステムから新しいシステムへのアセットの移行や、サーバーに格納されている大量のアセットの移行を計画し実行するには、[移行ガイド](/help/assets/assets-migration-guide.md)を参照してください。AEM Desktop App と AEM／Creative Cloud 統合では、そのような移行をサポートしていません。大量のアセットを取り込む必要があり、メタデータのマッピング、変換および取り込みに関する様々な要件が多数あることから、移行には別のツールとアプローチを採用することをお勧めします。

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/in/enterprise/using/adobe-asset-link.html)
>* [AEM Desktop App ベストプラクティス](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [AEM Assets Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [AEM と Adobe Stock の統合](aem-assets-adobe-stock.md)

