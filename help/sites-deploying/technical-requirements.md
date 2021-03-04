---
title: 技術要件
seo-title: 技術要件
description: AEM でサポートされているクライアントおよびサーバーのプラットフォームのリスト。
seo-description: AEM でサポートされているクライアントおよびサーバーのプラットフォームのリスト。
uuid: d5bdcd41-3585-41f7-860d-8068a2931a72
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: platform
discoiquuid: 4d3c4650-3e2a-43b1-ad2d-8d0ae2254ca9
translation-type: tm+mt
source-git-commit: 95b5e70c1b474d4d207a5a33e8d1ab8ef39685b6
workflow-type: tm+mt
source-wordcount: '3272'
ht-degree: 82%

---


# 技術要件{#technical-requirements}

アドビは、このドキュメントの以下の情報に記載されているプラットフォームで Adobe Experience Manager（AEM）をサポートしています。

プラットフォーム自体に関連する問題については、プラットフォームのベンダーに直接お問い合わせください。

>[!NOTE]
>
>AEM をインストールするプラットフォームによっては、別のユーザー管理要件が適用される場合があります。

## 前提条件 {#prerequisites}

Adobe Experience Manager をインストールするための最小要件：

* Java Platform, Standard Edition JDK（またはその他のサポート対象の[Java仮想マシン](#java-virtual-machines)）
* Experience Manager Quickstart ファイル（スタンドアロン JAR または Web アプリケーションデプロイメント WAR）

### 最小サイズ要件 {#minimum-sizing-requirements}

Adobe Experience Managerを走らせるための最小要件：

* 5 GB の空きディスク領域（インストールディレクトリ内）
* 2 GB メモリ

>[!NOTE]
>
>* デジタルアセットを使用する場合は、より多くの基本メモリが必要になります。詳しくは、[デプロイおよびメンテナンス](/help/sites-deploying/deploy.md#default-local-install)を参照してください。
>* [AEM Forms アドオンパッケージ](/help/forms/using/installing-configuring-aem-forms-osgi.md)には 15 GB の一時領域が必要です。

>



詳細は、[ハードウェアサイズのガイドライン](/help/managing/hardware-sizing-guidelines.md)を参照してください。

### サポートレベル {#support-levels}

ここでは、Adobe Experience Manager でサポートされているクライアントおよびサーバープラットフォームを示します。アドビは、推奨構成とその他の構成の両方について、複数のレベルのサポートを提供しています。

### サポートされる構成 {#supported-configurations}

アドビは以下の構成を推奨し、標準ソフトウェア保守契約の一環として完全なサポートを提供しています。

<table> 
 <tbody> 
  <tr> 
   <td>サポートレベル</td> 
   <td>説明<br /> </td> 
  </tr> 
  <tr> 
   <td><strong>A：サポート対象</strong></td> 
   <td>アドビはこの構成への完全なサポートと保守を提供します。この構成は、アドビの品質保証プロセスでカバーされます。</td> 
  </tr> 
  <tr> 
   <td><strong>R：制限サポート</strong></td> 
   <td>顧客のプロジェクト成功のために、アドビは、制限されたサポートプログラムの範囲内で完全なサポートを提供します。このサポートプログラムでは、特定の条件を満たす必要があります。R レベルのサポートでは、顧客からの正式な依頼とアドビによる承認が必要です。詳しくは、アドビカスタマーケアまでお問い合わせください。</td> 
  </tr> 
 </tbody> 
</table>

### サポートされていない構成 {#unsupported-configurations}

| サポートレベル | 説明 |
|---|---|
| **Z：サポート対象外** | この構成はサポートされません。アドビは、この構成が動作するかどうかに関する一切の表明をせず、この構成をサポートしません。 |

## サポートされているプラットフォーム {#supported-platforms}

### Java Virtual Machines {#java-virtual-machines}

このアプリケーションの実行には、Java 仮想マシンが必要です。Java 仮想マシンは、Java Development Kit（JDK）ディストリビューションによって提供されます。

Adobe Experience Manager は、次のバージョンの Java 仮想マシンで動作します。

>[!CAUTION]
>
>Java ベンダーが発表するセキュリティ情報を常に確認し、実稼動環境の安全性とセキュリティを確保すること、および最新の Java 更新プログラムをインストールすることを推奨します。

<table> 
 <tbody> 
  <tr> 
   <td>プラットフォーム</td> 
   <td>サポートレベル<br /> </td> 
  </tr> 
  <tr> 
   <td>Oracle Java SE 11 JDK [1]</td> 
   <td>Z：サポート対象外 </td> 
  </tr> 
  <tr> 
   <td>Oracle Java SE 10 JDK [1]</td> 
   <td>Z：サポート対象外 </td> 
  </tr> 
  <tr> 
   <td>Oracle Java SE 9 JDK [1]</td> 
   <td>Z：サポート対象外</td> 
  </tr> 
  <tr> 
   <td><strong>Oracle Java SE 8 JDK - 64 ビット</strong></td> 
   <td>A：サポート対象 [3]<br /> </td> 
  </tr> 
  <tr> 
   <td>IBM J9 VM - ビルド 2.9、JRE 1.8.0 [2]</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>IBM J9 VM - ビルド 2.8、JRE 1.8.0 [2]</td> 
   <td>A：サポート対象</td> 
  </tr> 
 </tbody> 
</table>

1. Oracle は Oracle Java SE 製品の「長期サポート」（LTS）モデルに移行しました。Java 9および10は、Oracle別にLTS以外のリリースです([OracleJava SEサポート・ロードマップ](https://www.oracle.com/technetwork/java/eol-135779.html)を参照)。 アドビでは、AEM を実稼働環境で実行するための Java については、LTS リリース版のみサポートします。

1. IBM JRE は、WebSphere Application Server とともに使用する場合にのみサポートされます。
1. パブリックアップデート終了後の LTS リリースのすべてのメンテナンスアップデートを含む Oracle Java SE JDK のサポートと配布が、アドビによって直接サポートされます。対象となるのは、Oracle Java SE テクノロジーを利用しているすべての AEM ユーザーです。詳しくは、[OracleのJavaサポート(Adobe Experience ManagerQ&amp;A](assets/adobe-oracle-java-license-agreement.pdf))を参照してください。

### ストレージと永続性 {#storage-persistence}

Adobe Experience Manager のリポジトリのデプロイには、様々なオプションがあります。サポートされるテクノロジーとストレージオプションについては、以下のリストを参照してください。

<table> 
 <tbody> 
  <tr> 
   <td><strong>プラットフォーム</strong></td> 
   <td><strong>説明</strong></td> 
   <td><strong>サポートレベル</strong></td> 
  </tr> 
  <tr> 
   <td><strong>TAR ファイルを使用したファイルシステム [1]</strong></td> 
   <td>リポジトリ</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td><strong>データストア[1]を持つファイルシステム</strong></td> 
   <td>バイナリ</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>ファイルシステムの TAR ファイルへのバイナリの格納 [1]</td> 
   <td>バイナリ</td> 
   <td>Z：実稼動環境ではサポート対象外</td> 
  </tr> 
  <tr> 
   <td>Amazon S3</td> 
   <td>バイナリ</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Microsoft Azure Blob Storage</td> 
   <td>バイナリ</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>MongoDB Enterprise 3.6 [5, 6]</td> 
   <td>リポジトリ</td> 
   <td>A: 制限付きサポート</td> 
  </tr> 
  <tr> 
   <td>MongoDB Enterprise 3.4 [2, 3, 6]</td> 
   <td>リポジトリ</td> 
   <td>A: 制限付きサポート</td> 
  </tr> 
  <tr> 
   <td>MySQL 5.7</td> 
   <td>Forms データベース</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>IBM DB2 11.1<br /> </td> 
   <td>Forms データベース</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>IBM DB2 10.5</td> 
   <td>リポジトリおよび Forms データベース</td> 
   <td>R：制限サポート（4）</td> 
  </tr> 
  <tr> 
   <td>Oracleデータベース12c(12.1.x)</td> 
   <td>リポジトリおよび Forms データベース</td> 
   <td>R：制限サポート</td> 
  </tr> 
  <tr> 
   <td>Microsoft SQL Server 2017</td> 
   <td>Forms データベース</td> 
   <td>Z:非対応(4)</td> 
  </tr> 
  <tr> 
   <td>Microsoft SQL Server 2016</td> 
   <td>Forms データベース</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Microsoft SQL Server 2014</td> 
   <td>Forms データベース</td> 
   <td>R：制限サポート（4）</td> 
  </tr> 
  <tr> 
   <td><strong>Apache Lucene（クイックスタート組み込み）</strong></td> 
   <td>検索サービス</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Apache Solr</td> 
   <td>検索サービス</td> 
   <td>A：サポート対象</td> 
  </tr> 
 </tbody> 
</table>

1. 「ファイルシステム」には、POSIX 準拠のブロックストレージが含まれます。ブロックストレージには、ネットワークストレージテクノロジーが含まれます。ファイルシステムのパフォーマンスが状況に応じて変化し、全体的なパフォーマンスに影響を及ぼす可能性があることに注意してください。ネットワークやリモートファイルシステムと一緒に AEM の負荷テストを行うことを推奨します。
1. MongoDB Sharding は AEM ではサポートされていません。
1. MongoDB Storage Engine WiredTiger のみサポートされています。
1. AEM Forms ではサポートされていません。
1. MongoDB Enterprise 3.6 は、AEM バージョン 6.4.2.0 以降でサポートされます。
1. MongoDB 3.4のサポートは終了(EOL)に達し、MongoDB 3.6は2021年4月30日にEOLに到達する予定です。 今後、AEM製品に関する問題に対しては、Adobeがサポートを提供するだけになることに注意してください。

>[!NOTE]
>
>AEM コミュニティの機能について詳しくは、[コミュニティのデプロイ](/help/communities/deploy-communities.md)を参照してください。

>[!NOTE]
>
>MongoDB はサードパーティソフトウェアであり、AEM ライセンスパッケージには含まれていません。詳しくは、[MongoDB のライセンスポリシー](https://www.mongodb.org/about/licensing/)ページを参照してください。
>
>MongoDB を利用した AEM デプロイメントを最大限活用するために、アドビは、プロフェッショナルサポートを受けられる MongoDB Enterprise バージョンのライセンスを取得することを推奨しています。詳しくは、[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)を参照してください。
>
>このライセンスには、標準レプリカセットが含まれます。このレプリカセットは、1 つのプライマリインスタンスと 2 つのセカンダリインスタンスで構成されており、これらのインスタンスは、オーサーとパブリッシュのいずれのデプロイメントにも使用できます。
>
>MongoDB でオーサーとパブリッシュの両方を実行したい場合は、個別の 2 つのライセンスを購入する必要があります。
>
>アドビカスタマーケアは、AEM での MongoDB の使用に関する問題の絞り込みを支援します。
>
>詳しくは、[MongoDB for Adobe Experience Manager のページ](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。

>[!NOTE]
>
>上記のサポート対象リレーショナルデータベースはサードパーティソフトウェアであり、AEM ライセンスパッケージには含まれていません。
>
>サポート対象リレーショナルデータベースを使用して AEM 6.4 を実行するには、別途データベースベンダーとサポート契約を締結する必要があります。アドビカスタマーケアは、リレーショナルデータベースを AEM 6.4 で利用することに関連する問題の絞り込みを支援いたします。
>
>**AEM 6.4 では現在、ほとんどのリレーショナルデータベースがレベル R の範囲でサポートされ、前述のレベル R の説明にあるサポートの基準とサポートプログラムが適用されます。**

### サーブレットエンジン／アプリケーションサーバー  {#servlet-engines-application-servers}

Adobe Experience Manager はスタンドアロンサーバー（quickstart JAR ファイル）として実行することも、サードパーティのアプリケーションサーバー内の Web アプリケーション（WAR ファイル）として実行することもできます。

必要な Servlet API バージョンは Servlet 3.1 以上、Servlet 4.0 未満です。

| プラットフォーム | サポートレベル |
|---|---|
| **Quickstart 組み込みサーブレットエンジン（Jetty 9.3）** | A：サポート対象 |
| Oracle WebLogic Server 12.2（12cR2） | A：サポート対象 |
| IBM WebSphere Application Server Continuous Delivery（LibertyProfile）（Web Profile 7.0 および IBM JRE 1.8） | A：サポート対象 |
| IBM WebSphere Application Server 9.0 | A：サポート対象 |
| Apache Tomcat 8.5.x | A：サポート対象 |
| JBoss EAP 7.1.0 と JBoss Application Server | A：サポート対象（1） |
| JBoss EAP 7.0.0 と JBoss Application Server | A：サポート対象 |

1. AEM Forms ではサポートされていません。

### サーバーオペレーティングシステム {#server-operating-systems}

Adobe Experience Manager は次のサーバープラットフォームで動作します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>プラットフォーム</strong></td> 
   <td><strong>サポートレベル</strong></td> 
  </tr> 
  <tr> 
   <td><strong>Linux、Red Hat ディストリビューションベース</strong></td> 
   <td>A：サポート対象（1）</td> 
  </tr> 
  <tr> 
   <td>Linux、Debian ディストリビューションベース（Ubuntu を含む）</td> 
   <td>A：サポート対象（4）</td> 
  </tr> 
  <tr> 
   <td>Linux、SUSE ディストリビューションベース</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Microsoft Windows Server 2016</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Microsoft Windows Server 2012 R2</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Oracle Solaris 11</td> 
   <td>A：制限付きでサポート（3、5、7）<br />R：新規契約では制限サポート</td> 
  </tr> 
  <tr> 
   <td>IBM AIX 7.2</td> 
   <td>A：制限付きでサポート（2、5、7）<br />R：新規契約では制限サポート</td> 
  </tr> 
 </tbody> 
</table>

1. Linux Kernel 2.6、3.x、4.xには、Red Hat Enterprise Linux、CentOS、OracleLinux、AmazonLinuxなど、Red Hatディストリビューションの派生物が含まれています。 AEM Formsのアドオン機能は、CentOS 7およびRed Hat Enterprise Linux 7でのみサポートされています。
1. AEM Assets：[XMP メタデータの書き戻しのサポート](#requirements-for-aem-assets-xmp-metadata-write-back)の節を参照してください。
1. AEM Assets：Dynamic Media 画像はサポートされていません。Dynamic Media ビデオはサポートされています。
1. AEM Forms は Ubuntu 16.04 LTS でのみサポートされています。
1. AEM Assets：[Raw ファイル変換](/help/assets/camera-raw.md)はサポートされていません。
1. AEM Forms：実稼動環境はサポートされていません。
1. AEM Assets：[拡張 PDF ラスタライザ](/help/assets/aem-pdf-rasterizer.md)はサポートされていません。
1. AEM Forms：サポート対象外

### 仮想／クラウドコンピューティング環境 {#virtual-cloud-computing-environments}

Microsoft Azure や Amazon Web Services（AWS）など、クラウドコンピューティング環境の仮想マシンでの Adobe Experience Manager の稼動は、このページに記載されている技術要件およびアドビの標準サポート条件に従ってサポートされています。

AEM を Azure または AWS にデプロイする場合は、Adobe Managed Services を使用することをお勧めします。Adobe Managed Services を使用することで、これらのクラウドコンピューティング環境での AEM のデプロイと運用の経験とスキルを持つエキスパートのサポートを活用できます。[Adobe Managed Services に関するドキュメント](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)も参照してください。

AEM を Azure や AWS にデプロイするその他あらゆる場合、またはその他のクラウドコンピューティング環境にデプロイする場合、アドビによるサポートは、このページに記載されている技術仕様に従って、仮想コンピューティング環境に対して提供されます。これらのクラウド環境で実行される AEM に関連する問題を報告する場合は、その問題が、クラウドコンピューティング環境に固有のクラウドサービスと関係なく再現可能である必要があります。ただし、クラウドサービスが、このページに記載されている技術要件の一部として特別にサポートされている場合は除きます（Azure Blob ストレージ、AWS S3 など）。

Adobe Managed Services の外部で Azure または AWS に AEM をデプロイする場合は、クラウドプロバイダーまたは使用するクラウド環境への AEM のデプロイメントをサポートするパートナーと直接共同作業することを強くお勧めします。選択したクラウドプロバイダーまたはパートナーは、アーキテクチャのサイズ仕様、設計および実装を担当し、顧客独自のパフォーマンス、負荷、スケーラビリティおよびセキュリティの要件が満たされるように支援します。

### Dispatcher のプラットフォーム（Web サーバー）  {#dispatcher-platforms-web-servers}

Dispatcher は、キャッシュおよびロードバランシングコンポーネントです。[最新バージョンのDispatcherをダウンロードします](https://helpx.adobe.com/jp/experience-manager/dispatcher/release-notes.html)。Experience Manager 6.4 ではバージョン 4.3.1 以降の Dispatcher が必要です。

Dispatcher バージョン 4.3.1 で使用する場合は、次の Web サーバーがサポートされています。

| プラットフォーム | サポートレベル |
|---|---|
| **Apache httpd 2.4.x** （下記の1,2も参照） | A：サポート対象 |
| Microsoft IIS 10（Internet Information Server） | A：サポート対象 |
| Microsoft IIS 8.5（Internet Information Server） | A：サポート対象 |

1. Apache httpd のソースコードをベースとして構築された Web サーバーは、ベースとした httpd のバージョンと同じサポートレベルでサポートされます。これらに当てはまるか不明の場合は、アドビに問い合わせて、それぞれのサーバー製品に関するサポートレベルを確認してください。次の場合：

   1. HTTP サーバーが公式の Apache ソースディストリビューションのみを使用して構築されている。または、
   1. HTTP サーバーが実行中のオペレーティングシステムの一部として配布されている。例：IBM HTTP Server、Oracle HTTP Server

1. Dispatcher は、Windows オペレーティングシステム版の Apache 2.4.x ではサポートされていません。

## サポートされているクライアントプラットフォーム  {#supported-client-platforms}

### オーサリングユーザーインターフェイス向けにサポートされているブラウザー {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager ユーザーインターフェイスは次のクライアントプラットフォームで動作します。すべてのブラウザーは、デフォルトのプラグインおよびアドインのセットを使用してテストされています。

AEM のユーザーインターフェイスは、大きめの画面（通常はノートブックまたはデスクトップコンピューター）およびタブレットフォームファクター（Apple iPad、Microsoft Surface など）に向けて最適化されています。携帯電話のフォームファクターはサポートされていません。

>[!NOTE]
>
>**リリースサイクルの短いブラウザーのサポート**
>
>Mozilla Firefox、Google Chrome および Microsoft Edge では、数ヶ月ごとに更新プログラムがリリースされます。アドビは、これらのブラウザーの今後のバージョンで以下に示したサポートレベルを維持するために、Adobe Experience Manager の更新プログラムを提供します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>ブラウザー</strong></td> 
   <td><strong>UI のサポート<br /> </strong></td> 
   <td><strong>クラシック UI のサポート</strong></td> 
  </tr> 
  <tr> 
   <td><strong>Google Chrome（エバーグリーン）</strong></td> 
   <td>A：サポート対象</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Microsoft Edge（エバーグリーン）</td> 
   <td>A：サポート対象</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Microsoft Internet Explorer 11</td> 
   <td>A：サポート対象</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Mozilla Firefox（エバーグリーン）</td> 
   <td>A：サポート対象</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Mozilla Firefox 最新 ESR [1]</td> 
   <td>A：サポート対象</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Apple Safari 12.x（macOS）</td> 
   <td>A：サポート対象</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Apple Safari 11.x（macOS）</td> 
   <td>A：サポート対象</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Apple Safari 10.x（macOS）</td> 
   <td>A：サポート対象</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Apple Safari（iOS 12.x）</td> 
   <td>A：サポート対象 [2]</td> 
   <td>Z：サポート対象外</td> 
  </tr> 
  <tr> 
   <td>Apple Safari （iOS 11.x）</td> 
   <td>A：サポート対象 [2]</td> 
   <td>Z：サポート対象外</td> 
  </tr> 
  <tr> 
   <td>Apple Safari（iOS 10.3）</td> 
   <td>A：サポート対象 [2]</td> 
   <td>Z：サポート対象外</td> 
  </tr> 
 </tbody> 
</table>

1. Firefox の延長サポート版（ESR）。[詳しくは、mozilla.org を参照してください。](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. Apple iPad のサポート。

### Web サイト向けにサポートされているブラウザー  {#supported-browsers-for-websites}

一般的に、AEM Sites でレンダリングされる Web サイトのブラウザーサポートは、AEM ページテンプレート、デザイン、コンポーネント出力の実装に依存するので、これらの部品を実装する団体によって管理されます。

### WebDAV クライアント  {#webdav-clients}

**Microsoft Windows 7 以降**

Microsoft Windows 7 以降を使用して、SSL で保護されていない AEM インスタンスに正常に接続するには、保護されていないネットワーク上での基本認証を Windows で有効にする必要があります。そのためには、Web クライアントの Windows レジストリを次のように変更する必要があります。

1. 次のレジストリのサブキーを探します。

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. このサブキーに 2 以上の値を使用して、BasicAuthLevel レジストリエントリを追加します。

詳しくは、[Microsoft Support KB 841215](https://support.microsoft.com/default.aspx/kb/841215) を参照してください。

Windows で WebDav クライアントの応答性を改善する方法については、[Microsoft Support KB 2445570](https://support.microsoft.com/kb/2445570) を参照してください。

## プラットフォームに関するその他の注意点  {#additional-platform-notes}

ここでは、Adobe Experience Manager およびそのアドオンの実行に関する注意点や詳細情報を説明します。

### IPv4 と IPv6  {#ipv-and-ipv}

Adobe Experience Manager のすべての要素（インスタンス、Dispatcher）は、IPv4 と IPv6 のいずれのネットワークにもインストールできます。

特別な設定は不要で、シームレスに運用できます。必要に応じて、使用するネットワークの種類に適した形式を使用して IP アドレスを指定できます。

つまり、IP アドレスを指定する必要がある場合には、次の形式から（必要に応じて）選択できます。

* IPv6アドレス

   例：`https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4アドレス

   例：`https://123.1.1.4:4502`

* サーバー名

   例：`https://www.yourserver.com:4502`

* `localhost`のデフォルトのケースは、IPv4とIPv6の両方のネットワークインストールに対して解釈されます

   例：`http://localhost:4502`

### AEM Dynamic Media アドオンの要件 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media はデフォルトで無効になっています。[Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media)を有効にするを参照してください。

Dynamic Mediaを有効にすると、次の追加の必要システム構成が適用されます。
>[!NOTE]
>
>以下のシステム要件は、Dynamic Media — ハイブリッドモードを使用する場合は&#x200B;**__**&#x200B;のみが適用されます。Dynamic Media — ハイブリッドモードには埋め込みイメージサーバがあり、このサーバは特定のオペレーティングシステムでのみ認証されています。
>
>Dynamic Media - Scene7 モード（**dynamicmedia_scene7** 実行モード）で Dynamic Media を実行する場合は、追加のシステム要件はありません。AEM と同じシステム要件が適用されます。Dynamic Media - Scene7 モードのアーキテクチャはクラウドベースの画像サービスを使用しており、AEM に組み込まれたサービスを使用していません。

#### ハードウェア {#hardware}

以下のハードウェア要件は、LinuxとWindowsの両方のオペレーティングシステムに適用されます。

* Intel Xeon または AMD Opteron CPU（4 コア以上）
* 16 GB 以上の RAM

#### Linux {#linux}

LinuxでDynamic Mediaを使用する場合は、次の前提条件が必要です。

* RedHat Enterprise 7 または CentOS 7 以降（最新の修正パッチを適用）
* 64 ビットのオペレーティングシステム
* スワッピング無効（推奨）
* SELinux 無効（以下の注意を参照）

>[!NOTE]
>
>LC_CTYPE（ロケール）が en_US.UTF-8 以外に設定されている場合、Dynamic Media は機能しません。値を確認するには、コマンドプロンプトで「locale」と入力します。設定が異なっている場合は、AEM を実行する前に「export LC_CTYPE=」と入力して、LC_CTYPE 環境変数を空の文字列に設定します。

>[!NOTE]
>
>**SELinux の無効化：**&#x200B;画像サービングは、SELinux が有効の場合は動作しません。このオプションはデフォルトで有効です。この問題を修正するには、**/etc/selinux/config** ファイルを編集し、SELinux 値を次のように変更します。
>
>`SELINUX=enforcing`コピー先：`SELINUX=disabled`

>[!NOTE]
>
>**NUMA アーキテクチャ：** AMD64 および Intel EM64T のプロセッサーを搭載したシステムは、通常は NUMA プラットフォームとして構成されます。このようなプラットフォームでは、カーネルにより、1 つのメモリノードではなく複数のメモリノードがブート時に作成されます。
>
>複数のノードを作成することで、他のノードが使い果たされる前に 1 つ以上のノードでメモリが枯渇する場合があります。メモリの枯渇が発生した場合、カーネルは、空きメモリがあってもプロセス（Image Server、Platform Server など）を強制終了することがあります。
>
>そのため、そのようなシステムを実行している場合は、**numa=off** ブートオプションを使用して NUMA をオフにし、カーネルによるこれらのプロセスの強制終了を防ぐことをお勧めします。

>[!NOTE]
>
>**サーバーのホスト名は解決可能である必要がある：**&#x200B;サーバーのホスト名が IP アドレスに解決できることを確認してください。解決できない場合は、完全修飾ホスト名と IP アドレスを **/etc/hosts** に次のように追加してください。
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* 物理メモリ（RAM）の 2 倍以上のスワップ領域

WindowsでDynamic Mediaを使用するには、x64およびx86用のMicrosoft Visual Studio 2010、2013および2015再頒布可能パッケージをインストールする必要があります。

x64

* Microsoft Visual Studio 2010の再配布可能なファイルは、[https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/ja-jp/download/details.aspx?id=13523)にあります。
* Microsoft Visual Studio 2013の再配布可能なファイルは、[https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/ja-jp/download/details.aspx?id=40784)にあります。
* Microsoft Visual Studio 2015の再配布可能なファイルは、[https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/ja-jp/download/details.aspx?id=48145)にあります。

x86

* Microsoft Visual Studio 2010の再配布可能なファイルは、[https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/ja-jp/download/details.aspx?id=5555)にあります。
* Microsoft Visual Studio 2013の再配布可能なファイルは、[https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)にあります。
* Microsoft Visual Studio 2015の再配布可能なファイルは、[https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/ja-jp/download/details.aspx?id=52685)にあります。

#### MacOS {#macos}

* 10.9.x 以降
* 試用およびデモの目的でのみサポート

### AEM Forms PDF Generator の要件  {#requirements-for-aem-forms-pdf-generator}

<table> 
 <tbody> 
  <tr> 
   <th><p><strong>製品</strong></p> </th> 
   <th><p><strong>PDF への変換でサポートされている形式</strong></p> </th> 
  </tr> 
  <tr> 
   <td><p><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 クラシックトラック</a></p> </td> 
   <td><p>XPS、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC）、HTML、HTM、DWG、DXF、DWF</p> </td> 
  </tr> 
  <tr> 
   <td>Microsoft® Project 2016</td> 
   <td>MPP</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Publisher 2016</td> 
   <td>PUB</td> 
  </tr> 
  <tr> 
   <td>Microsoft® Office Visio 2016</td> 
   <td>VSD</td> 
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
   <td>Corel WordPerfect X7</td> 
   <td>WP、WPD<br /> </td> 
  </tr> 
  <tr> 
   <td>OpenOffice 4.1.2</td> 
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLSX、DOC、DOCX、PPT、PPTX、画像形式(BMP、JPEG、JPG、TIF、TIFF、TIFF)JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、およびTXT</td> 
  </tr> 
  <tr> 
   <td><p>OpenOffice 3.4</p> </td> 
   <td><p>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLSX、DOC、DOCX、PPT、PPTX、画像形式(BMP、JPEG、JPG、TIF、TIFF、TIFF)JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、およびTXT</p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>PDF Generator では、英語、フランス語、ドイツ語および日本語版のサポート対象のオペレーティングシステムとアプリケーションのみがサポートされます。
>
>さらに、次の点に注意してください。
>
>* PDF Generator で変換を実行するには、[Acrobat 2017 クラシックトラックバージョン 17.011.30078 以降](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html)が必要です。
>* AEM Forms では、32 ビットエディションのサポート対象ソフトウェアのみがサポートされます。
>* OCR PDF（検索可能な PDF）、PDF の最適化および PDF の書き出しの機能は、Microsoft Windows でのみサポートされます。
>* HTML2PDF サービスは AIX で終了しています。
>* OpenOffice 用 PDF Generator 変換は、Windows、Linux および Solaris でのみサポートされます。
>* OCR PDF、PDF を最適化および PDF を書き出しの機能は、Windows でのみサポートされます。
>* Acrobat のバージョンは、PDF Generator 機能を有効にするために、AEM Forms にバンドルされます。バンドルされたバージョンは、AEM Forms PDF Generator で使用するために、AEM Forms ライセンスの期間中、AEM Forms でのみプログラムによってアクセスされます。詳細については、ご使用の導入環境に応じて、AEM Forms製品の説明([オンプレミス](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)または[Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))を参照してください。&quot;

>



### AEM Formsデザイナーの要件{#requirements-for-aem-forms-designer}

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

### AEM Assets の XMP メタデータの書き戻しの要件 {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP の書き戻しは次のプラットフォームおよびファイル形式でサポートされ、有効にされます。

**オペレーティングシステム**

* Linux（32 ビット、64 ビットシステムでは 32 ビットアプリケーションのサポートが必要）。32ビットのクライアントライブラリをインストールする手順については、[How to enable XMP抽出 and write-back on 64ビットのRedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)を参照してください。

* Windows Server
* Oracle Solaris
* Mac OS X（64 ビット）

**ファイル形式**

* JPEG
* PNG
* TIFF
* PDF
* INDD
* AI
* EPS

### AEM Screens Player の要件  {#requirements-for-aem-screens-player}

AEM Screens Player バージョン 3.3.x では、次のオペレーティングシステムをサポートしています。

* Microsoft Windows 10 Enterprise LTSB
* Google Chome OS 62 以上
* Google Android 5.1.1とAndroidシステムWebViewバージョン52以降の更新
* Apple iOS 10.3 以上
* Apple macOS 10.12 以上
