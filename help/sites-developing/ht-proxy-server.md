---
title: プロキシサーバーツールを使用する方法
seo-title: How to use the Proxy Server Tool
description: プロキシサーバーは、クライアントとサーバーの間で要求を中継する中間サーバーとして機能します
seo-description: The proxy server acts as an intermediate server that relays requests between a client and a server
uuid: 30f4f46d-839e-4d23-a511-12f29b3cc8aa
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: dfbc1d2f-80c1-4564-a01c-a5028b7257d7
exl-id: 63f3a172-b551-433a-aad5-58c6bfda82bb
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 29%

---

# プロキシサーバーツールを使用する方法{#how-to-use-the-proxy-server-tool}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

プロキシサーバは、クライアントとサーバとの間で要求を中継する中間サーバとして機能します。 プロキシサーバは、クライアントとサーバとの間のすべてのやり取りを追跡し、TCP 通信全体のログを出力します。 これにより、メインサーバーにアクセスする必要なく、何が起こっているかを正確に監視できます。

プロキシサーバーは AEM インストール環境の次の場所にあります。

`crx-quickstart/opt/helpers/proxy-2.1.jar`

プロキシサーバーを使用すると、基になる通信プロトコルに関係なく、クライアントとサーバーの間のすべてのやり取りを監視できます。 例えば、次のプロトコルを監視できます。

* Web ページの HTTP
* セキュリティで保護された Web ページの HTTPS
* 電子メールメッセージ用の SMTP
* ユーザー管理用の LDAP

たとえば、TCP/IP ネットワークを介して通信する 2 つのアプリケーション間にプロキシサーバーを配置できます。例： Web ブラウザーとAEM。 これにより、CQ ページの要求時の状況を正確に監視できます。

## プロキシサーバーツールの起動 {#starting-the-proxy-server-tool}

コマンドラインでサーバーを起動します。

`java -jar proxy-2.1.jar <host> <remoteport> <localport> [options]`

**パラメーター**

`<host>`

接続先の CRX インスタンスのホストアドレスです。インスタンスがローカルマシン上にある場合、このアドレスは `localhost` になります。

`<remoteport>`

ターゲット CRX インスタンスのホストポートです。例えば、新しくインストールする AEM インストールのデフォルト値は **`4502`** です。また、新しくインストールする AEM オーサーインスタンスのデフォルト値は `4502` です。

`<localport>`

プロキシ経由で CRX インスタンスにアクセスするために接続するローカルマシン上のポートです。

**オプション**

`-q`（クワイエットモード）

出力をコンソールウィンドウに書き込みません。 接続速度を低下させたくない場合や、出力をファイルに記録する場合（ —logfile オプションを参照）に、このオプションを使用します。

`-b`（バイナリモード）

トラフィックで特定のバイトの組み合わせを探している場合は、バイナリモードを有効にします。 次に、16 進数と文字の出力が出力されます。

`-t`（タイムスタンプのログエントリ）

各ログ出力にタイムスタンプを追加します。 タイムスタンプは秒単位なので、単一のリクエストの確認には適さない場合があります。 この関数を使用して、長い期間プロキシサーバーを使用する場合は、特定の時間に発生したイベントを見つけます。

`-logfile <filename>`（ログファイルへの書き込み）

クライアントとサーバーの会話をログファイルに書き込みます。 このパラメーターは、クワイエットモードでも機能します。

**`-i <numIndentions>`**（インデントの追加）

アクティブな各接続は、読みやすくするためにインデントされます。 初期設定は 16 レベルです。 この機能は `proxy.jar version 1.16` で導入されました。

### ログ形式 {#log-format}

proxy-2.1.jar が生成するログエントリはすべて次の形式になります。

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

例えば、Web ページのリクエストは次のようになります。

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C は、このエントリがクライアントから送信されたことを示します（Web ページのリクエストです）
* 0 は接続番号です（接続カウンターは 0 から始まります）
* #00000バイトストリーム内のオフセット。これは最初のエントリなので、オフセットは 0 です。
* `[GET <?>]` は、サンプルの HTTP ヘッダー（url）におけるリクエストのコンテンツです。

接続を閉じると、次の情報がログに記録されます。

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

これは、6 番目の接続において平均速度でクライアント（`C`）とサーバー（`S`）間でやり取りされたバイト数を示します。

**ログ出力の例**

例えば、要求されたときに次のコードを生成するページを考えてみましょう。

### 例 {#example}

例として、次のリポジトリにある非常にシンプルな html ドキュメントについて考えてみましょう。

`/content/test.html`

さらに、次の画像ファイルがあります。

`/content/test.jpg`

`test.html` のコンテンツは次のとおりです。

```xml
<html>
<head>
    <title>Test</title>
</head>  
<body>
    Test<br>
    <img src="test.jpg">
</body>
</html>
```

AEM インスタンスが `localhost:4502` で実行されている場合は、次のようにプロキシを起動します。

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

これで、`localhost:4444` にあるプロキシ経由で CQ／CRX インスタンスにアクセスできます。このポート経由のすべての通信は `test.log` に記録されます。

プロキシの出力を見ると、ブラウザーとAEMインスタンスの間のインタラクションが表示されます。

起動時に、プロキシは次の出力を行います。

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

ブラウザーを開いてテストページにアクセスします。

`http://localhost:4444/content/test.html`

ブラウザーがそのページの `GET` リクエストをおこなったことを確認します。

```shell
C-0-#000000 -> [GET /content/test.html HTTP/1.1 ]
C-0-#000033 -> [Host: localhost:4444 ]
C-0-#000055 -> [Connection: keep-alive ]
C-0-#000079 -> [User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11 ]
C-0-#000212 -> [Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8 ]
C-0-#000285 -> [Accept-Encoding: gzip,deflate,sdch ]
C-0-#000321 -> [Accept-Language: en-US,en;q=0.8 ]
C-0-#000354 -> [Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3 ]
C-0-#000402 -> [Cookie: login-token=179ba6bd-e0a7-4909-a965-e11c7f2bc2fc%3a618bd8a8-fbaf-43c5-827d-c84c62248c5e_22ee860cc9036fee%3acrx.default%3b21148fb0-eb6c]
C-0-#000543 -> [-43c9-a2b9-c8d40618d8ae%3ad87a3d1a-5e9a-4d5a-bab1-0ee60ad6d8df_d0e4ddce0fcd84b6%3acrx.default%3b5cb95227-ea51-47bf-850b-68ad1dfd7297%3af3bbb6]
C-0-#000684 -> [59-7913-4285-8857-832c087bafd5_c484727d3b3665ad%3acrx.default; ys-cq-siteadmin-tree=o%3Awidth%3Dn%253A240%5EselectedPath%3Ds%253A/content ]
C-0-#000824 -> [ ]
```

AEM インスタンスが `test.html` ファイルのコンテンツを使用して応答します。

```shell
S-0-#000000 -> [HTTP/1.1 200 OK ]
S-0-#000017 -> [Connection: Keep-Alive ]
S-0-#000041 -> [Server: Day-Servlet-Engine/4.1.24  ]
S-0-#000077 -> [Content-Type: text/html;charset=utf-8 ]
S-0-#000116 -> [Content-Length: 104 ]
S-0-#000137 -> [Date: Mon, 16 Jul 2012 11:23:38 GMT ]
S-0-#000174 -> [Last-Modified: Mon, 16 Jul 2012 11:19:27 GMT ]
S-0-#000220 -> [ ]
S-0-#000222 -> [<html>]
S-0-#000229 -> [<head>]
S-0-#000236 -> [    <title>Test</title>]
S-0-#000260 -> [</head> ]
S-0-#000269 -> [<body>]
S-0-#000276 -> [ Test<br>]
S-0-#000286 -> [    <img src="test.jpg">]
S-0-#000311 -> [</body>]
S-0-#000319 -> [</html>]
```

### プロキシサーバーの使用 {#uses-of-the-proxy-server}

次のシナリオは、プロキシサーバーを使用する目的のいくつかを示しています。

**cookie とその値の確認**

次のログエントリの例は、プロキシの開始後に開かれた 6 番目の接続でクライアントが送信したすべての cookie とその値を示しています。

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**ヘッダーとその値の確認**

次のログエントリの例は、サーバーがキープアライブ接続を確立でき、コンテンツの長さのヘッダーが正しく設定されたことを示しています。

```
S-7-#000017 -> [Connection: Keep-Alive ]
 ...
 S-7-#000107 -> [Content-Length: 124 ]
```

**キープアライブが機能するかどうかの確認**

キープアライブは、HTTP の機能で、クライアントがサーバーへの TCP 接続を再利用して、複数のリクエスト（ページコード、画像、スタイルシートなど）を実行できます。 キープアライブを使用しない場合、クライアントはリクエストごとに新しい接続を確立する必要があります。

キープアライブが機能するかどうかを確認するには：

* プロキシサーバーを起動します。
* ページをリクエストします。
* キープアライブが機能している場合、接続カウンターは 5～10 接続を超えないでください。
* キープアライブが機能していない場合、接続カウンターは急速に増加します。

**失われたリクエストの検索**

複雑なサーバー設定（ファイアウォールや Dispatcher など）でリクエストが失われた場合、プロキシサーバーを使用して、リクエストが失われた場所を特定できます。 ファイアウォールの場合：

* ファイアウォールの前にプロキシを開始
* ファイアウォール後に別のプロキシを開始する
* これらを使用して、リクエストの取得範囲を確認します。

**要求のハング**

リクエストが時々ハングする場合：

* プロキシを開始します。
* アクセスログを待つか、タイムスタンプを持つ各エントリを含むファイルに書き込みます。
* リクエストがハングし始めると、開いている接続の数と、問題を引き起こしているリクエストを確認できます。
