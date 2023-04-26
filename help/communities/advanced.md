---
title: 高度なスコアとバッジ
seo-title: Advanced Scoring and Badges
description: 高度なスコアの設定
seo-description: Setting up advanced scoring
uuid: 3854b668-729a-42b8-b7cd-5d5ec1ca8380
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.4/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 42fb3c50-8728-4897-ade9-6b839294a10e
role: Admin
exl-id: c9406aae-288e-4cdf-ac01-cb26b423639e
source-git-commit: a70f874ad7fcae59ee4c6ec20e23ffb2e339590b
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---

# 高度なスコアとバッジ {#advanced-scoring-and-badges}

## 概要 {#overview}

高度なスコアでは、メンバーをエキスパートとして識別するためのバッジを授与できます。 高度なスコアリングでは、数量に基づいてポイントを割り当てます *および* メンバーが作成したコンテンツの品質。一方、基本スコアでは、作成したコンテンツの量に基づいてポイントを割り当てます。

この違いは、スコアの計算に使用されるスコアリングエンジンによるものです。 基本スコアエンジンは、単純な計算を適用します。 高度なスコアエンジンは、トピックの自然言語処理 (NLP) を通じて推測される、価値のある関連コンテンツに貢献するアクティブなメンバーに対して報酬を与えるアダプティブなアルゴリズムです。

コンテンツの関連性に加えて、スコアリングアルゴリズムは、投票や回答の割合など、メンバーのアクティビティを考慮に入れます。 基本的なスコアリングには定量的なものも含まれますが、高度なスコアリングではアルゴリズム的に使用されます。

したがって、高度なスコアエンジンでは、分析を意味のあるものにするのに十分なデータが必要です。 作成されるコンテンツの量と品質に応じてアルゴリズムが継続的に調整されるので、エキスパートになるための達成度のしきい値は、常に再評価されます。 また、 *減衰* メンバーの古い投稿の エキスパートメンバーが、事前に決定した時点で、エキスパートの地位を得た問題への参加を停止した場合 ( [スコアエンジンの設定](#configurable-scoring-engine)) エキスパートとしての地位を失う可能性があります。

高度なスコアの設定は、基本的なスコアとほぼ同じです。

* 基本的なスコアと高度なスコアおよびバッジルールは次のとおりです。 [コンテンツに適用済み](implementing-scoring.md#apply-rules-to-content) 同じように
   * 基本スコアと高度なスコアおよびバッジルールを同じコンテンツに適用できる
* [コンポーネントのバッジの有効化](implementing-scoring.md#enable-badges-for-component) 汎用

スコアルールとバッジルールの設定に違いは次のとおりです。

* 設定可能な高度なスコアエンジン
* 高度なスコアルール：
   * `scoringType` に設定 **[!UICONTROL 詳細]**
   * ストップワードが必要

* 高度なバッジルール：
   * `badgingType` に設定 **[!UICONTROL 詳細]**
   * `badgingLevels` 賞に対するエキスパートレベルの数を設定
   * 必要 `badgingPaths` しきい値の代わりのバッジの配列配列配列がポイントとバッジをマッピングします

>[!NOTE]
>
>高度なスコアおよびバッジ機能を使用するには、 [エキスパート特定パッケージ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg).

## 設定可能なスコアエンジン {#configurable-scoring-engine}

高度なスコアエンジンは、高度なスコアアルゴリズムに影響を与えるパラメーターを持つ OSGi 設定を提供します。

![chlimage_1-260](assets/chlimage_1-260.png)

* **[!UICONTROL スコア付けの重み付け]**
トピックの場合、スコアの計算時に最も優先度が高い動詞を指定します。 1 つ以上のトピックを入力できますが、次に限定されます **1 つの話題に対する 1 つの動詞**. 詳しくは、 [トピックと動詞](implementing-scoring.md#topics-and-verbs).

   次の形式で入力 `topic,verb` コンマはエスケープされます。 例：

   `/social/forum/hbs/social/forum\,ADD`

   デフォルトでは、Q&amp;A とフォーラムコンポーネントの ADD 動詞が設定されています。


* **[!UICONTROL スコアリング範囲]**

   高度なスコアの範囲は、この値（可能な最大スコア）と 0（可能な最小スコア）で定義されます。

   デフォルト値は 100 なので、スコアリング範囲は 0 ～ 100 です。


* **[!UICONTROL エンティティの減衰時間間隔]**

   このパラメーターは、すべてのエンティティのスコアが低下するまでの時間数を表します。 これは、コミュニティサイトのスコアに古いコンテンツを含めなくなるために必要です。

   デフォルト値は216000時間（24 年以内）です。


* **[!UICONTROL スコア付け成長率]**

   スコアを指定します。 0 からスコア範囲の間。この値を超えると、成長が遅くなり、エキスパートの数が制限されます。

   デフォルト値は 50 です。

## 高度なスコアルール {#advanced-scoring-rules}

基本スコアでは、バッジの獲得に必要な数がわかっています。

高度なスコアリングでは、必要な量は、システム内の品質データの量に基づいて、常に調整されます。 スコアは、ベルカーブと同様の方法で継続的に計算されます。

メンバーがアクティブでなくなったトピックに関するエキスパートバッジを獲得した場合、時間の経過と共に減衰が原因でバッジが失われる可能性があります。

### ScoringType {#scoringtype}

スコア付けルールは、スコア付けサブルールのセットで、それぞれが `scoringType`.

高度なスコアエンジンを呼び出すには、 `scoringType`は、次のように設定する必要があります。 `advanced`.

詳しくは、 [スコアサブルール](implementing-scoring.md#scoring-sub-rules).

![chlimage_1-261](assets/chlimage_1-261.png)

### ストップワード {#stopwords}

高度なスコアリングパッケージでは、stopwords ファイルを含む設定フォルダーがインストールされます。

* `/etc/community/scoring/configuration/stopwords`

高度なスコアアルゴリズムは、ストップワードファイルに含まれる単語のリストを使用して、コンテンツの処理中に無視される一般的な英語の単語を識別します。

このファイルが変更される可能性はありません。

ストップワードファイルがない場合、高度なスコアエンジンはエラーをスローします。

## 高度なバッジルール {#advanced-badging-rules}

高度なバッジルールのプロパティは、 [基本的なバッジルールのプロパティ](implementing-scoring.md#badging-rules).

ポイントをバッジ画像に関連付ける代わりに、許可されるエキスパートの数と、授与するバッジの画像を特定するだけで済みます。

![chlimage_1-262](assets/chlimage_1-262.png)

| **プロパティ** | **タイプ** | **値の説明** |
|---------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| badgingPath | 文字列[] | （必須）badgingLevels の数までのバッジ画像の複数値文字列。 バッジ画像のパスを並べ替える必要があるので、最初の画像は最も高いエキスパートに与えられます。 badgingLevels で指定した数より少ないバッジが存在する場合、配列の最後のバッジが残りの配列を補完します。 例：/etc/community/badging/images/expert-badge/jcr:content/expert.png |
| badgingLevels | Long | （オプション）与える専門知識のレベルを指定します。 例えば、エキスパートとほぼエキスパート（2 つのバッジ）が必要な場合は、値を 2 に設定します。 badgingLevel は、badgingPath プロパティにリストされるエキスパート関連のバッジ画像の数に対応している必要があります。 初期設定は 1 です。 |
| badgingType | 文字列 | （必須）スコアリングエンジンを「basic」または「advanced」として識別します。 &quot;advanced&quot;に設定し、それ以外の場合、デフォルトは&quot;basic&quot;です。 |
| scoringRules | 文字列[] | （オプション）バッジルールを、リストされたスコアルールで識別されるスコアイベントに制限する複数値の文字列。例：/etc/community/scoring/rules/adv-comments-scoringDefault は、制限なしです。 |

## 含まれるルールとバッジ {#included-rules-and-badge}

### 含まれるバッジ {#included-badge}

このベータリリースには、報酬ベースのエキスパートバッジが 1 つ含まれます。

* 専門家

   `/etc/community/badging/images/expert-badge/jcr:content/expert.png`

![chlimage_1-263](assets/chlimage_1-263.png)

エキスパートバッジをアクティビティの報酬として表示するには、次の 2 つの点が必要です。

* `badges` フォーラムや Q&amp;A コンポーネントなど、機能に対して有効にする必要があります
* 高度なスコアルールとバッジルールを、コンポーネントが配置されているページ（または上位ページ）に適用する必要があります

以下の基本情報を参照してください。

* [コンポーネントのバッジの有効化](implementing-scoring.md#enable-badges-for-component)
* [ルールの適用](implementing-scoring.md#apply-rules-to-content)

### 含まれるスコアルールとサブルール {#included-scoring-rules-and-sub-rules}

ベータリリースには、 [フォーラム機能](functions.md#forum-function) （フォーラム機能のフォーラムおよびコメントコンポーネントごとに 1 つずつ）:

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

**メモ：**

* 両方 `rules`および `sub-rules` ノードはタイプです `cq:Page`
* `subRules` は String 型の属性です[] 規則の `jcr:content` ノード
* `sub-rules` は、様々なスコアルールで共有できます
* `rules` はリポジトリの場所に配置し、全員に対して読み取り権限を付与する必要があります
   * ルール名は、場所に関係なく一意である必要があります

### 含まれるバッジルール {#included-badging-rules}

このリリースには、 [高度なフォーラムおよびコメントのスコアリングルール](#included-scoring-rules-and-sub-rules).

* /etc/community/badging/rules/adv-comments-badging
* /etc/community/badging/rules/adv-forums-badging

**メモ：**

* `rules` ノードはタイプです `cq:Page`
* `rules`はリポジトリの場所に配置し、全員に対して読み取り権限を付与する必要があります
   * ルール名は、場所に関係なく一意である必要があります
