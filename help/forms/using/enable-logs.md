---
title: HTML5 フォーム内でのログの有効化
seo-title: Enable logging for HTML5 forms
description: ロガーユーティリティはフォームのログを可能にし、フォーム関連の問題のデバッグに役立ちます。
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
ht-degree: 71%

---

# HTML5フォーム内でのログの有効化 {#enable-logging-for-html-forms}

ロガーユーティリティを設定することで、HTML5フォームでログの作成を開始することができます。ロガーユーティリティにはいくつかのレベルがあり、要件に応じてレベルを設定することができます。HTML5フォームは、サーバーコンポーネントとクライアントコンポーネントから構成されています。両方のコンポーネントに対してログを設定できます。 

## サーバー側のログの設定 {#configuring-server-side-logging}

次の手順を実行して、サーバーサイドログを構成します。

1. `https://[server]:[port]/system/console/configMgr` にアクセスします。を探して開きます。 *Apace Sling ログロガー設定* オプション。 ダイアログボックスが表示されます。

   ![ Apace Sling ロギングのロガー設定オプションのダイアログボックス](assets/logconfig.png)

   Apace Sling ロギングロガー設定オプション

1. **ログレベル**&#x200B;を&#x200B;**デバッグ**&#x200B;に変更します。 

1. の名前とパスを指定します。 **ログファイル**.

   >[!NOTE]
   >
   >HTML5 フォームログディレクトリ内にログを生成する場合は、ファイル名の前に ../logs/ を追加します。

1. **Logger** を HTMLFormsPerfLogger **に変更します。**「**保存**」をクリックします。

## クライアントロギングの設定 {#configuring-client-logging}

次の方法により、HTML5 フォームのクライアント側のロギングを有効にできます。

* `log` という名前の要求パラメーターの使用
* CQ Configuration Manager の使用

### 要求パラメーターの使用によるログの有効化 {#enabling-logging-using-request-parameter}

この方法を使用して、特定の要求に対するログを生成できます。要求パラメーターの名前は **log** です。ログ URL は次のとおりです。

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
   <td>ログはブラウザーの<strong>コンソール</strong>に送信されます。</td> 
  </tr> 
  <tr> 
   <td>2</td> 
   <td>ログはクライアント側の JavaScript オブジェクトに収集され、<strong>サーバー</strong>にポストできます。 </td> 
  </tr> 
  <tr> 
   <td>3</td> 
   <td>両方の上記のオプション<br /> </td> 
  </tr> 
 </tbody> 
</table>

#### ログのレベル {#log-levels}

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
   <td>FATAL<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>2</td> 
   <td>ERROR<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>3</td> 
   <td>WARN<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>4</td> 
   <td>INFO<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>5</td> 
   <td>DEBUG<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>6</td> 
   <td>TRACE<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>7</td> 
   <td>ALL<br type="_moz" /> </td> 
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
   <td>がない場合、</td> 
   <td>xfa （スクリプティングエンジン関連ログ）</td> 
  </tr> 
  <tr> 
   <td>b</td> 
   <td>xfaView （レイアウトエンジン関連ログ）<br type="_moz" /> </td> 
  </tr> 
  <tr> 
   <td>c</td> 
   <td>xfaPerf （パフォーマンス関連ログ）<br type="_moz" /> </td> 
  </tr> 
 </tbody> 
</table>

#### ログの設定 {#log-configuration}

ログ URL では、ログ設定クエリーの文字列パラメーターは次のとおりに定義します。

`{destination}-{a level}-{b level}-{c level}`

次に例を示します。

<table> 
 <tbody> 
  <tr> 
   <th>ログの設定</th> 
   <th>詳細</th> 
  </tr> 
  <tr> 
   <td>2-a4-b5-c6<br type="_moz" /> </td> 
   <td>保存場所：Server<br /> xfa レベル：INFO<br /> xfaView レベル：DEBUG<br /> xfaPerf レベル： TRACE</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>a（xfa）、b（xfaView）、および c（xfaPerf）のそれぞれのログカテゴリに対するデフォルトログレベルは 2（エラー）です。そのため、ログ設定 2-b6 では、異なるカテゴリのログレベルは：\
>a (xfa):2 （デフォルトレベルのエラー）\
>b (xfaView):6 ( ユーザー指定TRACE)\
>a (xfaPerf):2 （デフォルトレベルのエラー）

### Configuration Manager の使用によるログの有効化 {#enabling-logging-using-configuration-manager}

ログを有効にするために Configuration Manager を使用すると、ログが再び無効になるまで、レンダリング要求ごとにログが生成されます。

1. CQ Configuration Manager( ) にログインします。 `https://[server]:[port]/system/console/configMgr` 管理者の資格情報を使用してログインします。
1. **「LC Forms Configurations」**&#x200B;を探してクリックします。
1. 「Debug Options」テキストボックスで、前のセクションで説明されたとおりにログ設定を入力します。例：**2-a4-b5-c6**

   ![Forms 設定](assets/forms_configuration.png)

   Forms 設定

## ログのアップロード {#uploading-logs}

宛先が 1 として設定されている場合、すべてのクライアントスクリプトのログメッセージはコンソールに送信されます。管理者がサーバーログと共にこれらのログを必要とする場合は、宛先レベルを 2 に設定します。 このレベルでは、すべてのログはクライアント側の JS オブジェクトに収集され、フォームがデフォルトのプロファイルでレンダリングされる場合は、 **ログを送信** ボタンが **既存のフィールドをハイライト** 」ボタンをクリックします。 ユーザーがリンクをクリックすると、収集したすべてのログがサーバーに投稿され、サーバー上の設定済みエラーログファイルに記録されます。

デフォルトでは、すべての情報が /crx-repository/logs/ ディレクトリに保存されている error.log ファイルに追加されます。

ログファイルの場所と名前を変更するには、次の操作を実行します。

1. 管理者として「Configuration Manager」にログインします。Configuration Manager のデフォルトの URL は、 `https://[*Server*]:[*Port*]/system/console/configMgr`.
1. **「Apace Sling ロギングロガー設定」**&#x200B;をクリックします。ダイアログボックスが表示されます。

   ![logconfig-1](assets/logconfig-1.png)

1. **ログレベル**&#x200B;をデバッグに変更します。 

1. パスと名前を指定 **ログファイル**.

   >[!NOTE]
   >
   >他のログファイルが保存されている同じディレクトリにログを作成するには、Log Files プロパティで ../logs/&lt;filename> を指定します。

1. を **ロガー** から **HTMLFormsPerfLogger** をクリックし、 **保存**.
