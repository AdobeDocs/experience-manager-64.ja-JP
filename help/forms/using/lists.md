---
title: ドキュメントフラグメント
seo-title: Document Fragments
description: Correspondence Management では、テキスト、リスト、条件、レイアウトフラグメントなどのドキュメントフラグメントを使用して、顧客とのやり取りの静的、動的、繰り返し可能なコンポーネントを作成できます。
seo-description: Document Fragments, such as Text, lists, conditions, and layout fragments, in Correspondence Management let you form the static, dynamic, and repeatable components of customer correspondence.
uuid: d1baa9eb-dffe-4e02-af95-394e7ee0d6ee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
discoiquuid: 7bdf1f06-c298-4695-bad1-e402cf472086
feature: Correspondence Management
exl-id: 3bc32053-d35d-4c19-a311-48b0b99eefb8
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '6818'
ht-degree: 35%

---

# ドキュメントフラグメント {#document-fragments}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## ドキュメントフラグメント {#document-fragments-1}

ドキュメントフラグメントは、レターや通信を構成できる、通信の再利用可能なパーツやコンポーネントです。 ドキュメントフラグメントには、次の種類があります。

* **テキスト**:テキストアセットは、1 つ以上の段落で構成されるコンテンツです。 段落は静的または動的にすることができます。
* **リスト**:リストは、テキスト、リスト、条件、画像を含む、ドキュメントフラグメントのグループです。 リスト要素の順序は、固定または編集可能にすることができます。 レターを作成する際に、一部またはすべてのリスト要素を使用して、再利用可能な要素のパターンを複製できます。
* **条件**:条件を使用すると、指定されたデータに基づいて、通信の作成時に含めるコンテンツを定義できます。 条件については、制御変数で説明します。 制御変数は、データディクショナリ要素またはプレースホルダーのいずれかです。
* **レイアウトフラグメント**:レイアウトフラグメントは、1 つ以上のレター内で使用できるレイアウトです。 レイアウトフラグメントは、繰り返し可能なパターン（特に動的テーブル）を作成するために使用します。 レイアウトには、「住所」や「参照番号」など、一般的なフォームフィールドを含めることができます。 また、ターゲット領域を示す空のサブフォームを含めることもできます。レイアウト (XDP) は Designer で作成され、AEM Formsにアップロードされます。

## テキスト {#text}

テキストアセットは、1 つ以上の段落で構成されるコンテンツです。 段落は静的または動的にすることができます。動的段落には、データ要素への参照が含まれます。データ要素の値は実行時に提供されます。 例えば、レターのあいさつ文の顧客名は動的なデータ要素で、実行時に値が使用可能になります。 これらの値を変更すると、同じレターテンプレートを使用して、異なる顧客のレターを生成できます。

Correspondence Management Solution は、動的データ項目（可変データ）に対して 2 種類のサポートを行います。

* **データディクショナリ要素**:これらの要素はデータディクショナリに連結され、指定されたデータソースから値を取得します。 データディクショナリ変数は保護も保護も保護もできます。 通信の作成時に、ユーザーは保護されていないデータ辞書変数のデフォルト値を変更できますが、保護された変数は変更できません。
* **プレースホルダー**:これらは、バックエンドのデータソースに連結されない変数です。 通信の作成時にユーザーが値を入力する必要があります。 プレースホルダーは、デフォルトでは保護されていません。

>[!NOTE]
>
>Correspondence Management テンプレートでは、プレースホルダーを作成する際に一意の名前を作成するように強制されません。 テキストと条件など、同じ名前のプレースホルダを 2 つ作成し、その両方をレターテンプレートで使用する場合、最後に挿入したプレースホルダの値が両方のプレースホルダに使用されます。 2 つのプレースホルダの名前が同じ場合、そのタイプが比較されます。 型が異なる場合、型は String になります。 ただし、モジュール内では、同じ名前のプレースホルダを複数作成することはできません。

### テキストの作成 {#create-text}

1. 「**フォーム**／**ドキュメントフラグメント**」を選択します。

1. タップ **作成** > **テキスト。** または、テキストアセットを選択して、 **編集**.
1. テキストの次の情報を指定します。

   * **タイトル：（オプション）**&#x200B;テキストアセットのタイトルを入力します。タイトルは一意である必要はなく、特殊文字や英語以外の文字を含めることもできます。テキストは、サムネイルやアセットプロパティなど、タイトル（使用可能な場合）で参照されます。
   * **名前：**&#x200B;テキストアセットの一意の名前。どの状態にも、同じ名前のアセット（テキスト、条件、リスト）は 2 つ存在できません。 「名前」フィールドに入力できるのは、英語の文字、数字、ハイフンのみです。 「名前」フィールドは、「タイトル」フィールドに基づいて自動的に入力されます。 「タイトル」フィールドに入力した特殊文字、スペース、および英数字以外の文字はハイフンに置き換えられます。「タイトル」フィールドの値は「名前」フィールドに自動的にコピーされますが、値を編集することもできます。
   * **説明**:アセットの説明を入力します。
   * **データ辞書**:必要に応じて、マッピングするデータディクショナリを選択します。 この属性を使用すると、テキストアセット内のデータディクショナリ要素への参照を追加できます。
   * **タグ**:必要に応じて、カスタムタグを作成するには、テキストフィールドに値を入力し、Enter キーを押します。 タグのテキストフィールドの下にタグが表示されます。 このテキストを保存すると、新しく追加されたタグも作成されます。

1. **次へ**&#x200B;をタップします。テキストの段落やデータ要素をテキストに追加できるエディターページが、Correspondence Management によって表示されます。

   ブラウザーのデフォルトのスペルチェッカーは、テキストエディターでスペルチェックを行います。 スペルチェックや文法チェックを管理するには、ブラウザのスペルチェッカー設定を編集するか、またはスペルチェックや文法チェックを行うためのブラウザプラグインやアドオンをインストールします。

   また、テキストエディターでは、様々なキーボードショートカットを使用して、テキストの管理、編集や書式設定を行うこともできます。[テキストエディター](/help/forms/using/keyboard-shortcuts.md#p-formatting-p)キーボードショートカットについて詳しくは、「Correspondence Management キーボードショートカット」を参照してください。

1. テキストエディターが開くので、テキストを入力します。ページの最上部にあるツールバーを使用して、テキストの書式設定や、条件、リンク、改ページの挿入を行います。


   ![ツールバー](assets/advancedediting.png)

   **図：** *ツールバー*

   * **リンク**：テキストにハイパーリンクを挿入します。タップ **[!UICONTROL リンク]**&#x200B;をクリックし、 **[!UICONTROL URL]** フィールドで、 **[!UICONTROL 代替テキスト]** 「 」フィールドで「 」をタップし、 ![保存](assets/save_icon.svg).
   * **繰り返し**：区切り文字を使用して、データディクショナリのコレクション要素を繰り返し印刷します。
   * **条件**:タップして条件を挿入します。 条件に基づいてテキストを挿入します。 条件が true の場合、文字にテキストが表示され、それ以外の場合は表示されません。
   * **説明を追加**：テキストに注釈を追加します。これは作成者に表示されるメタデータで、作成したレターには含まれません。
   * **改ページ**：テキストモジュールの改ページ属性を false に設定した場合、テキストモジュールはページ間で区切られません。

   テキストエディターが開きます。テキストを入力します。段落、整列、リストなど、編集のタイプによってツールバーが変わります。

   ![ツールバーのタイプを選択](assets/toolbarselection.png)

   **図：** *ツールバーのタイプを選択します。段落、整列またはリスト*

   ![段落ツールバー](assets/fonteditingtoolbar.png)

   **図：** *段落ツールバー*

   ![整列ツールバー](assets/paragrapheditingtoolbar.png)

   **図：** *整列ツールバー*

   ![リストツールバー](assets/bulleteditingtoolbar.png)

   **図：** *リストツールバー*

1. MS Word やHTMLページなど、別のアプリケーションに存在するテキストの段落を 1 つ以上再利用するには、テキストをコピーしてテキストエディターに貼り付けます。 コピーしたテキストの書式は、テキストエディターでも保持されます。

   編集可能なテキストモジュールでは、1 つ以上のテキスト段落をコピーして貼り付けることができます。 例えば、次のような許容可能な居住証明書の箇条書きリストを含む MS Word ドキュメントがあるとします。

   ![pastetextmsword](assets/pastetextmsword.png)

   MS Word ドキュメントから編集可能なテキストモジュールに、テキストを直接コピーして貼り付けることができます。 箇条書きリスト、フォント、テキストの色などの書式は、テキストモジュールでも保持されます。

   ![pastetexttextmodule](assets/pastetexttextmodule.png)

   >[!NOTE]
   >
   >ただし、貼り付けられたテキストの書式設定にはいくつかの[制約](https://helpx.adobe.com/jp/aem-forms/kb/cm-copy-paste-text-limitations.html)があります。

1. 必要に応じて、ドキュメントフラグメントに特殊文字を挿入します。例えば、特殊文字パレットを使用して、以下の特殊文字を挿入することができます。

   * 通貨記号（€、￥、£ など）
   * 数学記号（∑、√、∂、^ など）
   * 句読記号（‟、” など）

   ![specialcharacters](assets/specialcharacters.png)

   Correspondence Managementhas では、210 種類の特殊文字に初期状態から対応しています。管理者は、[カスタマイズすることで特殊文字を増やしたり、カスタムの特殊文字を追加したりする](/help/forms/using/custom-special-characters.md)ことができます。

1. 編集可能なインラインモジュールのテキストの一部をハイライト表示または強調するには、テキストを選択して「ハイライト表示の色」をタップします。

   ![textbackgroundcolorapplied](assets/textbackgroundcolorapplied.png)

   基本色パレットに表示されている基本色 **`[A]`** を直接タップすることも、スライダー **`[B]`** を使用して、その色の適切な網掛けを選択した後で&#x200B;**選択**&#x200B;をタップすることもできます。

   オプションで、「詳細」タブに移動して、適切な色相、明度、彩度 **`[C]`** を選択して正確な色を作成し、「選択 **`[D]`**」をタップして、その色を適用してテキストをハイライト表示することもできます。

   ![textbackgroundcolor](assets/textbackgroundcolor.png)

1. データディクショナリ要素とプレースホルダー要素をデータパネルからテキストにドラッグ&amp;ドロップします。

   To:

   * テキストにデータディクショナリ要素を追加し、リストからデータ要素を選択して、「挿入」（![insert](assets/insert.png)）をタップします。「保護」を選択すると、データディクショナリ要素は読み取り専用となり、レターエディターに表示されますが、「通信を作成」ユーザーインターフェイスや Correspondence Creator には表示されません。
   * テキストにプレースホルダー要素を追加し、データ要素パネルで「新規作成」をタップし、新しいデータ要素の詳細を入力した後、「作成」をタップして、新しい要素をリストに追加します。 新しいプレースホルダーは、データディクショナリ要素と同じ方法でテキストに挿入できます。 プレースホルダーを編集するには、プレースホルダーを選択して「編集」をタップします。

   ![プレースホルダー要素](assets/placeholder_elements_in_xmldata.png)

   **図：** *データディクショナリのサンプルデータファイルで指定されたプレースホルダー要素*

   ![レター内のプレースホルダー要素](assets/placeholder_elements_in_text.png)

   **図：** *サンプルデータファイルで指定されたデータディクショナリ変数から入力された、CCR ビューのプレースホルダー要素値*

1. インライン条件と繰り返しを使用して、文脈性の高い、構成力のあるレターにすることができます。インライン条件と繰り返しについて詳しくは、[レターのインライン条件と繰り返し](/help/forms/using/cm-inline-condition.md)を参照してください。
1. **保存**&#x200B;をタップします。

#### テキストの検索と置換 {#searching-and-replacing-text}

大量のテキストを含むテキスト要素で作業する際、特定のテキスト文字列を検索する必要があります。また、特定のテキスト文字列を別の文字列と置換する必要がある場合もあります。

検索と置換機能を使用すると、テキスト要素内の任意の文字列を検索（および置換）できます。 この機能には、強力な正規表現検索も含まれています。

#### テキストモジュールでテキストを検索するには {#to-search-text-in-a-text-module}

1. テキストエディターでテキストモジュールを開きます。

1. 「検索と置換」をタップします。
1. 検索するテキストを「検索」テキスト・ボックスに入力し、「検索」を押します。 テキストモジュールで検索テキストがハイライト表示されます。 

1. テキストの次のインスタンスを検索するには、再び「検索」を押します。

   「検索」ボタンを押し続けると、ページの下方に検索が継続されます。テキストの最後のインスタンスが見つかった後に表示される「**モジュールの最後に達しました**」のメッセージは、検索結果がそれ以上見つからないことを示します。

   ただし、テキストモジュールで検索テキストのインスタンスが見つからない場合は、**一致が見つかりませんでした**&#x200B;というメッセージが表示されます。

1. 「検索」を再び押すと、検索はページの一番上から続行されます。

#### 検索オプション {#search-options}

**大文字／小文字の一致**：検索は、大文字／小文字が一致する結果のみを返します。

**単語全体：**&#x200B;単語全体が一致する結果のみを返します。

**注意：** 「検索」テキストボックスに特殊文字を入力すると、「単語全体」オプションは無効になります。

**Reg ex：**&#x200B;正規表現を使用して検索します。例えば、次の正規表現はテキストモジュール内のメールアドレスを検索します。

`[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}`

#### テキストモジュールでテキストを検索および置換するには {#to-search-and-replace-text-in-a-text-module}

1. テキストエディターでテキストモジュールを開きます。 

1. 「検索と置換」をタップします。
1. 検索するテキストを「検索」テキストボックスに入力し、検索するテキストを置換するテキストを入力して、「置換」を押します。
1. 検索テキストが見つかった場合、そのテキストは「置換」テキストに置き換えられます。

   * 検索テキストの別のインスタンスが見つかった場合、そのインスタンスはテキストモジュール内でハイライト表示されます。 「置換」を再度押すと、3 つ目のインスタンスが見つかった場合に、ハイライト表示されたインスタンスが置き換えられ、カーソルが前に移動します。
   * 別のインスタンスが見つからない場合、カーソルは最後に置き換えられたインスタンスで停止します。

1. 「検索」を再び押すと、検索はページの一番上から続行されます。

   「すべてを置換」オプションを使用して、テキストモジュール内のテキストのインスタンスをすべて置き換えます。 us`` を行うと、「検索と置換」ダイアログで置換の数がメッセージとして表示されます。

#### テキストモジュールのベストプラクティス/ヒントとテクニック {#best-practices-tips-and-tricks-for-text-modules}

* 重複を避けるために、一貫した命名規則を使用します。
* テキストモジュールで適切なデータディクショナリの連結を使用します。
* テキストアセットを変更する際にテキストエディターを使用する場合、次の規則が適用されます。

   * **変数の追加：**&#x200B;可
   * **変数の削除：**&#x200B;可
   * **プロパティの更新：**&#x200B;可
   * **データディクショナリの変更：**&#x200B;データディクショナリ要素が使用されなくなるまでは可。更新時にデータディクショナリを変更することはできません。

## リスト {#list}

リストは、テキスト、（その他の）リスト、条件、画像を含む、ドキュメントフラグメントのグループです。 リスト要素の順序は、固定または編集可能にすることができます。 レターを作成する際に、一部またはすべてのリスト要素を使用して、再利用可能な要素のパターンを複製できます。 リストは基本的に、他のターゲット内でネスト可能なターゲットとして動作します。

### リストの実装 {#implementing-lists}

リストの実装は、次の 2 つの手順で構成されます。

1. 名前、説明、データディクショナリなどのコアプロパティを定義する。
1. リストの一部であるコンテンツのセクション。次に、リストのロック順序やライブラリアクセスなどのプロパティを設定します。

### リストの作成 {#create-a-list}

リストは、レターテンプレートで単一の単位として使用できる関連コンテンツのグループです。 リストには、任意の種類のコンテンツを追加できます。 リストはネストすることもできます。 リストモジュールは、次のように指定できます。

* **注文済み**:通信を作成ランタイムで順序を変更することはできません。
* **ライブラリアクセス**:ユーザーは、リストにモジュールを追加できます。 このフラグは、ライブラリのアクセスを有効にするかどうかを指定します。 有効（開く）にすると、レターのプレビュー中にモジュールをリストに追加できます。
* リストを作成する際に、次のようなタイプを指定できます。
* **プレーン**:リストに追加のスタイル書式は適用されません。
* **箇条書き**:単純な箇条書きで書式設定されたリスト。
* **番号付き**:標準 (1、2、...)、大文字のローマ数字 (I、II、...)、小文字のローマ数字 (i、ii、...) を含む数値リスト。
* **レター付き**:小文字 (a、b、...) および大文字 (A、B、...) の選択肢を含むアルファベット順のリスト。
* **カスタム**:任意の番号付き/文字付きタイプおよびプレフィックスとサフィックスの値を作成できます。

1. 「**フォーム**／**ドキュメントフラグメント**」を選択します。

1. 「**作成**／**リスト**」を選択します。

1. リストの次の情報を指定します。

   * **タイトル（オプション）:入力** リストのタイトル。 タイトルは一意である必要はなく、特殊文字や英語以外の文字を含めることもできます。リストは、サムネイルやアセットプロパティなど、タイトル（使用可能な場合）で参照されます。
   * **名前：**&#x200B;リストの一意の名前。どの状態にも、同じ名前のアセット（テキスト、条件、リスト）は 2 つ存在できません。 「名前」フィールドに入力できるのは、英語の文字、数字、ハイフンのみです。 「名前」フィールドは、「タイトル」フィールドの値が自動的に入力されます。「タイトル」フィールドに入力した特殊文字、スペース、および英数字以外の文字はハイフンに置き換えられます。「タイトル」フィールドの値は「名前」に自動的にコピーされますが、値を編集することもできます。
   * **説明（オプション）**：アセットの説明を入力します。
   * **データディクショナリ（オプション）**：接続するデータディクショナリを選択します。リストと同じデータディクショナリを使用するアセット、またはデータディクショナリが割り当てられていないアセットのみをリストに追加できます。 データディクショナリをリストに割り当てると、レターテンプレートを作成する際に、適切なリストを見つけやすくなります。
   * **タグ（オプション）**：適用するタグを選択します。新しいタグ名を入力して作成することもできます。（「**保存**」をタップすると、新しいタグが作成されます。）

1. 「**次へ**」をタップします。
1. 「**アセットを追加**」をタップします。
1. リストにアセットを追加するには、アセット選択ページでアセットを選択して「**完了**」をタップします。

   ![アセットを選択してリストに追加します](assets/selectassets.png)

1. アセットがリスト項目ページに追加されます。


   リスト内のアセットの順序を変更するには、矢印アイコン（![dragndrop](assets/dragndrop.png)）を長押しして、ドラッグ＆ドロップします。ユーザーが通信を作成ユーザーインターフェイスでレターテンプレートを開くと、ここで定義した順にコンテンツがアセンブリされます。

   ![リスト内のアセットの並べ替えと設定](assets/listitems.png)

1. 次のオプションを選択して、CCR ユーザーインターフェイスでのリストの動作を指定できます。

   * **ライブラリアクセス**:ライブラリにアクセスしてアセットを追加するには、「ライブラリアクセス」をタップします。 「ライブラリアクセス」が有効な場合、要求処理担当者はリストにコンテンツを追加できます。 そうしないと、要求処理担当者はリストに定義したコンテンツに限定されます。
   * **順序をロック**：要求処理担当者が順序を変更できないようにリストのアセット順をロックするには、「順序をロック」をタップします。このオプションを選択しない場合、要求処理担当者はリスト項目の順序を変更できます。
   * **箇条書き記号を追加**:モジュールに箇条書きスタイルまたは段落番号スタイルを適用するには、このオプションを使用します。 事前に設計されたリストスタイルまたはカスタムのリストスタイルを使用できます。 また、各リスト項目の前後に表示するテキストを指定することもできます。
   * **改ページ**：リストのコンテンツに改ページを追加するには、このオプション（![break](assets/break.png)）を選択します。このオプション（![nobreak](assets/nobreak.png)）を選択しない場合、リストのコンテンツが次のページにオーバーフローすると、リストの間でページを区切らずにリスト全体が次のページに移動します。
   * **割り当て設定**:リストに追加できるアセットの最小数と最大数を指定するには、このオプションを使用します。

1. リスト内の各アセットの実行時の動作を指定するには、次のオプションを選択します。

   * **編集可能：**&#x200B;このオプションを選択すると、通信を作成ユーザーインターフェイスでコンテンツを編集できます。（このオプションはリストモジュールと画像モジュールには使用できません） 。
   * **必須：**&#x200B;このオプションを選択すると、通信を作成ユーザーインターフェイスでコンテンツが必須となります。
   * **選択済み：**&#x200B;このオプションを選択すると、通信を作成ユーザーインターフェイスでコンテンツが事前に選択されます。
   * **スタイルをスキップ：**&#x200B;このオプションを選択すると、通信を作成ユーザーインターフェイスでコンテンツの箇条書きと段落番号がスキップされます。( このオプションは、画像モジュールでは使用できません。 また、「スタイルをスキップ」、「複合」、「無視」の各リストスタイルの間で、1 つのモジュールに適用できるオプションは 1 つだけです。 モジュールに「箇条書き記号を追加」を選択した場合、これらのオプションの 1 つをモジュールに使用できます )。
   * **インデント：**&#x200B;リストの一部として選択した各モジュールやコンテンツのインデントレベルを変更できます。インデントはレベル単位で指定します（ゼロから始まります）。1 インデントレベルは、36 pt のパディングに対応します。
   * **複合：**&#x200B;選択すると、複合段落番号が、外側の（親）リストのスタイルとそのリストのスタイルの組み合わせとして適用されます。この入れ子リストの複合段落番号は、この入れ子リストが外側のリストで表示される順序に基づきます。
   * **無視リストスタイル**：「複合段落番号」オプションをオフにすると、「リストスタイルを無視する」オプションが有効になります。このオプションを選択すると、入れ子になったリストのスタイルは無視され、外側のリストから番号が続きます。 したがって、入れ子リストのモジュールは、外側のリスト自体の一部として扱われ、入れ子リストで指定されたスタイルは無視されます。 入れ子リストに対して「リストスタイルを無視する」オプションをオフにした場合、入れ子リストに含まれるモジュールには、独自の番号付けスタイルが設定されます。
   * **次を保持：**&#x200B;リストに含まれるアセットの改ページを設定します。リストの 1 つのアセットの「次と合わせる」プロパティを **オン**&#x200B;に値を入力すると、そのアセットと次のアセットは同じページに表示されます。 これは、選択したアセットと次のアセットのコンテンツがページ間で区切られないことを意味します。

1. 「**保存**」をタップします。

### ベストプラクティス/ヒントとテクニック {#best-practices-tips-and-tricks}

* 重複を避けるために、一貫した命名規則を使用します。
* 適切なデータディクショナリの連結を使用する
* リストエディターを使用してリストを変更する場合、次の規則が適用されます。

   * プロパティの更新：可
   * **データディクショナリの変更：**&#x200B;データディクショナリを使用するアイテムが関連付けられなくなるまでは可。更新時にデータディクショナリを変更することはできません。

## 条件 {#conditions}

条件を使用すると、指定されたデータに基づいて、通信/レターの作成時に含めるコンテンツを定義できます。 条件については、制御変数で説明します。 条件を追加するときに、制御変数の値に基づいてアセットを含めることもできます。

選択したオプションに基づいて、true と判断された最初の式のみ、現在の条件変数に基づいて評価されるか、すべての条件が評価されます。 通信を作成 (CCR) でレターに入力する際、条件は「ホワイトボックス」として動作します。 条件がリストになると、リストのすべての必須項目と事前選択項目が出力されます。 これらの項目のいずれかが条件またはリスト自体である場合、結果のコンテンツも、テキストおよび画像コンテンツのフラットリストとして、トップダウンの深さ優先順で出力されます。 条件の結果は、任意のタイプ（テキスト、リスト、条件、画像）です。

### 条件の実装 {#implementing-conditions}

条件エディターには、 [式ビルダー](/help/forms/using/expression-builder.md) 複数のプレースホルダーとデータディクショナリ要素の両方を使用した式の作成をサポートするユーザーインターフェイス。 このような式では、一般的なオペランドとローカル/グローバル関数を使用できます。 各式は、一部のコンテンツに関連付けることができ、必要に応じて、true と評価される式がない場合にデフォルトのセクションを含めることができます。 すべての式は、定義された順序で評価され、最初に true を返す式が選択され、その条件モジュールによって関連するコンテンツが返されます。

例えば、レターの利用条件のテキストが顧客の州によって異なり、データディクショナリに「state」と呼ばれる要素が含まれている場合、条件を次のように追加できます。\
・ state = NY、T&amp;C_NY テキスト段落を選択\
・ state = NC、T&amp;C_NC テキスト段落を選択

条件エディターを使用して、デフォルトの条件を指定できます。 制御変数の値がどの条件とも一致しない場合は、デフォルト条件に関連付けられたコンテンツが使用されます。 前述の例の後に、次の条件の行を追加できます。
\
• Default, select T&amp;C_Rest

### 条件の作成 {#create-a-condition}

1. 「**フォーム**／**ドキュメントフラグメント**」を選択します。
1. 「**作成／条件**」を選択します。
1. リストの次の情報を指定します。

   * **タイトル（オプション）：**&#x200B;条件のタイトルを入力します。タイトルは一意である必要はなく、特殊文字や英語以外の文字を含めることもできます。条件は、そのタイトルによって（利用可能な場合）、サムネールやアセットのプロパティとして参照されます。
   * **名前**：条件の一意の名前。どの状態にも、同じ名前のアセット（テキスト、条件、リスト）は 2 つ存在できません。 「名前」フィールドに入力できるのは、英語の文字、数字、ハイフンのみです。 「名前」フィールドは、「タイトル」フィールドに基づいて自動的に入力されます。 「タイトル」フィールドに入力した特殊文字、スペース、および英数字以外の文字はハイフンに置き換えられます。「タイトル」フィールドの値は「名前」に自動的にコピーされますが、値を編集することもできます。
   * **説明（オプション）**：条件の説明を入力します。
   * **データ辞書（オプション）**：接続するデータ辞書をオプションとして選択します。条件と同じデータディクショナリを使用するアセット、またはデータディクショナリが割り当てられていないアセットのみをリストに追加できます。 データディクショナリをリストに割り当てると、レターテンプレートを作成する際に、適切な条件を見つけやすくなります。
   * **タグ（オプション）**：適用するタグをオプションとして選択します。新しいタグ名を入力して作成することもできます。（「**保存**」をタップすると、新しいタグが作成されます。）

1. 「**次へ**」をタップします。
1. 「**アセットを追加**」をタップします。
1. アセットを条件に追加するには、アセットを選択ページでアセットを選択し、「**完了**」をタップします。アセットが式ウィンドウに追加されます。
1. 条件の実行時の動作を指定するには、次のオプションを選択します。

   * **複数の結果評価を無効にする\複数の結果評価を有効にする**:このオプションが有効な場合（「複数を有効にする…」と表示される場合）、すべての条件が評価され、結果はすべての true 条件の合計になります。 このオプションを無効にする（「複数の結果評価を無効化」を表示する）と、true と判断された最初の条件のみが評価され、その条件が出力されます。
   * **改ページ**：条件のモジュール間に改ページを追加するには、このオプション（![break](assets/break.png)）を選択します。このオプション（![nobreak](assets/nobreak.png)）を選択しない場合、条件が次のページにオーバーフローすると、条件の間でページを区切らずに条件全体が次のページに移動します。

1. 条件内のアセットの順序を変更するには、矢印アイコン（![dragndrop](assets/dragndrop.png)）を長押しして、ドラッグ＆ドロップします。ユーザーが通信の作成ユーザーインターフェイスでレターテンプレートを開くと、ここで定義した順にコンテンツがアセンブルされます。
1. 行を削除するには、「**削除**」をタップします。デフォルトの行で「削除」をタップすると、アセット情報のみがクリアされます。
1. 「**コピー**」をタップし、行を複製します。
1. 「**編集**」をタップし、アセットを変更するか、式を編集します。

   詳細情報：

   * アセットを更新するには、アセット列の下にあるフォルダーアイコンをタップします。
   * 式ビルダーを開いて式を挿入するには、式列の下にあるフォルダーアイコンをタップします。式ビルダーについて詳しくは、[式ビルダー](/help/forms/using/expression-builder.md)を参照してください。

### ベストプラクティス/ヒントとテクニック {#best-practices-tips-and-tricks-1}

* 検索を容易にし、重複を避けるために、一貫性のある命名規則を使用します。
* 条件はケースステートメントと同じように動作するので、条件の順序は重要です。 最初の一致が返されます。
* 適切なデータディクショナリの連結を使用する
* 条件エディターを使用して条件を編集する場合、次のルールが適用されます。

   * **変数の追加：**&#x200B;可
   * **変数の削除：**&#x200B;可
   * **プロパティの更新：**&#x200B;可
   * **データ辞書の変更：**&#x200B;データ辞書要素が使用されなくなるまでは可。

## レイアウトフラグメント {#layoutfragments}

レイアウトフラグメントは、Designer で作成された XDP に基づいています。 レイアウトフラグメントを作成するには、XDP を作成し、[それを AEM Forms にアップロード](/help/forms/using/import-export-forms-templates.md)する必要があります。

1 つ以上のレイアウトフラグメントは、レターの一部を形成し、それらのパーツのグラフィカルなレイアウトを定義できます。 レイアウトフラグメントには、「住所」や「参照番号」などの一般的なフォームフィールドや、ターゲット領域を表す空のサブフォームを含めることができます。 また、レイアウトフラグメントを使用してテーブルを作成し、テーブルをレターに挿入できます。

一般的な使用例は、再利用可能なレイアウトパターンをレター内に配置し、それらのレイアウトパターン用のレイアウトフラグメントを作成する場合です。 例えば、複数の文字が同じ順序で出現する、レターの敬称、住所、件名の部分です。 または、複数のレターで使用されている行数と列数が同じテーブルなどを使用します。

既存の XDP に基づいてレイアウトフラグメントを作成できます。 レイアウトフラグメントは、フィールドとターゲット領域、または 1 つ以上のテーブルで構成できます。 レイアウト内のテーブルは、静的または動的に設定できます。 XDP は Designer で作成され、 [AEM Formsにアップロード済み](/help/forms/using/import-export-forms-templates.md). XDP は、レイアウトフラグメントまたはレターの構造を形成できます。 詳しくは、[レイアウトデザイン](/help/forms/using/layout-design-details.md)を参照してください。

ターゲット領域にバインドされたフラグメントを使用すると、作成時にレターを変更できます。 異なるサイズのレイアウトフラグメントを作成し、適切なフラグメントをターゲット領域に連結できます。 レイアウトフラグメントを使用すると、次のようなテーブルプロパティの一部をカスタマイズすることもできます。

1. 行数と列数を増やすことができます。
1. 追加の行と列にヘッダーとフッターのテキストを指定できます。
1. テーブルの列の幅の比率を定義できます。 実行時に、テーブルの列は、定義された比率と使用可能な領域に従ってサイズ変更されます。 幅の比率の合計は 100 にする必要があります。 それ以外の場合は適用されません。
1. テーブルがプレースホルダー（空白のセルが 1 つだけ含まれる）の場合、新しい列のタイプ（ターゲット領域/フィールド）を定義できます。
1. ヘッダー行とフッター行を非表示にできます。

この手順を実行する前に、Designer を使用して XFA フラグメントを作成します。 フラグメントには、フィールドやターゲット領域を整理するためのテーブルを含めることができます。 Designer では、次の 2 種類のテーブルを作成できます。静的および動的。 静的テーブルには、固定数の行が含まれます。 静的テーブルには、ターゲット領域とフィールドを含めることができます。 これらのターゲット領域およびフィールドを繰り返し DDE にバインドすることはできません。 動的テーブルには、1 つの行を含めることもできます。 テーブルのセルに連結されるデータによって、動的テーブルの行数が決まります。 動的テーブルには、フィールドのみを含めることができます。 DDE は、繰り返しまたは繰り返しなしで指定できます。

テーブルを設計する際は、次の点に注意してください。

1. レイアウトフラグメントの作成時に、テーブルをカスタマイズできます。 ただし、「カスタマイズ」オプションは、テーブルの親サブフォームがフローの場合にのみ有効です。
1. 動的テーブルの場合、すべてのフィールド、繰り返し可能な行およびテーブルで、データを正しく結合するために「名前を使用」の連結を使用します。
1. 動的テーブルの場合、テーブルフィールドに連結される繰り返し DDE はすべて同じ階層の一部になります。 繰り返さない DDE の場合、このような制限はありません。
1. レイアウトフラグメントを親ターゲット領域テーブルにマージする際は、使用可能なスペースに応じてサイズが変更されますが、サイズ変更は、レイアウトフラグメントに最上位サブフォーム内にターゲット領域やフィールドが直接含まれていない場合にのみおこなわれます。 テーブル内のターゲット領域とフィールドは許可されています。
1. プレースホルダーテーブルを作成できます。 プレースホルダーテーブルには、1 つの空白セルのみが含まれます。

* プレースホルダーテーブルの場合、フラグメントの作成時に次のプロパティをカスタマイズできます。

   * 行数
   * 列数
   * 各列のヘッダーおよびフッター
   * 各列のタイプ（ターゲット領域/フィールド）
   * 各列の幅の比率

* プレースホルダー以外のテーブルの場合は、次のプロパティをカスタマイズできます。

   * 行数
   * 列数
   * 追加の列のヘッダーとフッター
   * 各列の幅の比率

レター内でフラグメントをネストできます。 これは、フラグメント内にフラグメントを追加できることを意味します。 Correspondence Management ソリューションは最大 4 レベルのネストをレター内でサポートします。**レター**＞**フラグメント**＞**フラグメント**＞**フラグメント**＞**フラグメント**

レイアウトフラグメントで静的および動的テーブルを使用する例について詳しくは、[サンプルファイルの使用例：レター内での静的および動的テーブルの使用](#examplewithsamplefiles)を参照してください。

### レイアウトフラグメントの作成 {#creating-a-layout-fragment}

1. 「**作成**／**レイアウトフラグメント**」を選択します。
1. Correspondence Management に利用可能な XDP が表示されます。レイアウトフラグメントのベースとする XDP を選択し、「**次へ**」をタップします。
1. レイアウトの次の情報を指定します。

   * **タイトル（オプション）：**&#x200B;レイアウトフラグメントのタイトルを入力します。タイトルは一意である必要はなく、特殊文字や英語以外の文字を含めることもできます。レイアウトフラグメントは、そのタイトルによって（利用可能な場合）、サムネールやアセットのプロパティとして参照されます。
   * **名前：**&#x200B;レイアウトフラグメントの一意の名前。どの状態にも、同じ名前のアセット（テキスト、条件、リスト）は 2 つ存在できません。 「名前」フィールドに入力できるのは、英語の文字、数字、ハイフンのみです。 「名前」フィールドは、「タイトル」フィールドに基づいて自動的に入力されます。 「タイトル」フィールドに入力した特殊文字、スペース、および英数字以外の文字はハイフンに置き換えられます。「タイトル」フィールドの値は「名前」に自動的にコピーされますが、値を編集することもできます。この名前はアセットの管理ユーザーインターフェイスのリストに表示されます。
   * **説明（オプション）**：アセットの管理ユーザーインターフェイスのリストに表示される説明。
   * **タグ（オプション）**：条件に適用するタグをオプションで選択します。新しいタグの名前を入力して作成することもできます。

1. 「**テーブル**」タブをタップし、レイアウトの次の情報を指定します。

   * **の設定**:設定するテーブルを選択します。 ドロップダウン内のテーブル名のサフィックスは、テーブルが静的な場合は「静的」、テーブルが動的な場合は「動的」です。 静的テーブルには、固定数の行が含まれます。 静的テーブルには、ターゲット領域とフィールドを含めることができます。 これらのターゲット領域およびフィールドを繰り返し DDE にバインドすることはできません。 テーブルのセルに連結されるデータによって、動的テーブルの行数が決まります。
   * **行**:レイアウトの行数を選択します。 設定した行数は、元の行数以上である必要があります。
   * **列**:レイアウトの列数を選択します。 設定する列数は、元の列数以上である必要があります。

   列ごとに、次の詳細が必要です。

   * **ヘッダー**:ヘッダー用に表示するテキスト
   * **フッター**:フッターに表示するテキスト
   * **タイプ**:追加の列のタイプ。 フィールドまたはターゲット領域。 「タイプ」は、静的プレースホルダーテーブルに対して有効です。 型は、セルレベルではなく列レベルで定義できます。 拡張列内のすべてのセルの型は同じです。 動的テーブルの場合、すべての列はフィールドタイプです。 プレースホルダー以外のテーブルの場合、追加の列のタイプを定義することはできません。 この場合、拡張された列の追加のセルのタイプは、その行の最後の列のタイプと同じです。および追加行のセルのタイプは、その列の最後のセルのタイプと同じです。
   * **幅の比率：**&#x200B;テーブル列の幅の比率。

   レイアウトフラグメントで静的および動的テーブルを使用する例について詳しくは、[サンプルファイルの使用例：レター内での静的および動的テーブルの使用](create-letter.md#insert-data-modules-and-layout-fragments-in-a-letter-and-configure-them)を参照してください。

1. 「**保存**」をタップします。

### Correspondence Management に XDP をアップロード {#upload-an-xdp-to-correspondence-management}

Correspondence Management に XDP をアップロード/読み込む手順については、 [AEM Formsへのアセットの読み込みと書き出し](/help/forms/using/import-export-forms-templates.md).

### ベストプラクティス/ヒントとテクニック {#best-practices-tips-and-tricks-2}

#### デフォルトのサブフォーム連結を設定 {#set-the-default-subform-binding}

Designer でターゲット領域を作成する場合、新しいすべてのサブフォームのデフォルトの連結を「なし」に設定すると便利です。

デフォルトの連結を設定するには：

1. Designer で、**ツール**／**オプション**／**データ連結**／**サブフォームの連結**&#x200B;をタップします。

1. 「新規サブフォームのデフォルト連結」リストで、 **データ連結がありません**.

これにより、挿入/サブフォームコマンドを使用するか、オブジェクトパレットからドラッグ&amp;ドロップして挿入したサブフォームは、デフォルトで「なし」の連結を持つようになります。 つまり、デフォルトでは、コンテンツを追加したり、連結設定を変更したり、サブフォームに「_int」サフィックスを付けたりしない限り、新しいサブフォームはすべてターゲット領域になります。

#### 第 508 条遵守 {#section-compliance}

通信を作成ユーザーインターフェイスで作成した完成したレターが、後のワークフローでの入力に使用される場合。 レイアウトを作成する際は、 Section 508 に関する次の推奨事項に従います。 そうしないと、レターPDFは表示用になり、次の推奨事項を無視することができます。

* レイアウト内のすべてのターゲット領域サブフォームとすべてのフィールドには、タブ順が設定されます。
* キャプションを含むフィールドは、デフォルトで 508 に準拠しています。 フィールドの/field/assist/speak@priority属性は、デフォルトで「custom」に設定されています。つまり、カスタムのスクリーンリーダーテキストが提供されない限り、スクリーンリーダーはフィールドのキャプションを読み取ります。
* キャプションのないフィールドは、ツールチップを指定し、スクリーンリーダーがツールチップを読み取るように指定します。その際には、

`/field/assist/speak@priority="toolTip"` を設定し、`/field/assist/toolTip` でツールヒントのテキストを指定します。

#### Designer と Asset Configuration Manager での日付形式 {#date-formats-in-designer-and-asset-configuration-manager}

Designer でレイアウトをデザインする際は、日付フィールドの形式が、 [Correspondence Management 設定プロパティ](/help/forms/using/cm-configuration-properties.md). 詳しくは、Designer ヘルプの「フィールド値の書式設定とパターンの使用」を参照してください。

#### 日付範囲のキャプチャ {#capturing-date-ranges}

startDate ～ endDate など、日付の組み合わせを処理する場合は、1 つのサブフォームを使用して、完成したレターの配置が正しいことを確認し、フィールドの数を最小限に抑えます。

#### フォームレベルの連結の設定 {#setting-form-level-binding}

レイアウトに、単一の XML 要素にマッピングされる多数のフィールドとターゲット領域が含まれる場合、フォームレベルの連結を使用し、要素ごとに個別のノードを作成します。 Correspondence Management でデータをマッピングする際、フォームレベルで連結されたフィールドは無視されます。

#### マスターページでサブフォームのターゲット領域を使用しない {#do-not-use-subform-target-areas-in-a-master-page}

マスターページのサブフォームのターゲット領域は、アセットを管理ユーザーインターフェイスに表示されず、データをマッピングできません。

#### ターゲット領域に適した位置とタイプの選択 {#choosing-appropriate-positions-and-types-for-target-areas}

レイアウトをデザインする際は、サブフォームを選択する際に注意が必要です。 レイアウトに 1 つのサブフォームが含まれる場合、フロータイプにすることができます。 サブフォーム内にフィールドを配置した後は、別のサブフォームに含めて、ラップされたサブフォームもフローに配置し、レイアウトを乱さないようにすることができます。

#### マスターページへのフィールドの配置 {#placing-fields-on-master-pages}

マスターページにフィールドを配置する場合は、次の点に注意してください。

* マスターページフィールドの連結を「グローバルデータを使用」に設定します
* このフィールドは、マスターページのルート PageArea の直下に配置しないでください。
* フィールドを名前の付いたサブフォームに含め、名前の付いたサブフォームの連結が「名前による」に設定されていることを確認します。

## レイアウトフラグメントを使用したテーブルの作成 {#creating-tables-using-layout-fragments}

多くのレターテンプレートにはテーブルが含まれています。 テーブルは静的にすることができます。例えば、用語と条件のテーブルでは、各行が 1 つの条件を表し、各部分が別々の列に表示されます。 テーブルには、顧客名、アカウント ID、トランザクション番号、トランザクション金額などの情報を含む、動的なアカウント情報なども含まれます。

* **静的テーブル**:利用条件のテーブルなど、行の列数が異なるテーブルを作成する場合もあります。 各行が 1 つの条件を表し、各条件に異なるサブパーツを含めることができます。 各パーツは別々の列に表示されます。
* **動的テーブル**:レイアウトフラグメントは、動的テーブルのフィールドをコレクション DDE に連結する機能を提供します。 レター生成時に、コレクション DDE のサイズに応じて、テーブル行が生成されます。

DD には Nominee_details コレクション要素があります。このコレクション要素には 1 つの複合要素と、Nominee_name、Nominee_address、Nominee_gender という 3 つのプリミティブ要素があります。\
動的 XDP にも同じヘッダーがあります。このため、上記の DD フィールドを使用して、動的 XDP フィールドをマッピングできます。

### サンプルファイルの例：レター内での静的および動的テーブルの使用 {#examplewithsamplefiles}

この例では、動的テーブルと静的テーブルを作成し、動的テーブルを DDE に連結して、これら 2 つのテーブルを含むレターを作成する方法を示します。 この例を使用する際は、最初からファイルを作成するか、手順で指定した入力ファイルを使用できます。

1. 図に示すように、例で使用するデータディクショナリ (DD) を作成します。

   次に、「DD」を選択し、サンプルデータを書き出します。 取得する XML ファイルには、Employee データと Nominee_details 用の 3 つのインスタンスが含まれています（デフォルトでは、3 つのインスタンスがダウンロードされます）。 必要に応じて、を追加または削除できます )。 値を更新し、DD にテストデータを読み込みます。 CMP ファイルはパッケージで、DD が含まれています。 DD を Correspondence Management に読み込みます。

   データディクショナリとテストデータの使用について詳しくは、 [データ辞書](/help/forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![データディクショナリの構造](assets/dd.jpeg)

[ファイルを入手](assets/exportpackage_1431709897770.cmp.zip)

1. Designer で、2 つの XDP（レイアウトフラグメント）を作成します。動的テーブルと静的テーブル。 両方のレイアウトで、次の操作を行います。

   * テーブル列にサブフォームを追加します。テーブルの親サブフォームのレイアウトをフローに変更し、テーブル内のサブフォームの連結を削除してください。
   * テーブルのセルにサブフォームを追加します。テーブルの親サブフォームのレイアウトをフローに変更し、テーブル内のサブフォームの連結を削除してください。

   または、この手順を実行するために用意されている静的および動的 XDP を使用します。

   レイアウトフラグメントの使用について詳しくは、[レイアウトフラグメント](#layoutfragments)を参照してください。


   レイアウトのデザインについて詳しくは、[Designer ヘルプ](https://help.adobe.com/ja_JP/AEMForms/6.1/DesignerHelp/)を参照してください。

[ファイルを入手](assets/static.xdp.zip)

[ファイルを入手](assets/dynamic.xdp.zip)

1. XDP を AEM Forms にアップロードします。
1. 動的 XDP に基づいてレイアウトフラグメントを作成します。 プロパティの「テーブル」タブに、テーブルが動的であることが表示されます（「設定対象」フィールド）。 行数 (1) と列数 (3) は、XDP/レイアウトフラグメントから派生します。

   このレイアウトのフィールドは読み込んだ DD に後で連結されます。また、レターでは、行数がテストデータファイル（DD に付属している XML データファイル）のレコード数に基づいて動的に作成されます。

   ![レイアウトフラグメント画面を作成](assets/dynamictableproperties.png)
   [クリックして拡大](assets/dynamictableproperties.png)


1. 静的 XDP に基づいてレイアウトフラグメントを作成します。 プロパティの「テーブル」タブに、テーブルが静的であることが表示されます（「設定対象」フィールド）。 行数 (1) と列数 (3) は、XDP/レイアウトフラグメントから派生します。

   ここで列と行の数を変更できます。 この画面で選択した内容に応じて、静的テーブルの行と列の数は、このレイアウトで作成されるレター内で固定されます。
   [ ![レイアウトフラグメント画面を作成](assets/statictableproperties.png)](assets/statictableproperties-1.png)
   [クリックして拡大](assets/statictableproperties-1.png)

1. 両方のレイアウトフラグメントを使用してレターを作成します。 動的 XDP をレターに挿入する際に、フィールドの連結をデータディクショナリのコレクション要素に設定します。

   レターおよびレターテンプレートの作成について詳しくは、 [レターを作成](/help/forms/using/create-letter.md).

1. レターを保存し、プレビューします。 レターをプレビューすると、データディクショナリの値がレターに表示されます。 動的テーブルには、3 つの行があります。 これは、テストデータにこれらの行の 3 つのレコードが含まれているからです。

   静的テーブルには、レイアウトフラグメントの作成中に指定した数だけ行と列があります。

   ![レター内の静的テーブル](assets/statictableletter.png)

   動的テーブルの場合、3 つの行はテストデータファイルのレコード数に応じて表示されます。 これは、レイアウトをレターに追加する際に、動的テーブルのフィールドとデータディクショナリのコレクション要素の間に連結を作成したためです。 「名前」、「住所」、「性別」の値は、使用したテストデータファイルから入力されます。

   ![レター内の動的テーブル](assets/dynamictableletter.png)

## ドキュメントフラグメントのコピーを作成する {#create-a-copy-of-a-document-fragment}

既存のドキュメントフラグメントと類似したプロパティとコンテンツを持つドキュメントフラグメントをすばやく作成するには、そのドキュメントフラグメントをコピーして貼り付けます。

1. ドキュメントフラグメントのリストから、1 つ以上のドキュメントフラグメントを選択します。 UI にコピーアイコンが表示されます。
1. 「コピー」をタップします。UI に貼り付けアイコンが表示されます。 貼り付ける前に、フォルダ内に移動することもできます。 異なるフォルダーに同じ名前のアセットを含めることができます。 フォルダーについて詳しくは、[フォルダーとアセットの整理](/help/forms/using/import-export-forms-templates.md#folders-and-organizing-assets)を参照してください。
1. 「貼り付け」をタップします。 貼り付けダイアログが表示されます。 ドキュメントフラグメントを同じ場所にコピー&amp;ペーストすると、新しいレターのコピーに名前とタイトルが自動的に割り当てられますが、レターのタイトルと名前を編集することができます。
1. 必要に応じて、ドキュメントフラグメントのコピーを保存するタイトルと名前を編集します。
1. 「貼り付け」をタップします。 ドキュメントフラグメントのコピーが作成されます。
