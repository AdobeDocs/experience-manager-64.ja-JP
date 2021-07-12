---
title: Markdown
seo-title: Markdown
description: オーサリング中に、コンテンツフラグメントエディターは Markdown 構文を使用してユーザーがコンテンツを簡単に記述できるようにします。
seo-description: オーサリング中に、コンテンツフラグメントエディターは Markdown 構文を使用してユーザーがコンテンツを簡単に記述できるようにします。
uuid: 12b185a5-3d87-4d7c-8d09-8cc2726009a8
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.4/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: bde54663-9050-4a5a-93cb-7cd84ac7f071
exl-id: 209f0e02-b883-4104-8358-01cab15e5db2
feature: コンテンツフラグメント
role: User
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 95%

---

# Markdown {#markdown}

>[!CAUTION]
>
>一部のコンテンツフラグメント機能には、[AEM 6.4 Service Pack 2(6.4.2.0)以降のアプリケーション](/help/release-notes/sp-release-notes.md)が必要です。

[オーサリング](content-fragments-variations.md#authoring-your-content)中に、コンテンツフラグメントエディターは *Markdown* 構文を使用してユーザーがコンテンツを簡単に記述できるようにします。

![Markdown エディター](/help/assets/assets/cfm-6420-08.png)

次を定義できます。

* [見出し表記](/help/assets/content-fragments-markdown.md#heading-notation)
* [段落と改行](/help/assets/content-fragments-markdown.md#paragraphs-and-line-breaks)
* [リンク](/help/assets/content-fragments-markdown.md#links)
* [画像](/help/assets/content-fragments-markdown.md#images)
* [ブロック引用](/help/assets/content-fragments-markdown.md#block-quotes)
* [リスト](/help/assets/content-fragments-markdown.md#lists)
* [強調](/help/assets/content-fragments-markdown.md#emphasis)
* [コードブロック](/help/assets/content-fragments-markdown.md#code-blocks)
* [バックスラッシュエスケープ](/help/assets/content-fragments-markdown.md#backslash-escapes)

## 見出し表記 {#heading-notation}

ハッシュタグ（#）を前に付けて見出しを作成します。H1 には 1 つのハッシュタグ（#）、H2 には 2 つのハッシュタグ（##）のように使用します。最大で 6 個のハッシュタグを使用できます。次に例を示します。

    `## This is an H2`

    `### This is an H3`

    `###### This is a H6`

オプションで、テキストに等号で下線を付けて H1、マイナス符号で下線を付けて H2 を作成することもできます。次に例を示します。

    `This is an H1`

    `=============`

    `This is an H2`

    `-------------`

## 段落と改行 {#paragraphs-and-line-breaks}

段落とは、1 つ以上の空白行によって区切られている、1 つ以上の連続したテキスト行です。空白行とは、スペースまたはタブしか含まれていない行です。通常の段落はスペースまたはタブでインデントされません。

改行するには、行の末尾に 2 つ以上のスペースを付けてからリターンします。

## リンク {#links}

インラインリンクと参照リンクを作成できます。

どちらのスタイルでも、リンクテキストはブラケット `[]` で囲みます。

インラインリンクの例を次に示します。

    `This is [an example](https://example.com/ "Title") inline link.`

    `This is [an example of an email link](emailto:myaddress@mydomain.info)`

    `[This link](https://example.net/) has no title attribute.`

参照リンクの構文は次のとおりです。

    `Hey you should [checkout][0] this [cool thing][wiki] that I [made][].`

    `[0]: https://www.google.ca`

    `[wiki]: https://www.wikipedia.org`

    `[made]: https://www.stackoverflow.com`

## 画像 {#images}

画像の構文はリンクと似ています。インライン画像と参照画像を作成できます。

例えば、インライン画像の構文は次のようになります。

    `![Alt text](/path/to/img.jpg)`

    `![Alt text](/path/to/img.jpg "Optional title")`

構文の内容は次のとおりです。

* 感嘆符：! 。
* 1 組のブラケットが後に続き、その中に画像の alt 属性テキストが含まれています。
* 1 組の丸括弧が後に続き、その中に画像の URL またはパスが含まれています。さらに、title 属性を二重引用符または一重引用符で囲んで指定することもできます。

参照スタイルの画像の構文は次のとおりです。

    `![Alt text][id]`

「id」は、定義された画像参照の名前です。画像参照は、次のようにリンク参照と同じ構文を使用して定義されます。

    `[id]: url/to/image "Optional title attribute"`

## ブロック引用 {#block-quotes}

テキストを引用するときは、テキストの先頭に > 記号を付けます。次に例を示します。

    `>This is block quotes`

    `>asdhfjlkasdhlf`

    `>asdfahsdlfasdfj`

ブロック引用はネストできます。次に例を示します。

    `> This is the first level of quoting.`

    `>`

        `>> This is nested blockquote.`

    `>`

    `> Back to the first level.`

## リスト {#lists}

順序付きと順序なし両方のリストを作成できます。

順序なしリストを作成するには、&amp;ast; 記号をリストの項目の前に付けます。次に例を示します。

    `* item in list`

    `* item in list`

    `* item in list`

順序付きリストを作成するには、数字の後にピリオドを付けて、リストの項目の前に付けます。次に例を示します。

    `1. First item in list.`

    `2. Second item in list.`

    `3. Third item in list.`

## 強調 {#emphasis}

斜体または太字のスタイルをテキストに追加できます。

次のように斜体を追加できます。

    `*single asterisks*`

    `_single underscores_`

    `Keyboard shortcut: Ctrl-I (Cmd-I)`

次のようにテキストを太字にすることができます。

    `**double asterisks**`

    `__double underscores__`

    `Keyboard shortcut: Ctrl-B (Cmd-B)`

コードの範囲を示すには、逆引用符(&amp;grave;)で囲みます。 事前に書式設定されたコードブロックとは異なり、コード範囲は通常の段落内のコードを示します。

次に例を示します。

    ``Use the `printf()` function.``

## コードブロック {#code-blocks}

コードブロックは通常はソースコードを示すために使用されます。コードブロックを作成するには、1 個のタブまたは少なくとも 4 個分のスペースを使用してコードをインデントします。次に例を示します。

    `This is a normal paragraph.`

        `This is a code block.`

## バックスラッシュエスケープ {#backslash-escapes}

書式設定構文で特殊な意味を持つリテラル文字を表示するには、バックスラッシュエスケープを使用します。例えば、ある単語を（HTML の &lt;em> タグではなく）リテラルアスタリスクで囲みたい場合は、次のようにアスタリスクの前にバックスラッシュを使用します。

    `\\*literal asterisks\\*`

バックスラッシュエスケープは次の文字に使用できます。

    ` \ backslash`

    `` ` backtick``

    ` * asterisk`

    ` _ underscore`

    ` {} curly braces`

    ` [] square brackets`

    ` () parentheses`

    ` # hash mark`

    ` + plus sign`

    ` - minus sign (hyphen)`

    ` . dot`
