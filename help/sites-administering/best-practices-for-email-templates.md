---
title: 電子メールテンプレートのベストプラクティス
description: Adobe Experience Managerで適切に開発された電子メールキャンペーンテンプレートを作成できる、電子メールデザインに関するベストプラクティスを紹介します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: best-practices, integration
exl-id: a72c0f77-458f-4ea0-b8ca-59e71fef2c5d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 67%

---

# 電子メールテンプレートのベストプラクティス{#best-practices-for-email-templates}

このドキュメントでは、適切な電子メールキャンペーンテンプレートを作成するための、電子メールデザインに関するいくつかのベストプラクティスについて説明します。

AEM で利用可能なデモキャンペーンは、これらすべてのベストプラクティスに従っています。デモキャンペーンでのベストプラクティスの実装方法は、各ベストプラクティスで説明しています。

独自のニュースレターを作成する際に、これらのベストプラクティスを利用してください。

>[!NOTE]
>
>すべてのキャンペーンコンテンツは、 `master` タイプのページ `cq/personalization/components/ambitpage`. 例えば、キャンペーン構造を計画する場合、次のようになります。
>
>* `/content/campaigns/teasers/en/campaign-promotion-global`
>
>マスターページの下に配置する必要があります。
>
>* `/content/campaigns/teasers/master/en/campaign-promotion-global`


>[!NOTE]
>
>Adobe Campaignのメールテンプレートを作成する場合は、プロパティを含める必要があります **acMapping** 値 **mapRecipient** 内 **jcr:content** 」ノードを選択しないと、Adobe Campaignテンプレートを **ページプロパティ** AEMの（フィールドが無効になっている）。

## テンプレート／ページコンポーネント {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table> 
 <tbody> 
  <tr> 
   <td><strong>ベストプラクティス</strong></td> 
   <td><strong>実装</strong></td> 
  </tr> 
  <tr> 
   <td><p>ドキュメントタイプを指定して、一貫したレンダリングを確実におこなうようにします。</p> <p>先頭に DOCTYPE を追加します（HTML または XHTML）。</p> </td> 
   <td><p>設計によって設定可能 <i>cq:doctype</i> プロパティ<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>デフォルトは、"XHTML" です。</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>"HTML_5" に変更できます。</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td> 
  </tr> 
  <tr> 
   <td><p>文字定義を指定して、特殊文字の正しいレンダリングを確実におこなうようにします。</p> <p>CHARSET 宣言（例：iso-8859-15、UTF-8）をに追加します。 &lt;head&gt;</p> </td> 
   <td><p>UTF-8 に設定します。</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td> 
  </tr> 
  <tr> 
   <td><p>を使用してすべての構造をコーディングする &lt;table&gt;要素。 より複雑なレイアウトの場合、テーブルをネストして複雑な構造を構築します。</p> <p>電子メールは、css がなくても見やすくする必要があります。</p> </td> 
   <td><p>テーブルは、コンテンツ構築でテンプレート全体にわたって使用されます。現在のところ、最大で 4 つのネストされたテーブルを使用しています（1 つの基本テーブル + 最大 3 つのネストレベル）。</p> <p>&lt;div&gt; タグは、適切なコンポーネント編集を確実におこなうために、オーサリングモードでのみ使用します。</p> </td> 
  </tr> 
  <tr> 
   <td>要素の属性（cellpadding、valign、width など）を使用してテーブルの寸法を設定します。これは、ボックスモデル構造を強制します。</td> 
   <td><p>すべてのテーブルには、以下のような必要な属性が含まれます。 <i>ボーダー</i>, <i>cellpadding</i>, <i>cellspacing</i> および <i>幅</i>.</p> <p>テーブル内の要素の位置を調整するには、すべてのテーブルセルに属性を設定します <i>valign="top"</i> 設定されている。</p> </td> 
  </tr> 
  <tr> 
   <td><p>可能であれば、モバイルでの使いやすさを考慮します。メディアクエリーを使用して、小さい画面でのテキストサイズを大きくして、リンク用に親指サイズのヒット領域を提供します。</p> <p>設計で可能であれば、電子メールをレスポンシブにします。</p> </td> 
   <td>CSS スタイルがデモデザインの説明で使用されている限り、メディアクエリーを使用してモバイルフレンドリーなバージョンを提供します。</td> 
  </tr> 
  <tr> 
   <td>すべての CSS を最初に配置するよりも、インライン CSS が優れています。</td> 
   <td><p>基盤となる HTML 構造をより効果的に実演し、ニュースレターの構造を容易にカスタマイズできるようにするには、一部の CSS 定義のみをインラインにします。</p> <p>ベーススタイルとテンプレートのバリエーションは、 &lt;head&gt; 」と入力します。 ニュースレターの最終版では、これらの CSS 定義は、HTML にインラインになっている必要があります。自動インライン化メカニズムが計画されていますが、現在は利用できません。</p> </td> 
  </tr> 
  <tr> 
   <td>CSS をシンプルに保ちます。複合スタイル宣言、短縮形コード、CSS レイアウトプロパティ、複雑なセレクターおよび疑似要素を避けます。</td> 
   <td>CSS スタイルがデモデザインの説明で使用されている限り、推奨される CSS は次のようになります。</td> 
  </tr> 
  <tr> 
   <td>電子メールの幅は、最大 600 ～ 800 pixel にする必要があります。これは、多くのクライアントで提供されるプレビューパネルのサイズ内での動作を優れたものにします。</td> 
   <td>この <i>幅</i> のコンテンツテーブルは、デモデザインでは 600px に制限されています。</td> 
  </tr> 
 </tbody> 
</table>

## 画像 {#images}

/libs/mcm/campaign/components/image

| **ベストプラクティス** | **実装** |
|---|---|
| 追加 *alt* 画像の属性 | この *alt* 属性は、画像コンポーネントに必須として定義されています。 |
| 用途 *jpg* の代わりに *png* 画像の形式 | 画像は、画像コンポーネントでは、常に、 JPG として提供されます。 |
| 用途 `<img>` 要素を使用します。 | テンプレートでは、背景画像データは使用されていません。 |
| 写真に style=&quot;display block&quot; 属性を追加します。Gmail での表示を向上できます。 | すべての画像には、デフォルトで、 *style=&quot;display block&quot;* 属性。 |

## テキストとリンク {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table> 
 <tbody> 
  <tr> 
   <td><strong>ベストプラクティス</strong></td> 
   <td><strong>実装</strong></td> 
  </tr> 
  <tr> 
   <td>CSS でスタイルの代わりに html を使用 (font-family)</td> 
   <td>RichTextEditor（例：textimage コンポーネントに含まれるもの）は、選択したテキストへのフォントファミリーおよびフォントサイズの選択および適用をサポートするようになりました。タグとしてレンダリングされます。</td> 
  </tr> 
  <tr> 
   <td>次のような基本的なクロスプラットフォームフォントを使用します。 <i>Arial, Verdana, Georgia</i> および <i>Times New Roman</i>.</td> 
   <td><p>ニュースレターのデザインによって異なります。</p> <p>デモデザインでは、Helvetica フォントが使用されますが、存在しない場合は一般的なサンセリフフォントに戻ります。</p> </td> 
  </tr> 
 </tbody> 
</table>

## 汎用 {#generic}

| **ベストプラクティス** | **実装** |
|---|---|
| W3C バリデーターを使用して、HTML コードを修正します。すべての開始タグが適切に閉じられるようにします。 | コードは検証されました。XHTML の遷移 Doctype の場合、 `<html>` 要素が見つかりません。 |
| JavaScript やFlashを気にしないでください。これらのテクノロジーは、主に E メールクライアントでサポートされていません。 | JavaScript も Flash も、ニュースレターテンプレートでは使用していません。 |
| マルチパート送信では、プレーンテキストバージョンを追加します。 | 新しいウィジェットは、ページプロパティに組み込まれ、ページコンテンツからプレーンテキストを簡単に抽出できます。これは、最終的なプレーンテキストバージョンの開始点として使用できます。 |

## キャンペーンニュースレターのテンプレートと例 {#campaign-newsletter-templates-and-examples}

AEM には、キャンペーンニュースレターを作成するためのいくつかのテンプレートおよびコンポーネントが標準で付属しています。これらのテンプレートおよびコンポーネントを使用して、カスタムのニュースレターを作成できます。

### テンプレート {#templates}

基盤を提供し、様々なコンテンツの流れを可能にするために、3 つの少しずつ違ったテンプレートのタイプが標準で用意されています。これらを使用して、カスタムニュースレターを簡単に作成できます。

すべてのユーザーが **ヘッダー**, a **フッター** および **本文** 」セクションに入力します。 body セクションの下で、各テンプレートは **列デザイン** （1、2、3 列）。

![chlimage_1-318](assets/chlimage_1-318.png)

### コンポーネント {#components}

現在、[キャンペーンテンプレート内で使用可能なコンポーネントが 7 つ](/help/sites-authoring/adobe-campaign-components.md)あります。これらのコンポーネントは、すべてアドビのマークアップ言語である **HTL** に基づいています。

| **コンポーネント名** | **コンポーネントパス** |
|---|---|
| 見出し | /libs/mcm/campaign/components/heading |
| 画像 | /libs/mcm/campaign/components/image |
| テキストおよびパーソナライゼーション | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| リンク | /libs/mcm/campaign/components/reference |
| Dynamic Media Classic( 旧称Scene7) の画像テンプレート | /libs/mcm/campaign/s7image |
| ターゲット参照 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>これらのコンポーネントは、メールコンテンツに最適化されています。つまり、このドキュメントで説明したベストプラクティスを厳密に順守します。その他の標準提供コンポーネントを使用すると、通常、これらのルールに違反します。

これらのコンポーネントについて詳しくは、[Adobe Campaign コンポーネント](/help/sites-authoring/adobe-campaign-components.md)を参照してください。
