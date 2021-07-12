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
role: Admin
exl-id: c9406aae-288e-4cdf-ac01-cb26b423639e
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 51%

---

# 高度なスコアとバッジ {#advanced-scoring-and-badges}

## 概要 {#overview}

高度なスコアを使用すると、メンバーをエキスパートとして識別するバッジを授与できます。高度なスコアでは、メンバーが作成したコンテンツの量&#x200B;*と*&#x200B;に基づいてポイントを割り当てます。一方、基本スコアでは、作成したコンテンツの量に基づいてポイントを割り当てます。

この違いは、スコアの計算に使用されるスコアエンジンによるものです。基本スコアエンジンは、単純な計算を適用します。 高度なスコアエンジンは、トピックの自然言語処理(NLP)を通じて推測される、価値のある関連性の高いコンテンツに貢献するアクティブなメンバーに報酬を与えるアダプティブなアルゴリズムです。

このスコアアルゴリズムでは、コンテンツの関連度に加え、投票や回答の割合など、メンバーのアクティビティが考慮されます。基本的なスコアには定量的に含まれますが、高度なスコアではアルゴリズム的に使用されます。

したがって、高度なスコアエンジンの分析を意味あるものにするには、十分なデータが必要です。作成されるコンテンツの量と品質に合わせてアルゴリズムが継続的に調整されるので、エキスパートになるための達成度のしきい値は、常に再評価されます。 メンバーの古い投稿の&#x200B;*decay*&#x200B;という概念もあります。 エキスパートメンバーが、事前に決めた時点でエキスパートステータスを得た主題への参加を停止すると（[スコアエンジン設定](#configurable-scoring-engine)を参照）、エキスパートとしての地位を失う可能性があります。

高度なスコアの設定方法は、基本スコアとほとんど同じです。

* 基本的なスコアと高度なスコアとバッジのルールは、同じ方法でコンテンツ](implementing-scoring.md#apply-rules-to-content)に[適用されます
   * 基本スコアと高度なスコアとバッジのルールを同じコンテンツに適用できます。
* [一般的なコンポーネントに対するバ](implementing-scoring.md#enable-badges-for-component) ッジの有効化

スコアルールおよびバッジルールの設定では、以下の点が異なります。

* 設定可能な高度なスコアエンジン
* 高度なスコアルール：
   * `scoringType` 詳細に設 **[!UICONTROL 定]**
   * ストップワードが必要

* 高度なバッジルール：
   * `badgingType` 詳細に設 **[!UICONTROL 定]**
   * `badgingLevels` を授与するエキスパートレベルの数に設定
   * しきい値の代わりに、バッジの`badgingPaths`配列が必要です。配列とバッジのマッピングは、

>[!NOTE]
>
>高度なスコアおよびバッジ機能を使用するには、[エキスパートIDパッケージ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg)をインストールします。

## 設定可能なスコアエンジン {#configurable-scoring-engine}

この高度なスコアエンジンには OSGi 設定が用意されており、パラメーターを設定して高度なスコアアルゴリズムを調整できます。

![chlimage_1-260](assets/chlimage_1-260.png)

* **[!UICONTROL スコア]**
の重み付けトピックの場合、スコアを計算する際に最も高い優先度を付与する動詞を指定します。1つ以上のトピックを入力できますが、1つのトピック**につき**&#x200B;動詞に制限されます。 [トピックと動詞](implementing-scoring.md#topics-and-verbs)を参照してください。

   コンマはエスケープして`topic,verb`と入力します。 次に例を示します。

   `/social/forum/hbs/social/forum\,ADD`

   デフォルトでは、Q&amp;Aとフォーラムコンポーネントの「ADD」動詞が設定されます。


* **[!UICONTROL スコア範囲]**

   高度なスコアの範囲は、0 からこの値までとして定義されます。

   デフォルト値は 100 であり、スコア範囲は 0 ～ 100 となります。


* **[!UICONTROL エンティティのディケイ時間間隔]**

   このパラメーターは、すべてのエンティティスコアが減衰されるまでの時間数を表します。 これは、コミュニティサイト上にある古いコンテンツをスコアに含めないようにするために必要な設定です。

   デフォルト値は 216000 時間（約 24 年）です。


* **[!UICONTROL スコア付け成長率]**

   スコアを指定します。 0 から scoring range 値までの範囲でスコア値を指定します。この値を超えると、エキスパートの数を制限するために上昇率が低下します。

   デフォルト値は 50 です。

## 高度なスコアルール {#advanced-scoring-rules}

基本スコアでは、バッジ獲得に必要な量はあらかじめ決まっています。

高度なスコアでは、システム内の上質なデータの量に基づいて、バッジ獲得に必要な量が継続的に調整されます。スコアは、ベルの曲線と同じ方法で継続的に計算されます。

あるトピックでエキスパートのバッジを獲得したメンバーが、その後あまり活動しなくなった場合は、時間経過に伴う減衰によってバッジを失う可能性があります。

### ScoringType {#scoringtype}

スコアルールは、スコアサブルールの集まりです。各サブルールは、それぞれ `scoringType` を宣言します。

高度なスコアエンジンを呼び出すには、`scoringType` を `advanced` に設定する必要があります。

[スコアサブルール](implementing-scoring.md#scoring-sub-rules)を参照してください。

![chlimage_1-261](assets/chlimage_1-261.png)

### ストップワーズ {#stopwords}

高度なスコアパッケージでは、ストップワードファイルを含む設定フォルダーがインストールされます。

* `/etc/community/scoring/configuration/stopwords`

高度なスコアのアルゴリズムは、ストップワードファイルに含まれる単語のリストに基づいて、コンテンツ処理中に無視して構わない一般的な英単語を識別します。

このファイルが変更されることはありません。

ストップワードファイルが存在しない場合は、スコアエンジンによりエラーがスローされます。

## 高度なバッジルール {#advanced-badging-rules}

高度なバッジルールのプロパティは、[基本バッジルールのプロパティ](implementing-scoring.md#badging-rules)とは異なります。

ポイントとバッジ画像を関連付ける必要はなく、許可するエキスパートの数と、授与するバッジ画像を指定するだけで十分です。

![chlimage_1-262](assets/chlimage_1-262.png)

| **プロパティ** | **型** | **値の説明** |
|---------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| badgingPath | String[] | （必須）badgingLevelsの数までのバッジ画像の複数値文字列。 バッジ画像のパスを指定するときは、最も高いレベルのエキスパートに授与するものを最初に指定する必要があります。badgingLevels で指定された値よりもバッジの数が少ない場合、足りない部分には配列内の最終要素のバッジが使用されます。エントリ例：/etc/community/badging/images/expert-badge/jcr:content/expert.png |
| badgingLevels | Long | （オプション）授与する専門知識のレベルを指定します。 例えば、エキスパートとほぼエキスパート（2つのバッジ）が必要な場合は、値を2に設定します。 badgingLevelは、badgingPathプロパティにリストされるエキスパート関連のバッジ画像の数に対応している必要があります。 初期設定は 1 です。 |
| badgingType | 文字列 | （必須）スコアエンジンを「basic」または「advanced」として識別します。 「advanced」に設定すると、デフォルトは「basic」になります。 |
| scoringRules | 文字列[] | （オプション）バッジルールを、リストされたスコアルールで識別されるスコアイベントに制限する複数値の文字列。エントリ例：/etc/community/scoring/rules/adv-comments-scoringDefaultは、制限なしです。 |

## このリリースに含まれるルールとバッジ {#included-rules-and-badge}

### このリリースに含まれるバッジ {#included-badge}

このベータリリースには、以下の報奨ベースのエキスパートバッジが含まれています。

* 専門家

   `/etc/community/badging/images/expert-badge/jcr:content/expert.png`

![chlimage_1-263](assets/chlimage_1-263.png)

アクティビティに対する報奨としてエキスパートのバッジを表示するには、以下の 2 つの設定をする必要があります。

* `badges` フォーラムやQ&amp;Aコンポーネントなど、機能に対して有効にする必要がある
* 高度なスコアルールとバッジルールを、コンポーネントが配置されているページ（または上位ページ）に適用します。

以下の基本情報を参照してください。

* [コンポーネントのバッジの有効化](implementing-scoring.md#enable-badges-for-component)
* [ルールの適用](implementing-scoring.md#apply-rules-to-content)

### このリリースに含まれているスコアルールとサブルール {#included-scoring-rules-and-sub-rules}

ベータリリースには、[フォーラム機能](functions.md#forum-function)用の2つの高度なスコアルールが含まれています（それぞれフォーラム機能のフォーラムコンポーネントとコメントコンポーネント用）。

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

**備考:**

* `rules`ノードと`sub-rules`ノードの両方が`cq:Page`型です
* `subRules` は、ルールのノード[] のString型の属性で `jcr:content` す
* `sub-rules` は、複数のスコアルール間で共有できます。
* `rules` は、リポジトリ内の誰でも読み取れる場所に配置する必要があります。
   * ルール名は場所にかかわらず一意である必要があります。

### このリリースに含まれるバッジルール {#included-badging-rules}

このリリースには、[高度なフォーラムとコメントスコアルール](#included-scoring-rules-and-sub-rules)に対応する2つの高度なバッジルールが含まれています。

* /etc/community/badging/rules/adv-comments-badging
* /etc/community/badging/rules/adv-forums-badging

**備考:**

* `rules` ノードはタイプ  `cq:Page`
* `rules` は、リポジトリ内の誰でも読み取れる場所に配置する必要があります。
   * ルール名は場所にかかわらず一意である必要があります。
