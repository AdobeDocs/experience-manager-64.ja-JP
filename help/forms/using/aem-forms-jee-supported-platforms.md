---
title: JEE 上の AEM Forms でサポートされているプラットフォーム
seo-title: JEE 上の AEM Forms でサポートされているプラットフォーム
description: JEE での AEM Forms のインストールに必要な（およびサポートされた）インフラストラクチャコンポーネントのリスト
seo-description: JEE での AEM Forms のインストールに必要な（およびサポートされた）インフラストラクチャコンポーネントのリスト
uuid: 22f05fd4-f9fc-423e-8a86-1e75df4b2b44
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 1b9f8d98-e7e8-4b9b-a0df-52ccba324da3
role: Administrator
translation-type: tm+mt
source-git-commit: 75312539136bb53cf1db1de03fc0f9a1dca49791
workflow-type: tm+mt
source-wordcount: '3317'
ht-degree: 85%

---


# JEE 上の AEM Forms でサポートされているプラットフォーム {#supported-platforms-for-aem-forms-on-jee}

## サポートされているプラットフォーム {#supported-platforms}

### サポートレベル {#support-levels}

JEE サーバー上の AEM Forms は、サポートされているオペレーティングシステム、アプリケーションサーバー、データベース、データベースドライバー、JDK、LDAP サーバー、および電子メールサーバーを自由に組み合わせて設定することができます。

このドキュメントでは、JEE 上の AEM Forms でサポートされているクライアントおよびサーバーのプラットフォームを示します。アドビは、推奨構成とその他の構成の両方について、複数のレベルのサポートを提供しています。このドキュメントでは、その他のサポートされているソフトウェアとバージョン、例外事項、パッチ定義、およびサードパーティソフトウェアパッチサポートポリシーも示します。

>[!NOTE]
>
>* サポートされているサーバープラットフォームへの例外エラーの完全リストについては、[サポートされているサーバープラットフォームへの例外エラー](#exceptions-to-supported-server-platforms)を参照してください。
>* JEE 上の AEM Forms でサポートされるのは、英語、フランス語、ドイツ語および日本語版のサポート対象のオペレーティングシステムとアプリケーションのみです。

>



### 推奨設定 {#recommendedconfigurations}

アドビはこれらの設定を推奨し、標準ソフトウェア保守契約の一部として全面的または制限的サポートを提供します。

<table> 
 <tbody> 
  <tr> 
   <th>サポートレベル</th> 
   <th>説明</th> 
  </tr> 
  <tr> 
   <td>A：サポート対象<br /> </td> 
   <td>アドビはこの構成への完全なサポートと保守を提供します。この構成は、アドビの品質保証プロセスでカバーされます。</td> 
  </tr> 
  <tr> 
   <td>R：制限サポート</td> 
   <td>アドビは、特定の前提条件が満たされている場合、この設定に対して全面的なサポートを提供します。前提条件およびサポートのご依頼については、アドビエンタープライズサポートにお問い合わせください。</td> 
  </tr> 
  <tr> 
   <td>L：限定的サポート</td> 
   <td>特定の条件が満たされている場合、アドビは、この設定に対して全面的なサポートと保守サービスを提供します。この設定の場合、一部の機能については使用できません。前提条件およびサポートのご依頼については、アドビエンタープライズサポートにお問い合わせください。<br /> </td> 
  </tr> 
 </tbody> 
</table>

### サポート対象外の設定 {#unsupported-configurations}

| サポートレベル | 説明 |
|---|---|
| E：動作する見込み | この構成は動作する見込みであり、動作しないという報告はありません。 |
| Z：サポート対象外 | この構成はサポートされません。アドビは、この構成が動作するかどうかに関する一切の表明をせず、この構成をサポートしません。 |

### Java 仮想マシン (JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms を使用するには、Java 仮想マシンが必要です。Java 仮想マシンは、Java Development Kit（JDK）ディストリビューションに付属しています。Adobe Experience Manager は、次のバージョンの Java 仮想マシンで動作します。

<table> 
 <tbody> 
  <tr> 
   <th><p><strong>プラットフォーム</strong></p> </th> 
   <th><p><strong>サポートレベル</strong></p> </th> 
   <th><p><strong>サポートされているパッチ定義</strong></p> </th> 
  </tr> 
  <tr> 
   <td><p>Oracle Java™ SE 8（64 ビット版）</p> </td> 
   <td><p>A：サポート対象</p> </td> 
   <td><p>マイナーリリースとアップデート</p> </td> 
  </tr> 
  <tr> 
   <td>IBM® J9 Virtual Machine（ビルド 2.8、JRE 1.8.0）</td> 
   <td>A：サポート対象</td> 
   <td>マイナーリリースとアップデート</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>* JEE 上の AEM Forms では、実稼動環境に対して 64 ビットの JVM のみがサポートされています。
>* Java ベンダーが発表するセキュリティ情報を常に確認し、実稼働環境の安全性とセキュリティを確保すること、および最新の Java 更新プログラムをインストールすることを推奨します。

>



### データベースと CRX の永続性 {#databases-and-crx-persistence}

#### AEM の永続性サポート {#aem-persistence-support}

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>プラットフォーム</strong></p> </td> 
   <td><p><strong> 説明</strong></p> </td> 
   <td><p><strong>サポートレベル</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>ファイルシステム</p> </td> 
   <td><p>Repository Microkernel（TAR MK ファイル）</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr> 
  <tr> 
   <td><p>MongoDB Enterprise 3.4</p> </td> 
   <td><p>リポジトリ Microkernel</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr> 
  <tr> 
   <td>IBM DB2 11.1</td> 
   <td>リポジトリ Microkernel</td> 
   <td>サポート対象</td> 
  </tr> 
  <tr> 
   <td><p>Oracleデータベース12cリリース1</p> </td> 
   <td><p>リポジトリ Microkernel</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr> 
  <tr> 
   <td><p>Microsoft SQL Server 2016</p> </td> 
   <td><p>リポジトリ Microkernel</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr> 
 </tbody> 
</table>

* MongoDB はサードパーティソフトウェアであり、AEM ライセンスパッケージには含まれていません。詳しくは、[MongoDB のライセンスポリシー](https://www.mongodb.org/about/licensing/)ページを参照してください。

* AEM デプロイメントを最大限活用するために、アドビは、プロフェッショナルサポートを受けられる MongoDB Enterprise バージョンのライセンスを取得することを推奨しています。
* アドビカスタマーケアは、AEM での MongoDB の使用に関する問題の絞り込みを支援します。詳しくは、[MongoDB for Adobe Experience Manager のページ](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。
* 「ファイルシステム」には、POSIX 準拠のブロックストレージが含まれます。ブロックストレージには、ネットワークストレージテクノロジーが含まれます。ファイルシステムのパフォーマンスが状況に応じて変化し、全体的なパフォーマンスに影響を及ぼす可能性があることに注意してください。ネットワークやリモートファイルシステムと一緒に AEM の負荷テストを行うことを推奨します。
* MongoDB Storage Engine WiredTiger のみサポートされます。
* MongoDB Sharding は AEM ではサポートされていません。
* JEE 上の AEM Forms はRDBMK 永続性タイプの MySQL をサポートしません。
* Document Security モジュールは、Content Repository を使用しません。Document Security だけを使用し、HTML Workspace、HTML5 フォーム、アダプティブフォームを使用しない場合は、Content Repository をインストールしないでください。
* JEE 上の AEM Forms では、Oracle Multitenant アーキテクチャがサポートされます。

#### データベースのサポート {#database-support}

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>プラットフォーム</strong></p> </td> 
   <td><p><strong> 説明</strong></p> </td> 
   <td><p><strong>AEM 6.4 のサポートレベル</strong></p> </td> 
   <td><p><strong>JEE 上の AEM Forms 6.4 のサポートレベル</strong></p> </td> 
  </tr> 
  <tr> 
   <td>IBM DB2 11.1</td> 
   <td>リポジトリ Microkernel</td> 
   <td>サポート対象</td> 
   <td>サポート対象</td> 
  </tr> 
  <tr> 
   <td><p>Oracleデータベース12cリリース1</p> </td> 
   <td><p>リポジトリ Microkernel</p> </td> 
   <td><p>サポート対象</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr> 
  <tr> 
   <td><p>MySQL 5.7.19<br /> </p> </td> 
   <td><p>リポジトリ Microkernel</p> </td> 
   <td><p>正常機能が期待</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr> 
  <tr> 
   <td><p>Microsoft SQL Server 2016</p> </td> 
   <td><p>リポジトリ Microkernel</p> </td> 
   <td><p>正常機能が期待</p> </td> 
   <td><p>サポート対象</p> </td> 
  </tr> 
 </tbody> 
</table>

### データベースドライバー {#database-drivers}

<table> 
 <tbody> 
  <tr> 
   <th>データベース </th> 
   <th><p><strong>プラットフォーム</strong></p> </th> 
   <th><p><strong>サポートされているパッチ定義</strong></p> </th> 
  </tr> 
  <tr> 
   <td>MySQL</td> 
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.30-bin.jar(version 5.1.30)</p> </td> 
   <td><p>JEE での AEM Forms のインストールに付属</p> </td> 
  </tr> 
  <tr> 
   <td>Microsoft SQL Server<br /> </td> 
   <td><p>Microsoft® SQL Server JDBC ドライバー 6.2.1.0<br /> </p> <p>sqljdbc6.jar</p> </td> 
   <td><p>JEE での AEM Forms のインストールに付属</p> </td> 
  </tr> 
  <tr> 
   <td>Oracle</td> 
   <td><p>Oracle Database 12.1.0.2.0 JDBC ドライバー</p> <p>ojdbc7.jar（バージョン 12.1.0.2.0）<br /> </p> </td> 
   <td><p>JEE での AEM Forms のインストールに付属</p> </td> 
  </tr> 
  <tr> 
   <td>IBM DB2</td> 
   <td><p>IBM® DB2 ユニバーサル JDBC ドライバー 4.16.53 (db2jcc4.jar)</p> </td> 
   <td><p><a href="https://www-01.ibm.com/support/docview.wss?uid=swg21363866" target="_blank">IBM Web サイト</a>からドライバーをダウンロード</p> </td> 
  </tr> 
 </tbody> 
</table>

### アプリケーションサーバー {#application-servers}

<table> 
 <tbody> 
  <tr> 
   <td><p><strong> プラットフォーム</strong></p> </td> 
   <td><p><strong>サポートレベル</strong></p> </td> 
   <td><p><strong>サポートされているパッチ定義</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Oracle WebLogic Server 12.2.1 (12c R2) <sup>[1] [2] [4] [8]</sup></p> </td> 
   <td><p>A：サポート対象</p> </td> 
   <td><p>サービスパックと重要なアップデート</p> </td> 
  </tr> 
  <tr> 
   <td>IBM® WebSphere® Application Server 9.0 <sup>[2] [6]</sup><br /> </td> 
   <td>A：サポート対象</td> 
   <td>サービスパックと重要なアップデート</td> 
  </tr> 
  <tr> 
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.0.6 <sup>[1] [4] [5] [7] [8][11]</sup></p> </td> 
   <td><p>A：サポート対象</p> </td> 
   <td><p>パッチと累積パッチ（サポート対象の EAP バージョン用）<br /> </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>IBM® WebSphere® のクラスターは、Network Deployment エディションでのみサポートされます。

### サーバーオペレーティングシステム {#server-operating-systems}

#### 実稼動環境 {#production-environments}

<table> 
 <tbody> 
  <tr> 
   <th><p><strong> プラットフォーム</strong></p> </th> 
   <th><p><strong>サポートレベル</strong></p> </th> 
   <th><p><strong>サポートされているパッチ定義</strong></p> </th> 
  </tr> 
  <tr> 
   <td>Microsoft Windows Server 2016</td> 
   <td>A：サポート対象</td> 
   <td>サービスパックと重要なアップデート</td> 
  </tr> 
  <tr> 
   <td><p>Microsoft Windows Server 2012 R2 V6.3</p> </td> 
   <td><p>A：サポート対象</p> </td> 
   <td><p>サービスパックと重要なアップデート</p> </td> 
  </tr> 
  <tr> 
   <td><p>OracleSolaris™ 11 - V5.11<sup> [3] [10]</sup></p> </td> 
   <td><p>L：限定的サポート</p> </td> 
   <td><p>アップデートとパッチ</p> </td> 
  </tr> 
  <tr> 
   <td><p>Red Hat Enterprise Linux 7 (Kernel 3.x)</br><b>注意：</b> <a href="https://access.redhat.com/articles/4665701">Red Hat Enterprise Linux 6</a>はメンテナンス終了段階に達し、2020年11月30日に延長ライフサイクルサポート段階にトランジションします。 Adobeでは、アップグレードと新規インストールにRed Hat Enterprise Linux 7を推奨します。 既存のインストールでは、拡張ライフサイクルサポート段階でRed Hat Enterprise Linux 6を使用できます。</p> </td> 
   <td><p>A：サポート対象</p> </td> 
   <td><p>マイナーリリース、累積アップデート、および緊急アップデート</p> </td> 
  </tr> 
  <tr> 
   <td><p>SUSE® Linux® Enterprise Server 12</p> </td> 
   <td><p>A：サポート対象</p> </td> 
   <td><p>サービスパック、累積パッチ、および緊急セキュリティアップデート</p> </td> 
  </tr> 
  <tr> 
   <td>Oracle Linux® 7 Update 3</td> 
   <td>A：サポート対象</td> 
   <td>サービスパック、累積パッチ、および緊急セキュリティアップデート</td> 
  </tr> 
  <tr> 
   <td>CentOS 7<sup> [9]</sup></td> 
   <td>A：サポート対象</td> 
   <td>サービスパック、累積パッチ、および緊急セキュリティアップデート</td> 
  </tr> 
  <tr> 
   <td>IBM AIX 7.2 [10]</td> 
   <td>A：限定的サポート</td> 
   <td>サービスパック、累積パッチ、および緊急セキュリティアップデート</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>JEE 上の AEM Forms では、64 ビットのオペレーティングシステムのみがサポートされています。

#### 視覚化環境  {#virtualized-environment}

JEE 上の AEM Forms は、物理マシンまたはバーチャル環境で実行できます。ただし、バーチャル環境での AEM Forms の使用に問題が発生した場合は、その問題の物理マシン上での再現を試みてください。物理マシン上で問題が解決しない場合は、Adobeサポートに問い合わせて解決してください。 物理マシン上では再現されない問題に関しては、バーチャル環境のベンダーにお問い合わせください。

#### 開発環境 {#development-environments}

<table> 
 <tbody> 
  <tr> 
   <th><p><strong>プラットフォーム（基本バージョン）</strong></p> </th> 
   <th>サポートレベル</th> 
   <th><p><strong>サポートされているパッチ定義</strong></p> </th> 
  </tr> 
  <tr> 
   <td><p>Microsoft® Windows® 10</p> </td> 
   <td>E：動作する見込み</td> 
   <td><p>サービスパックと重要なアップデート</p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>* JEE 上の AEM Forms では、64 ビットのオペレーティングシステムのみがサポートされています。
>* PDF Generator サービスは Windows 10 ではサポートされていません。

>



### サポートされているサーバープラットフォームの例外事項 {#exceptions-to-supported-server-platforms}

JEE サーバーでの AEM Forms の設置でプラットフォームを選択するときは、次の例外事項を考慮してください。

1. JEE 上の AEM Forms では、IBM® AIX® 上での Oracle WebLogic および JBoss® をサポートしていません。
1. JEE 上の AEM Forms では、Oracle WebLogic および IBM® WebSphere® を MySQL でサポートしていません。
1. JEE 上の AEM Forms では、Intel® アーキテクチャでは Oracle Solaris™ をサポートしていません(SPARC® のみがサポートされています)。
1. JEE 上の AEM Forms では、SUSE Linux Enterprise Server 12 上での Oracle WebLogic および JBoss をサポートしていません。SUSE Linux Enterprise Server 12 上では、IBM WebSphere のみがサポートされています。
1. JEE 上の AEM Forms は、JBoss® では Oracle Java™ SE 以外のいかなる JDK もサポートしていません。
1. JEE 上の AEM Forms は、IBM® WebSphere® では IBM® JDK 以外のいかなる JDK もサポートしていません。
1. JEE 上の AEM Forms では、JBoss® で IBM® DB2 をサポートしていません。
1. CRX-repositoryは、TarMK、MongoDB、およびリレーショナルデータベース(RDBMK)タイプの永続性をサポートします。 アプリケーションサーバーとCRX-repositoryの間に2つの異なるデータベースシステムを持つことはできません。 ただし、JEE上のAEM Forms環境では、MongoMKをCRXリポジトリで使用し、サポートされているリレーショナルデータベースをアプリケーションサーバーで使用できます。
1. JEE 上の AEM Forms は CentOS 上の WebSphere Application Server をサポートしていません。
1. AIX オペレーティングシステムと Solaris オペレーティングシステムを使用できるのは、アップグレードを行う場合だけです。
1. JEE 上の AEM Forms では、JBoss ロールベースのアクセス制御（RBAC）をサポートしていません。

この他に、JEE 上での Adobe AEM Forms の導入のためにソフトウェアを選択する際には、次の項目を考慮してください。

* JEE 上の AEM Forms では、指定されたメジャーおよびマイナーバージョンのサポートソフトウェアに対して、アップデート、パッチ、および修正パックをサポートしています。ただし、次のメジャーまたはマイナーバージョンに対するアップデートは、とくに記載がない限りサポートされていません。
* クラスタベースのインストールは、TarMK 永続性タイプをサポートしません。サポートされている永続性については、[AEM Forms のインストールに永続性タイプを選択する](/help/forms/using/choosing-persistence-type-for-aem-forms.md)を参照してください。
* JEE 上の AEM Forms では、弊社の[サードパーティソフトウェアサポートポリシー](#third-party-patch-support-policy)に従い、さまざまなサードパーティ製のソフトウェアをサポートしています。
* JEE 上の AEM Forms では、サードパーティベンダーによって提供されているサポートに基づいてプラットフォームをサポートします。組み合わせによっては、サードパーティベンダーが許可しない場合があります。例えば、多くのベンダーが、自社のアプリケーションサーバーを IBM® DB2 で使用することを認めていません。この結果、JEE 上の AEM Forms でもこれらの組み合わせをサポートしていません。サポートされているソフトウェアバージョンを確実に選択するようにするために、サードパーティベンダーのサポート表もチェックしてください。
* JEE 上の AEM Forms は TarMK コールドスタンバイをサポートしません。
* JEE 上の AEM Forms は垂直クラスタリングをサポートしません。
* JEE 上の AEM Forms では、クラスター環境での MySQL データベースをサポートしていません。
* パッケージ JDBC モジュールが Weblogic 上で構成されている場合、RDBMK は DB2、MYSQL、MS SQL および Oracle データベースと一緒には機能しません。

### LDAP サーバー (オプション) {#ldap-servers-optional}

<table> 
 <tbody> 
  <tr> 
   <th><p><strong>製品（基本バージョン）</strong></p> </th> 
   <th><p><strong>サポートされているパッチ定義</strong></p> </th> 
  </tr> 
  <tr> 
   <td>Oracle Unified Directory（OUD）11g リリース 2</td> 
   <td>サービスパック</td> 
  </tr> 
  <tr> 
   <td>Microsoft Active Directory 2016</td> 
   <td>メンテナンスリリースおよび修正パック</td> 
  </tr> 
  <tr> 
   <td><p>Microsoft® Active Directory 2012</p> </td> 
   <td><p>オペレーティングシステムで提供されるアップデート</p> </td> 
  </tr> 
  <tr> 
   <td><p>Microsoft Active Directory Lightweight Directory Services 2012</p> </td> 
   <td><p>オペレーティングシステムで提供されるアップデート</p> </td> 
  </tr> 
  <tr> 
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td> 
   <td><p>フィーチャーパックと暫定フックス</p> </td> 
  </tr> 
  <tr> 
   <td>IBM Lotus Domino 8.5.0</td> 
   <td>メンテナンスリリースおよび修正パック</td> 
  </tr> 
  <tr> 
   <td>Novell eDirectory 8.8.7</td> 
   <td>製品アップデート</td> 
  </tr> 
 </tbody> 
</table>

### 電子メールサーバー (オプション) {#email-servers-optional}

* IBM Lotus Domino 9.0
* Microsoft Exchange 2013
* Microsoft Office 365

### コンテンツマネージャーと対応するコネクタ {#content-managers-and-corresponding-connectors}

<table> 
 <tbody> 
  <tr> 
   <td><strong>製品<br /> </strong></td> 
   <td><strong>バージョン</strong></td> 
  </tr> 
  <tr> 
   <td>IBM Content Manager サーバー</td> 
   <td>8.5 Fix pack 2<br /> </td> 
  </tr> 
  <tr> 
   <td>IBM Content Manager クライアント</td> 
   <td><p>バージョン8.5<strong> </strong>はサポートされています</p> </td> 
  </tr> 
  <tr> 
   <td>EMC Documentum</td> 
   <td>7.0 および 7.3</td> 
  </tr> 
  <tr> 
   <td>IBM Filenet</td> 
   <td>5.2</td> 
  </tr> 
  <tr> 
   <td>Microsoft Sharepoint</td> 
   <td>2013 および 2016<br /> </td> 
  </tr> 
 </tbody> 
</table>

### Cordova のサポート  {#support-for-cordova}

AEM FormsアプリでApache Cordovaがサポートされるようになりました。サポートされるCordovaのプラットフォーム固有のバージョンは次のとおりです。

* Apache Cordova 6.4.0
* Cordova iOS 4.3.0
* Cordova Android 6.0.0
* Cordova Windows 4.4.3

### PDF Generator のソフトウェアサポート {#software-support-for-pdf-generator}

<table> 
 <tbody> 
  <tr> 
   <th><p><strong>製品</strong></p> </th> 
   <th><p><strong>PDF への変換でサポートされている形式</strong></p> </th> 
  </tr> 
  <tr> 
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 クラシックトラック</a></td> 
   <td>XPS、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC）、HTML、HTM、DWG、DXF、DWF</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Office 2016</td> 
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF、TXT</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Office 2013</td> 
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF、TXT</td> 
  </tr> 
  <tr> 
   <td>WordPerfect X7</td> 
   <td>WP、WPD</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Office Visio 2013</td> 
   <td>VSD、VSDX</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Office Visio 2016</td> 
   <td>VSD、VSDX</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Publisher 2013</td> 
   <td>PUB</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Publisher 2016</td> 
   <td>PUB</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Project 2013</td> 
   <td>MPP</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Project 2016</td> 
   <td>MPP</td> 
  </tr> 
  <tr> 
   <td>OpenOffice 4.1.2</td> 
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLSX、DOC、DOCX、PPT、PPTX、画像形式(BMP、JPEG、JPG、TIF、TIFF、TIFF)JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、およびTXT</td> 
  </tr> 
  <tr> 
   <td>OpenOffice 3.4</td> 
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLSX、DOC、DOCX、PPT、PPTX、画像形式(BMP、JPEG、JPG、TIF、TIFF、TIFF)JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、およびTXT</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>PDF Generator では、英語、フランス語、ドイツ語および日本語版のサポート対象のオペレーティングシステムとアプリケーションのみがサポートされます。
>
>さらに、次の点に注意してください。
>
>* PDF Generatorで変換を実行するには、32ビット版の[Acrobat2017クラシックトラックバージョン17.011.30078以降](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html)が必要です。
>* PDF Generator では、32 ビットリテール版の Microsoft Office Professional Plus および変換に必要なその他のソフトウェアのみサポートしています。
>* PDF Generator では Microsoft Office 365 をサポートしていません。
>* OpenOffice 用 PDF Generator 変換は、Windows、Linux および Solaris でのみサポートされます。
>* HTML2PDF サービスは AIX で終了しています。
>* OCR PDF、PDF を最適化および PDF を書き出しの機能は、Windows でのみサポートされます。
>* Acrobat のバージョンは、PDF Generator 機能を有効にするために、AEM Forms にバンドルされます。バンドルされたバージョンは、AEM Forms PDF Generator で使用するために、AEM Forms ライセンスの期間中、AEM Forms でのみプログラムによってアクセスされます。詳細については、ご使用の導入環境に応じて、AEM Forms製品の説明([オンプレミス](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)または[Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))を参照してください。&quot;

>



### アクセシビリティサポートの例外事項 {#exceptions-to-accessibility-support}

AEM Forms の次のサブシステムは、[リハビリテーション法 508 条](https://www.section508.gov/)に準拠していません。

* アダプティブフォームオーサリング UI
* Forms Manager オーサリング UI
* Correspondence Management オーサリング UI
* 管理 UI（管理コンソール UI）

## JEE 上の AEM Forms の必要システム構成 {#system-requirements-for-aem-forms-on-jee}

### 最小ハードウェア要件 {#minimum-hardware-requirements}

<table> 
 <tbody> 
  <tr> 
   <td>プラットフォーム</td> 
   <td>最小ハードウェア要件</td> 
  </tr> 
  <tr> 
   <td>Microsoft Windows Server</td> 
   <td>Intel® Xeon® E5-2680、2.4 GHz プロセッサー（またはそれと同等のプロセッサー）<br /> VMWare ESX 5.1 以降<br /> RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br /> 空きディスク容量：15GB の一時的空き容量のほかに、<br />JEF 上の AEM Forms 用に22GB の空き容量</td> 
  </tr> 
  <tr> 
   <td>Sun Solaris</td> 
   <td>UltraSPARC® IIIi、1.5 GHz プロセッサー<br /> Solaris コンテナ（ゾーン）パーティション<br /> RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br /> 空きディスク容量：6 GB の一時的空き容量のほかに、<br /> JEF 上の AEM Forms 用に 22GB の空き容量</td> 
  </tr> 
  <tr> 
   <td>IBM AIX</td> 
   <td>P6 pSeries 520（モデル 52A）9131-52A、1.8 GHz プロセッサー<br /> LPAR パーティション<br /> RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br /> 空きディスク容量：6 GB の一時的空き容量のほかに、<br /> JEF 用の AEM Forms 用に 22GB の空き容量</td> 
  </tr> 
  <tr> 
   <td>SUSE Linux Enterprise Server</td> 
   <td>Intel Xeon E5-2670v2、1 つの vCPU、2.5 GHz プロセッサー<br /> AWS m3.medium（3 つの ECU）<br /> RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br /> 空きディスク容量：6 GB の一時的空き容量のほかに、<br /> JEF 上の AEM Forms 用に 22GB の空き容量</td> 
  </tr> 
  <tr> 
   <td>Red Hat Enterprise Linux</td> 
   <td>Intel Xeon E5-2670v2、1 つの vCPU、2.5 GHz プロセッサー<br /> AWS m3.medium（3 つの ECU）<br /> RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br /> 空きディスク容量：6 GB の一時的空き容量のほかに、<br />JEE 上の AEM Forms 用に 22 GB の空き容量<br /> </td> 
  </tr> 
  <tr> 
   <td>小規模な実稼働環境の場合のハードウェア要件</td> 
   <td> 
    <ul> 
     <li><strong>Intel を使用している環境</strong>：Intel® Xeon® E5-2680、2.4 GHz 以上デュアルコアプロセッサーを使用するとパフォーマンスがさらに向上します。</li> 
     <li><strong>Sun SPARC を使用している環境：</strong>UltraSPARC V 以降。</li> 
     <li><strong>IBM AIX を使用している環境：</strong> Power6 以降<br /> </li> 
     <li><strong>メモリ：</strong>4 GB <br /> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

上記以外の要件については、以下を参照してください。

* [JEE上でのシングルサーバーのAEM Forms導入に必要なシステム構成](https://www.adobe.com/go/learn_aemforms_sysreq_single_64)
* [JEE 上でのクラスター化された AEM Forms の導入に必要なシステム構成](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_64)

## JEE 上の AEM Forms でサポートされているクライアント {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

>[!NOTE]
>
>32 ビットおよび 64 ビット両方のオペレーティングシステムがサポートされています。

<table> 
 <tbody> 
  <tr> 
   <th><p><strong>プラットフォーム</strong></p> </th> 
   <th><p><strong>サポートされているパッチ定義</strong></p> </th> 
  </tr> 
  <tr> 
   <td><p>Microsoft® Windows® 10</p> <p>(Enterprise、Pro、Basic)</p> </td> 
   <td>サービスパックと重要なアップデート</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Windows® 2012 Server R2</td> 
   <td>サービスパックと重要なアップデート</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Windows® 2016 Server</td> 
   <td>サービスパックと重要なアップデート</td> 
  </tr> 
 </tbody> 
</table>

* インストールのためのディスク空き容量： 1.7 GB （Workbench のみ）、2.7 GB （Workbench、 Designer 、およびサンプルアセンブリのフルインストールを単一ドライブで行う場合）、400 MB （一時的インストールディレクトリ）、200 MB （ユーザー一時ディレクトリ）、および200 MB （Windows 一時ディレクトリ）

>[!NOTE]
>
>これらの場所がすべて 1 つのドライブ上にある場合は、インストール時に 1.5 GB の空き容量が必要です。一時ディレクトリにコピーされるファイルは、インストールが完了すると削除されます。

* Workbench を実行するためのメモリ：2 GB の RAM
* ハードウェア要件： Intel® Pentium® 4 または AMD の同等の 1 GHz プロセッサー
* 1024 X 768 ピクセル以上のモニター解像度、16 ビットカラー以上
* JEE サーバーの AEM Forms に対する TCP/IPv4 または TCP/IPv6 ネットワーク接続

>[!NOTE]
>
>Workbench を Windows にインストールするには、管理者権限が必要です。管理者以外のアカウントを使用してインストールする場合は、適切なアカウントの資格情報が求められます。

### デザイナー {#designer}

* Microsoft® Windows® 2012 Server R2、Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server、Microsoft® Windows® 10
* 1 GHz 以上の高速プロセッサー（PAE、NX、および SSE2 に対応）
* 1 GB の RAM（32-bit OS の場合）または 2 GB の RAM（64-bit OS の場合）
* 16 GB のディスク空き容量（32-bit OS の場合）または 20 GB のディスク空き容量（64-bit OS の場合）
* グラフィックメモリ — 128 MBのGPU （256 MBを推奨）
* 2.35 GB のハードディスク空き容量
* 1024 X 768 ピクセル以上のモニター解像度
* ビデオハードウェアアクセラレーション（オプション）
* Acrobat Pro DC、Acrobat Standard DC、Adobe Acrobat Reader DC
* Designerをインストールするための管理者権限

### Adobe Acrobat と Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table> 
 <tbody> 
  <tr> 
   <th><p><strong>Acrobat および Adobe Reader（Base）</strong></p> </th> 
   <th><p><strong>サポートされているパッチ定義</strong></p> </th> 
  </tr> 
  <tr> 
   <td>Acrobat 2017（クラシックトラック）</td> 
   <td>バージョン 17.011.30078 以降<br /> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Acrobat DC Product Family では、基本的に別々の製品である Acrobat と Reader のそれぞれに、「クラシック」と「継続」の 2 種類のトラックが用意されています。2つのトラックの詳細と比較については、[https://www.adobe.com/go/acrobatdctracksを参照してください。](https://www.adobe.com/go/acrobatdctracks)

### ブラウザー {#browsers}

#### デスクトップ {#desktops}

<table> 
 <tbody> 
  <tr> 
   <th><p><strong>ブラウザー（ベース）</strong></p> </th> 
   <th><p><strong>サポートレベル</strong></p> </th> 
   <th><p><strong>サポートされているパッチ定義</strong></p> </th> 
  </tr> 
  <tr> 
   <td><p>Microsoft Edge</p> </td> 
   <td><p>A：サポート対象</p> </td> 
   <td><p>サービスパックとアップデート</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox 45.x</p> </td> 
   <td><p>A：サポート対象</p> </td> 
   <td><p>すべてのアップデート</p> </td> 
  </tr> 
  <tr> 
   <td><p>Google Chrome 46 以降</p> </td> 
   <td><p>A：サポート対象</p> </td> 
   <td><p>すべてのアップデート</p> </td> 
  </tr> 
  <tr> 
   <td>Apple Safari 11.x</td> 
   <td>A：サポート対象</td> 
   <td>すべてのアップデート</td> 
  </tr> 
  <tr> 
   <td><p>Google Chrome および Firefox（MAC OS X 上）</p> </td> 
   <td><p>A：サポート対象</p> </td> 
   <td><p>すべてのアップデート</p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>以下にデスクトップに対する一部のブラウザー関連の例外事項を示します。
>
>* 多くの最新のブラウザーは現在、NPAPI ベースのプラグインをサポートしていません。このプラグインがAEM Formsのアプリケーションやワークフローに与える影響について詳しくは、[NPAPIブラウザープラグインのサポート終了とその影響](https://helpx.adobe.com/jp/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html)を参照してください。
>* Safari は Macintosh OS X でのみサポートされています。


#### モバイルクライアント {#mobile-clients}

<table> 
 <tbody> 
  <tr> 
   <th><p><strong>ブラウザー（ベース）</strong></p> </th> 
   <th><p><strong>サポートされているパッチ定義</strong></p> </th> 
  </tr> 
  <tr> 
   <td><p>Chrome on Android™ 4.1.2 以降</p> </td> 
   <td><p>すべてのアップデート</p> </td> 
  </tr> 
  <tr> 
   <td>Safari（iOS 11.0 以降）</td> 
   <td>すべてのアップデート</td> 
  </tr> 
  <tr> 
   <td>Windows 10 上の Internet Explorer</td> 
   <td>すべてのアップデート</td> 
  </tr> 
  <tr> 
   <td>Microsoft Edge<br /> </td> 
   <td>すべてのアップデート<br /> </td> 
  </tr> 
  <tr> 
   <td>ネイティブの Andriod ブラウザー（Android™ 4.4 以降で稼働するブラウザー）</td> 
   <td>すべてのアップデート</td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>* Forms Portal は iPad の Safari でのみサポートされています。

>



### AEM Forms アプリケーション {#aem-forms-workspace-app}

#### モバイルデバイスのサポート {#mobile-device-support}

AEM Forms アプリケーションは次のプラットフォームで利用可能です。

| **プラットフォーム** | **サポートされているデバイス** |
|---|---|
| Apple iOS 以上 | Apple iPhone、iPad、iPad Air、iPad mini [iOS 11以降] |
| Google Android | Android 4.4 (Android Kit Kat)以降、*[APIレベル19以降]*。 AEM Formsアプリは、7インチと10インチのSamsung Galaxyタブレット、7インチのGoogle Nexusタブレット、人気スマートフォンで認定されています。 |
| Microsoft Windows | Microsoft Windows 10オペレーティングシステムを実行するMicrosoft Surfaceデバイス、タブレット、ノートパソコン、およびデスクトップ。 |

### Adobe Flash Player {#adobe-flash-player}

<table> 
 <tbody> 
  <tr> 
   <th><p><strong>Flash Player（ベース）</strong></p> </th> 
   <th><p><strong>サポートされているパッチ定義</strong></p> </th> 
  </tr> 
  <tr> 
   <td><p>Flash Player 最新版</p> </td> 
   <td><p>マイナーバージョンとアップデート</p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Adobeは、2020](https://theblog.adobe.com/adobe-flash-update/)の終わりにFlash Playerの更新と配布を[停止します。

### Adobe Document Security Extension for Microsoft Office {#adobe-rights-management-extension-for-microsoft-office}

Adobe Document Security Extension for Microsoft® Office の必要システム構成を見るには、[ここ](https://www.adobe.com/jp/products/livecycle/rightsmanagement/extension/downloads.html)をクリックしてください。

### クライアントサポートの例外事項 {#exceptions-to-client-support}

Microsoft® Windows® 2012 は、Reader および Acrobat 以外は、指定されたすべてのクライアント側のソフトウェアに対してサポートされていません。

また、JEE 上の AEM Forms では、指定されたメジャーおよびマイナーバージョンのサポートソフトウェアに対して、アップデート、パッチ、および修正パックもサポートしています。ただし、次のメジャーまたはマイナーバージョンに対するアップデートは、とくに記載がない限りサポートされていません。

## サードパーティパッチサポートポリシー  {#third-party-patch-support-policy}

JEE 上の AEM Forms のサードパーティソフトウェアの必要システム構成は、それぞれの製品ドキュメントの「必要システム構成」セクションに記述されています。すべてのドキュメントは、[https://adobe.com/go/learn_aemforms_documentation_64](https://adobe.com/go/learn_aemforms_documentation_64)からアクセスできます。

JEE 上の AEM Forms のサードパーティリファレンスプラットフォームは、JEE 上の AEM Forms の開発とリリースの時点におけるサードパーティインフラストラクチャの特定のパッチレベルを記述してあり、そのバージョンの JEE 上の AEM Forms によってサポートされているインフラストラクチャの最小パッチ/サービスパックレベルを形成しています。

アドビシステムズ社では、サードパーティベンダーがリリース時に JEE 上の AEM Forms がサポートするバージョンとの後方互換性を保証していると仮定して、サードパーティベンダーの緊急および推奨パッチをサポートします。アドビシステムズ社は、JEE 上の AEM Forms ドキュメントに記載の最小パッチレベル後にリリースされたパッチのみをサポートします。

場合によっては、アドビシステムズ社は、主要な機能を変更しそのために完全な後方互換性をサポートしなくなったサードパーティアップデートをサポートしません。サポートされているアップデートの詳細については、「[サポートされているパッチ定義](https://helpx.adobe.com/jp/aem-forms/aem-forms-third-party-software-patch.html)」で、特定のベンダー製品とパッチタイプAdobeがサポートしているパッチを参照してください。

アドビシステムズ社の管理の及ばない状況においては、後方互換性を主張しているサードパーティ製パッチは、アドビ製品またはお客様の環境に悪い影響を及ぼす可能性があります。このような場合、アドビシステムズ社は、お客様がサードパーティからの緊急パッチを重要なシステムに適用する前にその影響を評価することを推奨します。アドビシステムズ社はサードパーティと共に妥当なビジネス努力を払って、通常のアドビサポートプログラムを通してあるいはサードパーティがパッチの問題を修正することによって、そのような問題を解決します。このことは、アドビによってサポートされる新たにリリースされたサードパーティ製パッチが、ベンダーによってマニュアルに記載されているようにまたは JEE 上の AEM Forms と機能することを保証するものではありません。

アドビシステムズ社は、任意の時点で、JEE 上の AEM Forms リリースおよびそれらのサポートされているパッチ定義によってサポートされているサードパーティリファレンスプラットフォームを変更する権利を保留します。

サードパーティ製パッチのその他の情報については、Adobe Enterprise Support サイトで、ご使用の製品に関するナレッジベース記事を検索することによっても見つけられることがあります。

[**サポートへのお問い合わせ**](https://www.adobe.com/account/sign-in.supportportal.html)
