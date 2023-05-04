---
title: OSGi 上での Forms ベースのワークフローのインストールと設定
seo-title: Installing and Configuring Forms-centric workflow on OSGi
description: AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 847c3351-dc46-4e60-a023-0f4e9e057c7c
topic-tags: installing
discoiquuid: 7333641e-8c8c-4b52-a7da-a2976c88592c
role: Admin
exl-id: 308b106f-4c5a-49d6-a7f6-c1e8a0bf62e9
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 69%

---

# OSGi 上での Forms ベースのワークフローのインストールと設定 {#installing-and-configuring-forms-centric-workflow-on-osgi}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

## はじめに {#introduction}

企業は、複数のフォーム、バックエンドシステム、その他のデータソースからデータを収集して処理します。データの処理には、レビューと承認の手順、繰り返しのタスク、データのアーカイブが含まれます。例えば、フォームをレビューし、PDF ドキュメントに変換する場合などです。手動でおこなうと、繰り返しタスクに多くの時間とリソースが必要になる場合があります。

[OSGi 上の Forms ベースのワークフロー](/help/forms/using/aem-forms-workflow.md) を使用して、アダプティブフォームベースのワークフローを迅速に構築することができます。これらのワークフローは、レビューと承認のワークフロー、ビジネスプロセスのワークフロー、その他の繰り返しタスクの自動化に役立ちます。これらのワークフローは、ドキュメントの処理 (PDFドキュメントの作成、アセンブリ、配布、アーカイブ、電子署名の追加、ドキュメントへのアクセス制限、バーコードフォームのデコードなど ) や、Acrobat Sign署名ワークフローの使用にも役立ちます。

これらのワークフローを一度設定すると、手動でトリガーして定義済みプロセスを完了することができ、また、ユーザーによるフォームの送信やインタラクティブ通信の際に、ワークフローをプログラムで実行することもできます。これは、AEM Forms のアドオンパッケージに含まれる機能で、

AEM Forms は強力なエンタープライズクラスのプラットフォームです。OSGi 上の Forms ベースのワークフローは、AEM Forms の機能の 1 つに過ぎません。機能の完全な一覧については、「[AEM Forms の概要](/help/forms/using/introduction-aem-forms.md)」を参照してください。

>[!NOTE]
>
>OSGi での Forms 中心のワークフローを使用すると、JEE スタックに本格的なプロセス管理機能をインストールしなくても、OSGi スタックで様々なタスクのワークフローを迅速に構築およびデプロイできます。OSGi 上の Forms ベースの AEM ワークフローと JEE 上のプロセスマネジメントの[比較](/help/forms/using/capabilities-osgi-jee-workflows.md)を参照して、機能の違いと類似点を学びます。
>
>比較の後、JEE スタックにプロセス管理機能をインストールする場合は、JEE スタックとプロセス管理機能のインストールと設定の詳細について、 [JEE での AEM Forms のインストールまたはアップグレード](/help/forms/home.md) を参照してください。

## デプロイメントトポロジ {#deployment-topology}

AEM Formsアドオンパッケージは、AEMにデプロイされたアプリケーションです。 OSGi 機能上で Forms ベースのワークフローを実行するには、最小限の AEM オーサーインスタンスまたは処理インスタンス（実稼動オーサー）が必要です。処理インスタンスは、[強化された AEM オーサー](/help/forms/using/hardening-securing-aem-forms-environment.md) インスタンスです。実稼動オーサーでは、ワークフローやアダプティブフォームの作成など、実際のオーサリングを実行しないでください。

次のトポロジは、AEM Formsインタラクティブ通信、Correspondence Management、AEM Formsデータキャプチャ、および OSGi 上のForms中心のワークフローを実行するためのトポロジを示しています。 トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![recommended-topology](assets/recommended-topology.png)

OSGi 上の AEM Forms の Forms ベースのワークフローは、AEM Form のオーサーインスタンス上で、AEM インボックスと AEM ワークフローモデルの作成 UI を実行します。

## システム要件 {#system-requirements}

>[!NOTE]
>
>[データキャプチャ機能のインストールと設定](/help/forms/using/installing-configuring-aem-forms-osgi.md)の記事で説明したように、AEM Forms を OSGi にインストール済みであれば、ドキュメントの[次の手順](#next-steps) に節スキップしてください。

Forms ベースのワークフローを OSGi 上でのインストールと設定を開始する前に、以下を確認してください。

* ハードウェアとソフトウェアのインフラが正しく設定されていること。サポート対象のハードウェアとソフトウェアの一覧について詳しくは、「[技術要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEMインスタンスのインストールパスに空白が含まれていません。
* AEMインスタンスが起動し、実行中です。 AEM の用語では、「インスタンス」とは、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。OSGi 上で Forms ベースのワークフローを実行するには、少なくとも 1 つの AEM インスタンス（オーサーまたは処理）が必要です。

   * **作成者**:コンテンツの作成、アップロード、編集、Web サイトの管理に使用されるAEMインスタンス。 公開の準備が整ったコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **処理中：** 処理インスタンスは [AEM オーサーの堅牢化](/help/forms/using/hardening-securing-aem-forms-environment.md) インスタンス。 オーサーインスタンスを設定し、インストールを実行した後でこれを強化することができます。 
   * **公開**:公開されたコンテンツをインターネットまたは内部ネットワーク経由で公開するAEMインスタンス。

* メモリ要件を満たしています。 AEM Forms アドオンパッケージでは、次が必要です。

   * 15 GB の一時領域 (Microsoft Windows ベースのインストール用 )
   * Unix ベースのインストールの場合、6 GB の一時的な空きスペースが必要です。

* UNIX ベースのシステムの追加要件：UNIX ベースのオペレーティングシステムを使用している場合は、各オペレーティングシステムのインストールメディアから次のパッケージをインストールします。

<table> 
 <tbody>
  <tr>
   <td>expat</td> 
   <td>libxcb</td> 
   <td>freetype</td> 
   <td>libXau</td> 
  </tr>
  <tr>
   <td>libSM</td> 
   <td>zlib</td> 
   <td>libICE</td> 
   <td>libuuid</td> 
  </tr>
  <tr>
   <td>glibc</td> 
   <td>libXext</td> 
   <td><p>nss-softokn-freebl</p> </td> 
   <td>fontconfig</td> 
  </tr>
  <tr>
   <td>libX11</td> 
   <td>libXrender</td> 
   <td>libXrandr</td> 
   <td>libXinerama</td> 
  </tr>
 </tbody>
</table>

## AEM Forms アドオンパッケージのインストール {#install-aem-forms-add-on-package}

AEM Formsアドオンパッケージは、AEMにデプロイされたアプリケーションです。 このパッケージには、OSGi 上の Forms ベースのワークフローとその他の機能が含まれます。次の手順を実行してアドオンパッケージをインストールします。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 内 **[!UICONTROL フィルター]** セクション：
   1. 選択 **[!UICONTROL Forms]** から **[!UICONTROL 解決策]** 」ドロップダウンリストから選択できます。
   2. パッケージのバージョンとタイプを選択します。「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
1. お使いのオペレーティングシステムに適したパッケージの名前をタップし、「**[!UICONTROL EULA 利用規約に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」をタップします。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=ja)を開き、「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択して「**[!UICONTROL インストール]**」をクリックします。

   [AEM Forms リリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)の記事に記載されている直接リンクからパッケージをダウンロードすることもできます。

1. パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**すぐにサーバーを再起動しないでください。** AEM Forms サーバーを停止する前に、ServiceEvent REGISTERED メッセージと ServiceEvent UNREGISTERED メッセージが [AEM-Installation-Directory]/crx-quickstart/logs/error.log ファイルに表示されなくなり、このログファイルが安定した状態になるまで待ってください。
1. 手順 1 から 7 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

## インストール後の設定 {#post-installation-configurations}

AEM Formsには、いくつかの必須およびオプションの設定があります。 必須の設定には、BouncyCastle ライブラリの設定やシリアル化エージェントの設定が含まれます。 オプションの設定には、ディスパッチャーおよび Adobe Target の設定が含まれます。

### 必須のインストール後の設定 {#mandatory-post-installation-configurations}

#### RSA ライブラリと BouncyCastle ライブラリの設定  {#configure-rsa-and-bouncycastle-libraries}

これらのライブラリを起動するには、すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行します。 

1. 基になる AEM インスタンスを停止します。
1. 編集用に [AEM インストールディレクトリ ]\crx-quickstart\conf\sling.properties ファイルを開きます。

   [AEM インストールディレクトリ ]\crx-quickstart\bin\start.bat を使用して AEM を起動する場合は、[AEM ルート ]\crx-quickstart\ にある sling.properties を編集してください。

1. 次のプロパティを sling.properties ファイルに追加します。

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. （AIX のみ）以下のプロパティを sling.properties ファイルに追加します。

   ```
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. ファイルを保存して閉じ、AEM インスタンスを起動します。
1. 手順 1 から 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

#### シリアル化エージェントの設定 {#configure-the-serialization-agent}

このパッケージを許可リストに加えるには、オーサーインスタンスとパブリッシュインスタンスの両方で以下の手順を実行します。

1. ブラウザーウィンドウで、AEM Configuration Manager を開きます。デフォルトの URL は `https://[server]:[port]/system/console/configMgr` です。
1. **デシリアライゼーションファイアウォール設定**&#x200B;を検索して開きます。
1. **sun.util.calendar** パッケージを&#x200B;**許可リストに加える**&#x200B;フィールドに追加します。「保存」をクリックします。
1. 手順 1 から 3 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

### インストール後のオプション設定 {#optional-post-installation-configurations}

#### Dispatcher の設定 {#configure-dispatcher}

Dispatcher は、AEMのキャッシュおよびロードバランシングツールです。 AEM Dispatcher は、AEMサーバーを攻撃から保護するのにも役立ちます。 エンタープライズクラスの Web サーバーと組み合わせて Dispatcher を使用することで、AEMインスタンスのセキュリティを強化できます。 [ディスパッチャー](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html)を使用する場合は、AEM Forms の次の設定を実行してください。

1. AEM Forms のアクセスの設定：

   dispatcher.any ファイルを編集用に開きます。 フィルターセクションに移動し、次のフィルターをフィルターセクションに追加します。

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   ファイルを保存して閉じます。 フィルターについて詳しくは、 [Dispatcher のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=ja).

1. リファラーフィルターサービスを設定します。

   Apache Felix Configuration Manager に管理者としてログインします。 Configuration Manager のデフォルト URL は `https://[server]:[port_number]/system/console/configMgr` です。**Configurations**&#x200B;メニューで「**Apache Sling Referrer Filter**」を選択します。「Allow Hosts」フィールドで、ディスパッチャーのホスト名を入力してそれをリファラーとして許可し、「**保存**」をクリックします。URL の形式は、`https://[server]:[port]` です。

#### キャッシュの設定 {#configure-cache}

キャッシュは、データアクセス時間の短縮、待ち時間の短縮、入出力 (I/O) 速度の向上を実現するメカニズムです。 アダプティブフォームのキャッシュには、アダプティブフォームのHTMLコンテンツと JSON 構造のみが保存されます。事前入力されたデータは保存されません。 これにより、アダプティブフォームのレンダリングに要する時間を短縮できます。

* アダプティブフォームのキャッシュを使用する場合は、 [AEM Dispatcher](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html) アダプティブフォームのクライアントライブラリ（CSS および JavaScript）をキャッシュする場合。
* カスタムコンポーネントを開発する際は、開発に使用するサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。

次の手順を実行してアダプティブフォームのキャッシュを設定します。

1. `https://[server]:[port]/system/console/configMgr` の AEM Web コンソール設定マネージャーに移動します。
1. 「**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定]**」をクリックして、設定値を編集します。設定値を編集ダイアログで、AEM Forms サーバーのインスタンスでキャッシュできるフォームまたはドキュメントの最大数を「**アダプティブフォームの数**」フィールドに指定します。デフォルト値は 100 です。「**保存**」をクリックします。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュ設定を無効にしたり変更したりすると、キャッシュがリセットされ、すべてのフォームとドキュメントがキャッシュから削除されます。

#### Acrobat Signの設定 {#configure-adobe-sign}

Acrobat Sign により、アダプティブフォームの電子サインワークフローを有効にできます。電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

OSGi 上の一般的なAcrobat SignおよびForms中心のワークフローシナリオでは、ユーザーがアダプティブフォームに入力してサービスの申し込みを行います。 例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申し込みフォームに入力、送信、署名すると、承認または却下のワークフローが開始されます。サービスプロバイダーは、AEMインボックスでアプリケーションを確認し、Acrobat Signを使用してアプリケーションに電子署名します。 同様の電子署名ワークフローを有効にするには、Acrobat SignとAEM Formsを統合します。

AEM FormsでAcrobat Signを使用するには、 [Acrobat SignとAEM Formsの統合](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

## 次の手順 {#next-steps}

OSGi 機能上で Forms ベースのワークフローを使用する環境を設定しました。この機能を使用するための手順は、次のとおりです。

* [OSGi 上の Forms ベースのワークフローの使用](/help/forms/using/aem-forms-workflow.md)
* [ワークフローステップのリファレンス](/help/sites-developing/workflows-step-ref.md)
* [レターとインタラクティブ通信の後処理](/help/forms/using/submit-letter-topostprocess.md)
