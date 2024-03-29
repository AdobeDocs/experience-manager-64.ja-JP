---
title: WCAG 2.0 のクイックガイド
seo-title: Quick Guide to WCAG 2.0
description: WCAG 2.0 のアクセシビリティに関するガイドラインの概要を簡単に説明します。
seo-description: Read a quick overview of the WCAG 2.0 accessibility guidelines.
uuid: a5cf463e-89e9-4cc0-9c91-69a1fd3d8ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/MANAGING
topic-tags: managing-accessibility
content-type: reference
discoiquuid: 3cac0e34-7514-48ce-a93b-592bbdbcd252
exl-id: 80edcd53-bc3c-4f61-8dfb-c592e7e51f60
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1708'
ht-degree: 48%

---

# WCAG 2.0 のクイックガイド{#quick-guide-to-wcag}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

AEMは、Web コンテンツのアクセシビリティガイドラインに対するコンプライアンスを最大限に高めるように開発されました。

この [Web コンテンツアクセシビリティガイドラインバージョン 2.0 (WCAG2)](https://www.w3.org/TR/WCAG/) は、 [World Wide Web Consortium(W3C)](https://www.w3.org/) 彼らの [Web Accessibility Initiative(WAI)](https://www.w3.org/WAI/).

WCAG 2.0 は、障害のあるユーザーが web コンテンツにアクセスして利用できるようにするための、テクノロジーから独立した一連のガイドラインおよび達成基準で構成されます。これらのガイドラインでは、Web コンテンツの作成者、デザイナー、開発者を対象として、視覚障碍、難聴、学習障碍、加齢に伴う制限をはじめとする障碍の種類に関係なく、できるだけ多くの人ができるだけ容易にアクセスできるようなリソースを作成するようアドバイスしています。

例えば、HTML の `alt` 属性を使用して画像（またはその他のテキスト以外のコンテンツ）を説明すると、視覚障碍または弱視の人にとって大きな助けとなります。`alt` 属性内のテキストの説明は、音声出力に変換したり、電子的に再生可能な点字ディスプレイに転送したりすることができます。

また、WCAG 2.0 は、*状況的問題*&#x200B;を抱える人などにも恩恵があります。ブラウズテクノロジー、ネットワーク接続速度、ブラウズ環境などの環境が原因で、障碍を抱える人と同じような障壁に直面することもあります。

Adobe Experience Manager を使用すると、コンテンツ作成者や Web サイトの所有者は、関連する WCAG 2.0 レベル A およびレベル AA の達成基準を満たす Web コンテンツを作成できます。

したがって、WCAG 2.0 の目的とガイドラインの構造を理解することは、Web アクセシビリティについて理解したり、ガイドラインを参考にアクセスしやすい Web コンテンツを作成したりするうえで重要です。

WCAG 2.0 の目的は次のようなガイドラインを提供することです。

* 次に該当 **テクノロジーに依存しない：**

   つまり、ガイドラインはHTMLだけでなく、様々な Web コンテンツ形式に適用できます。 つまり、WCAG 2.0 では、PDF、Flash、JavaScript、およびその他の最新／将来の Web テクノロジーによって生成または提供されるコンテンツをカバーしています。この目的は、WCAG 1.0 が他の Web コンテンツ形式を犠牲にしてHTMLに重点を置いているという点で、WCAG 1.0 の認識済みの弱点に対処することです。

* 次に該当 **テスト可能：**

   各ガイドラインは、客観的にテストできるように記述され、アクセシビリティの専門家グループがガイドラインの遵守に一般的に同意するように記述されています。 アクセシビリティガイドラインの課題の 1 つは、技術的にテスト可能なものもあれば、ガイドラインに正しく準拠しているかどうかの判断が人間に委ねられる場合もあることです。WCAG 2.0 は、WCAG 1.0 の一部のガイドラインおよびチェックポイントに存在する主観性を減らすために記述されています。

* **優先度の高いコンテキスト実装**&#x200B;をサポート

   WCAG 1.0 と同様に、WCAG 2.0 のガイドラインは優先事項に基づいており、障碍を持つ特定のユーザーグループに対してガイドラインに従わない場合の影響の可能性に関してです。 これにより、作成者は、特定の状況下で最も重要となるガイドラインを十分な情報から判断することができます。また、*アクセシビリティサポート*&#x200B;の概念が導入されました。そのため、作成者は、アクセシビリティサポートが完全ではない Web テクノロジーを最大限に生かす方法を判断したり、アクセシビリティ機能の恩恵を受けられるように、特定の支援テクノロジーまたはブラウザーを使用するようユーザーに要求したりすることができます。

これらの目的は、WCAG 2.0 の構造に大きく影響しています。

>[!NOTE]
>
>考えられるあらゆる障碍、またはあらゆるタイプの人を考慮に入れた Web サイトを作成することは不可能です。WCAG 2.0 の目的は、Web 作成者が、特定の条件下かつ妥当な範囲内で可能な限り容易にアクセスできるサイトを作成できるようにすることです。

>[!NOTE]
>
>WCAG 1.0 に詳しい方は、WCAG 2.0 にいくつかの変更があることに気付くかもしれません。これらは、範囲、組織、目的に関連しています。

## 構造 {#structure}

WCAG 2.0 は、アクセスしやすい Web コンテンツの作成の概念について段階的に詳しく紹介するように構成されています。この点から、WCAG 2.0 は相互に接続された非常に複雑なドキュメントセットであるという印象を受けますが、詳細情報を 1 つの非常に大きなドキュメントでまとめて提供するのではなく、作成者が必要とするときに（段階的に）提供することを目的としています。

WCAG 2.0 は、アクセシブルなデザインの 4 つの主要な原則で構成されています。 以下が該当します。

1. **知覚可能**:ユーザーは問題の Web コンテンツを感知できますか？
1. **操作可能**:ユーザーはナビゲートやデータ入力をおこなったり、web コンテンツとやり取りしたりできますか。
1. **理解可能**:ユーザーは、自分に提示された web コンテンツを処理し、理解することができますか？
1. **堅牢**:Web コンテンツは、従来のブラウズ環境や新しいブラウズ環境を含む、適切に幅広いブラウジング環境で意図した方法で利用できますか？

これらの原則は、略して「POUR」と呼ばれる場合があります。

* 各 **原則** 1 つ以上の **ガイドライン**.

   * ガイドラインは指示として表現され、正 (Do this...) または負 (Do not do this...) のどちらかです。
   * ガイドラインには 1.1 ～ 4.1 の番号が付けられます。最初の番号は親の原則に対応します。

* 各ガイドラインは、1 つ以上の **達成基準**.

   * 達成基準は、特定の Web ページに対して `True` または `False` のいずれかの表現で記述されています。
   * 達成基準には、選択肢または選択肢を含めることも、例外を含めることもできます。達成基準を満たす必要がない状況。
   * 達成基準には、親のガイドラインおよび原則に従って 1.1.1 ～ 4.1.1 の番号が付けられます。また、基準の意図を要約した短い名前が付けられ、参照が容易になります。 例えば、達成基準 1.1.1 は非テキストの代替値です。
   * 達成基準には、関連する&#x200B;**テクニック**&#x200B;のリストが含まれています（詳しくは、後述の説明を参照）。

## サポートリソース {#supporting-resources}

WCAG 2.0 のコアコンポーネントである原則、ガイドライン、および達成基準とは別に、一連のサポートドキュメントが用意されています。これらの中には、ガイドラインの各側面に準拠する方法を具体的にアドバイスするものもあれば、様々な能力を持つ Web 作成者、デザイナー、および開発者が WCAG 2.0 を理解し、できるだけ効果的に使用するのに役立つ一般的な参考資料もあります。

WCAG 2.0 は不変のドキュメントであり、変更されることはありませんが、これらのサポートリソースのほとんどは動的なドキュメントであり、今後、新興テクノロジーが登場したり、Web アクセシビリティの達成方法について新たな例が見つかったりした場合、内容が改訂および追加されていきます。

### WCAG 2.0 リソース {#wcag-resources}

* [WCAG 2.0 に関連するすべてのドキュメントの概要](https://www.w3.org/WAI/intro/wcag.php);
* [異なるコンポーネントが相互にどのように関係しているかの説明](https://www.w3.org/WAI/intro/wcag20);
* [WCAG 2.0 に関するよくある質問](https://www.w3.org/WAI/WCAG20/wcag2faq.html);

### WCAG 2.0 の各種テクニック {#techniques-for-wcag}

WCAG 2.0 の各種テクニックを「[Techniques for WCAG 2.0](https://www.w3.org/TR/WCAG20-TECHS/)」ページで参照できます。

これらの&#x200B;**テクニック**&#x200B;は、WCAG 2.0 階層の達成基準の下位レベルを構成するものです。これらは、WAI により、規範としてではなく、参考情報として分類されています。つまり、リソースを WCAG 2.0 に準拠させる際に、特定のテクニックに必ずしも従う必要はありません。

テクニックは達成基準よりもはるかに具体的なので、通常は特定のテクノロジーやコンテンツタイプ (HTMLやビデオなど )、状況（e コマースや e ラーニングアプリケーションなど）を指します。 テクニックは、特定のガイドラインや達成基準を満たす方法に関する実証済みの例と考えることができるので、特定のコンテキストで作業する作成者や開発者にとって役立ちます。

次の方法にアクセスできます。

* コレクションから（テクニックは一般的なものもあれば、HTML、CSS、クライアント側スクリプティングなど、特定のテクノロジーや形式に関連するものもあります）。
* 関連する達成基準から。 テクニックは複数の達成基準に適用できます。

各テクニックには、コレクションに関連する一意の番号が割り当てられます。 例えば、ARIA テクニックの 1 つは、 *テクニック ARIA2:「必須」プロパティを使用した必須フィールドの識別*.

テクニックは、「Sufficience」、「Advisory」、「Failure」のいずれかです。

* *十分なテクニック*&#x200B;は、従うと、特定の達成基準を十分に満たすことができます。
* *参考テクニック*&#x200B;は、従うと、アクセシビリティにプラスの影響を与えますが、それだけでは特定の達成基準を満たすのに十分ではない可能性があります。
* *失敗テクニック*&#x200B;は、達成基準を満たすことができない特定の例を示すものです。

テクニックの詳細には、説明、適用、例、詳細情報のリソース、および作成者がテストして技術の適用を成功に導く方法の詳細が含まれます。

テクニックのリストは完成しておらず、WAI は常に新しい例でリストを更新しています。これは、Web 技術の開発、設計アプローチ、研究結果を反映しています。 したがって、新しい追加に関するテクニックのリストを定期的に確認する価値があります。

### WCAG 2.0 の理解 {#understanding-wcag}

これは、一連のドキュメントを指し、読者が特定のガイドラインや達成基準の目的を正しく理解するのに役立つアドバイスを提供します。 以下が可能です。 [概要と詳細情報へのリンクをダウンロード](https://www.w3.org/TR/2008/NOTE-UNDERSTANDING-WCAG20-20081211/Overview.html).

個々のガイドラインと達成基準にも、次の情報を提供する独自の「理解」ページがあります。

* ガイドラインの意図
* 特定の達成基準
* ガイドラインの要件を満たすのに役立つが、特定の達成基準に該当しない助言テクニック。

各達成基準の個々の「理解」ページには、次の情報が表示されます。

* 達成基準の意図；
* 達成基準を満たす方法の一般的な例；
* 達成基準の達成方法に関する関連リソース（W3C 以外）
* テクニックと失敗：達成基準を満たす方法を具体的かつ詳細に示す例（詳しくは、後述の説明を参照）
* 主要用語：達成基準を理解するうえで重要となる用語集

「[Understanding Success Criterion 1.1.1 (&quot;Non-text content&quot;)](https://www.w3.org/TR/2008/NOTE-UNDERSTANDING-WCAG20-20081211/text-equiv-all.html)」に例が紹介されています。

### WCAG 2.0 に準拠する方法 {#how-to-meet-wcag}

「[How To Meet WCAG 2.0](https://www.w3.org/WAI/WCAG20/quickref/)」ページには、ガイドラインに準拠するための方法を示す節があります。この節では、WCAG を別の形式で示し、ガイドラインの内容を読者の興味や状況に最も関連する内容に絞り込むことができます。 Readerは、カスケーディングスタイルシートやスクリプティングなどの特定の Web コンテンツテクノロジーを指定したり、特定の優先度を指定したりすることで、表示する達成基準手法をフィルタリングできます。

フィルタリングをおこなわない場合、このリソースでは、すべての成功基準をガイドライン別にグループ化して提供します。 達成基準ごとに、次の情報が表示されます。

* 達成基準のテキスト。
* 対応する「理解」ドキュメントへのリンク
* 関連する十分なテクニックのリスト。各テクニックの詳細へのリンク。
* 関連するアドバイザリテクニックのリスト。各テクニックの詳細（存在する場合）へのリンク。
* 関連するエラーのリスト（各エラーの詳細へのリンク）。
