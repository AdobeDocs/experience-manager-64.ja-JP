---
title: セキュリティチェックリスト
seo-title: Security Checklist
description: AEM を設定およびデプロイする際の様々なセキュリティに関する考慮事項について説明します。
feature: Security
seo-description: Learn about the various security considerations when configuring and deploying AEM.
uuid: 8ecd0c35-249e-4f72-b7e9-97e72698b5c1
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.4/SITES
topic-tags: Security
content-type: reference
discoiquuid: a91e1264-8441-42f8-aa83-1d9c983d214a
exl-id: 0be6d031-f8b8-458b-a910-ff05d2b1a155
source-git-commit: c5b816d74c6f02f85476d16868844f39b4c47996
workflow-type: tm+mt
source-wordcount: '2866'
ht-degree: 89%

---

# セキュリティチェックリスト{#security-checklist}

>[!CAUTION]
>
>AEM 6.4 の拡張サポートは終了し、このドキュメントは更新されなくなりました。 詳細は、 [技術サポート期間](https://helpx.adobe.com/jp/support/programs/eol-matrix.html). サポートされているバージョンを見つける [ここ](https://experienceleague.adobe.com/docs/?lang=ja).

このセクションでは、デプロイ時に AEM のインストールが安全になるようにするために必要な様々な手順について説明します。このチェックリストは、上から順に適用するように設計されています。

>[!NOTE]
>
>その他の情報 [また、Open Web Application Security Project(OWASP) が発行した、最も危険なセキュリティ上の脅威に関する情報も入手できます](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

>[!NOTE]
>
>開発段階に適用されるその他の[セキュリティに関する考慮事項](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations)も参照してください。

## 主なセキュリティ対策 {#main-security-measures}

### 実稼動準備モードでの AEM の実行 {#run-aem-in-production-ready-mode}

詳しくは、「[実稼動準備モードでの AEM の実行](/help/sites-administering/production-ready.md)」を参照してください。

### トランスポート層のセキュリティのための HTTPS の有効化 {#enable-https-for-transport-layer-security}

インスタンスの安全を確保するには、オーサーインスタンスとパブリッシュインスタンスの両方の HTTPS トランスポート層を有効にする必要があります。

>[!NOTE]
>
>詳しくは、[HTTP over SSL の有効化](/help/sites-administering/ssl-by-default.md)を参照してください。

### セキュリティホットフィックスのインストール {#install-security-hotfixes}

最新の[アドビ提供のセキュリティホットフィックス](https://helpx.adobe.com/experience-manager/kb/aem63-available-hotfixes.html?lang=ja)がインストールされていることを確認してください。

### AEM および OSGi コンソールの管理者アカウントのデフォルトパスワードの変更 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

インストール後に、（すべてのインスタンスに対する）権限のある [**AEM** `admin`アカウント](#changing-the-aem-admin-password)のパスワードを変更することを強くお勧めします。

以下のアカウントが該当します。

* AEM `admin` アカウント

   AEM 管理者アカウントのパスワードを変更すると、CRX へのアクセス時には新しいパスワードを使用する必要があります。

* OSGi Web コンソールの `admin` パスワード

   この変更は、web コンソールへのアクセスに使用する admin アカウントにも適用されます。そのため、web コンソールへのアクセスの際にも同じパスワードを使用する必要があります。

これらの 2 つのアカウントは、個別の資格情報を使用する異なるアカウントです。デプロイメントをセキュリティで保護するには、それぞれに強力なパスワードを設定することが不可欠です。

#### AEM admin パスワードの変更 {#changing-the-aem-admin-password}

AEM 管理者アカウントのパスワードは、[Granite の操作 - ユーザー](/help/sites-administering/granite-user-group-admin.md)コンソールで変更できます。

このコンソールでは、`admin` アカウントの編集と[パスワードの変更](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)を行うことができます。

>[!NOTE]
>
>管理者アカウントを変更すると、OSGi web コンソールのアカウントも変更されます。管理者アカウントを変更したら、OSGi アカウントを別のアカウントに変更する必要があります。

#### OSGi web コンソールのパスワード変更の重要性 {#importance-of-changing-the-osgi-web-console-password}

AEM `admin` アカウントとは別に、OSGi web コンソールのデフォルトのパスワードを変更しない場合は、次の問題が発生する可能性があります。

* 起動時およびシャットダウン時にデフォルトのパスワードでサーバーが公開される（大規模なサーバーの場合は数分かかる場合があります）
* リポジトリがダウンまたはバンドルを再起動中で、OSGI を実行中に、サーバーが公開される

Web コンソールのパスワードの変更について詳しくは、「[OSGi web コンソールの管理者パスワードの変更](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password)」を参照してください。

#### OSGi web コンソールの管理者パスワードの変更 {#changing-the-osgi-web-console-admin-password}

Web コンソールへのアクセスに使用するパスワードの変更も必要です。そのためには、[Apache Felix OSGi Management Console](/help/sites-deploying/osgi-configuration-settings.md) の以下のプロパティを設定します。

**ユーザー名**&#x200B;と&#x200B;**パスワード**：Apache Felix web 管理コンソールにアクセスするための資格情報です。\
インスタンスのセキュリティを確保するには、最初のインストールの後にパスワードを変更する必要があります。

次の手順を実行します。

1. Web コンソール（`<server>:<port>/system/console/configMgr`）にアクセスします。
1. ** Apache Felix OSGi Management Console**に移動し、 **ユーザー名** および **パスワード**.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. 「**保存**」をクリックします。

### カスタムエラーハンドラーの実装 {#implement-custom-error-handler}

情報の開示を防ぐために、カスタムエラーハンドラーページ（特に 404 および 500 HTTP 応答コード）を定義することをお勧めします。

>[!NOTE]
>
>詳しくは、[カスタムスクリプトまたはエラーハンドラーの作成方法](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html)に関するナレッジベースの記事を参照してください。

### Dispatcher のセキュリティチェックリストの完了 {#complete-dispatcher-security-checklist}

AEM Dispatcher はインフラストラクチャの重要な部分です。[ Dispatcher のセキュリティチェックリスト](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=ja#getting-started)を確認することを強くお勧めします。

>[!CAUTION]
>
>Dispatcher を使用する場合は、「.form」セレクターを無効にする必要があります。

## 検証手順 {#verification-steps}

### レプリケーションの設定とユーザーのトランスポート {#configure-replication-and-transport-users}

AEM の標準インストールでは、`admin` をデフォルトの[レプリケーションエージェント](/help/sites-deploying/replication.md)内のトランスポート認証情報のユーザーとして指定します。また、管理者ユーザーは、オーサーシステムでレプリケーションを展開する際に使用します。

セキュリティに関する考慮事項については、次の 2 つの点を考慮して、特定の使用例がすぐに反映されるように両方を変更する必要があります。

* **トランスポートユーザー**&#x200B;は管理者ユーザーにしないでください。代わりに、公開システムの関連部分へのアクセス権のみを持つユーザーを公開システムに設定し、そのユーザーの認証情報をトランスポートに使用します。

   バンドルされたレプリケーション受信者ユーザーから開始し、状況に合わせてそのユーザーのアクセス権限を設定できます。

* **レプリケーションユーザー**&#x200B;または&#x200B;**エージェントユーザー ID** も admin 以外のユーザー（ただし、レプリケーションされるコンテンツの確認のみ可能なユーザー）にする必要があります。レプリケーションユーザーは、レプリケーション対象のコンテンツを、発行者に送信する前に作成者システムで収集するために使用します。

### 操作ダッシュボードのセキュリティヘルスチェックの確認 {#check-the-operations-dashboard-security-health-checks}

AEM 6 には、システムオペレーターが問題のトラブルシューティングやインスタンスの正常性の監視を行うための新しい操作ダッシュボードが導入されました。

このダッシュボードには、セキュリティヘルスチェックのコレクションも付属しています。実稼動インスタンスでの運用を開始する前に、すべてのセキュリティヘルスチェックのステータスを確認することをお勧めします。詳しくは、[操作ダッシュボードのドキュメント](/help/sites-administering/operations-dashboard.md)を参照してください。

### サンプルコンテンツが存在するかどうかを確認 {#check-if-example-content-is-present}

すべてのサンプルコンテンツとユーザー（Geometrixx プロジェクトとそのコンポーネントなど）は、公開してアクセスできるようにする前に、実稼働システムから完全にアンインストールして削除する必要があります。

>[!NOTE]
>
>このインスタンスが[実稼動準備モード](/help/sites-administering/production-ready.md)で実行されている場合、サンプルの We.Retail アプリケーションは削除されます。何らかの理由でサンプルコンテンツがアンインストールされていない場合は、パッケージマネージャーに移動し、すべての We.Retail パッケージを検索してアンインストールします。 詳しくは、 [パッケージの操作方法](package-manager.md).

### CRX 開発バンドルが存在するかどうかの確認 {#check-if-the-crx-development-bundles-are-present}

これらの開発用 OSGi バンドルは、アクセスできるようにする前に、オーサーとパブリッシュの両方の実稼働システムからアンインストールする必要があります。

* Adobe CRXDE サポート（com.adobe.granite.crxde-support）
* Adobe Granite CRX Explorer（com.adobe.granite.crx-explorer）
* Adobe Granite CRXDE Lite（com.adobe.granite.crxde-lite）

### Sling 開発バンドルが存在するかどうかの確認 {#check-if-the-sling-development-bundle-is-present}

この [AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) Apache Sling Tooling Support Install(org.apache.sling.tooling.support.install) をデプロイします。

この OSGi バンドルは、アクセスできるようにする前に、オーサーとパブリッシュの両方の実稼働システムからアンインストールする必要があります。

### クロスサイトリクエストフォージェリーからの保護 {#protect-against-cross-site-request-forgery}

#### CSRF 対策フレームワーク {#the-csrf-protection-framework}

AEM 6.1 には、クロスサイトリクエストフォージェリ攻撃 ( **CSRF 保護フレームワーク**. 使用方法について詳しくは、[ドキュメント](/help/sites-developing/csrf-protection.md)を参照してください。

#### Sling リファラーフィルター {#the-sling-referrer-filter}

CRX WebDAV および Apache Sling のクロスサイトリクエストフォージェリー（CSRF）に関する既知のセキュリティ問題に対処するには、リファラーフィルターの設定を追加して使用する必要があります。

リファラーフィルターサービスは、次の設定が可能な OSGi サービスです。

* どの http メソッドをフィルターするか
* 空のリファラーヘッダーを使用できるかどうか
* サーバーホスト以外に許可されるサーバーのリスト

   デフォルトでは、localhost のすべてのバリエーションおよびサーバーのバインド先の現在のホストの名前がリストに含まれます。

リファラーフィルターサービスを設定するには：

1. 次の場所で Apache Felix コンソール（**設定**）を開きます。

   `https://<server>:<port_number>/system/console/configMgr`

1. `admin` としてログインします。
1. **設定**&#x200B;メニューで、次の項目を選択します。

   `Apache Sling Referrer Filter`

1. 「`Allow Hosts`」フィールドに、リファラーとして許可するすべてのホストを入力します。各エントリは、

   &lt;protocol>://&lt;server>:&lt;port> の形式である必要があります。

   例：

   * `https://allowed.server:80` の場合、このサーバーからの指定ポートでの要求がすべて許可されます。
   * https 要求も許可する場合は、2 行目を入力する必要があります。
   * このサーバーからすべてのポートを許可する場合は、ポート番号として `0` を使用できます。

1. リファラーヘッダーが空の場合やない場合を許可するには、「`Allow Empty`」フィールドを選択します。

   >[!CAUTION]
   >
   >ご利用のシステムが CSRF 攻撃を受ける可能性があるため、`cURL` などのコマンドラインツールを使用する場合は、空の値を許可するのではなく、リファラーを指定することをお勧めします。

1. このフィルターが「`Filter Methods`」フィールドを使用してチェックする方法を編集します。

1. 「**保存**」をクリックして変更を保存します。

### OSGi 設定 {#osgi-settings}

アプリケーションのデバッグを容易にするために、一部の OSGi 設定はデフォルトで指定されています。パブリッシュとオーサーの実稼働インスタンスでは、これらを変更して、内部情報が公開されないようにする必要があります。

>[!NOTE]
>
>以下の設定はすべて（**Day CQ WCM デバッグフィルター**&#x200B;は除く）、[実稼動準備モード](/help/sites-administering/production-ready.md)で自動的にカバーされます。このため、インスタンスを実稼動環境にデプロイする前に、すべての設定を確認することをお勧めします。

次の各サービスに対して、指定した設定を変更する必要があります。

* [Adobe Granite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md):

   * 「**縮小**」を有効にして CRLF 文字と空白文字を削除する
   * 「**Gzip**」を有効にして、1 回のリクエストでファイルを gzip で圧縮してアクセスできるようにする。
   * 「**デバッグ**」を無効にする
   * 「**タイミング**」を無効にする

* [Day CQ WCM デバッグフィルター](/help/sites-deploying/osgi-configuration-settings.md)：

   * 「**有効**」の選択を解除

* [Day CQ WCM フィルター](/help/sites-deploying/osgi-configuration-settings.md)：

   * （パブリッシュインスタンスのみ）「**WCM モード**」を「無効」に設定

* [Apache Sling Java Script Handler](/help/sites-deploying/osgi-configuration-settings.md):

   * 「**デバッグ情報の生成**」を無効化

* [Apache Sling JSP スクリプトハンドラー](/help/sites-deploying/osgi-configuration-settings.md)：

   * 「**デバッグ情報の生成**」を無効化
   * 「**マッピングされたコンテンツ**」を無効化

詳しくは、「[OSGi 設定](/help/sites-deploying/osgi-configuration-settings.md)」を参照してください。

AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

## 参考情報 {#further-readings}

### サービス拒否（DoS）攻撃の軽減 {#mitigate-denial-of-service-dos-attacks}

サービス拒否（DoS）攻撃とは、意図したユーザーがコンピュータリソースを利用できない状態にする試みです。これは多くの場合、リソースをオーバーロードすることで実行されます。以下は例です。

* 外部ソースから大量のリクエストを発生させる。
* システムが正常に提供できないような大量の情報を要求される。

   例えば、リポジトリ全体の JSON 表現を要求されます。

* 無制限の個数の URL を含むコンテンツページを要求される。URL にはハンドル、何らかのセレクター、拡張子、サフィックスを含める場合があり、そのいずれかを変わる可能性があります。

   例えば、`.../en.html` は次のようにリクエストされる可能性があります。

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   有効なすべてのバリエーションがディスパッチャーによってキャッシュされ（例えば、`200` 応答を返し、キャッシュするように設定されている場合）、最終的にはファイルシステムがいっぱいになり、以降の要求に対してサービスを提供できなくなります。

このような攻撃を防ぐには、多くの設定ポイントがあります。ここでは、AEMに直接関係する設定についてのみ説明します。

**DoS を防ぐための Sling の設定**

Sling は *コンテンツ中心型* です。これは、各（HTTP）リクエストが JCR リソース（リポジトリーノード）の形でコンテンツにマッピングされるため、コンテンツに焦点を当てた処理が行われることを意味します。

* 最初のターゲットは、コンテンツを保持しているリソース（JCR ノード）です.
* 次に、リソースのプロパティを要求の特定の部分（例：セレクター、拡張子など）と組み合わせてレンダラー（スクリプト）が特定されます。

>[!NOTE]
>
>詳しくは、「[Sling リクエストの処理](/help/sites-developing/the-basics.md#sling-request-processing)」を参照してください。

このアプローチにより Sling は非常に強力で柔軟性が高くなりますが、柔軟性が高いことについては常に慎重に管理する必要があります。

DoS の悪用を防ぐ方法は次のとおりです。

1. アプリケーションレベルで制御を組み込みます。可能なバリエーションの数が多いので、デフォルト設定では実現できません。

   アプリケーションでは、次の操作を実行する必要があります。

   * アプリケーションのセレクターを制御して、必要とされる明示的なセレクター&#x200B;*のみ*&#x200B;提供し、他のすべてに対しては `404` を返します。
   * コンテンツノードを無制限に出力できないようにします。

1. 問題となる可能性のある、デフォルトのレンダラー設定を確認します。

   * 特に、ツリー構造が複数のレベルに及ぶ JSON レンダラーです。

      例えば、次のようなリクエストの場合、

      `http://localhost:4502/.json`

      リポジトリ全体を JSON 表現でダンプできてしまいます。これにより、サーバーで重大な問題が発生します。そのため、Sling では最大の結果数に制限を設定します。JSON レンダリングの深度を制限するには、次の値を設定できます。

      **JSON の最大結果数**（`json.maximumresults`）

      [Apache Sling GET サーブレット](/help/sites-deploying/osgi-configuration-settings.md)の設定で指定します。この制限を超えると、レンダリングが止まります。AEM 内での Sling 用のデフォルト値は `1000` です。

   * 予防策として、他のデフォルトレンダラー（HTML、プレーンテキスト、XML）を無効にします。ここでも、[Apache Sling GETサーブレット](/help/sites-deploying/osgi-configuration-settings.md)を設定します。
   >[!CAUTION]
   >
   >JSON レンダラーを無効にしないでください。これは AEM の通常処理に必要なレンダラーです。

1. ファイアウォールを使用して、インスタンスへのアクセスをフィルタリングします。

   * 保護しないままにした場合にサービス拒否攻撃につながる可能性があるインスタンスについては、オペレーティングシステムレベルのファイアウォールを使用して、インスタンスのポイントへのアクセスをフィルタリングする必要があります。

**フォームセレクターを使用することで生じる DoS に対する軽減策**

>[!NOTE]
>
>この軽減策は、Forms を使用していない AEM 環境でのみ実行してください。

AEM は `FormChooserServlet` 用の標準インデックスを提供していないため、クエリでフォームセレクターを使用すると、高コストのリポジトリトラバーサルが発生し、大抵の場合 AEM インスタンスが停止します。フォームセレクターは、クエリに文字列 **&amp;ast;.form.&amp;ast;** が含まれていれば検出されてしまいます。

これを軽減するには、次の手順に従ってください。

1. ブラウザーで *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr* を参照して、web コンソールに移動します

1. **Day CQ WCM Form 選択サーブレット**&#x200B;を検索します
1. エントリをクリックした後、次のウィンドウで「**詳細検索が必要**」を無効にします。

1. 「**保存**」をクリックします。

**アセットダウンロードサーブレットによって発生する DoS を軽減**

AEMのデフォルトのアセットダウンロードサーブレットを使用すると、認証済みユーザーは、任意の大きさの同時ダウンロードリクエストを発行して、サーバーやネットワークに負荷がかかる可能性のあるアセットの ZIP ファイルを作成できます。

この機能で生じる可能性のある DoS リスクを軽減するには、以下を実行します。 `AssetDownloadServlet` OSGi コンポーネントは、最新のAEMバージョンのパブリッシュインスタンスに対して、デフォルトで無効になっています。

設定でアセットダウンロードサーバーを有効にする必要がある場合は、 [この記事](/help/assets/download-assets-from-aem.md#disable-asset-download-servlet) を参照してください。

### WebDAV の無効化 {#disable-webdav}

WebDAV は、オーサー環境とパブリッシュ環境の両方で無効にする必要があります。これは、適切な OSGi バンドルを停止することで実行できます。

1. 以下で実行されている **Felix 管理コンソール**&#x200B;に接続します。

   `https://<*host*>:<*port*>/system/console`

   例えば、`http://localhost:4503/system/console/bundles` です。

1. バンドルのリストで、次の名前のバンドルを探します。

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. （「アクション」列にある）停止ボタンをクリックして、このバンドルを停止します。

1. 再び、バンドルのリストで、次の名前のバンドルを探します。

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 停止ボタンをクリックして、このバンドルを停止します。

   >[!NOTE]
   >
   >AEM の再起動は不要です。

### ユーザーのホームパスに個人を特定できる情報を公開していないことの確認 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

リポジトリユーザーのホームパスに個人が証明できる情報を公開しないようにすることで、ユーザーを保護することが重要です。

AEM 6.1 以降では、新しく実装された `AuthorizableNodeName` インターフェイスにより、ユーザー ID（または認証可能な ID）のノード名を保存する方法が変わりました。新しいインターフェイスでは、ノード名にユーザー ID が表示されなくなり、代わりにランダムな名前が生成されます。

この方法は AEM で認証できる ID を生成するデフォルトの方法になったので、この方法を有効にするための設定は不要です。

非推奨ですが、既存のアプリケーションとの下位互換性を保つために古い実装が必要な場合に備えて、無効にすることができます。 これを行うには、次の手順を実行する必要があります。

1. Web コンソールに移動して、**Apache Jackrabbit Oak SecurityProvider** のプロパティ **requiredServicePids** から org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName エントリを削除します。

   また、OSGi 設定の **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID を探すことで、Oak Security Provider を見つけることもできます。

1. Web コンソールから **Apache Jackrabbit Oak Random Authorizable Node Name** OSGi 設定を削除します。

   この設定の PID である **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** を検索すると、簡単に該当箇所が見つかります。

>[!NOTE]
>
>詳しくは、「[許可可能なノード名の生成](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html)」で Oak のドキュメントを参照してください。

### クリックジャッキングの防止 {#prevent-clickjacking}

クリックジャッキングを防ぐには、`SAMEORIGIN` に設定した HTTP ヘッダー `X-FRAME-OPTIONS` を指定するように web サーバーを設定することをお勧めします。

クリックジャッキングについて詳しくは、[OWASP のサイト](https://www.owasp.org/index.php/Clickjacking)を参照してください。

### 必要に応じて暗号化キーの適切なレプリケートを確認 {#make-sure-you-properly-replicate-encryption-keys-when-needed}

特定の AEM 機能および認証スキームでは、すべての AEM インスタンスに暗号化キーをレプリケートする必要があります。

キーの保存方法は 6.3 とそれ以前のバージョンでは異なるので、キーのレプリケーションはバージョン間で異なる方法で行われることに注意してください。

詳しくは以下を参照してください。

#### AEM 6.3 用のキーのレプリケート {#replicating-keys-for-aem}

以前のバージョンではレプリケーションキーがリポジトリに保存されていましたが、AEM 6.3 以降はファイルシステムに保存されます。

そのため、複数のインスタンスの全体でキーをレプリケートするには、ソースインスタンスからファイルシステム上のターゲットインスタンスの場所にキーをコピーする必要があります。

具体的には、次の操作が必要です。

1. コピーする鍵要素を含む AEM インスタンス（通常はオーサーインスタンス）にアクセスします。
1. ローカルファイルシステム内で、com.adobe.granite.crypto.file を見つけます。例えば、次のパスにあります。

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   各フォルダー内の `bundle.info` ファイルは、バンドル名を示します。 

1. データフォルダーに移動します。例：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. HMAC ファイルとマスターファイルをコピーします。
1. 次に、HMAC キーの複製先のターゲットインスタンスに移動し、データフォルダーにアクセスします。例：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 前の手順でコピーした 2 つのファイルを貼り付けます。
1. ターゲットインスタンスが既に実行されている場合は、[Crypto バンドルを更新](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle)します。
1. 鍵のレプリケーション先のすべてのインスタンスに対して上記の手順を繰り返します。

>[!NOTE]
>
>AEM を初めてインストールする際に以下のパラメーターを追加すると、6.3 より前のキーの保存方法に戻すことができます。
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### AEM 6.2 以前のバージョンでの鍵のレプリケーション {#replicating-keys-for-aem-and-older-versions}

AEM 6.2 以前のバージョンでは、鍵は `/etc/key` ノードの下のリポジトリに保存されます。

インスタンス間でキーを安全にレプリケートするには、このノードのみをレプリケートすることをお勧めします。ノードを選択してレプリケートするには、次の CRXDE Lite を使用します。

1. CRXDE Liteを開く ( *https://&lt;serrveraddress>:4502/crx/de/index.jsp*
1. `/etc/key` ノードを選択します。
1. 「**レプリケーション**」タブに移動します。
1. 「**レプリケーション**」ボタンをクリックします。

### 侵入テストの実施 {#perform-a-penetration-test}

実稼動に移行する前に、AEM インフラストラクチャの侵入テストを実施することを強くお勧めします。

### 開発のベストプラクティス {#development-best-practices}

新しい開発が [セキュリティのベストプラクティス](/help/sites-developing/security.md) AEM環境を安全に保つため。
