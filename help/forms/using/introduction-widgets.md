---
title: アダプティブフォームおよび HTML5 フォームの外観フレームワーク
seo-title: Appearance framework for adaptive and HTML5 forms
description: Mobile FormsはフォームテンプレートをHTML5 フォームとしてレンダリングします。 これらのフォームは、jQuery、Backbone.js および Underscore.js ファイルを外観とスクリプティングを有効にするために使用します。
seo-description: Mobile Forms render Form Templates as HTML5 forms. These forms use jQuery, Backbone.js and Underscore.js files for the appearance and to enable scripting.
uuid: 183b8d71-44fc-47bf-8cb2-1cf920ffd23a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: customization
discoiquuid: 3c2a44a7-24e7-49ee-bf18-eab0e44efa42
exl-id: 272d3ec1-7f92-4f4a-9e98-954136b20b27
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 27%

---

# アダプティブフォームおよび HTML5 フォームの外観フレームワーク {#appearance-framework-for-adaptive-and-html-forms}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

フォーム（アダプティブフォームと HTML5 フォーム）は、[jQuery](https://jquery.com/)、[Backbone.js](https://backbonejs.org/)および[Underscore.js](https://underscorejs.org/)ライブラリを外観とスクリプト作成のために使用します。このフォームはまた、フォーム内のすべての対話操作要素（例えばフィールドやボタン）に対して [jQuery UI](https://jqueryui.com/) **Widgets**&#x200B;アーキテクチャを使用します。このアーキテクチャにより、フォーム開発者は、Formsで使用可能な jQuery ウィジェットとプラグインの豊富なセットを使用できます。 また、ユーザーから leadDigits/trailDigits 制限やパターン形式文字列の実装などのデータを取得しながら、フォーム固有のロジックを実装することもできます。 フォーム開発者は、カスタムの外観を作成して使用することで、データ取得の操作性を向上させ、より使いやすくすることができます。

この記事は、jQuery ウィジェットと jQuery ウィジェットに関する十分な知識を持つ開発者向けです。 外観フレームワークに関する洞察を提供し、開発者がフォームフィールドの別の外観を作成できるようにします。

外観フレームワークは、様々なオプション、イベント (トリガー)、および関数に基づいて、フォームとのユーザーのやり取りをキャプチャし、モデルの変更に応じてエンドユーザーに通知します。 さらに、次の点に注意してください。

* フレームワークは、フィールドの外観に関する一連のオプションを提供します。 これらのオプションはキーと値のペアで、次の 2 つのカテゴリに分類されます。一般的なオプションおよびフィールドタイプ固有のオプション。
* 外観は、契約の一部として、enter や exit などの一連のトリガーを設定します。
* 一連の関数を実装するには、外観が必要です。 一般的な関数と、フィールドタイプの関数に固有の関数があります。

## 共通オプション {#common-options}

次に、グローバルオプションを設定します。 これらのオプションは、すべてのフィールドで使用できます。

<table> 
 <tbody>
  <tr>
   <th>プロパティ </th> 
   <th>説明</th> 
  </tr>
  <tr>
   <td>name</td> 
   <td>スクリプト式でこのオブジェクトまたはイベントを指定するために使用される識別子です。例えば、このプロパティはホストアプリケーションの名前を指定します。</td> 
  </tr>
  <tr>
   <td>value</td> 
   <td>フィールドの実際の値。 </td> 
  </tr>
  <tr>
   <td>displayValue</td> 
   <td>フィールドのこの値が表示されます。 </td> 
  </tr>
  <tr>
   <td>screenReaderText</td> 
   <td>画面Readerは、この値を使用して、フィールドに関する情報を読み上げます。 フォームは値を提供し、その値を上書きできます。<br /> </td> 
  </tr>
  <tr>
   <td>tabIndex</td> 
   <td>フォームのタブシーケンスにおけるフィールドの位置フォームのデフォルトタブの順序を変更する場合にのみ、tabIndex を上書きします。</td> 
  </tr>
  <tr>
   <td>役割</td> 
   <td>要素の役割（見出し、表など）。</td> 
  </tr>
  <tr>
   <td>高さ</td> 
   <td>ウィジェットの高さ。 ピクセル単位で指定します。 </td> 
  </tr>
  <tr>
   <td>width</td> 
   <td>ウィジェットの幅。 ピクセル単位で指定します。</td> 
  </tr>
  <tr>
   <td>access</td> 
   <td>サブフォームなど、コンテナオブジェクトのコンテンツにアクセスするために使用されるコントロールです。</td> 
  </tr>
  <tr>
   <td>paraStyles</td> 
   <td>ウィジェットへの XFA 要素の para プロパティ。</td> 
  </tr>
  <tr>
   <td>dir</td> 
   <td>テキストの方向。 指定できる値は、ltr（左から右）と rtl（右から左）です。</td> 
  </tr>
 </tbody>
</table>

これらのオプション以外にも、フレームワークには、フィールドのタイプに応じて異なる他のオプションがいくつか用意されています。 各フィールド固有のオプションの詳細を以下に示します。

### フォームフレームワークとのやり取り {#interaction-with-forms-framework}

フォームフレームワークとやり取りするには、ウィジェットがいくつかのトリガーを設定し、フォームスクリプトの動作を有効にします。 ウィジェットがこれらのイベントをスローしない場合、そのフィールド用にフォームで記述された一部のスクリプトは機能しません。

#### ウィジェットでトリガーされたイベント {#events-triggered-by-widget}

<table> 
 <tbody>
  <tr>
   <th>イベント </th> 
   <th>説明</th> 
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td> 
   <td>このイベントは、フィールドがフォーカスされたときにトリガーされます。 これにより、「Enter」スクリプトをフィールドに対して実行できます。 イベントをトリガーする構文は次のとおりです。<br /> （ウィジェット）を使用します。_trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td> 
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td> 
   <td>このイベントは、ユーザーがフィールドを離れるたびにトリガーされます。 これにより、エンジンはフィールドの値を設定し、その「終了」スクリプトを実行できます。 イベントをトリガーする構文は次のとおりです。<br /> （ウィジェット）を使用します。_trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td> 
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td> 
   <td>このイベントは、フィールドに記述された「変更」スクリプトをエンジンが実行できるようにトリガーされます。 イベントをトリガーする構文は次のとおりです。<br /> （ウィジェット）を使用します。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td> 
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td> 
   <td>このイベントは、フィールドがクリックされるたびにトリガーされます。 これにより、エンジンはフィールドで記述された「クリック」スクリプトを実行できます。 イベントをトリガーする構文は次のとおりです。<br /> （ウィジェット）を使用します。_trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td> 
  </tr>
 </tbody>
</table>

#### ウィジェットで実装された API {#apis-implemented-by-widget}

外観フレームワークは、カスタムウィジェットに実装されているウィジェットの関数を呼び出します。 ウィジェットは次の関数を実装する必要があります。

<table> 
 <tbody>
  <tr>
   <th>Function</th> 
   <th>説明</th> 
  </tr>
  <tr>
   <td>フォーカス：function()</td> 
   <td>フィールドにフォーカスを置きます。</td> 
  </tr>
  <tr>
   <td>クリック：function()</td> 
   <td>フォーカスをフィールドに移し、XFA_CLICK_EVENT を呼び出します。</td> 
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>erorrMessage: string </em>representing the error<br /> <em>errorType: string (“warning”/”error”)</em></p> <p><strong>注意</strong>:適用可能なのはHTML5 のフォームのみです。</p> </td> 
   <td>エラーメッセージとエラータイプをウィジェットに送信します。 ウィジェットにエラーが表示されます。</td> 
  </tr>
  <tr>
   <td><p>clearError:function()</p> <p><strong>注意</strong>:適用可能なのはHTML5 のフォームのみです。</p> </td> 
   <td>フィールドのエラーが修正された場合に呼び出されます。 ウィジェットはエラーを非表示にします。</td> 
  </tr>
 </tbody>
</table>

## フィールドのタイプに固有のオプション {#options-specific-to-type-of-field}

すべてのカスタムウィジェットは上記の仕様に準拠する必要があります。異なるフィールドの機能を使用するには、ウィジェットはその特定のフィールドのガイドラインに準拠する必要があります。

### テキスト編集：テキストフィールド {#textedit-text-field}

<table> 
 <tbody>
  <tr>
   <th>オプション</th> 
   <th>説明</th> 
  </tr>
  <tr>
   <td>multiline</td> 
   <td>フィールドが改行文字の入力をサポートする場合は true、サポートしない場合は false です。</td> 
  </tr>
  <tr>
   <td>maxChars</td> 
   <td>フィールドに入力できる最大文字数。</td> 
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>注意</strong>:HTML5 フォームのみ適用可能</p> </td> 
   <td>テキストの幅がウィジェットの幅を超えた場合のテキストフィールドの動作を指定します。</td> 
  </tr>
 </tbody>
</table>

### 選択リスト：DropDownList、ListBox {#choicelist-dropdownlist-listbox}

<table> 
 <tbody>
  <tr>
   <th>オプション</th> 
   <th>説明</th> 
  </tr>
  <tr>
   <td>value<br /> </td> 
   <td>選択した値の配列。<br /> </td> 
  </tr>
  <tr>
   <td>item<br /> </td> 
   <td>オプションとして表示するオブジェクトの配列。 各オブジェクトには、次の 2 つのプロパティが含まれます。<br /> 保存：保存、表示する値：表示する値。<br /> <br /> </td> 
  </tr>
  <tr>
   <td><p>編集可能な状態で</p> <p><strong>注意</strong>:適用可能なのはHTML5 のフォームのみです。<br /> </p> </td> 
   <td>値が true の場合、ウィジェットでカスタムテキストの入力が有効になります。<br /> </td> 
  </tr>
  <tr>
   <td>displayValue<br /> </td> 
   <td>表示する値の配列。<br /> </td> 
  </tr>
  <tr>
   <td>multiselect<br /> </td> 
   <td>複数の選択が許可される場合は true、許可されない場合は false です。<br /> </td> 
  </tr>
 </tbody>
</table>

#### API {#api}

<table> 
 <tbody>
  <tr>
   <th>Function</th> 
   <th>説明</th> 
  </tr>
  <tr>
   <td><p>addItem:<em> function(itemValues)<br /> itemValues：display と save の値が含まれているオブジェクト <br /> {sDisplayVal: &lt;displayValue&gt;, sSaveVal: &lt;save Value&gt;}</em></p> </td> 
   <td>アイテムをリストに追加します。</td> 
  </tr>
  <tr>
   <td>deleteItem<em>: function(nIndex)<br /> nIndex：リストから削除する項目のインデックス<br /> </em><br /> <br /> </td> 
   <td>リストからオプションを削除します。</td> 
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td> 
   <td>リストからすべてのオプションをクリアします。</td> 
  </tr>
 </tbody>
</table>

### 数値編集：NumericField, DecimalField {#numericedit-numericfield-decimalfield}

| オプション | 説明 |
|---|---|
| dataType | フィールドのデータタイプを表す文字列（整数/小数）。 |
| leadDigits | 10 進数で許可される最大先頭桁数。 |
| fracDigits | 10 進数で許可される最大分数桁数。 |
| ゼロ | フィールドのロケールでのゼロの文字列表現。 |
| decimal | フィールドのロケールでの小数の文字列表現。 |

### チェックボタン：ラジオボタン、チェックボックス {#checkbutton-radiobutton-checkbox}

<table> 
 <tbody>
  <tr>
   <th>オプション</th> 
   <th>説明</th> 
  </tr>
  <tr>
   <td>値</td> 
   <td><p>値の配列（オン/オフ/中立）。</p> <p>これは、checkButton のさまざまなステートのための値の配列です。values[0] は状態がオンの場合の値、 values[1] は状態がオフの場合の値です。<br /> values[2] は、状態が NEUTRAL の場合の値です。 値の配列の長さは、状態オプションの値と等しくなります。<br /> </p> </td> 
  </tr>
  <tr>
   <td>状態</td> 
   <td><p>許可されている状態の数。 </p> <p>アダプティブフォームの場合は 2 つ（オン、オフ）、HTML5 フォームの場合は 3 つ（オン、オフ、中間）です。</p> </td> 
  </tr>
  <tr>
   <td>state</td> 
   <td><p>要素の現在の状態。</p> <p>アダプティブフォームの場合は 2 つ（オン、オフ）、HTML5 フォームの場合は 3 つ（オン、オフ、中間）です。</p> </td> 
  </tr>
 </tbody>
</table>

### DateTimeEdit:(DateField) {#datetimeedit-datefield}

| オプション | 説明 |
|---|---|
| 日 | そのフィールドのローカライズされた日数。 |
| 月 | そのフィールドのローカライズされた月の名前。 |
| ゼロ | 数値 0 のローカライズされたテキスト。 |
| clearText | クリアボタンのローカライズされたテキスト。 |
