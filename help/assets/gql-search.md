---
title: GQL 全文検索
description: での GQL 全文検索機能の詳細 [!DNL Experience Manager] アセット。 タイトル、説明、作成者名など、特定のメタデータに基づいてアセットを検索する場合に使用します。
contentOwner: AG
feature: Search,Metadata
role: User
exl-id: e819501c-4ac3-447f-944c-67adc42e8c61
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 16%

---

# GQL 全文検索 {#gql-full-text-search}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

での GQL 全文検索機能の詳細 [!DNL Experience Manager] アセット。 タイトル、説明、作成者名など、特定のメタデータに基づいてアセットを検索する場合に使用します。

GQL 全文検索機能を使用すると、タイトル、説明、作成者など、特定のメタデータに基づいてアセットを検索できます。

タイトルなど、メタデータに基づいてアセットを検索するには、検索パネルで、メタデータキーワードに続いてその値を指定します。 GQL 全文検索機能は、入力した値に完全に一致するメタデータを持つアセットのみを取得します。

例えば、「Target」というタイトルのアセットを検索するには、次の手順を実行します。

## アセットの検索 {#searching-assets}

1. Assets ユーザーインターフェイスのツールバーで、 **[!UICONTROL 検索]** アイコンをクリックして「オムニサーチ」ボックスを表示します。

   ![](assets/do-not-localize/chlimage_1.png)

1. オムニサーチボックスにカーソルを置き、Enter キーを押します。
1. グローバルナビゲーションアイコンをクリックまたはタップして、 **[!UICONTROL フィルター]** パネル。
1. オムニサーチボックスで、値「Target」を指定します。 検索対象を特定のフォルダーに限定するには、フィルターパネルの参照アイコンをクリックまたはタップして、フォルダーを選択します。 この場合、一致はフォルダーとその配下のサブフォルダー内でのみ検索されます。

   >[!NOTE]
   >
   >また、フォルダーに対して全文検索を実行することもできます。 この場合、空でないフルテキスト検索語句を指定する必要があります。

   ![gql_search](assets/gql_search.png)

1. 押す **[!UICONTROL 入力]**. この [!DNL Assets] ユーザーインターフェイスには、タイトルが「Target」と完全に一致するアセットのみが表示されます。

GQL 全文検索機能では、次の条件に基づいてアセットを検索できます。

* 複数のメタデータフィールド（プロパティ）に対して指定した値を AND 演算で組み合わせて作成した複雑なクエリ
* 単一のメタデータフィールドに対する複数の値
* 部分文字列が一致

GQL 全文検索機能では、次のメタデータプロパティに基づいてアセットを検索できます。 プロパティの名前（author、title など）と値は、大文字と小文字が区別されます。

>[!NOTE]
>
>GQL 全文検索は、全文述語に対してのみ機能します。

| プロパティ | 検索形式（ファセット値） |
|---|---|
| [!UICONTROL タイトル] | title:John |
| [!UICONTROL 作成者] | creator:John |
| [!UICONTROL 投稿者] | contributor:John |
| [!UICONTROL 場所] | location:India |
| [!UICONTROL 説明] | description:&quot;Sample Image&quot; |
| [!UICONTROL 作成ツール] | creatortool:&quot;Adobe Photoshop 7.0&quot; |
| [!UICONTROL 著作権の所有者] | copyrightowner:&quot;Adobe Systems&quot; |
| [!UICONTROL 投稿者] | contributor:John |
| [!UICONTROL 使用条件] | usageterms:&quot;CopyRights Reserved&quot; |
| [!UICONTROL 作成日] | 作成済み:YYYY-MM-DDTHH:MM:SS.000+05:30...YYYY-MM-DDTHH:MM:SS.000+05:30 |
| [!UICONTROL 有効期限] | 有効期限:YYYY-MM-DDTHH:MM:SS.000+05:30...YYYY-MM-DDTHH:MM:SS.000+05:30 |
| [!UICONTROL オンタイム] | ontime:YYYY-MM-DDTHH:MM:SS.000+05:30...YYYY-MM-DDTHH:MM:SS.000+05:30 |
| [!UICONTROL オフタイム] | オフタイム:YYYY-MM-DDTHH:MM:SS.000+05:30...YYYY-MM-DDTHH:MM:SS.000+05:30 |
| [!UICONTROL 時間の範囲] （有効期限： dateontime、offtime） | ファセットフィールド：下限…上 |
| [!UICONTROL パス] | /content/dam/&lt;folder name=&quot;&quot;> |
| [!UICONTROL PDF タイトル] | pdftitle:&quot;Adobe文書&quot; |
| [!UICONTROL 件名] | subject:&quot;Training&quot; |
| [!UICONTROL タグ] | tags:&quot;Location And Travel&quot; |
| [!UICONTROL タイプ] | type:&quot;image\png&quot; |
| [!UICONTROL 画像の幅] | width:lowerbound...上 |
| [!UICONTROL 画像の高さ] | height:lowerbound..上 |
| [!UICONTROL ユーザー] | person:John |

複雑なクエリの検索形式の例：

* 複数のファセットフィールドを持つアセットをすべて表示する（例：title=John Doe および creatortool=Adobe Photoshop）：

tiltle:&quot;John Doe&quot; creatortool :Adobe(&amp;A);

* ファセット値が 1 語ではなく文になっているすべてのアセットを表示する ( 例：title=Scott Reynolds)

title:&quot;Scott Reynolds&quot;

* 単一のプロパティに複数の値を持つアセットを表示する ( 例：title=Scott Reynolds または John Doe)

title:&quot;Scott Reynolds&quot; OR &quot;John Doe&quot;

* プロパティ値が特定の文字列で始まるアセットを表示する ( 例：title は Scott Reynolds)

title:&quot;Scott&quot;

* プロパティ値が特定の文字列で終わるアセットを表示する ( 例：title は Scott Reynolds)

title:&quot;Reynolds&quot;

* プロパティ値に特定の文字列が含まれるアセットを表示する ( 例：title =バーゼル会議室 )

title:&quot;Meeting&quot;;

* 特定の文字列を含み、特定のプロパティ値を持つアセットを表示する ( 例：title=John Doe のアセットで文字列Adobeを検索します。

&amp;ast;Adobe&amp;ast;title:&quot;John Doe &quot;OR title:&quot;John Doe&quot; &amp;ast;Adobe&amp;ast;

>[!NOTE]
>
>path、limit、size および orderby の各プロパティを他のプロパティと OR で結合することはできません。
>
>ユーザー生成プロパティのキーワードは、プロパティエディターにおけるフィールドラベルからスペースを削除して小文字で表記したものです。

>[!NOTE]
>
>サブアセットのみを検索する JCR クエリを記述する場合、一致した参照元のアセットも一致したサブアセットと共に表示されます。

全文検索では、 — や^などの演算子もサポートされます。 これらの文字を文字列リテラルとして検索するには、検索式を二重引用符で囲みます。例えば、「Notebook - Beauty」ではなく、「&quot;Notebook - Beauty&quot;」と指定します。

## 検索の強化 {#boosting-search}

特定のアセットのキーワードの関連性を高め、そのキーワードに基づく検索を促進できます。 つまり、特定のキーワードを昇格させた画像は、これらのキーワードに基づいて検索を行う際に、検索結果の上部に表示されます。

1. Assets UI で、キーワードを昇格させるアセットのプロパティページを開きます。
1. 次に切り替え： **[!UICONTROL 詳細]** タブを押し、クリックまたはタップします。 **[!UICONTROL 追加]** under **[!UICONTROL 検索キーワードに採用]**.

   ![elevate_for_search](assets/elevate_for_search.png)

1. 「**[!UICONTROL 昇格を検索]**」ボックスで、画像検索時の強化の対象となるキーワードを指定し、「**[!UICONTROL 追加]**」をクリックまたはタップします。必要に応じて、同じ方法で複数のキーワードを指定します。

   ![add_search_word](assets/add_search_word.png)

1. 「**[!UICONTROL 保存して閉じる]**」をクリックまたはタップします。
1. 「オムニサーチ」ボックスでキーワードを検索します。 昇格させたこのキーワードの対象となるアセットが、上位の検索結果の中に表示されます。
