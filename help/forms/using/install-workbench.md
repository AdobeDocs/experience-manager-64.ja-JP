---
title: workbench のインストール
seo-title: Install workbench
description: workbench をインストールします。
uuid: null
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: null
source-git-commit: 19dcda357b34e7160792d43cb9335fc3be0dedbc
workflow-type: tm+mt
source-wordcount: '2743'
ht-degree: 56%

---


# workbench のインストール {#install-workbench}

このドキュメントでは、Workbench のインストールと設定の手順を示します。このインストールプログラムは Designer もインストールします。

## について {#about}

このドキュメントは、インストール、設定、管理または Workbench のデプロイを担当している管理者または開発者を対象としています。アップグレードされた Adobe® AEM forms® Enterprise Suite（ES）Update 1（8.2.x）および Adobe® AEM forms® Enterprise Suite 2（ES2）プロセスをサポートするためのシステム設定に必要な情報も含まれています。このドキュメントで扱う内容は、Microsoft® Windows®オペレーティングシステムに関する十分な知識を持つユーザーを対象としています。

## 追加情報 {#additional-information}

この表のリソースは、 AEM Formsの詳細情報と使用の開始に役立ちます。
<table> 
 <tbody> 
  <tr> 
   <td><p><strong>情報</strong></p> </td> 
   <td><p><strong>参照先</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Workbench の手順に関する情報</p> </td> 
   <td><p><a href="http://www.adobe.com/go/learn_aemforms_workbench_61">Workbench ヘルプ</a><br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>AEM Formsと他のAdobe製品との統合に関する一般情報</p> </td> 
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">AEM Formsの概要</a><br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>AEM Formsアプリケーションを作成し、Workspace でテストするためのチュートリアル</p> </td> 
   <td><p><a href="http://adobe.com/go/learn_aemforms_firstapp_ds_65">最初のAEM Formsアプリケーションの作成</a><br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>AEM Formsで利用できるすべてのドキュメント</p> </td> 
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">AEM Formsドキュメント</a><br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>AEM Formsと統合するその他のサービスおよび製品</p> </td> 
   <td><p><a href="http://www.adobe.com/jp/">www.adobe.com</a><br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>現在のバージョンに関するパッチアップデート、テクニカルノート、および追加情報</p> </td> 
   <td><p><a href="https://www.adobe.com/account/sign-in.supportportal.html">アドビの販売代理店にお問い合わせください。</a><br /><br /> </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>AEM FormsのFlex Workspace は非推奨（廃止予定）となりました。 AEM Formsリリースで使用できます。

## インストールの準備 {#before-you-install}

### Workbench のインストールの概要 {#workbench-installation-overview}

Workbench は、開発者およびフォーム作成者が自動化されたビジネスプロセスおよびフォームを作成するための統合開発環境（IDE）です。また、Workbench はそれらのプロセスおよびフォームで使用するリソースやサービスを管理するためにも使用されます。

次の図に、以下を含む Workbench のインストールについて示します。
* Workbench を使用した Process Design
* Designer を使用した Form Design

>[!NOTE]
>
>AEM Formsサーバーには、別のインストールプログラムが必要です。 詳しくは、 JEE 上のAEM Formsのインストールに関するドキュメントを参照してください。

## システムの前提条件 {#system-prerequisites}

このセクションでは、ハードウェアとソフトウェアの要件、およびサポートされるプラットフォームについて説明します。

### ハードウェアおよびソフトウェアの最小要件 {#minimum-hardware-software-requirements}

**Workbench**
最低限、次の要件をお勧めします。インストール用のディスク容量：
* 680 MB（Workbench のみの場合）.
* 2.15 GB（Workbench 、Designer およびサンプルアセンブリを 1 つのドライブにフルインストールした場合）.
* 一時インストールディレクトリ用に 400 MB（ユーザーの ¥temp ディレクトリに 200 MB、Windows 一時ディレクトリに 200 MB）.

>[!NOTE]
>
>これらの場所がすべて 1 台のドライブ上に存在する場合は、インストール時に 1.5 GB の空き容量が必要です。 一時ディレクトリにコピーされるファイルは、インストールが完了すると削除されます。

* ハードウェア要件： Intel® Pentium® 4 または AMD の同等の 1 GHz プロセッサー.
* （から）最新バージョンのAdobe AIRをダウンロードしてインストールする <a href="http://www.adobe.com/">www.adobe.com</a>) は、Workbench と統合された Community Help Client に必要です。
* Java™ Runtime Environment(JRE)6.0 Update 22 以降の 6.0 への更新 *10 の新機能*.
* 1024 X 768 ピクセル以上のモニター解像度、16 ビットカラー以上.
* AEM Formsサーバーへの TCP/IPv4 または TCP/IPv6 ネットワーク接続。
* Visual C++再頒布可能ランタイムパッケージ 2012 32 ビットをインストールします。
* Visual C++ 2013 32 ビット再頒布可能ランタイムパッケージをインストールします。

>[!NOTE]
>
>Adobe® Acrobat X がマシンにインストールされている場合は、アンインストールしてから Workbench をインストールしてください。 Acrobat は、Workbench のインストール後に再インストールできます。

>[!NOTE]
>
>Workbench をインストールするには、管理者権限が必要です。管理者以外のアカウントを使用してインストールする場合は、適切なアカウントの資格情報が求められます。

### サポートされているプラットフォーム {#supported-platforms}

Workbench でサポートされているプラットフォームの完全なリスト ( [AEM Forms Supported Platforms](http://adobe.com/go/learn_aemforms_supportedplatforms_65_jp).

## Designer のインストールに関する考慮事項 {#designer-installation-considerations}

Workbench のインストールには、対応する Designer（英語版のみ）がデフォルトで含まれています。Workbench インストールアプリケーションがコンピューター上に Designer の既存のバージョンを検出した場合は、インストールが終了する場合があり、続行する前に現在のバージョンの Designer を削除する必要があります。
次の表に、発生する可能性のある Designer のすべてのインストールシナリオと、Workbench をインストールするときに行う必要のあるすべてのアクションを一覧で示します。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>現在インストールされている Designer のバージョン</strong></p> </td> 
   <td><p><strong>必要なアクション</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Acrobat Pro または Acrobat Pro Extended（Designer が付属）</p> </td> 
   <td><p>なし. Workbench のインストールで、Acrobat Pro または Acrobat Pro Extended と共にインストールされた Designer のインスタンスがコンピューター上で検出されます。異なるバージョンの Designer は、同じシステム上で共存できます（例：Designer 8.2.x と 9.0.x）。Acrobat 10 Pro またはAcrobat 10 Pro Extended と共にインストールされている Designer のバージョンをアンインストールする必要はありません。
<br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>Designer（スタンドアロン）</p> </td> 
   <td><p>なし. Workbench に付属する Designer のバージョンは英語版のみです。Workbench インストーラーでは、新しいバージョンの Designer は再インストールされません。代わりに、Workbench インストーラーにバンドルされている更新バージョンにパッチが適用されます。これにより、ローカライズバージョンの Designer を Workbench 内で使用することができます。<br /> <br /> </p> </td> 
  </tr> 
 </tbody> 
</table>

### Designer（スタンドアロン）をアンインストールするには {#uninstall-designer-standalone}

1. に移動します。 **Campaign コントロールパネル/プログラム/プログラムと機能**
1. 「現在インストールされているプログラム」リストで、「**Adobe Designer**」を選択します。
1. クリック **アンインストール** 次に、 **はい**.

### Windows 10 で Designer（スタンドアロン）をアンインストールするには {#uninstall-designer-standalone-windows10}

1. に移動します。 **Campaign コントロールパネル/プログラム/プログラムと機能**
1. 「現在インストールされているプログラム」リストで、「**Adobe Designer**」を選択します。
1. クリック **アンインストール** 次に、 **はい**.

### Acrobat ProまたはAcrobat Pro Extended に付属の Designer をアンインストールするには {#uninstall-designer-included-with-acrobatpro-or-acrobatextended}

1. に移動します。 **Campaign コントロールパネル/プログラム/プログラムと機能**
1. 「現在インストールされているプログラム」リストで、「**Adobe Acrobat Pro**」または「**Adobe Acrobat Pro Extended**」を選択します。
1. クリック **変更** 次に、 **次へ**.
1. 選択 **変更** 次に、 **次へ**.
1. 選択 **Adobeデザイナ**&#x200B;を選択します。 **この機能は使用できません**&#x200B;をクリックし、 **次へ**
1. クリック **更新** 次に、 **完了**

### Windows 10 でAcrobat ProまたはAcrobat Pro Extended に付属の Designer をアンインストールするには {#uninstall-designer-included-with-acrobatpro-or-acrobatextended-windows10}

1. に移動します。 **Campaign コントロールパネル/プログラム/プログラムと機能**
1. 「現在インストールされているプログラム」リストで、「**Adobe Acrobat Pro**」または「**Adobe Acrobat Pro Extended**」を選択します。
1. クリック **変更** 次に、 **次へ**.
1. 選択 **変更** 次に、 **次へ**.
1. 選択 **Adobeデザイナ**&#x200B;を選択します。 **この機能は使用できません**&#x200B;をクリックし、 **次へ**
1. クリック **更新** 次に、 **完了**

## Workbench のインストール {#installing-workbench}

この章では、Workbench をインストールする方法について説明します。

### Workbench のインストールと実行 {#installing-and-running-workbench}

Workbench をインストールする前に、Workbench の実行に必要なソフトウェアとハードウェアが環境に含まれていることを確認する必要があります（次の節を参照）。 **インストールの前に**) をクリックします。

**Workbench をインストールして実行するには：**

1. 次のいずれかのタスクを実行します。
   * インストールメディアの ¥workbench ディレクトリに移動して、run_windows_installer.bat ファイルをダブルクリックします。
   * Workbench をファイルシステムにダウンロードして解凍します。ダウンロード後、¥workbench ディレクトリに移動して run_windows_installer.bat ファイルをダブルクリックします。

   >[!IMPORTANT]
   >
   >Workbench インストーラーは、DVD またはローカルドライブからのみ実行できます。リモートサイトから実行することはできません。

   >[!NOTE]
   >
   >「Java 仮想マシンを作成できませんでした」というエラーが発生した場合は、値が —Xmx512M の_JAVA_Virtuals という環境変数を作成し、OPTIONSを実行します。

1. はじめに画面で「次へ」をクリックします。
1. 使用許諾契約書を読み、「使用許諾契約書の条件に同意します」を選択して、「次へ」をクリックします。
1. （オプション）フォームを作成および変更するツールが必要な場合は、「Adobe Designer のインストール」を選択します。

   >[!NOTE]
   >
   >Acrobat 10 と共にインストールされた Designer を引き続き使用するには、このオプションの選択を解除したままにします。

1. 表示されたデフォルトのディレクトリをそのまま使用するか、「選択」をクリックして Workbench をインストールするディレクトリに移動し、「次へ」をクリックします。

   >[!NOTE]
   >
   >インストールディレクトリのパスには、#（ポンド）および $（ドル）文字を含めることはできません。

1. インストール前の概要を確認して、「インストール」をクリックします。インストールプログラムによりインストールの進行状況が表示されます。
1. インストールの概要を確認します。「AEM Forms Workbench を起動」を選択して Workbench を起動し、「次へ」をクリックします。
1. リリースノートを確認して「完了」をクリックします。
1. コンピューターに以下のアイテムがインストールされました。
   * **Workbench**:スタートメニューから Workbench を実行するには、All Programs/AEM Forms/Workbench を選択します（このメニューにショートカットフォルダーを保存する場合）。 詳しくは、 Workbench の使用に関するドキュメントを参照してください。
   * **Designer**:Designer には、Workbench 内からアクセスできます。 詳しくは、Designer ヘルプの「はじめに」を参照してください。
   * **Workbench プラグイン**:6 ページ目の「3.3 Workbench Eclipse 機能のインストール」の手順に従います。
   * **AEM Forms SDK**:SDK の使用について詳しくは、 <a href="http://www.adobe.com/go/learn_lc_programming_10_jp">AEM Formsを使用したプログラミング</a>.

## プロセスのアップグレード {#upgrading-processes}

AEM Forms Update 1 およびLiveCycleES2 プロセスは、アップグレードウィザードを使用してAEM Formsアプリケーションにアップグレードできます。 詳しくは、Workbench ヘルプの既存のアーティファクトのアップグレードに関するドキュメントを参照してください。

### Workbench の Eclipse 機能のインストール {#installing-workbench-eclipse-feature}

オプションで、Workbench 機能を Eclipse に追加できます。 Workbench をインストールした後で、Workbench を追加できます。 例えば、JBoss の場合、次の場所にファイルが格納されます。

* Workbench_DVD/additional/eclipse から Eclipse 3.6 をダウンロードしてインストールする <a href="https://www.eclipse.org/downloads/">www.eclipse.org/downloads</a>.

### Workbench 用の Eclipse 更新機能の設定 {#configuring-eclipse-update-feature-for-workbench}

Workbench では、最新バージョンの Eclipse を使用できる更新機能が用意されています。ただし、各ダウンロードファイルに以下の特定の追加モジュールが含まれていることを確認する必要があります。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Eclipse のバージョン</strong></p> </td> 
   <td><p><strong>Workbench で必要なモジュール</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Eclipse 3.6.x</p> </td> 
   <td><p>

* グラフィック編集フレームワーク GEF [org.eclipse.gef.feature.group]:これは、「グラフィカルモデリングフレームワーク SDK」に含まれています [org.eclipse.gmf.sdk.feature.group]

* WST XML Core [org.eclipse.wst.xml_core.feature.feature.group]:これは「Eclipse XML エディターとツール」に含まれています [org.eclipse.wst.xml_ui.feature.feature.group]

* プラグイン「org.apache.commons.lang_2.3.0」 [該当なし]:これは「Mylyn タスクリスト（必須）」に含まれています [org.eclipse.mylyn_feature.feature.group]

   </p> </td> 
  </tbody>
  </table>

**Workbench 機能をインストールして Eclipse にデプロイするには**:
1. Eclipse を起動します。
1. Help／Install New Software を選択し、「Add」をクリックして Add Repository ダイアログを開きます。
1. Add Repository ダイアログで「Local」をクリックして、Workbench のインストールによってプラグインの ZIP ファイルが保存されたディレクトリを参照し、「workbench-updatesite.zip」を選択してから「Open」をクリックします。
1. 次の画面に表示される手順に従って、Workbench の機能を Eclipse にデプロイします。

   >[!NOTE]
   >
   >「Warning: You are about to install an unsigned feature」メッセージを無視し、「Install」をクリックして続行します。

   >[!NOTE]
   >
   >Flash Builder用のAdobeAEM Forms Discovery プラグインを使用すると、リモートエンドポイントを通じてAEM Formsの一部であるサービスを呼び出すAdobeFlexおよびAIRアプリケーションをすばやく構築できます。 プラグインのインストールと更新の方法に関する情報は、Adobeの Web サイト ( **リンクが必要です**.

### サーバーの設定とログ {#configuring-and-logging-server}

Workbench を使用するには、通常は別のコンピューター上で、AEM Formsのインスタンスが実行されている必要があります。 AEM Formsにログインするには、ユーザー名とパスワード、およびサーバーの場所に関する詳細が必要です。

>[!NOTE]
>
>EMC Documentum またはIBM FileNet リポジトリプロバイダーを使用するようにAEM Formsを設定し、AEM forms 管理コンソールでデフォルトとして設定されたリポジトリ以外のリポジトリにログインする場合は、ユーザー名をusername@Repositoryに指定します。

### タイムアウトの設定 {#configuring-timeout-settings}

デフォルトでは、Workbench は動作状況に関係なく 2 時間後にタイムアウトになります。タイムアウトの設定を編集するには、管理コンソールヘルプの「User Management の設定」の「詳細なシステム属性の設定」を参照してください。

### HTTPS 経由で接続するための Workbench の設定 {#configuring-workbench-to-connect-over-HTTPS}

Workbench を HTTPS 経由でAEM Formsサーバーに接続するには、公開鍵を発行した認証局 (CA) が Workbench によって信頼されていると認識されるようにする必要があります。 証明書が信頼できるソースからのものと認識されない場合は、 [Workbench_HOME]/workbench/jre/lib/security ディレクトリ

>[!NOTE]
>
>[Workbench_HOME] は、Workbench をインストールしたディレクトリを表します。 デフォルトの場所はC:\Program Files (x86)\Adobe Experience Manager forms Workbench です。

HTTPS には、証明書で指定されている名前を使用して接続してください。この名前は通常、完全修飾ホスト名です。

**cacert ファイルを更新するには、以下を実行します。**:
1. Secure Sockets Layer（SSL）証明書のコピーがあることを確認します。SSLサーバーを設定した管理者に問い合わせるか、または Web ブラウザーを使用して証明書を書き出します。

   >[!NOTE]
   >
   >証明書を書き出すには、Web ブラウザーを開いて管理コンソールにログインし、ブラウザーに証明書をインストールしてから、ブラウザーから一時的な保存場所 ( または直接 [Workbench_HOME]/workbench/jre/lib/security ディレクトリ ) に保存されます。

1. 証明書を [Workbench_HOME]/workbench/jre/lib/security ディレクトリ

1. コマンドプロンプトウィンドウを開き、に移動します。 [Workbench_HOME]/workbench/jre/bin に移動し、次のコマンドを入力します。
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`ここで、
   * changeit：cacerts キーストアのデフォルトのパスワードです。
   * certname：手順 1 で選択した証明書です。
   * example：証明書用に選択したエイリアスです。この値は変更できます

1. 証明書を信頼するように求めるプロンプトが表示されたら、「Yes」と入力し、Enter キーを押します。keytool は次に cacerts ファイルをに読み込みます。 [Workbench_HOME]/workbench/jre/lib/security ディレクトリ

1. Workbench を閉じて再起動し、変更を適用します。

### 動的に生成されるテンプレート用のキャッシュ設定の指定 {#configuring-cache-settings-for-dynamically-generated-templates}

アプリケーションで、XFA コンテンツを自動的に更新することによって固有のテンプレートをすばやく生成する場合は、キャッシュ操作の以下の側面を考慮する必要があります。実際には、各トランザクションで新しい固有のテンプレートが使用されています。

Forms Generator または Output が、特定のフォームテンプレートのキャッシュ内のエントリを検索または更新する場合は、以下の複数のキー値を使用して、アクセスする特定のキャッシュエントリを探します。

* **テンプレートファイルの名前**：キャッシュされているフォームの固有のプライマリ識別子として使用される、テンプレートの場所およびファイル名です。
* **タイムスタンプ**：テンプレートファイルには、フォームの最終更新時間の確定に使用するタイムスタンプが含まれています。
* **テンプレートの UUID**：各テンプレートには、Designer により、フォームとそのバージョンに応じて固有の識別子（UUID）が挿入されます。埋め込まれた UUID は、フォームが更新されるびに更新されます。例えば、XDP テンプレートには次の内容が表示されます。

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=http://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="http://www.xfa.org/schema/xfa-template/2.6/">`

* **レンダリングオプション**：キャッシュの内容は、固有のレンダリングオプションのセットごとにレンダリングフォームキャッシュ内に個別に保存されます。


Forms サービスは、ファイル名またはリポジトリの場所を参照するか、メモリ内で XML オブジェクトとしての値を使用することによって、テンプレートを受け取ります。
* **参照によって渡されるテンプレート**：コンテンツルートおよびファイル名を使用します。この方法を使用して、固有のテンプレートが、要求ごとに異なるファイル名で渡されると、ディスクキャッシュは無制限に増えて再利用できなくなります。これを防ぐには、固有のテンプレートは同じファイル名を使用して渡し、すべての要求で同じキャッシュが更新されるようにします。
* **値によって渡されるテンプレート**：theinDataDoc パラメーターを使用して、データと共に渡されるテンプレートのバイトを使用します。この方法を使用して、固有のテンプレートが、異なる UUID を指定して渡されると、ディスクキャッシュは無制限に増えて再利用できなくなります。これを防ぐには、すべてのテンプレートから UUID 属性を削除し、テンプレートのキャッシュが作成されないようにします。または、Null 以外の同一の UUID を渡すと、キャッシュオブジェクトは作成されますがすべての要求で同じキャッシュが更新されるようになります。

キャッシュが無限に増えるのを防ぐには、新しいAEM Forms API を使用して動的に生成されるテンプレート（renderHTMLForm2 および renderPDFForm2）をレンダリングする際に、次の要因を考慮します。

新しい API を使用する場合、テンプレートはドキュメントオブジェクトとして渡され、休止状態になっているかどうかに基づいてFormsサービスで処理されます。

UUID およびコンテンツルートがキャッシュのキーとして機能するパッシブにしたドキュメントの場合は、以下の側面を考慮します。
* UUID が含まれないパッシブにした入力テンプレートに対しては、キャッシュは作成されません。
* UUID とコンテンツルートが同一の、パッシブにした複数の入力テンプレートが渡される場合は、同じキャッシュが上書きされます。

ファイル名およびコンテンツルートがキャッシュのキーとして機能する、パッシブにしていないドキュメントの場合は、以下の側面を考慮します。
* パッシブにしていない入力テンプレートの場合、キャッシュは、ドキュメントの生成元となったコンテンツルートとファイル名に依存します。コンテンツルートとテンプレートのファイル名が同じ要求についてのみ、同じキャッシュが使用されます。動的に生成されたテンプレートが Forms サービスに渡されるとき、以下のベストプラクティスによってにキャッシュが無制限に増えないようになります。
   * UUID を削除するか、動的に生成されたすべてのテンプレートで同一の UUID を渡します。
   * テンプレートのバイト、またはディスク上の同じファイル名からドキュメントを生成します。

### Workbench のアンインストール {#uninstalling-workbench}

アンインストーラーを起動するには、Campaign コントロールパネルの [ プログラムの追加と削除 ] 機能を使用します。 Workbench および Designer アプリケーションには、個別のアンインストールプログラムがあります。

## AEM Forms XDC Editor の設定 {#configuring-aem-forms-xdc-editor}

XDC Editor を使用すると、ネットワークプリンターの管理者は XML Forms Architecture Device Configuration（XDC）ファイルの作成および変更ができます。XDC ファイルには、プリンターの機能が記述されます。例えば、プリンター言語、用紙サイズとトレイ位置との関係付けなどが記述されます。

ネットワークプリンターの管理者が XDC Editor を使用する前に、サンプルの XDC ファイルを配置し直して、『XDC Editor を使用したデバイスプロファイルの作成』を確認してください。

**サンプル XDC ファイルを取得するには**:
1. AEM Formsサーバーで、 [AEM Formsルート]\sdk\samples\Output\IVS.
1. このフォルダーの内容を、Workbench または Eclipse システムからアクセス可能なディレクトリにコピーします。

**XDC Editor のヘルプを入手するには**:
1. AEM Formsのドキュメント Web サイトに移動します。
1. 「開発」タブをクリックし、「XDC Editor を使用したデバイスプロファイルの作成」へ移動します。xdc_editor_help_web.zip ファイルをダウンロードし、「お読みください」ファイル内の手順に従ってヘルプファイルをインストールします。

