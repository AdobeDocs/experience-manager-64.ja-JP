---
title: OSGi でのForms中心のワークフローのインストールと設定
seo-title: Installing and Configuring Forms-centric workflow on OSGi
description: 'AEM Forms インタラクティブ通信をインストールして設定し、業務上の書簡、ドキュメント、取引明細書、給与金通知、マーケティング用メール、請求書、ウェルカムキットを作成します。 '
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 847c3351-dc46-4e60-a023-0f4e9e057c7c
topic-tags: installing
discoiquuid: 7333641e-8c8c-4b52-a7da-a2976c88592c
role: Admin
exl-id: 308b106f-4c5a-49d6-a7f6-c1e8a0bf62e9
source-git-commit: 3c050c33a384d586d74bd641f7622989dc1d6b22
workflow-type: tm+mt
source-wordcount: '1611'
ht-degree: 56%

---

# OSGi でのForms中心のワークフローのインストールと設定 {#installing-and-configuring-forms-centric-workflow-on-osgi}

## はじめに {#introduction}

企業は、複数のフォーム、バックエンドシステム、その他のデータソースからデータを収集して処理します。 データの処理には、レビューと承認の手順、繰り返しのタスク、データのアーカイブが含まれます。 例えば、フォームをレビューし、PDFドキュメントに変換する場合などです。 手動でおこなうと、繰り返しタスクに多くの時間とリソースがかかる場合があります。

以下を使用できます。 [OSGi 上のForms中心のワークフロー](/help/forms/using/aem-forms-workflow.md) アダプティブフォームベースのワークフローを迅速に構築するため。 これらのワークフローは、レビューと承認のワークフロー、ビジネスプロセスのワークフロー、その他の繰り返しタスクの自動化に役立ちます。 これらのワークフローは、ドキュメントの処理 (PDFドキュメントの作成、アセンブリ、配布、アーカイブ、電子署名の追加、ドキュメントへのアクセス制限、バーコードフォームのデコードなど ) や、Adobe Sign署名ワークフローの使用にも役立ちます。

設定後は、これらのワークフローを手動でトリガーして、定義済みのプロセスを完了したり、ユーザーがフォームやインタラクティブ通信を送信したときにプログラムを使用して実行したりできます。 これは、AEM Forms のアドオンパッケージに含まれる機能で、

AEM Forms は強力なエンタープライズクラスのプラットフォームです。OSGi 上のForms中心のワークフローは、AEM Formsの機能の 1 つに過ぎません。 機能の完全な一覧については、「[AEM Forms の概要](/help/forms/using/introduction-aem-forms.md)」を参照してください。

>[!NOTE]
>
>OSGi での Forms 中心のワークフローを使用すると、JEE スタックに本格的なプロセス管理機能をインストールしなくても、OSGi スタックで様々なタスクのワークフローを迅速に構築およびデプロイできます。参照先 [比較](/help/forms/using/capabilities-osgi-jee-workflows.md) OSGi 上のForms中心のAEM Workflows と JEE 上の Process Management の機能の違いと類似点について説明します。
>
>比較後、JEE スタックに Process Management 機能をインストールする場合は、 [JEE でのAEM Formsのインストールまたはアップグレード](/help/forms/home.md) JEE スタックのインストールと設定、および Process Management 機能に関する詳細。

## デプロイメントトポロジ {#deployment-topology}

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。OSGi 機能上でForms中心のワークフローを実行するには、少なくとも 1 つの AEM オーサーインスタンスまたは処理インスタンス（実稼動オーサー）が必要です。 処理インスタンスは [AEM オーサーの堅牢化](/help/forms/using/hardening-securing-aem-forms-environment.md) インスタンス。 実稼動環境の作成者では、ワークフローやアダプティブフォームの作成など、実際のオーサリングを実行しないでください。

次のトポロジは、AEM Forms のインタラクティブ通信、Correspondence Management、AEM Forms のデータ取得および OSGi 機能にあるフォーム中心のワークフローを実行するための指標トポロジです。トポロジーについて詳しくは、「[AEM Forms のアーキテクチャとデプロイメントトポロジー](/help/forms/using/aem-forms-architecture-deployment.md)」を参照してください。

![推奨トポロジ](assets/recommended-topology.png)

OSGi 上のAEM Forms Forms中心のワークフローは、AEM FormsのオーサーインスタンスでAEM Inbox とAEM Workflow Model の作成 UI を実行します。

## システム要件 {#system-requirements}

>[!NOTE]
>
>スキップして [次の手順](#next-steps) ドキュメントの「 」セクション (OSGi に既にAEM Formsをインストールしている場合 ) [データキャプチャ機能のインストールと設定](/help/forms/using/installing-configuring-aem-forms-osgi.md) 記事。

OSGi でのForms中心のワークフローのインストールと設定を開始する前に、以下を確認してください。

* ハードウェアとソフトウェアのインフラが正しく設定されていること。サポート対象のハードウェアおよびソフトウェアの詳細な一覧については、「[技術的要件](/help/sites-deploying/technical-requirements.md)」を参照してください。

* AEM インスタンスのインストールパスに空白が含まれていないこと。
* AEM インスタンスが稼働していること。AEM の用語では、「インスタンス」は、サーバー上でオーサーモードまたはパブリッシュモードで実行されている AEM のコピーのことです。OSGi 上でForms中心のワークフローを実行するには、少なくとも 1 つのAEMインスタンス（オーサーまたは処理）が必要です。

   * **作成者：**&#x200B;コンテンツを作成、アップロード、編集し、Web サイトを管理する AEM インスタンス。公開する準備ができたコンテンツは、パブリッシュインスタンスにレプリケートされます。
   * **処理：**&#x200B;処理インスタンスは、[強化された AEM オーサー](/help/forms/using/hardening-securing-aem-forms-environment.md)インスタンスです。オーサーインスタンスを設定し、インストールの実行後に強化することができます。
   * **パブリッシュ**：発行されたコンテンツをインターネットまたは社内ネットワークを通じて公開する AEM インスタンス。

* メモリ要件が満たされていること。AEM Forms アドオンパッケージには次の一時領域が必要となります。

   * Microsoft Windows ベースのインストールの場合、15 GB の一時的な空きスペースが必要です。
   * Unix ベースのインストールの場合、6 GB の一時的な空きスペースが必要です。

* Unix ベースのシステムの追加必要システム構成：Unix ベースのオペレーティングシステムを使用する場合は、それぞれのオペレーティングシステムのインストールメディアから、次のパッケージをインストールしてください。

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

AEM Forms アドオンパッケージは AEM にデプロイされるアプリケーションです。このパッケージには、OSGi 上のForms中心のワークフローとその他の機能が含まれます。 次の手順を実行してアドオンパッケージをインストールします。

1. [ソフトウェア配布](https://experience.adobe.com/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」をタップします。
1. 「**[!UICONTROL フィルター]**」セクションで、
   1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
   2. パッケージのバージョンとタイプを選択します。 また、 **[!UICONTROL ダウンロードを検索]** 」オプションを使用して結果をフィルターします。
1. 使用するオペレーティングシステムに適したパッケージ名をタップし、「 」を選択します。 **[!UICONTROL 使用許諾契約書に同意する]**&#x200B;をタップし、 **[!UICONTROL ダウンロード]**.
1. [パッケージマネージャー](https://docs.adobe.com/content/help/ja/experience-manager-65/administering/contentmanagement/package-manager.html)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
1. パッケージを選択し、 **[!UICONTROL インストール]**.

   また、 [AEM Formsリリース](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) 記事。

1. パッケージのインストールが完了したら、AEM インスタンスを再起動するよう指示されます。**すぐにはサーバーを再起動しないでください。** AEM Formsサーバーを停止する前に、 ServiceEvent REGISTERED メッセージと ServiceEvent UNREGISTERED メッセージが [AEM-Installation-Directory]/crx-quickstart/logs/error.logファイルとログは安定しています。
1. 手順 1 から 7 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

## インストール後の設定 {#post-installation-configurations}

AEM Forms には、いくつかの必須およびオプションの設定があります。必須の設定には、BouncyCastle ライブラリおよびシリアル化エージェントの設定が含まれます。オプションの設定には、ディスパッチャーおよび Adobe Target の設定が含まれます。

### インストール後の必須の設定 {#mandatory-post-installation-configurations}

#### RSA ライブラリと BouncyCastle ライブラリの設定  {#configure-rsa-and-bouncycastle-libraries}

すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行し、ライブラリの委任を起動します。

1. 基になる AEM インスタンスを停止します。
1. を開きます。 [AEMインストールディレクトリ]\crx-quickstart\conf\sling.propertiesファイルを編集します。

   次を使用した場合： [AEMインストールディレクトリ]\crx-quickstart\bin\start.batを開始して、次の場所にある sling.properties を編集します。 [AEM_root]\crx-quickstart\.

1. 以下のプロパティを sling.properties ファイルに追加します。

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. （AIX のみ）次のプロパティを sling.properties ファイルに追加します。

   ```
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. ファイルを保存して閉じ、AEM インスタンスを起動します。
1. 手順 1 から 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

#### シリアル化エージェントの設定 {#configure-the-serialization-agent}

すべてのオーサーインスタンスとパブリッシュインスタンスで次の手順を実行し、パッケージをに追加し許可リストます。

1. ブラウザーウィンドウで、AEM Configuration Manager を開きます。デフォルトの URL は `https://[server]:[port]/system/console/configMgr` です。
1. **デシリアライゼーションファイアウォール設定**&#x200B;を検索して開きます。
1. を **sun.util.calendar** パッケージを **許可リスト** フィールドに入力します。 「保存」をクリックします。
1. 手順 1 から 3 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します。

### インストール後のオプションの設定 {#optional-post-installation-configurations}

#### Dispatcher の設定 {#configure-dispatcher}

ディスパッチャーは AEM のキャッシングおよびロードバランスツールです。AEM ディスパッチャーはまた、AEM サーバーを攻撃から保護することにも役立ちます。エンタープライズクラスの Web サーバーと一緒にディスパッチャーを使用することで、AEM インスタンスのセキュリティを向上できます。次を使用する場合、 [Dispatcher](https://helpx.adobe.com/jp/experience-manager/dispatcher/using/dispatcher-configuration.html)次に、AEM Formsの次の設定を実行します。

1. AEM Forms のアクセスの設定:

   dispatcher.any ファイルを開いて編集します。フィルターセクションに移動し、次のフィルターをフィルターセクションに追加します。

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   ファイルを保存して閉じます。フィルターについて詳しくは、「[ディスパッチャードキュメント](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)」を参照してください。

1. リファラーフィルターサービスの設定：

   管理者として Apache Felix Configuration Manager にログインします。Configuration Manager のデフォルト URL は次のとおりです。 `https://[server]:[port_number]/system/console/configMgr`. **Configurations**&#x200B;メニューで「**Apache Sling Referrer Filter**」を選択します。「Allow Hosts」フィールドで、ディスパッチャーのホスト名を入力してそれをリファラーとして許可し、「**保存**」をクリックします。エントリのフォーマットは、 `https://[server]:[port]`.

#### キャッシュの設定 {#configure-cache}

キャッシングは、データへのアクセスにかかる時間を短縮し、遅延を削減して I/O 速度を改善するメカニズムです。アダプティブフォームのキャッシュは、アダプティブフォームの HTML コンテンツと JSON の構造のみを保存し、事前入力されたデータは保存しません。これにより、アダプティブフォームのレンダリングの時間を短縮します。

* アダプティブフォームのキャッシュを使用するときは、[AEM ディスパッチャー](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) を使用してアダプティブフォームのクライアントライブラリ（CSS および JavaScript）をキャッシュします。
* カスタムコンポーネントの開発時には、開発に使用されるサーバー上でアダプティブフォームのキャッシュを無効にしておく必要があります。

アダプティブフォームのキャッシュを設定するには、以下の手順を実行します。

1. `https://[server]:[port]/system/console/configMgr` の AEM Web コンソール設定マネージャーに移動します。
1. 「**[!UICONTROL アダプティブフォームおよびインタラクティブ通信 Web チャネルの設定]**」をクリックして、設定値を編集します。設定値を編集ダイアログで、AEM Formsサーバーのインスタンスでキャッシュできるフォームまたはドキュメントの最大数を指定します。 **アダプティブFormsの数** フィールドに入力します。 デフォルト値は 100 です。「**保存**」をクリックします。

   >[!NOTE]
   >
   >キャッシュを無効にするには、「アダプティブフォームの数」フィールドの値を **0** に設定します。キャッシュ設定を無効にしたり変更したりすると、キャッシュがリセットされ、すべてのフォームとドキュメントがキャッシュから削除されます。

#### Adobe Sign の設定 {#configure-adobe-sign}

Adobe Sign により、アダプティブフォームの電子署名ワークフローを有効にすることができます。電子サインを使用すると、法務、販売、給与、人事管理など、様々な分野におけるドキュメント処理ワークフローが改善されます。

OSGi 上の一般的なAdobe SignおよびForms中心のワークフローシナリオでは、ユーザーがアダプティブフォームに入力してサービスの申し込みを行います。 例えば、クレジットカードの申込フォームや住民サービスフォームなどです。ユーザーが申込フォームに入力、送信、署名すると、承認/却下ワークフローが開始されます。 サービスプロバイダーは、AEMインボックスでアプリケーションを確認し、Adobe Signを使用してアプリケーションに電子署名します。 これに類似した電子署名ワークフローを有効にするには、Adobe Sign を AEM Forms に統合します。

AEM Forms で Adobe Sign を使用するには、「[Adobe Sign を AEM Forms に統合する](/help/forms/using/adobe-sign-integration-adaptive-forms.md)」を参照してください。

## 次の手順 {#next-steps}

OSGi 機能上でForms中心のワークフローを使用する環境を設定している。 現在は、この機能を使用するための手順は次のとおりです。

* [OSGi でのForms中心のワークフローの使用](/help/forms/using/aem-forms-workflow.md)
* [ワークフローステップのリファレンス](/help/sites-developing/workflows-step-ref.md)
* [レターとインタラクティブ通信の後処理](/help/forms/using/submit-letter-topostprocess.md)
