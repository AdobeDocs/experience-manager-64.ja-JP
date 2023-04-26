---
title: カスタムポータルにおける通信を作成の UI の統合
seo-title: Integrating Create Correspondence UI with your custom portal
description: 通信の作成 UI をカスタムポータルに統合する方法を説明します
seo-description: Learn how to integrate create correspondence UI with your custom portal
uuid: 4ae9c5fb-bb9d-46d8-be84-455f386ab443
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
discoiquuid: cb232931-60b7-4956-bc77-10636c19325e
feature: Correspondence Management
exl-id: 8b1bbd85-66ba-4e96-917a-d768d84a417f
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 19%

---

# 通信作成用 UI のカスタムポータルへの統合 {#integrating-create-correspondence-ui-with-your-custom-portal}

## 概要 {#overview}

この記事では、通信を作成ソリューションを環境に統合する方法について詳しく説明します。

## URL ベースの呼び出し {#url-based-invocation}

カスタムポータルから通信を作成アプリケーションを呼び出す方法の 1 つは、次の要求パラメーターを使用して URL を準備することです。

* レターテンプレートの識別子（cmLetterId パラメータを使用）またはレターテンプレートの名前（cmLetterName パラメータを使用）

* 目的のデータソースから取得した XML データの URL（cmDataUrl パラメーターを使用）。

例えば、カスタムポータルは、次のような URL を準備します\
`https://[server]:[port]/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`（ポータル上のリンクからの href にすることができます）。\
ポータルにレターテンプレート名が付いている場合、URL は\
`https://[server]:[port]/content/cm/createcorrespondence.html?cmLetterName=[letter name]&cmDataUrl=[data URL]`

>[!NOTE]
>
>このような呼び出し方法では、必要なパラメーターが URL で同じ（明確に表示される）を公開することで、GETリクエストとして渡されるので、安全ではありません。

>[!NOTE]
>
>通信を作成アプリケーションを呼び出す前に、データを保存してアップロードし、指定された dataURL で通信を作成 UI を呼び出します。 これは、カスタムポータル自体から実行することも、別のバックエンドプロセスを通じて実行することもできます。

## インラインデータベースの呼び出し {#inline-data-based-invocation}

通信を作成アプリケーションを呼び出すもう 1 つの（より安全な）方法は、次の場所の URL にヒットするだけで済みます。 `https://[server]:[port]/[contextPath]/aem/forms/createcorrespondence.html`：通信を作成アプリケーションをPOSTリクエストとして呼び出すためのパラメーターとデータを送信する際に（エンドユーザーに対して非表示にする）。 つまり、以前のアプローチでは不可能で、理想的ではなかった、同じリクエストの一環として、通信を作成アプリケーションの XML データをインラインで渡すことができます。

### レターを指定するためのパラメーター {#parameters-for-specifying-letter}

<table> 
 <tbody>
  <tr>
   <td><strong>名前</strong></td> 
   <td><strong>種類</strong></td> 
   <td><strong>説明</strong></td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>文字列</td> 
   <td>レターインスタンスの ID です。</td> 
  </tr>
  <tr>
   <td>cmLetterName</td> 
   <td>文字列</td> 
   <td><p>レターテンプレートの識別子。 </p> <p>1 台のサーバー上に同じ名前の CM 文字が複数存在する場合、URL で cmLetterName パラメーターを使用すると、「名前が付いた複数の文字が存在します」というエラーがスローされます。 その場合、URL に cmLetterName ではなく cmLetterId パラメータを使用します。</p> </td> 
  </tr>
  <tr>
   <td>cmLetterId</td> 
   <td>文字列</td> 
   <td>レターテンプレートの名前。</td> 
  </tr>
 </tbody>
</table>

テーブル内のパラメーターの順序は、レターの読み込みに使用するパラメーターの優先順位を指定します。

### XML データソースを指定するためのパラメーター {#parameters-for-specifying-the-xml-data-source}

<table> 
 <tbody>
  <tr>
   <td><strong>名前</strong></td> 
   <td><strong>種類</strong></td> 
   <td><strong>説明</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>cq、ftp、http、file などの基本的なプロトコルを使用したソースファイルからの XML データ。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>文字列</td> 
   <td>レターインスタンスで使用可能な xml データを使用します。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>ブール値</td> 
   <td>データディクショナリに添付されたテストデータを再利用する。</td> 
  </tr>
 </tbody>
</table>

テーブル内のパラメーターの順序は、XML データの読み込みに使用するパラメーターの優先順位を指定します。

### その他のパラメーター {#other-parameters}

<table> 
 <tbody>
  <tr>
   <td><strong>名前</strong></td> 
   <td><strong>種類</strong></td> 
   <td><strong>説明</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>ブール値</td> 
   <td>True に設定すると、レターがプレビューモードで開きます<br /> </td> 
  </tr>
  <tr>
   <td>ランダム</td> 
   <td>Timestamp</td> 
   <td>ブラウザーのキャッシュの問題を解決するには、以下を実行します。</td> 
  </tr>
 </tbody>
</table>

cmDataURL に http または cq プロトコルを使用している場合、http または cq の URL には匿名でアクセスできます。
