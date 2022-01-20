---
title: コーディングのヒント
seo-title: Coding Tips
description: AEM のコーディングのヒント
seo-description: Tips for coding for AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
exl-id: edc06f41-d0ee-45b0-b2f9-a8fa80e6a8d2
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 52%

---

# コーディングのヒント{#coding-tips}

## 可能な限り taglib または HTL を使用する {#use-taglibs-or-htl-as-much-as-possible}

スクリプトレットを JSP に含めると、コード内の問題のデバッグが難しくなります。また、JSP にスクリプトレットを含めると、ビューレイヤーとビジネスロジックを分離するのが難しくなります。これは、単一責任原則と MVC 設計パターンの違反です。

### わかりやすいコードを記述する {#write-readable-code}

コードを記述するのは一度ですが、何度も読まれます。私たちが書いたコードをきれいにするのに時間を費やすと、私たちや他の開発者は後で読む必要があるので、道端に配当を払う。

### 目的を明確に表す名前を選択する {#choose-intention-revealing-names}

別のプログラマーがモジュールを開かなくても内容がわかるようにすることが理想的です。同様に、メソッドを読まずに何をするかを知ることができるはずです。 これらのアイデアを購読すれば購読するほど、コードを読みやすくなり、コードを記述したり変更したりできるようになります。

AEM のコードベースでは、次のような規則が使用されます。


* インターフェイスの単一実装は、 `<Interface>Impl`例： `ReaderImpl`.
* 1 つのインターフェイスの複数の実装には、 `<Variant><Interface>`例： `JcrReader` および `FileSystemReader`.
* 抽象基本クラスには、 `Abstract<Interface>` または `Abstract<Variant><Interface>`.
* パッケージの名前はです `com.adobe.product.module`.  各 Maven アーティファクトまたは OSGi バンドルには、独自のパッケージが必要です。
* Java 実装は、その API の下の impl パッケージに配置します。


これらの規則を必ずお客様の実装に適用しなければならないというわけではありませんが、コードをメンテナンスしやすい状態に維持できるように、規則を定義してそれに準拠することが重要です。

名前を見れば、その目的が明らかになるようにすることが理想的です。名前が本来のように明確でない場合に対する一般的なコードテストは、変数やメソッドの目的を説明するコメントの存在です。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>不明確</strong></p> </td> 
   <td><p><strong>消去</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>int d; //elapsed time in days</p> </td> 
   <td><p>int elapsedTimeInDays;</p> </td> 
  </tr> 
  <tr> 
   <td><p>//get tagged images<br /> public List getItems() {}</p> </td> 
   <td><p>public List getTaggedImages() {}</p> </td> 
  </tr> 
 </tbody> 
</table>

### 繰り返しを避ける  {#don-t-repeat-yourself}

DRY（Don&#39;t repeat yourself）は、同じコードセットを繰り返してはならないということです。これは、文字列リテラルなどにも当てはまります。 コードの複製は、何かが変更される必要があり、探し出され、削除される必要がある場合に、欠陥の扉を開きます。

### 範囲を限定しない CSS ルールを避ける {#avoid-naked-css-rules}

CSS ルールは、アプリケーションのコンテキスト内のターゲット要素に固有でなければなりません。例えば、 *.content .center* が過度に広くなり、システム全体の多数のコンテンツに影響を与える可能性があり、将来、他のユーザーがこのスタイルを上書きする必要が生じる可能性があります。 *.myapp-centertext* 中央揃えを指定するので、より具体的なルールになります *テキスト* を設定します。

### 廃止された API を使用しない {#eliminate-usage-of-deprecated-apis}

API が廃止された場合は常に、廃止された API を使用する代わりに、推奨される新しいアプローチを確認することをお勧めします。これにより、今後のアップグレードがよりスムーズになります。

### ローカライズ可能なコードを記述する {#write-localizable-code}

作成者によって指定されない文字列は、JSP/Java の I18n.get() および JavaScript の CQ.I18n.get() を使用して AEM の i18n ディクショナリへの呼び出しでラップする必要があります。****&#x200B;この実装は、実装が見つからない場合に渡された文字列を返すので、主要言語で機能を実装した後に、柔軟にローカライゼーションを実装できます。

### 安全のためにリソースパスをエスケープする {#escape-resource-paths-for-safety}

JCR のパスにスペースを使用することはできませんが、スペースが使用されていても、コードが中断しないようにする必要があります。Jackrabbit では、escape() および escapePath() メソッドを含む Text ユーティリティクラスを提供しています。**** JSP の場合、Granite UI では *granite:encodeURIPath() EL* 関数に置き換えます。

### XSS API や HTL を使用して、クロスサイトスクリプティング攻撃を防ぐ {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM では、パラメーターを簡単にクリーンにして、クロスサイトスクリプティング攻撃に対する安全性を確保するための XSS API を提供しています。さらに、HTL ではこれらの保護機能がテンプレート言語に直接組み込まれています。 API チートシートは、次の場所でダウンロードできます。 [開発 — ガイドラインとベストプラクティス](/help/sites-developing/dev-guidelines-bestpractices.md).

### 適切なログ機能を実装する {#implement-appropriate-logging}

Java コードについては、AEM では、メッセージをログに記録するための標準 API として slf4j をサポートしており、管理の一貫性を確保するために OSGi コンソールから使用可能な設定と組み合わせて使用する必要があります。Slf4j は 5 つの異なるログレベルを公開します。 メッセージをログに記録するレベルを選択する際には、次のガイドラインを使用することをお勧めします。

* ERROR：コードが中断され、処理を続行できない場合。これは、多くの場合、予期しない例外の結果として発生します。 通常、これらのシナリオにスタックトレースを含めると便利です。
* WARN：正しく動作していない部分があるが、処理は続行できる場合。これは、多くの場合、例外が予期した結果です ( 例： *PathNotFoundException*.
* INFO：システムを監視する際に役立つ情報。これがデフォルトであり、ほとんどのお客様が環境にこの設定を残すことに注意してください。 したがって、あまり使用しないでください。
* DEBUG：処理に関するより詳細な情報。サポートを受けながら問題をデバッグする際に役立ちます。
* TRACE：メソッドの開始／終了など、最も詳細な情報。これは通常、開発者のみが使用します。

JavaScript の場合は、開発時にのみ console.log を使用し、リリース前にすべてのログステートメントを削除する必要があります。**

### カーゴカルトプログラミングを避ける {#avoid-cargo-cult-programming}

内容を理解せずに、コードをコピーしないでください。不確かな場合は、明確でないモジュールや API の経験を持つユーザーに問い合わせることをお勧めします。
