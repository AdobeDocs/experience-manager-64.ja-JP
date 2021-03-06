---
title: JEE 上の AEM Forms 環境の堅牢化
seo-title: Hardening Your AEM Forms on JEE Environment
description: 企業のイントラネット内で動作する JEE 上のAEM Formsのセキュリティを強化するための、様々なセキュリティ強化設定について説明します。
seo-description: Learn a variety of security-hardening settings to enhance the security of AEM Forms on JEE running in a corporate intranet.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
role: Admin
exl-id: 5aa02fae-b9dd-45bf-9826-16e9e5686727
source-git-commit: e608249c3f95f44fdc14b100910fa11ffff5ee32
workflow-type: tm+mt
source-wordcount: '7304'
ht-degree: 73%

---

# JEE 上の AEM Forms 環境の堅牢化 {#hardening-your-aem-forms-on-jee-environment}

企業のイントラネット内で動作する JEE 上のAEM Formsのセキュリティを強化するための、様々なセキュリティ強化設定について説明します。

この記事では、JEE 上の AEM Forms を実行するサーバーを保護するための推奨事項とベストプラクティスについて説明します。ここでは、オペレーティングシステムとアプリケーションサーバーのホストの堅牢化について包括的な説明はしません。この記事では、企業のイントラネット内で実行されている JEE 上のAEM Formsのセキュリティを強化するために実装する必要がある、様々なセキュリティ強化設定について説明します。 なお、JEE 上の AEM Forms アプリケーションサーバーのセキュリティを確実に保つには、これだけでなく、セキュリティの監視、検出および応答の方策を実装することも必要です。

この記事では、インストールと設定の作業において、次の各段階で適用する堅牢化手法について説明します。

* **インストール前：**&#x200B;この手法は、JEE 上の AEM Forms をインストールする前に実行します。
* **インストール：** この方法は、JEE 上のAEM Formsのインストールプロセスで使用します。
* **インストール後：**&#x200B;この手法は、インストール終了後と、それ以降の定期的な管理作業として実行します。

JEE 上の AEM Forms は詳細なカスタマイズが可能で、様々な環境で動作します。推奨事項には、一部の組織のニーズに合わないものも含まれている可能性があります。

## インストール前 {#preinstallation}

JEE 上の AEM Forms をインストールする前には、ネットワーク層とオペレーティングシステムに対してセキュリティソリューションを適用することができます。ここでは、いくつかの問題と、この領域におけるセキュリティの脆弱性を減らすための推奨事項について説明します。

**UNIX および Linux へのインストールと設定**

JEE 上の AEM Forms のインストール作業や設定作業を実行するときは、ルートシェルを使用しないでください。デフォルトでは、ファイルは /opt ディレクトリの下にインストールされるので、インストールを実行するユーザーには /opt 以下のすべてのファイルの権限が必要です。または、各ユーザーには /user ディレクトリに対するすべてのファイル権限があらかじめ付与されているので、/user ディレクトリにインストールを実行することもできます。

**Windows へのインストールと設定**

自動オプションインストールを使用して JBoss に JEE 上の AEM Forms をインストールする場合、または PDF Generator をインストールする場合、Windows へのインストールは管理者として実行する必要があります。また、PDF Generator をネイティブアプリケーションサポートと共に Windows にインストールする場合は、Microsoft Office をインストールしたのと同じ Windows ユーザーとしてインストールを実行する必要があります。インストールの権限について詳しくは、使用しているアプリケーションサーバー版の「JEE 上のAEM Formsのインストールとデプロイ」ドキュメントを参照してください。

### ネットワーク層のセキュリティ {#network-layer-security}

ネットワークセキュリティの脆弱性は、インターネットまたはイントラネットに接続しているすべてのアプリケーションサーバーにとって、最も重大な脅威の 1 つです。ここでは、このような脆弱性に対してネットワーク上のホストを堅牢化する手順について説明します。具体的には、ネットワークのセグメント化、TCP/IP（Transmission Control Protocol/Internet Protocol）スタックの堅牢化、ホスト保護のためのファイアウォールの使用などの手順を取り上げます。

次の表では、ネットワークセキュリティの脆弱性を減らすための一般的なプロセスについて説明します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>説明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>非武装地帯（DMZ）</p> </td> 
   <td><p>forms サーバーを非武装地帯（DMZ）にデプロイします。ファイアウォールの内側に配置された、JEE 上の AEM Forms を実行するアプリケーションサーバーに対して、少なくとも 2 つのレベルでセグメント化が必要です。Web サーバーを含む DMZ から外部ネットワークを分離します。同様に、外部ネットワークは内部ネットワークからも分離している必要があります。ファイアウォールを使用して、この分離した層を実装します。必要最小限のデータのみが許可されるように、各ネットワーク層を通過するトラフィックを分類して制御します。</p> </td> 
  </tr> 
  <tr> 
   <td><p>プライベート IP アドレス</p> </td> 
   <td><p>AEM Formsアプリケーションサーバー上の RFC 1918 プライベート IP アドレスで、Network Address Translation(NAT) を使用します。非公開 IP アドレス (10.0.0.0/8、172.16.0.0/12、192.168.0.0/16) を割り当てて、攻撃者がインターネットを介して NAT の内部ホストとの間でトラフィックをルーティングするのをより難しくします。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ファイアウォール</p> </td> 
   <td><p>次の基準を使用して、ファイアウォールソリューションを選択します。</p> 
    <ul> 
     <li><p>単純なパケットフィルタリングソリューションではなく、プロキシサーバーまたは「ステートフルインスペクション」<em></em>をサポートするファイアウォールを実装する。</p> </li> 
     <li><p>をサポートするファイアウォールを使用する <em>明示的に許可されたもの以外のすべてのサービスを拒否する</em> セキュリティ枠組み</p> </li> 
     <li><p>デュアルホームまたはマルチホームのファイアウォールソリューションを実装する。このアーキテクチャによって、最も高いセキュリティレベルが実現し、権限のないユーザーがファイアウォールセキュリティを迂回できないようにすることができます。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>データベースポート</p> </td> 
   <td><p>データベースのデフォルトのリスニングポート（MySQL - 3306、Oracle - 1521、MS SQL - 1433）は、使用しないでください。データベースポートの変更について詳しくは、データベースのドキュメントを参照してください。</p> <p>データベースポートを変更すると、JEE 上の AEM Forms の設定全体に影響します。デフォルトポートを変更した場合、JEE 上の AEM Forms のデータソースなど、設定の別の領域を変更内容に合わせて修正する必要があります。</p> <p>JEE 上のAEM Formsでのデータソースの設定について詳しくは、「 JEE 上のAEM Formsのインストールとアップグレード」または「使用しているアプリケーションサーバー用の JEE 上のAEM Formsへのアップグレード」( ) を参照してください。 <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Formsユーザーガイド</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### オペレーティングシステムのセキュリティ {#operating-system-security}

次の表では、オペレーティングシステムに存在するセキュリティの脆弱性を最小にするために役立つ方法について説明します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p></th> 
   <th><p>説明</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>セキュリティパッチ</p></td> 
   <td><p>ベンダーのセキュリティパッチとアップデートが迅速に適用されない場合、権限のないユーザーがアプリケーションサーバーにアクセスするリスクが高まります。実稼働サーバーにセキュリティパッチを適用する場合は、適用する前にテストしてください。</p><p>さらに、パッチを定期的にチェックしてインストールするためのポリシーとプロシージャを作成してください。</p></td> 
  </tr> 
  <tr> 
   <td><p>ウイルス対策ソフトウェア</p></td> 
   <td><p>ウイルススキャンプログラムは、署名をスキャンするか、異常な動作を監視することによって、感染ファイルを識別します。スキャンプログラムでは、ウイルスの署名をファイルに保管します。通常、このファイルはローカルハードドライブに格納されます。新しいウイルスは次から次へと出現するので、ウイルススキャンプログラムですべての最新のウイルスを識別できるように、このファイルを頻繁に更新する必要があります。</p></td> 
  </tr> 
  <tr> 
   <td><p>ネットワークタイムプロトコル（NTP）</p></td> 
   <td><p>フォレンジック分析のために、forms サーバーの時計は常に正確に設定されている必要があります。NTP を使用して、インターネットに直接接続しているすべてのシステムの時間を同期させてください。</p></td> 
  </tr> 
 </tbody> 
</table>

お使いのオペレーティングシステムのセキュリティ情報について詳しくは、 [オペレーティング・システムのセキュリティ情報](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## インストール {#installation}

ここでは、AEM Forms インストールプロセスで、セキュリティの脆弱性を減らすために使用できる方法について説明します。これらの方法では、状況によってはインストールプロセスのオプションを使用します。次の表では、各方法について解説します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>説明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>権限</p> </td> 
   <td><p>ソフトウェアのインストールに必要な権限の数を最小限にします。 Administrators グループに属していないアカウントでコンピューターにログインします。Windows では、runas コマンドを使用して、管理者ユーザーとして JEE 上の AEM Forms インストーラーを実行することができます。UNIX および Linux システムでは、<code>sudo</code> などのコマンドを使用してソフトウェアをインストールします。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ソフトウェアソース</p> </td> 
   <td><p>信頼できないソースから JEE 上の AEM Forms をダウンロードまたは実行しないでください。</p> <p>悪意のあるプログラムには、データの盗難、改変、削除、サービス拒否などの様々な手段でセキュリティを侵害するコードが含まれています。必ず、Adobe DVD または信頼できるソースから入手した JEE 上の AEM Forms をインストールしてください。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ディスクのパーティション</p> </td> 
   <td><p>JEE 上の AEM Forms は、専用のディスクパーティションに配置してください。ディスクのセグメント化とは、セキュリティを強化するために、サーバー上の特定のデータを個別の物理ディスクに保管するプロセスのことです。この方法でデータを整理すると、ディレクトリトラバーサル攻撃のリスクを軽減することができます。システムパーティションとは別に、JEE 上の AEM Forms コンテンツディレクトリをインストールするパーティションを作成することを検討してください。（Windows のシステムパーティションには system32 ディレクトリまたはブートパーティションが含まれています）。</p> </td> 
  </tr> 
  <tr> 
   <td><p>コンポーネント</p> </td> 
   <td><p>既存のサービスを評価し、不要なサービスを無効化またはアンインストールしてください。不要なコンポーネントやサービスをインストールしないでください。</p> <p>アプリケーションサーバーのデフォルトインストールには、サーバーの用途によっては必要のないサービスが含まれている可能性があります。攻撃のエントリポイントを最小限に抑えるために、デプロイメントに先立って、不要なサービスをすべて無効にする必要があります。例えば、JBoss では、META-INF/jboss-service.xml 記述子ファイル内の不要なサービスをコメントアウトします。</p> </td> 
  </tr> 
  <tr> 
   <td><p>クロスドメインポリシーファイル</p> </td> 
   <td><p>サーバー上に <code>crossdomain.xml</code> ファイルが存在すると、そのサーバーを直ちに弱化させる可能性があります。ドメインのリストに可能な限り制限をかけることをお勧めします。ガイド<code>crossdomain.xml</code>（非推奨）<em>を使用する場合、開発環境から実稼働環境への移行中に使用される </em> ファイルを配置しないでください。Web サービスで使用されるガイドの場合、ガイドを提供するサーバーと同じサーバー上にそのサービスがあれば、<code>crossdomain.xml</code> ファイルはまったく必要ありません。しかし、サービスが別のサーバー上にある場合や、クラスターが関係している場合は、<code>crossdomain.xml</code> ファイルが存在している必要があります。参照： <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>crossdomain.xml ファイルについて詳しくは、を参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td><p>オペレーティングシステムのセキュリティ設定</p> </td> 
   <td><p>192 ビットまたは 256 ビットの XML 暗号化を Solaris プラットフォームで使用する必要がある場合は、必ず <code>pkcs11_softtoken_extra.so</code> の代わりに <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## インストール後の手順 {#post-installation-steps}

JEE 上の AEM Forms のインストールが完了したら、セキュリティ上の観点から、定期的に環境の保守を行うことが重要です。

次の節では、デプロイ済みの Forms サーバーを保護するための、各種の推奨タスクについて詳細に説明します。

### AEM Forms のセキュリティ {#aem-forms-security}

次の推奨設定は、管理 Web アプリケーションの外にある JEE 上の AEM Forms サーバーに適用されます。サーバーのセキュリティリスクを軽減するには、この設定を JEE 上の AEM Forms のインストール直後に適用してください。

**セキュリティパッチ**

ベンダーのセキュリティパッチとアップデートが迅速に適用されない場合、権限のないユーザーがアプリケーションサーバーにアクセスするリスクが高まります。実稼働サーバーにセキュリティパッチを適用する場合は、事前にテストを実施し、 アプリケーションの互換性と可用性を確認した上で適用してください。また、パッチのチェックとインストールを定期的に行うためのポリシーと手続きを定めてください。JEE 上の AEM Forms のアップデートは Enterprise 製品のダウンロードサイトにあります。

**サービスアカウント（Windows への JBoss 自動インストールのみ）**

JEE 上の AEM Forms は、デフォルトでは、LocalSystem アカウントを使用してサービスをインストールします。組み込み LocalSystem ユーザーアカウントは、高いレベルのアクセス権限を付与されており、Administrators グループに属しています。ワーカープロセス ID を LocalSystem ユーザーアカウントで実行した場合、そのワーカープロセスはシステム全体に対してフルアクセス権限を持ちます。

JEE 上の AEM Forms のデプロイ先のアプリケーションサーバーを実行するには、次の手順に従って、管理者以外の固有のアカウントを使用してください。

1. Microsoft 管理コンソール（MMC）で、forms サーバーサービスへのログインに使用するローカルユーザーを作成します。

   * 「**ユーザーはパスワードを変更できない**」オプションを選択します。
   * 「**所属するグループ**」タブに、「**ユーザー**」グループが表示されていることを確認してください。

   >[!NOTE]
   >
   >PDF Generator 用のこの設定は変更できません。

1. **スタート**／**設定**／**管理ツール**／**サービス**&#x200B;を選択します。
1. JEE 上の AEM Forms 向けの JBoss をダブルクリックして、サービスを停止します。
1. 「**ログオン**」タブで、「**アカウント**」を選択し、作成したユーザーアカウントを参照して、アカウントのパスワードを入力します。
1. MMC で、「**ローカルセキュリティ設定**」を開き、**ローカルポリシー**／**ユーザー権利の割り当て**&#x200B;を選択します。
1. forms サーバーを実行しているユーザーアカウントに、次の権限を割り当てます。

   * ターミナルサービスを使ったログオンを拒否する
   * ローカルでログオンを拒否する
   * サービスとしてログオン（通常は既に設定済み）

1. 新しく作成したユーザーアカウントに、JEE 上の AEM Forms Web コンテンツディレクトリの項目に対する「読み取りと実行」、「フォルダーの内容の一覧表示」、「読み取り」の各権限を付与します。
1. アプリケーションサーバーを起動します。

**Configuration Manager ブートストラップサーブレットの無効化**

Configuration Manager は、アプリケーションサーバーにデプロイ済みのサーブレットを利用して、JEE 上の AEM Forms データベースのブートストラップを実行します。Configuration Manager は、設定が完了する前にこのサーブレットにアクセスするので、承認済みユーザーのみにアクセスを限定するセキュリティは施されていません。Configuration Manager を使用して JEE 上の AEM Forms の設定を完了した後は、このサーブレットを無効にしてください。

1. adobe-livecycle — を解凍します。[appserver].ear ファイル。
1. META-INF/application.xml ファイルを開きます。
1. adobe-bootstrapper.war セクションを検索します。

   ```as3
   <!-- bootstrapper start --> 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   <!-- bootstrapper end-->
   ```

1. AEM Forms Server を停止します。
1. adobe-bootstrapper.war および adobe-lcm-bootstrapper-redirectory. war モジュールを次のようにコメントアウトします。

   ```as3
   <!-- bootstrapper start --> 
   <!-- 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   --> 
   <!-- bootstrapper end-->
   ```

1. META-INF/application.xml ファイルを保存して閉じます。
1. EAR ファイルの zip ファイルを作成し、アプリケーションサーバーに再デプロイします。
1. AEM Forms サーバーを開始します。
1. 以下の URL をブラウザーに入力して、変更をテストし、機能しなくなることを確認します。

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Trust Store へのリモートアクセスのロックダウン**

Configuration Manager を使用して、Acrobat Reader DC Extensions の資格情報を JEE 上の AEM Forms Trust Store にアップロードできます。つまり、リモートプロトコル（SOAP および EJB）経由の Trust Store 資格情報サービスへのアクセスは、デフォルトで有効になっています。Configuration Manager を使用して権限秘密鍵証明書をアップロードした後、または後で管理コンソールを使用して資格情報を管理する場合は、このアクセスは不要になりました。

[サービスへの不要なリモートアクセスの無効化](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services)の手順に従って、Trust Store の全サービスへのリモートアクセスを無効にすることができます。

**すべての不要な匿名アクセスの無効化**

一部の forms サーバーサービスには、匿名の呼び出しによって実行される操作があります。このようなサービスへの匿名アクセスが必要ない場合は、[サービスへの不要な匿名アクセスの無効化](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services)の手順に従って、アクセスを無効にしてください。

#### デフォルトの管理者パスワードの変更 {#change-the-default-administrator-password}

JEE 上の AEM Forms をインストールすると、上級管理者ユーザーまたはログイン ID 管理者ユーザーのために、デフォルトパスワードが「*password*」であるデフォルトユーザーアカウントが 1 つ設定されます。このパスワードは、Configuration Manager を使用して直ちに変更してください。

1. Web ブラウザーに次の URL を入力します。

   ```as3
   https://[host name]:[port]/adminui
   ```

   デフォルトのポート番号は次のいずれかです。

   **JBoss：** 8080

   **WebLogic Server：** 7001

   **WebSphere：** 9080

1. 「**ユーザー名**」フィールドに `administrator` と入力し、「**パスワード**」フィールドに `password` と入力します。
1. **設定**／**User Management**／**ユーザーとグループ**&#x200B;をクリックします。
1. 「`administrator`検索&#x200B;**」フィールドに** と入力し、「**検索**」をクリックします。
1. ユーザーの一覧で「**上級管理者**」 をクリックします。
1. ユーザーを編集ページで「**パスワードの変更**」をクリックします。
1. 新しいパスワードを指定し、「**保存**」をクリックします。

次の手順を実行することで CRX 管理者のデフォルトパスワードの変更もお勧めします。

1. ログイン `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` デフォルトのユーザー名/パスワードを使用します。
1. 検索フィールドに「管理者」と入力し、「**移動**」をクリックします。
1. 選択 **管理者** 検索結果で、 **編集** アイコンが表示されます。
1. 「**新しいパスワード**」フィールドに新しいパスワードを、「**パスワード**」フィールドに古いパスワードを指定します。
1. ユーザーインターフェイスの右下にある保存アイコンをクリックします。

#### WSDL の生成の無効化 {#disable-wsdl-generation}

Web Service Definition Language（WSDL）の生成は、開発者が WSDL の生成を使用してクライアントアプリケーションを構築する開発環境でのみ有効にしてください。実稼働環境では WSDL の生成を無効化して、サービスの内部詳細が公開されないようにすることができます。

1. Web ブラウザーに次の URL を入力します。

   ```as3
   https://[host name]:[port]/adminui
   ```

1. **設定／コアシステム設定／設定**&#x200B;をクリックします。
1. 選択を解除 **WSDL を有効にする** をクリックし、 **OK**.

### アプリケーションサーバーのセキュリティ {#application-server-security}

次の表では、JEE 上の AEM Forms アプリケーションのインストール後に、アプリケーションサーバーを保護するために使用するいくつかの方法について説明します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>説明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>アプリケーションサーバーの管理コンソール</p> </td> 
   <td><p>アプリケーションサーバーで JEE 上の AEM Forms のインストール、設定およびデプロイを完了したら、アプリケーションサーバーの管理コンソールへのアクセスを無効にする必要があります。詳しくは、アプリケーションサーバーのドキュメントを参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td><p>アプリケーションサーバーの cookie の設定</p> </td> 
   <td><p>アプリケーションの cookie は、アプリケーションサーバーが管理しています。アプリケーションをデプロイするときに、アプリケーションサーバーの管理者は cookie の環境設定をサーバー全体に対してまたは個別のアプリケーションに対して指定することができます。デフォルトでは、サーバーの設定が優先します。</p> <p>アプリケーションサーバーで生成されるすべてのセッション cookie に <code>HttpOnly</code> 属性が含まれている必要があります。例えば、JBoss Application Server を使用している場合、SessionCookie 要素を <code>httpOnly="true"</code> 内 <code>WEB-INF/web.xml</code> ファイル。</p> <p>cookie の送信には HTTPS のみを使用するように制限することもできます。このように設定すると、cookie が HTTP を経由して暗号化されずに送信されることはありません。アプリケーションサーバーの管理者は、サーバーの cookie 保護をグローバルに有効化する必要があります。例えば、JBoss アプリケーションサーバーを使用する場合、<code>secure=true</code> ファイルで、<code>server.xml</code> へのコネクタ要素を修正することができます。</p> <p>cookie の設定について詳しくは、アプリケーションサーバーのドキュメントを参照してください。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ディレクトリの参照</p> </td> 
   <td><p>存在しないページに対する要求、またはディレクトリ名に対する要求（最後がスラッシュ（/）で終わる要求文字列）が行われた場合、アプリケーションサーバーによってディレクトリの内容が返されないようにする必要があります。これが行われないようにするには、アプリケーションサーバーのディレクトリ参照を無効にします。管理コンソールアプリケーションおよびサーバーで実行している他のアプリケーションについても、ディレクトリ参照を無効にしてください。</p> <p>JBoss の場合、web.xml ファイルの <code>DefaultServlet</code> プロパティの初期化パラメーターの listings 値を <code>false</code> に設定します。次に例を示します。</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listings&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>WebSphere の場合、ibm-web-ext.xmi ファイルの <code>directoryBrowsingEnabled</code> プロパティを <code>false</code> に設定します。</p> <p>WebLogic の場合、weblogic.xml ファイルの index-directories プロパティを <code>false</code> に設定します。次に例を示します。</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### データベースのセキュリティ {#database-security}

データベースの保護を行う場合、データベースのベンダーが挙げている対策を実装することを慎重に検討してください。データベースのユーザーには、JEE 上の AEM Forms でデータベースを使用するために必要な最小限の権限を付与するようにします。例えば、データベースの管理権限を持つアカウントは使用しないでください。

Oracle では、データベースアカウントで使用する必要がある権限は、CONNECT、RESOURCE および CREATE VIEW だけです。他のデータベースについての同様の要件については、「[JEE 上の AEM Forms のインストールの準備（シングルサーバー）](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64)」を参照してください。

#### Windows 上での統合セキュリティの設定（JBoss 版） {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 変更 [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} を追加 `integratedSecurity=true` を接続 URL に追加します。

   ```as3
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. アプリケーションサーバーを実行しているコンピューターの Windows システムパスに sqljdbc_auth.dll ファイルを追加します。sqljdbc_auth.dll ファイルは、Microsoft SQL JDBC 6.2.1.0 ドライバーのインストールフォルダー内にあります。
1. JBoss Windows サービス（JBoss for JEE 上の AEM Forms）のログオンプロパティを、ローカルシステムから、JEE 上の AEM Forms データベースと最低限の権限を持つログインアカウントに変更します。Windows サービスとしてではなく、コマンドラインから JBoss を実行している場合、この手順を行う必要はありません。
1. SQL Server のセキュリティを「**混合**」モードから「**Windows 認証のみ**」に変更します。

#### Windows 上での統合セキュリティの設定（WebLogic 版） {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Web ブラウザーの URL 行に次の URL を入力して、WebLogic Server 管理コンソールを起動します。

   ```as3
   https://[host name]:7001/console
   ```

1. Change Center で、「**Lock &amp; Edit**」をクリックします。
1. 「ドメイン構造」で、 *[base_domain]* > **サービス** > **JDBC** > **データソース** 右側のウィンドウで、 **IDP_DS**.
1. 次の画面の「**Configuration**」タブで「**Connection Pool**」タブをクリックし、「**Properties**」ボックスに `integratedSecurity=true` と入力します。
1. 「ドメイン構造」で、 **[base_domain]** > **サービス** > **JDBC** > **データソース** 右側のウィンドウで、 **RM_DS**.
1. 次の画面の「**Configuration**」タブで「**Connection Pool**」タブをクリックし、「**Properties**」ボックスに `integratedSecurity=true` と入力します。
1. アプリケーションサーバーを実行しているコンピューターの Windows システムパスに sqljdbc_auth.dll ファイルを追加します。sqljdbc_auth.dll ファイルは、Microsoft SQL JDBC 6.2.1.0 ドライバーのインストールフォルダー内にあります。
1. SQL Server のセキュリティを「**混合**」モードから「**Windows 認証のみ**」に変更します。

#### Windows 上での統合セキュリティの設定（WebSphere 版） {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

WebSphere では、統合セキュリティを設定できるのは外部の SQL Server JDBC ドライバーを使用している場合のみです。WebSphere の埋め込みの SQL Server JDBC ドライバーを使用している場合は設定できません。

1. WebSphere Administrative Console にログインします。
1. ナビゲーションツリーで、**Resources**／**JDBC**／**Data Sources** をクリックし、右側のウィンドウで「**IDP_DS**」をクリックします。
1. 右側のウィンドウの「Additional Properties」で「**Custom Properties**」をクリックし、「**New**」をクリックします。
1. 内 **名前** ボックス、タイプ `integratedSecurity` そして、 **値** ボックス、タイプ `true`.
1. ナビゲーションツリーで、**Resources**／**JDBC**／**Data Sources** をクリックし、右側のウィンドウで「**RM_DS**」をクリックします。
1. 右側のウィンドウの「Additional Properties」で「**Custom Properties**」をクリックし、「**New**」をクリックします。
1. 内 **名前** ボックス、タイプ `integratedSecurity` そして、 **値** ボックス、タイプ `true`.
1. WebSphere がインストールされているコンピューター上で、Windows システムパス（C:¥Windows）に sqljdbc_auth.dll ファイルを追加します。sqljdbc_auth.dll ファイルは、Microsoft SQL JDBC 1.2 ドライバーのインストール先と同じ場所にあります ( デフォルトは *[InstallDir]*/sqljdbc_1.2/enu/auth/x86) を参照してください。
1. **スタート**／**コントロールパネル**／**サービス**&#x200B;を選択し、WebSphere の Windows サービス（IBM WebSphere Application Server &lt;version> - &lt;node>）を右クリックして、「**プロパティ**」を選択します。
1. プロパティダイアログボックスで、「**ログオン**」タブをクリックします。
1. 「**アカウント**」を選択し、必要な情報を入力して、使用するログインアカウントを設定します。
1. SQL Server のセキュリティを「**混合**」モードから「**Windows 認証のみ**」に変更します。

### データベース内の機密性の高い情報の保護 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms データベーススキーマには、システム設定やビジネスプロセスに関する機密性の高い情報が含まれているので、ファイアウォールの内側に隠しておく必要があります。データベースは、forms サーバーと同じ信頼境界内にあると見なされる必要があります。情報の意図しない開示やビジネスデータの盗難を防ぐために、データベース管理者（DBA）は、権限のある管理者のみにアクセスを制限するようにデータベースを設定する必要があります。

追加の予防策として、データベースベンダー固有のツールを使用して、次のデータを含むテーブルの列を暗号化することを考慮してください。

* Rights Management ドキュメントキー
* Trust Store HSM PIN 暗号化キー
* ローカルユーザーパスワードハッシュ

ベンダー固有のツールについて詳しくは、 [データベースのセキュリティ情報](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### LDAP のセキュリティ {#ldap-security}

LDAP（Lightweight Directory Access Protocol）ディレクトリは、通常、エンタープライズユーザーおよびグループ情報のソースとして、またパスワード認証実行の手段として JEE 上の AEM Forms で使用されます。LDAP ディレクトリが SSL（Secure Socket Layer）を使用するように設定されていること、および JEE 上の AEM Forms が SSL ポートを使用して LDAP ディレクトリにアクセスするように設定されていることを確認してください。

#### LDAP のサービス拒否 {#ldap-denial-of-service}

LDAP を使用した最もよく行われる攻撃は、攻撃者が大量の認証エラーを故意に引き起こすというものです。この攻撃を受けると、LDAP ディレクトリサーバーは、すべての LDAP 依存のサービスからユーザーをロックアウトしなければならなくなります。

試行できる認証エラーの回数と、それに伴うロックアウト時間の値を設定すると、AEM Forms への認証でユーザーが繰り返しエラーになったときに、AEM Forms がロックアウトを実行します。管理コンソールで、小さい値を選択します。 認証エラーの許容回数を選択するときは、許容回数に達した後に、LDAP ディレクトリサーバーより前に AEM Forms がユーザーをロックアウトすることを理解することが重要です。

#### 自動アカウントロックの設定 {#set-automatic-account-locking}

1. 管理コンソールにログインします。
1. **設定**／**ユーザー管理**／**ドメイン管理**&#x200B;をクリックします。
1. 「自動アカウントロックの設定」で、「**連続する認証エラーの最大回数**」を 3 などの小さい値に設定します。
1. 「**保存**」をクリックします。

### 監査とログ {#auditing-and-logging}

アプリケーションの監査およびログ機能を適切に保護した状態で使用することで、セキュリティを確保し、他の異常なイベントを追跡して、それらのイベントを可能な限り迅速に検出することができます。アプリケーション内における監査とログの効果的な使用には、成功したログインと失敗したログインの追跡、キーレコードの作成と削除などのキーアプリケーションイベントの追跡などが挙げられます。

監査を使用して、各種の攻撃を検出することができます。具体的には、以下のものがあります。

* ブルートフォースパスワードアタック
* サービス拒否攻撃
* 敵意のある入力値と関連するクラスのスクリプト挿入攻撃

次の表では、サーバーの脆弱性を減らすために使用できる監査およびログの方法について説明します。

<table> 
 <thead> 
  <tr> 
   <th><p>問題</p> </th> 
   <th><p>説明</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>ログファイル ACL</p> </td> 
   <td><p>JEE 上の AEM Forms ログファイルには、適切なアクセス制御リスト（ACL）を設定します。</p> <p>適切な資格情報を設定することで、攻撃者によってファイルが削除されないように防御します。</p> <p>ログファイルディレクトリのセキュリティ権限として、Administrators グループおよび SYSTEM グループのフルコントロール権限が必要です。AEM Forms ユーザーアカウントには、読み取りおよび書き込み権限のみが必要です。</p> </td> 
  </tr> 
  <tr> 
   <td><p>ログファイルの冗長性</p> </td> 
   <td><p>リソースに余裕があれば、攻撃者がアクセスできないように、Syslog、Tivoli、Microsoft Operations Manager（MOM）やその他のメカニズムを使用して、ログを別のサーバーにリアルタイムで送信してください。</p> <p>この方法でログを保護することで、改ざんを防ぐことができます。さらに、中央リポジトリにログを保管することで、対比と監視に役立ちます（例えば、複数の forms サーバーを使用している場合に、パスワードの照会先となる複数のコンピューターに対してパスワード推測攻撃が行われた場合など）。</p> </td> 
  </tr> 
 </tbody> 
</table>

## 社外からのアクセスを可能にするための JEE 上の AEM Forms の設定 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

JEE 上の AEM Forms のインストールが完了したら、定期的に環境のセキュリティの保守を行うことが重要です。ここでは、JEE 上の AEM Forms 実稼働サーバーのセキュリティを維持するための推奨タスクについて説明します。

### Web アクセスのリバースプロキシの設定 {#setting-up-a-reverse-proxy-for-web-access}

「*リバースプロキシ*」は、1 セットの JEE 上の AEM Forms Web アプリケーションの URL を、外部ユーザーと内部ユーザーの両方から利用できるように設定するものです。この設定は、JEE 上の AEM Forms を実行するアプリケーションサーバーへのユーザーの直接接続を許可する方法よりも、高いセキュリティで保護されます。リバースプロキシは、JEE 上の AEM Forms を実行しているアプリケーションサーバーに対するすべての HTTP 要求を実行します。ユーザーは、リバースプロキシに対するネットワークアクセスしか持たないので、リバースプロキシでサポートされている URL 接続のみを試みることができます。

**リバースプロキシサーバーで使用する JEE 上のAEM Formsルート URL**

次のアプリケーションルート URL は、各 JEE 上の AEM Forms Web アプリケーションのものです。リバースプロキシは、エンドユーザーに提供する Web アプリケーション機能の URL だけを公開するように設定する必要があります。

一部の URL は、エンドユーザーが使用する Web アプリケーションを示しています。Configuration Manager のその他の URL は、リバースプロキシ経由の外部ユーザーのアクセスを許可しないので、公開しないでください。

<table> 
 <thead> 
  <tr> 
   <th><p>ルート URL</p> </th> 
   <th><p>用途および関連する Web アプリケーション</p> </th> 
   <th><p>Web ベースのインターフェイス</p> </th> 
   <th><p>エンドユーザーアクセス</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>PDF ドキュメントに使用権限を適用する Acrobat Reader DC Extensions エンドユーザー Web アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Rights Management エンドユーザー Web アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>Rights Management の Web サービス URL</p> </td> 
   <td><p>不可</p> </td> 
   <td><p>可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>PDF Generator 管理 Web アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CM タスク/*</p> </td> 
   <td><p>Workspace エンドユーザー Web アプリケーション</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Workspace クライアントアプリケーションが必要とする Workspace サーブレットおよび Data Services</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>JEE 上の AEM Forms をブートストラップするサーブレット</p> </td> 
   <td><p>不可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>forms サーバー Web サービスの情報ページ</p> </td> 
   <td><p>不可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>すべての forms サーバーサービス用の Web サービス URL</p> </td> 
   <td><p>不可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Rights Management 管理 Web アプリケーション</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>管理コンソールホームページ</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>secured/*</p> </td> 
   <td><p>Trust Store Management 管理ページ</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>フォームのレンダリングのテストとデバッグを行う Forms IVS アプリケーション</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>Output サービスのテストとデバッグを行う Output IVS アプリケーション</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>Rights Management のための REST URL</p> </td> 
   <td><p>不可</p> </td> 
   <td><p>可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>Output 管理ページ</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Forms Web アプリケーションファイル</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>HTML 変換時に、JavaScript の取得に使用</p> </td> 
   <td><p>不可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Forms 管理ページ</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>WebDAV（デバッグ）アクセス用の URL</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>アプリケーションおよびサービスユーザーインターフェイス</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>Workspace 管理ページ</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>残りのサポートページ</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>JEE 上の AEM Forms Core 設定ページ</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>User Management 認証</p> </td> 
   <td><p>不可</p> </td> 
   <td><p>可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>User Management 管理インターフェイス</p> </td> 
   <td><p>可</p> </td> 
   <td><p>不可</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DoumentManager/*</p> </td> 
   <td><p>HTTP ドキュメント対応の SOAP トランスポートまたは EJB トランスポート経由でリモートエンドポイント、SOAP WSDL エンドポイントおよび Java SDK にアクセスするときに、処理するドキュメントをアップロードおよびダウンロードする。</p> </td> 
   <td><p>はい</p> </td> 
   <td><p>はい</p> </td> 
  </tr> 
 </tbody> 
</table>

## クロスサイト要求偽造攻撃からの保護 {#protecting-from-cross-site-request-forgery-attacks}

クロスサイトリクエストフォージェリ (CSRF) 攻撃は、Web サイトがユーザーに対して持つ信頼を悪用し、ユーザーが許可していない、意図しないコマンドを送信します。 この攻撃は、ユーザーが既に認証済みの別のサイトにアクセスするために、Web ページにリンクやスクリプト、または電子メールメッセージに URL を含めることで設定されます。

例えば、別の Web サイトを同時に参照しながら管理コンソールにログインしたとします。 CSRF 攻撃者は、このような状況を狙って、閲覧されるサイトの Web ページに含まれている HTML img タグの `src` 属性などに、攻撃対象 Web サイト内のサーバー側スクリプトを参照する URL を記述しておきます。Web ブラウザーに備わっている Cookie ベースのセッション認証メカニズムにより、攻撃者の Web サイトは正当なユーザーを装って、攻撃対象のサーバー側スクリプトに悪意ある要求を送信することができます。

CSRF に共通の特性を次に示します。

* ユーザーの ID を信頼したサイトに関与する。
* その ID に対するサイトの信頼を利用する。
* ユーザーのブラウザーをだましてターゲットサイトに HTTP 要求を送信させる。
* 副次的な悪影響のある HTTP 要求に関与する。

JEE 上のAEM Formsは、リファラーフィルター機能を使用して CSRF 攻撃をブロックします。 この節では、リファラーのフィルタリングメカニズムについて次の用語を使用します。

* **許可されているリファラー：** リファラーは、リクエストをサーバーに送信するソースページのアドレスです。 JSP ページまたはフォームの場合、リファラーは通常、閲覧履歴の前のページです。 画像のリファラーは、通常、画像が表示されるページです。 サーバーリソースへのアクセスが許可されているリファラーを識別するには、許可されているリファラーリストにリファラーを追加します。
* **許可されるリファラーの例外：** 許可されたリファラーリストの特定のリファラーに対するアクセス範囲を制限する必要がある場合があります。 この制限を実施するには、そのリファラーの個々のパスを「許可されたリファラーの例外」リストに追加します。 許可されているリファラーの例外リスト内のパスから要求を受け取った場合、forms サーバー上のリソースを呼び出すことはできません。 特定のアプリケーションに対して許可されたリファラー例外を定義し、また、すべてのアプリケーションに適用される例外のグローバルリストを使用できます。
* **許可されている URI:** これは、リファラーヘッダーを確認せずに提供されるリソースのリストです。 例えば、サーバーの状態に変更を加えることのない、リソースのヘルプページをこのリストに追加できます。許可された URI リスト内のリソースが、リファラーが誰であるかに関係なく、リファラーフィルターでブロックされることはありません。
* **ヌルリファラー：** 親 Web ページに関連付けられていない、または親 Web ページから派生していないサーバーリクエストは、ヌルリファラーからのリクエストと見なされます。 例えば、新しいブラウザーウィンドウを開き、アドレスを入力して Enter キーを押すと、サーバーに送信されるリファラーが null になります。 Web サーバーに HTTP リクエストを送信するデスクトップアプリケーション（.NET または SWING）も、Null リファラーをサーバーに送信します。

### リファラーフィルタリング {#referer-filtering}

リファラーのフィルタリングプロセスは、次のように記述できます。

1. forms サーバーが、呼び出しに使用される HTTP メソッドを確認します。

   1. POSTの場合、forms サーバーがリファラーヘッダーのチェックを実行します。
   1. GETの場合、forms サーバーはリファラーチェックをバイパスします。ただし、 *CSRF_CHECK_GETS* が true に設定されている場合、リファラーヘッダーのチェックが実行されます。 ** CSRF_CHECK_GETS は、アプリケーションの ** web.xml ファイル内に設定されます。

1. forms サーバーは、要求された URI が許可リストに加えるされているかどうかを確認します。

   1. URI が許可リストに加えるされた場合、サーバーは要求を受け入れます。
   1. 要求された URI が許可リストに加えるされない場合、サーバーは要求のリファラーを取得します。

1. リクエストにリファラーがある場合、サーバーは許可されているリファラーかどうかを確認します。 許可されている場合、サーバーはリファラーの例外を確認します。

   1. 例外の場合、リクエストはブロックされます。
   1. 例外でない場合、要求はパスします。

1. リクエストにリファラーがない場合、サーバーは null リファラーが許可されているかどうかを確認します。

   1. Null リファラーが許可されている場合、リクエストが渡されます。
   1. Null リファラーが許可されていない場合、サーバーは要求された URI が Null リファラーの例外であるかどうかを確認し、それに応じて要求を処理します。

### リファラーフィルタリングの管理 {#managing-referer-filtering}

JEE 上のAEM Formsには、サーバーリソースへのアクセスが許可されるリファラーを指定するリファラーフィルターが用意されています。 デフォルトでは、リファラーフィルターは、安全な HTTP メソッド ( 例：GET) を使用する要求をフィルタリングしません ( ただし、 *CSRF_CHECK_GETS* が true に設定されている。 「許可されているリファラー」エントリのポート番号が 0 に設定されている場合、JEE 上のAEM Formsは、ポート番号に関係なく、そのホストからのリファラーを持つすべての要求を許可します。 ポート番号が指定されていない場合は、デフォルトのポート 80（HTTP）またはポート 443（HTTPS）からの要求のみが許可されます。許可されているリファラーリストのすべてのエントリが削除されると、リファラーフィルタリングは無効になります。

Document Services を初めてインストールすると、許可されているリファラーリストが、Document Services がインストールされているサーバーのアドレスで更新されます。 サーバーのエントリには、サーバー名、IPv4 アドレス、IPv6 アドレス（IPv6 が有効の場合）、ループバックアドレス、localhost エントリなどがあります。許可されているリファラーリストに追加された名前は、ホストオペレーティングシステムから返されます。 例えば、IP アドレスが10.40.54.187のサーバーには、次のエントリが含まれます。 `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. ホストオペレーティングシステムによって返された不適格な名前（IPv4 アドレス、IPv6 アドレス、または修飾ドメイン名を持たない名前）の場合許可リスト、は更新されません。 ビジネス環境に合わせて「許可されているリファラー」リストを変更します。 実稼動環境に forms サーバーをデプロイする際には、デフォルトの許可されているリファラーリストを使用しないでください。 許可されているリファラー、リファラーの例外または URI を変更した後、必ずサーバーを再起動して、変更を有効にします。

**許可されているリファラーリストの管理**

許可されたリファラーリストは、管理コンソールのユーザー管理インターフェイスから管理できます。 User Management インターフェイスを使用すると、リストを作成、編集または削除できます。*を参照してください。 [CSRF 攻撃の防止](/help/forms/using/admin-help/preventing-csrf-attacks.md)*セクション *管理ヘルプ* を参照してください。

**許可されるリファラーの例外と許可される URI リストの管理**

JEE 上のAEM Formsには、「許可されたリファラーの例外」リストと「許可された URI 」リストを管理する API が用意されています。 この API を使用すると、リストを取得、作成、編集または削除できます。使用可能な API のリストを次に示します。

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

API について詳しくは、「* AEM Forms on JEE API Reference*」を参照してください。

以下を使用： ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** 許可されるリファラーの例外のリストをグローバルレベルで表示します。つまり、すべてのアプリケーションに適用できる例外を定義します。 このリストには、絶対パス ( 例えば、  `/index.html`) または相対パス ( 例：  `/sample/`) をクリックします。 また、相対 URI の末尾に正規表現を追加することもできます。例えば、  `/sample/(.)*`.

***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** リスト ID は、`UMConstants` 名前空間の `com.adobe.idp.um.api` クラスで定数として定義されており、`adobe-usermanager-client.jar` にあります。この AEM Forms API を使用すると、リストを取得、作成、編集または削除できます。例えば、グローバルに許可されているリファラーの例外リストを作成するには、次を使用します。

```as3
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

アプリケーション固有の例外については、***CSRF_ALLOWED_REFERER_EXCEPTIONS*** リストを使用します。

**リファラーフィルターの無効化**

リファラーフィルターによって forms サーバーへのアクセスが完全にブロックされ、許可されたリファラーリストを編集できない場合は、サーバー起動スクリプトを更新して、リファラーフィルタリングを無効にできます。

次を含める： `-Dlc.um.csrffilter.disabled=true` 起動スクリプトの JAVA 引数を使用し、サーバーを再起動します。 許可されているリファラーリストを適切に再設定した後で、JAVA 引数を削除するようにしてください。

**カスタム WAR ファイルのリファラーフィルタリング**

管理者は、ビジネス要件に合わせて JEE 上の AEM Forms を操作するためのカスタム WAR ファイルを用意している場合があります。カスタム WAR ファイルのリファラーフィルタリングを有効にするには、以下を実行します。 ***adobe-usermanager-client.jar*** を WAR のクラスパスに追加し、次のパラメーターを指定して、* web.xml*ファイルにフィルターエントリを含めます。

**CSRF_CHECK_GETS** は、リファラーリクエストのGETチェックを制御します。 このパラメーターが定義されていない場合、デフォルト値は false に設定されます。このパラメーターは、GET 要求をフィルタリングする場合にのみ指定します。

**CSRF_ALLOWED_REFERER_EXCEPTIONS** は、「許可されているリファラーの例外」リストの ID です。 リファラーフィルターは、リスト ID によって識別されるリスト内のリファラーからの要求が、forms サーバー上のリソースを呼び出すのを防ぎます。

**CSRF_ALLOWED_URIS_LIST_NAME** は、許可されている URI リストの ID です。リファラーフィルターは、リクエストの Referrer ヘッダーの値に関係なく、リスト ID で識別されるリスト内のリソースに対する要求をブロックしません。

**CSRF_ALLOW_NULL_REFERER** は、リファラーが null の場合、または存在しない場合のリファラーフィルタの動作を制御します。 このパラメーターが定義されていない場合、デフォルト値は false に設定されます。このパラメーターは、null リファラーを許可する場合にのみ指定します。 null リファラーを許可すると、一部のタイプのクロスサイトリクエストフォージェリ攻撃が可能になる場合があります。

**CSRF_NULL_REFERER_EXCEPTIONS** は、リファラーが null の場合にリファラーチェックが実行されない URI のリストです。 このパラメーターは、*CSRF_ALLOW_NULL_REFERER* が false に設定されている場合にのみ有効です。リスト内で複数の URI を指定するときはコンマで区切ります。

*サンプル* WAR ファイルに対する ***web.xml*** ファイルのフィルターエントリの例を次に示します。

```as3
<filter> 
       <filter-name> filter-name </filter-name> 
       <filter-class> com.adobe.idp.um.auth.filter.RemoteCSRFFilter </filter-class> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_ALLOW_NULL_REFERER </param-name> 
      <param-value> false </param-value> 
     </init-param> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_CHECK_GETS </param-name> 
      <param-value> true </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
       <param-name> CSRF_NULL_REFERER_EXCEPTIONS </param-name> 
       <param-value> /SAMPLE/login, /SAMPLE/logout  </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_REFERER_EXCEPTIONS </param-name> 
      <param-value> SAMPLE_ALLOWED_REF_EXP_ID </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_URIS_LIST_NAME </param-name> 
      <param-value> SAMPLE_ALLOWED_URI_LIST_ID     </param-value> 
     </init-param> 
</filter> 
    ........ 
    <filter-mapping> 
      <filter-name> filter-name </filter-name> 
      <url-pattern>/*</url-pattern> 
    </filter-mapping>
```

**トラブルシューティング**

適切なサーバー要求が CSRF フィルターによってブロックされる場合は、次のいずれかを試してみてください。

* 拒否されたリクエストにリファラーヘッダーがある場合は、許可されているリファラーリストに追加することを慎重に検討します。 信頼できるリファラーのみを追加します。
* 拒否されたリクエストにリファラーヘッダーがない場合は、リファラーヘッダーを含めるようにクライアントアプリケーションを変更します。
* クライアントがブラウザーで動作できる場合は、そのデプロイメントモデルを試してみます。
* 最後の手段として、許可されている URI リストにリソースを追加できます。ただし、これは推奨設定ではありません。

## ネットワーク設定の保護 {#secure-network-configuration}

ここでは、JEE 上の AEM Forms が必要とするプロトコルとポートについて説明し、保護されたネットワーク設定で JEE 上の AEM Forms をデプロイするための推奨事項を示します。

### JEE 上の AEM Forms で使用されるネットワークプロトコル {#network-protocols-used-by-aem-forms-on-jee}

前の節で説明したように、保護されたネットワークアーキテクチャを設定する場合、エンタープライズネットワーク内の JEE 上の AEM Forms と他のシステムのやり取りのために次のネットワークプロトコルが必要です。

<table> 
 <thead> 
  <tr> 
   <th><p>プロトコル</p> </th> 
   <th><p>使用方法</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>Configuration Manager およびエンドユーザー Web アプリケーションをブラウザーに表示する</p> </li> 
     <li><p>すべての SOAP 接続</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP[SOAP]</p> </td> 
   <td> 
    <ul> 
     <li><p>.NET アプリケーションなどの Web サービスクライアントアプリケーション</p> </li> 
     <li><p>Adobe Reader® は JEE 上の AEM Forms サーバー Web サービスとのやり取りに SOAP を使用する</p> </li> 
     <li><p>Adobe Flash® アプリケーションは Forms サーバー Web サービスとのやり取りに SOAP を使用する</p> </li> 
     <li><p>SOAP モードで使用された場合に JEE 上の AEM Forms SDK によって呼び出される</p> </li> 
     <li><p>Workbench 設計環境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>Enterprise JavaBeans（EJB）モードで使用された場合に JEE 上の AEM Forms SDK によって呼び出される</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP/POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>サービスに対する電子メールベースの入力（電子メールエンドポイント）</p> </li> 
     <li><p>電子メールを使用したユーザータスク通知</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC ファイル IO</p> </td> 
   <td><p>サービスに対する入力用の監視フォルダーを JEE 上の AEM Forms で監視する（監視フォルダーエンドポイント）</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>ディレクトリ内の組織ユーザーとグループ情報を同期する</p> </li> 
     <li><p>対話的にやり取りするユーザーに LDAP 認証を行う</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>JDBC サービスを使用したプロセスの実行時に、外部データベースに対するクエリーとプロシージャの呼び出しを行う</p> </li> 
     <li><p>JEE 上の AEM Forms リポジトリへの内部からのアクセス</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>任意の WebDAV クライアントによる JEE 上の AEM Forms デザイン時リポジトリ（フォーム、フラグメントなど）のリモート参照を有効にする</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>JEE 上の AEM Forms サーバーサービスがリモートエンドポイントとして設定されている Adobe Flash アプリケーション</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>JEE 上の AEM Forms は監視対象の MBeans を JMX を使用して公開する</p> </td> 
  </tr> 
 </tbody> 
</table>

### アプリケーションサーバーのポート {#ports-for-application-servers}

ここでは、サポートしている各種のアプリケーションサーバーのデフォルトポート（および代替設定の範囲）について説明します。これらのポートについては、JEE 上の AEM Forms を実行しているアプリケーションサーバーに接続するクライアントに対して許可するネットワーク機能に応じて、内側のファイアウォール上で有効と無効を切り替える必要があります。

>[!NOTE]
>
>デフォルトでは、サーバーは、adobe.com 名前空間内に複数の JMX MBeans を公開します。サーバーの正常性監視に有用な情報だけが公開されます。ただし、情報開示を防ぐには、信頼できないネットワーク内の呼び出し元によって JMX MBeans の参照と正常性評価基準へのアクセスが行われないようにする必要があります。

**JBoss ポート**

<table> 
 <thead> 
  <tr> 
   <th><p>目的</p> </th> 
   <th><p>ポート</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Web アプリケーションへのアクセス</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>HTTP/1.1 コネクタポート 8080</p> <p>AJP 1.3 コネクタポート 8009</p> <p>SSL/TLS コネクタポート 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>CORBA サポート</p> </td> 
   <td><p>[JBossroot]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**WebLogic ポート**

<table> 
 <thead> 
  <tr> 
   <th><p>目的</p> </th> 
   <th><p>ポート</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Web アプリケーションへのアクセス</p> </td> 
   <td> 
    <ul> 
     <li><p>管理サーバーリスンポート：デフォルトは 7001</p> </li> 
     <li><p>管理サーバー SSL リスンポート：デフォルトは 7002</p> </li> 
     <li><p>管理対象サーバー用に設定されたポート：8001 など</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JEE 上の AEM Forms へのアクセスに必要とされない WebLogic 管理ポート</p> </td> 
   <td> 
    <ul> 
     <li><p>管理対象サーバーリスンポート：1 ～ 65534 の範囲で設定可能</p> </li> 
     <li><p>管理対象サーバー SSL リスンポート：1 ～ 65534 の範囲で設定可能</p> </li> 
     <li><p>ノードマネージャーリスンポート：デフォルトは 5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere ポート**

JEE 上のAEM Formsで必要な WebSphere ポートについて詳しくは、WebSphere Application Server UI の Port number setting を参照してください。

### SSL の設定 {#configuring-ssl}

「 」の節で説明する物理アーキテクチャの参照 [JEE 上のAEM Formsの物理アーキテクチャ](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)を使用する場合は、使用するすべての接続に対して SSL を設定する必要があります。 特に SOAP 接続は、ネットワーク上にユーザー資格情報が公開されないように、すべて SSL 経由で行う必要があります。

JBoss、WebLogic および WebSphere 上で SSL を設定する手順については、[管理ヘルプ](https://www.adobe.com/go/learn_aemforms_admin_64)の「SSL の設定」を参照してください。

### SSL リダイレクトの設定 {#configuring-ssl-redirect}

SSL をサポートするようにアプリケーションサーバーを設定した後、 アプリケーションおよびサービスに対するすべての HTTP トラフィックは、SSL ポートを使用するように強制されます。

WebSphere または WebLogic で SSL リダイレクトを設定するには、使用しているアプリケーションサーバーのドキュメントを参照してください。

1. コマンドプロンプトを開き、 /JBOSS_HOME/standalone/configuration ディレクトリに移動して、次のコマンドを実行します。

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. JBOSS_HOME/standalone/configuration/standalone.xmlファイルを編集用に開きます。

   次の期間の後 &lt;subsystem xmlns=&quot;urn&lt;span id=&quot; translate=&quot;no&quot; />ドメイン:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;> 要素を追加し、次の詳細を追加します。:jboss:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. https コネクタ要素に次のコードを追加します。

   ```
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   standalone.xml ファイルを保存して閉じます。

## Windows 固有のセキュリティに関する推奨事項 {#windows-specific-security-recommendations}

ここでは、JEE 上の AEM Forms の実行に使用する場合の Windows 固有のセキュリティ推奨事項について説明します。

### JBoss サービスアカウント {#jboss-service-accounts}

JEE 上の AEM Forms 自動インストールは、デフォルトで、ローカルシステムアカウントを使用してサービスアカウントを設定します。組み込みのローカルシステムユーザーアカウントは、高いレベルのアクセス権限を付与されており、Administrators グループに属しています。ワーカープロセス ID をローカルシステムユーザーアカウントで実行した場合、ワーカープロセスはシステム全体に対してフルアクセス権限を持ちます。

#### 管理者以外のアカウントでのアプリケーションサーバーの実行 {#run-the-application-server-using-a-non-administrative-account}

1. Microsoft 管理コンソール（MMC）で、forms サーバーサービスへのログインに使用するローカルユーザーを作成します。

   * 「**ユーザーはパスワードを変更できない**」オプションを選択します。
   * 「**所属するグループ**」タブに、「ユーザー」グループが表示されていることを確認してください。

1. **設定**／**管理ツール**／**サービス**&#x200B;を選択します。
1. アプリケーションサーバーサービスをダブルクリックし、サービスを停止します。
1. 「**ログオン**」タブで、「**アカウント**」を選択し、作成したユーザーアカウントを参照して、アカウントのパスワードを入力します。
1. ローカルセキュリティ設定ウィンドウの「ユーザー権利の割り当て」で、forms サーバーを実行しているユーザーアカウントに次の権限を付与します。

   * ターミナルサービスを使ったログオンを拒否する
   * ローカルでログオンを拒否する
   * サービスとしてログオン（通常は既に設定済み）

1. 新しく作成したユーザーアカウントに、JEE 上の AEM Forms Web コンテンツディレクトリの項目に対する「読み取りと実行」、「フォルダの内容の一覧表示」、「読み取り」の各権限を付与します。
1. アプリケーションサーバーサービスを起動します。

### ファイルシステムのセキュリティ {#file-system-security}

JEE 上の AEM Forms は、次の方法でファイルシステムを利用します。

* ドキュメントの入力と出力を処理する際に使用する一時ファイルを格納する
* インストールしたソリューションコンポーネントのサポートに使用されるファイルをグローバルアーカイブストアに格納する
* ファイルシステムフォルダーからサービスへの入力として使用されるドロップファイルを監視フォルダーに格納する

forms サーバーサービスのドキュメントを送受信する方法として監視フォルダーを使用する場合、ファイルシステムのセキュリティを確保するために一層の予防策を講じる必要があります。ユーザーが監視フォルダーにコンテンツをドロップした場合、コンテンツは監視フォルダーを通じて公開されます。この場合、サービスは実際のエンドユーザーを認証していません。代わりに、フォルダーレベルに設定されている ACL と共有レベルセキュリティに応じて、サービスを呼び出して実行することのできるユーザーを決定しています。

## JBoss 固有のセキュリティに関する推奨事項 {#jboss-specific-security-recommendations}

ここでは、JEE 上のAEM Formsを実行する際に使用する JBoss 7.0.6 に固有のアプリケーションサーバー設定に関する推奨事項について説明します。

### JBoss 管理コンソールおよび JMX コンソールの無効化 {#disable-jboss-management-console-and-jmx-console}

JBoss 管理コンソールと JMX コンソールへのアクセスは、自動インストールオプションを使用して JBoss に JEE 上の AEM Forms をインストールしたときに設定されます。独自の JBoss Application Server を使用している場合は、JBoss 管理コンソールおよび JMX 監視コンソールへのアクセスが保護されていることを確認してください。JMX 監視コンソールへのアクセスは、jmx-invoker-service.xml という JBoss 設定ファイルで設定されています。

### ディレクトリ参照の無効化 {#disable-directory-browsing}

管理コンソールにログインした後で、URL を変更することで、コンソールのディレクトリリストを参照できます。 例えば、URL を次のいずれかの URL に変更すると、ディレクトリ一覧が表示される場合があります。

```as3
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## WebLogic 固有のセキュリティに関する推奨事項 {#weblogic-specific-security-recommendations}

ここでは、JEE 上の AEM Forms の実行時に WebLogic 9.1 を保護するためのアプリケーションサーバー設定の推奨事項について説明します。

### ディレクトリ参照の無効化 {#disable_directory_browsing-1}

weblogic.xml ファイルの index-directories プロパティを `false` に設定します。次に例を示します。

```as3
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### WebLogic SSL ポートの有効化 {#enable-weblogic-ssl-port}

デフォルトでは、WebLogic はデフォルト SSL リスンポート 7002 を有効にしません。SSL を設定する前に、WebLogic Server 管理コンソールでこのポートを有効にしてください。

## WebSphere 固有のセキュリティに関する推奨事項 {#websphere-specific-security-recommendations}

ここでは、JEE 上の AEM Forms の実行時に WebSphere を保護するためのアプリケーションサーバー設定の推奨事項について説明します。

### ディレクトリ参照の無効化 {#disable_directory_browsing-2}

を `directoryBrowsingEnabled` プロパティを ibm-web-ext.xml ファイルで次の値に設定します。 `false`.

### WebSphere 管理セキュリティの有効化 {#enable-websphere-administrative-security}

1. WebSphere Administrative Console にログインします。
1. ナビゲーションツリーで、に移動します。 **セキュリティ** > **グローバルセキュリティ**
1. 「**Enable administrative security**」を選択します。
1. 「**Enable application security**」および「**Use Java 2 security**」の選択を解除します。
1. 「**OK**」または「**Apply**」をクリックします。
1. 「**Messages**」ボックスで、「**Save directly to the master configuration**」をクリックします。
