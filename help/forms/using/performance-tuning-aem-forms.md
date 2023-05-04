---
title: AEM Forms サーバーのパフォーマンスチューニング
seo-title: Performance tuning of AEM Forms server
description: AEM Formsが最適に動作するように、キャッシュ設定と JVM パラメーターを微調整できます。 また、Web サーバーを使用すると、AEM Formsデプロイメントのパフォーマンスを向上できます。
seo-description: For AEM Forms to perform optimally, you can fine-tune the cache settings and JVM parameters. Also, using a web server can enhance the performance of AEM Forms deployment.
uuid: 77eaeecc-ca52-4d3d-92e6-1ab4d91b9edd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: Configuration
discoiquuid: 5d672b56-00c4-46a0-974b-e174fbdf07d6
role: Admin
exl-id: bc750571-08a5-414c-aed5-4e839f6695ae
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 27%

---

# AEM Forms サーバーのパフォーマンスチューニング {#performance-tuning-of-aem-forms-server}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

この記事では、ボトルネックを減らし、AEM Formsデプロイメントのパフォーマンスを最適化するために実装できる戦略とベストプラクティスについて説明します。

## キャッシュ設定 {#cache-settings}

AEM Formsのキャッシュ戦略は、 **モバイルForms設定** AEM Web Configuration Console のコンポーネントの場所：

* (OSGi 上の AEM Forms) `https://[server]:[port]/system/console/configMgr`
* (JEE での AEM Forms) `https://[server]:[port]/lc/system/console/configMgr`

キャッシュに使用できるオプションを次に示します。

* **なし**:アーティファクトをキャッシュしないよう強制します。 これにより、実際にはパフォーマンスが低下し、キャッシュがないために高いメモリ可用性が必要になります。
* **保守的**:インラインフラグメントと画像を含むテンプレートなど、フォームのレンダリング前に生成される中間アーティファクトのみをキャッシュするように指示します。
* **積極的**:保守的なキャッシュレベルのすべてのアーティファクトに加えて、レンダリングされたHTMLコンテンツを含め、キャッシュ可能なほとんどすべてのものをキャッシュするよう強制します。 最高のパフォーマンスを発揮しますが、キャッシュされたアーティファクトの保存に多くのメモリを消費することもあります。 アグレッシブキャッシュ戦略では、レンダリングされたコンテンツがキャッシュされるので、フォームのレンダリング時に一定の時間パフォーマンスが得られます。

AEM Formsのデフォルトのキャッシュ設定は、最適なパフォーマンスを得るのに十分でない可能性があります。 したがって、次の設定を使用することをお勧めします。

* **キャッシュ方法**:積極的
* **キャッシュサイズ**（フォーム数）：必要に応じて
* **最大オブジェクトサイズ**：必要に応じて

![Mobile Forms の設定](assets/snap.png)

>[!NOTE]
>
>AEM Dispatcher を使用してアダプティブフォームをキャッシュする場合、事前入力されたデータを含むフォームを含むアダプティブフォームもキャッシュします。 このようなフォームがAEM Dispatcher のキャッシュから提供されると、事前入力されたデータや古いデータがユーザーに提供される場合があります。 そのため、事前入力されたデータを使用しないアダプティブフォームをキャッシュするには、AEM Dispatcher を使用します。 さらに、Dispatcher キャッシュでは、キャッシュされたフラグメントは自動的に無効化されません。 そのため、フォームフラグメントをキャッシュする場合は使用しないでください。 このようなフォームやフラグメントの場合は、 [アダプティブフォームのキャッシュ](/help/forms/using/configure-adaptive-forms-cache.md).

## JVM パラメーター {#jvm-parameters}

最適なパフォーマンスを得るために、次の JVM `init` 引数を使用して、`Java heap` と `PermGen` を設定することを推奨します。

```java
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>推奨設定は、Windows 2008 R2 8 コアおよび Oracle HotSpot 1.7 (64 ビット) JDK を対象とし、ご使用のシステム構成に従ってスケールアップまたはスケールダウンする必要があります。

## Web サーバーの使用 {#using-a-web-server}

アダプティブフォームとHTML5 フォームは、HTML5 形式でレンダリングされます。 フォームサイズやフォーム内の画像などの要因に応じて、結果の出力が大きくなる場合があります。 データ転送を最適化するための推奨されるアプローチは、要求が提供される Web サーバーを使用してHTML応答を圧縮することです。 このアプローチは、応答サイズ、ネットワークトラフィック、およびサーバーとクライアントマシンの間でのデータのストリーミングに要する時間を削減します。

例えば、JBoss を使用する Apache Web Server 2.0 32 ビット上で圧縮を有効にするには、次の手順を実行します。

>[!NOTE]
>
>次の手順は Apache Web Server 2.0 32 ビット以外のサーバーには適用されません。その他のサーバーに固有の手順については、対応する製品ドキュメントを参照してください。

次の手順で、Apache Web サーバーで圧縮を有効にするために必要な変更を示します

**お使いのオペレーティングシステムに適した Apache Web サーバーソフトウェアを入手します**

* Windows の場合：Apache Web サーバーを Apache HTTP Server Project サイトからダウンロードします。
* Solaris 64 ビット：Apache Web サーバーを Sunfreeware for Solaris Web サイトからダウンロードします。
* Linux:Apache Web サーバーは Linux システムにプレインストールされています。

Apache は HTTP プロトコルを使用して CRX と通信できます。 これらの設定は、HTTP を使用した最適化のためのものです。

1. `APACHE_HOME/conf/httpd.conf` ファイル内で次のモジュール設定をコメント解除します。

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Linux の場合、デフォルトの `APACHE_HOME` は `/etc/httpd/` です。

1. crx のポート 4502 のプロキシを設定します。

   次の設定を `APACHE_HOME/conf/httpd.conf` 設定ファイルに追加します。

   ```java
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 圧縮を有効化します。次の設定を `APACHE_HOME/conf/httpd.conf` 設定ファイルに追加します。

   **HTML5 フォームの場合**

   ```java
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **アダプティブフォームの場合**

   ```java
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   crx サーバーにアクセスするには、`https://[server]:80` を使用します。ここで、`server` は Apache サーバーが実行されているサーバーの名前です。

## AEM Formsを実行しているサーバーでのウイルス対策ソフトウェアの使用 {#using-an-antivirus-on-server-running-aem-forms}

ウイルス対策ソフトウェアを実行しているサーバのパフォーマンスが低下する場合があります。 常にウイルス対策（オンアクセススキャン）ソフトウェアでは、システムのすべてのファイルをスキャンします。 サーバーのパフォーマンスが低下する可能性があり、AEM Formsのパフォーマンスに影響が出る場合があります。

パフォーマンスを向上させるには、次のAEM Formsファイルおよびフォルダを、常にオン（オンアクセス）のスキャンから除外するようにアンチウイルスソフトウェアを指示します。

* AEMインストールディレクトリ。 完全なディレクトリを除外できない場合は、次の項目を除外します。

   * [AEM インストールディレクトリ]\crx-repository\temp
   * [AEM インストールディレクトリ]\crx-repository\repository
   * [AEM インストールディレクトリ]\crx-repository\launchpad

* アプリケーションサーバーの一時ディレクトリ。 デフォルトの場所は以下のとおりです。

   * (Jboss) [AEM インストールディレクトリ]\jboss\standalone\tmp
   * (Weblogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere) \Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(AEM Forms on JEE のみ )** グローバルドキュメントストレージ (GDS) ディレクトリ。 デフォルトの場所は以下のとおりです。

   * (JBoss) `[appserver root]/server/[server]/svcnative/DocumentStorage`
   * (WebLogic) `[appserverdomain]/[server]/adobe/LiveCycleServer/DocumentStorage`
   * (WebSphere) `[appserver root]/installedApps/adobe/[server]/DocumentStorage`

* **（JEE 上の AEM Forms のみ）** AEM Forms サーバーのログファイルと一時ディレクトリ。デフォルトの場所は以下のとおりです。

   * サーバーログ — `[AEM Forms installation directory]\Adobe\AEM forms\[app-server]\server\all\logs`
   * 一時ディレクトリ - [AEM Forms インストールディレクトリ]\temp

>[!NOTE]
>
>* GDS と一時ディレクトリに別の場所を使用している場合は、AdminUI( ) を開きます。 `https://[server]:[port]/adminui)`に移動します。 **「ホーム」>「設定」>「コアシステム設定」>「コア設定」** をクリックして、使用中の場所を確認します。
* 上記のディレクトリを除外しても AEM Forms サーバーのパフォーマンスが改善されない場合は、Java 実行可能ファイル（java.exe）も除外してください。
>

