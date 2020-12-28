---
title: カスタムスタンドアロンインストール
seo-title: カスタムスタンドアロンインストール
description: 'スタンドアロン AEM インスタンスのインストール時に使用可能なオプションについて学習します。 '
seo-description: 'スタンドアロン AEM インスタンスのインストール時に使用可能なオプションについて学習します。 '
uuid: e1cb45c4-3b2b-4951-8f67-213072e825b3
contentOwner: Tyler Rushton
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: deploying
discoiquuid: c9e51008-6009-49a2-9c74-1c610cef2e7f
translation-type: tm+mt
source-git-commit: b7e5c42009acb5044d1112e66b8e65b528355736
workflow-type: tm+mt
source-wordcount: '1523'
ht-degree: 69%

---


# カスタムスタンドアロンインストール{#custom-standalone-install}

ここでは、スタンドアロン AEM インスタンスのインストール時に使用可能なオプションについて説明します。AEM 6 を新規インストールした後のバックエンドストレージタイプの選択について詳しくは、[ストレージ要素](/help/sites-deploying/storage-elements-in-aem-6.md)も参照してください。

## ファイル名の変更によるポート番号の変更 {#changing-the-port-number-by-renaming-the-file}

AEMのデフォルトポートは4502です。そのポートが使用できない場合、または既に使用されている場合、Quickstartは、次のように最初に使用可能なポート番号を使用するように自動的に設定します。4502, 8080, 8081, 8082, 8083, 8084, 8085, 8888, 9362, `<random>`.

また、quickstart jarファイルの名前を変更してポート番号を設定し、ファイル名にポート番号が含まれるようにすることもできます。（例：`cq5-publish-p4503.jar`、`cq5-author-p6754.jar`）。

クイックスタート jar ファイル名を変更する際に従わなければならない様々なルールがあります。

* ファイル名を変更する場合は、`cq5-publish-p4503.jar`のように`cq;`と開始する必要があります。

* ポート番号の直前には -p を付けることをお勧めします。例えば、cq5-publish-p4503.jar または cq5-author-p6754.jar のように指定します。**

>[!NOTE]
>
>ポート番号の抽出の際には以下の点にご注意ください。
>
>* ポート番号は 4 桁または 5 桁にする
>* ダッシュの後にこれらの数字を指定する
>* ファイル名に他の桁数がある場合は、ポート番号の前に`-p`を付ける必要があります。
>* ファイル名の先頭のプレフィックス「cq5」は無視される

>



>[!NOTE]
>
>開始コマンドの`-port`オプションを使用して、ポート番号を変更することもできます。

## 実行モード {#run-modes}

**実行モード**&#x200B;を使用すれば、特定の目的（オーサー、パブリッシュ、テスト、開発、イントラネットなど）に合わせてAEM インスタンスを調整できます。これらのモードでは、サンプルコンテンツの使用を制御することもできます。このサンプルコンテンツは、クイックスタートの構築前に定義され、パッケージや設定などを含めることができ、実稼働の準備が完了したインストール環境をサンプルコンテンツを含まないスリムな状態に保つ場合に特に便利です。詳しくは、次のページを参照してください。

* [実行モード](/help/sites-deploying/configure-runmodes.md)

## ファイルインストールプロバイダーの追加  {#adding-a-file-install-provider}

デフォルトでは、`crx-quickstart/install`フォルダーはファイルの監視対象です。\
このフォルダーは存在しませんが、実行時に作成できます。

バンドル、設定、またはコンテンツパッケージがこのディレクトリに配置されると、自動的に取得されてインストールされます。削除すると、アンインストールされます。\
これは、バンドル、コンテンツパッケージまたは設定をリポジトリに追加するためのもう 1 つの方法です。

この方法は次に示すいくつかの事例で特に有効です。

* 開発時に、ファイルシステムへの項目の追加が容易になります。
* 問題が発生した場合は、Web コンソールとリポジトリにアクセスできません。その際に、このディレクトリにバンドルを追加してインストールできます。
* クイックスタートを起動する前に `crx-quickstart/install` フォルダーを作成して、そこにパッケージを追加できます。

>[!NOTE]
>
>例については、[サーバー起動時にCRXパッケージを自動的にインストールする方法](https://helpx.adobe.com/experience-manager/kb/HowToInstallPackagesUsingRepositoryInstall.html)も参照してください。

## Windows サービスとしての Adobe Experience Manager のインストールと起動 {#installing-and-starting-adobe-experience-manager-as-a-windows-service}

>[!NOTE]
>
>管理者としてログオンする際に次の手順を実行するか、またはコンテキストメニューの「**管理者として実行**」オプションを使用して手順を開始／実行してください。
>
>管理者権限を持つユーザーとしてログオンしただけでは&#x200B;**不十分**&#x200B;です。管理者としてログオンしていない状態でこれらの手順の完了すると、「**アクセスが拒否されました**」というエラーが表示されます。

AEM を Windows サービスとしてインストールして起動するには：

1. crx-quickstart\opt\helpers\instsrv.bat ファイルをテキストエディターで開きます。
1. 64ビットWindowsサーバーを設定する場合は、prunsrvのすべてのインスタンスを、オペレーティングシステムに応じて、次のいずれかのコマンドに置き換えます。

   * prunsrv_amd64
   * prunsrv_ia64

   このコマンドは、32ビットJavaではなく64ビットJavaのWindowsサービスデーモンを開始する適切なスクリプトを呼び出します。

1. プロセスが複数のプロセスに分岐しないようにするには、最大ヒープサイズと PermGen JVM パラメーターの値を増やします。`set jvm_options`コマンドを探し、値を次のように設定します。

   `set jvm_options=-XX:MaxPermSize=256M;-Xmx1792m`

1. コマンドプロンプトを開き、現在のディレクトリを AEM インストールの crx-quickstart/opt/helpers フォルダーに変更し、次のコマンドを入力してサービスを作成します。

   `instsrv.bat cq5`

   サービスが作成されたことを確認するには、管理ツールコントロールパネルで「サービス」を開くか、コマンドプロンプトで「`start services.msc`」と入力します。 cq5サービスがリストに表示されます。

1. 次のいずれかの方法でサービスを起動します。

   * コントロールパネルの「サービス」で、「cq5」をクリックして、「開始」をクリックします。

   ![chlimage_1-71](assets/chlimage_1-71.png)

   * コマンドラインで、&quot;net start cq5&quot; と入力します。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Windowsは、サービスが実行中であることを示します。AEM開始とprunsrv実行可能ファイルがタスクマネージャーに表示されます。 Webブラウザーで、AEM(例えば、AEMを使用している開始ーに`http://localhost:4502`)に移動します。

   ![chlimage_1-73](assets/chlimage_1-73.png)

>[!NOTE]
>
>instsrv.bat ファイル内のプロパティ値は、Windows サービスの作成時に使用されます。instsrv.bat 内のプロパティ値を編集する場合は、サービスをアンインストールしてから再インストールする必要があります。

>[!NOTE]
>
>AEMをサービスとしてインストールする場合は、Configuration Managerの`com.adobe.xmp.worker.files.ncomm.XMPFilesNComm`のlogsディレクトリの絶対パスを指定する必要があります。

サービスをアンインストールするには、コントロールパネルの「**サービス**」で「**停止**」をクリックするか、コマンドラインでフォルダーに移動して、&quot;`instsrv.bat -uninstall cq5`&quot; と入力します。&quot;**&quot; と入力すると、コントロールパネルの「**&#x200B;サービス`net start`」のリストまたはコマンドライン内のリストからサービスが削除されます。

## 一時的な作業ディレクトリの場所の再定義 {#redefining-the-location-of-the-temporary-work-directory}

Javaマシンの一時フォルダーのデフォルトの場所は`/tmp`です。AEMは、例えばパッケージの作成時に、このフォルダーも使用します。

一時フォルダーの場所を変更する場合（例えば、空き容量の多いディレクトリが必要な場合）は、JVMパラメーターを追加して`<new-tmp-path>`を定義します。

`-Djava.io.tmpdir="/<new-tmp-path>"`

定義先は次のいずれかです。

* サーバー起動コマンドライン
* serverctl または start スクリプトの CQ_JVM_OPTS 環境パラメーター

## クイックスタートファイルから使用可能なその他のオプション  {#further-options-available-from-the-quickstart-file}

その他のオプションや名前の変更規則については、クイックスタートヘルプファイルを参照してください。このファイルは —helpオプションから利用できます。ヘルプにアクセスするには、次のように入力します。

* `java -jar cq5-<version>.jar -help`

```shell
Loading quickstart properties: default
Loading quickstart properties: instance
Setting properties from filename '/Users/Desktop/AEM/cq-quickstart-5.6.0.jar'
--------------------------------------------------------------------------------
Adobe Experience Manager Quickstart (build 20130129)                            
--------------------------------------------------------------------------------
Usage:                                                                          
 Use these options on the Quickstart command line.                              
--------------------------------------------------------------------------------

-help (--help,-h)
         Show this help message                                                 
-quickstart.server.port (-p,-port) <port>
         Set server port number                                                 
-contextpath (-c,-org.apache.felix.http.context_path) <contextpath>
         Set context path                                                       
-debug <port>
         Enable Java Debugging on port number; forces forking                   
-gui 
         Show GUI if running on a terminal                                      
-nobrowser (-quickstart.nobrowser)
         Do not open browser at startup                                         
-unpack
         Unpack installation files only, do not start the server (implies       
         -verbose)                                                              
-v (-verbose)
         Do not redirect stdout/stderr to files and do not close stdin          
-nofork
         Do not fork the JVM, even if not running on a console                  
-fork
         Force forking the JVM if running on a console, using recommended       
         default memory settings for the forked JVM.                            
-forkargs <args> [<args> ...]
         Additional arguments for the forked JVM, defaults to '-Xmx1024m        
         -XX:MaxPermSize=256m '.  Use -- to specify values starting with -,     
         example: '-forkargs -- -server'                                        
-a (--interface) <interface>
         Optional IP address (interface) to bind to                             
-pt <string>
         Process type (main/fork) - do not use directly, used when forking a    
         process                                                                
-r <string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string> [<string>]]]]]]]]]
         Runmode(s) - Use this to define the run mode(s)                        
-b <string>
         Base folder - defines the path under which the quickstart work folder  
         is created                                                             
-low-mem-action <string>
         Low memory action - what to do if memory is insufficient at startup    
-use-control-port
         Start a control port                                                   
-ll <level>
         Define launchpad log level (1 = error...4 = debug)                     
--------------------------------------------------------------------------------
Quickstart filename options                                                     
--------------------------------------------------------------------------------
Usage:                                                                          
 Rename the jar file, including one of the patterns shown below, to set the     
corresponding option. Command-line options have priority on these filename      
patterns.                                                                       
--------------------------------------------------------------------------------

-NNNN
         Include -NNNN.jar or -pNNNN in the renamed jar filename to run on port 
         NNNN, for example: quickstart-8085.jar                                 
-nobrowser
         Include -nobrowser in the renamed jar filename to avoid opening the    
         browser at startup, example: quickstart-nobrowser-8085.jar             
-publish
         Include -publish in the renamed jar filename to run cq5 in "publish"   
         mode, example: cq5-publish-7502.jar                                    
--------------------------------------------------------------------------------
The license.properties file
--------------------------------------------------------------------------------
  The license.properties file stores licensing information, created from the    
  licensing form displayed on first startup and stored in the folder from where 
  Quickstart is run.                                                            
--------------------------------------------------------------------------------
Log files
--------------------------------------------------------------------------------
  Once Quickstart has been unpacked and started, log files can be found under   
  ./crx-quickstart/logs.                                                        
--------------------------------------------------------------------------------
```

## Amazon EC2 環境への AEM のインストール {#installing-aem-in-the-amazon-ec-environment}

AEMをAmazon Elastic Compute Cloud(EC2)インスタンスにインストールする場合、EC2インスタンスにauthorとpublishの両方をインストールすると、AEM](/help/sites-deploying/custom-standalone-install.md)のインスタンスを[インストールする手順に従って、作成者インスタンスが正しくインストールされます。ただし、発行インスタンスは作成者になります。

EC2 環境にパブリッシュインスタンスをインストールする前に、次の手順を実行してください。

1. インスタンスを初めて起動する前に、パブリッシュインスタンスの jar ファイルを展開します。ファイルを展開するには、次のコマンドを使用します。

   ```xml
   java -jar quickstart.jar -unpack
   ```

   >[!NOTE]
   >
   >インスタンスを初めて起動した&#x200B;**後**&#x200B;にモードを変更する場合は、実行モードを変更できません。

1. 次のコマンドを実行してインスタンスを起動します。

   ```xml
   java -jar quickstart.jar -r publish
   ```

   >[!CAUTION]
   >
   >上記のコマンドを実行してインスタンスを展開した後は、最初にそのインスタンスを実行してください。そうしないと、quickstart.properties ファイルが生成されません。このファイルが生成されない場合は、以降の AEM のアップグレードが失敗します。

1. **bin** フォルダー内の **start** スクリプトを開いて、次のセクションを確認します。

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='author'
   fi
   ```

1. 実行モードを&#x200B;**パブリッシュ**&#x200B;に変更して、ファイルを保存します。

   ```xml
   # runmode(s)
   if [ -z "$CQ_RUNMODE" ]; then
    CQ_RUNMODE='publish'
   fi
   ```

1. インスタンスを停止し、**start** スクリプトを実行して再起動します。

## インストールの確認  {#verifying-the-installation}

次のリンクを使用して、インストールが機能していることを確認できます（すべての例では、インスタンスが localhost のポート 8080 で実行されていること、および CRX が /crx に、Launchpad が / の下にインストールされていることを前提としています）。

* `http://localhost:8080/crx/de`

   CRXDE Liteコンソール。

* `http://localhost:8080/system/console`

   Webコンソール

## インストール後のアクション {#actions-after-installation}

AEM WCM の様々な設定を行うことができますが、インストール直後には特定のアクションを実行するか、または少なくとも確認が必要な項目があります。

* お使いのシステムが安全であることを確認するために必要なタスクについては、[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。
* AEM WCM と共にインストールされたデフォルトのユーザーとグループのリストを確認します。また、他のアカウントに対してアクションを実行するかどうかを確認します。詳しくは、[ユーザー管理とセキュリティ](/help/sites-administering/security.md)を参照してください。

## CRXDE Lite および Web コンソールへのアクセス  {#accessing-crxde-lite-and-the-web-console}

AEM WCM を起動したら、次の場所にアクセスできます。

* [CRXDE Lite](#accessing-crxde-lite) - リポジトリにアクセスする場合やリポジトリを管理する場合に使用します。
* [Web コンソール](#accessing-the-web-console) - OSGi バンドル（OSGi コンソールとも呼ばれる）を管理または設定する場合に使用します。

### CRXDE Lite へのアクセス  {#accessing-crxde-lite}

CRXDE Liteを開くには、ようこそ画面から&#x200B;**CRXDE Lite**&#x200B;を選択するか、ブラウザを使用して

```
 https://<<i>host</i>>:<<i>port</i>>/crx/de/index.jsp
```

次に例を示します。\
`http://localhost:4502/crx/de/index.jsp` &quot;

![installcq_crxdelite](assets/installcq_crxdelite.png)

### Accessing the Web Console {#accessing-the-web-console}

Adobe CQのWebコンソールにアクセスするには、ようこそ画面から&#x200B;**OSGiコンソール**&#x200B;を選択するか、ブラウザを使用して

```
 https://<<i>host</i>>:<<i>port</i>>/system/console
```

次に例を示します。\
`http://localhost:4502/system/console`\
またはBundlesページ用\
`http://localhost:4502/system/console/bundles`

![chlimage_1-74](assets/chlimage_1-74.png)

詳しくは、[Web コンソールでの OSGi 設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)を参照してください。

## トラブルシューティング {#troubleshooting}

インストール中に発生する可能性のある問題の処理について詳しくは、以下を参照してください。

* [トラブルシューティング](/help/sites-deploying/troubleshooting.md)

## Adobe Experience Manager のアンインストール  {#uninstalling-adobe-experience-manager}

AEM は単一のディレクトリにインストールされるので、アンインストールユーティリティは必要ありません。インストールディレクトリ全体を削除するだけでアンインストールできます。ただし、AEM のアンインストール方法は、その目的および使用している永続ストレージによって変わります。

例えば、デフォルトの TarPM インストールなど、永続ストレージがインストールディレクトリに埋め込まれている場合、フォルダーを削除するとデータも削除されます。

>[!NOTE]
>
>AEM を削除する前にリポジトリをバックアップすることを強く推奨します。&lt;cq-installation-directory> 全体を削除すると、リポジトリも削除されます。削除する前にリポジトリのデータを保管する場合は、&lt;cq-installation-directory>/crx-quickstart/repository フォルダーを他の場所に移動またはコピーしてから、その他のフォルダーを削除するようにしてください。

例えば、データベースサーバーなど、AEM のインストールが外部ストレージを使用している場合、フォルダーを削除してもデータは自動的には削除されませんが、ストレージ設定が削除されるので、JCR コンテンツの復元は困難になります。
