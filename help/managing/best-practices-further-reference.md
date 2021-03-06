---
title: チェックリスト - 詳細情報
seo-title: The Checklist - Further Reference
description: 「プロジェクトの管理 - ベストプラクティスチェックリスト」で扱ったドキュメントや原則を拡張および補足する詳細情報について学習します。
seo-description: Learn about further details that elaborate on and/or augment the documents and principles covered by the Managing Projects - Best Practices Checklist.
uuid: 58a8b4ab-e447-4a12-b9e9-4cd3db11e06a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/MANAGING
topic-tags: managing-checklist
content-type: reference
discoiquuid: 6fc2751e-f42a-4519-bc8c-695057f21b69
exl-id: d561bb0a-352f-4be2-95ed-32dd1e2b4019
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '3741'
ht-degree: 100%

---

# チェックリスト - 詳細情報{#the-checklist-further-reference}

このページでは、[プロジェクトの管理 - ベストプラクティスチェックリスト](/help/managing/best-practices.md)で扱ったドキュメントの内容や原則を拡張および補足する詳細情報を提供します。

## AEM - 何を使用するか {#aem-what-will-you-be-using}

>[!CAUTION]
>
>ここに示すリストは完全ではなく、概要として示しています。

### AEM 内の機能 {#features-within-aem}

AEM を実装するとき（特に初回）は、[AEM の機能とワークフロー](https://www.adobe.com/ja/marketing/experience-manager.html)を見直して、必要な領域を確認する必要があります。

次のような使用する AEM の機能と、デザインへの影響を検討します。

* [Commerce](/help/sites-administering/ecommerce.md)
* [Screens](https://docs.adobe.com/content/help/ja/experience-manager-screens/user-guide/aem-screens-introduction.html)
* [Assets](/help/assets/assets.md)
* [タグ](/help/sites-administering/tags.md)
* [マルチサイト管理と翻訳](/help/sites-administering/msm-and-translation.md)
* [Forms](/help/forms/home.md)
* [Communities](/help/communities/deploy-communities.md)
* [Livefyre](https://answers.livefyre.com/product/livefyre-for-adobe-experience-manager-aem/livefyre-for-adobe-experience-manager/)

また、[リリースノート](/help/release-notes/release-notes.md)で AEM の様々なバージョンをチェックして、新機能が追加された時期を確認してください。

### 統合 {#integrations}

AEM は、他のアドビ製品やサードパーティのサービスと統合できます。統合により、さらなるパワーと機能を自由に利用できます。

詳しくは、[ソリューションの統合](/help/sites-administering/integration.md)を参照してください。

## 移行かアップグレードか {#migrate-or-upgrade}

主に考慮する点は、以下のいずれを実行するかです。

* 配置済みの既存のインストールをアップグレードする。
* 現在のシステムのコンテンツを新規インストールに移行する。

旧バージョンから最新バージョンに移行する場合、次の 2 つのオプションがあります。

* [パッケージマネージャー](/help/sites-administering/package-manager.md)を使用して、旧システムから新システムにすべてのコンテンツおよびアプリケーションコードをエクスポートします。
* 配置済みの旧システムを[アップグレード](/help/sites-deploying/upgrade.md)します。ほとんどの場合、このオプションが推奨されます。

## 基本ルール {#basic-ground-rules}

あらゆるプロジェクトと同様に、できるだけ早い時期に基本原則を確立することが重要です。次の機能が含まれます。

>[!NOTE]
>
>これらは一般的な項目です。AEM に関連した具体例については、[ベストプラクティスチェックリスト](/help/managing/best-practices.md)で扱っています。

* **役割**

   役割は明確に定義し、プロジェクトに関わる全員に知らせる必要があります。また、以下の役割を特に強調して知らせることをお勧めします。

   * 意思決定者
   * 連絡先

* **責務**

   * 各役割に対して、プロジェクトに関連した責務を明確に定義すると、混乱を防ぐことができます。

* **関与**

   できるだけ早く関係者を関与させることで、プロジェクトの&#x200B;*ステークホルダー*&#x200B;になるように働きかけ、成功に向けての意欲を向上させることができます。

   * 顧客側では、作成者が含まれます。作成者は、日々システムを使用する必要があります。
   * 独自のプロジェクトチーム内に、品質保証に責任を持つ担当者も含まれます。 顧客の要件を理解するほど、テストの計画がより適切になります。

* **伝達経路**

   * これらを過度に正式に定義するべきではありませんが、具体的な定義は、主要な人々が常に情報を提供し、その結果、最新の状態に保つようにする必要があります。 外部の関係者とのコミュニケーションには、特に注意が必要です。

* **プロセス**

   定義するプロセスは、個々のプロジェクトに応じて異なります。 再度、以下を考慮して、これらのシンプルな設定を維持するようにしてください。

   * 任意のサードパーティとやり取りするためのプロセス（および通信のパス）の定義例：設計代理店やサードパーティのソフトウェアサプライヤーなど。
   * 多くの場合、顧客は独自のプロジェクト管理およびレポート作成の手順とツールを持ちます。

* **追跡ツール**

   バグやタスクなど、プロジェクトに関する情報を追跡できる多くのツールがあります。詳しくは、[使用する可能性があるツールの概要](#overview-of-potential-tools)を参照してください。

   * ここで注意すべき重要な点は、情報のコピーを 1 つだけ保持し、情報を共有することです（したがって、使用中のツールにアクセスする）。 これにより、メンテナンスが容易になり、不一致を防ぐのに役立ちます。

* **範囲**

   様々なレベルで、プロジェクトでカバーする内容を明確に定義します。

   * 個々のリリース（反復リリースプロセスを使用する場合、顧客に提供されるか社内テストチームに提供されるかに関係なく）。
   * AEM プロジェクト。
   * プロジェクト全体（サードパーティ製ソフトウェア、テストへの影響、組織の問題、その他多くを含みます）。
   * プロジェクトの範囲内に&#x200B;*ない*&#x200B;ものを示すことが役に立つ場合もあります。混乱や誤認を回避できますが、基本的な問題での使用に限定されます。

* **レポート**

   レポートする情報、形式、頻度およびレポート先を明確に定義します。

* **用語**

   * 使用される略語／顧客固有の用語を定義します。

* **前提**

   * あらゆる想定事項を定義します。

この情報は、プロジェクトハンドブック内で定義できます。また、Wiki の使用も、継続的な変化に効率よく対応するために役立ちます。定義するポイントに関わらず、重要な要因は以下のとおりです。

* 情報の定義と管理
* 関係者全員に対して、情報が明確に伝達されます。 標準的なプロジェクト管理方法ではありますが、役割定義が明確であるかや、伝達が良好であるかによって、プロジェクトの成否が左右されるということを繰り返し肝に銘じてください。
* バグ追跡や問題追跡など、追跡される情報は、1 つのバージョンだけを保持する。

## 主要業績評価指標とターゲット指標 {#key-performance-indicators-and-target-metrics}

組織は主要業績評価指標（KPI）を使用して、ターゲット達成の成功を評価します。これらの指標は測定可能な値です。これにより、特定の目的がいかに効果的に達成されているかを示すことができます。

以下の指標があります。

* ビジネス：

   * 主要なビジネス目標を測定します。
   * 実際のビジネスやシナリオに適した KPI を選択することが重要です。その KPI が何であるか、どのように測定するか、誰がどのように使用するかを明確に定義する必要があります。

* パフォーマンス：

   * システムのパフォーマンスの測定方法を定義します。
   * 例として、ページの読み込み時間、サーバーの応答時間、データベースのクエリパフォーマンスなどがあります。

指標の一部は、特定および定義されたターゲット指標をベースとすることができますが、すべてそうする必要はありません。

### ターゲット指標 {#target-metrics}

指標は、Web サイトの品質の量的な測定を定義するために使用されます。基本的には、パフォーマンスの達成目標の定義であり、[KPI（主要業績評価指標）](#key-performance-indicators-and-target-metrics)を定義する際に使用できます。

多数のメトリックを定義できますが、その多くは、パフォーマンスと同時性に関する目標を定義するものです。特に、量的に示すことが難しく、*感情*&#x200B;によって評価される傾向にある次のような要素について定義します。

* 「Web サイトの現在の速度が&#x200B;*遅すぎる*」 - *低速*&#x200B;になるのはいつか。

* 「同僚がログインすると、すべてが&#x200B;*停止*&#x200B;する」 - システムでサポートされる同時ユーザー数は何人か。
* 「検索時にシステムが&#x200B;*停止*&#x200B;する」 - どのような種類の検索要求がシステムに影響を及ぼすか。
* 「ファイルのダウンロードに&#x200B;*長く*&#x200B;時間がかかる」 - （標準ネットワーク条件下で）許容されるダウンロード時間はどれくらいか。

Target 指標は、プロジェクトの開始時に次の目的で定義されます。

* 提供する Web サイトの期待されるディメンションを示す
* 達成したい最低品質を示す
* これらの要因が実際にどのように測定されるかを定義する
* [主要業績評価指標](#key-performance-indicators-and-target-metrics)の基礎として使用される

ターゲット指標を定義する際は、常に注意する必要があります。

* 高く設定しすぎると、まったく到達できない可能性がある
* 低く設定しすぎると、変動が目立たない可能性がある
* 繰り返し、一貫して測定できるようにする
* 異なる要因を測定するようバランスを提供する
* 特定の指標はテスト環境に関連しますが、一部の指標は、実稼動 web サイトで測定可能かつ再現可能である必要がある、実際のシナリオを反映する必要があります
* Web サイトに対する指標の重要性に従って指標を優先順位付けする
* 指標を現実的に監視できるセットに制限する

これらのメトリックは、プロジェクトの開発時に必要に応じて更新したり、調整したりできます。プロジェクトが正常に実装されたら、これらのメトリックを使用してインストール環境を制御したり、継続中の操作に必要なサービスレベルの監視や維持を行ったりすることができます。

適切に使用すると、これらの指標は役立つツールとなりますが、無責任に使用すると時間を無駄にすることになります。いつものように、何をどのように測定するのか、およびその理由を理解する必要があります。

>[!NOTE]
>
>この節では、考慮すべき基本原則と問題を取り扱います。インストールはそれぞれ異なるので、測定する実際の値も異なります。

### すべての基礎となるプロジェクトデザイン {#everything-rests-on-your-project-design}

測定されるすべての指標は、ある意味で、プロジェクトのデザインの影響を受けます。 逆に、問題が多数ある場合は、デザインの変更によって解決されるのが最善です。

したがって、デザインを決定する&#x200B;*前に*&#x200B;ターゲットメトリックを定義する必要があります。これにより、これらの要因に基づいてデザインを最適化できます。 プロジェクトが開発されると、基本的なデザイン原則を変更するのは難しくなります。

Web サイトの構造を作成する際には、AEM Web サイトで推奨される構造に従います。次の問題や原則を必ず理解しておいてください。

* Web サイトのコンテンツを構築する方法。
* テンプレートとコンポーネントの動作方法。
* キャッシュの仕組み。
* パーソナライズされたコンテンツの影響。
* 検索機能の仕組み。
* CSS と関連テクノロジーを使用して、コンパクトで冗長でない HTM Lコードを作成する方法。

デザインがガイドラインに従っていないと感じる場合や、影響の一部が不明な場合は、プログラミング段階を開始する前や、内容を入力する前に、これらの問題を明確にしてください。

### インフラストラクチャ {#infrastructure}

インフラストラクチャを定義または評価するため、次のようなターゲット値を定義すると役立ちます。

* 訪問者／日（平均とピークの両方）
* ヒット／日（平均とピークの両方）
* 使用可能にする web ページの数
* web コンテンツの量

使用時の状況、および Web サイトの戦略的意義に応じて、以下の項目がインフラストラクチャの評価や選択に役立ちます。

* サーバーの数
* AEM インスタンス（オーサーおよびパブリッシュ）の数

### パフォーマンス {#performance}

評価できるパフォーマンス要因はいくつかあります。

* 個々のページの応答時間（アカウントを考慮）

   * オーサー環境での応答時間
   * パブリッシュ環境での応答時間

* 検索リクエストの応答時間

この節と[パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)を併せて読むと、実際のパフォーマンス測定技術の詳細を把握できます。

#### 個々のページの応答時間 {#response-times-for-individual-pages}

Web サイトが訪問者の要求に応答するまでにどの程度の時間がかかるかは、非常に重要な問題です。

当然、応答時間は個々の要求によって異なりますが、平均的なターゲット時間の値を定義することはできます。この値が達成可能かつ維持可能な数値と証明されれば、Web サイトのパフォーマンスを監視したり、潜在的な問題の進行を示したりするために使用できます。

オーサー環境とパブリッシュ環境でのターゲットの違い

オーサー環境とパブリッシュ環境では、対象ユーザーが異なるので、目標とする応答時間が異なります。

* **オーサー環境**

   この環境は、コンテンツの入力および更新をおこなう作成者が使用する環境なので、以下のように設定することが必要です。

   * コンテンツページとそのページ上の個別の要素を更新する際に多数のリクエストを生成する、少人数のユーザー向けに作成する
   * コンテンツを Web サイトにできるだけ早く展開し、生産性を最大限に高める

* **パブリッシュ環境**

   この環境には、ユーザー向けに提供するコンテンツが置かれます。

   * 速度は重要であるが、多くの場合、オーサー環境より遅くなる
   * パフォーマンス強化メカニズムの追加は、多くの場合、次のように適用されます。

      * コンテンツがキャッシュされる
      * 負荷分散が適用される

#### ターゲット応答時間の設定 {#setting-target-response-times}

以上に基づき、どうすれば達成可能な（平均）応答時間を決定できるでしょうか。これは多くの場合、経験の問題です。

* Web サイトでの過去のエクスペリエンス
* AEM の使用経験
* 平均応答時間を超える複雑なページの認識（可能な場合は個別に最適化する必要があります）

ただし、（制御下にある状況では）以下のガイドラインを適用できます。

* ページに対するリクエストの 70 ％に 100 ms 未満で応答。
* ページに対するリクエストの 25 ％に 100 ms ～ 300msで応答。
* ページに対するリクエストの 4 ％に 300 ms ~ 500ms 未満で応答。
* ページに対するリクエストの 1 ％に 500 ms ～ 1000 ms で応答。
* ページ要求への応答時間が 1 秒を超えることはない。

以上の数値は、次の条件を前提としています。

* パブリッシュ環境で測定される（オーサー環境や CFC のオーバーヘッドではない）
* サーバー上で測定される（ネットワークオーバーヘッドを考慮しない）
* キャッシュされない（AEM 出力キャッシュや Dispatcher キャッシュがない）
* 多数の依存ファイル（HTML、JS、PDF など）を伴う複雑な要求のみ
* 他のシステム負荷なし

いくつかのメカニズムを使用して応答時間を監視できます。

* **AEM request.log を使用した応答時間の監視**

   パフォーマンス分析は、リクエストログから始めることをお勧めします。この情報を使用して、個々のリクエストの応答時間を確認できます。 詳しくは、[パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)を参照してください。

* **HTML コメントを使用した応答時間の監視**

   `*HTML comments* can be used to include response time information within the source of each page:`

   `</body> </html>v <-- Page took 58 milliseconds to be rendered by the server --> Response times for search requests`

#### 検索リクエスト {#search-requests}

検索要求は、以下の両方の点で、Web サイトに重大な影響を与える可能性があります。

* 実際の検索の応答時間

   * 高速な検索機能が、Web サイトの品質目標です。

* 全般的なパフォーマンスへの影響

   * 検索機能は、（巨大である可能性の高い）コンテンツのセクションや、特別に抽出されたインデックスをスキャンする必要があるので、この機能が最適化されていないと、システム全体のパフォーマンスに影響する可能性があります。

検索要求のターゲット設定についても、以下に応じて経験に基づいておこないます。

* AEM の使用経験
* 検索の使用頻度を、他の目標と比較して評価する
* 永続性マネージャー
* 検索インデックス
* 検索機能の複雑さ。検索用語が 1 語のみ許可される基本的な検索機能は、AND／OR／NOT を使用して複雑な検索ステートメントを作成できる高度な検索よりも速くなります。

このカスタマイズの計画および統合は、プロジェクトの最初の時点からおこなう必要があります。監視には次のメカニズムを使用することができます。

* **AEM request.log を使用した検索応答時間の監視**

   この場合も、request.log を使用することで、検索要求の応答時間を監視できます。詳しくは、[パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)を参照してください。

* **検索応答時間の測定のプログラム化メカニズム**

   検索要求に関して収集する情報、および検索要求のパフォーマンスをカスタマイズするには、プロジェクトのソースコードに情報収集を含めることをお勧めします。詳しくは、[パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)を参照してください。

### 並行性 {#concurrency}

Web サイトは、オーサー環境とパブリッシュ環境の両方で多数のユーザー／訪問者に公開されます。ユーザーの数は通常、テスト時に使用したユーザー数より多くなりますが、同時に変動があり、予測が困難です。パフォーマンスへの悪影響を意識せずに作業できる同時ユーザー／訪問者数の平均値を考慮して、Web サイトをデザインする必要があります。この場合も `request.log` を使用して、同時実行をテストできます。詳しくは、[パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)を参照してください。

同時ユーザー数のターゲットは、環境のタイプによって異なります。

* **オーサー環境**

   * 通常、同時ユーザー数は正確に見積もることができます。 同時にアクティブとなる作成者の数は把握できなくても、作成者の総数はわかります。

* **パブリッシュ環境**

   * これは予測が難しいので、ターゲット値を選択する必要があります。これも、現在の web サイトでの経験と、新しい web サイトに対する現実的な期待に基づくものにする必要があります。
   * 特別なイベント（例えば非常に人気のあるコンテンツを新規公開する場合）では、予測を超えたり、（イベントのチケットの発売時に報道されると）処理能力を超えたりすることもあります。

### 処理能力とボリューム {#capacity-and-volume}

関連するメトリックについて説明する前に、いくつかの用語の大まかな定義を示します。

* **ボリューム**

   * システムが処理および提供する出力の量です。

* **処理能力**

   * システムがボリュームを提供する能力です。
   * 次の表に示すように、処理能力とボリュームの測定方法は各手順で異なります。最高のパフォーマンスを得るには、処理能力が各手順のボリュームに釣り合い、処理能力とボリュームの両方がすべての手順で共有されていることを確認します。例えば、要求ごとにサーバーでナビゲーションを計算する代わりに、クライアントコンピューターで計算したり、キャッシュに配置したりできます。

* **処理能力とボリューム**

   | 対象／場所 | 処理能力 | ボリューム |
   |---|---|---|
   | クライアント | ユーザーのコンピューターの処理能力。 | ページレイアウトの複雑さ。 |
   | ネットワーク | ネットワークの帯域幅。 | ページ（コード、画像など）のサイズ。 |
   | Dispatcher キャッシュ | Web サーバーのサーバーメモリ（メインメモリとハードドライブ）。 | Web サーバー（メインメモリとハードドライブ）。キャッシュされたページの数とサイズ。 |
   | 出力キャッシュ | AEM サーバーのサーバーメモリ（メインメモリとハードドライブ）。 | 出力キャッシュ内のページの数とサイズ、ページあたりの依存関係の数。Dispatcher キャッシュを使用すると、このボリュームが少なくなります。 |
   | Web サーバー | Web サーバーの処理能力。 | リクエストの数量。キャッシュを使用すると、このボリュームが少なくなります。 |
   | テンプレート | Web サーバーの処理能力。 | テンプレートの複雑さ。 |
   | リポジトリ | リポジトリのパフォーマンス。 | リポジトリから読み込まれたページの数。 |

### その他のメトリック {#other-metrics}

以上の節では、定義される主なメトリックについて説明しました。

具体的な要件に応じて、個別に、または上記の分類を考慮して、追加の指標を個別に定義すると便利です。

ただし、web サイトのあらゆる側面を測定および定義しようとするのではなく、簡単かつ確実に機能する、正確で中核的な少しの指標を使用することをお勧めします。Web サイトは、その性質上、ユーザーに引き渡されるとすぐに変更と進化が始まります。

## セキュリティ {#security}

セキュリティはきわめて重要であり、対処すべき課題として深刻性を増しています。プロジェクトの早期の段階からセキュリティについて検討し、計画する必要があります&#x200B;***。***

[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)では、デプロイ時に AEM インストールを確実に保護するための手順が詳細に説明されています。その他のセキュリティ要素については、[セキュリティ（開発時）](/help/sites-developing/security.md)および[ユーザー管理とセキュリティ](/help/sites-administering/security.md)を参照してください。

## 並列タスクと反復タスク {#parallel-and-iterative-tasks}

>[!NOTE]
>
>このセクションでは、以下の点について留意してください。
>
>* AEM プロジェクトの&#x200B;*最初の*&#x200B;実装に関連する概要が提供されています。
>* 抽象的な概要を示すことを意図しています。具体的なフェーズ／マイルストーン／タスクについては、[プロジェクトチェックリスト](/help/managing/best-practices.md)を参照してください。
>* 時間単位は理論上のものです。
>


標準的な AEM プロジェクトを新規に実装するには、以下のようなタスクを検討する必要があります。

* セールスプロセスから引き継がれます。
* 顧客アプリケーションを実装します（**開発**）。
* 顧客サイトにインフラストラクチャ（および関連プロセス）をインストールして設定します（**インフラストラクチャ**）。
* コンテンツを作成（または移行）します（**コンテンツ**）。
* 運営に引き継ぎます（**メンテナンス／サポート**）。
* リリースをフォローアップします。

![chlimage_1-2](assets/chlimage_1-2.png)

すべての面で、反復アプローチを使用することをお勧めします。

![chlimage_1-3](assets/chlimage_1-3.png)

>[!NOTE]
>
>実稼動環境の実際の条件で調整、最適化およびユーザートレーニングができるように、プロジェクト開始を&#x200B;**ソフトローンチ**（不完全な可用性、複数の反復）と&#x200B;**ハードローンチ**（完全な可用性 - ライブ）に分割します。

>[!NOTE]
>
>プロジェクトのライフサイクルで実行（または評価）する必要のあるタスクの例については、[プロジェクトチェックリスト](/help/managing/best-practices.md)を参照してください。

各カテゴリについての留意事項を次に示します。

* **開発**

   * 基本アーキテクチャを最初に定義します。
   * 開発にはいくつかの繰り返し（スプリント）を使用します。

      * 最初のスプリントは最初の全開発サイクルに相当します。
      * 最初のスプリントの結果として、テスト環境への最初の開発が行われます。
      * すべてのスプリントが実行可能な結果を持ちます。
      * スプリントごとに顧客の承認（最低限の構造テストとフィードバック）が取得されます。
   * プロジェクトの進行中に利用可能な AEM バージョンが最終的に更新されるように計画します。
   * スプリント中にテストおよび最適化が行われるように計画します。
   * 安定化および最適化フェーズを計画します。
   * 今後のリリース対象として計画している項目のログを作成します。
   * パートナーの関与と引き継ぎを計画します。


* **インフラストラクチャ**

   * 基本アーキテクチャを最初に定義します。

      * パフォーマンス要件を定義します。
      * パフォーマンス目標を定義します（つまり、期待事項を明確に定義します）。
      * サイジングを含め、ハードウェアとインフラストラクチャのアーキテクチャを定義します。
      * デプロイメントを定義します。
   * 最初のスプリントと次の初期設定の準備にいくつかの繰り返しを使用します。

      * 開発環境
      * 開発プロセス
      * テスト環境
      * 開発プロセス（設定管理を含む）
   * いくつかの負荷テストを計画します。
   * スプリント中にテストおよび最適化が行われるように計画します。
   * 安定化および最適化フェーズを計画します。
   * 実稼働環境にできるだけ早期にデプロイします（運営チームにシステムのセットアップ経験を積ませます）。
   * 指定されたユーザーと定義済み役割をできるだけ早期に使用します。
   * トレーニング（管理者向けトレーニングなど）を計画します。
   * 運営への引き継ぎを計画します。



* **コンテンツ**

   * 基本アーキテクチャとは次のようなものです。
      * コンテンツ階層を稼働させます。
      * コンテンツの概念を定義するのに役立ちます。
      * MSM の使用方法とレイアウトを定義します。
      * 役割、グループ、ワークフロー、および権限を定義します。
   * オフラインページの作成が有益かどうかを検討します。
   * 初期ページおよびコンテンツの早期作成を計画します（テストおよびフィードバック用）。
   * 既存のコンテンツの移行を計画します。
   * リファクタリング後の「スプリント中移行」を計画します。
   * 「コンテンツバーンダウン」（実稼動コンテンツのサイトマップ）を計画します。

## 時間と労力の見積もり {#estimating-time-and-effort}

結果のタスクリストに応じて、（上位レベルの）タスク定義に対する時間と労力の初期見積もりを行うことができます。 これには、誰（顧客またはパートナー）がいつ何をするかを示す指標が含まれます。

次のリストは、関連する作業の標準的な概算と相互関係、つまりコストを示しています。

>[!CAUTION]
>
>これらの数字は初期見積もりにのみ使用できます。経験豊富な AEM 開発者は詳細な分析をおこなう必要があります。

| フェーズ | 労力 |
|---|---|
| 開発 | コンポーネントノードごとに 2 ～ 4 時間の概算見積もりを使用すると、すべての開発要件を満たします。 |
| 開発者によるテスト | 開発 15 ％ |
| フォローアップ | 開発 10 ％ |
| ドキュメント化 | 開発 15 ％ |
| JavaDoc 文書化 | 開発 10 ％ |
| バグ修正 | 開発 15 ％ |
| プロジェクト管理 | 進行中のプロジェクトの管理および統制にかかるプロジェクトコストの 20 ％ |

その後の詳細な計画で、使用可能なリソースや必要なリソースを、納期やコストに関連付けることができます。

## 参照アーキテクチャ {#reference-architecture}

参照アーキテクチャは、AEM アーキテクチャにテンプレートソリューションを提供するために用意されました。参照アーキテクチャは、拡張性、信頼性、セキュリティなどの、企業システムで一般的に発生する問題に対処します。

次のサイトメトリックを定義する必要があります。

| 分類 | 定義 |
|---|---|
| インターネットサイトの数 |  |
| イントラネットサイトの数 |  |
| コードベースの数（インターネットとイントラネットが異なる場合など） |  |
| 個々のページの数 |  |
| 1 日あたりのサイト訪問の数 |  |
| 1 日あたりのページビューの数 |  |
| 1 日あたりのデータ転送量（GB） |  |
| 同時ユーザーの数（閉じられたユーザーグループ） |  |
| 同時訪問者の数（公開） |  |
| 同時作成者の数 |  |
| 登録済み作成者の数 |  |
| 営業日あたりのページアクティベーションの数 |  |
| デプロイ時のページアクティベーションの数 |  |

## 使用する可能性があるツールの概要 {#overview-of-potential-tools}

次のリストは、使用可能な各種ツールを示しています。このリストはあくまでもツールの紹介で、詳細な推奨リストではありません。その他の任意のツールは使用できないということを意味するものではありません。

<table>
 <tbody>
  <tr>
   <td><strong>製品</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>AEM</td>
   <td><p>AEM 自体は、アプリケーションの監視、テスト、調査およびデバッグを支援する様々なメカニズムを提供し、それには以下を含みます。</p>
    <ul>
     <li><a href="/help/sites-developing/developer-mode.md">開発者モード</a></li>
     <li><a href="/help/sites-developing/hobbes.md">テストコンソール</a></li>
     <li><a href="/help/sites-administering/operations-dashboard.md">操作ダッシュボード</a></li>
     <li><a href="/help/sites-authoring/content-insights.md">コンテンツインサイト</a></li>
     <li><a href="/help/sites-authoring/author-environment-tools.md#content-tree">コンテンツツリー</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Selenium</td>
   <td><a href="https://docs.seleniumhq.org/">Selenium</a> は、オープンソースのテストツールです。テストはブラウザーで直接実行され、ユーザーの作業がエミュレートされます。</td>
  </tr>
  <tr>
   <td>Microsoft Project</td>
   <td>一般的に使用されるプロジェクト管理ツール。</td>
  </tr>
  <tr>
   <td>Jira</td>
   <td><a href="https://www.atlassian.com/software/jira">Jira</a> は、ソフトウェアバグを詳細に追跡および管理するためオープンソースツールです。必要に応じて、バグの詳細情報にワークフローを組み込むこともできます。</td>
  </tr>
  <tr>
   <td>Git</td>
   <td><a href="https://git-scm.com/">Git</a> は、リビジョン管理ソフトウェアです。</td>
  </tr>
  <tr>
   <td>Eclipse</td>
   <td><p>Eclipse は、様々なプロジェクトからなるオープンソース IDE です。ソフトウェアをライフサイクルに沿って構築、デプロイ、管理するために必要な広範なフレームワーク、ツールおよびランタイムで構成されるオープン開発プラットフォームを構築することに焦点を当てています。</p> <p>詳しくは、<a href="/help/sites-developing/howto-projects-eclipse.md">Eclipse を使用して AEM プロジェクトを開発する方法</a>を参照してください。</p> </td>
  </tr>
  <tr>
   <td>IntelliJ</td>
   <td><p>各種機能を包括的に備えたプロフェッショナル向け IDE です（そのため、ライセンス費が発生します）。 </p> <p>詳しくは、<a href="/help/sites-developing/ht-intellij.md">IntelliJ IDEA を使用して AEM プロジェクトを開発する方法</a>を参照してください。</p> </td>
  </tr>
  <tr>
   <td>Maven</td>
   <td><a href="https://maven.apache.org/">Maven</a> は、プロジェクトの構築プロセス（ソフトウェアおよびドキュメント）を管理するための包括的なソフトウェアプロジェクト管理ツールです。</td>
  </tr>
 </tbody>
</table>

## 参考情報 {#further-reading}

また、次の各節では、特に注目すべき内容を取り上げています。

* [はじめに](/help/sites-deploying/deploy.md#getting-started)
* [技術要件](/help/sites-deploying/technical-requirements.md)
* [インスタンスの監視および保守](/help/sites-deploying/monitoring-and-maintaining.md)

### ベストプラクティス {#best-practices}

アドビでは、以下のようなすべてのフェーズおよびオーディエンスに対してさらにベストプラクティスを提供しています。

* [デプロイ](/help/sites-deploying/best-practices.md)
* [オーサリング](/help/sites-authoring/best-practices.md)
* [管理](/help/sites-administering/administer-best-practices.md)
* [開発](/help/sites-developing/best-practices.md)
* [プロジェクト管理](/help/managing/best-practices.md)
