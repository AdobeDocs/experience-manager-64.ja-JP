---
title: HTML5 フォーム内でのログの有効化
seo-title: Enable logging for HTML5 forms
description: ロガーユーティリティは、フォームのログを有効にし、フォーム関連の問題をデバッグするのに役立ちます。
seo-description: The logger utility enables logging for a form and helps you debug form-related issues.
uuid: d6279092-57f3-4fc6-b41b-9caf65459d4d
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: hTML5_forms
discoiquuid: 23bc7cd2-7d06-4ef8-977a-778e290daef9
feature: Mobile Forms
exl-id: c7953d1b-a332-4138-b744-516f3881cd4d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 55%

---

# HTML5 フォーム内でのログの有効化 {#enable-logging-for-html-forms}

ロガーユーティリティを設定して、HTML5 forms のログの作成を開始できます。 ロガーユーティリティには様々なレベルがあり、必要に応じてレベルを設定できます。 HTML5 フォームには、サーバーとクライアントのコンポーネントが含まれています。 両方のコンポーネントに対してログを設定できます。 

## サーバー側ログの設定 {#configuring-server-side-logging}

次の手順を実行して、サーバー側ログを設定します。

1. `https://[server]:[port]/system/console/configMgr` に移動します。*Apace Sling ロギングロガー設定* オプションを探して開きます。ダイアログボックスが表示されます。

   ![Apace Sling ロギングのロガー設定オプションのダイアログボックス](assets/logconfig.png)

   Apace Sling ロギングロガー設定オプション

1. **ログレベル**&#x200B;を&#x200B;**デバッグ**&#x200B;に変更します。 

1. **ログファイル**&#x200B;のパスと名前を指定します。

   >[!NOTE]
   >
   >HTML5 Forms ログディレクトリ内にログを生成する場合は、ファイル名の前に ../logs/ を追加します。

1. **ロガー**&#x200B;を **HTMLFormsPerfLogger に変更します。**「**保存**」をクリックします。

## クライアントログの設定 {#configuring-client-logging}

次の方法を使用して、HTML5 フォームでクライアント側のログを有効にすることができます。

* `log` という名前の要求パラメーターの使用
* CQ Configuration Manager の使用

### リクエストパラメーターを使用したログの有効化 {#enabling-logging-using-request-parameter}

この方法を使用すると、特定のリクエストのログを生成できます。 リクエストパラメーターの名前は **ログ**. ログ URL は次のとおりです。

`https://<server>:<port>/content/xfaforms/profiles/test.html?contentRoot=<path of the folder containing form xdp>&template=<name of the xdp>&log=<log configuration>.`

ログの設定はログレベルとロガーカテゴリで構成されています。

#### ログの宛先 {#log-destination}

<table> 
 <tbody> 
  <tr> 
   <th><strong>ログの宛先</strong></th> 
   <th><strong>説明</strong></th> 
  </tr> 
  <tr> 
   <td>1</td> 
   <td>ログはブラウザーに送信されます <strong>コンソール</strong></td> 
  </tr> 
  <tr> 
   <td>2</td> 
   <td>ログはクライアント側の JavaScript オブジェクトで収集され、に投稿できます。 <strong>サーバー</strong> </td> 
  </tr> 
  <tr> 
   <td>3</td> 
   <td>上記のオプションの両方<br /> </td> 
  </tr> 
 </tbody> 
</table>

#### ログレベル {#log-levels}

<table> 
 <tbody> 
  <tr> 
   <th>ログレベル</th> 
   <th>説明</th> 
  </tr> 
  <tr> 
   <td>0</td> 
   <td>オフ<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>1</td> 
   <td>致命的<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>2</td> 
   <td>エラー <br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>3</td> 
   <td>警告<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>4</td> 
   <td>情報<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>5</td> 
   <td>デバッグ<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>6</td> 
   <td>TRACE<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>7</td> 
   <td>すべて<br type="_moz" /> </td> 
  </tr> 
 </tbody> 
</table>

#### ロガーカテゴリ {#logger-categories}

<table> 
 <tbody> 
  <tr> 
   <th>ログカテゴリ</th> 
   <th>説明</th> 
  </tr> 
  <tr> 
   <td>a</td> 
   <td>xfa（スクリプティングエンジン関連のログ）</td> 
  </tr> 
  <tr> 
   <td>b</td> 
   <td>xfaView （レイアウトエンジン関連のログ）<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>c</td> 
   <td>xfaPerf （パフォーマンス関連ログ）<br type="_moz" /> </td> 
  </tr> 
 </tbody> 
</table>

#### ログ設定 {#log-configuration}

ログ URL では、ログ設定クエリー文字列パラメーターは次のように定義されます。

`{destination}-{a level}-{b level}-{c level}`

次に例を示します。

<table> 
 <tbody> 
  <tr> 
   <th>ログ設定</th> 
   <th>説明</th> 
  </tr> 
  <tr> 
   <td>2-a4-b5-c6<br type="_moz" /> </td> 
   <td>宛先：サーバー<br /> xfa レベル：情報<br /> xfaView レベル：デバッグ<br /> xfaPerf レベル：TRACE</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>各ログカテゴリ a(xfa)、b(xfaView) および c(xfaPerf) のデフォルトのログレベルは 2(ERROR) です。 したがって、ログ設定の場合は次のようになります。2-b6（異なるカテゴリのログレベルは次のとおりです）。\
>a（xfa）：2（デフォルトレベルのエラー）\
>b（xfaView）：6（ユーザー指定トレース）\
>a（xfaPerf）：2（デフォルトレベルのエラー）

### Configuration Manager の使用によるログの有効化 {#enabling-logging-using-configuration-manager}

ログを有効化するために Configuration Manager を使用すると、ログが再び無効化されるまで、すべてのレンダリング要求に対してログが生成されます。

1. CQ Configuration Manager に `https://[server]:[port]/system/console/configMgr` でログインし、管理者の資格情報でログインしてください。
1. を検索してクリックします。 **モバイルForms設定**.
1. 前の節で説明したように、「 Debug Options 」テキストボックスにログ設定を入力します。次に例を示します。 **2-a4-b5-c6**

   ![Forms 設定](assets/forms_configuration.png)

   Forms 設定

## ログのアップロード中 {#uploading-logs}

宛先が 1 に設定されている場合、すべてのクライアントスクリプトログメッセージがコンソールに送信されます。 管理者がサーバーログと供にこれらのログを必要とする場合は、出力先レベルを 2 に設定します。このレベルでは、すべてのログはクライアント側の JS オブジェクトに収集されて、フォームがデフォルトプロファイルでレンダリングされる場合、ツールバーの&#x200B;**既存のフィールドのハイライト**&#x200B;ボタンの左に&#x200B;**ログを送信**&#x200B;ボタンが表示されます。ユーザーがリンクをクリックすると、収集されたすべてのログはサーバーに投稿され、サーバー上の設定されたエラーログファイルに記録されます。

デフォルトでは、すべての情報が /crx-repository/logs/ ディレクトリに保存されている error.log ファイルに追加されます。

ログファイルの場所と名前を変更するには、次の手順を実行します。

1. 管理者として「 Configuration Manager」にログインします。Configuration Manager のデフォルトの URL は、`https://[*Server*]:[*Port*]/system/console/configMgr` です。
1. クリック **Apache Sling Logging Logger Configuration**. ダイアログボックスが表示されます。

   ![logconfig-1](assets/logconfig-1.png)

1. **ログレベル**&#x200B;をデバッグに変更します。 

1. **ログファイル**&#x200B;のパスと名前を指定します。

   >[!NOTE]
   >
   >他のログファイルが保存されている同じディレクトリにログを作成するには、Log Files プロパティで ../logs/&lt;filename> を指定します。

1. **Logger** を **HTMLFormsPerfLogger** に変更し、「**保存**」をクリックします。
