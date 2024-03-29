---
title: フォームのコンバージョン率の測定と効率性の改善
seo-title: Measure and improve effectiveness and conversion of forms
description: AEM Formsは、Adobe TargetおよびAdobe Analyticsのソリューションと統合されており、フォームのパフォーマンスとコンバージョン率を測定および改善できます。
seo-description: AEM Forms integrates with Adobe Target and Adobe Analytics solutions that allows you to measure and improve the performance and conversion rate of your forms.
uuid: 5876f2f3-1c97-4fb9-a032-b869ee3c6a45
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: integrations
discoiquuid: 6b62b280-d101-410a-ba8c-02940f766c32
exl-id: 364dd7f3-9009-440e-8aff-28e2dac08fe7
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 29%

---

# フォームのコンバージョン率の測定と効率性の改善 {#measure-and-improve-effectiveness-and-conversion-of-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 課題 {#the-challenge-br}

今日、組織はますます顧客の裁量を拡大し、複数チャンネルにまたがるデジタルのセルフサービス経由で取引を行うことを推奨しています。ただし、1 対 1 のフィードバックメカニズムがない場合は、デジタルフォームを測定して実験し、顧客体験を向上させ、コンバージョンを増やすのが困難になります。

ROI を最大化するには、組織は、顧客がサービスとどのようにやり取りするかを監視し、顧客体験を強化するためにデジタルアーティファクト（フォーム）を試す必要があります。 成功を測定し、改善戦略を定義するには、組織は次のような質問に対する回答が必要です。

* フォームを使用してアクセスまたは取引を試みた顧客の数は？
* トランザクションを正常に完了した顧客の数は？
* フォームを破棄した人の数は？
* お客様が問題に直面している問題領域は何ですか。
* どのような変更を加え、何がコンバージョンの改善につながるのかをテストするには、どうすればよいですか？

## 解決策 {#the-solution}

AEM Forms は、[Adobe Marketing Cloud](https://www.adobe.com/jp/marketing-cloud.html) ソリューション（[Adobe Analytics](https://www.adobe.com/jp/marketing-cloud/web-analytics.html) と[Adobe Target](https://www.adobe.com/jp/marketing-cloud/testing-targeting.html)）に統合されているため、フォームのパフォーマンスをモニタリングして分析し、コンバージョン率を上げるためのエクスペリエンスを開発することができます。

## ワークフロー {#the-workflow}

フォームのパフォーマンスを測定し、コンバージョン率を向上させる方法の詳細について説明します。

### ターゲットオーディエンス {#target-audience}

* マーケティング戦略と成功を担当するビジネスユーザーとアナリスト
* インフラストラクチャとソリューションのセットアップとメンテナンスを担当する IT スタッフ

### 関連するAEM Formsのコンポーネントと機能 {#aem-forms-components-and-features-involved}

* アダプティブフォーム
* Adobe Analytics との統合（顧客がアダプティブフォームをどのように利用しているかについて、情報の収集、整理、レポートを行う）
* Adobe Targetとの統合により、アダプティブフォームで A/B テストを実行

### 前提 {#assumptions}

* Adobe Marketing Cloud アカウントを所有し、Analytics および Taget ソリューションに登録済みであること。
* 顧客がアクセスできる発行済みのアダプティブフォームがあります。

### ワークフロー手順 {#workflow-steps}

#### 手順 1：AEM Forms で Analytics および Target を設定 {#step-configure-analytics-and-target-in-aem-forms-br}

**Analytics の設定**

顧客がフォームでどのような操作を行っているかに関する深いインサイトを得るには、まずAEM Formsで Analytics を設定する必要があります。 以下の手順を実行します。

1. Adobe Analytics でのレポートスイートの作成
1. AEM でクラウドサービス設定の作成
1. AEM でクラウドサービスのフレームワーク作成
1. AEM で AEM Forms Analytics Configuration サービスを設定
1. AEM でフォームの Analytics を有効化

手順について詳しくは、[アダプティブフォームの分析とレポートの設定](/help/forms/using/configure-analytics-forms-documents.md)を参照してください。

**Target の設定**

アダプティブフォームで A/B テストを作成および実行するには、[AEM Forms での Target の設定と統合](/help/forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p)を参考にして AEM Forms で Target を設定してください。

#### 手順 2：分析レポートの表示 {#step-view-analytics-report-br}

Analytics を有効にしたフォームに顧客がアクセスし、やり取りすると、そのやり取りは高度にセキュリティ保護された Analytics データベースに取り込まれます。 データベースはクライアント別にセグメント化され、安全な接続を介してアクセスできます。

AEMで分析が有効なフォームに関するレポートを表示し、データを分析することができます。 レポートを表示するには：

1. AEMサーバーで、に移動します。 **Forms / Formsとドキュメント**.
1. 分析レポートを表示するフォームを選択します。
1. 「 Analytics レポート」アイコンをクリックします。 レポートが表示されます。

フォームで Analytics が収集し、レポートするデータポイントを見てみましょう。

**Forms analytics レポート**

アダプティブフォームの分析レポートでは、フォームレベルで次の KPI（主要業績評価指標）が取り込まれます。

* **平均記入時間**:フォームの記入に費やした平均時間
* **インプレッション数**：検索結果にフォームが表示された回数

* **レンディション**：フォームがレンダリングされた、または開かれた回数
* **ドラフト**:フォームがドラフトとして保存された回数

* **送信**:フォームが送信された回数
* **中止**:フォームが完了せずに離脱した回数
* **訪問回数/送信回数**:送信あたりの訪問数の割合

さらに、フォーム内の各パネルに関する次の詳細を取得できます。

* **時間**：パネルとパネル内のフィールドに費やした平均時間（秒）

* **エラー**：フォームのレンダリング 1000 回ごとの、パネルとパネル内のフィールドでのエラー発生回数

* **ヘルプ**：フォームのレンダリング 1000 回ごとの、パネルとパネル内のフィールドでユーザーがコンテキスト内ヘルプにアクセスした回数

![アダプティブフォームのサンプル分析レポート](assets/summary-report.png)

分析レポートの詳細については、「[AEM Forms の分析レポートの確認方法と詳細](/help/forms/using/view-understand-aem-forms-analytics-reports.md)」を参照してください。

>[!NOTE]
>
>Adobe Marketing Cloud の Analytics アカウントで詳細なレポートを表示することにより、顧客がフォームをどのように利用しているかについて詳しく分析することができます。

#### 手順 3：データポイントの分析 {#step-analyze-data-points}

この手順では、分析レポートのデータポイントを分析し、フォームのパフォーマンスを推測します。 成功 KPI を満たさない場合は、データに基づいて仮説を作成し、問題を修正するための解決策を見つけます。 次に例を示します。

* フォームの平均記入時間が予想よりも長い場合は、フォームが複雑で顧客にとって理解しにくく、フォームで標準の用語が使用されていない、フォームが長すぎるなどの可能性があります。 この場合、フォームの構造とフィールドの簡略化、フォームデザインの再作業、フォームの長さの短縮、非標準のフォームフィールドに関するヘルプの説明や例の追加などを行うことができます。
* ほとんどの顧客がフォームパネルのヘルプにアクセスしていることをデータが示している場合は、入力する情報について困惑していることが明らかです。 別の用語を使用する場合や、そのパネルに入力例やヘルプ説明を追加する場合があります。
* フォームの中止または中断率が予想より高い場合は、フォームのレンダリングに時間がかかる、顧客が誤ってフォームにランディングした、または複雑すぎるなどの理由が考えられます。 この場合、検索結果に表示されるフォームの説明を最適化したり、フォームを簡略化したり、読み込み速度を上げるためにフォームを最適化したりすることができます。

これらのデータポイントを分析し、仮説に辿り着いたら、必要な変更をフォームに加えます。

#### 手順 4:分析と修正点を検証する {#step-validate-your-analysis-and-fixes}

この手順では、フォームに加えた変更を検証し、コンバージョン率に影響があるかどうかを確認します。

**A/B テストの実行**

AEM Formsと Target を統合すると、アダプティブフォームの A/B テストを作成できます。 A/B テストでは、フォームの様々なエクスペリエンスをリアルタイムでランダムに顧客に提示し、どのエクスペリエンスが効果が高いか、またはより多くのコンバージョンを引き起こすかを把握します。 1 つのエクスペリエンスが他のエクスペリエンスよりも優れたコンバージョンを提供することを示す重要なデータが得られたら、そのエクスペリエンスを勝者として宣言し、今後は、すべての顧客に表示されるデフォルトエクスペリエンスになります。

アダプティブフォームの A/B テストの作成について詳しくは、 [アダプティブフォームの A/B テスト](/help/forms/using/ab-testing-adaptive-forms.md).

![アダプティブフォームの A/B テストのサマリーレポート例](assets/ab-test-report-2.png)

## ベストプラクティス {#best-practices}

実際のベストプラクティスは、このワークフローを実行する際に自分で特定するものです。 お客様の環境と要件に応じて異なります。 ワークフローを通じて学習を取り込み、ベストプラクティスとして文書化します。

フォームのデザインと A/B テストの実行に関する推奨事項を以下に示します。

**Formsデザイン**

* フォームはシンプルで短く、簡単に移動できます。 ナビゲーション用に方向指示キューを使用すること。
* フォームフィールドに標準的または一般的な用語を使用すること。
* ユーザーが間違いやすいところには、例示やヘルプなどでフィールドおよび入力必須箇所に説明を加えること。
* フォーム送信時のエラーを避けるために、可能な限りユーザー入力を入力時に検証します。
* デスクトップおよびモバイルデバイス用のレイアウトを最適化します。
* 既知のユーザーの情報を自動入力します。

**A/B テスト**

* A/B テストを実行する前に仮説を作成し、成功指標を特定してください。
* 代替エクスペリエンスで最小限のバリエーション（理想的には一度に 1 つ）を実行して、コンバージョン率への影響を把握します。
* 頻繁にテストを実施して非効率性を排除します。
