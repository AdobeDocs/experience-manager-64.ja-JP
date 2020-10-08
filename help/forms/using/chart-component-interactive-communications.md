---
title: インタラクティブ通信内でグラフを使用する
seo-title: インタラクティブ通信内のグラフコンポーネント
description: 'インタラクティブ通信内でグラフを使用すると、大量の情報を、分析が簡単で理解しやすい視覚的な形式で表現することができます  '
seo-description: AEM Forms には、インタラクティブ通信内でグラフを作成するためのグラフコンポーネントが用意されています。ここでは、グラフコンポーネントの基本的な設定とエージェント設定について説明します。
uuid: dedd670c-030b-4497-bbcb-3ad935cebcda
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: interactive-communications
discoiquuid: 16c7e698-258d-4e63-9828-f538dc7d3294
translation-type: tm+mt
source-git-commit: f86765084981cda1e255834bf83be0ff8a7a2a02
workflow-type: tm+mt
source-wordcount: '2423'
ht-degree: 47%

---


# インタラクティブ通信内でグラフを使用する {#using-charts-in-interactive-communications}

インタラクティブ通信内でグラフを使用すると、大量の情報を、分析が簡単で理解しやすい視覚的な形式で表現することができます

表やグラフはデータを視覚的に表現します。インタラクティブ通信で大量の情報を分かりやすい視覚的な形式で表現することにより、複雑なデータを視覚的に理解して分析することができます。

インタラクティブ通信を作成する際にグラフを追加することにより、インタラクティブ通信のフォームデータモデルから取得した 2 次元のデータを視覚的に表現することができます。グラフコンポーネントを使用すると、次のタイプのグラフの追加、設定ができます。

* 円グラフ
* 列
* ドーナツグラフ
* 棒グラフ（Web チャネルの場合のみ）
* 線グラフ
* 線とポイントグラフ
* ポイントグラフ
* 領域

## Add and configure chart in an Interactive Communication {#add-and-configure-chart-in-an-interactive-communication}

次の手順を実行して、対話型通信にグラフを追加します。

1. AEM のサイドバーにあるグラフコンポーネントを、インタラクティブ通信の印刷チャネルまたは Web チャネルにドラッグアンドドロップします。

   * 印刷チャネル:ターゲット領域と画像フィールド
   * Web チャネル：パネルとターゲット領域

   グラフコンポーネントをドロップすると、グラフ用のプレースホルダーが作成されます。

1. Tap the chart component in the Interactive Communication editor and from the Component toolbar select **[!UICONTROL Configure (]** ![configure_icon](assets/configure_icon.png)).

   グラフの基本プロパティがフォーカスされた状態で、プロパティサイドバーが表示されます。

   ![印刷チャネルの線グラフの基本プロパティ](assets/chart_basicproperties.png)
   **図：***印刷チャネルの折れ線グラフの基本プロパティ*

   ![Web チャネルの線グラフの基本プロパティ](assets/basicpropertieswebchannel.png)
   **図：***Webチャネルーの折れ線グラフの基本プロパティ*

1. 印刷チャネルと Web チャネルのグラフの基本プロパティを設定します。両方のチャネルで共通して使用されるプロパティのほかに、各チャネル固有のプロパティとグラフタイプ固有のプロパティも用意されています。

   * **[!UICONTROL 名前]**:グラフオブジェクトの名前。 ここで指定するグラフの名前は、グラフの出力には表示されませんが、グラフを参照するルールで使用されます。
   * **[!UICONTROL グラフの種類]**:グラフのタイプを指定します。円グラフ、列グラフ、ドーナツグラフ、線グラフ、線グラフ、線とポイントグラフ、ポイントグラフ、または領域グラフです。
   * **[!UICONTROL オブジェクトを非表示]**:最終出力でグラフを非表示にする場合に選択します。
   * **[!UICONTROL X 軸]**&#x200B;と **[!UICONTROL Y 軸]**&#x200B;で、以下のプロパティを指定します。

      * **[!UICONTROL タイトル]**:対話型通信に表示するX軸とY軸のタイトルを指定します。
      * **[!UICONTROL データモデルオブジェクト*]**：インタラクティブ通信の作成時に指定したフォームデータモデルの X 軸と Y 軸について、データモデルオブジェクトを参照して選択します。グラフのX軸とY軸にプロットするために、互いに関連して意味のある、同じ親データモデルオブジェクトの2つのコレクション型/配列型プロパティを選択します。
      * **[!UICONTROL 関数]**:統計関数を使用して軸の値を計算するには、X/Y軸の関数を選択します。 For more information about functions, see [Use functions in chart](#usefunction) and [Example 2: Application of sum and mean functions in a line chart](#applicationsumfrequency).

   >[!NOTE]
   >
   >印刷チャネルの X 軸でデータモデルオブジェクトを連結する場合、そのデータモデルオブジェクトのデータタイプは、Number、String、Date のいずれかでなければなりません。印刷チャネルの Y 軸でデータモデルオブジェクトを連結する場合、そのデータモデルオブジェクトのデータタイプは Number でなければなりません。印刷チャネルの右側に表示されている凡例を使用することをお勧めします。

   For more information on chart properties, see [Basic properties in charts](#basicpropertiescharts).

1. （印刷チャネルの場合のみ）「エージェント設定」で、このグラフをエージェントで使用するかどうかを指定します。If i **[!UICONTROL t Is Mandatory For the Agent To Use This Chart]** option is not selected, the agent can tap the eye icon for the chart in the Content tab of Agent UI to show/hide the chart.

   ![chart_agentproperties](assets/chart_agentproperties.png)

1. プロパティサイドバーで、 ![done_iconをタップします](assets/done_icon.png)。

   グラフのプレビューを表示して、グラフの外観とデータを確認します。必要な場合は、グラフのプロパティをさらに編集します。

1. インタラクティブ通信の編集画面に戻り、必要な変更を行います。

## 例 1：印刷チャネルと Web チャネルのグラフ出力 {#chartoutputprintweb}

「基本」タブで、グラフのタイプ、データを格納するソースフォームデータモデルのプロパティ、グラフの X 軸と Y 軸上に描画されるラベルを指定します。必要に応じて、グラフ上に表示される値を計算するための統計関数を指定することもできます。

ここでは、インタラクティブ通信を使用して生成されたクレジットカードの取引明細を例として、基本的なプロパティに関して最低限知っておくべき情報について説明します。具体的な例として、取引明細に記載されている様々な支払額を描画するグラフを生成する場合を考えてみます。この例では、インタラクティブ通信の印刷出力と Web 出力で、異なるタイプのグラフを使用します。

最初に、以下のプロパティを指定する必要があります。

* **[!UICONTROL グラフのタイプ]**：この例では、印刷チャネルで列グラフを生成し、Web チャネルでドーナツグラフを生成します。
* **[!UICONTROL データモデルオブジェクト]**：グラフの X 軸と Y 軸上に描画されるデータの取得元を指定します。この例では、X 軸に支払額を表示し、Y 軸に支出項目名を表示します。
* **[!UICONTROL タイトル]**：X 軸と Y 軸のタイトルを指定します（この例では、印刷チャネルの列グラフでのみ、このオプションを指定します）。この例では、X 軸のタイトルを「Amount ($)」、Y 軸のタイトルを「Expense」とします。
* **[!UICONTROL ラベルの方向]** (この例では印刷チャネルの列の種類のグラフのみ) — この例では `Tilt Left`

* **[!UICONTROL 経費の上にマウスを移動すると表示されるツールチップ]** (Webチャネルのみ) — この例では、 `${x}: $ ${y}``[Expense Label: $ Amount]` (例：テーマパーク訪問：$ 315)

![Interactive Communication](assets/chartprintchannel.png)**Figureの印刷出力の列グラフ：***対話型通信の印刷出力の列グラフ*

**A.** Y軸 — フォームデータモデルのプロパティから取得した金額、およびタイトルプロパティを金額($)に設定した金額($) **B.** X軸の方向をティルト左 **C.** X軸 — フォームデータモデルのプロパティから取得した費用の説明とタイトルプロパティを経費に設定

![Interactive Communication](assets/chartwebchannel.png)**FigureのWeb出力のドーナツグラフ：***対話型通信のWeb出力におけるドーナツグラフ*

**A.ドーナツの内側の半径プロパティが設定されてい** ます。 **B.** 凡例を表示プロパティが選択され、凡例の位置プロパティが右 **Cに設定されています。** ツールチップには、マウスを合わせたときの項目の詳細が表示されます。ツールチップは${x}に設定されます。${y}

## 例 2: 線グラフ内で Sum 関数と Frequency 関数を適用する {#applicationsumfrequency}

グラフ内で関数を適用すると、フォームデータモデルでは直接指定できないデータを描画することができます。この例では、クレジットカード明細の例を使用して、合計と頻度の関数をグラフに適用する方法を理解します。

![3つの「Bed and Breakfast」トランザクション](assets/creditcarddatalinechartcopy.png)**図を含む関数を持たない折れ線グラフ：***3つの「Bed and Breakfast」トランザクションを含む関数を持たない折れ線グラフ*

### Sum 関数 {#sum-function}

Sum 関数を適用することにより、同じデータプロパティの複数のインスタンスの値を合計し、グラフ上で 1 つの項目として表示することができます。例えば以下のグラフの場合、Y 軸に Sum 関数を適用すると、3 つの「Bed and Breakfast」項目の金額が合計され（それぞれの金額は、99.45 ドル、78 ドル、12 ドル）、1 つの項目としてグラフに表示されます（合計金額は 189.45 ドル）。

同じデータプロパティで複数のインスタンスが存在する場合は、Sum 関数を適用して合計値を表示すると、グラフが見やすくなります。

![creditcardchartmfunctioncopy](assets/creditcardchartsumfunctioncopy.png)

### Frequency 関数 {#frequency-function}

Frequency 関数をグラフに適用すると、X 軸に表示される項目の発生数が Y 軸に表示されます（またはその逆）。例えば、Frequency 関数を Y 軸に適用する（Amount/TransAmount）と、「Bed and Breakfast」項目の値が Y 軸上で「3」として表示され、残りの項目についてはすべて「1」として表示されます。

![creditcardcharterfrequencyfunctioncopy](assets/creditcardchartfrequencyfunctioncopy.png)

## Basic properties in charts {#basicpropertiescharts}

「基本」タブでは、次のプロパティを設定できます。

**名前** ：グラフ要素の識別子。 ここで指定した名前はグラフには表示されませんが、他のコンポーネント、スクリプト、SOM 式を参照する際にこの名前を使用すると便利です。

**タイトル(印刷チャネルのみ)** ：グラフのタイトルを指定します。

**グラフの種類** ：生成するグラフの種類を指定します。 有効なオプションは、円グラフ、列グラフ、ドーナツグラフ、棒グラフ（Web チャネルの場合のみ）、線グラフ、線とポイントグラフ、ポイントグラフ、領域グラフです。詳しくは、例1を参照してください。印刷およびWebでのグラフの出力。

**X軸/タイトル** :X軸のタイトルを指定します。

**X軸/データモデルオブジェクトマップ(&amp;ast);** X軸にプロットするフォームデータモデルのコレクション項目の名前を指定します。

**X軸/関数** :x軸の値の計算に使用する統計/カスタム関数を指定します。 関数の詳細については、「グラフでの関数の使用」および例2を参照してください。折れ線グラフでの合計関数と平均関数の適用

**X軸/ラベルの方向** — グラフ上のラベルの方向(印刷チャネル)。 ラベルの方向を[カスタム回転]として選択すると、[カスタム回転角度（度）]フィールドが表示されます。 「カスタム回転の角度（度）」フィールドでは、回転角度を 15 度単位で選択することができます。

**Y軸/タイトル** :Y軸のタイトルを指定します。

**Y軸/データモデルオブジェクトマップ(&amp;ast);** Y軸にプロットするフォームデータモデルのコレクション項目を指定します。 印刷チャネルでは、Y軸のデータモデルオブジェクトのタイプは数値である必要があります。

**Y軸/関数** :Y軸の値の計算に使用する統計/カスタム関数を指定します。 関数の詳細については、「グラフでの関数の使用」および例2を参照してください。折れ線グラフでの合計関数と平均関数の適用

**凡例を表示** ：有効な場合、円グラフまたはドーナツグラフの凡例を表示します。

**凡例の位置** ：グラフに対する凡例の位置を指定します。 使用できるオプションは、右端、左端、上、下です。

**高さ(印刷チャネルのみ)** グラフの高さ（ピクセル単位）。

**幅(印刷チャネルのみ)** ：グラフの幅（ピクセル単位）。

>[!NOTE]
>
>Web チャネルのグラフの幅については、スタイルレイヤーを使用するかテーマを適用して調整することができます。

**ツールチップ(Webチャネルのみ)** Webチャネルーのグラフ内のデータポイントにマウスを置くと、ツールチップが表示される形式を指定します。 デフォルト値は\${x}(\${y})です。 グラフのタイプに応じて、グラフ内のポイント、棒、スライスにマウスを置くと、変数\${x}と\${y}がx軸とy軸の対応する値に動的に置き換えられ、ツールチップに表示されます。

ツールヒントを無効にするには、「ツールヒント」フィールドを空白にします。このオプションは線グラフと領域グラフには適用できません。For example, see [Example 1: Chart output in print and web](#chartoutputprintweb).

**CSSクラス(Webチャネルのみ)** 「CSSクラス」フィールドにCSSクラスの名前を指定し、カスタムスタイルをグラフに適用します。

**前に必須の改ページ(印刷チャネルのみ)** ：必須の改ページをグラフの前に追加し、グラフを新しいページの先頭に配置する場合に選択します。

**次の後に必須の改ページ(印刷チャネルのみ)** ：必須の改ページをグラフの後に追加し、グラフの後ろの内容を新しいページの先頭に配置する場合に選択します。

**インデント(印刷チャネルのみ)** ：ページの左側のグラフのインデントを指定します。

**グラフ固有の設定** ：一般的な設定に加えて、次のグラフ固有の設定を使用できます。

* **内半径**：ドーナツグラフで使用できます。グラフ内の内側の円の半径をピクセルで指定できます。
* **線の色**：線グラフ、線とポイントグラフ、領域グラフで使用できます。グラフ内の線の色を 16 進値で指定できます。
* **点の色**:ポイントグラフと線グラフとポイントグラフで使用でき、グラフ内のポイントの色を16進値で指定できます。

* **領域の色**:面グラフで使用できます。グラフ内の線の下の領域の色を16進値で指定できます。

## グラフでの関数の使用 {#usefunction}

統計関数を使用するようにグラフを設定し、ソースデータの値を計算して、グラフにプロットできます。グラフ内で関数を適用すると、フォームデータモデルでは直接指定できないデータを描画することができます。

グラフコンポーネントにはいくつかの関数が組み込まれていますが、自分で関数を作成し、その関数を使用して Web チャネルのグラフを設定することもできます

![機能図](assets/functionchart.png)

>[!NOTE]
>
>関数はグラフの X 軸の値を計算する場合にも、Y 軸の値を計算する場合にも使用できます。

### デフォルトの関数 {#default-functions}

デフォルトでは、以下の関数をグラフコンポーネントに使用できます。

**平均（平均）** ：一方の軸にある特定の値のX軸またはY軸の値の平均を返します。

**[合計** ]一方の軸にある特定の値のX軸またはY軸のすべての値の合計を返します。

**[最大値** ]一方の軸にある特定の値のX軸またはY軸の最大値を返します。

**[頻度** ]一方の軸にある特定の値のX軸またはY軸の値の数を返します。

**[範囲** ]一方の軸にある特定の値のX軸またはY軸の最大値と最小値の差を返します。

**[中央値** ]一方の軸にある特定の値のX軸またはY軸の値を上半分と下半分に分ける値を返します。

**[最小** ]一方の軸にある特定の値のX軸またはY軸の最小値を返します。

**[モード** ]一方の軸にある特定の値のX軸またはY軸で最も多く出現する値を返します。

### Custom functions in web channel {#custom-functions-in-web-channel}

グラフでデフォルトの関数を使用するだけでなく、JavaScript™ でカスタム関数を作成し、Web チャネル用のグラフコンポーネントの関数リストにその関数を追加することもできます。

関数は入力された配列または値、カテゴリ名を使用して、値を返します。次に例を示します。

```
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

カスタム関数を作成したら、以下を実行してグラフの設定で使用できるようにします。

1. 該当するインタラクティブ通信に関連付けられているクライアントライブラリにカスタム関数を追加します。For more information, see [Configuring the Submit action](/help/forms/using/configuring-submit-actions.md) and [Using Client-Side Libraries](/help/sites-developing/clientlibs.md).

1. To display the custom function in Function drop-down, in CRXDe Lite, create an `nt:unstructured` node in the apps folder with the following properties:

   * Add property `guideComponentType` with value as `fd/af/reducer`. (mandatory)
   * Add property `value` to a fully qualified name of the custom JavaScript™ function. （必須）に設定し、その値をMultiplyなどのカスタム関数の名前に設定します。
   * Add property `jcr:description` with the value you want to display as the name of the custom function that appears in the Function drop-down. 例えば、**Multiply** と表示されます。
   * Add property `qtip` with value that will be short description of the custom function. 「**関数**」ドロップダウンリスト内の関数名にポインターを置くと、ここで指定した説明がツールヒントとして表示されます。

1. 「**すべて保存**」をクリックして設定を保存します。

これで関数をグラフで使用できるようになります。