---
title: グローバルドキュメントストレージディレクトリ
seo-title: Global document storage directory
description: グローバルドキュメントストレージ (GDS) ディレクトリは、プロセス内で使用される長期間有効なファイルの保存に使用されるディレクトリです。
seo-description: The global document storage (GDS) directory is a directory used to store long-lived files that are used within a process.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
exl-id: 37d6187f-4f91-4ad4-b0d6-eaae165abe64
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 8%

---

# グローバルドキュメントストレージディレクトリ{#global-document-storage-directory}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

この *グローバルドキュメントストレージ (GDS)* directory は、プロセス内で使用される長期間有効なファイルを保存するために使用されるディレクトリです。 これらのファイルには、PDF、ポリシー、フォームテンプレートが含まれます。 長期間有効なファイルは、多くのAEM forms デプロイメントの全体的な状態の重要な部分です。 長期間有効なドキュメントの一部またはすべてが失われたり破損したりした場合、forms サーバーが不安定になる可能性があります。 非同期ジョブ呼び出しの入力ドキュメントも GDS ディレクトリに保存されます。このドキュメントを使用して要求を処理する必要があります。 GDS ディレクトリをホストするファイルシステムの信頼性を考慮することが重要です。 品質とサービスレベルのニーズに応じて、RAID(Redundant Array of Independent Disks) やその他のテクノロジーを使用します。

長期間有効なファイルには、機密性の高いユーザー情報が含まれている場合があります。 この情報には、AEM forms API またはユーザーインターフェイスを使用してアクセスする際に、特別な資格情報が必要になる場合があります。 GDS ディレクトリがオペレーティングシステムを通じて適切に保護されていることが重要です。 GDS ディレクトリへの読み取り/書き込みアクセス権を持つのは、アプリケーションサーバーの実行に使用される管理者アカウントだけです。

GDS 用の安全で可用性の高いディレクトリを選択するほか、データベースでのドキュメントの保存を有効にすることもできます。 ドキュメントの保存にAEM forms データベースを使用している場合でも、AEM forms には GDS ディレクトリが必要です。 ( [データベースをドキュメントストレージに使用する場合のバックアップオプション](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

AEM forms アプリケーションデータは、GDS ディレクトリとAEM forms データベースに格納されます。 次の表に、データとその場所を示します。

<table> 
 <thead> 
  <tr> 
   <th><p>AEM forms Data</p></th> 
   <th><p>データベース</p></th> 
   <th><p>GDS</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>アプリケーションデータ（ユーザー、役割、プロセス、ポリシー、エンドポイント、イベントなど）</p></td> 
   <td><p>はい</p></td> 
   <td><p>いいえ</p></td> 
  </tr> 
  <tr> 
   <td><p>デプロイ済みのサービスコンテナ</p></td> 
   <td><p>はい</p></td> 
   <td><p>いいえ</p></td> 
  </tr> 
  <tr> 
   <td><p>Document Manager </p></td> 
   <td><p>いいえ</p></td> 
   <td><p>はい</p></td> 
  </tr> 
  <tr> 
   <td><p>Forms Repository</p></td> 
   <td><p>はい</p></td> 
   <td><p>いいえ</p></td> 
  </tr> 
  <tr> 
   <td><p>システム設定</p></td> 
   <td><p>はい</p></td> 
   <td><p>いいえ</p></td> 
  </tr> 
  <tr> 
   <td><p>監視フォルダー</p></td> 
   <td><p>いいえ</p></td> 
   <td><p>はい</p></td> 
  </tr> 
 </tbody> 
</table>

## GDS ディレクトリの設定 {#configuring-the-gds-directory}

GDS ディレクトリの場所は、AEM forms のインストールプロセス中に手動で設定できます。 インストール時に場所の設定が空のままの場合、アプリケーションサーバーのインストール下のディレクトリは次のようにデフォルトで表示されます。

* （JBoss）`*[appserver root]*/server/*[type]*/svcnative/DocumentStorage`
* (WebLogic) `*[appserverdomain]*/*[server]*/adobe/DocumentServer/DocumentStorage`
* （WebSphere）`*[appserver root]*/installedApps/adobe/*[server]*/DocumentStorage`

## デフォルトの GDS の場所の変更 {#change-the-default-gds-location}

AEM forms のインストールが完了したら、管理コンソールで GDS の場所を変更できます。 プロセスを完了するには、手動でデータの場所を変更する必要があります。

>[!NOTE]
>
>次の方法でデータを移行します。そうしないと、データが失われます。

1. 管理コンソールにログインし、設定/コアシステム設定/設定をクリックします。
1. 「グローバルドキュメントストレージディレクトリ」ボックスに、新しい GDS ディレクトリへのフルパスを入力し、「OK」をクリックします。
1. 直ちにアプリケーションサーバーをシャットダウンします。
1. 内部ディレクトリ構造を維持しながら、古い GDS ディレクトリから新しい場所にすべてのファイルを移動します。
1. アプリケーションサーバーを再起動します。

## デプロイメントファイルについて {#about-deployment-files}

AEM forms は、サービスコンテナと Java 2 Platform, Enterprise Edition(J2EE)EAR ファイルの 2 種類のデプロイメントファイルで構成されています。 EAR ファイルは、AEM forms のコア機能を含む、標準の J2EE アプリケーションバンドルで構成されています。 アプリケーションサーバー固有の EAR ファイルは、次のとおりです。

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

AEM forms の実装では、組み立てられた EAR ファイルとサポートファイルを、AEM forms ソリューションを実行する予定のアプリケーションサーバーにデプロイします。 複数のモジュールを設定してアセンブリした場合、デプロイ可能なモジュールはデプロイ可能な EAR ファイル内にパッケージ化されます。 これらのファイルをデプロイするには、ファイルを *[appserver home]*\server\all\deploy ディレクトリにコピーします。

モジュールとAEM forms アーカイブファイルは、JAR ファイルにパッケージ化されます。 J2EE タイプのファイルではないので、アプリケーションサーバーにはデプロイされません。 代わりに、GDS ディレクトリにコピーされ、その場所への参照がAEM forms データベースに保存されます。 この理由から、GDS ディレクトリをクラスターのすべてのノードで共有する必要があります。 すべてのノードは、DSC の中央ストレージディレクトリにアクセスできる必要があります。

>[!NOTE]
>
>サービスコンテナをデプロイする前に、GDS ディレクトリを作成して設定していることを確認してください。 ( [GDS ディレクトリの設定](global-document-storage-directory.md#configuring-the-gds-directory))
