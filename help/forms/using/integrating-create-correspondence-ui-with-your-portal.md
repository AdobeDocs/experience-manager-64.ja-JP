---
title: カスタムポータルにおける通信を作成の UI の統合
seo-title: カスタムポータルにおける通信を作成の UI の統合
description: 通信の作成 UI とカスタムポータルを統合する方法について説明します。
seo-description: 通信の作成 UI とカスタムポータルを統合する方法について説明します。
uuid: 4ae9c5fb-bb9d-46d8-be84-455f386ab443
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
discoiquuid: cb232931-60b7-4956-bc77-10636c19325e
translation-type: tm+mt
source-git-commit: 13d364ec820b48fb8b80da2ffd30faeeb7813a28

---


# カスタムポータルにおける通信を作成の UI の統合 {#integrating-create-correspondence-ui-with-your-custom-portal}

## 概要 {#overview}

ここでは、通信を作成のソリューションをお使いの環境に統合する方法の詳細を説明します。

## URL ベースの呼び出し {#url-based-invocation}

通信を作成アプリケーションをカスタムポータルから呼び出す 1 つの方法として、次の要求パラメーターを持つ URL を準備する方法が挙げられます。

* レターテンプレートの識別子（cmLetterId パラメーターを使用）、またはレターテンプレートの名前（cmLetterName パラメーターを使用） 

* 目的のデータソースから取得した XML データの URL（cmDataUrl パラメーターを使用）

例えば、カスタムポータルでは、URLを\
`https://[server]:[port]/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`に含まれている場合は、ポータル上のリンクからのhrefを指定できます。\
ポータルに手元のレターテンプレート名がある場合、URLは\
`https://[server]:[port]/content/cm/createcorrespondence.html?cmLetterName=[letter name]&cmDataUrl=[data URL]` です。

>[!NOTE]
>
>この呼び出し方法は安全ではありません。必要なパラメーターが URL に明示される GET 要求として渡されるからです。

>[!NOTE]
>
>通信を作成アプリケーションを呼び出す前に、データを保存、アップロードして、指定された dataURL で通信を作成の UI を呼び出します。この処理は、カスタムポータル自体で実行されるか、または異なるバックエンドプロセスで実行される可能性があります。

## インラインデータベースの呼び出し {#inline-data-based-invocation}

Another (and a more secure) way to call the Create Correspondence application could be to simply hit the URL at `https://[server]:[port]/[contextPath]/aem/forms/createcorrespondence.html`, while sending the parameters and data to call the Create Correspondence application as a POST request (hiding them from the end user). つまり、通信を作成アプリケーションの XML データを（cmData パラメーターを使用して、同じ要求の一部として）インラインで渡すことができることも意味します。これは、前述のアプローチでは、不可能で、理想的ではありませんでした。

### レターを指定するパラメーター {#parameters-for-specifying-letter}

<table> 
 <tbody>
  <tr>
   <td><strong>名前</strong></td> 
   <td><strong>タイプ</strong></td> 
   <td><strong>説明</strong></td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>文字列</td> 
   <td>レターインスタンスの識別子。</td> 
  </tr>
  <tr>
   <td>cmLetterName</td> 
   <td>文字列</td> 
   <td><p>レターテンプレートの識別子。 </p> <p>サーバー上に同じ名前の CM 文字が複数存在する場合、URL の cmLetterName パラメーターによって「名前に複数の文字が使用されています」というエラーがスローされます。このような場合、URL には cmLetterName の代わりに cmLetterId パラメーターを使用します。</p> </td> 
  </tr>
  <tr>
   <td>cmLetterId</td> 
   <td>文字列</td> 
   <td>レターテンプレートの名前です。</td> 
  </tr>
 </tbody>
</table>

テーブル中のパラメーターの順序が、レターの読み込みに使用されるパラメーターの優先順位を指定します。

### XML データソースを指定するパラメーター {#parameters-for-specifying-the-xml-data-source}

<table> 
 <tbody>
  <tr>
   <td><strong>名前</strong></td> 
   <td><strong>タイプ</strong></td> 
   <td><strong>説明</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>cq、ftp、http、file などの基本的なプロトコルを使用してソースファイルから取得する XML データです。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>文字列</td> 
   <td>レターインスタンスで使用可能な xml データを使用します。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>Boolean</td> 
   <td>データディクショナリに添付されたテストデータを再利用します。</td> 
  </tr>
 </tbody>
</table>

テーブル中のパラメーターの順序が、XML データの読み込みに使用されるパラメーターの優先順位を指定します。

### その他のパラメーター {#other-parameters}

<table> 
 <tbody>
  <tr>
   <td><strong>名前</strong></td> 
   <td><strong>タイプ</strong></td> 
   <td><strong>説明</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>Boolean</td> 
   <td>「True」に設定されている場合、レターをプレビューモードで開きます<br /> </td> 
  </tr>
  <tr>
   <td>ランダム</td> 
   <td>Timestamp</td> 
   <td>ブラウザーのキャッシュに関する問題を解決します。</td> 
  </tr>
 </tbody>
</table>

cmDataURLにhttpまたはcqプロトコルを使用している場合、http/cqのURLは匿名でアクセスできる必要があります。
