---
title: Document Security によって保護された PDF ドキュメントを AEM で検索可能にする
seo-title: Enable AEM to search document security protected PDF documents
description: 'ネイティブ AEM 検索を有効にし、DRM 保護された PDF ドキュメントで全テキストの検索を実行する方法について説明します。  '
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: c743cda3-252f-4c1f-8d94-e6d26d91dcd8
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: 759068fa-dc1b-4cf5-bc7b-62b8c5464831
feature: Document Security
exl-id: c405c69b-3588-4701-8f36-1ea0680e056d
source-git-commit: bd94d3949f0117aa3e1c9f0e84f7293a5d6b03b4
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 94%

---

# Document Security によって保護された PDF ドキュメントを AEM で検索可能にする {#enable-aem-to-search-document-security-protected-pdf-documents}

AEM 検索では、AEM アセットの検索と場所の特定をすることができます。また、プレーンテキストファイル、Microsoft Office ドキュメント、PDF ドキュメントなど、広く使用されているさまざまなドキュメント形式において、テキスト検索を実行することができます。ネイティブ検索を拡張し、[AEM Document Security で保護された PDF ドキュメント](/help/forms/using/admin-help/document-security.md)で全テキストの検索を実行することも可能です。このようなドキュメントで全テキストの検索を AEM で実行できるようにするには、次の手順を実行します。

1. 安全な接続の確立
1. サンプルポリシーで保護された PDF ドキュメントのインデックス作成

## 前提条件 {#prerequisites}

* OSGi 上で AEM Forms を使用している場合：

   * [AEM Forms Document Security Indexer パッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)を AEM Forms サーバーにインストールします。
   * JEE サーバー上で AEM Forms が起動して実行されていること、および Document Security が JEE サーバー上の対応する AEM Forms にインストールされていることを確認します。保護されたドキュメントのインデックスを作成するには、JEE サーバー上の AEM Form が必要です。

* JEE サーバー上で AEM Forms のみを使用している場合、Indexer パッケージはすでにインストールされています。
* すべてのバンドルが正常に実行していることを確認します。アクティブ状態になっていないバンドルが存在する場合は、すべてのバンドルが起動して実行されるまで待ちます。

   * OSGi 上のAEM Formsの場合、バンドルは次の場所にリストされます。 `https://[server]:[port]/system/console/bundles`.
   * JEE 上のAEM Formsの場合、バンドルは次の場所に一覧表示されます。 `https://[server]:[port]/[context-path]/system/console/bundles`. 例えば、`http://localhost:8080/lc/system/console/bundles` です。

* *sun.util.calendar* パッケージを許可リストに追加します。パッケージを許可リストに追加するには、次の手順を実行します。

   1. AEM web コンソールを開きます。URL は `https://[server]:[port]/system/console/configMgr` です。。
   1. **デシリアライゼーションファイアウォール設定**&#x200B;を探して開きます。
   1. sun.util.calendar パッケージを「ホワイトリストに登録されたクラスまたはパッケージのプレフィックス」フィールドに追加し、 **保存**.

## AEM Forms JEE と OSGi スタック間の安全な接続の確立 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

次のいずれかの方法を使用して安全な接続を確立します。

* JEE 上の AEM Forms の管理者資格情報を使用して Adobe LiveCycle Client SDK Bundle を設定します
* 相互認証を使用した Adobe LiveCycle Client SDK Bundle の設定

### JEE 上の AEM Forms の管理者資格情報を使用して Adobe LiveCycle Client SDK Bundle を設定します {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM web コンソールを開きます。URL は `https://[server]:[port]/system/console/configMgr` です。。
1. **Adobe LiveCycle Client SDK Bundle** を探して開きます。次の各フィールドの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の Forms のパス> のパラメータで AEM サーバーを再起動します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。
   * **ユーザー名**：AEM サーバーからの呼び出しの開始に使用される JEE 上の AEM Forms アカウントのユーザー名を指定します。指定したアカウントは、JEE サーバー上の AEM Forms で Document Services を開始することができる権限が付与されている必要があります。
   * **パスワード**：Username フィールドに表示される JEE 上の AEM Forms アカウントのパスワードを指定します。

   「**保存**」をクリックします。AEM は Document Security によって保護された PDF ドキュメントの検索が有効になっています。

### 相互認証を使用した Adobe LiveCycle Client SDK Bundle の設定 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. JEE 上の AEM Forms の相互認証を有効にします。詳しくは、「[CAC および相互認証](https://helpx.adobe.com/jp/livecycle/kb/cac-mutual-authentication.html)」を参照してください。
1. AEM web コンソールを開きます。URL は `https://[server]:[port]/system/console/configMgr` です。。
1. **Adobe LiveCycle Client SDK** Bundle を探して開きます。次の各プロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の AEM Forms のパス> のパラメータで AEM サーバーを再起動します。
   * **2way SSL の有効化**：「2way SSL の有効化」オプションを有効にします。
   * **キーストアファイル URL**：キーストアファイルの URL を指定します。
   * **TrustStore ファイル URL**：Truststore ファイルの URL を指定します.
   * **キーストアパスワード**：キーストアファイルのパスワードを指定します。
   * **TrustStore パスワード**：Truststore ファイルのパスワードを指定します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。

   「**保存**」をクリックします。AEM は Document Security によって保護された PDF ドキュメントの検索が有効になっています。

## サンプルポリシーで保護された PDF ドキュメントのインデックス作成 {#index-a-sample-policy-protected-pdf-document}

1. 管理者として AEM Assets にログインします。
1. AEM Digital Asset Manager でフォルダーを作成し、新しく作成したフォルダーにポリシーで保護された PDF ドキュメントをアップロードします。

   これで AEM 検索を使用してポリシーで保護されたドキュメントを検索できるようになりました。
