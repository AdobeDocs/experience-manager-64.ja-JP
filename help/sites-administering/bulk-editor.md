---
title: Bulk Editor
seo-title: The Bulk Editor
description: Bulk Editor の使用方法を説明します。
seo-description: Learn how to use the Bulk Editor.
uuid: 65158ea4-d0fb-4992-99c6-d4b4fa4c87d2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4da555b4-7fb2-4d55-b29f-8bd21f474c1a
exl-id: 61d85393-2764-447d-afcc-3af1d99e8dbb
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 58%

---

# Bulk Editor{#the-bulk-editor}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

Bulk Editor を使用すると、次の操作が可能なので、視覚的なページコンテキストが不要な場合に非常に効率的に編集できます。

* 複数のページからコンテンツを検索（および表示）。これは GQL（Google Query Language）を使用して行います。
* このコンテンツを Bulk Editor で直接編集。
* 変更を（元のページに）保存。
* このコンテンツをタブ区切り（.tsv）スプレッドシートファイルに書き出し。

>[!NOTE]
>
>コンテンツをリポジトリに読み込むこともできますが、デフォルトでは、**ツール**&#x200B;コンソールで使用できる Bulk Editor では無効になっています。

ここでは、**ツール**&#x200B;コンソールで Bulk Editor を操作する方法について説明します。通常、管理者は、Bulk Editor を使用して複数の項目を検索および編集します。これを行うには、GQL クエリを使用してテーブルに値を入力してから、作業対象のコンテンツ項目を選択します。作成者は通常、[製品リスト](/help/sites-authoring/default-components.md)コンポーネントを使用してアクセス可能なカスタマイズされた Bulk Editor アプリケーションの一部として Bulk Editor を使用します。

>[!CAUTION]
>
>を使用 [クラシック UI の廃止](/help/release-notes/deprecated-removed-features.md) AEM 6.4 では Bulk Editor も廃止されたので、Adobeは Bulk Editor をさらに強化する予定はありません。

## Bulk Editor の使用例 {#example-use-case-for-the-bulk-editor}

例えば、特定の調査に回答したユーザーの名前と電子メールアドレスがすべて必要な場合は、その情報を Bulk Editor で提供し、スプレッドシートに書き出すことができます。

このような使用例を示す例をGeometrixxWeb サイトに記載します。

1. 次に移動： **サポート** ページに移動してから、 **カスタマーサービス満足度** 調査。
1. **編集** の **フォームの開始** 段落 ダイアログで、 **詳細** タブ、展開 **アクションの設定**&#x200B;を選択し、「 **データの表示…**.

   ![customsurvey](assets/custsatsurvey.png)

1. Bulk Editor は完全にカスタマイズ可能ですが、この例では、ユーザーはコンテンツの編集はできず、情報をスプレッドシートに書き出すことのみ可能です。

   ![bulkeditor](assets/bulkeditor.png)

## Bulk Editor の使用方法 {#how-to-use-the-bulk-editor}

Bulk Editor では、次の操作を実行できます。

* [クエリパラメーターに基づいてコンテンツを検索し、指定した結果のプロパティを列に表示し、このコンテンツを編集して変更を保存します。](#searching-and-editing-content)
* [このコンテンツをタブ区切りスプレッドシートに書き出します。](#exporting-content)

* [コンテンツをタブ区切りスプレッドシートから読み込みます。](#importing-content)

### コンテンツの検索と編集 {#searching-and-editing-content}

Bulk Editor を使用して複数の項目を同時に編集するには：

1. 内 **ツール** コンソールで、 **インポーター** フォルダーを開いて展開します。
1. 次をダブルクリックします。 **バルクエディター** をクリックして開きます。
1. 選択要件を入力します。

<table> 
 <tbody> 
  <tr> 
   <td>フィールド</td> 
   <td>プロパティ</td> 
  </tr> 
  <tr> 
   <td>ルートパス</td> 
   <td>バルクエディターで検索するルートパスを示します（<br />例：<code>/content/geometrixx/en</code>）。バルクエディターはすべての子ノードを検索します。</td> 
  </tr> 
  <tr> 
   <td>クエリのパラメーター</td> 
   <td>GQL パラメーターを使用して、リポジトリ内でバルクエディターが検索する検索文字列を入力します。例えば、「<code>type:Page</code>」と入力すると、ルートパス内のすべてのページを検索し、「<code>text:professional</code>」と入力すると、「professional」という単語が含まれているすべてのページを検索し、「<code>"jcr:title":English</code>」と入力すると、タイトルが「English」となっているすべてのページを検索します。文字列のみを検索できます。</td> 
  </tr> 
  <tr> 
   <td>「コンテンツモード」チェックボックス</td> 
   <td>このチェックボックスをオンにして、 <code>jcr:content</code> 検索結果のサブノード（存在する場合）内のプロパティを読み取ります。ページにのみ使用します。プロパティ名の前には <code>"jcr:content/"</code></td> 
  </tr> 
  <tr> 
   <td>プロパティ / 列</td> 
   <td>Bulk Editor で返すプロパティのチェックボックスをオンにします。 選択したプロパティは、結果ペインの列見出しです。 デフォルトでは、ノードパスが結果に表示されます。</td> 
  </tr> 
  <tr> 
   <td>カスタムプロパティ / 列</td> 
   <td>「<strong>プロパティ/列</strong>」フィールドのリストにない他のプロパティを入力します。これらのカスタムプロパティは、結果ウィンドウに表示されます。複数のプロパティを追加する場合は、コンマでプロパティを区切ります。<i>メモ：</i>まだ存在していないカスタムプロパティを追加すると、AEM WCM には空白のセルが表示されます。空のセルを変更して保存すると、プロパティがノードに追加されます。 新しく作成されたプロパティは、ノードタイプの制約とプロパティの名前空間に従う必要があります。</td> 
  </tr> 
 </tbody> 
</table>

次に例を示します。

![searchfilter](assets/searchfilter.png)

1. クリック **検索**.結果が Bulk Editor に表示されます。

   上記の例では、検索条件を満たすすべてのページが返され、リクエストされた列と共に表示されます。

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 任意のセル内でダブルクリックして、必要な変更を行います。

   ![srchresultedit](assets/srchresultedit.png)

1. 「**保存**」をクリックして変更を保存します（「**保存**」ボタンは、セルを編集後に有効になります）。

   >[!CAUTION]
   >
   >ここで行った変更は、リポジトリコンテンツ（「**パス**」で参照されているページなど）に書き込まれます。

#### その他の GQL クエリパラメーター {#additional-gql-query-parameters}

* **path:** このパスの下のノードのみを検索します。1 つの path プレフィックスで複数の用語を指定した場合は、最後の用語のみが考慮されます。
* **type:** 指定したノードタイプのノードのみを返します。これには、primary や mixin などのタイプが含まれます。複数のノードタイプをコンマで区切って指定できます。GQL は、指定したいずれかのタイプに該当するノードを返します。
* **order：**&#x200B;指定したプロパティを基準として結果を並べます。複数のプロパティ名をコンマで区切って指定できます。結果を降順で並べるには、プロパティ名にマイナス記号のプレフィックスを付けます（例：order:-name）。プラス記号を使用すると、結果は昇順に戻ります。これはデフォルトでもあります。
* **limit:** 間隔を使用して結果の数を制限します（例：limit:10..20）。間隔は 0 を基準とし、start はその値を含み、end はその値を含みません。開いた間隔を指定することもできます（例：:limit:10..または limit:..20）。ドットを省略し、値を 1 つだけ指定した場合、GQL は最大でこの数の結果を返します。例：limit:10（最初の 10 件の結果を返します）

### コンテンツの書き出し {#exporting-content}

場合によっては、コンテンツをエクスポートし、Excel スプレッドシートで変更する必要があります。 例えば、メーリングリストを書き出し、リストに表示されるすべての電話番号の市外局番を Excel で直接変更し、行を追加するなどの作業を行う場合があります。

コンテンツを書き出すには：

1. コンテンツを検索します。詳しくは、 [コンテンツの検索と編集](#searching-and-editing-content).
1. クリック **書き出し** をクリックして、変更内容をタブ区切りの Excel スプレッドシートにエクスポートします。 AEM WCM が、ファイルをダウンロードする場所を尋ねます。

   >[!NOTE]
   >
   >デフォルトでは、変更は [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252) （CP-1252 とも呼ばれます）。 UTF-8 をチェックして、変更を UTF-8 で書き出すことができます。

   ![srchressultextport](assets/srchrsesultexport.png)

1. 場所を選択し、ファイルのダウンロードを確認します。
1. ファイルをダウンロードしたら、Microsoft Excel などのスプレッドシートプログラムから開くことができます。 スプレッドシートプログラムはファイルを読み込み、スプレッドシート形式に変換します。

   ![exportinexcel](assets/exportinexcel.png)

### コンテンツの読み込み {#importing-content}

デフォルトでは、バルクエディターを開くと、読み込み機能は非表示になります。パラメーター `hib=false` を URL に追加すれば、バルクエディターページに「**読み込み**」ボタンが表示されます。コンテンツは、任意のタブ区切り（`.tsv`）ファイルから読み込むことがでめます。読み込みが正常に機能するには、列見出し（セルの最初の行）が、読み込み先のテーブルの列見出しと一致している必要があります。

>[!NOTE]
>
>コンテンツを再度読み込むと、それらのノードの以前のコンテンツは削除されます。 重要な情報を上書きしないように注意してください。

コンテンツを読み込むには：

1. Bulk Editor を開きます。
1. 例えば、次のような手順を実行して、`?hib=false` を URL に追加します。

   `http://localhost:4502/etc/importers/bulkeditor.html?hib=false`

1. 「**読み込み**」をクリックします。
1. `.tsv` ファイルを選択します。データがリポジトリーに読み込まれます。
