---
title: 技術要件
seo-title: Technical Requirements
description: AEM でサポートされるクライアントおよびサーバープラットフォームのリスト。
seo-description: A list of the supported client and server platforms for AEM.
uuid: d5bdcd41-3585-41f7-860d-8068a2931a72
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/SITES
content-type: reference
topic-tags: platform
discoiquuid: 4d3c4650-3e2a-43b1-ad2d-8d0ae2254ca9
exl-id: 21c10b39-ca37-4085-86f8-063c30a180ed
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '3295'
ht-degree: 69%

---

# 技術要件 {#technical-requirements}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

アドビは、このドキュメントの以下の情報に記載されているプラットフォームで、Adobe Experience Manager（AEM）をサポートしています。

プラットフォーム自体に関する問題については、プラットフォームのベンダーに直接お問い合わせください。

>[!NOTE]
>
>AEM をインストールするプラットフォームに応じて、ユーザー管理に関する一連の要件が異なる場合があります。

## 前提条件 {#prerequisites}

Adobe Experience Manager をインストールするための最小要件

* Java Platform, Standard Edition JDK または他のサポートされている [Java 仮想マシン](#java-virtual-machines)がインストールされていること
* Experience Managerクイックスタートファイル（スタンドアロン JAR または Web アプリケーションデプロイメント WAR）

### 最小サイズ要件 {#minimum-sizing-requirements}

 Adobe Experience Manager を実行するための最小要件：

* 5 GB の空きディスク領域（インストールディレクトリ内）
* 2 GB メモリ

>[!NOTE]
>
>* デジタルアセットのユースケースには、より多くのベースメモリが必要です。詳しくは、「[デプロイと保守](/help/sites-deploying/deploy.md#default-local-install)」を参照してください。
>* [AEM Forms アドオンパッケージ](/help/forms/using/installing-configuring-aem-forms-osgi.md)には 15 GB の一時領域が必要です。
>


詳しくは、 [ハードウェアのサイズ設定のガイドライン](/help/managing/hardware-sizing-guidelines.md) を参照してください。

### サポートレベル {#support-levels}

このドキュメントには、Adobe Experience Manager でサポートされるクライアントおよびサーバーのプラットフォームが一覧化されています。アドビでは、推奨設定とその他の設定の両方について、複数のレベルのサポートを提供しています。

### サポートされる設定 {#supported-configurations}

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
   <td><strong>R：限定サポート</strong></td> 
   <td>お客様のプロジェクトを確実に成功させるために、アドビは特定の条件を満たす必要がある限定的なサポートプログラム内で、完全なサポートを提供します。R レベルのサポートでは、正式なお客様のリクエストとアドビの確認が必要です。詳しくは、Adobeカスタマーケアにお問い合わせください。</td> 
  </tr> 
 </tbody> 
</table>

### サポートされていない設定 {#unsupported-configurations}

| サポートレベル | 説明 |
|---|---|
| **Z：サポート対象外** | この設定はサポートされません。Adobe では、この設定が動作するかどうかに関する一切の表明をせず、この設定をサポートしません。 |

## サポートされているプラットフォーム {#supported-platforms}

### Java 仮想マシン {#java-virtual-machines}

このアプリケーションを実行するには、Java 仮想マシンが必要です。Java 仮想マシンは、Java デベロップメントキット（JDK）ディストリビューションによって提供されます。

Adobe Experience Manager は、次のバージョンの Java 仮想マシンで動作します。

>[!CAUTION]
>
>Java ベンダーが発表するセキュリティ情報を常に確認し、実稼動環境の安全性とセキュリティを確保すること、および最新の Java 更新プログラムをインストールすることを推奨します。

<table> 
 <tbody> 
  <tr> 
   <td>Platform</td> 
   <td>サポートレベル<br /> </td> 
  </tr> 
  <tr> 
   <td>OracleJava SE 11 JDK [1]</td> 
   <td>Z：サポート対象外 </td> 
  </tr> 
  <tr> 
   <td>OracleJava SE 10 JDK [1]</td> 
   <td>Z：サポート対象外 </td> 
  </tr> 
  <tr> 
   <td>OracleJava SE 9 JDK [1]</td> 
   <td>Z：サポート対象外</td> 
  </tr> 
  <tr> 
   <td><strong>Oracle Java SE 8 JDK - 64 ビット</strong></td> 
   <td>回答：サポート対象 [3]<br /> </td> 
  </tr> 
  <tr> 
   <td>IBM J9 VM — ビルド 2.9、JRE 1.8.0 [2]</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>IBM J9 VM — ビルド 2.8、JRE 1.8.0 [2]</td> 
   <td>A：サポート対象</td> 
  </tr> 
 </tbody> 
</table>

1. Oracle は Oracle Java SE 製品の「長期サポート」（LTS）モデルに移行しました。Java 9 と 10 は非 LTS リリースで、Oracle別 ( [OracleJava SE サポート・ロードマップ](https://www.oracle.com/jp/technetwork/java/eol-135779.html)) をクリックします。 Adobeでは、AEMを実稼動環境で実行するための Java の LTS リリースのみをサポートします。

1. IBM JRE は、WebSphere Application Server との組み合わせでのみサポートされます。
1. パブリックアップデート終了後の LTS リリースのすべてのメンテナンスアップデートを含む Oracle Java SE JDK のサポートと配布が、アドビによって直接サポートされます。対象となるのは、Oracle Java SE テクノロジーを利用しているすべての AEM ユーザーです。詳しくは、[Adobe Experience Manager 用 Oracle Java サポート Q&amp;A](assets/adobe-oracle-java-license-agreement.pdf) を参照してください。

### ストレージと永続性 {#storage-persistence}

Adobe Experience Manager のリポジトリをデプロイするには、様々なオプションがあります。次のリストに、サポートされるテクノロジーとストレージのオプションを示します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>プラットフォーム</strong></td> 
   <td><strong>説明</strong></td> 
   <td><strong>サポートレベル</strong></td> 
  </tr> 
  <tr> 
   <td><strong>TAR ファイルを含むファイルシステム [1]</strong></td> 
   <td>リポジトリ</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td><strong>データストア [1] を持つファイルシステム</strong></td> 
   <td>バイナリ</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>ファイルシステム [1] の TAR ファイルにバイナリを格納</td> 
   <td>バイナリ</td> 
   <td>Z：実稼動環境ではサポートされていません</td> 
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
   <td>A：サポート対象 制限あり</td> 
  </tr> 
  <tr> 
   <td>MongoDB Enterprise 3.4 [2, 3, 6]</td> 
   <td>リポジトリ</td> 
   <td>A：サポート対象 制限あり</td> 
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
   <td>リポジトリと Forms データベース</td> 
   <td>R：制限サポート (4)</td> 
  </tr> 
  <tr> 
   <td>Oracle Database 12c（12.1.x）</td> 
   <td>リポジトリと Forms データベース</td> 
   <td>R：制限サポート</td> 
  </tr> 
  <tr> 
   <td>Microsoft SQL Server 2017</td> 
   <td>Forms データベース</td> 
   <td>Z:サポート対象外 (4)</td> 
  </tr> 
  <tr> 
   <td>Microsoft SQL Server 2016</td> 
   <td>Forms データベース</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Microsoft SQL Server 2014</td> 
   <td>Forms データベース</td> 
   <td>R:制限サポート (4)</td> 
  </tr> 
  <tr> 
   <td><strong>Apache Lucene（Quickstart 組み込み）</strong></td> 
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

1. 「ファイルシステム」には、POSIX に準拠したブロックストレージが含まれます。 これには、ネットワークストレージテクノロジーが含まれます。ファイルシステムのパフォーマンスは異なり、全体的なパフォーマンスに影響を与える場合があることに注意してください。ネットワーク上またはリモートのファイルシステムと組み合わせて、テスト用 AEM を読み込むことをお勧めします。
1. MongoDB Sharding は AEM ではサポートしていません。
1. MongoDB Storage Engine WiredTiger のみがサポートされています。
1. AEM Formsではサポートされていません。
1. MongoDB Enterprise 3.6 は、AEMバージョン 6.4.2.0 以降でサポートされます。
1. MongoDB 3.4 のサポートは提供終了 (EOL) に達しましたが、MongoDB 3.6 は 2021 年 4 月 30 日に提供される予定です。 なお、Adobeでは、今後、AEM製品に関する問題に対するサポートのみが提供されることになります。

>[!NOTE]
>
>AEM Communities の機能について詳しくは、[Communities のデプロイ](/help/communities/deploy-communities.md)を参照してください。

>[!NOTE]
>
>MongoDB はサードパーティのソフトウェアで、AEM ライセンスパッケージには含まれていません。詳しくは、[MongoDB ライセンスポリシー](https://www.mongodb.org/about/licensing/)のページを参照してください。
>
>MongoDB でAEMのデプロイメントを最大限に活用するには、Adobeがプロフェッショナルサポートを受けられるように、MongoDB Enterprise バージョンのライセンスを取得することをお勧めします。 詳しくは、「[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)」を参照してください。
>
>ライセンスには、標準レプリカセットが含まれています。このセットは、1 つのプライマリインスタンスと 2 つのセカンダリインスタンスで構成され、オーサーデプロイメントまたはパブリッシュデプロイメントのどちらかに使用できます。
>
>MongoDB でオーサーとパブリッシュの両方を実行する場合は、2 つの異なるライセンスを購入する必要があります。
>
>アドビカスタマーケアは、AEM での MongoDB の使用に関する問題の絞り込みを支援します。
>
>詳しくは、[MongoDB for Adobe Experience Manager のページ](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。

>[!NOTE]
>
>サポートされる上記のリレーショナルデータベースはサードパーティのソフトウェアであり、AEM ライセンスパッケージには含まれていません。
>
>サポートされているリレーショナルデータベースでAEM 6.4 を実行するには、データベースベンダーとの別のサポート契約が必要です。 アドビカスタマーケアでは、AEM 6.4 でのリレーショナルデータベースの使用に関連する問題をサポートします。
>
>**ほとんどのリレーショナルデータベースは、現在、AEM 6.4 では Level-R 内でサポートされています。このデータベースには、上記の Level-R の説明に記載されているサポート基準とサポートプログラムが付属しています。**

### サーブレットエンジン / アプリケーションサーバー {#servlet-engines-application-servers}

Adobe Experience Managerは、スタンドアロンサーバー（quickstart JAR ファイル）として、またはサードパーティのアプリケーションサーバー（WAR ファイル）内の Web アプリケーションとして実行できます。

必要な最小サーブレット API バージョンは Servlet 3.1 ですが、Servlet 4.0 より下です。

| Platform | サポートレベル |
|---|---|
| **Quickstart 組み込みサーブレットエンジン（Jetty 9.3）** | A：サポート対象 |
| Oracle WebLogic Server 12.2（12cR2） | A：サポート対象 |
| IBM WebSphere Application Server Continuous Delivery（LibertyProfile）（Web Profile 7.0 および IBM JRE 1.8） | A：サポート対象 |
| IBM WebSphere Application Server 9.0 | A：サポート対象 |
| Apache Tomcat 8.5.x | A：サポート対象 |
| JBoss EAP 7.1.0 と JBoss Application Server | 回答：サポート対象 (1) |
| JBoss EAP 7.0.0 と JBoss Application Server | A：サポート対象 |

1. AEM Formsではサポートされていません。

### サーバーオペレーティングシステム {#server-operating-systems}

Adobe Experience Managerは、次のサーバープラットフォームで動作します。

<table> 
 <tbody> 
  <tr> 
   <td><strong>Platform</strong></td> 
   <td><strong>サポートレベル</strong></td> 
  </tr> 
  <tr> 
   <td><strong>Linux（Red Hat ディストリビューションに基づく）</strong></td> 
   <td>回答：サポート対象 (1)</td> 
  </tr> 
  <tr> 
   <td>Linux、Debian ディストリビューションベース（Ubuntu を含む）</td> 
   <td>回答：サポート対象 (4)</td> 
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
   <td>回答：サポート（制限あり）(3、5、7)<br /> R:新規契約の制限サポート</td> 
  </tr> 
  <tr> 
   <td>IBM AIX 7.2</td> 
   <td>回答：サポート（制限あり）(2、5、7)<br /> R:新規契約の制限サポート</td> 
  </tr> 
 </tbody> 
</table>

1. Linux Kernel 2.6、3.x および 4.x には、Red Hat ディストリビューションの派生 OS（Red Hat Enterprise Linux、CentOS、Oracle Linux、Amazon Linux など）が含まれます。AEM Forms のアドオン機能は、CentOS 7 および Red Hat Enterprise Linux 7 でのみサポートされています。
1. AEM Assets:の節を参照してください。 [XMPメタデータの書き戻しのサポート](#requirements-for-aem-assets-xmp-metadata-write-back)
1. AEM Assets:Dynamic Media Imaging はサポートされていません。 Dynamic Media Video がサポートされています。
1. AEM Formsは Ubuntu 16.04 LTS でのみサポートされています。
1. AEM Assets:サポートなし [Raw ファイル変換](/help/assets/camera-raw.md)
1. AEM Forms:実稼動環境のサポートなし
1. AEM Assets:サポートなし [強化PDFラスタライザ](/help/assets/aem-pdf-rasterizer.md)
1. AEM Forms:サポートなし

### 仮想／クラウドコンピューティング環境 {#virtual-cloud-computing-environments}

Adobe Experience Managerは、Microsoft Azure やAmazon Web Services(AWS) などのクラウドコンピューティング環境上での仮想マシンで、このページに記載されている技術要件と、Adobeの標準的なサポート条件に従って実行できるようサポートされています。

Adobeでは、AEMを Azure またはAWSにデプロイする場合は、Adobe Managed Services を使用することをお勧めします。 Adobe Managed Services を使用することで、これらのクラウドコンピューティング環境での AEM のデプロイと運用の経験とスキルを持つエキスパートのサポートを活用できます。次をご覧ください： [Adobe Managed Services に関する追加ドキュメント](https://www.adobe.com/jp/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).

Azure、AWS、またはその他のクラウドコンピューティング環境に AEM をデプロイするその他すべてのケースでは、アドビからのサポートはこのページに記載されている技術仕様に従って、仮想コンピューティング環境に限定されます。これらのクラウド環境で実行される AEM に関して報告された問題は、Azure Blob Storage や AWS S3 など、このページに記載されている技術要件の一部としてクラウドサービスが特にサポートされていない限り、クラウドコンピューティング環境に固有のクラウドサービスとは別に再現できる必要があります。

AEMを Adobe Managed Services 以外の Azure またはAWSにデプロイする方法に関する推奨事項については、クラウド環境でのAEMのデプロイをサポートするクラウドプロバイダーまたはAdobeパートナーと直接連携することを強くお勧めします。 選択したクラウドプロバイダーまたはパートナーは、特定のパフォーマンス、負荷、スケーラビリティ、セキュリティの要件を満たすために、アーキテクチャのサイズ設定、設計、実装を行います。

### Dispatcher プラットフォーム（web サーバー） {#dispatcher-platforms-web-servers}

Dispatcher は、キャッシュおよびロードバランシングコンポーネントです。[最新バージョンの Dispatcher をダウンロード](https://helpx.adobe.com/jp/experience-manager/dispatcher/release-notes.html)します。Experience Manager 6.4 ではバージョン 4.3.1 以降の Dispatcher が必要です。

Dispatcher バージョン 4.3.1 での使用では、次の web サーバーがサポートされています。

| Platform | サポートレベル |
|---|---|
| **Apache httpd 2.4.x** （後述の 1、2 も参照）。 | A：サポート対象 |
| Microsoft IIS 10（インターネット情報サーバー） | A：サポート対象 |
| Microsoft IIS 8.5（インターネット情報サーバー） | A：サポート対象 |

1. Apache httpd のソースコードをベースとして構築された Web サーバーは、ベースとした httpd のバージョンと同じサポートレベルでサポートされます。迷った場合は、Adobeに対し、それぞれのサーバ製品に関するサポートレベルの確認を依頼してください。 以下の場合に該当します。

   1. HTTP サーバーは、公式の Apache ソース配布のみを使用して構築されています。
   1. HTTP サーバーは、HTTP サーバーが実行されているオペレーティングシステムの一部として配信されました。例：IBM HTTP Server、Oracle HTTP Server

1. Dispatcher は、Windows オペレーティングシステム用の Apache 2.4.x では使用できません。

## サポートされているクライアントプラットフォーム {#supported-client-platforms}

### オーサリングユーザーインターフェイスでサポートされているブラウザー {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager のユーザーインターフェイスは、次のクライアントプラットフォームで使用できます。すべてのブラウザーは、デフォルトのプラグインとアドオンのセットを使用してテストされます。

AEM のユーザーインターフェイスは、大きめの画面（通常はノートブックやデスクトップコンピューター）とタブレットのフォームファクター（Apple iPad や Microsoft Surface など）向けに最適化されています。電話のフォームファクターはサポートされていません。

>[!NOTE]
>
>**リリースサイクルの短いブラウザーのサポート：**
>
>Mozilla Firefox、Google Chrome、Microsoft Edge のリリースは、数か月ごとに更新されます。アドビは、これらのブラウザーの今後のバージョンで以下に示すサポートレベルを維持するために、Adobe Experience Manager のアップデートの提供に取り組んでいます。

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
   <td>macOS の Apple Safari 12 x</td> 
   <td>A：サポート対象</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>macOS の Apple Safari 11 x</td> 
   <td>A：サポート対象</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>macOS の Apple Safari 10 x</td> 
   <td>A：サポート対象</td> 
   <td>A：サポート対象</td> 
  </tr> 
  <tr> 
   <td>Apple Safari（iOS 12.x）</td> 
   <td>A：サポート対象 [2]</td> 
   <td>Z：サポート対象外</td> 
  </tr> 
  <tr> 
   <td>Apple Safari（iOS 11.x）</td> 
   <td>A：サポート対象 [2]</td> 
   <td>Z：サポート対象外</td> 
  </tr> 
  <tr> 
   <td>Apple Safari(iOS 10.3)</td> 
   <td>A：サポート対象 [2]</td> 
   <td>Z：サポート対象外</td> 
  </tr> 
 </tbody> 
</table>

1. Firefox の拡張サポートリリース。[詳しくは、mozilla.org を参照してください。](https://www.mozilla.org/ja-JP/firefox/organizations/faq/)
1. Apple iPad のサポート

### Web サイトでサポートされているブラウザー {#supported-browsers-for-websites}

一般に、AEM Sites でレンダリングされる web サイトのブラウザーサポートは、AEM ページテンプレートの実装、設計およびコンポーネントの出力に依存するので、これらの部分を実装する当事者の管理下にあります。

### WebDAV クライアント {#webdav-clients}

**Microsoft Windows 7 以降**

Microsoft Windows 7 以降で、SSL で保護されていない AEM インスタンスに正常に接続するには、セキュリティで保護されていないネットワークを介したベーシック認証を Windows で有効にする必要があります。これには、WebClient の Windows レジストリの変更が必要です。

1. 以下のレジストリサブキーを探します。

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 2 つ以上の値を使用して、このサブキーに BasicAuthLevel レジストリのエントリを追加します。

詳しくは、 [Microsoftサポート KB 841215](https://support.microsoft.com/default.aspx/kb/841215).

Windows での WebDav クライアントの応答性を向上させるには、 [Microsoftサポート KB 2445570](https://support.microsoft.com/kb/2445570)

## プラットフォームに関するその他の注意事項 {#additional-platform-notes}

このセクションでは、Adobe Experience Manager とそのアドオンの実行に関する特別な注意事項と詳細情報を説明します。

### IPv4 と IPv6 {#ipv-and-ipv}

Adobe Experience Manager（インスタンス、Dispatcher）のすべての要素は、IPv4 と IPv6 の両方のネットワークにインストールできます。

特別な設定が不要なので、操作はシームレスです。必要に応じて、ネットワークの種類に適した形式で IP アドレスを指定するだけです。

つまり、IP アドレスを指定する必要がある場合には、次の形式から（必要に応じて）選択できます。

* IPv6 アドレス

   例：`https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4 アドレス

   例：`https://123.1.1.4:4502`

* サーバー名

   例：`https://www.yourserver.com:4502`

* デフォルトの `localhost` は、IPv4 と IPv6 の両方のネットワークインストールで解釈されます

   例：`http://localhost:4502`

### AEM Dynamic Media アドオンの要件 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media はデフォルトで無効になっています。詳しくは、 [Dynamic Mediaの有効化](/help/assets/config-dynamic.md#enabling-dynamic-media).

Dynamic Mediaを有効にすると、次の追加の必要システム構成が適用されます。
>[!NOTE]
>
>以下の必要システム構成が適用されます **_のみ_** Dynamic Media — ハイブリッドモードを使用している場合。Dynamic Media — ハイブリッドモードには、特定のオペレーティングシステムでのみ認定される、埋め込み画像サーバーがあります。
>
>Dynamic Media - Scene7 モード（**dynamicmedia_scene7** 実行モード）で Dynamic Media を実行する場合は、追加のシステム要件はありません。AEM と同じシステム要件が適用されます。Dynamic Media - Scene7モードのアーキテクチャでは、AEMに埋め込まれたサービスではなく、クラウドベースの画像サービスを使用します。

#### ハードウェア {#hardware}

以下のハードウェア要件は、Linux と Windows の両方のオペレーティングシステムに適用されます。

* 4 コア以上の Intel Xeon または AMD Opteron CPU
* 16 GB 以上の RAM

#### Linux {#linux}

Linux でのDynamic Mediaの使用には、次の前提条件が必要です。

* 最新の修正パッチが適用された RedHat Enterprise 7 または CentOS 7 以降
* 64 ビットオペレーティングシステム
* スワップ無効（推奨）
* SELinux 無効（後述の注意を参照）

>[!NOTE]
>
>ロケールが LC_CTYPE が en_US.UTF-8 と等しくないように設定されている場合、ダイナミックメディアが動作しなくなります。 その値を確認するには、コマンドプロンプトで「locale」と入力します。そのように設定しない場合は、AEM を実行する前に「export LC_CTYPE=」と入力して、LC_CTYPE 環境変数を空の文字列に設定します。

>[!NOTE]
>
>**SELinux の無効化：** SELinux がオンの場合、画像サービングは機能しません。このオプションはデフォルトで有効です。この問題を修正するには、 **/etc/selinux/config** ファイルを開き、SELinux 値を次の値から変更します。
>
>`SELINUX=enforcing`コピー先：`SELINUX=disabled`

>[!NOTE]
>
>**NUMA アーキテクチャ：** AMD64 および Intel EM64Tを使用するプロセッサを搭載したシステムは通常、NUMA（Non-Uniform Memory Architecture）プラットフォームとして構成されます。つまり、カーネルは単一のメモリノードを構築するのではなく、起動時に複数のメモリノードを構築します。
>
>複数のノード構成体を使用すると、他のノードが消費される前に、1 つまたは複数のノードでメモリが枯渇する可能性があります。メモリが枯渇した場合、使用可能なメモリがあっても、カーネルはプロセス（画像サーバーやプラットフォームサーバーなど）を強制終了する可能性があります。
>
>そのため、そうしたシステムを実行する場合は、**numa=off** 起動オプションを使用して NUMA をオフにし、カーネルがこれらのプロセスを強制終了するのを避けるようにすることをお勧めします。

>[!NOTE]
>
>**サーバーのホスト名は解決可能である必要があります。** サーバーのホスト名が IP アドレスに解決できることを確認します。 これが不可能な場合は、完全修飾ホスト名と IP アドレスを **/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* 物理メモリ（RAM）の少なくとも 2 倍の容量に等しいスワップ領域

Windows でDynamic Mediaを使用するには、x64 および x86 用のMicrosoft Visual Studio 2010、2013、および 2015 の再頒布可能パッケージをインストールする必要があります。

x64

* Microsoft Visual Studio 2010 の再頒布可能パッケージは、次の場所にあります。 [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/ja-jp/download/details.aspx?id=13523)
* Microsoft Visual Studio 2013 の再頒布可能パッケージは、次の場所で入手できます。 [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/ja-jp/download/details.aspx?id=40784)
* Microsoft Visual Studio 2015 の再頒布可能パッケージは、次の場所にあります。 [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/ja-jp/download/details.aspx?id=48145)

x86

* Microsoft Visual Studio 2010 の再頒布可能パッケージは、次の場所にあります。 [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/ja-jp/download/details.aspx?id=5555)
* Microsoft Visual Studio 2013 の再頒布可能パッケージは、次の場所で入手できます。 [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Microsoft Visual Studio 2015 の再頒布可能パッケージは、次の場所にあります。 [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/ja-jp/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x 以降
* 体験版およびデモ版のみサポート

### AEM Forms PDF Generator の要件 {#requirements-for-aem-forms-pdf-generator}

<table> 
 <tbody> 
  <tr> 
   <th><p><strong>製品</strong></p> </th> 
   <th><p><strong>PDF への変換でサポートされる形式</strong></p> </th> 
  </tr> 
  <tr> 
   <td><p><a href="https://helpx.adobe.com/jp/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 クラシックトラック</a></p> </td> 
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
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX 、JP2、J2K、J2C、JPC）、HTML、HTM、RTF、TXT</td> 
  </tr> 
  <tr> 
   <td><p>OpenOffice 3.4</p> </td> 
   <td><p>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX 、JP2、J2K、J2C、JPC）、HTML、HTM、RTF、TXT</p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>PDF Generator は、サポート対象のオペレーティングシステムとアプリケーションの英語版、フランス語版、ドイツ語版、および日本語版のみをサポートしています。
>
>さらに、次の点に注意してください。
>
>* PDFジェネレーターに必要 [Acrobat 2017 classic track バージョン 17.011.30078以降](https://helpx.adobe.com/jp/acrobat/release-note/release-notes-acrobat-reader.html) をクリックして変換を実行します。
>* AEM Formsは、サポートされているソフトウェアの 32 ビット版のみをサポートしています。
>* OCRPDF( 検索可能なPDF)、Optimize PDFおよびExport PDFの機能は、Microsoft Windows でのみサポートされます。
>* HTML2PDFサービスは、AIX では非推奨です。
>* OpenOffice 用のPDFジェネレーター変換は、Windows、Linux および Solaris でのみサポートされています。
>* OCR PDF、Optimize PDF、Export PDF の各機能は、Windows でのみサポートされます。
>* Acrobat のバージョンは、PDF Generator 機能を有効にするために AEM Forms にバンドルされています。バンドルされたバージョンには、AEM Forms PDF Generator で使用するために、AEM Forms のライセンス期間中に AEM Forms でのみプログラムでアクセスする必要があります。詳しくは、デプロイメントに応じて、 AEM Forms 製品の説明（[オンプレミス](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-on-premise.html)または [Managed Services](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-managed-services.html)）を参照してください。
>


### AEM Forms Designer の要件 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2012 Server R2、Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server、Microsoft® Windows® 10
* 1 GHz 以上の高速プロセッサー（PAE、NX、および SSE2 に対応）
* 1 GB の RAM（32 ビット OS の場合）または 2 GB の RAM（64 ビット OS の場合）
* 16 GB のディスク空き容量（32 ビット OS の場合）または 20 GB のディスク空き容量（64 ビット OS の場合）
* グラフィックメモリ - 128 MB の GPU（256 MB 推奨）
* 2.35 GB のハードディスク空き容量
* 1024 x 768 ピクセル以上のモニター解像度
* ビデオハードウェアアクセラレーション（オプション）
* Acrobat Pro DC、Acrobat Standard DC、Adobe Acrobat Reader DC
* Designer をインストールするための管理者権限

### AEM Assets XMPメタデータの書き戻しの要件 {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP の書き戻しは、次のプラットフォームおよびファイル形式でサポートされ、有効になります。

**オペレーティングシステム**

* Linux（32 ビット、64 ビットシステムでは 32 ビットアプリケーションのサポートが必要）。 32 ビットのクライアントライブラリをインストールする手順については、[64 ビット RedHat Linux で XMP の抽出と書き戻しを有効にする方法](https://helpx.adobe.com/jp/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)を参照してください。

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

### AEM Screens Player の要件 {#requirements-for-aem-screens-player}

AEM Screens Player バージョン 3.3.x では、次のオペレーティングシステムをサポートしています。

* Microsoft Windows 10 Enterprise LTSB
* Google Chrome OS 62+
* Google Android 5.1.1（更新済み Android System WebView バージョン 52 以降）
* Apple iOS 10.3 以降
* Apple macOS 10.12 以降
