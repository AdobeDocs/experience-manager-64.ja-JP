---
title: 高度なスコアとバッジ
seo-title: 高度なスコアとバッジ
description: 高度なスコアの設定
seo-description: 高度なスコアの設定
uuid: 3854b668-729a-42b8-b7cd-5d5ec1ca8380
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 42fb3c50-8728-4897-ade9-6b839294a10e
translation-type: tm+mt
source-git-commit: ddf92a270835259998aa28f5960abcf55f56d1fc

---


# 高度なスコアとバッジ {#advanced-scoring-and-badges}

## 概要 {#overview}

高度なスコアを使用すると、メンバーをエキスパートとして識別するバッジを授与できます。Advanced scoring assigns points based on the quantity *and* quality of content created by a member, whereas basic scoring assigns points simply based on the quantity of content created.

この違いは、スコアの計算に使用されるスコアエンジンによるものです。基本スコアリングエンジンは、単純な計算を適用します。 アドバンススコアリングエンジンは、トピックの自然言語処理(NLP)を通じて演出される、価値の高い関連コンテンツに貢献するアクティブメンバーに報奨を与えるアダプティブアルゴリズムです。

このスコアアルゴリズムでは、コンテンツの関連度に加え、投票や回答の割合など、メンバーのアクティビティが考慮されます。基本スコアリングには定量的なものも含まれますが、高度スコアリングではアルゴリズム的に使用されます。

したがって、高度なスコアエンジンの分析を意味あるものにするには、十分なデータが必要です。エキスパートになるための達成のしきい値は、作成されたコンテンツの量と品質にアルゴリズムが継続的に調整されるので、常に再評価されます。 There is also a concept of *decay* of a member&#39;s older posts. If an expert member stops participating in the subject matter where they gained expert status, at some pre-determined point (see [scoring engine configuration](#configurable-scoring-engine)) they could lose their status as an expert.

高度なスコアの設定方法は、基本スコアとほとんど同じです。

* Basic and advanced scoring and badging rules are [applied to content](implementing-scoring.md#apply-rules-to-content) in the same manner
   * 基本および高度なスコアおよびバッジルールを同じコンテンツに適用できます。
* [コンポーネントのバッジの有効化](implementing-scoring.md#enable-badges-for-component) ：汎用

スコアルールおよびバッジルールの設定では、以下の点が異なります。

* 設定可能な高度なスコアリングエンジン
* 高度なスコアリングルール：
   * `scoringType` 詳細に設 **[!UICONTROL 定]**
   * ストップワードが必要です

* 詳細なバッジルール：
   * `badgingType` 詳細に設 **[!UICONTROL 定]**
   * `badgingLevels` を授与するエキスパートレベルの数に設定
   * Requires `badgingPaths` array of badges instead of thresholds array mapping points to badges

>[!NOTE]
>
>高度なスコアおよびバッジ機能を使用するには、エキスパートIDパッケージ [をインストールしま](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg)す。

## 設定可能なスコアエンジン {#configurable-scoring-engine}

この高度なスコアエンジンには OSGi 設定が用意されており、パラメーターを設定して高度なスコアアルゴリズムを調整できます。

![chlimage_1-260](assets/chlimage_1-260.png)

* **[!UICONTROL スコアの重]**&#x200B;みトピックの場合、スコアを計算する際に最も高い優先度を与える必要がある動詞を指定します。 One or more topics may be entered, but limited to **one verb per topic**. See [Topics and Verbs](implementing-scoring.md#topics-and-verbs).

   コンマはエスケープさ `topic,verb` れたとおりに入力されます。 次に例を示します。

   `/social/forum/hbs/social/forum\,ADD`

   
デフォルトは、QnAおよびフォーラムコンポーネントのADD動詞に設定されます。


* **[!UICONTROL スコアリング範囲]**

   高度なスコアの範囲は、0 からこの値までとして定義されます。

   デフォルト値は 100 であり、スコア範囲は 0 ～ 100 となります。


* **[!UICONTROL エンティティ減衰時間間隔]**

   このパラメーターは、すべてのエンティティスコアがディケードされる時間数を表します。 これは、コミュニティサイト上にある古いコンテンツをスコアに含めないようにするために必要な設定です。

   デフォルト値は 216000 時間（約 24 年）です。


* **[!UICONTROL スコアリング増加率]**

   スコアを指定します。 0 から scoring range 値までの範囲でスコア値を指定します。この値を超えると、エキスパートの数を制限するために上昇率が低下します。

   デフォルト値は 50 です。

## 高度なスコアルール {#advanced-scoring-rules}

基本スコアでは、バッジ獲得に必要な量はあらかじめ決まっています。

高度なスコアでは、システム内の上質なデータの量に基づいて、バッジ獲得に必要な量が継続的に調整されます。スコアリングは、ベル曲線と同様の方法で連続的に計算されます。

あるトピックでエキスパートのバッジを獲得したメンバーが、その後あまり活動しなくなった場合は、時間経過に伴う減衰によってバッジを失う可能性があります。

### ScoringType {#scoringtype}

スコアルールは、スコアサブルールの集まりです。各サブルールは、それぞれ `scoringType` を宣言します。

高度なスコアエンジンを呼び出すには、`scoringType` を `advanced` に設定する必要があります。

[スコアサブルール](implementing-scoring.md#scoring-sub-rules)を参照してください。

![chlimage_1-261](assets/chlimage_1-261.png)

### Stopwords {#stopwords}

高度なスコアパッケージでは、ストップワードファイルを含む設定フォルダーがインストールされます。

* `/etc/community/scoring/configuration/stopwords`

高度なスコアのアルゴリズムは、ストップワードファイルに含まれる単語のリストに基づいて、コンテンツ処理中に無視して構わない一般的な英単語を識別します。

このファイルが変更されることはありません。

ストップワードファイルが存在しない場合は、スコアエンジンによりエラーがスローされます。

## 高度なバッジルール {#advanced-badging-rules}

高度なバッジルールのプロパティは、[基本バッジルールのプロパティ](implementing-scoring.md#badging-rules)とは異なります。

ポイントとバッジ画像を関連付ける必要はなく、許可するエキスパートの数と、授与するバッジ画像を指定するだけで十分です。

![chlimage_1-262](assets/chlimage_1-262.png)

| **プロパティ** | **タイプ** | **値の説明** |
|---------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| badgingPath | String[] | （必須）badgingLevelsの数までのバッジ画像の複数値の文字列。 バッジ画像のパスを指定するときは、最も高いレベルのエキスパートに授与するものを最初に指定する必要があります。badgingLevels で指定された値よりもバッジの数が少ない場合、足りない部分には配列内の最終要素のバッジが使用されます。例：/etc/community/badging/images/expert-badge/jcr:content/expert.png |
| badgingLevels | Long | （オプション）授与する専門知識のレベルを指定します。 例えば、エキスパートとほぼエキスパート（2つのバッジ）が必要な場合、値は2に設定する必要があります。 badgingLevelは、badgingPathプロパティに対してリストされたエキスパート関連バッジ画像の数に対応する必要があります。 初期設定は 1 です。 |
| badgingType | 文字列 | （必須）スコアリングエンジンが「基本」または「詳細」であることを示します。 「advanced」に設定した場合、デフォルトは「basic」です。 |
| scoringRules | String[] | （オプション）バッジルールを、リストされたスコアリングルールで識別されるスコアリングイベントに制限する複数値の文字列。例：/etc/community/scoring/rules/adv-comments-scoringデフォルトは制限なし。 |

## このリリースに含まれるルールとバッジ {#included-rules-and-badge}

### このリリースに含まれるバッジ {#included-badge}

このベータリリースには、以下の報奨ベースのエキスパートバッジが含まれています。

* 専門家

   `/etc/community/badging/images/expert-badge/jcr:content/expert.png`

![chlimage_1-263](assets/chlimage_1-263.png)

アクティビティに対する報奨としてエキスパートのバッジを表示するには、以下の 2 つの設定をする必要があります。

* `badges` は、フォーラムやQnAコンポーネントなど、機能に対して有効にする必要があります。
* 高度なスコアルールとバッジルールを、コンポーネントが配置されているページ（または上位ページ）に適用します。

以下の基本情報を参照してください。

* [コンポーネントのバッジの有効化](implementing-scoring.md#enable-badges-for-component)
* [ルールの適用](implementing-scoring.md#apply-rules-to-content)

### このリリースに含まれているスコアルールとサブルール {#included-scoring-rules-and-sub-rules}

Included in the beta release are two advanced scoring rules for the [forum function](functions.md#forum-function) (one each for the forum and comments components of the forum feature):

1. /etc/community/scoring/rules/adv-comments-scoring

   * `subRules[]` =

      /etc/community/scoring/rules/sub rules/adv-comments-rule

      /etc/community/scoring/rules/sub rules/adv-voting-rule-owner

      /etc/community/scoring/rules/sub rules/adv-voting-rule

2. /etc/community/scoring/rules/adv-forums-scoring

   * `subRules[]` =

      /etc/community/scoring/rules/sub rules/adv-forums-rule

      /etc/community/scoring/rules/sub rules/adv-comments-rule

      /etc/community/scoring/rules/sub rules/adv-voting-rule-owner

**注意：**

* Both `rules`and `sub-rules` nodes are of type `cq:Page`
* `subRules` は、ルールのノード上のString[] 型の属性です `jcr:content` 。
* `sub-rules` は、複数のスコアルール間で共有できます。
* `rules` は、リポジトリ内の誰でも読み取れる場所に配置する必要があります。
   * ルール名は場所にかかわらず一意である必要があります。

### このリリースに含まれるバッジルール {#included-badging-rules}

Included in the release are two advanced badging rules that correspond to the [advanced forums and comments scoring rules](#included-scoring-rules-and-sub-rules).

* /etc/community/badging/rules/adv-comments-badging
* /etc/community/badging/rules/adv-forums-badging

**注意：**

* `rules` ノードのタイプ `cq:Page`
* `rules` は、リポジトリ内の誰でも読み取れる場所に配置する必要があります。
   * ルール名は場所にかかわらず一意である必要があります。
