---
title: Workbench のインストール
seo-title: Install workbench
description: Workbench をインストールします。
uuid: null
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: author
discoiquuid: null
source-git-commit: 19dcda357b34e7160792d43cb9335fc3be0dedbc
workflow-type: tm+mt
source-wordcount: '2743'
ht-degree: 46%

---


# Workbench のインストール {#install-workbench}

このドキュメントでは、Workbench のインストールと設定の手順を説明します。 このインストールプログラムは Designer もインストールします。

## について {#about}

このドキュメントは、Workbench のインストール、設定、管理またはデプロイを担当する管理者または開発者を対象としています。
アップグレードされたAdobe® AEM forms® Enterprise Suite (ES) Update 1(8.2.x) およびAdobe® AEM forms® Enterprise Suite 2(ES2) プロセスをサポートするようにシステムを設定するために必要な情報も含まれています。
このドキュメントで扱う内容は、Microsoft® Windows® オペレーティングシステムに関する十分な知識がある読者を想定しています。

## 追加情報 {#additional-information}

次の表に、AEM Forms の学習およびこの使用を開始する際に役立つ情報を示します。
<table> 
 <tbody> 
  <tr> 
   <td><p><strong>詳しくは、</strong></p> </td> 
   <td><p><strong>参照先</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Workbench の手順情報</p> </td> 
   <td><p><a href="http://www.adobe.com/go/learn_aemforms_workbench_61_jp">Workbench ヘルプ</a><br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>AEM Forms および AEM Forms を他の Adobe 製品と統合するための方法に関する一般的な情報</p> </td> 
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65_jp">AEM Forms の概要</a><br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>AEM Formsアプリケーションを作成し、Workspace でテストするためのチュートリアル</p> </td> 
   <td><p><a href="http://adobe.com/go/learn_aemforms_firstapp_ds_65">最初のAEM Formsアプリケーションの作成</a><br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>AEM Forms 用のすべてのドキュメント</p> </td> 
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65_jp">AEM Forms のドキュメント</a><br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>AEM Formsと統合するその他のサービスおよび製品</p> </td> 
   <td><p><a href="http://www.adobe.com/jp/">www.adobe.com</a><br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>この製品バージョンに関するパッチアップデート、テクニカルノート、および追加情報</p> </td> 
   <td><p><a href="https://www.adobe.com/jp/account/sign-in.supportportal.html">連絡先Adobeエンタープライズサポート</a><br /> <br /> </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>AEM Forms の Flex Workspace は非推奨（廃止予定）となりました。AEM Forms のリリースで使用できます。

## インストールの準備 {#before-you-install}

### Workbench のインストールの概要 {#workbench-installation-overview}

Workbench は、開発者とフォーム作成者が、自動化されたビジネスプロセスとフォームを作成するために使用する統合開発環境 (IDE) です。 また、プロセスおよびフォームが使用するリソースおよびサービスの管理にも使用されます。

以下の図は、Workbench のインストールを示しています。
* Workbench を使用したプロセスデザイン
* Designer を使用したフォームデザイン

>[!NOTE]
>
>AEM Forms サーバーでは個別のインストールプログラムが必要です。詳しくは、JEE インストールドキュメントで AEM Forms を参照してください。

## システムの前提条件 {#system-prerequisites}

この節では、ハードウェアとソフトウェアの要件およびサポートされているプラットフォームの概要を説明します。

### ハードウェアおよびソフトウェアの最小要件 {#minimum-hardware-software-requirements}

**Workbench**
最小要件を次に示します。
インストール用のディスク容量：
* 680 MB（Workbench のみの場合）.
* 2.15 GB（Workbench 、Designer およびサンプルアセンブリを 1 つのドライブにフルインストールした場合）.
* 一時インストールディレクトリ用に 400 MB（ユーザーの ¥temp ディレクトリに 200 MB、Windows 一時ディレクトリに 200 MB）.

>[!NOTE]
>
>これらの場所がすべて 1 つのドライブ上にある場合は、インストール時に 1.5 GB の空き容量が必要です。一時ディレクトリにコピーされるファイルは、インストールが完了すると削除されます。

* ハードウェア要件： Intel® Pentium® 4 または AMD の同等の 1 GHz プロセッサー.
* （から）最新バージョンのAdobe AIRをダウンロードしてインストールする <a href="http://www.adobe.com/jp/">www.adobe.com</a>) は、Workbench と統合された Community Help Client に必要です。
* Java™ Runtime Environment(JRE)6.0 Update 22 以降の 6.0 への更新 *10 の新機能*.
* 1024 X 768 ピクセル以上のモニター解像度、16 ビットカラー以上.
* AEM Forms サーバーに対する TCP/IPv4 または TCP/IPv6 ネットワーク接続。
* Visual C++ 再頒布可能ランタイムパッケージ 2012 32 ビットをインストールします。
* Visual C++ 再頒布可能ランタイムパッケージ 2013 32 ビットをインストールします。

>[!NOTE]
>
>Adobe® Acrobat® X がコンピューターにインストールされている場合は、Workbench をインストールする前にアンインストールしてください。 Acrobatは、Workbench をインストールした後に再インストールできます。

>[!NOTE]
>
>Workbench をインストールするには、管理者権限が必要です。 管理者以外のアカウントを使用してインストールする場合は、適切なアカウントの資格情報を求めるプロンプトが表示されます。

### サポートされているプラットフォーム {#supported-platforms}

Workbench でサポートされているプラットフォームの完全なリストについては、[AEM Forms でサポートされているプラットフォーム](http://adobe.com/go/learn_aemforms_supportedplatforms_65_jp)を参照してください。

## Designer のインストールに関する考慮事項 {#designer-installation-considerations}

Workbench のインストールには、対応する英語版の Designer がデフォルトで含まれています。 Workbench インストールアプリケーションがコンピューター上で既存バージョンの Designer を検出した場合、インストールが終了することがあります。この場合、続行するには現在のバージョンの Designer を削除する必要があります。次の表に、Workbench をインストールする際に発生する可能性のある Designer のインストールシナリオの完全なリストと、実行する必要のあるアクションを示します。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Designer のバージョンが現在インストールされています</strong></p> </td> 
   <td><p><strong>必要なアクション</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Acrobat ProまたはAcrobat Pro Extended （Designer を含む）</p> </td> 
   <td><p>なし. Workbench のインストールで、Acrobat Pro または Acrobat Pro Extended と共にインストールされた Designer のインスタンスがコンピューター上で検出されます。異なるバージョンの Designer は、同じシステム上で共存できます（例：Designer 8.2.x と 9.0.x）。Acrobat 10 Pro またはAcrobat 10 Pro Extended と共にインストールされている Designer のバージョンをアンインストールする必要はありません。
<br /> <br /> </p> </td> 
  </tr> 
  <tr> 
   <td><p>Designer（スタンドアロン）</p> </td> 
   <td><p>なし. Workbench に付属する Designer のバージョンは英語版のみです。Workbench インストーラーでは、新しいバージョンの Designer は再インストールされません。代わりに、Workbench インストーラーにバンドルされている更新バージョンにパッチが適用されます。 これにより、Workbench 内でローカライズ版の Designer を使用することもできます。<br /> <br /> </p> </td> 
  </tr> 
 </tbody> 
</table>

### Designer（スタンドアロン）をアンインストールするには {#uninstall-designer-standalone}

1. **コントロールパネル／プログラム／プログラムと機能**&#x200B;に移動します。
1. 「現在インストールされているプログラム」リストで、「**Adobe Designer**」を選択します。
1. 「**アンインストール**」をクリックしてから、「**はい**」をクリックします。

### Windows 10 で Designer（スタンドアロン）をアンインストールするには： {#uninstall-designer-standalone-windows10}

1. **コントロールパネル／プログラム／プログラムと機能**&#x200B;に移動します。
1. 「現在インストールされているプログラム」リストで、「**Adobe Designer**」を選択します。
1. 「**アンインストール**」をクリックしてから、「**はい**」をクリックします。

### Acrobat ProまたはAcrobat Pro Extended に付属の Designer をアンインストールするには {#uninstall-designer-included-with-acrobatpro-or-acrobatextended}

1. **コントロールパネル／プログラム／プログラムと機能**&#x200B;に移動します。
1. [ 現在インストールされているプログラム ] の一覧で、 **Adobe Acrobat Pro** または **Adobe Acrobat Pro Extended**.
1. クリック **変更** 次に、 **次へ**.
1. 選択 **変更** 次に、 **次へ**.
1. 選択 **Adobeデザイナ**&#x200B;を選択します。 **この機能は使用できません**&#x200B;をクリックし、 **次へ**
1. クリック **更新** 次に、 **完了**

### Windows 10 でAcrobat ProまたはAcrobat Pro Extended に付属の Designer をアンインストールするには {#uninstall-designer-included-with-acrobatpro-or-acrobatextended-windows10}

1. **コントロールパネル／プログラム／プログラムと機能**&#x200B;に移動します。
1. [ 現在インストールされているプログラム ] の一覧で、 **Adobe Acrobat Pro** または **Adobe Acrobat Pro Extended**.
1. クリック **変更** 次に、 **次へ**.
1. 選択 **変更** 次に、 **次へ**.
1. 選択 **Adobeデザイナ**&#x200B;を選択します。 **この機能は使用できません**&#x200B;をクリックし、 **次へ**
1. クリック **更新** 次に、 **完了**

## Workbench のインストール {#installing-workbench}

この章では、Workbench のインストール方法について説明します。

### Workbench のインストールと実行 {#installing-and-running-workbench}

Workbench をインストールする前に、Workbench の実行に必要なソフトウェアとハードウェアが使用環境に含まれていることを確認してください（**インストールの前に**&#x200B;の節を参照してください）。

**Workbench をインストールして実行するには：**

1. 次のいずれかのタスクを実行します。
   * インストールメディアの\workbench ディレクトリに移動し、 run_windows_installer.bat ファイルをダブルクリックします。
   * Workbench をダウンロードして、ファイルシステムに解凍します。 ダウンロード後、 \workbench ディレクトリに移動し、 run_windows_installer.bat ファイルをダブルクリックします。

   >[!IMPORTANT]
   >
   >Workbench インストーラーは、DVD またはローカルドライブからのみ実行できます。 リモートサイトから実行することはできません。

   >[!NOTE]
   >
   >「Java 仮想マシンを作成できませんでした」というエラーが表示された場合は、_JAVA_OPTIONS という名前の環境変数を -Xmx512M という値で作成し、インストーラーを実行します。

1. はじめに画面で「次へ」をクリックします。
1. 使用許諾契約書を読み、「使用許諾契約書の条件に同意します」を選択して、「次へ」をクリックします。
1. （オプション）フォームを作成および変更するツールが必要な場合は、「Adobe Designer のインストール」を選択します。

   >[!NOTE]
   >
   >Acrobat 10 と共にインストールされた Designer を引き続き使用するには、このオプションの選択を解除したままにします。

1. 表示されるデフォルトのディレクトリをそのまま使用するか、「選択」をクリックして Workbench のインストール先ディレクトリを選択し、「次へ」をクリックします。

   >[!NOTE]
   >
   >インストールディレクトリのパスには、#（ポンド）および $（ドル）文字を含めることはできません。

1. インストール前の概要を確認して、「インストール」をクリックします。インストールの進行状況がインストールプログラムに表示されます。
1. インストールの概要を確認します。 「Adobe AEM forms Workbench の起動」を選択して Workbench を起動し、「次へ」をクリックします。
1. リリースノートを確認して「完了」をクリックします。
1. コンピューターに以下のアイテムがインストールされました。
   * **Workbench**：スタートメニューにショートカットフォルダーを保存するよう選択した場合にこのメニューから Workbench を起動するには、すべてのプログラム／AEM Forms／Workbench を選択します。詳しくは、Workbenchの使用ドキュメントを参照してください。
   * **Designer**：Designer は Workbench 内部からアクセスできます。詳しくは、Designer ヘルプのはじめにのトピックを参照してください。
   * **Workbench プラグイン**:6 ページ目の「3.3 Workbench Eclipse 機能のインストール」の手順に従います。
   * **AEM Forms SDK**：SDK 使用方法の詳細については、<a href="http://www.adobe.com/go/learn_lc_programming_10">AEM Forms によるプログラミング</a>を参照してください。

## プロセスのアップグレード {#upgrading-processes}

AEM Forms Update 1 およびLiveCycleES2 プロセスは、アップグレードウィザードを使用してAEM Formsアプリケーションにアップグレードできます。 詳しくは、Workbench ヘルプの既存のアーティファクトのアップグレードドキュメントを参照してください。

### Workbench Eclipse 機能のインストール {#installing-workbench-eclipse-feature}

オプションで、Workbench 機能を Eclipse に追加できます。 Workbench をインストールした後で、Workbench を追加できます。 例えば、JBoss の場合、次の場所にファイルが格納されます。

* Workbench_DVD/additional/eclipse から Eclipse 3.6 をダウンロードしてインストールする <a href="https://www.eclipse.org/downloads/">www.eclipse.org/downloads</a>.

### Workbench 用の Eclipse 更新機能の設定 {#configuring-eclipse-update-feature-for-workbench}

Workbench では、最新の Eclipse バージョンを使用できるように更新機能がサポートされています。 ただし、各ダウンロードに特定の追加モジュールが含まれていることを確認する必要があります。

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Eclipse バージョン</strong></p> </td> 
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
1. 「ヘルプ」>「新しいソフトウェアのインストール」を選択し、「追加」をクリックして、「リポジトリを追加」ダイアログを開きます。
1. リポジトリを追加ダイアログで、「ローカル」をクリックし、Workbench インストールがプラグインの ZIP ファイルを保存したディレクトリを参照して、「workbench-updatesite.zip」を選択し、「開く」をクリックします。
1. 後続の画面の手順に従って、Workbench 機能を Eclipse にデプロイします。

   >[!NOTE]
   >
   >「警告：署名されていない機能をインストールしようとしています」と表示されたら、[ インストール ] をクリックして続行します。

   >[!NOTE]
   >
   >Flash Builder用のAdobeAEM Forms Discovery プラグインを使用すると、リモートエンドポイントを通じてAEM Formsの一部であるサービスを呼び出すAdobeFlexおよびAIRアプリケーションをすばやく構築できます。 プラグインのインストールと更新の方法に関する情報は、Adobeの Web サイト ( **リンクが必要です**.

### サーバーの設定とログ {#configuring-and-logging-server}

Workbench を使用するには、通常は別のコンピューターで AEM Forms のインスタンスを実行させる必要があります。AEM Forms にログインにするには、ユーザー名とパスワードおよびこのサーバーの場所に関する詳細情報が必要です。

>[!NOTE]
>
>EMC Documentum または IBM FileNet リポジトリプロバイダーを使用するように AEM Forms を設定している場合、AEM Forms 管理コンソール でデフォルトとして設定されている以外のリポジトリにログインするには、ユーザー名を username@Repository と指定します。

### タイムアウトの設定 {#configuring-timeout-settings}

デフォルトでは、Workbench は動作状況に関係なく 2 時間後にタイムアウトになります。タイムアウトの設定を編集するには、管理コンソールヘルプ の「User Management の設定」の「詳細なシステム属性の設定」を参照してください。

### HTTPS 経由で接続するための Workbench の設定 {#configuring-workbench-to-connect-over-HTTPS}

Workbench を HTTPS 経由でAEM Formsサーバーに接続するには、公開鍵を発行した認証局 (CA) が Workbench によって信頼されていると認識されるようにする必要があります。 この証明書が信頼できるソースに由来すると認識されない場合、[Workbench_HOME]/workbench/jre/lib/security ディレクトリにある cacert ファイルを更新する必要があります。

>[!NOTE]
>
>[Workbench_HOME] は、Workbench をインストールしたディレクトリを表します。デフォルトの場所は C:¥Program Files (x86)¥Adobe Experience Manager forms Workbench です。

HTTPS には、証明書で指定されている名前を使用して接続してください。 この名前は通常、完全修飾ホスト名です。

**cacert ファイルを更新するには**：
1. Secure Sockets Layer(SSL) 証明書のコピーがあることを確認します。 SSL サーバーを設定した管理者に問い合わせるか、Web ブラウザーを使用して証明書を書き出します。

   >[!NOTE]
   >
   >証明書を書き出すには、web ブラウザーを開いて管理コンソールにログインし、ブラウザーに証明書をインストールします。次にブラウザーから一時的な保存場所（または直接 [Workbench_HOME]/workbench/jre/lib/security ディレクトリ）に証明書を書き出します。

1. 証明書を [Workbench_HOME]/workbench/jre/lib/security ディレクトリにコピーします。

1. コマンドプロンプトウィンドウを開き、[Workbench_HOME]/workbench/jre/bin に移動して、次のコマンドを入力します。
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`ここで、
   * changeit：cacerts キーストアのデフォルトのパスワードです。
   * certname：手順 1 で選択した証明書です。
   * example：証明書用に選択したエイリアスです。この値は変更できます。

1. 証明書を信頼するように求めるプロンプトが表示されたら、「Yes」と入力し、Enter キーを押します。次に、keytool が cacerts ファイルを [Workbench_HOME]/workbench/jre/lib/securit ディレクトリに読み込みます。

1. Workbench を閉じて再起動し、変更を適用します。

### 動的に生成されるテンプレートのキャッシュ設定の指定 {#configuring-cache-settings-for-dynamically-generated-templates}

XFA コンテンツを自動的に更新して、アプリケーションが一意のテンプレートをその場で生成する場合は、キャッシュ操作の以下の側面を考慮する必要があります。 実際には、各トランザクションは新しい一意のテンプレートを使用します。

Forms Generator または Output が特定のフォームテンプレートのキャッシュ内のエントリを検索または更新する場合、複数のキー値を使用して、アクセスする特定のキャッシュエントリを検索します。

* **テンプレートファイル名**:キャッシュされたフォームの一意のプライマリ識別子として使用されるテンプレートの場所とファイル名。
* **タイムスタンプ**:テンプレートファイルには、フォームの最終更新時刻の決定に使用されるタイムスタンプが含まれます。
* **テンプレート UUID**:Designer は、各テンプレートに、フォームとそのバージョンに固有の識別子 (UUID) を挿入します。 埋め込まれた UUID は、フォームが更新されるたびに更新されます。 例えば、XDP テンプレートには次のコンテンツが表示されます。

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=http://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="http://www.xfa.org/schema/xfa-template/2.6/">`

* **レンダリングオプション**:レンダリングされたフォームキャッシュ内で、キャッシュの内容は、一意のレンダリングオプションのセットごとに別々に保存されます。


Formsサービスは、ファイル名またはリポジトリの場所を参照するか、メモリ内の XML オブジェクトとして値を使用して、テンプレートを受け取ります。
* **参照によって渡されるテンプレート**:コンテンツルートとフォーム名を使用します。 この方法を使用して、リクエストごとに異なるファイル名を持つ一意のテンプレートが渡される場合、ディスクキャッシュは無限に増え、再利用されません。 これを防ぐには、一意のテンプレートを同じファイル名で渡して、すべてのリクエストで同じキャッシュが更新されるようにする必要があります。
* **値によって渡されるテンプレート**:theinDataDoc パラメーターを使用して、データと共に渡されるテンプレートのバイトを使用します。 この方法を使用して、異なる UUID を持つ一意のテンプレートを渡すと、ディスクキャッシュは無限に増え、再利用されなくなります。 これを防ぐには、テンプレートのキャッシュが作成されないように、すべてのテンプレートから UUID 属性を削除する必要があります。 また、同じ null 以外の UUID を渡すと、キャッシュオブジェクトを作成できますが、リクエストのたびに同じキャッシュが更新されます。

キャッシュが無制限に増えないようにするために、新しい AEM Forms API（renderHTMLForm2 および renderPDFForm2）を使用して動的に生成されるテンプレートのレンダリングについて、次の要因を考慮します。

新しい API を使用する場合、テンプレートはドキュメントオブジェクトとして渡され、パッシブにするかしないかに基づいて Forms サービス内で処理されます。

UUID およびコンテンツルートがキャッシュキーとして機能するパッシブにしたドキュメントの場合は、以下の側面を考慮してください。
* UUID のないパッシブにした入力テンプレートに対しては、キャッシュは作成されません。
* 同じ UUID とコンテンツルートを持つ、パッシブにした複数の入力テンプレートが渡された場合、同じキャッシュが上書きされます。

ファイル名とコンテンツルートがキャッシュキーとして機能する、パッシブにしないドキュメントの場合は、次の側面を考慮してください。
* パッシブにしていない入力テンプレートの場合、キャッシュは、ドキュメントの生成元となったコンテンツルートとファイル名に依存します。コンテンツルートとテンプレートのファイル名が同じ要求についてのみ、同じキャッシュが使用されます。次のベストプラクティスは、動的に生成されたテンプレートがFormsサービスに渡される際に、キャッシュが無限に増えないようにするためのものです。
   * 動的に生成されるすべてのテンプレートで、UUID を取り除くか、同じ UUID を渡します。
   * テンプレートのバイトまたはディスク上の同じファイル名からドキュメントを生成します。

### Workbench のアンインストール {#uninstalling-workbench}

コントロールパネルのプログラムの追加と削除機能を使用して、アンインストーラーを起動します。Workbench および Designer アプリケーションには、個別のアンインストールプログラムがあります。

## AEM Forms XDC Editor の設定 {#configuring-aem-forms-xdc-editor}

XDC Editor を使用すると、ネットワークプリンター管理者は、XML Forms Architecture Device Configuration(XDC) ファイルの作成と変更をおこなうことができます。 XDC ファイルは、プリンターの機能を記述したものです。例えば、プリンターの言語や、用紙サイズとトレイの位置との関係などを記述したものです。

ネットワークプリンターの管理者が XDC Editor を使用する前に、サンプルの XDC ファイルを配置し直して、『XDC Editor を使用したデバイスプロファイルの作成』を確認してください。

**サンプルの XDC ファイルを入手するには**：
1. AEM Forms サーバーで、[AEM Forms root]\sdk\samples\Output\IVS から XDC フォルダーを探します。
1. このフォルダーの内容を、Workbench または Eclipse システムからアクセス可能なディレクトリにコピーします。

**XDC Editor のヘルプを入手するには**：
1. AEM Forms ドキュメントの web サイトへ移動します。
1. 「開発」タブをクリックし、「XDC Editor を使用したデバイスプロファイルの作成」へ移動します。xdc_editor_help_web.zip ファイルをダウンロードし、「お読みください」ファイル内の手順に従ってヘルプファイルをインストールします。

