---
title: アダプティブフォームの操作のベストプラクティス
seo-title: Best practices for working with adaptive forms
description: AEM Formsプロジェクトの設定、アダプティブフォームの開発、AEM Formsシステムのパフォーマンスの最適化のベストプラクティスについて説明します。
seo-description: Explains best practices for setting up an AEM Forms project, developing adaptive forms, and optimizing the performance for AEM Forms system.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
feature: Adaptive Forms
exl-id: 0c64940c-273d-4f23-afcb-38bf54cddd36
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '4144'
ht-degree: 33%

---

# アダプティブフォームの操作のベストプラクティス {#best-practices-for-working-with-adaptive-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## 概要 {#overview}

Adobe Experience Manager（AEM）Forms を使用すると、複雑なトランザクションを単純で使いやすいデジタルエクスペリエンスに変えることができます。ただし、効率的で生産的なAEM Formsエコシステムを実装、構築、実行、維持するためには、多大な取り組みが必要です。

ここでは、フォーム管理者、フォーム作成者、開発者がAEM Forms、特にアダプティブフォームコンポーネントを扱う際に知っておくべきガイドラインや推奨事項を紹介します。 フォーム開発プロジェクトの設定から、AEM Formsの設定、カスタマイズ、オーサリング、最適化に至るまで、ベストプラクティスを説明します。 これらのベストプラクティスを実行することで、AEM Formsのエコシステム全体のパフォーマンスを向上できます。

また、AEM の一般的なベストプラクティスについて、以下をお読みになることもお勧めします。

* [ベストプラクティス：AEM のデプロイおよび維持](/help/sites-deploying/best-practices.md)
* [ベストプラクティス：コンテンツのオーサリング](/help/sites-authoring/best-practices.md)
* [ベストプラクティス：AEM の管理](/help/sites-administering/administer-best-practices.md)
* [ベストプラクティス：ソリューションの開発](/help/sites-developing/best-practices.md)

## AEM Formsのセットアップと設定 {#set-up-and-configure-aem-forms}

### フォーム開発プロジェクトの設定 {#setting-up-forms-development-project}

プロジェクト構造の簡素化と標準化により、開発やメンテナンスの作業を大幅に削減できます。 AEMプロジェクトの構築には、Apache Maven がオープンソースツールとして推奨されます。

* Apache Maven `aem-project-archetype` を使用して、AEM プロジェクトの構造を作成および管理します。AEM プロジェクトに合わせて、推奨される構造およびテンプレートを作成します。さらに、ビルドを自動化し、変更制御システムを提供するので、プロジェクト管理が容易になります。

   * Maven `archetype:generate` コマンドを使用して、最初の構造を生成します。
   * Maven `eclipse:eclipse` コマンドを使用して eclipse プロジェクトファイルを生成し、プロジェクトを eclipse 内に読み込みます。

詳しくは、[Apache Maven を使用して AEM プロジェクトをビルドする方法](/help/sites-developing/ht-projects-maven.md)を参照してください。

* FileVault ツールまたは VLT は、CRX またはAEMインスタンスのコンテンツをファイルシステムにマッピングする際に役立ちます。 AEMプロジェクトコンテンツのチェックインやチェックアウトなど、変更管理の操作を行うことができます。 [VLT ツールの使用方法](/help/sites-developing/ht-vlttool.md)を参照してください。

* Eclipse 統合開発環境を使用する場合は、AEM Developer Tools を使用して、Eclipse IDE をAEMインスタンスとシームレスに統合し、AEMアプリケーションを作成できます。 詳しくは、 [AEM developer tools for Eclipse](/help/sites-developing/aem-eclipse.md).

### オーサリング環境の計画 {#planning-for-authoring-environment}

AEMプロジェクトを設定したら、アダプティブフォームのテンプレートおよびコンポーネントのオーサリングとカスタマイズの方法を定義します。

* アダプティブフォームテンプレートは、アダプティブフォームの構造とヘッダーとフッターの情報を定義する専用のAEMページです。 テンプレートには、アダプティブフォームのレイアウト、スタイル、基本構造が事前に設定されています。 AEM Formsには、アダプティブフォームの作成に使用できる標準のテンプレートとコンポーネントが用意されています。 ただし、必要に応じて、カスタムのテンプレートやコンポーネントを作成できます。 アダプティブフォーム内で必要となる追加のテンプレートやコンポーネントの要件を収集することをお勧めします。 詳しくは、 [アダプティブフォームおよびコンポーネントのカスタマイズ](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* AEM Formsでは、次のフォームモデルに基づいてアダプティブフォームを作成することができます。 フォームモデルは、フォームとAEMシステムとの間でデータを交換するためのインターフェイスとして機能し、アダプティブフォーム内外のデータフローに XML ベースの構造を提供します。 また、フォームモデルは、スキーマと XFA 制約の形式でアダプティブフォームにルールと制約を適用します。

   * **なし**:このオプションで作成されたアダプティブフォームは、フォームモデルを使用しません。 このようなフォームで生成されるデータ XML は、フィールドと対応する値を持つフラットな構造です。
   * **XML または JSON スキーマ**：XML スキーマと JSON スキーマは、組織内のバックエンドシステムによって生成されて使用されるデータの構造を表します。アダプティブフォームにスキーマを関連付け、そのスキーマの要素を使用することにより、アダプティブフォームに動的なコンテンツを追加することができます。スキーマの要素は、アダプティブフォームを作成する際に、コンテンツブラウザーの「データモデルオブジェクト」タブで使用できます。スキーマ要素をドラッグ＆ドロップしてフォームを作成できます。
   * **XFA フォームテンプレート**:XFA ベースの Forms5 に投資している場合、これは理想的なフォームHTMLです。 XFA ベースのフォームをアダプティブフォームに直接変換する方法を提供します。 既存の XFA ルールは、関連するアダプティブフォーム内でも保持されます。 作成されたアダプティブフォームは、検証、イベント、プロパティ、パターンなどの XFA 構成をサポートします。
   * **フォームデータモデル**：データベース、web サービス、AEM ユーザープロファイルなどのバックエンドシステムを統合し、アダプティブフォームに事前入力して、送信されたフォームデータをバックエンドシステムに再び書き込む場合は、このフォームモデルが適しています。フォームデータモデルエディターを使用すると、アダプティブフォームの作成に使用できるフォームデータモデル内のエンティティやサービスを定義して設定することができます。 詳しくは、 [AEM Forms Data Integration](/help/forms/using/data-integration.md).

データモデルを選択する際には、要件に適合するかどうかだけでなく、すでに XFA および XSD アセットに投資をしている場合、それらの既存の投資を拡張できるかどうかを考慮することが重要です。生成される XML はスキーマで定義された XPATH に従ったデータを含むため、XSD モデルを使用してフォームテンプレートを作成することをお勧めします。フォームデータモデルのデフォルトの選択肢として XSD モデルを使用すると、データの処理や消費を行うバックエンドシステムからデザインを切り離し、1 対 1 のフォームフィールドマッピングによりフォームのパフォーマンスを向上させるのに役立ちます。 また、フィールドの BindRef は、XML でそのデータ値の XPATH にすることができます。

詳しくは、 [アダプティブフォームの作成](/help/forms/using/creating-adaptive-form.md).

* アダプティブフォームには、共通するセクションがいくつかあります。 これらを特定し、コンテンツの再利用を促進する戦略を定義できます。 アダプティブフォームを使用すると、スタンドアロンフラグメントを作成して、複数のフォームで再利用することができます。 アダプティブフォーム内のパネルをフラグメントとして保存することもできます。 フラグメント内の変更は、関連するすべてのフォームに反映されます。 これにより、オーサリング時間を短縮し、フォーム間の一貫性を確保できます。 また、フラグメントを使用するとアダプティブフォームが軽量になるので、特に大きなフォームのオーサリングエクスペリエンスが向上します。 詳しくは、[アダプティブフォームフラグメント](/help/forms/using/adaptive-form-fragments.md)を参照してください。

### アダプティブフォームおよびコンポーネントのカスタマイズ {#customize-components}

* AEM Formsには、アダプティブフォームの作成に使用できる、標準のアダプティブフォームテンプレートが用意されています。 また、独自のテンプレートを作成することもできます。 AEMには、静的および編集可能なテンプレートが用意されています。

   * 静的テンプレートは、開発者が定義し、設定します。
   * 編集可能テンプレートは、作成者がテンプレートエディターを使用して作成します。 テンプレートエディターを使用して、テンプレートの基本的な構造と初期コンテンツを定義できます。 構造レイヤーでの変更は、そのテンプレートを使用するすべてのフォームに反映されます。 初期コンテンツには、事前設定済みのテーマ、事前入力サービス、送信アクションなどが含まれる場合があります。 ただし、フォームエディターを使用して、フォームに対してこれらの設定を変更することはできます。 詳しくは、[アダプティブフォームテンプレート](/help/forms/using/template-editor.md)を参照してください。

* 特定のフィールドやパネルインスタンスにスタイルを設定するには、[インラインスタイル](/help/forms/using/inline-style-adaptive-forms.md)を使用します。または、CSS ファイルでクラスを定義し、コンポーネントの CSS クラスプロパティでクラス名を指定します。
* コンポーネントにクライアントライブラリを含めると、そのコンポーネントを使用するアダプティブフォームやフラグメント全体で一貫してスタイルを適用できます。 詳しくは、 [アダプティブフォームのページコンポーネントの作成](/help/forms/using/custom-adaptive-forms-templates.md).
* クライアントライブラリで定義されたスタイルを適用し、アダプティブフォームコンテナプロパティの「 CSS ファイルパス」フィールドでクライアントライブラリへのパスを指定して、アダプティブフォームを選択します。
* スタイルのクライアントライブラリを作成するには、テーマエディターの基本 clientlib またはフォームコンテナのプロパティで、カスタム CSS ファイルを設定します。
* アダプティブフォームには、レスポンシブ、タブ付き、アコーディオン、ウィザードなどのパネルレイアウトが用意されており、フォームコンポーネントをパネルにレイアウトする方法を制御できます。 カスタムパネルレイアウトを作成して、フォーム作成者が使用できるようにすることができます。 詳しくは、[アダプティブフォームのカスタムレイアウトコンポーネントの作成](/help/forms/using/custom-layout-components-forms.md)を参照してください。
* また、フィールドやパネルレイアウトなど、アダプティブフォームの特定のコンポーネントをカスタマイズすることもできます。

   * 以下を使用： [オーバーレイ](/help/sites-developing/overlays.md) コンポーネントのコピーを変更するAEMの機能。 デフォルトのコンポーネントを変更することはお勧めしません。
   * /libs 内の既製のアダプティブフォームコンポーネントのレイアウトをカスタマイズするには、次の手順を実行します。 [カスタムレイアウトコンポーネントの作成](/help/forms/using/custom-layout-components-forms.md) に加えて [デフォルトレイアウト](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * カスタムウィジェットや外観を作成して、カスタムインタラクティビティを導入します。 デフォルトのコンポーネントを変更することはお勧めしません。 詳しくは、 [外観フレームワーク](/help/forms/using/introduction-widgets.md).

* PII データの取り扱いに関する推奨事項については、[個人を特定できる情報の取り扱い](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p)を参照してください。

## アダプティブフォームの作成 {#author-adaptive-forms}

### オーサリングにタッチ操作向け UI を使用 {#using-touch-optimized-ui-for-authoring}

* フォーム階層の下位にあるフィールドにすばやくアクセスするには、サイドバーのオブジェクトブラウザーを使用します。検索ボックスを使用してフォームまたはオブジェクトツリー内のオブジェクトを検索し、オブジェクト間を移動することができます。
* サイドバーのコンポーネントブラウザーでコンポーネントのプロパティを表示して編集するには、コンポーネントを選択して ![cmppr-1](assets/cmppr-1.png) をクリックします。コンポーネントをダブルクリックして、そのプロパティをプロパティブラウザーに表示することもできます。
* フォームに対するクイックアクションを実行するには、キーボードショートカットを使用します。 [AEM Forms のキーボードショートカット](/help/forms/using/keyboard-shortcuts.md)を参照してください。

* アダプティブフォームのコンポーネントは、アダプティブフォームのページでのみ使用することをお勧めします。 コンポーネントは、親階層に依存します。 このため、AEM ページではこれらのコンポーネントを使用しないでください。

また、 [アダプティブフォームのオーサリングの概要](/help/forms/using/introduction-forms-authoring.md).

### アダプティブフォームでのルールの使用 {#using-rules-in-adaptive-forms}

AEM Forms [ルールエディター](/help/forms/using/rule-editor.md) これにより、アダプティブフォームのコンポーネントに動的な動作を追加するルールを作成できます。 これらのルールを使用すると、条件を評価し、フィールドの表示または非表示、値の計算、ドロップダウンリストの動的な変更など、コンポーネントへのアクションをトリガーできます。

ルールエディターには、ルールを記述するためのビジュアルエディターとコードエディターが用意されています。 コードエディターモードを使用してルールを記述する際は、次の点を考慮してください。

* ルールを記述する際に競合が発生する可能性を避けるために、フォームフィールドとコンポーネントに意味のある一意の名前を付けます。
* ルールの式で、コンポーネント自身を参照するには、コンポーネントの `this` 演算子を使用します。これにより、コンポーネント名が変更されても、ルールは有効なままになります。例えば、`field1.valueCommit script: this.value > 10` のようになります。

* 他のフォームコンポーネントを参照する場合には、コンポーネント名を使用します。フィールドまたはコンポーネントの値を取得するには、`value` プロパティを使用します。例えば、`field1.value` のようになります。

* 競合を回避するために、コンポーネントは固有の相対階層で参照します。例えば、`parentName.fieldName` のようになります。

* 複雑なルールや共通で使用するルールを扱う場合には、指定してアダプティブフォーム間で再利用できる別のクライアントライブラリの機能としてビジネスロジックを書くことを検討します。クライアントライブラリは独立のライブラリとし、jQuery および Underscore.js 以外の外部依存はなくす必要があります。クライアントライブラリは、送信されたフォームデータの[サーバーサイドの再検証](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form)を実行するために使用することもできます。
* アダプティブフォームは、アダプティブフォームとの通信やアクションの実行に使用できる一連の API を提供します。 主な API の一部を次に示します。 詳しくは、 [アダプティブFormsの JavaScript ライブラリ API リファレンス](https://adobe.com/go/learn_aemforms_documentation_63_jp).

   * `guideBridge.reset()`：フォームをリセットします。
   * `guideBridge.submit()`：フォームを送信します。
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`：フィールドにフォーカスを設定します。
   * `guideBridge.validate(errorList, somExpression, focus)`：フォームを検証します。
   * `guideBridge.getDataXML(options)`：フォームデータを XML として取得します。
   * `guideBridge.resolveNode(somExpression)`：フォームオブジェクトを取得します。
   * `guideBridge.setProperty(somList, propertyName, valueList)`：フォームオブジェクトのプロパティを設定します。
   * 上記に加えて、以下のフィールドプロパティを使用できます。

      * `field.value` でフィールドの値を変更します。
      * f`ield.enabled` でフィールドを有効／無効にします。
      * `field.visible` でフィールドの表示／非表示を変更します。

* アダプティブフォームの作成者は、フォーム内でビジネスロジックを構築するために JavaScript コードを記述する必要が生じる場合があります。 JavaScript は強力で効果的ですが、セキュリティ上の期待に基づいて妥協する可能性が高くなります。 したがって、フォーム作成者が信頼できるペルソナであることと、フォームを実稼動環境に配置する前に JavaScript コードを確認して承認するプロセスがあることを確認する必要があります。 管理者は、役割や機能に基づいて、ルールエディターへのアクセスをユーザーグループに制限できます。 詳しくは、 [選択したユーザーグループにルールエディターへのアクセスを許可する](/help/forms/using/rule-editor-access-user-groups.md).
* ルール内で式を使用して、アダプティブフォームを動的にすることができます。 すべての式は有効な JavaScript 式で、アダプティブフォームのスクリプティングモデル API を使用します。 これらの式は、特定のタイプの値を返します。数式およびベストプラクティスについて詳しくは、[アダプティブフォームの式](/help/forms/using/adaptive-form-expressions.md)を参照してください。

### テーマの操作 {#working-with-themes}

アダプティブフォームテーマを使用すると、フォーム間で適用して、見た目とスタイルを一貫させる再利用可能なスタイルを作成できます。 テーマを使用してフォームコンポーネントやパネルのスタイル設定を定義することをお勧めします。テーマに関するベストプラクティスの一部を次に示します。

* テキストスタイル、背景、画像をすばやく適用するには、アセットライブラリを使用します。 スタイルがアセットライブラリに追加されると、他のテーマでも、フォームエディターのスタイルモードで使用できます。
* ページレベルのセレクターを使用して、フォントやページの背景などのグローバル設定を適用します。
* クライアントライブラリを使用して、既存のスタイル設定や高度なスタイル設定をテーマに読み込みます。
* フォームスタイルレイヤー内の特定のフィールド、パネル、ボタンにスタイル設定を上書きできます。
* テーマがスタイル設定の要件を満たさない場合は、guideFieldNode、guideFieldLabel、guideFieldWidget、guidePanelNode などの事前定義済みのクラスを使用して、フォーム間で共通のスタイルを適用できます。

詳しくは、 [テーマ](/help/forms/using/themes.md).

### 大規模フォームと複雑なフォームのパフォーマンスの最適化 {#optimizing-performance-of-large-and-complex-forms}

通常、フォーム作成者とエンドユーザーは、オーサリングモードで、または実行時に、大きなフォームを読み込む際にパフォーマンスの問題に直面します。 フォーム内のオブジェクト（フィールドやパネル）の数が増えると、オーサリングとランタイムのエクスペリエンスは低下し始めます。 また、複数の作成者が共同作業したり、フォームを同時に作成するのを防ぎます。

大規模フォームのパフォーマンスの問題を解決するには、次のベストプラクティスを検討してください。

* 可能な場合には、XFA をアダプティブフォームに変換する場合でも、XSD フォームデータモデルを使用してアダプティブフォームを作成することをお勧めします。
* アダプティブフォームには、ユーザーからの情報を取り込むフィールドとパネルのみを含めます。 静的コンテンツを最小限に抑えるか、URL を使用してそれらを別のウィンドウで開くことを検討します。
* すべてのフォームは特定の目的のために設計されていますが、ほとんどのフォームには一般的なセグメントがいくつかあります。 例えば、個人の詳細、住所、雇用の詳細などです。 フォームの共通の要素およびセクションに対して[アダプティブフォームフラグメント](/help/forms/using/adaptive-form-fragments.md)を作成し、それらを複数のフォーム間で使用します。既存のフォーム内のパネルをフラグメントとして保存することもできます。 フラグメント内の変更は、関連するすべてのアダプティブフォームに反映されます。 これにより、複数の作成者が同時に、1 つのフォームを構成する別のフラグメントの作業を行えるため、オーサリングの共同作業が促進されます。

   * アダプティブフォームと同様に、フラグメント固有のスタイル設定とカスタムスクリプトはすべて、フラグメントコンテナダイアログを使用してクライアントライブラリで定義することをお勧めします。 また、外部のオブジェクトに依存しない自己十分なフラグメントを作成してみてください。
   * クロスフラグメントスクリプティングの使用は避けます。 フラグメントの外部に参照する必要があるオブジェクトがある場合は、そのオブジェクトを親フォームの一部にしてみます。 オブジェクトが別のフラグメントに存在する必要がある場合は、スクリプト内でその名前で参照します。

* 自動保存で「保存と再開」を使用すると、アダプティブフォームが定期的に保存され、後で再度訪問してフォームを完了することができます。
* フラグメントの読み込みを遅延的に設定します。 遅延読み込みとマークされたフラグメントは、実行時に必要な場合にのみレンダリングされます。 大きなフォームの場合、読み込み時間が大幅に短縮されます。 また、繰り返し可能なパネルを持つフラグメントでもサポートされています。 詳しくは、 [遅延読み込みの設定](/help/forms/using/lazy-loading-adaptive-forms.md).

   * レスポンシブグリッドレイアウトのフラグメントや最初のパネルでは、遅延読み込みを設定しないでください。
   * ファイル添付および利用条件コンポーネントは、遅延読み込みフラグメントではサポートされません。
   * 遅延読み込み済みパネルの値を「値を使用」としてマークします。その値がフォームの他の部分で使用されている場合は、その値が、含まれているパネルがアンロードされたときに使用できるようになります。
   * 条件に基づいて表示または非表示する必要があるフラグメントに対して、表示ルールを記述することを検討します。

### アダプティブフォームの事前入力 {#prefilling-adaptive-forms}

バックエンドから取得したデータをアダプティブフォームフィールドに事前に入力することで、ユーザーがすばやくフォームに入力して入力したり、入力の間違いを防ぐことができます。

* AEM Formsには、事前定義済みのデータ XML ファイルからデータを読み取り、事前入力 XML ファイル内のコンテンツをアダプティブフォームのフィールドに事前入力するための事前入力サービスが用意されています。
* 事前入力データ XML は、アダプティブフォームに関連付けられたフォームモデルのスキーマに準拠している必要があります。
* 事前入力 XML には「`afBoundedData`」および「`afUnBoundedData`」セクションを含めて、アダプティブフォームの連結されたフィールドと連結されていないフィールドのどちらにも事前入力するようにします。

* フォームデータモデルに基づいたアダプティブフォームの場合、AEM Forms にはすぐに使用できるフォームデータモデルの事前入力サービスが用意されています。事前入力サービスは、アダプティブフォーム内のデータモデルオブジェクトに対してデータソースに対してクエリを実行し、フォームのレンダリング時にフィールド値を事前入力します。
* アダプティブフォームでは、ファイル、crx、サービス、または http プロトコルを事前入力することもできます。
* AEM Formsは、OSGi サービスとしてプラグインしてアダプティブフォームに事前入力できる、カスタム事前入力サービスをサポートしています。

詳しくは、[アダプティブフォームフィールドの事前入力](/help/forms/using/prepopulate-adaptive-form-fields.md)を参照してください。

### アダプティブフォームへの署名と送信 {#signing-and-submitting-adaptive-forms}

アダプティブフォームでは、ユーザーが指定したデータを処理するために送信アクションが必要です。 送信アクションとは、アダプティブフォームを使って送信されるデータに対して実行されるタスクを決定するものです。

* アダプティブフォームには、初期設定済みの複数の送信アクションがあります。詳しくは、[送信アクションの設定](/help/forms/using/configuring-submit-actions.md)を参照してください。
* デフォルトの送信アクションが実際のユースケースに適していない場合は、カスタム送信アクションを作成できます。詳しくは、[アダプティブフォーム向けのカスタム送信アクションの作成](/help/forms/using/custom-submit-action-form.md)を参照してください。
* サーバーサイドの検証を含めて、無効なデータ送信を防ぎます。

アダプティブフォームでAcrobat Signの複数署名操作を活用することができます。 アダプティブフォームでAcrobat Signを設定する際は、以下の点を考慮してください。 詳しくは、 [アダプティブフォームでのAcrobat Signの使用](/help/forms/using/working-with-adobe-sign.md).

* Acrobat Sign対応のアダプティブフォームは、すべての署名者がフォームに署名した後でのみ送信されます。 すべての署名者によりフォームが署名されるまで、フォームは「保留中の署名」状態で表示されます。
* フォーム内署名機能を設定したり、送信時に署名者を署名ページにリダイレクトしたりできます。
* 必要に応じて、順次署名または並列署名を設定します。

### レコードのドキュメントを生成中 {#generating-document-of-record}

レコードのドキュメント (DoR) は、印刷、署名、またはアーカイブが可能な、アダプティブフォームの統合PDFバージョンです。

* アダプティブフォームが基にしているフォームデータモデルに応じて、DoR 用のテンプレートを次のように設定できます。

   * **XFA フォームテンプレート**:関連する XDP ファイルを DoR テンプレートとして使用します。
   * **XSD スキーマ**:アダプティブフォームで使用されているのと同じ XML スキーマを使用する、関連する XFA テンプレートを使用します。
   * **なし**:自動生成された DoR を使用します。

* アダプティブフォームエディターの「レコードのドキュメント」タブから、ヘッダー、フッター、画像、色、フォントなどを直接設定します。
* `DoRService` を使用して、DoR をプログラムにより生成します。
* DoR から非表示フィールドを除外します。
* `afAcceptLang` リクエストパラメーターを使用して、別のロケールで DoR を表示します。

### アダプティブフォームのデバッグとテスト {#debugging-and-testing-adaptive-forms}

[AEM Chrome プラグイン](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) は、Google Chrome 用のブラウザー拡張機能で、アダプティブフォームのデバッグ用のツールを提供します。 フォーム作成者および開発者は、これらのツールを使用して次のことを実行できます。

* フォームのレンダリングのボトルネックを特定し、パフォーマンスを最適化する
* フォーム内でのキーワードと bindRef エラーのデバッグ
* ログの有効化と設定
* フォーム内のルールとスクリプトのデバッグ
* guideBridge API の参照と詳細

詳しくは、[AEM Chrome プラグイン - アダプティブフォーム](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/)を参照してください。

Calvin SDK は、アダプティブフォームをテストするためのアダプティブフォーム開発者用のユーティリティ API です。Calvin SDK は [Hobbes.js テストフレームワーク](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/test-api/index.html)上に構築されます。このフレームワークを使用して、次のテストを実行できます。

* アダプティブフォームのレンディション機能
* アダプティブフォームの事前入力エクスペリエンス
* アダプティブフォームの送信エクスペリエンス
* 式ルール
* 検証
* 遅延読み込み

詳しくは、 [アダプティブフォームのテストの自動化](/help/forms/using/calvin.md).

### AEMサーバー上のアダプティブフォームの検証 {#validating-adaptive-forms-on-aem-server}

クライアントでの検証を回避する試みや、データ送信の漏洩やビジネスルール違反の可能性を防ぐには、サーバー側の検証が必要です。 サーバー側の検証は、必要なクライアントライブラリを読み込むことで、サーバーで実行されます。

* クライアントライブラリに、アダプティブフォーム内の式を検証する関数を含め、アダプティブフォームコンテナダイアログでクライアントライブラリを指定します。 詳しくは、 [サーバー側の再検証](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* サーバーサイド検証により、フォームモデルが検証されます。検証用に別個のクライアントライブラリを作成し、同じクライアントライブラリ内でHTMLのスタイル設定や DOM 操作など他の要素と混在させないことをお勧めします。

### アダプティブフォームのローカライズ {#localizing-adaptive-forms}

AEMでは、アダプティブフォームのローカライズに使用できる翻訳ワークフローが提供されています。 詳しくは、 [AEM翻訳ワークフローを使用したアダプティブフォームのローカライズ](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

アダプティブフォームをローカライズする際のベストプラクティスの一部を次に示します。

* 複数のフォームに共通する要素に対してアダプティブフォームフラグメントを使用し、フラグメントをローカライズします。これにより、フラグメントを 1 回ローカライズするだけで、ローカライズされたフラグメントが使用されるすべてのフォームに反映されます。
* 新しいコンポーネントの追加や、ローカライズされたフォームへのスクリプトの適用などの変更は、自動的にはローカライズされません。 したがって、ローカライズを何度も行わなければならない状況を避けるには、フォームをローカライズする前に完成させる必要があります。
* ブラウザーのロケールを上書きし、指定したロケールでフォームをレンダリングするには、`afAcceptLang` 要求パラメーターを使用します。例えば、次の URL を使用すると、ブラウザー設定で指定されたロケールに関係なく、日本語ロケールでのフォームのレンダリングが強制されます。

   `https://[*server*]:[*port*]/<*contextPath*>/<*formFolder*>/<*formName*>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Formsでは現在、英語 (en)、スペイン語 (es)、フランス語 (fr)、イタリア語 (it)、ドイツ語 (de)、日本語 (ja)、ポルトガル語 — ブラジル語 (pt-BR)、中国語 (zh-TW)、韓国語 (ko-KR) の各ロケールのアダプティブフォームコンテンツのローカライゼーションをサポートしています。 ただし、アダプティブフォームの新しいロケールのサポートを実行時に追加することはできます。 詳しくは、 [アダプティブフォームのローカリゼーション用に新しいロケールをサポート](/help/forms/using/supporting-new-language-localization.md).

## 実稼動用のフォームプロジェクトを準備する {#prepare-forms-project-for-production}

### フォーム処理サーバーの追加 {#adding-forms-processing-server}

ファイアウォールの内側のセキュリティ保護されたゾーンにある、AEM Formsサーバーの追加のインスタンスを設定できます。 このインスタンスは、次の目的で使用できます。

* **バッチ処理**：反復的なジョブや、負荷の大きいバッチとしてスケジュールされるジョブ。例えば、印刷ステートメント、通信の生成、PDFジェネレーター、出力、アセンブラーなどのドキュメントサービスの使用などです。
* **PII データの保存**:PII データを処理サーバーに保存します。 PII データの保存に既にカスタムストレージプロバイダーを使用している場合は、必須ではありません。

### プロジェクトの別の環境への移動 {#moving-project-to-another-environment}

多くの場合、AEMプロジェクトを別の環境に移動する必要があります。 移動時に覚えておくべき重要な点は次のとおりです。

* 既存のクライアントライブラリ、カスタムコード、設定のバックアップを作成します。
* 製品パッケージとパッチを、新しい環境で指定した順序で手動でデプロイします。
* 新しいAEMサーバー上に、プロジェクト固有のコードパッケージとバンドルを手動で、別のパッケージまたはバンドルとしてデプロイします。
* （*JEE 上の AEM Forms のみ*）LCA および DSC を手動で Forms ワークフローサーバー上にデプロイします。
* 用途 [Export-Import](/help/forms/using/import-export-forms-templates.md) 機能を使用して、アセットを新しい環境に移動できます。 レプリケーションエージェントを設定し、アセットを公開することもできます。

### AEM の設定 {#configuring-aem}

全体的なパフォーマンスを向上させるためにAEMを設定するためのベストプラクティスの一部を次に示します。

* Felix コンソールからの JavaScript および CSS の HTML クライアントライブラリ圧縮を有効にします。
* すべてのクライアントライブラリを `/etc.clientlibs/fd` にキャッシュし、追加のカスタムクライアントライブラリを AEM ディスパッチャーにキャッシュすることで、発行したフォームの応答速度とセキュリティを向上させます。詳しくは、[ディスパッチャー](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)を参照してください。

* `/content/forms/af/` パス および `/content/dam/formsanddocuments/*` パスはキャッシュしないでください。アダプティブフォームのキャッシュ設定について詳しくは、[アダプティブフォームのキャッシュ](/help/forms/using/configure-adaptive-forms-cache.md)を参照してください。

* Web サーバーHTMLモジュールを使用して圧縮を有効にします。 詳しくは、 [AEM Formsサーバーのパフォーマンス調整](/help/forms/using/performance-tuning-aem-forms.md).
* 大規模なフォームのリクエスト設定ごとに呼び出しを増やします。 詳しくは、 [大規模フォームと複雑なフォームのパフォーマンスの最適化](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* 作成 [エラーハンドラーによって表示されるカスタムエラーページ](https://helpx.adobe.com/experience-manager/6-2/sites-developing/customizing-errorhandler-pages.html).
* AEM Forms サーバーを保護します。

   * `nosamplecontent` 実行モードを使用して、実稼働サーバーにサンプルコンテンツおよびサンプルユーザーがデプロイされていないことを確認します。[AEM の実稼動準備完了モードでの実行](/help/sites-administering/production-ready.md)を参照してください。

* ヒープサイズは 8 GB 以上にしてください。 その他の設定については、 [AEM Formsサーバーのパフォーマンス調整](/help/forms/using/performance-tuning-aem-forms.md).
* サービスレベルのタスクを実行するには、管理セッションではなく、サービスユーザーセッションを使用します。 詳しくは、 [サービス認証](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### ドラフトおよび送信済みフォームデータ用の外部ストレージの設定 {#external-storage}

実稼動環境では、送信されたフォームデータをAEMリポジトリに保存しないことをお勧めします。 送信アクション「Forms Portal Store」、「コンテンツを保存」、「PDFを保存」のデフォルト実装では、フォームデータがAEMリポジトリに保存されます。 これらの送信アクションは、デモ目的でのみ使用されます。 また、「保存して再開」機能や「自動保存」機能でも、デフォルトでポータルストレージが使用されます。このため、次の推奨事項を検討してください。

* **ドラフトデータの保存**：アダプティブフォームの「ドラフト」機能を使用している場合は、カスタムサービスプロバイダーインターフェイス（SPI）を実装して、データベースなどのより安全なストレージにドラフトデータを保存してください。詳しくは、「[ドラフト&amp;送信コンポーネントとデータベースの統合](/help/forms/using/integrate-draft-submission-database.md)」を参照してください。

* **送信データの保存**：「フォームポータル送信保存」を使用している場合は、カスタム SPI を実装してデータベースに送信データを保存してください。統合例については、[ドラフト&amp;送信コンポーネントとデータベースの統合の例](/help/forms/using/integrate-draft-submission-database.md) を参照してください。

   安全なストレージにフォームデータと添付ファイルを保存するカスタム送信アクションを作成することもできます。詳しくは、[アダプティブフォーム向けカスタム送信アクションの作成](/help/forms/using/custom-submit-action-form.md) を参照してください。

### 個人を特定できる情報の処理 {#handling-personally-identifiable-information}

組織にとっての主な課題の 1 つは、個人を特定できる (PII) データの処理方法です。 このようなデータの処理に役立つベストプラクティスの一部を次に示します。

* データベースなどの安全で外部ストレージを使用して、ドラフトフォームや送信済みフォームのデータを保存します。 [ドラフトおよび送信済みフォームのデータを格納する外部ストレージの設定](/help/forms/using/adaptive-forms-best-practices.md#external-storage)を参照してください。
* 自動保存を有効にする前に、利用条件フォームコンポーネントを使用して、ユーザーから明示的な同意を得てください。 この場合、ユーザーが利用条件コンポーネントの条件に同意した場合にのみ自動保存を有効にします。
