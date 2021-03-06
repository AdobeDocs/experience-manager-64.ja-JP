---
title: '遅延読み込みによる大きなフォームのパフォーマンスの向上 '
seo-title: Improve performance of large forms with lazy loading
description: 遅延読み込みを使用すると、フォームのフラグメントが表示されるまでそれらの初期化と読み込みを延期することにより、大きく複雑なアダプティブフォームのパフォーマンスを向上できます。
seo-description: Lazy loading significantly improves the performance of large and complex adaptive forms by deferring initialization and loading of form fragments until they are visible.
uuid: 3ead2b82-f895-4a7b-9683-495fcd94fade
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: d570ead9-8f9c-4668-8b23-e8984d9b25e9
feature: Adaptive Forms
exl-id: 92d88888-343c-4edb-9b11-8e876539573a
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 100%

---

# 遅延読み込みによる大きなフォームのパフォーマンスの向上  {#improve-performance-of-large-forms-with-lazy-loading}

## 遅延読み込みの概要 {#introduction-to-lazy-loading}

フォームが数百以上のフィールドを持ち、大きく複雑になると、エンドユーザーはフォームがレンダリングされる際に長時間待たされることになります。この応答時間を最小にするために、アダプティブフォームでは、フォームを複数の論理的なフラグメントに分解し、これらのフラグメントが表示される必要な時が来るまでそれらの初期化や読み込みを遅延するように設定できます。これを遅延読み込みと呼びます。さらに、遅延読み込みが設定されたフラグメントは、ユーザーがフォーム内の他のセクションに移動するとアンロードされ、フラグメントは表示されなくなります。

まず最初に、遅延読み込みを設定する前に、要件と準備手順を説明します。

## 遅延読み込みを設定するための準備 {#preparing-to-configure-lazy-loading}

アダプティブフォーム内のフラグメントの遅延読み込みを設定する前に、フラグメントを作成し、スクリプトで使用されたり他のフラグメントで参照されたりする値を特定し、遅延読み込みされたフラグメントの表示をコントロールするためのルールを定義するといった、戦略を定義することが重要です。

* **フラグメントの特定と作成**
遅延読み込みを設定できるのは、アダプティブフォームのフラグメントのみです。フラグメントとは、アダプティブフォームの外側にある独立したセグメントであり、フォーム間で再利用できるものです。したがって、遅延読み込みを実装するための最初の手順は、フォーム内の論理的なセクションを特定し、それらをフラグメントに変換することです。フラグメントは、最初から作成することも、または既存のフォームパネルをフラグメントとして保存することもできます。

   フラグメントの作成について詳しくは、[アダプティブフォームフラグメント](/help/forms/using/adaptive-form-fragments.md)を参照してください。

* **グローバルな値の特定とマーク付け**
フォームベースのトランザクションには、ユーザーからの適切なデータを取得し、それを処理してフォーム入力エクスペリエンスを簡素化するための動的な要素が含まれます。例えば、フォームのフラグメント X 内にフィールド A があり、その値が別のフラグメント内のフィールド B の有効性を決定するとします。この場合、フラグメント X が遅延読み込みに対してマーク付けされた場合、フィールド A の値は、フラグメント X が読み込まれていないときでも、フィールド B を検証するために利用できる必要があります。これを実現するには、フィールド A をグローバルとしてマーク付けします。これにより、その値が、フラグメント X が読み込まれていないときでもフィールド B の検証のために使用できるようになります。

   フィールド値をグローバルにする方法については、[遅延読み込みの設定](/help/forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p)を参照してください。

* **フィールドの表示をコントロールするルールの記述**
フォームには、必ずしもすべてのユーザーや条件に適用されないフィールドやセクションがいくつか含まれます。フォームの作成者や開発者は、ユーザーの入力に基づいてその表示をコントロールするために表示／非表示ルールを使用します。例えば、会社住所フィールドは、フォームの職業ステータスで無職を選択したユーザーには表示されません。ルールの作成について詳しくは、[ルールエディターの使用](/help/forms/using/rule-editor.md)を参照してください。

   遅延読み込みされたフラグメント内で表示ルールを活用して、必要な場合にのみ条件付きフィールドを表示させることができます。また、条件付きフィールドをグローバルとしてマーク付けして、遅延読み込みフラグメントの表示式内でそれを参照することもできます。

## 遅延読み込みの設定 {#configuring-lazy-loading}

次の手順を実行して、アダプティブフォームフラグメントに対して遅延読み込みを有効にします。

1. 遅延読み込みを有効にしたいフラグメントを含むアダプティブフォームをオーサリングモードで開きます。
1. アダプティブフォームフラグメントを選択して、![cmppr](assets/cmppr.png) をタップします。
1. サイドバーで、「**[!UICONTROL フラグメントを緩慢に読み込む]**」を有効にして、「**完了**」をタップします。

   ![アダプティブフォームフラグメントに対して遅延読み込みを有効にする](assets/lazy-loading-fragment.png)

   フラグメントの遅延読み込みが有効になりました。

遅延読み込みフラグメント内のオブジェクトの値をグローバルとしてマーク付けすることで、これらの値は、そのフラグメントが読み込まれていなくてもスクリプトで使用できるようになります。以下の操作を実行します。

1. アダプティブフォームフラグメントをオーサリングモードで開きます。
1. グローバルとしてマークしたい値のフィールドをタップしてから、![](assets/cmppr.png) をタップします。
1. サイドバーで、**[!UICONTROL 遅延読み込み中に値を使用]**を有効にします。
   ![サイドバーの遅延読み込みフィールド](assets/enable-lazy-loading.png)

   この値は、グローバルとしてマーク付けされ、そのフラグメントが読み込まれていないときでもスクリプト内で使用できるようになります。

## 遅延読み込みを設定するための注意点とベストプラクティス {#considerations-and-best-practices-for-configuring-lazy-loading}

遅延読み込みを使用する際に留意しておかなければならない制限事項、推奨事項および重要な点を以下に示します。

* 大きなフォームに対して遅延読み込みを設定する場合は、XFA ベースのアダプティブフォームより XSD スキーマベースのアダプティブフォームを使用することが推奨されます。XFA ベースのアダプティブフォームにおける遅延読み込みの導入によるパフォーマンスの向上は、XSD ベースのアダプティブフォームと比べ比較的小さいです。
* レスポンシブグリッドレイアウトではフラグメントに遅延読み込みを設定しないでください。パフォーマンスが低下します。
* アダプティブフォームの読み込み時に表示する最初のパネル内のフラグメントに対しては遅延読み込みを設定しないことが推奨されます。
* 遅延読み込みは、フラグメント階層の最大 2 レベルまでサポートされます。
* グローバルとして設定されたフィールドがアダプティブフォーム内で一意であることを確認してください。
* 条件に基づいて表示または非表示する必要があるフラグメントに対して、フラグメントの表示ルールを記述することを検討します。例えば、配偶者情報フラグメントは、ユーザーによって指定された婚姻ステータスに基づいて表示または非表示にできます。
* ファイル添付および利用条件コンポーネントは、遅延読み込みフラグメントではサポートされません。

### 遅延読み込みを設定するためのスクリプトに関するベストプラクティス {#scripting-best-practices-for-configuring-lazy-loading}

遅延読み込みパネル用のスクリプトの作成時に留意しておく必要のある重要な点を以下に示します。

* 遅延読み込みが設定されたフラグメントで使用される初期化および計算スクリプトは、べき等になるようにしてください。べき等のスクリプトとは、何度実行しても同じ結果になるスクリプトです。
* フィールドのグローバルに使用できるプロパティを使用して、遅延読み込みパネル内にあるフィールドの値をフォームのその他のすべてのパネルで使用できるようにしてください。
* フィールドがフラグメント間でグローバルとしてマークされているかどうかにかかわらず、遅延パネル内部のフィールドの参照値を転送しないでください。
* パネルリセット機能を使用して、パネル上で表示されているすべてのものを、以下のクリック式を使用してリセットしてください。

   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;: &quot;navigablePanel&quot;})).resetData()
