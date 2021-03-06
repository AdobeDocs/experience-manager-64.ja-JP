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
source-git-commit: b921cf3a1739b031eea5c319953d20a024515544
workflow-type: tm+mt
source-wordcount: '2830'
ht-degree: 86%

---

# セキュリティチェックリスト{#security-checklist}

ここでは、デプロイの際に AEM インストールのセキュリティを確保するために必要となる様々な手順について説明します。このチェックリストは、上から順に適用するように設計されています。

>[!NOTE]
>
>[Open Web Application Security Project（OWASP）で公開されている、最も危険性の高いセキュリティ上の脅威](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)についても確認できます。

>[!NOTE]
>
>開発段階に適用されるその他の[セキュリティに関する考慮事項](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations)も参照してください。

## 主なセキュリティ対策 {#main-security-measures}

### 実稼動準備モードでの AEM の実行 {#run-aem-in-production-ready-mode}

詳しくは、[実稼動準備モードでの AEM の実行](/help/sites-administering/production-ready.md)を参照してください。

### トランスポート層のセキュリティのための HTTPS の有効化 {#enable-https-for-transport-layer-security}

インスタンスの安全を確保するには、オーサーインスタンスとパブリッシュインスタンスの両方の HTTPS トランスポート層を有効にする必要があります。

>[!NOTE]
>
>詳しくは、[HTTP over SSL の有効化](/help/sites-administering/ssl-by-default.md)を参照してください。

### セキュリティホットフィックスのインストール {#install-security-hotfixes}

[アドビが提供する最新のセキュリティホットフィックス](https://helpx.adobe.com/jp/experience-manager/kb/aem63-available-hotfixes.html)がインストールされていることを確認してください。

### AEM および OSGi コンソールの admin アカウントのデフォルトパスワードの変更 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

インストール後に、（すべてのインスタンスに対する）権限のある [**AEM** `admin` アカウント](#changing-the-aem-admin-password)のパスワードを変更することを強くお勧めします。

以下のアカウントが該当します。

* AEM `admin` アカウント

   AEM admin アカウントのパスワードを変更したら、CRX にアクセスする際に新しいパスワードを使用する必要があります。

* この `admin` OSGi Web コンソールのパスワード

   この変更は、Web コンソールへのアクセスに使用する管理者アカウントにも適用されるので、アクセス時には同じパスワードを使用する必要があります。

これらの 2 つのアカウントは、個別の資格情報を使用する異なるアカウントです。デプロイメントをセキュリティで保護するには、それぞれに強力なパスワードを設定することが不可欠です。

#### AEM admin パスワードの変更 {#changing-the-aem-admin-password}

AEM の admin アカウントのパスワードは、[Granite の操作 - ユーザー](/help/sites-administering/granite-user-group-admin.md)コンソールで変更できます。

このコンソールでは、`admin` アカウントの編集と[パスワードの変更](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)をおこなうことができます。

>[!NOTE]
>
>admin アカウントを変更すると、OSGi Web コンソールのアカウントも変更されます。admin アカウントの変更後は、OSGi アカウントを変更してください。

#### OSGi Web コンソールのパスワード変更の重要性 {#importance-of-changing-the-osgi-web-console-password}

AEM `admin` アカウントとは別に、OSGi Web コンソールのデフォルトのパスワードを変更しない場合は、次の問題が発生する可能性があります。

* 起動／シャットダウン（大規模なサーバーでは数分かかる場合があります）時にデフォルトのパスワードを使用するサーバーのリスク
* リポジトリの停止／バンドルの再起動時（OSGi は実行されている場合）のサーバーのリスク

Web コンソールのパスワードの変更について詳しくは、以下の [OSGi Web コンソールの admin パスワードの変更](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password)を参照してください。

#### OSGi Web コンソールの admin パスワードの変更 {#changing-the-osgi-web-console-admin-password}

また、Web コンソールへのアクセスに使用するパスワードを変更する必要があります。これは、 [Apache Felix OSGi Management Console](/help/sites-deploying/osgi-configuration-settings.md):

**ユーザー名** および **パスワード**:Apache Felix Web Management Console にアクセスするための資格情報。\
インスタンスのセキュリティを確保するために、最初のインストール後にパスワードを変更する必要があります。

次の手順を実行します。

1. Web コンソール ( ) に移動します。 `<server>:<port>/system/console/configMgr`.
1. ** Apache Felix OSGi Management Console**に移動し、 **ユーザー名** および **パスワード**.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. 「**保存**」をクリックします。

### カスタムエラーハンドラーの実装 {#implement-custom-error-handler}

情報が開示されないようにするには、（404 および 500 HTTP 応答コード専用の）カスタムエラーハンドラーページを定義することをお勧めします。

>[!NOTE]
>
>詳しくは、[カスタムスクリプトまたはエラーハンドラーの作成方法](https://helpx.adobe.com/jp/experience-manager/kb/CustomErrorHandling.html)に関するナレッジベースの記事を参照してください。

### ディスパッチャーのセキュリティチェックリストの確認 {#complete-dispatcher-security-checklist}

AEM ディスパッチャーはインフラストラクチャの重要な部分です。[ディスパッチャーのセキュリティチェックリスト](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=ja#getting-started)を確認することを強くお勧めします。

>[!CAUTION]
>
>Dispatcher を使用して「.form」セレクターを無効にする必要があります。

## 検証手順 {#verification-steps}

### レプリケーションおよびトランスポートユーザーの設定 {#configure-replication-and-transport-users}

AEM の標準インストールでは、`admin` をデフォルトの[レプリケーションエージェント](/help/sites-deploying/replication.md)内のトランスポート資格情報のユーザーとして指定します。また、admin ユーザーはオーサーシステムでレプリケーションのソースを特定する場合にも使用されます。

セキュリティを考慮して、特定の使用事例に対応するように両方のユーザーを変更してください。その際の注意事項を次に示します。

* この **輸送利用者** 管理者ユーザーではない。代わりに、パブリッシュシステムの関連する部分に対するアクセス権のみを持つユーザーをパブリッシュシステム上に設定し、そのユーザーの資格情報をトランスポートに使用します。

   バンドルされたレプリケーション受信者ユーザーから開始し、状況に合わせてそのユーザーのアクセス権限を設定できます。


* **レプリケーションユーザー**&#x200B;または&#x200B;**エージェントユーザー ID** も admin 以外のユーザー（ただし、レプリケーションされるコンテンツの確認のみ可能なユーザー）にする必要があります。レプリケーションユーザーは、レプリケーション対象のコンテンツを、発行者に送信する前に作成者システムで収集するために使用します。


### 操作ダッシュボードのセキュリティヘルスチェックの確認 {#check-the-operations-dashboard-security-health-checks}

AEM 6 には新しく操作ダッシュボードが導入されています。このダッシュボードは、システムオペレーターが問題のトラブルシューティングやインスタンスのヘルスの監視をおこなうためのものです。

また、このダッシュボードには一連のセキュリティヘルスチェック機能が用意されています。実稼動インスタンスの運用を開始する前に、すべてのセキュリティヘルスチェックのステータスを確認しておくことをお勧めします。詳しくは、[操作ダッシュボードのドキュメント](/help/sites-administering/operations-dashboard.md)を参照してください。

### サンプルコンテンツが存在するかどうかの確認 {#check-if-example-content-is-present}

実稼動システムを公開する前に、そのシステム上のすべてのサンプルコンテンツ／ユーザー（Geometrixx プロジェクトやそのコンポーネントなど）を完全にアンインストールして削除しておく必要があります。

>[!NOTE]
>
>このインスタンスが[実稼動準備モード](/help/sites-administering/production-ready.md)で実行されている場合、サンプルの We.Retail アプリケーションは削除されます。何らかの理由でこれが当てはまらない場合は、パッケージマネージャーに移動して、すべての We.Retail パッケージを検索してアンインストールすることで、サンプルコンテンツをアンインストールできます。詳しくは、 [パッケージの操作方法](package-manager.md).

### CRX 開発バンドルが存在するかどうかの確認 {#check-if-the-crx-development-bundles-are-present}

実稼動のオーサーシステムとパブリッシュシステムへのアクセスを可能にする前に、それらの両方のシステムで、以下の開発用 OSGi バンドルをアンインストールしておく必要があります。

* Adobe CRXDE サポート（com.adobe.granite.crxde-support）
* Adobe Granite CRX Explorer（com.adobe.granite.crx-explorer）
* Adobe Granite CRXDE Lite（com.adobe.granite.crxde-lite）

### Sling 開発バンドルが存在するかどうかの確認 {#check-if-the-sling-development-bundle-is-present}

[AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) は Apache Sling Tooling Support Install（org.apache.sling.tooling.support.install）をデプロイします。

実稼動のオーサーシステムとパブリッシュシステムへのアクセスを可能にする前に、それらの両方のシステムで、この OSGi バンドルをアンインストールしておく必要があります。

### クロスサイトリクエストフォージェリからの保護 {#protect-against-cross-site-request-forgery}

#### CSRF 対策フレームワーク {#the-csrf-protection-framework}

AEM 6.1 には、クロスサイトリクエストフォージェリから保護する **CSRF 対策フレームワーク**&#x200B;と呼ばれるメカニズムが搭載されています。使用方法について詳しくは、[ドキュメント](/help/sites-developing/csrf-protection.md)を参照してください。

#### Sling Referrer Filter {#the-sling-referrer-filter}

CRX WebDAV および Apache Sling のクロスサイトリクエストフォージェリ（CSRF）に関する既存のセキュリティ問題に対応するには、リファラーフィルターを使用するために設定を追加する必要があります。

リファラーフィルターサービスは OSGi のサービスの 1 つであり、次の設定が可能です。

* フィルター処理する HTTP メソッド
* 空のリファラーヘッダーを使用できるかどうか
* と、サーバーホストに加えて許可されるサーバーのリスト。

   デフォルトでは、localhost のすべてのバリエーションと、サーバーがバインドされる現在のホスト名がリストに含まれます。

リファラーフィルターサービスを設定するには：

1. Apache Felix コンソール (**設定**):

   `https://<server>:<port_number>/system/console/configMgr`

1. ログイン名 `admin`.
1. **Configurations** メニューで、次の項目を選択します。

   `Apache Sling Referrer Filter`

1. 「`Allow Hosts`」フィールドに、リファラーとして許可するすべてのホストを入力します。各エントリは、フォームである必要があります

   &lt;protocol>://&lt;server>:&lt;port>

   次に例を示します。

   * `https://allowed.server:80`の場合、特定のポートを使用して、このサーバーからの要求がすべて許可されます。
   * https 要求も許可する場合は、2 行目を入力する必要があります。
   * このサーバーのすべてのポートを許可する場合は、ポート番号として `0` を使用できます。


1. 空の、または欠落しているリファラーヘッダーを許可する場合は、「`Allow Empty`」フィールドを選択します。

   >[!CAUTION]
   >
   >空の値を許可するのではなく `cURL` などのコマンドラインツールを使用する場合は、リファラーを指定することをお勧めします。これは、システムが CSRF 攻撃を受ける可能性があるためです。

1. 「`Filter Methods`」フィールドを使用して、このフィルターがチェックに使用する方法を編集します。


1. 「**保存**」をクリックして変更を保存します。

### OSGi 設定 {#osgi-settings}

一部の OSGi 設定は、アプリケーションのデバッグを容易におこなえるようにデフォルトで設定されます。実稼動のパブリッシュインスタンスとオーサーインスタンスでは、これらの設定を変更して、内部情報が公開されないようにする必要があります。

>[!NOTE]
>
>**Day CQ WCM Debug Filter** を除く以下のすべての設定は、自動的に[実稼動準備モード](/help/sites-administering/production-ready.md)の対象になります。このため、インスタンスを実稼動環境にデプロイする前にすべての設定を見直すことをお勧めします。

以下に示す各サービスについて、記載されている設定を変更してください。

* [Adobe Granite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md)：

   * 「**Minify**」を有効化（CRLF および空白文字を削除）
   * 「**Gzip**」を有効化（1 回の要求でファイルを gzip してアクセスするため）
   * 「**Debug**」を無効化
   * 「**Timing**」を無効化

* [Day CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md):

   * 「**Enable**」を選択解除

* [Day CQ WCM Filter](/help/sites-deploying/osgi-configuration-settings.md)：

   * （パブリッシュインスタンスのみ）「**WCM Mode**」を「disabled」に設定

* [Apache Sling Java Script Handler](/help/sites-deploying/osgi-configuration-settings.md)：

   * 「**Generate Debug Info**」を無効化

* [Apache Sling JSP Script Handler](/help/sites-deploying/osgi-configuration-settings.md):

   * 「**Generate Debug Info**」を無効化
   * **Mapped Content**

詳しくは、[OSGi 設定](/help/sites-deploying/osgi-configuration-settings.md)を参照してください。

AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

## 追加情報 {#further-readings}

### サービス拒否（DoS）攻撃の軽減 {#mitigate-denial-of-service-dos-attacks}

サービス拒否（DoS）攻撃は、対象となるユーザーがコンピューターリソースを使用できない状態にするものです。多くの場合、この攻撃ではリソースを過負荷状態にします。次に例を示します。

* 外部のソースから大量の要求を送信する。
* システムが正常に提供可能な量を超える情報を要求する。

   例えば、リポジトリ全体の JSON 表現を要求します。

* 無制限の数の URL を含むコンテンツページを要求する。URL にはハンドル、複数のセレクター、拡張子およびサフィックスを含めることができます。それらのいずれかを変更できます。

   例： `.../en.html` また、次のようにリクエストすることもできます。

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   有効なすべてのバリエーション（例えば、`200` という応答が返され、バリエーションをキャッシュするように設定されている場合）がディスパッチャーによってキャッシュされるので、最終的にはファイルシステムがいっぱいになり、以降の要求に対してサービスを提供できなくなります。

このような攻撃を防ぐための設定のポイントは多数ありますが、ここでは AEM に直接関連する設定についてのみ説明します。

**DoS を防ぐための Sling の設定**

Sling はコンテンツ中心型です&#x200B;*。*&#x200B;つまり、（HTTP）要求がそれぞれ JCR リソース（リポジトリーノード）の形式でコンテンツにマップされるので、コンテンツに焦点を当てた処理が行われるということです。

* 最初のターゲットは、コンテンツを保持しているリソース（JCR ノード）です。。
* 次に、リソースのプロパティを要求の特定の部分（例：セレクター、拡張子など）と組み合わせてレンダラー（スクリプト）が特定されます。

>[!NOTE]
>
>詳しくは、[Sling の要求処理](/help/sites-developing/the-basics.md#sling-request-processing)を参照してください。

このアプローチにより Sling が強化され、柔軟性も向上しますが、これまでどおり柔軟性の管理には注意が必要です。

DoS の悪用を防ぐ方法は次のとおりです。

1. アプリケーションレベルで制御を組み込みます。バリエーションの数が原因で、デフォルト設定が適していない可能性があります。

   アプリケーションで必要な処理は次のとおりです。

   * **&#x200B;アプリケーションのセレクターを制御して、必要とされる明示的なセレクターのみ提供し、他のすべてに対しては `404`   を返します。
   * コンテンツノードの出力が無制限に大量におこなわれないようにします。

1. 問題点となっている可能性のあるデフォルトのレンダラーの設定を確認します。

   * 具体的には、ツリー構造が複数のレベルに及ぶ JSON レンダラーです。

      例えば、次のリクエストがあります。

      `http://localhost:4502/.json`

      は、JSON 表現でリポジトリ全体をダンプできませんでした。 これにより、サーバーで重大な問題が発生します。そのため、Sling では結果の最大数に制限を設定します。JSON レンダリングの深さを制限するには、次の値を設定します。

      **JSON の最大結果数** ( `json.maximumresults`)

      を [Apache SlingGETサーブレット](/help/sites-deploying/osgi-configuration-settings.md). この制限を超えると、レンダリングは行われません。AEM 内での Sling 用のデフォルト値は `1000` です。

   * 予防策として、デフォルトの他のレンダラー（HTML、プレーンテキスト、XML）を無効にします。この場合も [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md) を設定します。
   >[!CAUTION]
   >
   >JSON レンダラーを無効にしないでください。これは AEM の通常の処理に必要なレンダラーです。

1. ファイアウォールを使用してインスタンスへのアクセスをフィルタリングします。

   * 保護のない状態ではサービス拒否攻撃を受ける恐れがあるので、オペレーティングシステムレベルのファイアウォールを使用してインスタンスへのアクセスをフィルタリングする必要があります。

**フォームセレクターを使用することで生じる DoS を軽減**

>[!NOTE]
>
>この軽減策は、Forms を使用していない AEM 環境でのみ実行するべきです。

AEM は `FormChooserServlet` 用の標準インデックスを提供していないため、クエリでフォームセレクターを使用すると、高コストのリポジトリートラバーサルが発生し、大抵の場合 AEM インスタンスが停止します。フォームセレクターは、 **&amp;ast;.form.&amp;ast;** 文字列をクエリに含めます。

これを軽減するために、以下の手順に従ってください。

1. ブラウザーで *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. **Day CQ WCM Form Chooser Servlet** を検索します。
1. エントリをクリックした後、次のウィンドウで「**Advanced Search Require**」を無効にします。

1. 「**保存**」をクリックします。

**アセットダウンロードサーブレット使用することで生じる DoS を軽減**

AEM のデフォルトアセットダウンロードサーブレットを使用すると、認証されたユーザーは、表示可能なアセットの ZIP ファイルを作成するために任意のサイズの同時ダウンロード要求を発行することができますが、その結果、サーバーやネットワークに過剰な負荷をかけるおそれがあります。

この機能で生じる可能性がある DoS リスクを軽減するために、最新の AEM バージョンでは、パブリッシュインスタンスに対して、`AssetDownloadServlet` OSGi コンポーネントがデフォルトで無効になっています。

セットアップでアセットダウンロードサーブレットを有効にする必要がある場合、詳細については[この記事](/help/assets/download-assets-from-aem.md#disable-asset-download-servlet)をご覧ください。

### WebDAV の無効化 {#disable-webdav}

WebDAV は、オーサリングとパブリッシュの両方の環境で無効にする必要があります。そのためには、適切な OSGi バンドルを停止します。

1. **Felix Management Console** に接続します。

   `https://<*host*>:<*port*>/system/console`

   例えば、`http://localhost:4503/system/console/bundles` のように指定します。

1. バンドルのリストで、次の名前のバンドルを探します。

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. （「Actions」列にある）停止ボタンをクリックして、このバンドルを停止します。

1. 再び、バンドルのリストで、次の名前のバンドルを探します。

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 停止ボタンをクリックして、このバンドルを停止します。

   >[!NOTE]
   >
   >AEM の再起動は不要です。

### ユーザーのホームパスに個人を特定できる情報を公開していないことの確認 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

ユーザーの保護に重要なのは、リポジトリユーザーのホームパスに個人を特定できる情報を公開しないことです。

AEM 6.1 以降では、新しく実装された `AuthorizableNodeName` インターフェイスにより、ユーザー ID（または許可可能 ID）のノード名を保存する方法が変わりました。新しいインターフェイスでは、ノード名にユーザー ID を表示する代わりに、ランダムな名前を生成します。

これは現在は AEM で許可可能 ID を生成するデフォルトの方法なので、これを有効にするために設定を変更する必要はありません。

推奨されませんが、既存のアプリケーションとの後方互換性確保のために以前の実装が必要な場合は、この機能を無効にすることもできます。これをおこなうには、次の手順を実行する必要があります。

1. Web コンソールに移動し、プロパティから** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**エントリを削除します。 **requiredServicePids** in **Apache Jackrabbit Oak SecurityProvider**.

   また、OSGi 設定の **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID を探すことで、Oak Security Provider を見つけることもできます。

1. Web コンソールから **Apache Jackrabbit Oak Random Authorizable Node Name** OSGi 設定を削除します。

   この設定の PID である **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** を検索すると、簡単に該当箇所が見つかります。

>[!NOTE]
>
>詳しくは、「Oak Documentation」の[Authorizable Node Name Generation（英語）](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html)を参照してください。

### クリックジャッキングの防止 {#prevent-clickjacking}

クリックジャッキングを防ぐには、`SAMEORIGIN` に設定した HTTP ヘッダー `X-FRAME-OPTIONS` を指定するように Web サーバーを設定することをお勧めします。

詳細 [クリックジャッキングに関する情報は、 OWASP のサイトを参照してください。](https://www.owasp.org/index.php/Clickjacking).

### 必要な場合は暗号鍵を適切にレプリケーションする {#make-sure-you-properly-replicate-encryption-keys-when-needed}

特定の AEM 機能および認証スキームでは、すべての AEM インスタンスに暗号鍵をレプリケーションする必要があります。

これをおこなう前に、6.3 とそれ以前のバージョンでは鍵を保存する方法が異なるので、鍵のレプリケーションはバージョン間で異なることに注意してください。

詳しくは、以下を参照してください。

#### AEM 6.3 での鍵のレプリケーション {#replicating-keys-for-aem}

以前のバージョンではレプリケーション鍵はリポジトリに保存されましたが、AEM 6.3 からはファイルシステム上に保存されます。

したがって、インスタンス間で鍵をレプリケーションするには、ソースインスタンスからターゲットインスタンスのファイルシステム上の場所に鍵をコピーする必要があります。

具体的には、以下をおこなう必要があります。

1. コピーする鍵要素を含む AEM インスタンス（通常はオーサーインスタンス）にアクセスします。
1. ローカルファイルシステム内で、com.adobe.granite.crypto.file を見つけます。例えば、次のパスにあります。

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   各フォルダー内の `bundle.info` ファイルは、バンドル名を示します。 

1. データフォルダーに移動します。次に例を示します。

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. HMAC とマスターファイルをコピーします。
1. 次に、HMAC 鍵の複製先となるターゲットインスタンスにアクセスし、データフォルダーに移動します。次に例を示します。

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 前の手順でコピーした 2 つのファイルを貼り付けます。
1. ターゲットインスタンスが既に実行されている場合は、[Crypto バンドルを更新](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle)します。
1. 鍵のレプリケーション先のすべてのインスタンスに対して上記の手順を繰り返します。

>[!NOTE]
>
>最初に AEM をインストールするときに次のパラメーターを追加することによって、6.3 よりも前の鍵の保存方法に戻すことができます。
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### AEM 6.2 以前のバージョンでの鍵のレプリケーション {#replicating-keys-for-aem-and-older-versions}

AEM 6.2 以前のバージョンでは、キーは、 `/etc/key` ノード。

インスタンス全体で鍵を安全にレプリケーションするために推奨される方法は、このノードのみをレプリケーションすることです。CRXDE Lite によって、ノードを選択してレプリケーションできます。

1. CRXDE Liteを開く ( *https://&lt;serrveraddress>:4502/crx/de/index.jsp*
1. を選択します。 `/etc/key` ノード。
1. 「**レプリケーション**」タブに移動します。
1. 「**レプリケーション**」ボタンを押します。

### 侵入テストの実施 {#perform-a-penetration-test}

実稼動に移行する前に、AEM インフラストラクチャの侵入テストを実施することを強くお勧めします。

### 開発のベストプラクティス {#development-best-practices}

AEM 環境の安全を確保するには、新規開発において[セキュリティのベストプラクティス](/help/sites-developing/security.md)に従うことが重要です。
