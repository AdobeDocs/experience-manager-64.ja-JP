---
title: Experience Manager と Creative Cloud の統合のベストプラクティス
description: 統合のベストプラクティス [!DNL Experience Manager] Adobe Creative Cloudを使用したデプロイメントにより、アセット転送ワークフローを効率化し、効率を最大限に高める
contentOwner: AG
feature: Collaboration,Adobe Asset Link,Desktop App
role: User,Admin
exl-id: cb9bea05-3359-4fb4-b935-59e522a5f387
source-git-commit: 1679bbab6390808a1988cb6fe9b7692c3db31ae4
workflow-type: tm+mt
source-wordcount: '3488'
ht-degree: 68%

---

# [!DNL Experience Manager] および [!DNL Creative Cloud] 統合のベストプラクティス {#aem-and-creative-cloud-integration-best-practices}

<!-- TBD: Reconcile with 6.5 article that's ahead of this article now in terms of content streamlining and structuring.
-->

Adobe Experience Manager Assets は、Adobe Creative Cloud と統合できるデジタルアセット管理（DAM）ソリューションです。DAM ユーザーがクリエイティブチームと協力してコンテンツ作成プロセスでのコラボレーションを効率化できるようにサポートします。

Adobe Creative Cloud は、デジタルアセットの作成を支援するソリューションとサービスのエコシステムをクリエイティブチームに提供します。これには、デスクトップおよびモバイルアプリケーション、デスクトップ同期や Web エクスペリエンスを備えたストレージなどのクラウドサービス、および Adobe Stock などのマーケットプレイスが含まれます。

使用例に基づいてデスクトップとエンタープライズクラスの DAM の間で選択すべき統合や、つながるワークフローに関連するベストプラクティスについては、このドキュメントで説明します。

>[!NOTE]
>
>フォルダーの共有元 [!DNL Experience Manager] のCreative Cloudは廃止され、このガイドでは扱われなくなりました。 Adobeは、次のような新しい機能を使用することをお勧めします。 [Adobeアセットリンク](https://helpx.adobe.com/jp/enterprise/using/adobe-asset-link.html) または [[!DNL Experience Manager] デスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=ja) クリエイティブユーザーがで管理されるアセットにアクセスできるようにする [!DNL Experience Manager].

## クリエイティブ、マーケター、DAM ユーザーのコラボレーションニーズ {#collaboration-needs-of-creatives-marketers-and-dam-users}

| 要件 | 使用例 | 関係するサーフェス |
|---|---|---|
| デスクトップ上でクリエイティブプロフェッショナル向けのエクスペリエンスを簡素化する | クリエイティブプロフェッショナル（より広い意味では、ネイティブアセット作成アプリケーションで作業しているデスクトップユーザー）向けに、DAM（[!DNL Assets]）で管理されるアセットへのアクセスを効率化します。変更を簡単かつ簡単に見つけ、（開く）、編集して次の場所に保存する方法が必要です。 [!DNL Experience Manager]新しいファイルをアップロードします。 | Windows または Mac デスクトップ、Creative Cloud アプリ |
| すぐに使用できる高品質なアセットを Adobe Stock から提供する | マーケターは、アセットの調達と検出を支援することでコンテンツ作成プロセスの促進に貢献します。クリエイティブプロフェッショナルは、承認されたアセットをクリエイティブツール内から直接使用します。 | [!DNL Assets];Adobe Stock marketplace;メタデータフィールド |
| 組織でアセットを配布および共有する | 社内部門／支店および外部のパートナー、ディストリビューター、代理店は、親組織で共有されている承認済みアセットを使用します。組織では、作成したアセットを安全かつシームレスに共有して幅広く再利用したいと考えています。 | Brand Portal、Asset Share Commons |

## コラボレーションニーズをサポートするアドビ製品／サービス {#adobe-offerings-to-support-the-collaboration-need}

| 関係するユーザーに対する価値提案 | アドビ製品／サービス | 関係するサーフェス |
|---|---|---|
| クリエイティブユーザーがからアセットを検出する [!DNL Experience Manager]、開いて使用する、変更を編集し、次の場所にアップロードする、 [!DNL Experience Manager]、新しいファイルをにアップロードする [!DNL Experience Manager](Creative Cloudアプリを終了せず ) | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Photoshop、Illustrator、InDesign |
| ビジネスユーザーは、アセットのオープンと使用、編集と [!DNL Experience Manager] への変更内容のアップロード、[!DNL Experience Manager] への新しいファイルのアップロードをデスクトップ環境から簡単に行えます。汎用の統合を使用して、アドビ以外のアセットも含め、あらゆるアセットタイプをネイティブデスクトップアプリケーションで開きます。 | [[!DNL Experience Manager] デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja) | [!DNL Experience Manager]Windows および Mac デスクトップ上の デスクトップアプリケーション |
| マーケターとビジネスユーザーは、内からAdobe Stockアセットを検出、プレビュー、ライセンス、保存および管理します。 [!DNL Experience Manager]. ライセンスを取得し保存したアセットは、限定された Adobe Stock メタデータを提供してガバナンスの強化に役立ちます。 | [Adobe Experience Manager と Adobe Stock との連携](aem-assets-adobe-stock.md) | [!DNL Experience Manager] Web インターフェイス |

ここでは、主に、コラボレーションニーズの最初の 2 つの側面に焦点を当てます。アセットの大規模な配布と調達については、使用例として簡単に説明します。そのようなニーズに対するソリューションとしては、Adobe Brand Portal または Asset Share Commons を検討してください。代替ソリューション（[ Brand Portal](https://helpx.adobe.com/jp/experience-manager/brand-portal/user-guide.html)、[Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) コンポーネントに基づいて構築できるソリューション、[リンク共有](/help/assets/link-sharing.md)、[Experience Manager Assets ](/help/assets/managing-assets-touch-ui.md) の使用など）については、それぞれ固有の要件に基づいた検討が必要です。

![Creative Cloud接続 [!DNL Experience Manager]:使用する機能の決定](assets/creative-connections-aem.png)

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

### ユースケースのマッピング

| 使用例 | [!DNL Experience Manager] デスクトップアプリケーション | フォルダーの共有 | その他のソリューション |
|---|---|---|---|
| 少数の DAM アセットをクリエイティブユーザーと共有する | ✔✔ | ✔ |  |
| 多数の DAM アセットをクリエイティブユーザーと共有する | ✔✔ | ✘ | [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=ja) <br> [アセット共有](assets-finder-editor.md) |
| DAM へのアクセス権を持っているユーザーと DAM アセットを共有する | ✔✔ | ✔ | [リンク共有](link-sharing.md) |
| DAM へのアクセス権を持っていないユーザーと DAM アセットを共有する | ✘ | ✔✔ | [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) <br> [アセット共有](assets-finder-editor.md) |
| 少数／小さいボリュームのアセットを DAM に保存する | ✔✔ | ✔ | [Web UI によるアップロード](managing-assets-touch-ui.md) |
| 多数のアセットを DAM に保存する (3) | ✔✔ | ✘ | [Web UI によるアップロード](managing-assets-touch-ui.md) <br> カスタムスクリプト/ツール |
| DAM へ膨大な量のアセットを移行する | ✘ | ✘ | [移行ガイド](assets-migration-guide.md) |
| デスクトップですばやくアセットを開く | ✔✔ | ✘ |  |
| デスクトップですばやくアセットを開いて変更する | ✔✔ | ✘ |  |

シンボルの凡例：

* ✔✔：推奨されるソリューション
* ✔：許容されるソリューション
* ✘：この例に使用してはならない

補足：

* (1) 少ない資産数例えば、プロジェクトやキャンペーンに関連するアセットの小さなセットなどです
* (2) 多数の資産例えば、組織内の承認済みアセットのすべてについて
* (3) 用途 [!DNL Experience Manager] デスクトップアプリケーションのアップロードフォルダー機能

アセット配布使用例をサポートするには、他のソリューションを考慮に入れる必要があります。

* [Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) 設定可能な SaaS アドオンの場合は [!DNL Experience Manager] アセットを公開するためのアセット。
* カスタムソリューションは [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) のコードベースに基づいて作成される。
* [!DNL Experience Manager][ リンク共有](/help/assets/link-sharing.md)：リンクを使用してアドホックでアセットを共有する。
* [[!DNL Experience Manager] Assets Web インターフェイス](/help/assets/managing-assets-touch-ui.md) 外部の当事者が保護する領域を持つ [!DNL Experience Manager] アクセス制御の設定と必要な IT/ネットワーク構成の調整を行い、外部ユーザーが [!DNL Experience Manager].

## 主な概念と使用例 {#key-concepts-and-use-cases}

### よく使用される用語 {#glossary-of-common-terms}

* **作業中（WIP）またはクリエイティブ WIP：**&#x200B;アセットライフサイクルのフェーズ。アセットに対してまだ複数の変更が行われている最中であり、通常は、より広範なチームと共有するための準備がまだできていない状態。
* **クリエイティブレディアセット：**&#x200B;より広範なチームと共有するための準備ができているアセット。または、マーケティングチームもしくは LOB チームと共有するためにクリエイティブチームによって選択／承認されているアセット。
* **アセット承認：** 既に DAM にアップロードされているアセットに対して実行される承認プロセス。通常、ブランド承認および法的承認などが含まれます。
* **最終アセット：**&#x200B;すべての承認／メタデータタグ付けが完了し、より広範なチームに使用される準備ができているアセット。このようなアセットは DAM に保存され、すべてのユーザー（またはすべての関係者）が使用できるようになっています。マーケティングチャネルで使用したり、クリエイティブチームがデザインの作成に使用したりできます。
* **アセットの小規模な更新／変更：**&#x200B;デジタルアセットに対する迅速で小規模な変更。多くの場合、リタッチ作業や小規模な編集の要求、アセットレビューまたは承認に対応するために行われます（例えば、再配置、テキストサイズの変更、彩度／明るさ、色などの調整）。
* **アセットの大規模な更新／変更：**&#x200B;デジタルアセットに加えられる、大規模な作業が必要な変更。その変更作業は比較的長期にわたる場合もあります。通常は複数の変更が含まれます。アセットは、更新中、複数回保存する必要があります。アセットの大規模な更新により、ほとんどの場合、アセットのステージは WIP になります。
* **DAM：**&#x200B;デジタルアセット管理。このドキュメントでは、 [!DNL Experience Manager Assets]（特に断りのない限り）
* **クリエイティブユーザー：** Creative Cloud のアプリケーションとサービスを使用してデジタルアセットを作成するクリエイティブプロフェッショナル。クリエイティブチームに所属し、Creative Cloud を使用するが、デジタルアセットの作成は行わないメンバー（クリエイティブディレクターやクリエイティブチームマネージャーなど）を含む場合もあります。
* **DAM ユーザー：** DAM システムの一般的な利用者。組織によっては、マーケティング分野のユーザーもマーケティング以外の分野のユーザーも含まれます（例えば、事業部門（LOB）ユーザー、ライブラリアン、販売担当者など）。

### 使用時の考慮事項 [!DNL Experience Manager] とCreative Cloudの統合 {#considerations-when-using-aem-and-creative-cloud-integration}

* 詳しくは、 [デスクトップアプリケーションのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* 詳しくは、 [Adobe Stock統合](aem-assets-adobe-stock.md)
* 詳しくは、 [Adobeアセットリンク](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)

これは、Experience ManagerとCreative Cloudの統合に関するベストプラクティスの概要です。 以下のそれぞれの項目の詳細は、このドキュメントで後述されています。

* **Photoshop、InDesign、Illustrator のいずれかで作業しているクリエイティブユーザーの場合：** Adobe Asset Link は、 からチェックアウトされたアセットの更新の適切な処理など、最適なユーザーエクスペリエンスを提供します。[!DNL Experience Manager]
* **任意の汎用ファイル形式またはアプリケーションについてデスクトップからアセットへのアクセスを簡素化する場合：**[!DNL Experience Manager] デスクトップアプリケーションを使用します。
* **アセットを DAM に保存する理由とタイミングを理解する：**&#x200B;更新を組織内の広範なチームで利用できるようにする必要があります。
* **共有するアセットの量に注意を払う：**&#x200B;アセットを配布する場合、ガバナンスとセキュリティが最も重要な要素になる可能性があります。Brand Portal のように、大規模なアセット配布を想定したツールの使用を検討してください。
* **アセットのライフサイクルを理解する：**&#x200B;組織内のそれぞれのチームでアセットがどのように処理されるかを理解します。
* **アセットへの頻繁な保存を慎重に処理する：** Adobe Asset Link では、PS、AI、ID を使用して自動的に処理します。他のアプリケーションの場合は、すべての変更が DAM で必要な場合を除き、マップされたフォルダーや共有フォルダーでは WIP 状態のタスクを実行しないでください。

### からAdobe Stock Assets にアクセス [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[[!DNL Experience Manager] とAdobe Stockの統合](/help/assets/aem-assets-adobe-stock.md) 提供 [!DNL Experience Manager] アセットをAdobe Stockからに検索、プレビュー、ライセンス、保存できるユーザー [!DNL Experience Manager]. ライセンス取得され保存された Adobe Stock アセットには、限定された Stock メタデータが付いており、このメタデータを使用してアセットをさらに絞り込むことができます。

この統合に関するいくつかの重要な点を以下に示します。

* Adobe在庫のアセットをに保存するとき [!DNL Experience Manager]、通常の [!DNL Experience Manager] アセット（にバイナリを保存） [!DNL Experience Manager] リポジトリ。 Adobe Stockに関連する一部のメタデータは、 [!DNL Experience Manager]を使用しない場合、取り込みプロセスは他のファイルの場合と同じように表示されます。 例えば、スマートタグがアクティブな場合、保存時にこれらのアセットにタグが追加されます。
* 保存先のアセット [!DNL Experience Manager] はコピーであり、Adobe Stockへのリンクではありません。

**[!DNL Experience Manager]Adobe Stock から Creative Cloud 内の に保存されたアセットの操作**。この統合は Adobe Asset Link とは無関係ですが、Adobe Asset Link では Stock から保存されたこれらのアセットをそのように認識し、Photoshop、Illustrator、InDesign の Adobe Asset Link 拡張 UI でこれらのアセットに追加のメタデータと Stock アイコンを表示します。ファイルは通常のものなので、閲覧や開きなどに使用できます [!DNL Experience Manager] に保存したアセット [!DNL Experience Manager].
Adobeの Asset Link 拡張機能が存在するCreative Cloudアプリで作業するクリエイティブユーザー。また、Adobe Stockからにライセンス済みのアセットにアクセスできる [!DNL Experience Manager]を使用すると、Creative Cloudライブラリパネルを使用して、Adobe Stockアセットの検索、プレビュー、ライセンス取得をおこなうこともできます。
ライセンスを取得してに保存されたAdobe Stockのアセット [!DNL Experience Manager] ～へのアクセスを広範なチームが利用できるようになる [!DNL Experience Manager] Assets のデプロイメントに加えて、Creative Cloudライブラリパネルを使用してAdobe Stockのクリエイティブライセンスアセットを自分で使用する場合は、デフォルトでCreative Cloudアカウントでのみ使用できます。

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM article.
-->

## DAM へのアセットの保存について {#about-storing-assets-in-a-dam}

クリエイティブチームとマーケティング／事業部門（LOB）チームの間の効率的なワークフローをデザインし、最適なサポート機能を選択するには、アセットを DAM に保存するタイミングと理由を理解することが重要です。

### アセットを DAM に保存する理由 {#why-assets-are-stored-in-dam}

アセットを DAM に保存すると、アクセスおよび検索がしやすくなります。これにより、組織またはエコシステムの多数のユーザー（パートナー、顧客などを含む）が、アセットを活用できるようになります。

ほとんどの組織は、（を介して Web チャネルなどのチャネルに公開する）ダウンストリームマーケティング/LOB プロセスに関連するアセットのみを保存するように選択しています [!DNL Experience Manager] Adobe Experience Cloud、Advertising Cloudが提供し、Analytics Cloudが測定し、ユーザーやパートナーに提供するサイトやその他のチャネル。 また、レビュー／承認プロセスを受ける可能性のあるアセットも DAM に保存します。このように、DAM に保存されるアセットのほとんどは活用される可能性の高いアセットであり、活用の予定がないアセットの保存が防止されます。

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

DAM の既存アセットに対する変更要求が出された後、マーケティングチームのレビューのためにクリエイティブチームが行った更新も、関連する更新の一例です。この更新は、今後の参考にしたり、以前のバージョンに戻したりするために、DAM に保存してバージョン管理する必要があります。

以下は、通常、関係がないと見なされる更新の例です。

* マーケティングレビューの準備ができる前に、アセットの最終ではないバージョンがアップロードされた場合
* アセットの準備ができたとクリエイティブチームが判断する前に、WIP フェーズのアセットにクリエイティブの変更が頻繁に加えられた場合

### DAM へのユーザーアクセス権 {#user-access-to-dam}

[!DNL Experience Manager] Assets では、 Assets デプロイメントに対するアクセス権に基づいて、2 つのタイプのユーザーがサポートされています。[!DNL Experience Manager]通常、エンタープライズネットワーク（ファイアウォール）の内側にいるユーザーは、DAM への直接アクセス権を持っています。エンタープライズネットワークの外側にいるその他のユーザーは、直接アクセス権を持っていません。このユーザータイプにより、技術的観点から、どの統合を使用できるかが決定されます。

#### DAM への直接アクセス権を持つクリエイティブユーザー {#creative-users-with-direct-access-to-dam}

通常、社内のクリエイティブチームや、社内ネットワークに  内部ネットワークに転送された場合、を含め、DAM インスタンスにアクセスできます [!DNL Experience Manager] ログインします。

この場合、 [!DNL Experience Manager] デスクトップアプリケーションを使用すると、最終/承認済みアセットに簡単にアクセスし、クリエイティブレディアセットを DAM に保存することができます。

#### DAM へのアクセス権を持たないクリエイティブユーザー {#creative-users-without-access-to-dam}

DAM インスタンスへの直接アクセス権を持たない外部のエージェンシーやフリーランサーも、承認済みアセットにアクセスしたり、新しいデザインを DAM に追加したりする必要が生じることがあります。

その場合、 [!DNL Experience Manager]/Creative Cloudの統合により、ワークフローが改善されました。 クリエイティブユーザーは、Adobe ID を持ち、ストレージサービス付きの Creative Cloud アカウントを持っていることが前提条件です。

以下の方法で、最終／承認済みアセットへのアクセスを提供することができます。

* 多数のアセットへのアクセスを提供するには：用途 [[!DNL Experience Manager] Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html)またはのお客様の実装 [アセット共有](assets-finder-editor.md) オン [!DNL Experience Manager] パブリッシュインフラストラクチャ

* 一部のアセットへのアクセスを提供するには： [!DNL Experience Manager] Adobe Creative Cloudとのフォルダー共有は、 [!DNL Experience Manager] Assets Brand Portalまたはアセット共有。 この統合にはいくつかの制限があり、この記事で詳しく説明します。

### ユースケース {#use-cases}

以下の使用例は、DAM とデザイナーのデスクトップの間の様々なワークフローのタイプについて説明しています。

#### DAM のアセットを使用した新しいデザインの作成 {#creating-new-designs-using-assets-from-dam}

以下の図は、デジタルアセットのライフサイクルを示しています。クリエイティブユーザーおよび DAM ユーザー（マーケティング担当者、LOB ユーザー）が、既存アセットを活用する方法、既存アセットを使用して別のアセットを作成する方法、承認のために既存アセットを送信する方法についての説明です。

![chlimage_1-301](assets/chlimage_1-301.png)

アセットのライフサイクルには、以下のステージがあります。

1. 承認済みアセットをクリエイティブデスクトップで共有する：DAM にある最終アセットがクリエイティブユーザーのデスクトップで使用できるようになります。
1. 新しいデザイン（クリエイティブデジタルアセット）を作成する：新しいファイルが WIP 領域に保存されます。
1. 承認されたアセットを新しいデザインで使用（配置）:クリエイティブユーザーが、アセットアプリ内の既存の承認済みアセットを使用して新しいCreative Cloudを生成する
1. WIP の更新を頻繁に保存する：クリエイティブユーザーが、ファイルを繰り返し更新し、頻繁に保存します。このステージでは、クリエイティブユーザーが他者と共同作業をおこない、頻繁に更新を保存します。ただし、この更新は、  通常、DAM ユーザーに対しては関心がありません。
1. アセットは、クリエイティブレディの状態になり、クリエイティブレディフォルダーに保存されます。
1. アセットの  更新：DAM のユーザーは、アセットの更新または新しいファイルを使用できます
1. アセットは実稼動環境に配置されます：これは DAM プロセスで、組織に応じて、タグ付け、承認、アクセス制御の変更で構成される場合があります。 このステージでは、アセットは最終アセットと見なされ、DAM を使用している、より広範なチームが使用できるようになります。また、クリエイティブユーザーが、このアセットを使用して、別のアセットを作成することもできます。

このプロセスでアセットを管理する方法について、いくつか一般的な推奨事項があります。

* WIP ファイル用の専用ストレージ領域/システム ( Adobe Creative Cloud Assets 同期フォルダーなど ) を使用します。DAM ユーザーに関連しない頻繁な更新は、内からではなく、専用のシステムで処理するのが最適です [!DNL Experience Manager] アセット。 WIP アセットは、Adobe Creative Cloudデスクトップアプリケーションを使用してローカルディスクに同期したり、ローカルストレージに保存したりできます。
* 最終アセットと DAM にアップロードするアセットには別々のフォルダー／共有を使用する：わかりやすいように、最終アセットには専用のマッピングされた／共有フォルダー（上記の例の「最終」）、DAM にアップロードして戻す予定のアセットにも専用のフォルダー（同「クリエイティブレディ」）を使用します。

#### DAM で管理されている既存のアセットの変更 {#changing-existing-assets-managed-in-dam}

場合によっては、DAM にあるアセットを変更する必要が生じることがあります。以下に例を示します。

* でおこなわれたレビューおよび承認からのアセットの変更リクエスト [!DNL Experience Manager] Assets
* 既存の最終アセットを大規模に更新する場合
* 既存のファイルを少し編集する場合（特にファイルが最終的に承認される前）

この場合、 [!DNL Experience Manager] デスクトップアプリケーションを使用すると、これらの操作を最も簡単に実行できます。

![chlimage_1-302](assets/chlimage_1-302.png)

以下の図は、一連のイベントを示しています。

<!-- TBD for formatting. 
This article will get fixed automatically when 6.5 content is ported to it.
And 6.5 content will be ported after updating it for [!DNL Experience Manager] desktop app 2.0 best practices.
And it will be updated for DA2.0 best practices after 6.5 repo is available for writers to edit content in.
-->

* **1:** DAM からデスクトップにアセットを共有するか、選択したデスクトップ (Adobe Photoshopなど ) で直接開きます。 ファイルをチェックアウトしてロックすることをお勧めします。
* **2：**&#x200B;小規模な更新：ファイルを編集して変更を保存します。
* 手順 2 で考えられる別のフロー

   * **A：**&#x200B;大規模な更新：ファイルを大幅に変更する必要が生じた場合は、WIP フォルダー／領域にファイルをコピーして、時々保存してください。
   * **B：**&#x200B;作業は WIP フォルダーのファイルで続行します。保存された変更は、DAM のバージョンには同期されません。
   * **C：**&#x200B;更新が完了したら、マッピングされたフォルダーにファイルをコピーバック／保存します。

* **3：**&#x200B;アセットの更新が DAM で反映されます。ファイルをチェックインしてロックを解除します。
* **4:** アセットは実稼動環境に配置されます。

このプロセスでアセットを管理する方法について、いくつか一般的な推奨事項があります。

* 開いたファイルを、 [!DNL Experience Manager] デスクトップアプリケーションに適用されます（ファイルに加えた変更が小さい場合を除く）。
* さらに変更を加えたい場合は、分離された WIP フォルダーにファイルをコピーし、時々保存しながら、クリエイティブチームと共同作業をおこないます。

#### DAM への一括アップロード {#bulk-upload-to-dam}

同時に大量のファイルを DAM にアップロードする必要が生じることもあります。例えば、以下のような場合です。

* 撮影した大量の写真や 大規模なプロジェクトの撮影
* クリエイティブエージェンシーから提供されたアセットのアップロード
* 大規模なアセットのセットから一部選択したアセットのアップロード（選択が DAM の外でおこなわれた場合）

これは、デスクトップユーザーの通常のワークフローの一部として、  写真撮影など ) を、デスクトップユーザーのワークフローの通常の部分として追加します。 大規模なアセット移行については、ここでは説明しません。

以下の機能を活用すると、アセットを一括でアップロードすることができます。

* 大きなフォルダーや階層フォルダーをアップロードするには、 [!DNL Experience Manager] デスクトップアプリケーション。 [フォルダーのアップロード](https://helpx.adobe.com/jp/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) 機能。 フォルダーの階層構造もアップロードできます。アセットはバックグラウンドでアップロードされます。そのため、アセットは Web ブラウザーのセッションに拘束されません。
* 1 つのフォルダーからいくつかのファイルをアップロードする場合は、ファイルをデスクトップから直接 Web UI にドラッグするか、 [!DNL Experience Manager] アセット Web UI

>[!NOTE]
>
>ビジネス要件によっては、カスタムアップローダーを使用することもできます。

#### デスクトップから直接デジタルアセットを管理 {#managing-digital-assets-directly-from-desktop}

ネットワークファイル共有を使用してデジタルアセットを管理する場合は、 [!DNL Experience Manager] デスクトップアプリケーションは、便利な代替ツールと見なすことができます。 ネットワークファイル共有から移行する場合は、 [!DNL Experience Manager] Web UI には、ネットワーク共有（検索、コレクション、メタデータ、コラボレーション、プレビューなど）で可能な限り多くのデジタルアセット管理機能の豊富なセットが用意されています。 [!DNL Experience Manager] デスクトップアプリケーションは、デスクトップ上の作業とサーバー側の DAM リポジトリーを接続するための便利なリンクを提供します。

を使用しない [!DNL Experience Manager] のネットワーク共有でアセットを直接管理するデスクトップアプリケーション [!DNL Experience Manager] アセット。 例えば、 [!DNL Experience Manager] 複数のファイルを移動またはコピーするデスクトップアプリケーション。 代わりに、 [!DNL Experience Manager] フォルダーを Finder/エクスプローラーからネットワーク共有にドラッグするアセット Web UI、または [!DNL Experience Manager] アセットフォルダーのアップロード機能。

#### アセットの移行 {#asset-migration}

既存のシステムから新しいシステムへのアセットの移行や、サーバーに格納されている大量のアセットの移行を計画し実行するには、[移行ガイド](/help/assets/assets-migration-guide.md)を参照してください。[!DNL Experience Manager] Desktop App と ／Creative Cloud 統合では、そのような移行をサポートしていません。[!DNL Experience Manager]大量のアセットを取り込む必要があり、メタデータのマッピング、変換および取り込みに関する様々な要件が多数あることから、移行には別のツールとアプローチを採用することをお勧めします。

>[!MORELIKETHIS]
>
>* [Adobeアセットリンク](https://helpx.adobe.com/in/enterprise/admin-guide.html/in/enterprise/using/adobe-asset-link.ug.html)
>* [[!DNL Experience Manager] デスクトップアプリケーションのベストプラクティス](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [[!DNL Experience Manager] Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=ja)
>* [[!DNL Experience Manager] とAdobe Stockの統合](aem-assets-adobe-stock.md)

